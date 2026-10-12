---
title: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer ou Apple Safari
description: Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft&reg; Edge, Microsoft&reg; Internet Explorer ou Apple Safari
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%
---
# Não é possível abrir o PDF forms baseado em XFA no Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer ou Apple Safari{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

Muitas versões recentes do navegador incluem seu próprio suporte limitado para PDF forms baseado em XFA. Embora esses navegadores possam abrir PDF forms baseado em XFA, os recursos fornecidos são limitados. Se não conseguir abrir ou enviar um formulário do PDF baseado em XFA em um navegador moderno, use um dos seguintes métodos:

* Use o [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) ou o [Adobe® Adobe® Reader®](https://get.adobe.com/reader/), versão 8 ou posterior para abrir e enviar PDF forms baseado em XFA.
* O Acrobat e o Reader, no Microsoft® Windows®, permitem configurar o para abrir PDFs no modo de Exibição protegida, o que impede que o PDF forms baseado em XFA seja aberto. Certifique-se de que o modo de Exibição protegida na Acrobat ou Reader esteja desativado. Para obter mais informações, consulte [Modo de Exibição Protegido (somente Windows)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* (Para desenvolvedores do Forms) A Adobe Experience Manager Forms também oferece suporte a:

  * [renderize formulários baseados em XFA na HTML5 Forms](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) de modo que os formulários possam ser abertos em navegadores com suporte para HTML5, incluindo os navegadores executados em dispositivos móveis como iPad. A representação HTML5 dos formulários mantém o layout do design do formulário e é compatível com a maioria das lógicas de formulário (como JavaScript, cálculo de formulário e validações de formulário) incorporadas ao modelo de formulário XFA.
  * [converta formulários baseados em XFA em Forms adaptável responsivo móvel](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Esses formulários fornecem um layout responsivo, recursos de personalização e se adaptam dinamicamente às respostas do usuário, adicionando ou removendo campos ou seções, conforme necessário. Eles também fornecem conectores prontos para uso para várias fontes de dados, recursos de documentos de registro e conexão fácil com o Adobe Analytics para avaliação de desempenho. Para obter mais informações, consulte [Principais recursos e funcionalidades](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=en)
    Dessa forma, seus investimentos em tecnologia em formulários XFA são protegidos e continuam a fornecer uma experiência ideal para seus usuários finais. Para obter mais informações, consulte [documentação do produto Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html).
