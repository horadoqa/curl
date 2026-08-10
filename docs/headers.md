## Adicionando Cabeçalhos (Headers)

Os **headers (cabeçalhos)** são informações adicionais enviadas junto com uma requisição HTTP. Eles são utilizados para fornecer instruções ou informações ao servidor sobre a requisição.

No **cURL**, podemos adicionar um cabeçalho utilizando a opção **`-H`** (`--header`).

### Exemplo

```bash
curl -X GET https://api.exemplo.com/usuarios \
-H "Authorization: Bearer <token>"
```

Nesse exemplo, estamos enviando o seguinte header:

```http
Authorization: Bearer <token>
```

Esse cabeçalho é utilizado para **autenticar o cliente** em APIs que exigem um token de acesso.

### Entendendo o header

O header possui duas partes principais:

```text
Authorization: Bearer <token>
```

* **`Authorization`**: nome do cabeçalho utilizado para enviar as credenciais de autenticação.
* **`Bearer`**: indica o tipo de autenticação utilizado.
* **`<token>`**: representa o token de acesso fornecido pela API.

Na prática, o `<token>` deve ser substituído pelo token real:

```bash
curl -X GET https://api.exemplo.com/usuarios \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIs..."
```

O servidor pode utilizar esse token para verificar se o cliente possui permissão para acessar determinado recurso.

### Outros exemplos de Headers

Além do `Authorization`, podemos enviar diversos outros cabeçalhos.

Por exemplo, para informar que estamos enviando dados em JSON:

```bash
-H "Content-Type: application/json"
```

Ou para informar que esperamos receber uma resposta em JSON:

```bash
-H "Accept: application/json"
```

Também podemos enviar vários headers na mesma requisição:

```bash
curl -X POST https://api.exemplo.com/usuarios \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-H "Authorization: Bearer <token>" \
-d '{
    "nome": "Hora do QA",
    "email": "horadoqa@email.com"
}'
```

### Resumindo

A opção:

```bash
-H "Nome-Do-Header: valor"
```

permite adicionar um cabeçalho à requisição.

Os headers são muito utilizados para:

* **Autenticação e autorização** — `Authorization`
* **Informar o formato dos dados enviados** — `Content-Type`
* **Informar o formato esperado da resposta** — `Accept`
* **Enviar outras informações necessárias para a API**

> **Header = informação adicional enviada junto com a requisição HTTP.**
