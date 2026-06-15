# Regras de Negócio

Este documento lista as principais regras que guiam o funcionamento do Sistema de Gestão de Sala de Aula Online e demonstra como elas impactam a construção da solução.

### Lista de Regras de Negócio
* **RN01:** Somente professores previamente vinculados a uma turma podem criar, editar ou excluir atividades nela.
* **RN02:** Um estudante não pode realizar a submissão de uma atividade após a data e horário limite estipulados, a menos que o professor habilite a opção de "entrega com atraso".
* **RN03:** A criação de novas disciplinas e a alocação de professores nas turmas são ações exclusivas do perfil Administrador.
* **RN04:** O sistema deve registrar a data e hora exatas de cada submissão de atividade feita pelo estudante.
* **RN05:** As notas atribuídas às atividades devem seguir uma escala numérica de 0 a 100 pontos.
* **RN06:** Uma atividade não pode ser excluída pelo professor caso já exista alguma submissão de estudante atrelada a ela.

---

### Impacto das Regras na Solução

Para demonstrar a influência das regras de negócio no projeto, detalhamos o impacto de duas delas:

**Impacto da RN01 (Apenas professores vinculados podem gerenciar atividades)**
* **User Story:** "Como professor, desejo criar atividades para a minha turma, para que os estudantes possam enviar seus trabalhos."
* **BPMN:** A raia (lane) de "Criação de Atividade" no fluxo do processo pertencerá exclusivamente ao ator "Professor".
* **Arquitetura:** Exige um mecanismo de autenticação robusto (ex: JWT) e autorização baseada em papéis (RBAC - Role-Based Access Control) no backend, garantindo que a API bloqueie requisições de alunos.
* **Requisito Não Funcional:** Segurança.

**Impacto da RN06 (Bloqueio de exclusão de atividade com submissões)**
* **Casos de Uso:** O fluxo de exceção do Caso de Uso "Excluir Atividade" deve prever a verificação de submissões existentes e exibir uma mensagem de erro ao professor.
* **Modelagem de Dados (Arquitetura):** O banco de dados precisará de uma restrição de chave estrangeira (Foreign Key Constraint) para evitar a exclusão em cascata acidental e proteger a integridade dos dados acadêmicos.
* **Regra de Interface:** O botão "Excluir" deve ser desabilitado ou ocultado na interface do professor assim que o primeiro aluno fizer um envio.
