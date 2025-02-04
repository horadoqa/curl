## **2. Realizando Requisições com cURL**

### 2.1. **GET Request**
Uma requisição **GET** é usada para obter dados de um servidor.

**Exemplo:**
```bash
curl https://api.exemplo.com/usuarios
```
Isso retorna os dados da URL fornecida.

**Exemplo com cabeçalhos adicionais:**
```bash
curl -H "Authorization: Bearer <token>" https://api.exemplo.com/usuarios
```
Adicionamos um cabeçalho para autenticação usando um token.