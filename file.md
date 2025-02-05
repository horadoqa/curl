# Enviar Arquivos com cURL

Você pode enviar arquivos para o servidor utilizando o método **POST** e o parâmetro `-F` (form-data).

**Exemplo:**
```bash
curl -X POST -F "file=@/caminho/do/arquivo.jpg" https://api.exemplo.com/upload
```

Aqui, estamos enviando um arquivo de imagem para a URL de upload da API.