Sim. Eu faria isso em duas partes:

1. O script gera um **relatório em formato JUnit XML**, que o GitHub Actions consegue publicar.
2. Um segundo step roda **somente se o teste falhar** e envia uma notificação.

Uma opção simples e bastante usada é **Slack** via webhook. Para isso, você cria um `SLACK_WEBHOOK_URL` em **GitHub Secrets**.

### 1. Workflow completo

```yaml
name: Teste de API - ServeRest

on:
  # Todos os dias às 09:00 no horário de Brasília (12:00 UTC)
  schedule:
    - cron: "0 12 * * *"

  # Permite execução manual
  workflow_dispatch:

jobs:

  # ==========================================
  # TESTE DA API
  # ==========================================

  api-test:
    name: Teste CRUD - ServeRest
    runs-on: ubuntu-latest

    steps:

      # ------------------------------------------
      # Checkout
      # ------------------------------------------

      - name: Checkout do código
        uses: actions/checkout@v4

      # ------------------------------------------
      # Instalar dependências
      # ------------------------------------------

      - name: Instalar jq
        run: |
          sudo apt-get update
          sudo apt-get install -y jq

      # ------------------------------------------
      # Permissão do script
      # ------------------------------------------

      - name: Dar permissão ao script
        run: chmod +x ./teste-crud.sh

      # ------------------------------------------
      # Executar teste
      # ------------------------------------------

      - name: Executar testes CRUD
        id: api_test
        continue-on-error: true
        run: ./teste-crud.sh

      # ------------------------------------------
      # Gerar relatório
      # ------------------------------------------

      - name: Gerar relatório JUnit
        if: always()
        run: |
          mkdir -p reports

          if [ "${{ steps.api_test.outcome }}" = "success" ]; then
            cat > reports/api-test.xml <<'EOF'
          <?xml version="1.0" encoding="UTF-8"?>
          <testsuite name="ServeRest API" tests="1" failures="0">
            <testcase
              classname="ServeRest"
              name="CRUD de usuários"/>
          </testsuite>
          EOF
          else
            cat > reports/api-test.xml <<'EOF'
          <?xml version="1.0" encoding="UTF-8"?>
          <testsuite name="ServeRest API" tests="1" failures="1">
            <testcase
              classname="ServeRest"
              name="CRUD de usuários">
              <failure message="Falha durante a execução do CRUD">
                O teste da API falhou. Consulte os logs do GitHub Actions.
              </failure>
            </testcase>
          </testsuite>
          EOF
          fi

      # ------------------------------------------
      # Publicar relatório
      # ------------------------------------------

      - name: Publicar relatório de testes
        if: always()
        uses: dorny/test-reporter@v2
        with:
          name: Relatório ServeRest
          path: reports/api-test.xml
          reporter: java-junit

      # ------------------------------------------
      # Upload do relatório como artefato
      # ------------------------------------------

      - name: Salvar relatório
        if: always()
        uses: actions/upload-artifact@v4
        with:
          name: relatorio-api
          path: reports/api-test.xml

      # ------------------------------------------
      # Falha do teste
      # ------------------------------------------

      - name: Falhar workflow se API falhar
        if: steps.api_test.outcome == 'failure'
        run: |
          echo "❌ Os testes da API falharam."
          exit 1

  # ==========================================
  # NOTIFICAÇÃO
  # ==========================================

  notify:
    name: Notificar falha
    needs: api-test
    if: needs.api-test.result == 'failure'
    runs-on: ubuntu-latest

    steps:

      - name: Enviar alerta para Slack
        uses: slackapi/slack-github-action@v2.1.1
        with:
          webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
          webhook-type: incoming-webhook
          payload: |
            {
              "text": "🚨 FALHA NO TESTE DA API",
              "blocks": [
                {
                  "type": "header",
                  "text": {
                    "type": "plain_text",
                    "text": "🚨 Falha no teste da API"
                  }
                },
                {
                  "type": "section",
                  "fields": [
                    {
                      "type": "mrkdwn",
                      "text": "*Projeto:*\n${{ github.repository }}"
                    },
                    {
                      "type": "mrkdwn",
                      "text": "*Workflow:*\n${{ github.workflow }}"
                    },
                    {
                      "type": "mrkdwn",
                      "text": "*Branch:*\n${{ github.ref_name }}"
                    },
                    {
                      "type": "mrkdwn",
                      "text": "*Execução:*\n#${{ github.run_number }}"
                    }
                  ]
                },
                {
                  "type": "section",
                  "text": {
                    "type": "mrkdwn",
                    "text": "O teste diário do CRUD da API ServeRest apresentou falha."
                  }
                },
                {
                  "type": "actions",
                  "elements": [
                    {
                      "type": "button",
                      "text": {
                        "type": "plain_text",
                        "text": "Ver execução"
                      },
                      "url": "https://github.com/${{ github.repository }}/actions/runs/${{ github.run_id }}"
                    }
                  ]
                }
              ]
            }
```

### 2. Criar o Secret

No GitHub, entre no seu repositório:

**Settings → Secrets and variables → Actions → New repository secret**

Crie:

```text
Nome:
SLACK_WEBHOOK_URL

Valor:
URL do seu Webhook do Slack
```

O workflow acessa o valor através de:

```yaml
${{ secrets.SLACK_WEBHOOK_URL }}
```

Assim o webhook **não fica exposto no código do repositório**.

### 3. O que acontece quando o teste roda

**Cenário de sucesso:**

```text
09:00
  │
  ▼
GitHub Actions
  │
  ▼
Health Check → 200 ✅
  │
  ▼
POST → 201 ✅
  │
  ▼
GET → 200 ✅
  │
  ▼
PUT → 200 ✅
  │
  ▼
GET → 200 ✅
  │
  ▼
DELETE → 200 ✅
  │
  ▼
GET → 400 ✅
  │
  ▼
📊 Relatório
  │
  ▼
✅ Workflow SUCCESS
```

**Cenário de falha:**

```text
09:00
  │
  ▼
GitHub Actions
  │
  ▼
Health Check → 200 ✅
  │
  ▼
POST → 201 ✅
  │
  ▼
GET → 500 ❌
  │
  ▼
exit 1
  │
  ├──────────────► 📊 Relatório de falha
  │
  ▼
Workflow FAILED
  │
  ▼
🚨 Slack
  │
  ▼
"Falha no teste da API"
```

### Uma melhoria que eu recomendo

No estado atual, o relatório JUnit informa **que o CRUD falhou**, mas não exatamente **qual Status Code provocou a falha**.

Como seu script já sabe algo como:

```text
READ reprovado - Status Code: 500
Esperado: 200
```

podemos evoluir o `teste-crud.sh` para gerar o próprio relatório com informações como:

```text
Suite: ServeRest API

Health Check       PASS    200
CREATE             PASS    201
READ               FAIL    500
UPDATE             SKIPPED
DELETE             SKIPPED

Resultado: FAILED
```

Isso deixaria o projeto bem mais próximo de uma estrutura de **automação de testes de API profissional**, com **execução agendada + validação + relatório + artefato + notificação de falha**.
