# Exemplo de Login com o ServeRest

No ServeRest, podemos realizar a **autenticação de um usuário** por meio do endpoint `/login`.

Para isso, utilizamos uma requisição **POST**, enviando o e-mail e a senha do usuário no corpo da requisição, em formato JSON.

### Requisição

```bash
curl -X POST https://serverest.dev/login \
-H "Content-Type: application/json" \
-d '{
    "email": "hordoqa@email.com",
    "password": "1q2w3e4r"
}'
```

### Entendendo a requisição

* **`-X POST`** — define o método HTTP como **POST**.
* **`https://serverest.dev/login`** — é o endpoint responsável pelo login.
* **`Content-Type: application/json`** — informa ao servidor que os dados enviados estão no formato JSON.
* **`-d '{...}'`** — define o corpo da requisição, contendo as credenciais do usuário.

O JSON enviado contém:

```json t0cx5v"
{
    "email": "hordoqa@email.com",
    "password": "1q2w3e4r"
}
```

O servidor utiliza essas informações para **validar as credenciais do usuário**.

### Resposta de sucesso

Quando o e-mail e a senha estão corretos, o ServeRest retorna uma resposta contendo uma mensagem de sucesso e um **token de autenticação**:

```json 6m5v3p"
{
    "message": "Login realizado com sucesso",
    "authorization": "Bearer eyJhbGciOiJIUzI1NiIs..."
}
```

Esse token poderá ser utilizado posteriormente para acessar endpoints que exigem autenticação.

Por exemplo:

```bash q8y2ks"
curl -X GET https://serverest.dev/usuarios \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIs..."
```

> **Fluxo de autenticação:** primeiro realizamos o login → recebemos o token → enviamos o token no header `Authorization` nas requisições protegidas.
