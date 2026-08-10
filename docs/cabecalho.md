# Visualizando Cabeçalhos da Requisição e Resposta

Em uma requisição HTTP, os **headers (cabeçalhos)** carregam informações importantes sobre a comunicação entre o cliente e o servidor.

No cURL, podemos utilizar a opção **`-i`** (`--include`) para exibir os **cabeçalhos da resposta HTTP junto com o corpo da resposta**.

### Exemplo

```bash j2h4kf"
curl -i https://serverest.dev/usuarios
```

Ao utilizar o `-i`, o cURL exibirá primeiro os headers retornados pelo servidor e, em seguida, o conteúdo da resposta.

### Exemplo de resposta

A saída será semelhante a:

```text p8q3ls"
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

```text qf7v2a"
HTTP/1.1 200 OK
```

Esse é o **status da resposta**, indicando que a requisição foi processada com sucesso.

Já:

```text c4z8mn"
Content-Type: application/json
```

informa que o conteúdo retornado pelo servidor está no formato **JSON**.

Depois dos headers, temos uma linha em branco que separa os **cabeçalhos** do **corpo da resposta**:

```text m5q2xr"
Content-Type: application/json

{
    "quantidade": 2,
    "usuarios": [...]
}
```

### `-i` vs. `-v`

É importante diferenciar as opções `-i` e `-v`.

#### `-i`

```bash 4e6hsp"
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

```bash 5k9rwd"
curl -v https://serverest.dev/usuarios
```

O `-v` apresenta **informações mais detalhadas sobre a comunicação**, incluindo conexão, requisição enviada, headers enviados e headers recebidos.

Por isso, o `-v` é mais indicado quando estamos realizando **debugging** de uma requisição.

### Resumindo

A opção:

```bash 8w4nvc"
curl -i <URL>
```

permite visualizar os **headers da resposta HTTP junto com o corpo da resposta**.

> **`-i` = inclui os headers da resposta na saída do cURL.**

Já o:

> **`-v` = exibe informações detalhadas sobre o processo de comunicação HTTP.**

Essa diferença é importante para escolher a opção adequada durante os testes e o debugging de APIs.
