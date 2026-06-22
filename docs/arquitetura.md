# Arquitetura de Software

## 1. Estilo Arquitetural Escolhido
A arquitetura escolhida para o Sistema de Gestão de Sala de Aula Online (EduClass) é uma **Arquitetura Híbrida**, composta por:

* um **núcleo monólito modular organizado em camadas** (Apresentação → Aplicação → Domínio → Persistência), responsável pelo domínio principal do sistema (Usuários, Turmas, Atividades e Avaliação); e
* **serviços assíncronos desacoplados**, integrados ao núcleo por meio de um *Message Broker* no padrão **Publish-Subscribe**, responsáveis por tarefas que não devem bloquear o fluxo principal (Notificações e Relatórios).

**Justificativa:** Um monólito puramente em camadas simplificaria o desenvolvimento, mas concentraria no mesmo processo tarefas de naturezas muito diferentes — por exemplo, o envio de notificações por e-mail/push e a geração de relatórios, que são operações potencialmente lentas e de pico variável. Por outro lado, uma arquitetura totalmente baseada em microsserviços traria complexidade operacional excessiva para o escopo do projeto. A abordagem híbrida equilibra os dois mundos: mantém o domínio central coeso e de fácil manutenção em um monólito modular em camadas (garantindo consistência transacional forte para dados acadêmicos), ao mesmo tempo em que **desacopla operações assíncronas e de carga variável** em serviços independentes, comunicados por eventos. Isso melhora a escalabilidade, a resiliência (uma falha no serviço de notificações não derruba a entrega de atividades) e permite o uso de tecnologias adequadas a cada tarefa (*polyglot*).

## 2. Visão de Containers (resumo do C4 - Nível 2)
* **Clientes:** Aplicação Web (SPA em React + TypeScript) e Aplicativo Mobile (React Native).
* **API Gateway** (Spring Cloud Gateway): ponto único de entrada, responsável pelo roteamento das requisições e pela validação de autenticação/autorização.
* **Núcleo da Aplicação** (Monólito Modular em Java + Spring Boot): módulos de Turmas, Atividades, Avaliação e Usuários, organizados nas camadas Apresentação → Aplicação → Domínio → Persistência.
* **Message Broker** (RabbitMQ/Kafka): canal de eventos no padrão Publish-Subscribe.
* **Serviço de Notificações** (Node.js): consome eventos e dispara notificações por e-mail/push.
* **Serviço de Relatórios** (Python): consome eventos e processa relatórios de desempenho de forma assíncrona.
* **Banco de Dados** (PostgreSQL): persistência transacional do núcleo.
* **Sistemas Externos:** Provedor de Identidade (OAuth/SSO), Sistema Acadêmico (SIS), Armazenamento em Nuvem e Serviço de E-mail/Push.

## 3. Decisões Arquiteturais

Para suportar a solução proposta, definimos as seguintes decisões arquiteturais:

* **Decisão 1: Adoção de uma Arquitetura Híbrida (núcleo monólito modular em camadas + serviços assíncronos publish-subscribe).**
  * **Justificativa:** Mantém o domínio acadêmico coeso e simples de evoluir, enquanto isola tarefas assíncronas e de carga variável (notificações e relatórios) em serviços desacoplados. Evita tanto a rigidez de um monólito único quanto a complexidade operacional de microsserviços plenos, sendo adequada ao escopo e à equipe do projeto.

* **Decisão 2: Separação entre Cliente e Servidor (Clientes SPA/Mobile + Backend via API Gateway).**
  * **Justificativa:** O uso de uma API exposta por um API Gateway permite que o backend atenda a múltiplos clientes (web e mobile) de forma uniforme. Essa separação também permite que diferentes integrantes da equipe trabalhem no front e no back simultaneamente.

* **Decisão 3: Autenticação delegada a um Provedor de Identidade externo via OAuth 2.0 / OpenID Connect (SSO), com tokens JWT validados no API Gateway.**
  * **Justificativa:** Delegar a autenticação ao IdP institucional habilita o Login Único (SSO) e evita o gerenciamento direto de senhas pela plataforma. Os tokens emitidos são JWT, validados de forma *stateless* no API Gateway, que aplica autorização baseada em papéis (RBAC). Isso atende diretamente à RN01, bloqueando que estudantes acessem operações exclusivas de professores, e ao requisito não funcional de Segurança.

* **Decisão 4: Comunicação assíncrona via Message Broker (RabbitMQ/Kafka) no padrão Publish-Subscribe.**
  * **Justificativa:** Operações como notificar professores/estudantes e gerar relatórios não devem bloquear o fluxo principal de entrega e correção (conforme o BPMN). O núcleo publica eventos (ex.: "nova entrega", "nota lançada") e os serviços de Notificações e Relatórios os consomem de forma independente, aumentando a escalabilidade e a resiliência do sistema.

* **Decisão 5: Banco de Dados Relacional (PostgreSQL) para o núcleo transacional.**
  * **Justificativa:** O domínio acadêmico possui dados altamente estruturados e relacionamentos fortes (uma Disciplina possui Turmas; uma Turma possui Estudantes e Atividades; uma Atividade possui Submissões). O banco relacional garante integridade referencial, bloqueando ações indevidas como a exclusão de uma atividade que já possui submissões (RN06).

* **Decisão 6: Integração com sistemas institucionais externos.**
  * **Justificativa:** Para evitar cadastros duplicados e centralizar dados oficiais, a plataforma integra-se ao **Sistema Acadêmico (SIS)** via REST (sincronização de matrículas — RN08), ao **Armazenamento em Nuvem** para guardar anexos de atividades (escalabilidade de arquivos) e ao **Serviço de E-mail/Push** para a entrega efetiva das notificações.
