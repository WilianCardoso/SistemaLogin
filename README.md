# Sistema de Login

Projeto de portfólio: uma API REST de autenticação construída em Java com Spring Boot e Spring Security, utilizando JWT (JSON Web Token) para autenticação stateless.

## 🚀 Tecnologias

- **Java 21**
- **Spring Boot** — framework principal
- **Spring Security** — autenticação e autorização
- **Spring Data JPA** — persistência de dados
- **MySQL / MariaDB** — banco de dados relacional
- **JWT (jjwt)** — geração e validação de tokens
- **BCrypt** — criptografia de senhas
- **Maven** — gerenciador de dependências

## 🏗️ Arquitetura

O projeto segue uma arquitetura de API REST, separada do frontend (que será construído futuramente em React). A autenticação é **stateless**: nenhuma sessão é mantida no servidor — cada requisição autenticada carrega seu próprio token JWT.

```
src/main/java/com/github/WilianCardoso/login_system/
├── config/         # Configuração do Spring Security
├── controller/     # Endpoints REST (AuthController, TestController)
├── dto/            # Objetos de transferência de dados (records)
├── model/          # Entidades JPA (User, Role)
├── repository/     # Interfaces JpaRepository
└── service/        # Regras de negócio (JwtService, CustomUserDetailsService, JwtAuthFilter)
```

## 🔐 Funcionalidades

- Cadastro de usuário com senha criptografada (BCrypt)
- Login com geração de token JWT
- Autenticação stateless via header `Authorization: Bearer <token>`
- Controle de permissões por Role (`ROLE_USER`, expansível para `ROLE_ADMIN`, etc.)
- Rota protegida de exemplo (`/me`) validando o token

## 📌 Endpoints

| Método | Rota             | Descrição                          | Autenticação |
|--------|------------------|-------------------------------------|--------------|
| POST   | `/auth/register` | Cadastra um novo usuário            | Não          |
| POST   | `/auth/login`    | Autentica e retorna o token JWT     | Não          |
| GET    | `/me`            | Retorna dados do usuário autenticado| Sim (Bearer) |

### Exemplo — Registro

```http
POST /auth/register
Content-Type: application/json

{
  "nome": "Teste",
  "email": "teste@teste.com",
  "senha": "123456"
}
```

### Exemplo — Login

```http
POST /auth/login
Content-Type: application/json

{
  "email": "teste@teste.com",
  "senha": "123456"
}
```

Resposta:

```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9..."
}
```

### Exemplo — Rota protegida

```http
GET /me
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...
```

## ⚙️ Como rodar o projeto

### Pré-requisitos

- JDK 21+
- MySQL ou MariaDB rodando localmente
- Maven (o projeto já inclui o Maven Wrapper, não precisa instalar separado)

### Passos

1. Clone o repositório:
   ```bash
   git clone https://github.com/WilianCardoso/SistemaLogin.git
   cd SistemaLogin/login-system
   ```

2. Crie o banco de dados:
   ```sql
   CREATE DATABASE login_db;
   ```

3. Configure o `src/main/resources/application.properties` com suas credenciais de banco:
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/login_db?useSSL=false&serverTimezone=UTC
   spring.datasource.username=seu_usuario
   spring.datasource.password=sua_senha
   ```

4. Rode a aplicação:
   ```bash
   mvnw.cmd spring-boot:run
   ```

5. A API estará disponível em `http://localhost:8080`

## 🧪 Testando

Recomenda-se o uso do [Postman](https://www.postman.com/) ou [Insomnia](https://insomnia.rest/) para testar os endpoints.

## 🗺️ Próximos passos

- [ ] Tratamento de erros e validação de campos (Bean Validation)
- [ ] Frontend em React consumindo a API
- [ ] Refresh token
- [ ] Endpoint de logout

## 👤 Autor

Wilian Cardoso
