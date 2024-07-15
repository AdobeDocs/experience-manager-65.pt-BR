---
title: Grupos de comunidades
description: Saiba como o recurso de grupos da comunidade permite que você crie dinamicamente uma subcomunidade em um site da comunidade por usuários autorizados no Publish e no Author.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Grupos de comunidades {#community-groups}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados (membros da comunidade e autores) dos ambientes de publicação e criação.

Esta habilidade está presente quando a [função de grupos](/help/communities/functions.md#groups-function) está presente na estrutura do [site de comunidade](/help/communities/sites-console.md).

Um [modelo do grupo da comunidade](/help/communities/tools-groups.md) fornece o design da página do grupo da comunidade quando um grupo da comunidade é criado dinamicamente.

Um ou mais modelos de grupo são selecionados para a função de grupos quando a função é adicionada à estrutura de um site da comunidade ou a um modelo de site da comunidade. Essa lista de modelos de grupo é apresentada ao membro ou autor que cria dinamicamente um grupo dentro do site da comunidade.

## Criação de um novo grupo {#creating-a-new-group}

A capacidade de criar um grupo da comunidade depende da existência de um site da comunidade que inclui a função de grupos, como um criado a partir do [Modelo de site de referência](/help/communities/sites.md).

Os exemplos a seguir usam o site da comunidade criado a partir de `Reference Site Template` conforme descrito no tutorial [Introdução ao AEM Communities](/help/communities/getting-started.md).

Esta é a página que é carregada ao publicar quando o item de menu **Grupos** é selecionado:

![novo-grupo](assets/new-group.png)

Ao selecionar o ícone **Novo Grupo**, uma caixa de diálogo de edição é aberta.

Na guia **Configurações**, você fornece os recursos básicos do grupo:

![configurações-grupo](assets/group-settings.png)

* **Nome do Grupo**

  O título do grupo que você deseja exibir no site da comunidade. Evite usar caracteres de sublinhado (_) e palavras-chave, como recursos e configuração no nome do grupo.

* **Descrição**

  Uma descrição do grupo a ser exibida no site da comunidade.

* **Convidar**

  Uma lista de membros para convidar para o grupo. A pesquisa com digitação antecipada fornece sugestões de membros da comunidade para convidar.

* **Nome da URL do Grupo**

  O nome da página de grupo que se torna parte do URL.

* **Abrir grupo**

  Selecionar `Open Group` indica que qualquer visitante anônimo do site pode exibir o conteúdo e desmarca `Member Only Group`.

* **Grupo somente de membros**

  Selecionar `Member Only Group` indica que somente membros do grupo podem exibir o conteúdo e desmarca `Open Group`.

Na guia **Modelo**, você pode selecionar na lista de modelos de grupo da comunidade. Esses modelos foram especificados quando a função de grupos foi incluída na estrutura do site da comunidade ou em um modelo de site da comunidade.

![modelo-grupo](assets/group-template.png)

Na guia **Imagem**, é possível carregar uma imagem para exibição no grupo na página Grupos do site da comunidade. A folha de estilos padrão dimensiona a imagem para 170 x 90 pixels.

![imagem-grupo](assets/group-image.png)

Ao selecionar **Criar grupo**, as páginas do grupo são criadas com base no modelo escolhido, um grupo de usuários é criado para associação e a página Grupos é atualizada para mostrar a nova subcomunidade.

Por exemplo, a página Grupos com uma nova subcomunidade chamada &quot;Grupo de foco&quot;, para a qual uma miniatura de imagem foi carregada, aparece da seguinte maneira (ainda conectado como administrador de grupo da comunidade):

![página-grupo](assets/group-page.png)

Selecionar o link `Focus Group` abre a página Grupo de foco no navegador, que tem uma aparência inicial com base no modelo escolhido, e inclui um submenu abaixo do menu do site principal da comunidade:

![abrir-página-grupo](assets/open-group-page.png)

### Componente da lista de membros do grupo da comunidade {#community-group-member-list-component}

O componente `Community Group Member List` deve ser usado por desenvolvedores de modelos de grupo.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Community Group Essentials](/help/communities/essentials-groups.md) para desenvolvedores.

Para outras informações relacionadas a grupos da comunidade, visite [Gerenciando usuários e grupos de usuários](/help/communities/users.md).
