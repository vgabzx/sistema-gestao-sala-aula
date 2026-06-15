# User Stories (Histórias de Usuário)

Este documento contém os requisitos do sistema descritos sob a perspectiva do usuário, organizados para facilitar o desenvolvimento e os testes.

### US01 - Criar Atividade
* **Descrição:** Como professor, desejo criar uma nova atividade com título, descrição e prazo de entrega, para que os estudantes possam realizar as tarefas da disciplina.
* **Critérios de Aceitação:**
  * O sistema deve permitir anexar arquivos à atividade.
  * O professor deve definir obrigatoriamente um título e uma data limite.
  * Após a criação, todos os alunos matriculados na turma devem visualizar a atividade em seus murais.

### US02 - Entregar Atividade
* **Descrição:** Como estudante, desejo anexar arquivos e enviar minha resposta a uma atividade, para que o professor possa avaliá-la.
* **Critérios de Aceitação:**
  * O sistema deve aceitar arquivos em formatos comuns (PDF, DOCX, JPG).
  * O aluno deve receber uma confirmação visual de que a entrega foi registrada com sucesso.
  * O sistema deve bloquear envios após o prazo estabelecido, caso o professor não tenha habilitado entregas com atraso.

### US03 - Atribuir Nota e Feedback
* **Descrição:** Como professor, desejo visualizar as entregas dos alunos e atribuir uma nota e um comentário, para dar o retorno adequado sobre o desempenho deles.
* **Critérios de Aceitação:**
  * O professor deve poder inserir uma nota de 0 a 100.
  * O campo de feedback textual é opcional.
  * Assim que a nota for salva, o aluno correspondente deve conseguir visualizar a correção no seu painel.

### US04 - Visualizar Mural da Turma
* **Descrição:** Como estudante, desejo visualizar um mural cronológico com avisos, novos materiais e atividades, para me manter atualizado sobre a disciplina.
* **Critérios de Aceitação:**
  * As postagens mais recentes devem aparecer no topo do mural.
  * Cada postagem deve indicar claramente o nome de quem publicou e a data da publicação.

### US05 - Criar Nova Turma
* **Descrição:** Como administrador, desejo cadastrar novas turmas e alocar um professor responsável, para preparar o ambiente acadêmico do semestre.
* **Critérios de Aceitação:**
  * A turma deve ter um nome, semestre/ano de referência e um professor vinculado obrigatoriamente.
  * O sistema deve gerar um código único ou link de convite para a turma recém-criada.

### US06 - Acessar Materiais Didáticos
* **Descrição:** Como estudante, desejo baixar os materiais de apoio publicados pelo professor, para estudar o conteúdo das aulas offline.
* **Critérios de Aceitação:**
  * O download dos arquivos deve iniciar corretamente ao clicar no anexo.
  * Os materiais devem ficar organizados em uma aba ou seção específica da disciplina.
