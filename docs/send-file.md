# Enviar Arquivos com cURL

O cURL também permite **enviar arquivos para um servidor** por meio de requisições HTTP.

Para isso, podemos utilizar o parâmetro **`-F`** (`--form`), que envia os dados no formato **`multipart/form-data`**. Esse formato é muito utilizado em APIs que possuem endpoints para **upload de arquivos**.

### Exemplo

```bash
curl -X POST \
-F "file=@/caminho/do/arquivo.jpg" \
https://api.exemplo.com/upload
```

Nesse exemplo, estamos enviando o arquivo `arquivo.jpg` para o endpoint `/upload` da API.

### Entendendo a requisição

* **`-X POST`**: define o método HTTP como **POST**.
* **`-F`**: indica que os dados serão enviados como um formulário `multipart/form-data`.
* **`file=`**: é o nome do campo que a API espera receber.
* **`@/caminho/do/arquivo.jpg`**: o `@` informa ao cURL que o valor deve ser lido como um **arquivo local**.
* **`https://api.exemplo.com/upload`**: é o endpoint responsável por receber o arquivo.

Por exemplo, se o arquivo estiver na pasta `Downloads`:

```bash
curl -X POST \
-F "file=@/home/usuario/Downloads/foto.jpg" \
https://api.exemplo.com/upload
```

No Windows, o caminho pode ser semelhante a:

```bash
curl -X POST ^
-F "file=@C:\Users\Usuario\Downloads\foto.jpg" ^
https://api.exemplo.com/upload
```

### Enviando outros dados junto com o arquivo

Também podemos enviar **outros campos do formulário** junto com o arquivo.

Por exemplo:

```bash
curl -X POST \
-F "file=@/caminho/do/arquivo.jpg" \
-F "descricao=Foto de perfil" \
https://api.exemplo.com/upload
```

Nesse caso, a requisição envia dois campos:

* **`file`** — contém o arquivo.
* **`descricao`** — contém um texto com a descrição do arquivo.

### Por que utilizar `multipart/form-data`?

Quando precisamos enviar arquivos, o formato `multipart/form-data` permite combinar **arquivos e outros campos de formulário** na mesma requisição.

Por isso, é bastante comum encontrarmos esse formato em APIs que possuem funcionalidades como:

* Upload de imagens.
* Upload de documentos.
* Envio de anexos.
* Importação de arquivos.

### Resumindo

Para enviar um arquivo com cURL, podemos utilizar:

```bash
curl -X POST \
-F "campo=@/caminho/do/arquivo.extensao" \
https://api.exemplo.com/upload
```

> **`-F` = envia dados como `multipart/form-data`.**
> **`@` = indica que o valor deve ser enviado a partir de um arquivo local.**
