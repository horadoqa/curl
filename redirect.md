## **7. Seguir Redirecionamentos**

O parâmetro `-L` permite que o cURL siga redirecionamentos HTTP automaticamente.

**Exemplo:**
```bash
curl -L https://api.exemplo.com/redirect
```
Se o servidor responder com um redirecionamento (código 3xx), o cURL seguirá até o destino final.