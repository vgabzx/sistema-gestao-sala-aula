# Arquitetura de Software

## 1. Estilo Arquitetural Escolhido
A arquitetura escolhida para o Sistema de Gestão de Sala de Aula Online é a **Arquitetura em Camadas (Layered Architecture)** integrada via API REST.

**Justificativa:** Considerando os requisitos do sistema e o contexto do desenvolvimento de um MVP, a arquitetura em camadas oferece uma separação clara de responsabilidades (Apresentação, Regras de Negócio e Acesso a Dados). Isso facilita a organização do código, agiliza o desenvolvimento e é perfeitamente adequada para o escopo inicial do sistema, evitando a sobrecarga e a complexidade técnica desnecessária de uma arquitetura de Microsserviços.

## 2. Decisões Arquiteturais

Para suportar a solução proposta, definimos as seguintes decisões arquiteturais:

* **Decisão 1: Separação entre Cliente e Servidor (Frontend SPA + Backend API REST)**
  * **Justificativa:** O uso de uma API RESTful permite que o backend atenda a múltiplos clientes (como uma interface web e, futuramente, um aplicativo mobile). Essa separação também permite que diferentes integrantes da equipe trabalhem no front e no back simultaneamente.

* **Decisão 2: Mecanismo de Autenticação via JWT (JSON Web Token)**
  * **Justificativa:** Para garantir a segurança exigida pelas regras de negócio (como a RN01, que restringe a criação de atividades apenas a professores), escolhemos o JWT. Ele permite uma autenticação *stateless* (sem estado), o que significa que o servidor não precisa armazenar a sessão na memória, melhorando o desempenho e garantindo que cada requisição seja verificada de forma segura e independente.

* **Decisão 3: Banco de Dados Relacional (SQL)**
  * **Justificativa:** O domínio acadêmico possui dados altamente estruturados e relacionamentos fortes (ex: uma Disciplina possui Turmas; uma Turma possui Alunos e Atividades; uma Atividade possui Submissões). O uso de um banco de dados relacional (como PostgreSQL ou MySQL) garante a integridade referencial dos dados, bloqueando ações indevidas como a exclusão de uma atividade que já possui trabalhos entregues (conforme a RN06).
