# READ — GET Request

A requisição **GET** é utilizada para **consultar ou obter dados de um servidor**.

No ServeRest, podemos utilizar o método GET para consultar usuários, produtos e carrinhos, tanto para obter uma lista de registros quanto para buscar um registro específico pelo seu **`_id`**.

---

## Consultar Usuários

### Obter lista de usuários

Para consultar todos os usuários cadastrados, podemos utilizar:

```bash
curl https://serverest.dev/usuarios
```

Nesse caso, o **cURL utiliza o método GET automaticamente**, pois esse é o método padrão quando nenhum outro é especificado.

### Especificando o método GET

Também podemos informar explicitamente que queremos utilizar o método GET:

```bash
curl -X GET https://serverest.dev/usuarios \
-H "accept: application/json"
```

### Entendendo a requisição

* **`-X GET`**: define explicitamente o método HTTP como **GET**. No primeiro exemplo, essa opção não é necessária porque GET já é o método padrão do cURL.
* **`-H "accept: application/json"`**: adiciona um cabeçalho `Accept`, informando que o cliente espera receber a resposta no formato **JSON**.
* **`/usuarios`**: endpoint utilizado para consultar os usuários.

> **Importante:** o cabeçalho `Accept` indica o formato que o cliente prefere receber na resposta. Ele é diferente do `Content-Type`, que indica o formato dos dados enviados no body da requisição.

### Resumindo

Os dois comandos abaixo realizam uma requisição GET para consultar os usuários:

```bash
curl https://serverest.dev/usuarios
```

```bash
curl -X GET https://serverest.dev/usuarios \
-H "accept: application/json"
```

A principal diferença é que o segundo comando **explicita o método GET e informa o formato esperado da resposta**.

---

## Obter usuário por ID

Para consultar um usuário específico, devemos informar o seu **`_id`** na URL:

```bash
curl https://serverest.dev/usuarios/{_id}
```

Por exemplo:

```bash
curl https://serverest.dev/usuarios/7tS9K8NxabeHLEtk
```

Também podemos escrever a requisição de forma explícita:

```bash
curl -X GET https://serverest.dev/usuarios/7tS9K8NxabeHLEtk \
-H "accept: application/json"
```

Nesse caso, o servidor utiliza o `_id` informado na URL para localizar e retornar apenas aquele usuário.

---

# Consultar Produtos

O mesmo conceito pode ser aplicado aos produtos.

### Obter lista de produtos

```bash
curl https://serverest.dev/produtos
```

Ou, especificando o método e o formato esperado:

```bash
curl -X GET https://serverest.dev/produtos \
-H "accept: application/json"
```

### Obter produto por ID

Para consultar um produto específico:

```bash
curl https://serverest.dev/produtos/{_id}
```

Ou:

```bash
curl -X GET https://serverest.dev/produtos/{_id} \
-H "accept: application/json"
```

Substitua **`{_id}`** pelo identificador real do produto.

---

# Consultar Carrinhos

Também podemos utilizar GET para consultar os carrinhos cadastrados.

### Obter lista de carrinhos

```bash
curl https://serverest.dev/carrinhos
```

Ou:

```bash
curl -X GET https://serverest.dev/carrinhos \
-H "accept: application/json"
```

### Obter carrinho por ID

Para consultar um carrinho específico:

```bash
curl https://serverest.dev/carrinhos/{_id}
```

Ou:

```bash
curl -X GET https://serverest.dev/carrinhos/{_id} \
-H "accept: application/json"
```

Substitua **`{_id}`** pelo identificador real do carrinho.

---

## Resumindo

O método **GET** é utilizado para **ler ou consultar recursos** que já existem no servidor.

No ServeRest, podemos utilizar diferentes endpoints:

| Recurso       | Listar           | Consultar por ID       |
| ------------- | ---------------- | ---------------------- |
| **Usuários**  | `GET /usuarios`  | `GET /usuarios/{_id}`  |
| **Produtos**  | `GET /produtos`  | `GET /produtos/{_id}`  |
| **Carrinhos** | `GET /carrinhos` | `GET /carrinhos/{_id}` |

Dessa forma:

> **GET = Read (Ler/Consultar)**

No CRUD, o GET é responsável por **consultar os dados existentes no servidor**, sem criar, alterar ou excluir recursos.
