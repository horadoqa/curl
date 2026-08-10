# CREATE — POST Request

A requisição **POST** é utilizada para **enviar dados ao servidor**, geralmente com o objetivo de **criar um novo recurso**.

No ServeRest, podemos utilizar o método POST para cadastrar um novo usuário.

### Endpoint

```http
POST https://serverest.dev/usuarios
```

### Exemplo

```bash
curl -X POST https://serverest.dev/usuarios \
-H "Content-Type: application/json" \
-d '{
    "nome": "Hora do QA",
    "email": "horadoqa@email.com",
    "password": "1q2w3e4r",
    "administrador": "true"
}'
```

### Entendendo a requisição

* **`-X POST`**: define o método HTTP como **POST**.
* **`-H "Content-Type: application/json"`**: informa ao servidor que os dados enviados estão no formato **JSON**.
* **`-d '{...}'`**: define o **body da requisição**, ou seja, os dados que serão enviados para o servidor.

Nesse exemplo, estamos enviando os dados de um novo usuário:

```json
{
    "nome": "Hora do QA",
    "email": "horadoqa@email.com",
    "password": "1q2w3e4r",
    "administrador": "true"
}
```

O servidor recebe essas informações e tenta criar um novo cadastro.

### Resposta de sucesso

Quando o cadastro é realizado com sucesso, o ServeRest retorna o status **`201 Created`**, indicando que um novo recurso foi criado.

A resposta contém uma mensagem de confirmação e o **`_id`** gerado para o novo usuário:

```json
{
    "message": "Cadastro realizado com sucesso",
    "_id": "7tS9K8NxabeHLEtk"
}
```

O **`_id`** é um identificador único utilizado para localizar esse usuário em outras requisições, como **GET, PUT e DELETE**.

### E-mail já cadastrado

O campo **`email` deve ser único**. Portanto, se tentarmos cadastrar outro usuário utilizando um e-mail que já existe, o ServeRest retornará uma mensagem informando que o e-mail já está sendo utilizado:

```json
{
    "message": "Este email já está sendo usado"
}
```

### Resumindo

O fluxo de criação de um usuário com **POST** é:

1. Utilizamos o método **POST**.
2. Informamos o endpoint `/usuarios`.
3. Enviamos os dados do usuário no **body**, em formato JSON.
4. O servidor valida os dados recebidos.
5. Se tudo estiver correto, um novo usuário é criado.
6. O servidor retorna o **`_id`** do usuário criado.

> **POST = Create (Criar)**

Esse é o primeiro passo do CRUD: **criar um novo recurso no servidor**.
