---
title: Recurso de transmissão de atividades
seo-title: Recurso de transmissão de atividades
description: Atividades de um membro da comunidade com sessão iniciada
seo-description: Atividades de um membro da comunidade com sessão iniciada
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Recurso de transmissão de atividades{#activity-streams-feature}

## Introdução {#introduction}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras pela configuração do `Activity Streams` componente.

A capacidade de seguir adiciona outra visão das atividades quando os membros da comunidade seguem postagens de interesse ou atividades de outros membros da comunidade.

O documento descreve:

* adicionar o componente de Fluxos de atividade a um site do AEM
* configurações do componente de Fluxos de atividade

### Adicionar fluxos de atividade a uma página {#adding-activity-streams-to-a-page}

Se desejar adicionar um `Activity Streams` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Activity Streams`

e arraste-o para o lugar em uma página onde os fluxos de atividade devem aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/essentials-activities.md#essentials-for-client-side) necessárias forem incluídas, o `Activity Streams` componente aparecerá desta forma:

![chlimage_1-24](assets/chlimage_1-24.png)

### Configuração de fluxos de atividade {#configuring-activity-streams}

Selecione o componente inserido a ser acessado e selecione o `Activity Streams` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-25](assets/chlimage_1-25.png)

Na guia Atividades **do** usuário, especifique as atividades a serem exibidas:

![chlimage_1-26](assets/chlimage_1-26.png)

* **Número máximo de atividades** o número de atividades a serem exibidas

* **Caminho** do recurso de fluxo Deixe em branco para o padrão do site da comunidade ou do grupo da comunidade. O caminho do recurso de fluxo identifica a origem das atividades. O padrão está em branco.

* **Exibir visualização** de atividades do usuário se marcada, a página de atividades incluirá uma guia que filtra as atividades com base nas geradas na comunidade pelo membro atual. O padrão está marcado.

* **Exibir a exibição** de todas as atividades, se marcada, a página de atividades incluirá uma guia que inclui todas as atividades geradas na comunidade às quais o membro atual tem acesso. O padrão está marcado.

* **Exibir exibição** seguinte se marcada, a página de atividades incluirá uma guia que filtra as atividades com base nas atividades que o membro atual está seguindo. O padrão está marcado.

### Exibição Seguinte {#following-view}

Os componentes devem ser configurados para permitir o seguinte. Os recursos que permitem o seguinte são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca](/help/communities/file-library.md)[](/help/communities/comments.md)e comentários.

![chlimage_1-27](assets/chlimage_1-27.png)

O botão **Seguir **fornece um meio de seguir entradas como atividades, [notificações](/help/communities/notifications.md)ou [assinaturas](/help/communities/subscriptions.md). Sempre que o botão **Seguir **for selecionado, é possível ativar ou desativar uma seleção. A `Email Subscriptions` seleção só está presente quando configurada.

Se algum método de seguir for selecionado, o texto do botão mudará para **Seguinte**. Para sua conveniência, é possível optar por desativar todos os métodos `Unfollow All` .

O botão **Seguir **será exibido

* ao visualizar o perfil de outro membro
* em uma página principal de recursos, como fóruns, QnA e blogs

   * segue toda a atividade desse recurso geral

* para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog

   * segue toda a atividade dessa entrada específica

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Activity Streams Essentials](/help/communities/essentials-activities.md) para desenvolvedores.
