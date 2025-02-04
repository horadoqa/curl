### 2.2. **POST Request**
Uma requisição **POST** é usada para enviar dados ao servidor (geralmente para criar um novo recurso).

**Exemplo básico com dados em JSON:**
```bash
curl -X POST https://api.exemplo.com/usuarios -H "Content-Type: application/json" -d '{"nome": "João", "email": "joao@exemplo.com"}'
```
**Explicação:**
- `-X POST`: Especifica que é uma requisição POST.
- `-H "Content-Type: application/json"`: Define o tipo de conteúdo como JSON.
- `-d '{...}'`: Define o corpo da requisição (os dados a serem enviados).