---
title: Introdução ao AEM Forms
seo-title: Introduction to AEM Forms
description: Com o Adobe Experience Manager Forms, os usuários empresariais podem integrar formulários envolventes, responsivos e adaptáveis em sites da Web e móveis, simplificando o processo de inscrição digital e aumentando as taxas de conversão do cliente.
seo-description: With Adobe Experience Manager Forms, business users can integrate engaging, responsive, and adaptive forms into web and mobile sites, simplifying the digital enrollment process and increasing customer conversion rates.
uuid: a6564997-4227-4d5d-b27d-47a55a386238
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: introduction
discoiquuid: a20383f2-f86a-45bf-a39e-725ee764503b
docset: aem65
feature: Adaptive Forms
exl-id: e5533b4f-93b7-4ea9-a01d-fdf9528652c8
source-git-commit: 41ef1b05e4082bb50b93ff6511542ed56a77497c
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 11%

---

# Introdução ao AEM Forms{#introduction-to-aem-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html) |
| AEM 6.5 | Este artigo |

Para obter informações sobre os recursos e aprimoramentos mais recentes do AEM Forms, consulte [Novidades do AEM Forms](../../forms/using/whats-new.md).

## Sobre o AEM Forms {#about-aem-forms}

O Adobe Experience Manager (AEM) fornece uma solução fácil de usar para criar, gerenciar, publicar e atualizar formulários digitais complexos e, ao mesmo tempo, integrar-se a processos de back-end, regras de negócios e dados.

O AEM Forms combina criação, gerenciamento e publicação de formulários, juntamente com recursos de gerenciamento de correspondência, segurança de documentos e análise integrada para criar experiências envolventes de ponta a ponta. Projetado para funcionar em canais móveis e da Web, o AEM Forms pode ser integrado com eficiência aos seus processos de negócios, reduzindo processos e erros de papel e, ao mesmo tempo, melhorando a eficiência.

Frequentemente em grandes empresas, os formulários são criados uma vez e reutilizados, por meio de uma cópia enviada para um sistema de gerenciamento de conteúdo. Manter um grande banco de dados de formulários atualizado e torná-los detectáveis pode ser um desafio considerável. O AEM fornece um portal de formulários personalizável que garante que os clientes encontrem e acessem os formulários de que precisam, tanto na web quanto em canais móveis.

O AEM Forms fornece ferramentas de gerenciamento de formulários que permitem não apenas gerenciar formulários adaptáveis, mas também formulários XFA, PDF forms e ativos relacionados. Para obter mais informações, consulte [Introdução ao gerenciamento de formulários](../../forms/using/introduction-managing-forms.md).

>[!NOTE]
>
>O recurso do AEM Forms, como o Adaptive Forms, disponível em [QuickStart do AEM 6.5](/help/sites-deploying/deploy.md), destinam-se apenas a fins de exploração e avaliação. Para uso em produção, é essencial obter uma licença válida para o AEM Forms.


![Recursos de formulários AEM](do-not-localize/4th-draft.gif)

### Principais recursos {#key-capabilities}

Resumindo, a AEM Forms fornece recursos avançados de gerenciamento de formulários, como os descritos a seguir, que reduzem os processos manuais e aumentam a satisfação do cliente.

* Um portal centralizado do Forms para criação e implantação de formulários dinâmicos, incluindo PDF, HTML e formulários adaptáveis
* Uma interface gráfica de usuário fácil de usar que permite aos usuários empresariais importar, gerenciar, visualizar e publicar formulários com facilidade
* Um diretório responsivo de formulários com recursos avançados de pesquisa usando palavras-chave, tags e metadados
* Detecção dinâmica do dispositivo e do local de um usuário para renderizar o formulário adequadamente na Web e em canais móveis
* Integração com o Adobe Analytics para medir com eficiência as métricas de uso do formulário
* Integração com os serviços do Adobe Document Cloud eSign ou Rabiscar para assinar eletronicamente documentos contendo informações confidenciais
* Recursos automatizados de publicação de formulários e capacidade de fornecer comunicação pontual, personalizada e consistente por meio de vários canais

## Tipos de formulário AEM {#aem-form-types}

O AEM Forms permite estender formulários novos e existentes para criar:

* HTML e PDF forms perfeitos em pixels e paginados que se parecem quase com papel ou
* formulários adaptáveis que são renderizados automaticamente para o dispositivo e o navegador de um usuário.

**PDF forms**

Os PDF forms podem ser preenchidos off-line, salvos localmente e os dados do formulário podem ser enviados quando você estiver on-line. Você pode usar códigos de barras 2D para capturar dados de formulário e usar assinaturas digitais para validar a autenticidade para os usuários.

**formulários HTML**

Os formulários baseados em navegador do HTML5 podem ser visualizados em dispositivos móveis e navegadores de desktop. Você pode assinar eletronicamente os formulários HTML usando os serviços Scribble ou eSign.

**Formulários adaptáveis**

Os formulários adaptáveis podem se adaptar dinamicamente às respostas do usuário, adicionando ou removendo campos ou seções, conforme necessário. O AEM permite que você reutilize modelos de formulário Adobe XML para criar formulários adaptáveis.

### Recursos compatíveis {#supported-features}

Todos os tipos de formulários são compatíveis com os seguintes recursos:

* Layout dinâmico
* Validação do campo de formulário
* Ajuda contextual
* Processamento de scripts e manipulação de dados XML
* Design e verificação de acessibilidade
* Capacidade de salvar formulários no lado do servidor
* Suporte para anexos de arquivo
* Integração com o HTML Workspace para captura de dados

## Coleção de dados offline {#offline-data-collection}

Depois que os dados de formulário são enviados, o Adobe Experience Manager conecta os dados de formulário com os sistemas existentes, as regras de negócios e as pessoas necessárias.

A AEM Forms fornece o Forms Workspace, um aplicativo móvel que estende seus processos de negócios digitais para dispositivos móveis. Usando o Forms Workspace, você pode coletar e registrar dados mesmo quando estiver offline. O Forms Workspace usa os recursos do seu dispositivo móvel e permite capturar fotos, vídeos e coletar dados, como carimbos de data e hora e outras informações. Na próxima vez que você se conectar a uma rede, poderá sincronizar os dados coletados.

Capturar dados offline e sincronizá-los na próxima vez que você voltar online é especialmente útil para as pessoas no campo. Aumenta a produtividade e reduz erros.

**Vantagens de usar o Forms Workspace para a coleta de dados offline**

* Aplicativo de espaço de trabalho HTML fácil de usar para atribuição e rastreamento de tarefas
* Arrastar e soltar o ambiente de design do fluxo de trabalho
* Conectores de gerenciamento de conteúdo corporativo (ECM)
* Suporte a padrões abertos, incluindo XML e SOAP para conectar dados de formulários a sistemas corporativos
* Relatórios de HTML prontos para uso monitoram backlogs, filas de trabalho e Indicadores-chave de desempenho (KPIs)
* Painéis personalizáveis para obter insights em tempo real sobre as operações de negócios
* API para conexão com ferramentas de relatórios de terceiros

![Terceira versão](do-not-localize/3rd-draft.gif)

## Comunicação personalizada {#personalized-communication}

Uma parte importante de uma experiência digital de autoatendimento eficiente é fornecer informações oportunas e personalizadas que os usuários possam acessar de qualquer lugar e em qualquer dispositivo. Comunicações personalizadas e oportunas podem melhorar as taxas de conversão e a satisfação do usuário.

Usando o AEM Forms, os usuários empresariais podem criar experiências de usuário personalizadas atraentes personalizando modelos de documentos, incorporando informações de processos de back-end e incluindo componentes interativos. Uma interface de usuário intuitiva ajuda usuários não técnicos a desenvolver regras de negócios que decidem quando gerar uma comunicação com base em uma consulta ou iniciar uma resposta gerada pelo usuário.

Documentos personalizados, como recibos, kits de boas-vindas e demonstrativos, podem ser facilmente entregues em vários canais. As organizações podem direcionar o tráfego para portais da web personalizados, resultando na inscrição ou compra de serviços adicionais.

**Principais recursos**

* Ambiente de criação de correspondência com suporte para modelos, blocos de conteúdo, regras de negócios e muito mais
* Conversão e montagem de documentos
* Suporte para entrega de documentos sob demanda ou em lote por meio de vários canais, incluindo Web, email e papel
* Trilhas de auditoria com histórico de alterações
* Compatibilidade com assinaturas digitais para validar a integridade do conteúdo e a identidade do signatário
* Complemento de segurança de documentos para o AEM Forms, incluindo criptografia, políticas de uso, rastreamento e auditoria

![Layout dois](do-not-localize/layout-02.png)

Fluxo de trabalho de comunicação personalizado simplificado

