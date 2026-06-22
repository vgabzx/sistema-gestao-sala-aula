# Regras de Negócio

Este documento lista as principais regras que guiam o funcionamento do Sistema de Gestão de Sala de Aula Online (EduClass) e demonstra como elas impactam a construção da solução.

### Lista de Regras de Negócio
* **RN01:** Somente professores previamente vinculados a uma turma podem criar, editar ou excluir atividades nela.
* **RN02:** Um estudante não pode realizar a submissão de uma atividade após a data e horário limite estipulados, a menos que o professor habilite a opção de "entrega com atraso".
* **RN03:** O cadastro de usuários, a gestão de permissões e a configuração institucional (semestres, disciplinas e integrações) são ações exclusivas do perfil Administrador.
* **RN04:** O sistema deve registrar a data e hora exatas de cada submissão de atividade feita pelo estudante.
* **RN05:** As notas atribuídas às atividades devem seguir uma escala numérica de 0 a 100 pontos.
* **RN06:** Uma atividade não pode ser excluída pelo professor caso já exista alguma submissão de estudante atrelada a ela.
* **RN07:** Cada turma deve possuir um professor responsável, que é quem a cria dentro de uma disciplina e gera o código de convite utilizado para a matrícula dos estudantes.
* **RN08:** A matrícula de um estudante em uma turma pode ocorrer de duas formas: pela sincronização automática com o Sistema Acadêmico (SIS) institucional ou pela inserção, pelo próprio estudante, do código de convite gerado pelo professor.

---

### Impacto das Regras na Solução

Para demonstrar a influência das regras de negócio no projeto, detalhamos o impacto de três delas, evidenciando a rastreabilidade entre requisito, modelagem e arquitetura.

**Impacto da RN01 (Apenas professores vinculados podem gerenciar atividades)**
* **User Story:** US01 — "Como professor, desejo criar/publicar atividades para a minha turma, para que os estudantes possam realizar e enviar seus trabalhos."
* **Caso de Uso (UML):** "Publicar Atividade", restrito ao ator Professor.
* **BPMN:** A raia (lane) referente à criação/correção pertence exclusivamente ao ator "Professor".
* **Arquitetura:** A autenticação é delegada a um Provedor de Identidade externo via OAuth 2.0 / OIDC (SSO). O **API Gateway** valida o *token* JWT recebido e aplica autorização baseada em papéis (RBAC - Role-Based Access Control), garantindo que requisições de estudantes para endpoints exclusivos de professor sejam bloqueadas.
* **Requisito Não Funcional:** Segurança.

**Impacto da RN06 (Bloqueio de exclusão de atividade com submissões)**
* **Casos de Uso (UML):** O fluxo de exceção do caso de uso "Corrigir/Gerenciar Atividade" prevê a verificação de submissões existentes e a exibição de uma mensagem de erro ao professor.
* **Modelagem de Dados (Arquitetura):** O banco de dados relacional (PostgreSQL) utiliza uma restrição de chave estrangeira (*Foreign Key Constraint*) para evitar a exclusão em cascata acidental e proteger a integridade dos dados acadêmicos.
* **Regra de Interface:** O botão "Excluir" é desabilitado na interface do professor assim que o primeiro estudante realiza um envio.

**Impacto da RN08 (Matrícula via SIS ou código de convite)**
* **User Story:** US07 — "Como estudante, desejo matricular-me em uma turma informando o código de convite, para acessar seus conteúdos e atividades."
* **Caso de Uso (UML):** "Matricular-se em Turma", associado ao ator Estudante.
* **Arquitetura:** Exige a integração com o **Sistema Acadêmico (SIS)** externo por meio de uma API REST (sincronização de matrículas), conforme representado no Diagrama de Contexto e de Containers do C4. Essa regra motivou a decisão arquitetural de integração com sistemas institucionais.
