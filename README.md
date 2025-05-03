# Teste de Conhecimento em DevOps - Labtel/2025

## 1. Introdução

Este repositório contém a solução para o teste de conhecimento em DevOps proposto pelo Laboratório de Telecomunicações (Labtel).

### 2. Descrição da Tarefa

> Crie um ambiente de execução conteinerizado contemplando as camadas de Front-end, Back-end e Banco de Dados (MySQL). Para isso, utilize os códigos disponibilizados na vídeo aula, onde também é possível encontrar um arquivo `.sql` que deverá ser importado para o contêiner MySQL. O ambiente precisa ter uma rede própria, e os contêineres de Banco de Dados e Back-end devem se comunicar através dessa rede.  
>
> **Tarefa adicional:** envie as imagens criadas para o Docker Hub em sua conta pessoal e atualize o `docker-compose.yml` conforme necessário.

## 3. Tecnologias Utilizadas

- **WSL/Ubuntu** – Ambiente de desenvolvimento;
- **Docker** – Containerização dos serviços;
- **Visual Studio Code** – Editor de código;
- **Insomnia** - Ferramenta de testes de API utilizada para realizar requisições e validar os endpoints desenvolvidos;
- **Google Chrome** – Navegador utilizado para testes no Front-end;

## 4. Passo a Passo para Executar o Projeto

### 4.1. Clonar o Repositório

```bash
git clone https://github.com/JoaoGBarros/labtel_devops.git
cd labtel_devops

```

### 4.2. Subir o container

Para subir os containers contendo o frontend, back-end e banco de dados é necessario, primeiro, criar a rede que servirá para a comunicação entre o back-end e o banco de dados. Utilize o comando:

```bash 
docker network create airquality
```

Após a criação da rede, podemos realizar o comando:

```bash 
docker-compose up --build -d
```

### 4.3. Vericando conexão

Para verificar se os containers foram inicializados e estão funcionando corretamente 

#### 4.3.1 Acessar o Back-end

Acesse a documentação da API no endereço:


```bash 
http://localhost:18003/docs
``` 

Também é possivel realizar consultas requisições ao servidor para retornar os dados dos sensores. 

Tente realizar uma requisição por meio de um programa como `Insomnia` ou `Postman` para o endereço:

```bash 
http://localhost:18003/sensorData/?date_reference=<yyyy-mm-dd>&start_time=<hora>%3A<min>%3A<segundo>&end_time=<hora>%3A<min>%3A<segundo>
```
Substitua os parâmetros com os valores desejados.

#### 4.3.2. Acessar o Frontend

Acesse a aplicação web no endereço: 

```bash 
http://localhost:8080
```
Você poderá navegar pelas páginas Início, Mapa e Sobre.

No endereço http://localhost:8080/map, é possível visualizar o mapa interativo com os dados dos sensores. Os dados estão disponíveis até 28/03/2025.

## 5. Correções

Havia um problema ao realizar requisições entre 00:00:00 e 23:59:59, causado por uma adição de 3 horas nos horários inseridos. Isso resultava em buscas incorretas de dados (por exemplo, 23:59:59 se tornava 02:59:59 do mesmo dia).

O problema foi solucionado comentando as linhas responsáveis por essa alteração de horário no código do frontend (CPID-DevOps-AirQuality-Frontend\src\views\Map.vue linhas 118 e 119).
