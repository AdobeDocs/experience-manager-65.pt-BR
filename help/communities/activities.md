---
title: Recurso Fluxos de atividade
seo-title: Activity Streams Feature
description: Atividades de um membro da comunidade com sessão iniciada
seo-description: Activities of a signed-in community member
uuid: decd2d6c-4d4b-4698-a92c-2b5b441458cf
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 89f3630f-c01a-4dc0-9ff5-169785f22c01
docset: aem65
exl-id: 2b2a5de0-e7c7-4417-a217-4b929bc7dcfb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 4%

---

# Recurso Fluxos de atividade {#activity-streams-feature}

## Introdução {#introduction}

As atividades de um membro da comunidade assinado, como postar em um fórum ou blog, são coletadas em um fluxo que pode ser filtrado e exibido de várias maneiras pela configuração do `Activity Streams` componente.

A capacidade de seguir adiciona outra exibição de atividades quando os membros da comunidade seguem postagens de interesse ou seguem as atividades de outros membros da comunidade.

O documento descreve:

* Adicionar o componente Fluxos de atividade a um site AEM
* Configurações do componente Fluxos de atividade

### Adicionar fluxos de atividade a uma página {#adding-activity-streams-to-a-page}

Se desejar adicionar uma `Activity Streams` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Activity Streams`

e arraste-o para o lugar em uma página onde os fluxos de atividade devem aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-activities.md#essentials-for-client-side) são incluídos, é assim que a variável `Activity Streams` componente aparecerá :

![fluxos de atividades](assets/activity-component.png)

### Configuração de fluxos de atividade {#configuring-activity-streams}

Selecione o `Activity Streams` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

Em **Atividades do usuário** , especifique quais atividades exibir :

![atividades do usuário](assets/user-activities.png)

* **Número máximo de atividades**

   O número de atividades a serem exibidas

* **Caminho do recurso do fluxo**

   Deixe em branco como padrão para o site da comunidade ou grupo da comunidade. O caminho do recurso de fluxo identifica a origem das atividades. O padrão está em branco.

* **Visualização Exibir atividades do usuário**

   Se marcada, a página de atividades incluirá uma guia que filtra as atividades com base nas geradas na comunidade pelo membro atual. O padrão está marcado.

* **Visualização Exibir todas as atividades**

   Se marcada, a página de atividades incluirá uma guia que inclui todas as atividades geradas na comunidade às quais o membro atual tem acesso. O padrão está marcado.

* **Mostrar exibição seguinte**

   Se marcada, a página de atividades incluirá uma guia que filtra as atividades com base nas atividades que o membro atual está seguindo. O padrão está marcado.

### Seguinte exibição {#following-view}

Os componentes devem ser configurados para ativar o seguinte. Os recursos que permitem o seguinte são [blog](/help/communities/blog-feature.md), [fórum](/help/communities/forum.md), [QnA](/help/communities/working-with-qna.md), [calendário](/help/communities/calendar.md), [filelibrary](/help/communities/file-library.md)e [comentários](/help/communities/comments.md).

![visualização seguinte](assets/following-activities.png)

O **Seguir** fornece um meio de seguir entradas como atividades, [notificações](/help/communities/notifications.md)ou [assinaturas](/help/communities/subscriptions.md). Sempre que a variável **Seguir** for selecionado, é possível ativar ou desativar uma seleção. O `Email Subscriptions` A seleção só está presente quando configurada.

Se qualquer método de seguir for selecionado, o texto do botão será alterado para **Seguindo**. Para maior comodidade, é possível selecionar `Unfollow All` para desativar todos os métodos.

O **Seguir** será exibido:

* Ao visualizar o perfil de outro membro.
* Em uma página principal do recurso, como fóruns, QnA e blogs.

   * Segue todas as atividades para esse recurso geral.

* Para uma entrada específica, como um tópico de fórum, pergunta de QnA ou artigo de blog.

   * Segue todas as atividades da entrada específica.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos dos fluxos de atividade](/help/communities/essentials-activities.md) página para desenvolvedores.
