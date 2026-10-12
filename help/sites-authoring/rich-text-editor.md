---
title: Uso do Editor de rich text para criar conteúdo
description: Uso do editor de rich text para criar conteúdo no Adobe Experience Manager 6.5.
exl-id: 90cb8893-65f3-4d82-9880-ce8dd80891b1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 28%
---
# Uso do Editor de rich text para criar conteúdo {#use-rich-text-editor-to-author-content}

O Editor de Rich Text (RTE) é um elemento básico fundamental para inserir conteúdo textual no AEM. É a base de vários componentes, incluindo:

* [Texto](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/wcm-components/text)
* [Tabela](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/wcm-components/text#table)

## Edição no local {#in-place-editing}

Selecionar um componente baseado em texto com um único clique revelará a [barra de ferramentas do componente](/help/sites-authoring/editing-content.md#edit-configure-copy-cut-delete-paste) como com qualquer componente.

![screen_shot_2018-03-21at163054](assets/screen_shot_2018-03-21at163054.png)

Tocar/clicar novamente ou selecionar inicialmente o componente com um clique duplo lento abre a edição no local, que tem sua própria barra de ferramentas. Aqui você pode editar o conteúdo e fazer alterações básicas na formatação.

![screen_shot_2018-03-21at163214](assets/screen_shot_2018-03-21at163214.png)

Essa barra de ferramentas fornece as seguintes opções:

* **Formato**: permite que você defina Negrito, Itálico e Sublinhado.
* **Listas**: com este recurso, você pode criar listas com marcadores ou numeradas, ou definir o recuo.
* **Hiperlink**
* **Desvincular**
* **Tela cheia**
* **Fechar**
* **Salvar**

## Edição de tela cheia {#full-screen-editing}

Para componentes baseados em texto, tocar no modo de tela cheia na barra de ferramentas ![Modo de edição de tela cheia](do-not-localize/screen_shot_2018-03-21at163236.png) abrirá o editor de rich text e ocultará o restante do conteúdo da página.

O modo de tela cheia exibe todas as opções configuradas que podem ser usadas para criação. A disponibilidade é opções [depende da configuração](/help/sites-administering/rich-text-editor.md).

![screen_shot_2018-03-21at163248](assets/screen_shot_2018-03-21at163248.png)

Outras opções do editor de Rich Text incluem:

* **Âncora**: crie uma âncora no texto para a qual você poderá mais tarde vincular ou fazer referência.
* **Alinhar texto à esquerda**
* **Centralizar texto**
* **Alinhar texto à direita**

Feche o modo de tela cheia clicando no ícone Minimizar.

![screen_shot_2018-03-21at163323](assets/screen_shot_2018-03-21at163323.png)

>[!NOTE]
>
>Copiar listas aninhadas do Microsoft Word para o RTE pode gerar resultados inconsistentes e exigir ajuste manual após colar o texto no RTE.
