---
title: Alteração do conteúdo zero da página no Designer
seo-title: Alteração do conteúdo zero da página no Designer
description: Você sabe como alterar a mensagem exibida na Página Zero de um PDF XFA ao exibi-la em um visualizador que não seja da Adobe PDF?
seo-description: Você sabe como alterar a mensagem exibida na Página Zero de um PDF XFA ao exibi-la em um visualizador que não seja da Adobe PDF?
uuid: ac23fb21-3f15-48ea-aeeb-4ecc12b771ac
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 56b6a573-8aba-43e7-acb7-c2da45869d95
docset: aem65
feature: Formulários adaptáveis
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 2%

---


# Alteração do conteúdo zero da página no Designer {#changing-page-zero-content-in-designer}

O conteúdo zero da página é exibido por padrão quando um visualizador que não seja da Adobe PDF, como o visualizador de PDF padrão em [!DNL Chrome] ou [!DNL Firefox], não consegue ler o conteúdo do formulário PDF/XFA. A mensagem padrão Zero da página é mostrada abaixo.

![defaultpage0message](assets/defaultpage0message.png)

[!DNL AEM Forms] A versão do Designer permite que você altere a mensagem exibida na Página Zero. Para alterar a mensagem Zero da página, execute as seguintes etapas:

1. Certifique-se de ter a versão [!DNL AEM Forms] do Designer instalada. Você pode verificar a versão na tela Sobre do designer.

1. Abra o formulário no qual deseja alterar o conteúdo Zero da página.

1. Clique em **[!UICONTROL Arquivo]** > **[!UICONTROL Propriedades do formulário]**.

1. Na caixa de diálogo [!UICONTROL Propriedades do formulário], clique em ![mais](assets/plus.png) (ícone de adição) para adicionar uma propriedade personalizada.

1. Especifique **_pagezerocontent** como o nome da propriedade.
1. Adicione a nova mensagem Zero da página, no formato Rich Text, como valor. Por exemplo:


   `<body xmlns="https://www.w3.org/1999/xhtml" xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/"><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">You are seeing this message maybe because you are using a non Adobe PDF Viewer or an Old version of Adobe Reader. You can upgrade to the latest version of Adobe Reader for Windows, Mac, or Linux by visiting <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/reader_download.</p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in"><span style="xfa-spacerun:yes"> </code></p><p style="font-family:'Times';font-size:12pt;letter-spacing:0in">For more assistance with Adobe Reader visit <span style="xfa-spacerun:yes"> </code>https://www.adobe.com/go/acrreader.</p></body>`

1. Salve o formulário como PDF.

1. Exiba o formulário PDF no navegador para confirmar que a mensagem foi atualizada. O exemplo de valor acima é exibido da seguinte maneira:

   ![mensagem alterada](assets/changedmessage.png)

>[!NOTE]
>
>A propriedade personalizada recém-criada pode não aparecer corretamente na caixa de diálogo Propriedades do formulário ao reabrir o formulário. No entanto, funciona bem e o formulário exibe a mensagem Página zero atualizada.
