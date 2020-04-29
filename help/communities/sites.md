---
title: Modelos de site
seo-title: Modelos de site
description: Como acessar o console Modelos de site
seo-description: Como acessar o console Modelos de site
uuid: d2f7556e-7e43-424e-82f1-41790aeb2d98
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 202d7dba-2b34-431d-b10f-87775632807f
translation-type: tm+mt
source-git-commit: 89156f94f2d0494d44d4f0b99abfba4fafbc66d3

---


# Modelos de site {#site-templates}

O console Modelos de site é muito semelhante ao console Modelos [de](tools-groups.md) grupo, que está focado em funções de interesse para grupos da Comunidade.

>[!NOTE]
>
>Os consoles para a criação de sites [da](sites-console.md)comunidade, modelos [de site da](sites.md)comunidade, modelos [de grupos da](tools-groups.md) comunidade e funções [da](functions.md) comunidade são para uso somente no ambiente do autor.


## Console de modelos de site {#site-templates-console}

No ambiente do autor, para acessar o console de sites da comunidade:

* Da navegação global: **[!UICONTROL Ferramentas > Comunidades > Modelos de site]**

Este console exibe os modelos a partir dos quais um site [da](sites-console.md) comunidade pode ser criado e permite a criação de novos modelos de site.

![chlimage_1-18](assets/chlimage_1-18.png)

## Criar modelo de site {#create-site-template}

Para começar a criar um novo modelo de site, selecione `Create`.

Isso exibirá o painel do Editor de sites, que contém três subpainéis:

### Basic info {#basic-info}

![chlimage_1-19](assets/chlimage_1-19.png)

No painel Informações básicas, um nome, uma descrição e se o modelo está ativado ou desativado são configurados:

* **[!UICONTROL Nome do modelo do site da comunidade]**

   A ID do nome do modelo.

* **[!UICONTROL Descrição do modelo do site da comunidade]**

   A descrição do modelo.

* **[!UICONTROL Desativado/Ativado]**

   Um switch de alternância que controla se o modelo é referenciável.

### Miniatura     {#thumbnail}

![chlimage_1-20](assets/chlimage_1-20.png)

(Opcional) Selecione o ícone Carregar imagem para exibir uma miniatura junto com o nome e a descrição dos criadores dos sites da comunidade.

### Estrutura {#structure}

![chlimage_1-21](assets/chlimage_1-21.png)

Para adicionar funções de comunidade, arraste do lado direito para a esquerda na ordem em que os links de menu do site devem aparecer. Os estilos serão aplicados ao modelo durante a criação do site.

Por exemplo, se desejar um home page, arraste a função Página da biblioteca e solte sob o construtor de modelos. Isso resultará na abertura da caixa de diálogo de configuração da página. Consulte o console [de](functions.md) funções para obter informações sobre as caixas de diálogo de configuração.

Continue arrastando e soltando quaisquer outras funções da comunidade desejadas para um site da comunidade com base neste modelo.

A função page fornece uma página vazia. A função groups fornece a capacidade de criar um site de grupo (subcomunidade) dentro do site da comunidade.

>[!CAUTION]
>
>A função groups *não* deve ser a *primeira nem a única* função na estrutura do site.
>
>Qualquer outra função, como a função [de](functions.md#page-function)página, deve ser incluída e listada primeiro.


![chlimage_1-22](assets/chlimage_1-22.png)

### Função Modelos de grupo para grupos {#group-templates-for-groups-function}

Ao incluir uma função de grupos no modelo do site, a configuração exige a especificação das opções de modelo de grupo permitidas quando um novo grupo é criado no ambiente de publicação.

>[!CAUTION]
>
>A função Grupos *não* deve ser a *primeira nem a única* função na estrutura do site.


![chlimage_1-23](assets/chlimage_1-23.png)

Ao selecionar dois ou mais modelos de grupo da comunidade, uma opção é fornecida ao administrador do grupo ao criar um novo grupo na comunidade.

![chlimage_1-24](assets/chlimage_1-24.png)

## Modelo de site de edição {#edit-site-template}

Ao exibir modelos de site no console [principal Modelos de](#site-templates-console)site, é possível selecionar um modelo de site existente para edição.

Esse processo fornece os mesmos painéis que [cria um modelo](#create-site-template)de site.
