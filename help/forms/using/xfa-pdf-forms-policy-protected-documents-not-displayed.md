---
title: Problemas de exibição para documentos do PDF forms baseados em XFA e protegidos por política
description: Problemas de exibição para documentos do PDF forms baseados em XFA e protegidos por política
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Problemas de exibição para documentos do PDF forms baseados em XFA e protegidos por política

Verifique os seguintes motivos se não conseguir abrir um formulário do PDF baseado em XFA ou um documento protegido por política usando o Gerenciamento de Direitos do Adobe LiveCycle:

* Os documentos PDF forms baseados em XFA e protegidos por política exigem o Adobe® Acrobat® ou Adobe® Reader®, versão 8 e posterior. Consulte [Downloads da Adobe](https://www.adobe.com/downloads.html) para baixar a Reader ou o Acrobat mais recente.
* Navegadores como o Mozilla Firefox e o Google Chrome oferecem um visualizador do PDF integrado que não é compatível com o PDF forms baseado em XFA. Para exibir PDF forms baseados em XFA nesses navegadores, você deve configurar o para abrir PDFs usando Acrobat ou Reader. Para obter mais informações, consulte PDF forms baseado em XFA no Mozilla Firefox e no Google Chrome.
* O Acrobat e o Reader, no Microsoft® Windows®, permitem configurar o para abrir PDFs no modo de Exibição protegida, o que impede que documentos do PDF forms baseados em XFA e documentos protegidos por política sejam abertos. Certifique-se de que o modo de Exibição protegida na Acrobat ou Reader esteja desativado. Para obter mais informações, consulte [Modo de Exibição Protegido (somente Windows)](https://helpx.adobe.com/br/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Se você estiver tentando acessar documentos do PDF forms baseados em XFA ou documentos protegidos por política em seu dispositivo móvel, considere o seguinte:

   * Para abrir documentos protegidos por política em dispositivos móveis, é necessário o Adobe Reader para dispositivos móveis. Para obter mais informações, consulte [aplicativo móvel do Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * Dispositivos móveis e smartphones iOS, Android e Blackberry não são compatíveis com o plug-in Adobe Reader com formulários XFA. O LiveCycle ES4 fornece um serviço direcionado a dispositivos móveis usando o HTML5; o criador do formulário deve usar esse serviço para permitir que os formulários sejam usados nesses dispositivos.
   * Se você estiver usando o estilo Metro em um dispositivo móvel Windows 8, altere para o modo de exibição Clássico ou use o HTML5 com LiveCycle ES4.

>[!NOTE]
>
>O LiveCycle ES4 oferece suporte à renderização de formulários baseados em XFA no HTML5, de modo que os formulários possam ser abertos em navegadores com suporte ao HTML5, incluindo aqueles executados em dispositivos móveis como o iPad. A representação HTML5 dos formulários mantém o layout do design do formulário e é compatível com a maioria das lógicas de formulário (como JavaScript, cálculo de formulário e validações de formulário) incorporadas ao modelo de formulário XFA. Dessa forma, seus investimentos em tecnologia em formulários XFA são facilmente transferidos para os dispositivos em que a execução do plug-in Adobe Reader não é viável.
>Para obter mais informações, consulte Atualizando para a [documentação do produto LiveCycle](https://business.adobe.com/br/products/experience-manager/forms/aem-forms.html).

[Avisos legais](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Política de Privacidade Online](https://www.adobe.com/br/privacy.html)