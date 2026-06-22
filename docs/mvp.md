# Produto Mínimo Viável (MVP)

O MVP (Minimum Viable Product) define o conjunto estritamente necessário de funcionalidades para que o sistema possa ser lançado, testado e comece a gerar valor imediato para professores e estudantes.

> **Observação sobre escopo x arquitetura:** Os diagramas C4 representam a **arquitetura-alvo** completa da solução (incluindo serviços e clientes que serão totalmente explorados em versões futuras). O MVP descrito abaixo é um **recorte de escopo** dessa arquitetura: ele entrega o ciclo essencial de ensino e avaliação sobre a mesma base arquitetural híbrida, evitando retrabalho estrutural à medida que novas funcionalidades forem incorporadas.

## 1. Funcionalidades Essenciais (MVP)
Para a primeira versão da plataforma, o foco é o ciclo básico de ensino e avaliação. As funcionalidades incluem:
* Autenticação dos usuários via SSO (Provedor de Identidade institucional).
* Cadastro de usuários e gestão de permissões (perfil Administrador).
* Criação de turmas e geração de código de convite (perfil Professor).
* Matrícula dos estudantes por código de convite e sincronização básica de matrículas com o Sistema Acadêmico (SIS).
* Mural da turma para publicação de avisos, comunicados e materiais didáticos.
* Criação/publicação de atividades pelo professor (com título, descrição e prazo).
* Entrega de atividades (upload de arquivos para o armazenamento em nuvem) pelos estudantes.
* Atribuição de notas e feedback pelo professor.
* Notificações automáticas essenciais (nova atividade publicada e nota disponível), entregues de forma assíncrona pelo Serviço de Notificações.

## 2. Funcionalidades Futuras (Backlog)
Recursos que agregam valor, mas não são críticos para o funcionamento inicial, sendo priorizados para versões posteriores:
* Aplicativo mobile completo (a arquitetura já prevê o cliente mobile, mas a primeira entrega prioriza o cliente web).
* Relatórios e dashboards analíticos avançados de desempenho e engajamento para a coordenação.
* Fórum de discussões integrado para cada disciplina.
* Integração nativa com ferramentas de videochamada (ex.: Google Meet, Zoom).
* Criação de questionários online com correção automática (múltipla escolha).
* **Feedback assistido por IA** (funcionalidade inovadora — ver `docs/funcionalidade-inovadora.md`).

## 3. Justificativa da Priorização
A priorização foi baseada no problema central identificado na Visão do Produto: a desorganização na comunicação e na gestão de entregas. O MVP resolve diretamente essa dor primária, garantindo um ambiente centralizado onde o professor cria turmas, conduz sua disciplina e avalia os estudantes com eficiência, e onde o estudante se matricula, entrega trabalhos e recebe retorno.

As notificações essenciais foram incluídas no MVP porque são parte indissociável do processo de entrega modelado no BPMN (avisar professor sobre nova entrega e avisar estudante sobre nota disponível). Já funcionalidades de maior esforço técnico — como o app mobile completo, dashboards analíticos, videochamada e o feedback com IA — foram adiadas para garantir a entrega rápida de um produto funcional, permitindo validar o fluxo básico com os usuários antes de investir na construção dos módulos mais complexos. Como esses módulos já estão previstos na arquitetura híbrida (serviços assíncronos desacoplados via *message broker*), sua adição posterior não exige reestruturação do núcleo.
