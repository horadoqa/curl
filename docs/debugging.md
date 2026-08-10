# Debugging com cURL

Durante o desenvolvimento e os testes de uma API, muitas vezes precisamos entender **o que está acontecendo durante uma requisição HTTP**.

O cURL possui a opção **`-v` (verbose)**, que permite visualizar informações detalhadas sobre o processo de comunicação entre o cliente e o servidor.

### Exemplo

```bash
curl -v https://serverest.dev/usuarios
```

Ao utilizar o `-v`, o cURL exibe informações adicionais sobre a requisição, como:

* A tentativa de conexão com o servidor.
* A resolução do **DNS**, que transforma o domínio em um endereço IP.
* O estabelecimento da conexão.
* Os **headers enviados** pelo cliente.
* A requisição HTTP enviada ao servidor.
* Os **headers recebidos** na resposta.
* O **status code** retornado pelo servidor.
* O conteúdo da resposta.

### Exemplo de saída

A saída pode ser parecida com:

```text
* Host serverest.dev:443 was resolved.
* Connected to serverest.dev
> GET /usuarios HTTP/1.1
> Host: serverest.dev
> Accept: */*
>
< HTTP/1.1 200 OK
< Content-Type: application/json
<
{
    "quantidade": 2,
    "usuarios": [...]
}
```

Os símbolos ajudam a identificar o fluxo da comunicação:

* **`*`** — informações sobre o processo de conexão realizado pelo cURL.
* **`>`** — informações que estão sendo **enviadas pelo cliente** para o servidor.
* **`<`** — informações que estão sendo **recebidas do servidor**.

Por exemplo:

```text
> GET /usuarios HTTP/1.1
```

indica que o cliente enviou uma requisição **GET** para o endpoint `/usuarios`.

Já:

```text
< HTTP/1.1 200 OK
```

indica que o servidor respondeu com o status **`200 OK`**, informando que a requisição foi processada com sucesso.

### Quando utilizar o `-v`?

O modo verbose é especialmente útil quando uma requisição **não está funcionando como esperado**.

Por exemplo, podemos utilizá-lo para investigar:

* Erros de conexão.
* Problemas de DNS.
* Headers incorretos.
* Problemas de autenticação.
* Redirecionamentos.
* Status HTTP inesperados.
* Problemas de comunicação entre cliente e servidor.

### Resumindo

A opção:

```bash
curl -v <URL>
```

ativa o modo **verbose** do cURL e permite acompanhar com mais detalhes o processo de uma requisição HTTP.

> **`-v` = visualizar detalhes da comunicação entre o cliente e o servidor.**

É uma ferramenta muito útil para **debugging e troubleshooting de APIs**, principalmente quando precisamos descobrir em qual etapa da comunicação está ocorrendo um problema.
