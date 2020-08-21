---
title: Recurso de fluxos de atividade
seo-title: Recurso de fluxos de atividade
description: Atividades de um membro da comunidade conectado
seo-description: Atividades de um membro da comunidade conectado
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 4%

---


# Recurso de fluxos de atividade {#activity-streams-feature}

## Introdução {#introduction}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras pela configuração do `Activity Streams` componente.

A habilidade de seguir adiciona outra visualização de atividades quando os membros da comunidade seguem postagens de interesse ou seguem as atividades de outros membros da comunidade.

O documento descreve:

* Adicionar o componente de Fluxos de Atividade a um site AEM
* Configurações do componente Fluxos de Atividade

### Adicionar fluxos de Atividade a uma página {#adding-activity-streams-to-a-page}

Se desejar adicionar um `Activity Streams` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Activity Streams`

e arraste-o para o lugar em uma página onde os fluxos de atividade devem aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/essentials-activities.md#essentials-for-client-side) necessárias forem incluídas, o `Activity Streams` componente aparecerá desta forma:

![atividades](assets/activity-component.png)

### Configuração de fluxos de Atividade {#configuring-activity-streams}

Selecione o componente inserido a ser acessado e selecione o `Activity Streams` `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Na guia **Atividades** do usuário, especifique quais atividades serão exibidas:

![atividades do usuário](assets/user-activities.png)

* **Número máximo de atividades**

   O número de atividades a serem exibidas

* **Caminho do recurso do fluxo**

   Deixe em branco como padrão para o site da comunidade ou grupo da comunidade. O caminho do recurso de fluxo identifica a origem do atividade. O padrão está em branco.

* **Visualização Exibir atividades do usuário**

   Se marcada, a página atividades incluirá uma guia que filtros atividades com base naqueles gerados na comunidade pelo membro atual. O padrão está marcado.

* **Visualização Exibir todas as atividades**

   Se marcada, a página atividades incluirá uma guia que inclui todas as atividades geradas na comunidade à qual o membro atual tem acesso. O padrão está marcado.

* **Mostrar exibição seguinte**

   Se marcada, a página atividades incluirá uma guia que filtros atividades com base naqueles que o membro atual está seguindo. O padrão está marcado.

### Visualização seguinte {#following-view}

Os componentes devem ser configurados para permitir o seguinte. Os recursos que permitem o seguinte são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca](/help/communities/file-library.md)[](/help/communities/comments.md)e comentários.

![visualização seguinte](assets/following-activities.png)

O botão **Seguir** fornece um meio de seguir entradas como atividades, [notificações](/help/communities/notifications.md)ou [subscrições](/help/communities/subscriptions.md). Cada vez que o botão **Seguir** é selecionado, é possível ativar ou desativar uma seleção. A `Email Subscriptions` seleção só está presente quando configurada.

Se algum método de seguir for selecionado, o texto do botão mudará para **Seguinte**. Para sua conveniência, é possível selecionar `Unfollow All` alternar todos os métodos.

O botão **Seguir** será exibido:

* Ao exibir o perfil de outro membro.
* Em uma página principal de recursos, como fóruns, QnA e blogs.

   * Segue toda a atividade desse recurso geral.

* Para uma entrada específica, como um tópico do fórum, uma pergunta de QnA ou um artigo do blog.

   * Segue toda a atividade para essa entrada específica.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Atividade Streams Essentials](/help/communities/essentials-activities.md) para desenvolvedores.
