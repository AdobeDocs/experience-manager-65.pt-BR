---
title: Grupos de comunidades
seo-title: Grupos de comunidades
description: Criação de grupos de comunidade
seo-description: Criação de grupos de comunidade
uuid: c677d23d-5edb-414c-9013-130c88c2ea52
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d94708ee-ca6b-420c-9536-6889d752f9de
docset: aem65
translation-type: tm+mt
source-git-commit: 6337a57ea12f1e026f6c754a083307ce018a1c13
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# Grupos de comunidades {#community-groups}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados (membros da comunidade e autores) dos ambientes de publicação e autor.

Essa capacidade está presente quando a função [groups](/help/communities/functions.md#groups-function) está presente na estrutura [site da comunidade](/help/communities/sites-console.md).

Um [modelo de grupo da comunidade](/help/communities/tools-groups.md) fornece o design da página de grupo da comunidade quando um grupo da comunidade é criado dinamicamente.

Um ou mais modelos de grupo são selecionados para a função de grupos quando a função é adicionada à estrutura de um site da comunidade ou a um modelo de site da comunidade. Esta lista de modelos de grupo é apresentada ao membro ou autor que cria dinamicamente um novo grupo a partir do site da comunidade.

## Criando um Novo Grupo {#creating-a-new-group}

A capacidade de criar um novo grupo da comunidade depende da existência de um site da comunidade que inclui a função de grupos, como um criado a partir do [Modelo de site de referência](/help/communities/sites.md).

Os exemplos a seguir usam o site da comunidade criado a partir de `Reference Site Template`, conforme descrito no tutorial [Introdução ao AEM Communities](/help/communities/getting-started.md).

Esta é a página que carrega na publicação quando o item de menu **Grupos** é selecionado:

![new-group](assets/new-group.png)

Quando você seleciona o ícone **Novo grupo**, uma caixa de diálogo de edição é aberta.

Na guia **Settings**, você fornece os recursos básicos do grupo:

![group-settings](assets/group-settings.png)

* **Nome do grupo**

   O título do grupo a ser exibido no site da comunidade.

* **Descrição**

   Uma descrição do grupo a ser exibido no site da comunidade.

* **Convite**

   Uma lista de membros para convidar para entrar no grupo. A pesquisa antecipada fornecerá sugestões de membros da comunidade a serem convidados.

* **Nome do URL do grupo**

   O nome da página de grupo que se torna parte do URL.

* **Abrir grupo**

   Selecionar `Open Group` indica que qualquer visitante anônimo do site pode visualização no conteúdo e desmarcará `Member Only Group`.

* **Grupo somente de membros**

   Selecionar `Member Only Group` indica que apenas os membros do grupo podem visualização no conteúdo e desmarcarão `Open Group`.

Na guia **Modelo** é a capacidade de
selecione na lista de modelos de grupos da comunidade que foram especificados quando a função de grupos foi incluída na estrutura do site da comunidade ou em um modelo de site da comunidade.

![group-template](assets/group-template.png)

Na guia **Image** está a capacidade de carregar uma imagem para ser exibida para o grupo na página Grupos do site da comunidade. A folha de estilos padrão dimensionará a imagem para 170 x 90 pixels.

![group-image](assets/group-image.png)

Ao selecionar o botão **Criar grupo**, as páginas do grupo são criadas com base no modelo escolhido, e um grupo de usuários é criado para associação e a página Grupos será atualizada para mostrar a nova subcomunidade.

Por exemplo, a página Grupos com uma nova subcomunidade chamada &quot;Grupo de foco&quot;, para a qual uma miniatura de imagem foi carregada, será exibida da seguinte forma (ainda conectado como um administrador de grupo da comunidade):

![página de grupo](assets/group-page.png)

A seleção do link `Focus Group` abrirá a página Grupo de foco no navegador, que tem uma aparência inicial com base no modelo escolhido, e inclui um submenu abaixo do menu principal do site da comunidade:

![open-group-page](assets/open-group-page.png)

### Componente de Lista de membro do grupo da comunidade {#community-group-member-list-component}

O componente `Community Group Member List` destina-se ao uso por desenvolvedores de modelos de grupo.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Community Group Essentials](/help/communities/essentials-groups.md) para desenvolvedores.

Para obter outras informações relacionadas a grupos da comunidade, visite [Gerenciar usuários e grupos de usuários](/help/communities/users.md).
