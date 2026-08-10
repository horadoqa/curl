# UPDATE — PUT Request

A requisição **PUT** é utilizada para **atualizar os dados de um recurso que já existe no servidor**.

No ServeRest, para atualizar um usuário, utilizamos a seguinte rota:

```http
PUT https://serverest.dev/usuarios/{_id}
```

O **`_id`** identifica qual usuário será atualizado. Ele deve ser informado diretamente na URL da requisição.

### Exemplo

```bash
curl -X PUT https://serverest.dev/usuarios/7tS9K8NxabeHLEtk \
-H "Content-Type: application/json" \
-d '{
    "nome": "Hora do QA",
    "email": "horadoqa@exemplo.com",
    "password": "1q2w3e4r",
    "administrador": "true"
}'
```

Nesse exemplo, estamos enviando uma requisição **PUT** para atualizar o usuário cujo `_id` é:

```text
7tS9K8NxabeHLEtk
```

Os novos dados do usuário são enviados no **body da requisição**, no formato JSON:

```json
{
    "nome": "Hora do QA",
    "email": "horadoqa@exemplo.com",
    "password": "1q2w3e4r",
    "administrador": "true"
}
```

> **Importante:** o `_id` não é enviado no body. Ele é informado na própria URL para indicar qual registro deve ser atualizado.

### Resposta de sucesso

Se o usuário for encontrado e a atualização for realizada com sucesso, o ServeRest retorna:

```json
{
    "message": "Registro alterado com sucesso"
}
```

### Resumindo

O fluxo de uma atualização com **PUT** é:

1. Informamos o método **PUT**.
2. Passamos o **`_id` do usuário na URL**.
3. Enviamos os novos dados no **body**, em JSON.
4. O servidor localiza o usuário pelo `_id` e atualiza seus dados.
5. Em caso de sucesso, recebemos a mensagem **"Registro alterado com sucesso"**.
