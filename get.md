# GET Request

Uma requisição **GET** é usada para obter dados de um servidor.

**Obter lista de Usuários**

### 1. **Primeiro Comando:**
```bash
curl https://serverest.dev/usuarios
```

#### Explicação:
- **Método HTTP**: Por padrão, quando você usa o **cURL** sem especificar o método HTTP, ele faz uma requisição **GET**.
- **Cabeçalhos**: Este comando não especifica nenhum cabeçalho adicional, portanto, o cURL irá enviar a requisição sem cabeçalhos extras.
- **Resultado**: A requisição é uma **GET** (padrão), e a resposta dependerá do servidor. O servidor pode devolver uma resposta em formato JSON, HTML ou outro tipo, dependendo da configuração do servidor e do que está sendo solicitado.

### 2. **Segundo Comando:**
```bash
curl -X 'GET' 'https://serverest.dev/usuarios' -H 'accept: application/json'
```

#### Explicação:
- **Método HTTP**: Aqui, o comando especifica explicitamente o método **GET** com a opção `-X 'GET'`. Embora o `GET` seja o método padrão no cURL, explicitar o método pode ser útil em alguns casos, principalmente se você estiver fazendo outros tipos de requisições como **POST**, **PUT**, ou **DELETE**.
- **Cabeçalhos**: O comando inclui um cabeçalho **`accept: application/json`**, que informa ao servidor que o cliente está esperando uma resposta no formato **JSON**. Isso ajuda o servidor a formatar a resposta de acordo com o tipo de dado solicitado.
- **Resultado**: A resposta provavelmente será em **JSON**, já que o cabeçalho **`accept: application/json`** foi especificado.
Adicionamos um cabeçalho para autenticação usando um token.

---

### Resumo das Diferenças:

- **Método**: No primeiro comando, o método **GET** é implícito (padrão). No segundo comando, o método **GET** é explicitamente especificado com `-X 'GET'`.
  
- **Cabeçalhos**: O primeiro comando não envia cabeçalhos adicionais. O segundo comando inclui um cabeçalho **`accept: application/json`**, que informa ao servidor que a resposta esperada deve ser em JSON.

### Quando Usar:
- O **primeiro comando** é mais simples e suficiente quando você não precisa de cabeçalhos personalizados e está fazendo uma requisição **GET**.
- O **segundo comando** é mais adequado quando você quer garantir que o servidor envie uma resposta em um formato específico (como **JSON**) e quando você quer especificar explicitamente o método **GET**, embora isso não seja necessário para uma simples requisição GET.

Em termos de funcionamento, ambos os comandos realizam a mesma operação básica (uma requisição GET para obter os dados dos usuários do servidor), mas o segundo comando é mais explícito e tem um controle adicional sobre os cabeçalhos da requisição.

**Obter Usuários por ID**

```bash
curl https://serverest.dev/usuarios/{-id}
```

ou

```bash
curl -X 'GET' 'https://serverest.dev/usuarios/{-id}' -H 'accept: application/json'
```

---

**Obter Produtos**

```bash
curl https://serverest.dev/produtos
```

ou

```bash
curl -X 'GET' 'https://serverest.dev/produtos' -H 'accept: application/json'
```

**Obter Produtos por ID**

```bash
curl https://serverest.dev/produtos/{-id}
```

ou

```bash
curl -X 'GET' 'https://serverest.dev/produtos/{-id}' -H 'accept: application/json'
```

---

**Obter Carrinhos**

```bash
curl https://serverest.dev/carrinhos
```

ou

```bash
curl -X 'GET' 'https://serverest.dev/carrinhos' -H 'accept: application/json'
```

**Obter carrinhos por ID**

```bash
curl https://serverest.dev/carrinhos/{-id}
```

ou

```bash
curl -X 'GET' 'https://serverest.dev/carrinhos/{-id}' -H 'accept: application/json'
```