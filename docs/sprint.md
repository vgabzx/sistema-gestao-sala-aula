# Diário de Sprint

Este documento regista a organização da nossa equipa (consultoria), a divisão de tarefas ao longo das Sprints e as lições aprendidas durante a conceção e modelação do Sistema de Gestão de Sala de Aula Online.

## 1. Organização e Divisão de Tarefas
A equipa utilizou o **GitHub Projects (Kanban)** para gerir o fluxo de trabalho. As responsabilidades foram divididas de forma a garantir que todos os membros participassem ativamente e deixassem o seu registo (commits) no repositório.

* **Gabriel Ferrazza:** Configuração inicial do repositório, gestão do Kanban, estruturação do README e elaboração da Visão do Produto e Stakeholders.
* **Gabriel Mathias:** Levantamento de Regras de Negócio, definição de User Stories e auxílio na modelação do MVP.
* **Leonardo Bernardi:** Definição da Arquitetura de Software (decisões arquiteturais) e desenvolvimento dos diagramas C4.
* **Thiago Rodrigues:** Modelação de processos (BPMN) e criação do diagrama de Casos de Uso (UML).

*(Nota: Todos os membros reviram os documentos uns dos outros para garantir a coerência do projeto).*

## 2. Dificuldades Encontradas e Soluções Adotadas

* **Dificuldade 1:** Dúvida sobre o nível de detalhe no MVP vs. Funcionalidades Futuras.
  * **Solução:** Focámo-nos no problema central (entrega de trabalhos e comunicação). Tudo o que não era essencial para um professor avaliar um aluno (como videochamadas ou fóruns complexos) foi movido para o backlog futuro.

* **Dificuldade 2:** Integração das Regras de Negócio na Arquitetura.
  * **Solução:** Debatemos em equipa como a regra de "bloquear a exclusão de atividades com submissões" impactaria a base de dados. Decidimos documentar a necessidade de restrições de chaves estrangeiras (Foreign Keys) na nossa decisão de usar uma Base de Dados Relacional.

* **Dificuldade 3:** Organização dos diagramas no GitHub sem perder qualidade.
  * **Solução:** Optámos por desenhar os diagramas em ferramentas externas (como Draw.io/Lucidchart), exportar as imagens em alta resolução (PNG) e criar ficheiros `README.md` dentro das pastas (`uml/`, `bpmn/`, `c4/`) para exibir as imagens de forma documentada.
