---
title: Grupos de comunidades
description: Criação de grupos da comunidade
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: edcda6cb-df47-4afe-8a9a-82d8e386fe05
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 3%

---

# Grupos de comunidades {#community-groups}

O recurso de grupos da comunidade é a capacidade de uma subcomunidade ser criada dinamicamente em um site da comunidade por usuários autorizados (membros da comunidade e autores) dos ambientes de publicação e criação.

Essa capacidade está presente quando o [função de grupos](/help/communities/functions.md#groups-function) está presente no [site da comunidade](/help/communities/sites-console.md) estrutura.

A [modelo de grupo da comunidade](/help/communities/tools-groups.md) O fornece o design da página do grupo da comunidade quando um grupo da comunidade é criado dinamicamente.

Um ou mais modelos de grupo são selecionados para a função de grupos quando a função é adicionada à estrutura de um site da comunidade ou a um modelo de site da comunidade. Essa lista de modelos de grupo é apresentada ao membro ou autor que cria dinamicamente um grupo dentro do site da comunidade.

## Criação de um novo grupo {#creating-a-new-group}

A capacidade de criar um grupo da comunidade depende da existência de um site da comunidade que inclui a função de grupos, como um criado a partir do [Modelo de site de referência](/help/communities/sites.md).

Os exemplos a seguir usam o site da comunidade criado a partir do `Reference Site Template` conforme descrito na seção [Introdução ao AEM Communities](/help/communities/getting-started.md) tutorial.

Esta é a página que é carregada ao publicar quando a variável **Grupos** o item de menu está selecionado:

![novo grupo](assets/new-group.png)

Ao selecionar a variável **Novo grupo** ícone, uma caixa de diálogo de edição é aberta.

No **Configurações** você fornece os recursos básicos do grupo:

![configurações de grupo](assets/group-settings.png)

* **Nome do grupo**

  O título do grupo que você deseja exibir no site da comunidade. Evite usar caracteres de sublinhado (_) e palavras-chave, como recursos e configuração no nome do grupo.

* **Descrição**

  Uma descrição do grupo a ser exibida no site da comunidade.

* **Convite**

  Uma lista de membros para convidar para o grupo. A pesquisa com digitação antecipada fornece sugestões de membros da comunidade para convidar.

* **Nome do URL do grupo**

  O nome da página de grupo que se torna parte do URL.

* **Abrir grupo**

  Selecionar `Open Group` indica que qualquer visitante anônimo do site pode visualizar o conteúdo e desmarca `Member Only Group`.

* **Grupo somente de membros**

  Selecionar `Member Only Group` indica que somente membros do grupo podem exibir o conteúdo e desmarca `Open Group`.

No **Modelo** você pode selecionar na lista de modelos do grupo da comunidade. Esses modelos foram especificados quando a função de grupos foi incluída na estrutura do site da comunidade ou em um modelo de site da comunidade.

![modelo de grupo](assets/group-template.png)

No **Imagem** , você pode fazer upload de uma imagem para exibição para o grupo na página Grupos do site da comunidade. A folha de estilos padrão dimensiona a imagem para 170 x 90 pixels.

![imagem de grupo](assets/group-image.png)

Ao selecionar **Criar grupo**, as páginas para o grupo são criadas com base no modelo escolhido e um grupo de usuários é criado para associação, e a página Grupos é atualizada para mostrar a nova subcomunidade.

Por exemplo, a página Grupos com uma nova subcomunidade chamada &quot;Grupo de foco&quot;, para a qual uma miniatura de imagem foi carregada, aparece da seguinte maneira (ainda conectado como administrador de grupo da comunidade):

![página-grupo](assets/group-page.png)

Selecionar o `Focus Group` abre a página Grupo de foco no navegador, que tem uma aparência inicial com base no modelo escolhido, e inclui um submenu abaixo do menu do site principal da comunidade:

![open-group-page](assets/open-group-page.png)

### Componente da lista de membros do grupo da comunidade {#community-group-member-list-component}

A variável `Community Group Member List` O componente deve ser usado por desenvolvedores de modelos de grupo.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do grupo da comunidade](/help/communities/essentials-groups.md) página para desenvolvedores.

Para obter outras informações relacionadas a grupos da comunidade, visite [Gerenciar usuários e grupos de usuários](/help/communities/users.md).
