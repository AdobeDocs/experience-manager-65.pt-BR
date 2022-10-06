---
title: Preparar ativos para tradução
description: Crie pastas raiz de idioma para preparar ativos para tradução para suportar ativos multilíngues.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Preparar ativos para tradução {#preparing-assets-for-translation}

Ativos multilíngues significa ativos com binários, metadados e tags em vários idiomas. Geralmente, os binários, metadados e tags de ativos existem em um idioma, que é traduzido para outros idiomas para uso em projetos multilíngues.

Em [!DNL Adobe Experience Manager Assets], ativos multilíngues são incluídos em pastas, onde cada pasta contém os ativos em um idioma diferente.

Cada pasta de idioma é chamada de cópia de idioma. A pasta raiz de uma cópia de idioma, conhecida como raiz de idioma, identifica o idioma do conteúdo na cópia de idioma. Por exemplo, */content/dam/it* é a raiz do idioma italiano para a cópia em língua italiana. As cópias de idioma devem usar um [raiz de idioma configurada corretamente](preparing-assets-for-translation.md#creating-a-language-root) para que o idioma correto seja direcionado quando as traduções de ativos de origem forem executadas.

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

1. Crie a raiz do idioma do idioma principal. Por exemplo, a raiz de idioma da cópia em inglês na hierarquia de pasta de amostra é `/content/dam/en`. Verifique se a raiz do idioma está configurada corretamente de acordo com as informações em [Criar uma raiz de idioma](preparing-assets-for-translation.md#creating-a-language-root).

1. Adicione ativos ao idioma principal.
1. Crie a raiz de idioma de cada idioma de destino para o qual você precisa de uma cópia de idioma.

## Criar uma raiz de idioma {#creating-a-language-root}

Para criar a raiz de idioma, crie uma pasta e use um código de idioma ISO como o valor da propriedade Name. Depois de criar a raiz do idioma, você pode criar uma cópia de idioma em qualquer nível na raiz do idioma.

Por exemplo, a página raiz da cópia de idioma italiano da hierarquia de amostra tem `it` como a propriedade Name . A propriedade Name é usada como o nome do nó do ativo no repositório e, portanto, determina o caminho dos ativos. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. No [!DNL Assets] , clique em **[!UICONTROL Criar]** e escolha **[!UICONTROL Pasta]** no menu .

   ![Criar pasta](assets/Create-folder.png)

1. No **[!UICONTROL Nome]** digite o código do país no formato de `<language-code>`.

   ![Adicionar código de idioma na pasta](assets/Add-language-code-in-folder.png)

1. Clique em **[!UICONTROL Criar]**. A raiz do idioma é criada na variável [!DNL Assets] console.

## Exibir raízes do idioma {#viewing-language-roots}

[!DNL Experience Manager] A interface fornece uma **[!UICONTROL Referências]** painel que exibe uma lista de raízes de idioma criadas em [!DNL Assets].

1. No [!DNL Assets] selecione o idioma principal para o qual deseja criar cópias de idioma.
1. No painel esquerdo, selecione **[!UICONTROL Referências]** para abrir a [!UICONTROL Referência] painel.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. No painel Referências , clique em **[!UICONTROL Cópias de idioma]**. O [!UICONTROL Cópias de idioma] painel mostra as cópias de idioma dos ativos.

   ![cópias de idioma](assets/lang-copy2.png)
