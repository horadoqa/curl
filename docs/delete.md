# DELETE — DELETE Request

A requisição **DELETE** é utilizada para **remover um recurso existente do servidor**.

No ServeRest, podemos utilizar o método DELETE para excluir um usuário.

### Endpoint

```http
DELETE https://serverest.dev/usuarios/{_id}
```

O **`_id`** informado na URL identifica qual usuário será excluído.

### Exemplo

```bash
curl -X DELETE https://serverest.dev/usuarios/7tS9K8NxabeHLEtk
```

Nesse exemplo, estamos enviando uma requisição **DELETE** para excluir o usuário cujo `_id` é:

```text
7tS9K8NxabeHLEtk
```

Diferentemente do POST e do PUT, não precisamos enviar um **body** com os dados do usuário. O `_id` na própria URL é suficiente para que o servidor identifique o registro que deverá ser removido.

### Resposta de sucesso

Quando a exclusão é realizada com sucesso, o ServeRest retorna uma mensagem confirmando a operação:

```json
{
    "message": "Registro excluído com sucesso"
}
```

### Resumindo

O fluxo para excluir um usuário com **DELETE** é:

1. Utilizamos o método **DELETE**.
2. Informamos o endpoint `/usuarios`.
3. Passamos o **`_id` do usuário na URL**.
4. O servidor localiza o usuário pelo `_id`.
5. O registro é removido.
6. O servidor retorna uma mensagem confirmando a exclusão.

> **DELETE = Delete (Excluir)**

No CRUD, o DELETE é responsável por **remover um recurso existente do servidor**.
