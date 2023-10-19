---
title: Recurso de fluxos de atividade
description: Saiba como as atividades de um membro da comunidade conectado são coletadas em um fluxo que pode ser filtrado e exibido por meio do componente Fluxos de atividade.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 4%

---

# Recurso de fluxos de atividade {#activity-streams-feature}

## Introdução {#introduction}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras por meio da configuração do `Activity Streams` componente.

A capacidade de seguir o adiciona outra visualização de atividades quando os membros da comunidade seguem postagens de interesse ou seguem as atividades de outros membros da comunidade.

O documento descreve:

* Adicionar o componente Fluxos de atividade a um site de AEM
* Configurações do componente de Fluxos de atividade

### Adicionar fluxos de atividade a uma página {#adding-activity-streams-to-a-page}

Se desejar adicionar um `Activity Streams` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Activity Streams`

E arraste-o para o local em uma página onde os fluxos de atividade devem aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-activities.md#essentials-for-client-side) são incluídos, é assim que a variável `Activity Streams` é exibido:

![fluxos de atividade](assets/activity-component.png)

### Configuração de fluxos de atividade {#configuring-activity-streams}

Selecione o colocado `Activity Streams` para que você possa acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

No **Atividades do usuário** especifique quais atividades serão exibidas:

![user-activities](assets/user-activities.png)

* **Número máximo de atividades**

  O número de atividades a serem exibidas

* **Caminho do recurso do fluxo**

  Deixe em branco para definir como padrão o site da comunidade ou o grupo da comunidade. O caminho do recurso de fluxo identifica a origem das atividades. O padrão é em branco.

* **Visualização Exibir atividades do usuário**

  Se marcada, a página de atividades inclui uma guia que filtra atividades com base naquelas geradas dentro da comunidade pelo membro atual. O padrão está marcado.

* **Visualização Exibir todas as atividades**

  Se marcada, a página de atividades inclui uma guia que inclui todas as atividades geradas na comunidade à qual o membro atual tem acesso. O padrão está marcado.

* **Mostrar exibição seguinte**

  Se marcada, a página de atividades incluirá uma guia que filtra as atividades com base naquelas que o membro atual está seguindo. O padrão está marcado.

### Exibição Seguinte {#following-view}

Os componentes devem ser configurados para permitir o acompanhamento. Os recursos que permitem seguir são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca de arquivos](/help/communities/file-library.md), e [comentários](/help/communities/comments.md).

![following-view](assets/following-activities.png)

A variável **Seguir** fornece um meio de seguir entradas como atividades, [notificações](/help/communities/notifications.md)ou [assinaturas](/help/communities/subscriptions.md). Cada vez que a variável **Seguir** for selecionada, é possível ativar ou desativar uma seleção. A variável `Email Subscriptions` a seleção está presente somente quando configurada.

Se qualquer método de seguir for selecionado, o texto do botão será alterado para **Seguindo**. Por conveniência, é possível selecionar `Unfollow All` para desativar todos os métodos.

A variável **Seguir** é exibido:

* Ao exibir o perfil de outro membro.
* Em uma página principal de recursos, como fóruns, QnA e blogs.

   * Segue todas as atividades desse recurso geral.

* Para uma entrada específica, como um tópico de fórum, pergunta QnA ou artigo de blog.

   * Segue todas as atividades dessa entrada específica.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do Activity Streams](/help/communities/essentials-activities.md) página para desenvolvedores.
