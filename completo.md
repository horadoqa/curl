## **10. Exemplo Completo de Requisição com cURL**

Vamos construir um exemplo completo de uma requisição **POST** com autenticação, envio de dados em JSON, e cabeçalhos personalizados:

```bash
curl -X POST https://api.exemplo.com/usuarios \
    -H "Content-Type: application/json" \
    -H "Authorization: Bearer <token>" \
    -d '{"nome": "Maria", "email": "maria@exemplo.com"}'
```

Este comando:
1. Realiza uma requisição **POST**.
2. Define os cabeçalhos **Content-Type** e **Authorization**.
3. Envia os dados do usuário em formato JSON.