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
source-git-commit: 43663703a79b95ccdb83eb9b5730143bde101305
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---


# Grupos de comunidades {#community-groups}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados (membros da comunidade e autores) dos ambientes de publicação e autor.

Essa capacidade está presente quando a função [de](/help/communities/functions.md#groups-function) grupos está presente na estrutura do site [da](/help/communities/sites-console.md) comunidade.

Um modelo [de grupo da](/help/communities/tools-groups.md) comunidade fornece o design da página de grupo da comunidade quando um grupo da comunidade é criado dinamicamente.

Um ou mais modelos de grupo são selecionados para a função de grupos quando a função é adicionada à estrutura de um site da comunidade ou a um modelo de site da comunidade. Esta lista de modelos de grupo é apresentada ao membro ou autor que cria dinamicamente um novo grupo a partir do site da comunidade.

## Creating a New Group {#creating-a-new-group}

A capacidade de criar um novo grupo da comunidade depende da existência de um site da comunidade que inclui a função de grupos, como um criado a partir do Modelo [de site de](/help/communities/sites.md)referência.

Os exemplos a seguir usam o site da comunidade criado a partir do `Reference Site Template` como descrito no [tutorial Introdução aos AEM Communities](/help/communities/getting-started.md) .

Esta é a página que é carregada na publicação quando o item de menu **Grupos** é selecionado:

![chlimage_1-236](assets/chlimage_1-236.png)

Quando você seleciona o ícone **Novo grupo** , uma caixa de diálogo de edição é aberta.

Na guia **Configurações** , você fornece os recursos básicos do grupo:

![chlimage_1-237](assets/chlimage_1-237.png)

* **Nome do grupo**

   O título do grupo a ser exibido no site da comunidade.

* **Descrição**

   Uma descrição do grupo a ser exibido no site da comunidade.

* **Convite**

   Uma lista de membros para convidar para entrar no grupo. A pesquisa antecipada fornecerá sugestões de membros da comunidade a serem convidados.

* **Nome do URL do grupo**

   O nome da página de grupo que se torna parte do URL.

* **Abrir grupo**

   A seleção `Open Group` indica que qualquer visitante anônimo do site pode visualização no conteúdo e desmarcará a seleção `Member Only Group`.

* **Grupo somente de membros**

   A seleção `Member Only Group` indica que somente os membros do grupo podem visualização no conteúdo e desmarcarão a seleção `Open Group`.

Na guia **Modelo** está a capacidade de selecionar na lista de modelos de grupos da comunidade que foram especificados quando a função de grupos foi incluída na estrutura do site da comunidade ou em um modelo de site da comunidade.

![chlimage_1-238](assets/chlimage_1-238.png)

Na guia **Imagem** está a capacidade de carregar uma imagem para ser exibida para o grupo na página Grupos do site da comunidade. A folha de estilos padrão dimensionará a imagem para 170 x 90 pixels.

![chlimage_1-239](assets/chlimage_1-239.png)

Ao selecionar o botão **Criar grupo** , as páginas do grupo são criadas com base no modelo escolhido, e um grupo de usuários é criado para associação e a página Grupos será atualizada para mostrar a nova subcomunidade.

Por exemplo, a página Grupos com uma nova subcomunidade chamada &quot;Grupo de foco&quot;, para a qual uma miniatura de imagem foi carregada, será exibida da seguinte forma (ainda conectado como um administrador de grupo da comunidade):

![chlimage_1-240](assets/chlimage_1-240.png)

A seleção do `Focus Group` link abrirá a página Grupo de foco no navegador, que tem uma aparência inicial com base no modelo escolhido, e inclui um submenu abaixo do menu principal do site da comunidade:

![chlimage_1-241](assets/chlimage_1-241.png)

### Community Group Member List Component {#community-group-member-list-component}

O `Community Group Member List` componente é destinado ao uso por desenvolvedores de modelos de grupo.

### Informações adicionais {#additional-information}

Para obter mais informações, consulte a página [Community Group Essentials](/help/communities/essentials-groups.md) para desenvolvedores.

Para obter outras informações relacionadas a grupos da comunidade, visite [Gerenciar usuários e grupos](/help/communities/users.md)de usuários.
