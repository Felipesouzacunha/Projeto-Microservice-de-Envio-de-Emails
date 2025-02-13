# Projeto: Microsserviço de Envio de E-mails

## Descrição

Este projeto é um microsserviço para envio de e-mails, desenvolvido com Spring Boot, RabbitMQ e PostgreSQL. Ele recebe mensagens de uma fila RabbitMQ, processa os dados e envia um e-mail para o destinatário.

## Tecnologias Utilizadas

- Java 21
- Spring Boot
- Spring Data JPA
- Spring Mail
- RabbitMQ
- PostgreSQL

## Estrutura do Projeto

O projeto está dividido em dois microsserviços principais:

1. **ms-email**: Responsável por consumir mensagens da fila e enviar e-mails.
2. **ms-user**: Responsável por cadastrar usuários e enviar mensagens para a fila do RabbitMQ.

## Configuração do Ambiente

Antes de iniciar o projeto, configure os seguintes serviços:

### Banco de Dados PostgreSQL

1. Certifique-se de que o PostgreSQL esteja rodando na porta correta.
2. Configure as credenciais no arquivo `application.properties`:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/ms-email
   spring.datasource.username=postgres
   spring.datasource.password=1234
   spring.jpa.hibernate.ddl-auto=update
   ```

### RabbitMQ

1. Utilize uma instância local ou na nuvem.
2. Defina as credenciais no arquivo `application.properties`:
   ```properties
   spring.rabbitmq.addresses=amqps://<usuario>:<senha>@<host>/<vhost>
   broker.queue.email.name=default.email
   ```

### Servidor SMTP

Para enviar e-mails, configure as credenciais do SMTP no arquivo `application.properties`:

```properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=<seu_email>
spring.mail.password=<senha_do_app>
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
```

## Como Rodar o Projeto

1. Clone o repositório:
   ```sh
   git clone https://github.com/seu-usuario/ms-email-service.git
   ```
2. Acesse a pasta do projeto e rode o seguinte comando para construir o projeto:
   ```sh
   mvn clean install
   ```
3. Inicie o microsserviço de usuário:
   ```sh
   mvn spring-boot:run -pl ms-user
   ```
4. Inicie o microsserviço de e-mails:
   ```sh
   mvn spring-boot:run -pl ms-email
   ```

## Testando a Aplicação

1. Registre um novo usuário enviando um POST para `ms-user`:
   ```sh
   curl -X POST http://localhost:8081/users -H "Content-Type: application/json" -d '{"name":"João","email":"joao@email.com"}'
   ```
2. O RabbitMQ irá processar a mensagem e o `ms-email` enviará um e-mail para o usuário recém-cadastrado.

## Contribuição

Contribuições são bem-vindas! Para sugerir melhorias, abra uma issue ou envie um pull request.

## Licença

Este projeto está sob a licença MIT. Para mais detalhes, consulte o arquivo `LICENSE`.

