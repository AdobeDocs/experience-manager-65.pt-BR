---
title: Recurso de fluxos de atividade
description: Saiba como as atividades de um membro da comunidade conectado são coletadas em um fluxo que pode ser filtrado e exibido por meio do componente Fluxos de atividade.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Recurso de fluxos de atividade {#activity-streams-feature}

## Introdução {#introduction}

As atividades de um membro da comunidade conectado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras por meio da configuração do componente `Activity Streams`.

A capacidade de seguir o adiciona outra visualização de atividades quando os membros da comunidade seguem postagens de interesse ou seguem as atividades de outros membros da comunidade.

O documento descreve:

* Adicionar o componente Fluxos de atividade a um site de AEM
* Configurações do componente de Fluxos de atividade

### Adicionar fluxos de atividade a uma página {#adding-activity-streams-to-a-page}

Se quiser adicionar um componente `Activity Streams` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Activity Streams`

E arraste-o para o local em uma página onde os fluxos de atividade devem aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-activities.md#essentials-for-client-side) são incluídas, é assim que o componente `Activity Streams` aparece:

![fluxos-atividade](assets/activity-component.png)

### Configuração de fluxos de atividade {#configuring-activity-streams}

Selecione o componente `Activity Streams` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **Atividades do usuário**, especifique quais atividades exibir:

![atividades-usuário](assets/user-activities.png)

* **Número máximo de atividades**

  O número de atividades a serem exibidas

* **Caminho do recurso do fluxo**

  Deixe em branco para definir como padrão o site da comunidade ou o grupo da comunidade. O caminho do recurso de fluxo identifica a origem das atividades. O padrão é em branco.

* **Exibir Exibição de Atividades do Usuário**

  Se marcada, a página de atividades inclui uma guia que filtra atividades com base naquelas geradas dentro da comunidade pelo membro atual. O padrão está marcado.

* **Exibir Todas As Atividades**

  Se marcada, a página de atividades inclui uma guia que inclui todas as atividades geradas na comunidade à qual o membro atual tem acesso. O padrão está marcado.

* **Exibir a seguinte exibição**

  Se marcada, a página de atividades incluirá uma guia que filtra as atividades com base naquelas que o membro atual está seguindo. O padrão está marcado.

### Exibição Seguinte {#following-view}

Os componentes devem ser configurados para permitir o acompanhamento. Os recursos que permitem os seguintes itens são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [biblioteca de arquivos](/help/communities/file-library.md) e [comentários](/help/communities/comments.md).

![exibição seguinte](assets/following-activities.png)

O botão **Seguir** fornece um meio de seguir entradas como atividades, [notificações](/help/communities/notifications.md) ou [assinaturas](/help/communities/subscriptions.md). Sempre que o botão **Seguir** é selecionado, é possível ativar ou desativar uma seleção. A seleção `Email Subscriptions` está presente somente quando configurada.

Se qualquer método de acompanhamento for selecionado, o texto do botão será alterado para **Seguinte**. Para maior comodidade, é possível selecionar `Unfollow All` para desligar todos os métodos.

O botão **Seguir** é exibido:

* Ao exibir o perfil de outro membro.
* Em uma página principal de recursos, como fóruns, QnA e blogs.

   * Segue todas as atividades desse recurso geral.

* Para uma entrada específica, como um tópico de fórum, pergunta QnA ou artigo de blog.

   * Segue todas as atividades dessa entrada específica.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Activity Streams Essentials](/help/communities/essentials-activities.md) para desenvolvedores.
