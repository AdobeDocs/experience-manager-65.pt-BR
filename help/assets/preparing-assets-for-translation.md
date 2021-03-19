---
title: Preparar ativos para tradução
description: Crie pastas raiz de idioma para preparar ativos para tradução para suportar ativos multilíngues.
contentOwner: AG
role: Profissional de negócios, Administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 1%

---


# Preparar ativos para tradução {#preparing-assets-for-translation}

Ativos multilíngues significa ativos com binários, metadados e tags em vários idiomas. Geralmente, os binários, metadados e tags de ativos existem em um idioma, que é traduzido para outros idiomas para uso em projetos multilíngues.

Em [!DNL Adobe Experience Manager Assets], os ativos multilíngues são incluídos nas pastas, onde cada pasta contém os ativos em um idioma diferente.

Cada pasta de idioma é chamada de cópia de idioma. A pasta raiz de uma cópia de idioma, conhecida como raiz de idioma, identifica o idioma do conteúdo na cópia de idioma. Por exemplo, */content/dam/it* é a raiz do idioma italiano para a cópia de idioma italiano. As cópias de idioma devem usar uma [raiz de idioma configurada corretamente](preparing-assets-for-translation.md#creating-a-language-root) para que o idioma correto seja direcionado quando as traduções de ativos de origem forem executadas.

A cópia de idioma para a qual você adicionou ativos originalmente é o idioma principal. O idioma principal é a fonte traduzida para outros idiomas. Uma exemplo de hierarquia de pasta inclui várias raízes de idioma:

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

Execute as seguintes etapas para preparar os ativos para tradução:

1. Crie a raiz do idioma do idioma principal. Por exemplo, a raiz de idioma da cópia em inglês na hierarquia de pasta de amostra é `/content/dam/en`. Certifique-se de que a raiz de idioma esteja configurada corretamente de acordo com as informações em [Create a Language Root](preparing-assets-for-translation.md#creating-a-language-root).

1. Adicione ativos ao idioma principal.
1. Crie a raiz de idioma de cada idioma de destino para o qual você precisa de uma cópia de idioma.

## Criar uma raiz de idioma {#creating-a-language-root}

Para criar a raiz de idioma, crie uma pasta e use um código de idioma ISO como o valor da propriedade Name. Depois de criar a raiz do idioma, você pode criar uma cópia de idioma em qualquer nível na raiz do idioma.

Por exemplo, a página raiz da cópia de idioma italiano da hierarquia de amostra tem `it` como a propriedade Name . A propriedade Name é usada como o nome do nó do ativo no repositório e, portanto, determina o caminho dos ativos. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. No console [!DNL Assets], clique em **[!UICONTROL Criar]** e escolha **[!UICONTROL Pasta]** no menu.

   ![Criar pasta](assets/Create-folder.png)

1. No campo **[!UICONTROL Nome]**, digite o código do país no formato `<language-code>`.

   ![Adicionar código de idioma na pasta](assets/Add-language-code-in-folder.png)

1. Clique em **[!UICONTROL Criar]**. A raiz do idioma é criada no console [!DNL Assets].

## Exibir raízes de idioma {#viewing-language-roots}

[!DNL Experience Manager] A interface do fornece um  **** Painel de referência que exibe uma lista de raízes de idioma que foram criadas no  [!DNL Assets].

1. No console [!DNL Assets], selecione o idioma principal para o qual deseja criar cópias de idioma.
1. No painel à esquerda, selecione a opção **[!UICONTROL References]** para abrir o painel [!UICONTROL Reference].

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. No painel Referências , clique em **[!UICONTROL Cópias de idioma]**. O painel [!UICONTROL Cópias de idioma] mostra as cópias de idioma dos ativos.

   ![cópias de idioma](assets/lang-copy2.png)
