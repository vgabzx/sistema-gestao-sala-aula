# Funcionalidade Inovadora — Feedback Assistido por IA

## 1. Descrição
A funcionalidade inovadora do EduClass é o **Feedback Assistido por Inteligência Artificial**. Ao corrigir uma entrega, o professor pode acionar um assistente que analisa a submissão do estudante e gera uma **sugestão de feedback** (pontos fortes, pontos a melhorar e observações), além de uma **sugestão de nota** dentro da escala de 0 a 100.

O foco é o apoio à decisão: a IA produz um rascunho, mas **o professor mantém sempre a palavra final**, podendo editar, aceitar ou descartar a sugestão antes de publicá-la. Isso respeita a RN01 (a autoria da avaliação permanece com o professor) e a RN05 (escala de notas).

## 2. Benefício Esperado
* **Redução do tempo de correção:** o professor parte de um rascunho estruturado em vez de uma folha em branco, acelerando turmas numerosas.
* **Feedback mais rico e padronizado:** estudantes recebem retornos mais detalhados e consistentes, melhorando a aprendizagem.
* **Apoio, não substituição:** preserva o julgamento pedagógico do docente, que valida cada sugestão.

## 3. Viabilidade Técnica
A funcionalidade é viável por meio da integração com uma API de modelo de linguagem (LLM). O fluxo proposto:
1. O professor solicita a sugestão de feedback para uma submissão específica.
2. O núcleo da aplicação publica um evento de "solicitação de feedback" no Message Broker.
3. Um **Serviço de Feedback IA** (assíncrono, consumidor de eventos) recupera o conteúdo da submissão do Armazenamento em Nuvem, monta o *prompt* com o enunciado e os critérios da atividade e chama a API do LLM.
4. A sugestão retornada é persistida e disponibilizada ao professor na tela de correção, marcada claramente como "rascunho gerado por IA".

O processamento assíncrono evita travar a interface do professor enquanto a IA gera a resposta, e o uso de eventos reaproveita a infraestrutura de mensageria já existente.

## 4. Possíveis Impactos Arquiteturais
* **Novo serviço assíncrono:** adição de um **Serviço de Feedback IA** ao conjunto de serviços consumidores do Message Broker (mesmo padrão dos serviços de Notificações e Relatórios), reforçando a escolha da arquitetura híbrida com publish-subscribe.
* **Nova integração externa:** dependência de um **Provedor de LLM** (API externa), que passa a ser um sistema externo no Diagrama de Contexto.
* **Requisitos não funcionais:** atenção a privacidade dos dados dos estudantes (o que é enviado ao provedor), custo por requisição e tratamento de indisponibilidade da API externa (a correção manual deve continuar funcionando caso a IA falhe).

> **Observação:** Esta funcionalidade ainda não está representada nos diagramas atuais. Ao refinarmos o C4, recomenda-se adicionar o "Serviço de Feedback IA" (container) e o "Provedor de LLM" (sistema externo) para manter a rastreabilidade entre documentação e modelagem.
