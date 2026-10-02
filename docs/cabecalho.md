# Visualizando Cabeçalhos da Requisição e Resposta

Em uma requisição HTTP, os **headers (cabeçalhos)** carregam informações importantes sobre a comunicação entre o cliente e o servidor.

No cURL, podemos utilizar a opção **`-i`** (`--include`) para exibir os **cabeçalhos da resposta HTTP junto com o corpo da resposta**.

### Exemplo

```bash
curl -i https://serverest.dev/usuarios
```

Ao utilizar o `-i`, o cURL exibirá primeiro os headers retornados pelo servidor e, em seguida, o conteúdo da resposta.

### Exemplo de resposta

A saída será semelhante a:

```text
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 123
Date: Mon, 10 Aug 2026 10:00:00 GMT

{
    "quantidade": 2,
    "usuarios": [...]
}
```

Nesse exemplo, podemos observar:

```text
HTTP/1.1 200 OK
```

Esse é o **status da resposta**, indicando que a requisição foi processada com sucesso.

Já:

```text
Content-Type: application/json
```

informa que o conteúdo retornado pelo servidor está no formato **JSON**.

Depois dos headers, temos uma linha em branco que separa os **cabeçalhos** do **corpo da resposta**:

```text
Content-Type: application/json

{
    "quantidade": 2,
    "usuarios": [...]
}
```

### `-i` vs. `-v`

É importante diferenciar as opções `-i` e `-v`.

#### `-i`

```bash
curl -i https://serverest.dev/usuarios
```

O `-i` inclui os **headers da resposta** na saída, juntamente com o corpo.

É útil quando queremos verificar rapidamente informações como:

* Status code.
* `Content-Type`.
* `Content-Length`.
* Cookies.
* Outros headers retornados pelo servidor.

#### `-v`

```bash
curl -v https://serverest.dev/usuarios
```

O `-v` apresenta **informações mais detalhadas sobre a comunicação**, incluindo conexão, requisição enviada, headers enviados e headers recebidos.

Por isso, o `-v` é mais indicado quando estamos realizando **debugging** de uma requisição.

### Resumindo

A opção:

```bash
curl -i <URL>
```

permite visualizar os **headers da resposta HTTP junto com o corpo da resposta**.

> **`-i` = inclui os headers da resposta na saída do cURL.**

Já o:

> **`-v` = exibe informações detalhadas sobre o processo de comunicação HTTP.**

Essa diferença é importante para escolher a opção adequada durante os testes e o debugging de APIs.
