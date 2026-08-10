# Autenticação com cURL

Algumas APIs exigem que o cliente esteja **autenticado** antes de permitir o acesso a determinados recursos.

O cURL permite enviar informações de autenticação de diferentes formas. Duas das mais comuns são:

* **Basic Authentication**
* **Bearer Token**

---

## 4.1. Autenticação Basic

Na autenticação **Basic**, o usuário e a senha são enviados por meio do header `Authorization`.

No cURL, podemos utilizar a opção **`-u`** (`--user`) para informar as credenciais:

```bash
curl -u usuario:senha https://api.exemplo.com/usuarios
```

O cURL transforma essas credenciais no formato utilizado pelo protocolo HTTP e envia um header semelhante a:

```http
Authorization: Basic <credenciais>
```

Por exemplo:

```bash
curl -u joao:123456 https://api.exemplo.com/usuarios
```

> **Importante:** a autenticação Basic não significa que o usuário e a senha sejam enviados de forma segura por si só. Em aplicações reais, a comunicação deve utilizar **HTTPS** para proteger as credenciais durante o transporte.

---

## 4.2. Autenticação Bearer Token

Outra forma muito comum de autenticação é o uso de um **Bearer Token**.

Nesse modelo, o cliente primeiro obtém um token, normalmente por meio de um endpoint de login. Depois, esse token é enviado nas requisições que exigem autenticação.

O token é enviado no header:

```http
Authorization: Bearer <token>
```

No cURL:

```bash
curl -H "Authorization: Bearer <token>" \
https://api.exemplo.com/usuarios
```

Nesse exemplo:

* **`Authorization`**: é o nome do header utilizado para autenticação.
* **`Bearer`**: indica o tipo de credencial utilizada.
* **`<token>`**: representa o token de acesso fornecido pela API.

### Fluxo de autenticação

De forma simplificada, podemos representar o processo assim:

```text
1. Enviar usuário e senha
          ↓
2. API valida as credenciais
          ↓
3. API retorna um token
          ↓
4. Cliente envia o token nas próximas requisições
          ↓
5. API valida o token e permite o acesso
```

---

# Exemplo com o ServeRest

No ServeRest, podemos realizar o login enviando as credenciais para o endpoint de autenticação:

```bash
curl -X POST https://serverest.dev/login \
-H "Content-Type: application/json" \
-d '{
    "email": "hordoqa@email.com",
    "password": "1q2w3e4r"
}'
```

Se as credenciais forem válidas, a API retorna um token que poderá ser utilizado em requisições que exigem autenticação.

Depois de obter o token, podemos enviá-lo utilizando o header `Authorization`:

```bash
curl -X GET https://serverest.dev/usuarios \
-H "Authorization: Bearer <token>"
```

Substitua **`<token>`** pelo token retornado pela API.

---

# Exemplo Completo de Requisição com cURL

Agora podemos combinar vários conceitos que aprendemos até aqui: **POST, JSON, headers e autenticação com Bearer Token**.

```bash 2h7mcd"
curl -X POST https://serverest.dev/produtos \
-H "Content-Type: application/json" \
-H "Authorization: Bearer <token>" \
-d '{
    "nome": "Produto de teste",
    "preco": 100,
    "descricao": "Produto criado utilizando cURL",
    "quantidade": 10
}'
```

Nesse comando:

1. **`-X POST`** — define o método HTTP como **POST**.
2. **`Content-Type: application/json`** — informa que os dados enviados estão no formato **JSON**.
3. **`Authorization: Bearer <token>`** — envia o token utilizado para autenticação.
4. **`-d '{...}'`** — define o **body da requisição**, contendo os dados do produto.
5. **`https://serverest.dev/produtos`** — é o endpoint utilizado para criar o produto.

> **Resumo:** em uma API que utiliza Bearer Token, o processo normalmente consiste em **fazer login, obter o token e enviá-lo no header `Authorization` nas requisições protegidas**.
