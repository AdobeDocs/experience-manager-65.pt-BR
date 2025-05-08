---
title: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer ou Apple Safari
description: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer ou Apple Safari
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 2ffd69c153c60ada3fcb586ed5aa5bda48f645fc
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer ou Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muitas versões recentes do navegador incluem seu próprio suporte limitado para PDF forms baseado em XFA. Embora esses navegadores possam abrir PDF forms baseado em XFA, os recursos fornecidos são limitados. Se não conseguir abrir ou enviar um formulário do PDF baseado em XFA em um navegador moderno, use um dos seguintes métodos:

* Use o [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) ou o [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), versão 8 ou posterior para abrir e enviar PDF forms baseado em XFA.
* O Acrobat e o Reader, no Microsoft® Windows®, permitem configurar o para abrir PDFs no modo de Exibição protegida, o que impede que o PDF forms baseado em XFA seja aberto. Certifique-se de que o modo de Exibição protegida na Acrobat ou Reader esteja desativado. Para obter mais informações, consulte [Modo de Exibição Protegido (somente Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Para desenvolvedores do Forms) A Adobe Experience Manager Forms também oferece suporte a:

   * [renderize formulários baseados em XFA na HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=pt-BR&#key-capabilities-of-html-forms-br) de modo que os formulários possam ser abertos em navegadores com suporte para HTML5, incluindo os navegadores executados em dispositivos móveis como iPad. A representação HTML5 dos formulários mantém o layout do design do formulário e é compatível com a maioria das lógicas de formulário (como JavaScript, cálculo de formulário e validações de formulário) incorporadas ao modelo de formulário XFA.
   * [converta formulários baseados em XFA em Forms adaptável responsivo móvel](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=pt-BR&#create-an-adaptive-form-based-on-an-xfa-form-template). Esses formulários fornecem um layout responsivo, recursos de personalização e se adaptam dinamicamente às respostas do usuário, adicionando ou removendo campos ou seções, conforme necessário. Eles também fornecem conectores prontos para uso para várias fontes de dados, recursos de documentos de registro e conexão fácil com o Adobe Analytics para avaliação de desempenho. Para obter mais informações, consulte [Principais recursos e funcionalidades](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=pt-BR)
Dessa forma, seus investimentos em tecnologia em formulários XFA são protegidos e continuam a fornecer uma experiência ideal para seus usuários finais. Para obter mais informações, consulte [documentação do produto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=pt-BR).
