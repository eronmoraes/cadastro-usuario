# Cadastro de Usuário

API REST desenvolvida em **Java com Spring Boot** para gerenciamento de cadastro de usuários, com operações de criação, busca, atualização e remoção via e-mail ou ID.

## ✨ Funcionalidades

- ➕ Cadastrar novo usuário
- 🔍 Buscar usuário por e-mail
- ✏️ Atualizar dados de um usuário (atualização parcial)
- 🗑️ Remover usuário por e-mail

## 🛠️ Tecnologias utilizadas

- Java
- Spring Boot
- Spring Web (REST Controllers)
- Spring Data JPA
- Lombok
- H2 Database (banco de dados em memória)

## 📁 Estrutura do projeto

```
src/main/java/com/javaspring/cadastro_usuario/
├── controller/
│   └── UsuarioController.java
├── business/
│   └── UsuarioService.java
└── infrastructure/
    ├── entitys/
    │   └── Usuario.java
    └── repository/
        └── UsuarioRepository.java
```

## 🔗 Endpoints da API

Base URL: `/usuario`

### Cadastrar usuário
```http
POST /usuario
```
**Body (JSON):**
```json
{
  "nome": "Maria Silva",
  "email": "maria@email.com"
}
```
Retorna `200 OK` quando o cadastro é realizado com sucesso.

> ⚠️ O campo `email` é único no banco de dados — tentar cadastrar um e-mail já existente resulta em erro de violação de restrição (constraint).

### Buscar usuário por e-mail
```http
GET /usuario?email=maria@email.com
```
Retorna `200 OK` com os dados do usuário. Caso o e-mail não seja encontrado, retorna erro.

### Atualizar usuário
```http
PUT /usuario?id=1
```
**Body (JSON):** apenas os campos que deseja atualizar.
```json
{
  "nome": "Maria Silva Santos"
}
```
Retorna `200 OK` com o usuário atualizado. A atualização é **parcial**: campos não enviados (`null`) mantêm o valor já salvo. Caso o `id` não seja encontrado, retorna erro.

### Remover usuário
```http
DELETE /usuario?email=maria@email.com
```
Retorna `200 OK` quando removido com sucesso.

## ⚙️ Como executar o projeto

### Pré-requisitos
- Java 17+
- Maven

> O projeto usa **H2**, um banco de dados em memória — não é necessário instalar ou configurar nenhum banco externo para rodar localmente.

### Passos

```bash
# Clone o repositório
git clone https://github.com/eronmoraes/cadastro-usuario.git
cd cadastro-usuario

# Rode o projeto
./mvnw spring-boot:run
```

A API estará disponível em `http://localhost:8080`.

### Console do H2

Com a aplicação rodando, você pode acessar o console do banco em memória para visualizar as tabelas e dados diretamente pelo navegador:

```
http://localhost:8080/h2-console
```

**Dados de conexão:**
- JDBC URL: `jdbc:h2:mem:usuarios`
- User Name: `sa`
- Password: *(em branco)*

> ⚠️ Por ser um banco em memória, todos os dados são perdidos ao reiniciar a aplicação.

## 📌 Regras de negócio

- O campo **e-mail** é único — não é possível cadastrar dois usuários com o mesmo e-mail.
- A atualização de usuário (`PUT`) é feita por **ID** e é **parcial**: apenas os campos enviados no corpo da requisição são alterados; os demais mantêm o valor anterior.
- A remoção é feita pelo **e-mail** do usuário.

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para abrir uma *issue* ou enviar um *pull request*.

## 📄 Licença

Este projeto está sob a licença MIT.
