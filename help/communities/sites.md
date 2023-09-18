---
title: Modelos de site
description: Como acessar o console Modelos de site
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 05a944a3-adb1-47b4-b4a5-15bac91c995e
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 4%

---

# Modelos de site {#site-templates}

O console Modelos de site é semelhante ao [Modelos de grupo](tools-groups.md) que se concentra em funções de interesse para grupos da Comunidade.

>[!NOTE]
>
>Os consoles para a criação de [sites da comunidade](sites-console.md), [modelos de site da comunidade](sites.md), [modelos de grupo da comunidade](tools-groups.md), e [funções da comunidade](functions.md) são para uso somente no ambiente de criação.

## Console de modelos de site {#site-templates-console}

No ambiente de criação, para acessar o console de sites da comunidade:

* Na navegação global: **[!UICONTROL Ferramentas > Comunidades > Modelos de site]**

Esse console exibe os modelos a partir dos quais [site da comunidade](sites-console.md) pode ser criado e permite que novos modelos de site sejam criados.

![site-template](assets/site-template.png)

## Criar modelo de site {#create-site-template}

Para começar a criar um modelo de site, selecione `Create`.

Isso abre o painel Editor de sites, que contém três subpainéis:

### Informações básicas {#basic-info}

![site-template-basicinfo](assets/site-template-basicinfo.png)

No painel Informações básicas, um nome, uma descrição e se o modelo está ativado ou desativado são configurados:

* **[!UICONTROL Nome do modelo do site da comunidade]**

  A ID do nome do modelo.

* **[!UICONTROL Descrição do modelo do site da comunidade]**

  A descrição do modelo.

* **[!UICONTROL Desativado/Ativado]**

  Um switch que controla se o modelo é referenciável.

### Miniatura  {#thumbnail}

![miniatura do site](assets/site-thumbnail.png)

(Opcional) Selecione o ícone Fazer upload da imagem para exibir uma miniatura junto com o nome e a descrição para os criadores de sites da comunidade.

### Estrutura {#structure}

![estrutura do site](assets/site-structure.png)

Para adicionar funções da comunidade, arraste do lado direito para o lado esquerdo na ordem em que os links do menu do site devem aparecer. Os estilos são aplicados ao modelo durante a criação do site.

Por exemplo, se você quiser uma página inicial, arraste a função Página da biblioteca e solte-a no construtor de modelos. Isso resulta na abertura da caixa de diálogo de configuração da página. Consulte a [console de funções](functions.md) para obter informações sobre as caixas de diálogo de configuração.

Continue arrastando e soltando quaisquer outras funções da comunidade desejadas para um site da comunidade com base nesse modelo.

A função page fornece uma página vazia. A função Grupos permite criar um site de grupo (subcomunidade) no site de comunidade.

>[!CAUTION]
>
>A função Groups deve *não ser a primeira nem a única* na estrutura do site.
>
>Qualquer outra função, como a [função de página](functions.md#page-function), devem ser incluídos e listados primeiro.

![editor de site](assets/site-editor.png)

### Função Modelos de grupo para grupos {#group-templates-for-groups-function}

Ao incluir uma função Grupos no modelo de site, a configuração exige a especificação das opções de modelo de grupo permitidas quando um novo grupo é criado no ambiente de publicação.

>[!CAUTION]
>
>A função Groups deve *não ser a primeira nem a única* na estrutura do site.

![site-functions](assets/site-functions.png)

Ao selecionar dois ou mais templates do grupo da comunidade, uma escolha é fornecida ao administrador do grupo ao realmente criar um grupo na comunidade.

![site-function](assets/site-functions1.png)

## Modelo de sites de edição {#edit-site-template}

Ao visualizar modelos de site no principal [Console de Modelos de site](#site-templates-console), é possível selecionar um modelo de site existente para edição.

Esse processo fornece os mesmos painéis que [criar um modelo de site](#create-site-template).
