# Autenticação com cURL

O cURL permite realizar requisições autenticadas. Você pode passar a autenticação no formato **Basic** ou **Bearer Token**.

### 4.1. **Autenticação Basic**
```bash
curl -u usuario:senha https://api.exemplo.com/usuarios
```

### 4.2. **Autenticação Bearer Token**
```bash
curl -H "Authorization: Bearer <token>" https://api.exemplo.com/usuarios