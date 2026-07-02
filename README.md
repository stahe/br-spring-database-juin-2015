# Utilizando um banco de dados relacional com o ecossistema Spring (junho de 2015)

Este projeto tem como objetivo estudar e comparar diferentes arquiteturas de acesso a dados em uma aplicação Java baseada no ecossistema **Spring**, especificamente o **Spring JDBC** e o **Spring JPA**, aplicados a um banco de dados relacional.

O material teórico e didático correspondente está disponível aqui:  
👉 https://stahe.github.io/br-spring-database-juin-2015/

---

## Objetivos do projeto

- Compreender uma **arquitetura de aplicativo em camadas**
- Comparar duas abordagens para acesso a dados:
  - JDBC “clássico”
  - JPA (Java Persistence API)
- Medir e comparar o **desempenho** de ambas as soluções
- Estudar os desafios da **portabilidade entre SGBDs**

---

## Arquitetura geral

A aplicação é baseada em uma arquitetura em camadas, na qual o fluxo de execução ocorre da esquerda para a direita:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000007080000017A09403716.png)


### Função das camadas

#### Camada de interface do usuário (UI)
- Ponto de acesso à aplicação
- Recebe as ações do usuário
- Exibe os resultados

#### Camada de negócios
- Implementa as **regras de negócios**
- Processa dados provenientes de:
  - do banco de dados (via DAO)
  - do usuário (via interface do usuário)
- Pode retornar ou armazenar os resultados

#### Camada DAO (Data Access Object)
- Oferece uma **interface para acesso aos dados de negócios**
- Oculta os detalhes técnicos do acesso ao banco de dados
- Depende da tecnologia utilizada (JDBC ou JPA)

#### Camada JDBC
- Interface padrão para acesso a bancos de dados relacionais
- Independente do SGBD (por meio de drivers JDBC)
- Oferece bom desempenho, mas, na prática, portabilidade limitada

---

## Evolução para o JPA

Desde meados dos anos 2000, a arquitetura pode evoluir da seguinte forma:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

### Características do JPA

- A camada **JPA** gera as consultas SQL
- A camada DAO:
  - não contém mais SQL
  - trabalha com objetos persistentes
- Vantagens:
  - melhor portabilidade entre SGBDs
  - abstração do SQL proprietário
- Desvantagem:
  - o desempenho é, em geral, inferior ao do JDBC

O JPA formaliza conceitos que já haviam sido introduzidos por frameworks como o **Hibernate**.

---

## Comparação entre JDBC e JPA

O projeto implementa **duas implementações separadas de DAO**:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006E10000016947159BE8.png)


### Restrições comuns

- `DAO1` e `DAO2` implementam **a mesma interface `IDAO`**
- Os testes unitários são **idênticos** para ambas as implementações
- Objetivo: comparar **funcionalmente** e **em termos de desempenho**

---

## Testes e desempenho

- Os testes são executados com **JUnit**
- É utilizada uma única classe de teste (`JUnitTestsDao`)
- Com os resultados, é possível:
  - verificar a conformidade funcional;
  - comparar os tempos de execução do JDBC e do JPA;

---

## Portabilidade do SGBD

Embora o JDBC busque a máxima portabilidade:
- o SQL proprietário;
- as estratégias para geração de chaves primárias;
- as palavras reservadas específicas;

limitam essa portabilidade na prática.

Neste projeto, as arquiteturas JDBC e JPA foram portadas para **seis DBMS diferentes**, com configurações específicas para cada DBMS.

---

## Conclusão

Este projeto ilustra:
- as ponderações entre **desempenho** e **abstração**
- as escolhas arquitetônicas relacionadas ao acesso aos dados;
- a contribuição do Spring para a estruturação e a testabilidade das aplicações;

Ele constitui uma ferramenta educacional para compreender concretamente o JDBC, o JPA e suas aplicações comparativas em uma arquitetura Spring.

---
