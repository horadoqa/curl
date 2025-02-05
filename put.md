# PUT Request

A requisição **PUT** é usada para atualizar um recurso existente no servidor.

**Exemplo:**
```bash
curl -X PUT https://api.exemplo.com/usuarios/1 -H "Content-Type: application/json" -d '{"nome": "João Silva", "email": "joao.silva@exemplo.com"}'
```
Aqui estamos atualizando o usuário com ID 1.