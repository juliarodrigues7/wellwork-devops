🌐 Entrega DevOps — Global Solution
WellWork – Deploy em Duas VMs (Linux + Windows) + Testes via cURL

Este repositório contém toda a documentação da etapa de DevOps da Global Solution, demonstrando:

Criação e configuração das VMs na Azure

Deploy completo do backend Java dentro da VM Linux

Conexão com o banco Oracle da FIAP

Testes de API via cURL (CRUD completo)

Evidências, prints e comandos utilizados

🖥️ Máquinas Virtuais
 VM Linux

Responsável por rodar o backend Java

Conecta no Oracle FIAP

Onde foram executados os testes via cURL

VM Windows

Utilizada como segunda máquina virtual da entrega

Representa a camada de apresentação

Usada para validar acesso, interface e organização do ambiente

⚙️ Tecnologias Utilizadas

Microsoft Azure (máquinas virtuais)

Ubuntu Linux

Windows Server

Java 25

Spring Boot 3

Oracle Database FIAP

cURL

GitHub

📦 Deploy do Backend na VM Linux
1. Atualização e preparação do ambiente
sudo apt update
sudo apt install zip unzip -y
java -version

2. Clonando o repositório do backend
git clone <url-do-backend>
cd <pasta-do-backend>

3. Build e execução do backend
./mvnw clean package
java -jar target/*.jar


Durante a inicialização, o backend exibe:

Tomcat started on port 8080
jdbc:oracle:thin:@oracle.fiap.com.br:1521:orcl


Confirmando:

✔️ Servidor backend ativo
✔️ Banco Oracle conectado
✔️ Porta 8080 operante

🔄 Testes com cURL (CRUD Completo)

Todos os testes foram executados diretamente dentro da VM Linux, acessando o backend localmente.

🟦 CREATE
curl -i -X POST http://localhost:8080/api/usuario \
  -H "Content-Type: application/json" \
  -d '{
    "email": "julialinux@example.com",
    "senha": "123456",
    "cargo": "USER",
    "acessibilidade": "Nenhuma",
    "nome": "Julia Linux"
  }'


Retorno esperado:

HTTP/1.1 201

🟩 READ (listar usuários)
curl -i "http://localhost:8080/api/usuario?direction=ASC"


Retorna a lista de usuários cadastrados.

🟧 UPDATE (ID = 1)
curl -i -X PATCH http://localhost:8080/api/usuario \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1,
    "email": "julialinux@example.com",
    "senha": "123456",
    "nome": "Julia Linux Atualizada",
    "cargo": "USER",
    "acessibilidade": "Modo alto contraste"
  }'


Retorno esperado:

HTTP/1.1 200

🟥 DELETE (ID = 1)
curl -i -X DELETE http://localhost:8080/api/usuario \
  -H "Content-Type: application/json" \
  -d '{
    "id": 1
  }'


Retorno esperado:

HTTP/1.1 204
