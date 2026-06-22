# User Stories (Histórias de Usuário)

Este documento contém os requisitos do sistema descritos sob a perspectiva do usuário. As histórias cobrem os principais casos de uso representados no Diagrama de Casos de Uso (UML), garantindo a rastreabilidade entre requisitos e modelagem.

### US01 - Criar/Publicar Atividade
* **Descrição:** Como professor, desejo criar e publicar uma nova atividade com título, descrição e prazo de entrega, para que os estudantes possam realizar as tarefas da disciplina.
* **Critérios de Aceitação:**
  * O professor deve definir obrigatoriamente um título e uma data limite.
  * O sistema deve permitir anexar arquivos à atividade.
  * Após a publicação, todos os estudantes matriculados na turma devem visualizar a atividade no mural e receber uma notificação automática.

### US02 - Entregar Atividade
* **Descrição:** Como estudante, desejo anexar arquivos e enviar minha resposta a uma atividade, para que o professor possa avaliá-la.
* **Critérios de Aceitação:**
  * O sistema deve aceitar arquivos em formatos comuns (PDF, DOCX, JPG).
  * O estudante deve receber uma confirmação visual de que a entrega foi registrada com sucesso, com data e hora.
  * O sistema deve bloquear envios após o prazo estabelecido, caso o professor não tenha habilitado entregas com atraso.

### US03 - Corrigir e Atribuir Nota e Feedback
* **Descrição:** Como professor, desejo visualizar as entregas dos estudantes e atribuir uma nota e um comentário, para dar o retorno adequado sobre o desempenho deles.
* **Critérios de Aceitação:**
  * O professor deve poder inserir uma nota de 0 a 100.
  * O campo de feedback textual é opcional.
  * Assim que a nota for salva, o estudante correspondente deve receber uma notificação e conseguir visualizar a correção no seu painel.

### US04 - Visualizar Mural e Atividades
* **Descrição:** Como estudante, desejo visualizar um mural cronológico com avisos, novos materiais e atividades, para me manter atualizado sobre a disciplina.
* **Critérios de Aceitação:**
  * As postagens mais recentes devem aparecer no topo do mural.
  * Cada postagem deve indicar claramente o nome de quem publicou e a data da publicação.

### US05 - Criar Turma
* **Descrição:** Como professor, desejo criar turmas dentro de uma disciplina e gerar um código de convite, para preparar o ambiente acadêmico e permitir a entrada dos estudantes.
* **Critérios de Aceitação:**
  * A turma deve ter um nome e um semestre/ano de referência.
  * A turma deve ficar vinculada ao professor que a criou (RN07).
  * O sistema deve gerar um código único (ou link de convite) para a turma recém-criada.

### US06 - Acessar Materiais Didáticos
* **Descrição:** Como estudante, desejo baixar os materiais de apoio publicados pelo professor, para estudar o conteúdo das aulas.
* **Critérios de Aceitação:**
  * O download dos arquivos deve iniciar corretamente ao clicar no anexo.
  * Os materiais devem ficar organizados em uma aba ou seção específica da disciplina.

### US07 - Matricular-se em Turma
* **Descrição:** Como estudante, desejo matricular-me em uma turma informando o código de convite, para acessar seus conteúdos e atividades.
* **Critérios de Aceitação:**
  * O estudante deve conseguir ingressar na turma ao informar um código de convite válido.
  * Caso a matrícula já tenha sido sincronizada pelo Sistema Acadêmico (SIS), o estudante deve visualizar a turma automaticamente, sem necessidade do código.
  * Um código inválido ou expirado deve exibir mensagem de erro.

### US08 - Enviar Comunicado
* **Descrição:** Como professor, desejo enviar comunicados e avisos para a minha turma, para manter os estudantes informados sobre a disciplina.
* **Critérios de Aceitação:**
  * O comunicado deve ser publicado no mural da turma.
  * Todos os estudantes matriculados devem receber uma notificação do novo comunicado.

### US09 - Gerenciar Usuários e Permissões
* **Descrição:** Como administrador, desejo cadastrar usuários e gerenciar suas permissões, para controlar o acesso e os papéis dentro da plataforma.
* **Critérios de Aceitação:**
  * O administrador deve poder cadastrar e desativar usuários.
  * O administrador deve poder atribuir os papéis (estudante, professor, coordenador).
  * Apenas usuários com perfil de administrador podem acessar essas funções (RN03).

### US10 - Acompanhar Desempenho das Turmas
* **Descrição:** Como coordenador, desejo acompanhar relatórios de desempenho e engajamento das turmas, para supervisionar o andamento pedagógico.
* **Critérios de Aceitação:**
  * O coordenador deve visualizar indicadores consolidados por turma (ex.: entregas realizadas, médias de notas).
  * Os relatórios devem poder ser filtrados por disciplina, turma ou período.
