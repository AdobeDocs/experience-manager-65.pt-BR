---
title: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari
description: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: 55e9344c088a38bc4c9f916a13c310a029b3b2f4
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---


# Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muitas versões recentes de navegadores incluíram seu próprio suporte limitado para PDF forms baseados em XFA. Embora esses navegadores possam abrir PDF forms baseados em XFA, a extensão do suporte é desconhecida. Se você não conseguir abrir ou enviar um formulário PDF baseado em XFA em um navegador moderno, use um dos seguintes métodos:

* Use [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) ou [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), versão 8 ou posterior para abrir e enviar PDF forms baseados em XFA.
* O Acrobat e o Reader, no Microsoft® Windows®, permitem que você configure a abertura do PDF no modo Exibição protegida, o que impede a abertura de PDF forms baseados em XFA. Certifique-se de que o modo de Exibição protegida no Acrobat ou Reader esteja desativado. Para obter mais informações, consulte [Exibição protegida (somente Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* Se você estiver tentando acessar PDF forms com base em XFA em seu dispositivo móvel, use o Adobe Reader para dispositivos móveis. Para obter mais informações, consulte [Aplicativo móvel Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
* (Para desenvolvedores do Forms) A Adobe Experience Manager Forms também oferece suporte para
   * [renderizar formulários baseados em XFA no HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) de forma que os formulários possam ser abertos em navegadores com suporte para HTML5, incluindo aqueles executados em dispositivos móveis como iPad. A representação de HTML5 dos formulários mantém o layout do design de formulário e suporta a maioria das lógicas de formulário (como JavaScript, cálculo de formulário e validações de formulário) incorporadas no modelo de formulário XFA.
   * [converter formulários baseados em XFA em Forms adaptável móvel](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Esses formulários fornecem um layout responsivo, recursos de personalização e adaptam-se dinamicamente às respostas do usuário, adicionando ou removendo campos ou seções conforme necessário. Eles também fornecem conectores prontos para várias fontes de dados, recursos de Documento de registro e conexão fácil com o Adobe Analytics para avaliação de desempenho. Para obter mais informações, consulte [Principais recursos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

Dessa forma, seus investimentos em tecnologia em formulários XFA são facilmente transferidos para os dispositivos em que a execução do plug-in Adobe Reader não é viável. Para obter mais informações, consulte [Documentação do produto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
