## Adicionando Cabeçalhos (Headers)

Você pode adicionar cabeçalhos personalizados em suas requisições com o parâmetro `-H`.

**Exemplo:**
```bash
curl -X GET https://api.exemplo.com/usuarios -H "Authorization: Bearer <token>"
```
Aqui, estamos passando um cabeçalho de autorização para uma API que exige autenticação.