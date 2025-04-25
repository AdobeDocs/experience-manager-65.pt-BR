---
title: Como abrir o PDF forms baseado em XFA no Firefox e no Chrome
description: Como abrir o PDF forms baseado em XFA no Firefox e no Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Como abrir o PDF forms baseado em XFA no Firefox e no Chrome

## Problema

O visualizador integrado do PDF introduzido com o Mozilla Firefox e o Google Chrome não é compatível com o PDF forms baseado em XFA. Portanto, o PDF forms baseado em XFA não abre em versões posteriores do Firefox e do Chrome.

## Solução

Para usar o PDF forms baseado em XFA no Firefox e no Chrome, execute as seguintes etapas para configurar o Firefox e o Chrome para abrir PDFs usando o Adobe Reader ou o Adobe Acrobat.

>[!NOTE]
> 
> Verifique se o Adobe Reader ou Adobe Acrobat está instalado em sua máquina.

### Configurar Firefox

1. No Firefox, escolha **Ferramentas > Opções**.

1. No diálogo Opções, clique em **Aplicativos**.

1. Na guia Aplicativos, digite PDF no campo de pesquisa.

1. Para o tipo de conteúdo PDF (Portable Document Format) no resultado da pesquisa, selecione **Usar Adobe Acrobat (no Firefox)** na lista suspensa Ação.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Clique em OK.

1. Reinicie o Firefox.

### Configurar Chrome

1. No Chrome, acesse chrome://plugins/.

1. Clique em Desativar no Visualizador do Chrome PDF e em Ativar no Plug-in do Adobe PDF.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Para obter mais informações, consulte a documentação do [plug-in do Adobe PDF](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538) da Google.

>[!NOTE]
> 
> O LiveCycle ES4 oferece suporte à renderização de formulários baseados em XFA no HTML5, de modo que os formulários possam ser abertos em navegadores com suporte ao HTML5, incluindo aqueles executados em dispositivos móveis como o iPad. A representação HTML5 dos formulários mantém o layout do design do formulário e é compatível com a maioria das lógicas de formulário (como JavaScript, cálculo de formulário e validações de formulário) incorporadas ao modelo de formulário XFA. Dessa forma, seus investimentos em tecnologia em formulários XFA são transferidos facilmente para dispositivos em que a execução do plug-in Adobe Reader não é viável.
>Para obter mais informações, consulte a [documentação do produto LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Avisos legais](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Política de Privacidade Online](https://www.adobe.com/br/privacy.html)