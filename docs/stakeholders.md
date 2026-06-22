# Stakeholders (Partes Interessadas)

Os stakeholders representam os principais atores envolvidos no uso, gestão e suporte do Sistema de Gestão de Sala de Aula Online (EduClass).

## Atores Humanos
* **Estudantes:** Usuários com foco na aprendizagem. Acessam a plataforma para matricular-se em turmas, visualizar disciplinas, baixar materiais didáticos, entregar atividades e acompanhar suas notas e feedbacks.
* **Professores:** Usuários responsáveis pela condução pedagógica. Criam turmas, gerenciam conteúdos, publicam atividades, corrigem entregas, lançam avaliações e enviam comunicados à turma.
* **Coordenadores:** Usuários com perfil gerencial. Acompanham o desempenho das turmas e o engajamento dos estudantes por meio de relatórios, supervisionando o andamento dos professores e turmas.
* **Administradores:** Equipe técnica ou de secretaria. Responsáveis pelo cadastro de usuários, gestão de permissões, configuração institucional (semestres, disciplinas e integrações) e suporte técnico à plataforma.

## Sistemas Externos Integrados
Além dos atores humanos, a solução depende de sistemas externos da instituição, que também são partes interessadas do ponto de vista técnico (conforme o Diagrama de Contexto C4):

* **Provedor de Identidade (IdP):** Responsável pela autenticação única (SSO) via OAuth 2.0 / OpenID Connect.
* **Sistema Acadêmico (SIS):** Fonte oficial de matrículas e dados acadêmicos, sincronizados com a plataforma.
* **Armazenamento em Nuvem (Cloud Storage):** Responsável por guardar os anexos e arquivos das atividades.
* **Serviço de E-mail / Push:** Responsável pela entrega das notificações aos usuários.
