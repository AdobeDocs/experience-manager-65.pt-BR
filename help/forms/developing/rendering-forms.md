---
title: Renderização do Forms
seo-title: Rendering Forms
description: Use o serviço Forms para criar aplicativos clientes interativos de captura de dados que validam, processam, transformam e entregam formulários normalmente criados no Designer. Os autores de formulários podem desenvolver um design de formulário único que o serviço Forms renderiza no PDF, SWF ou HTML em vários ambientes de navegador.
seo-description: Use the Forms service to create interactive data capture client applications that validate, process, transform, and deliver forms typically created in Designer. Form authors can develop a single form design that the Forms service renders in PDF, SWF, or HTML in various browser environments.
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
role: Developer
exl-id: ec9ccf04-7cec-493a-91ab-0e399a905338
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# Renderização do Forms {#rendering-forms}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

**Sobre o serviço Forms**

O serviço Forms permite criar aplicativos clientes interativos de captura de dados que validam, processam, transformam e entregam formulários normalmente criados no Designer. Os autores de formulários podem desenvolver um design de formulário único que o serviço Forms renderiza no PDF, SWF ou HTML em vários ambientes de navegador.

Quando um usuário final solicita um formulário, um aplicativo cliente envia a solicitação para o serviço da Forms, que retorna o formulário em um formato apropriado. Assim que o serviço Forms receber uma solicitação, ele mesclará os dados com um design de formulário e, em seguida, fornecerá o formulário no formato desejado. A saída do serviço de Formulário é um formulário interativo, geralmente um documento PDF. Um formulário interativo permite que os usuários preencham campos localizados nele.

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvar o formulário como um arquivo PDF. Um aplicativo baseado na Web pode gravar o formulário no navegador da Web. Um aplicativo de desktop pode salvar o formulário como um arquivo PDF. Para demonstrar como gravar em um navegador da Web e em um arquivo PDF, o início rápido localizado na *Renderização do Forms* são organizadas da seguinte maneira:

* Os exemplos de API Java altamente digitados (modo SOAP) são um servlet Java.
* Os exemplos do serviço da Web (Java Base64) são um servlet Java.
* Os exemplos de serviço da Web (MTOM) são um aplicativo de console (nem todos os inícios rápidos têm um exemplo MTOM).

>[!NOTE]
>
>Para obter informações sobre como criar uma aplicação Web que usa servlets java para chamar o serviço Forms, consulte [Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Você pode passar um design de formulário (um arquivo XDP) ou um documento PDF para o serviço da Forms usando uma das duas formas a seguir:

* É possível referenciar o design de formulário usando um valor de URL. Essa abordagem envolve usar um `URLSpec` objeto. A raiz de conteúdo é passada para o serviço Forms usando o `URLSpec` do objeto `setContentRootURI` método . O nome do design de formulário ( `formQuery`) é passado como um parâmetro separado. Os dois valores são concatenados para obter a referência absoluta para o design de formulário. (A maioria dos ícones rápidos está localizada na seção *Renderização do Forms* use essa abordagem.)
* Você pode passar uma `com.adobe.idp.Document` que contém o design de formulário para o serviço Forms. Dois novos métodos nomeados `renderPDFForm2` e `renderHTMLForm2` aceite um `com.adobe.idp.Document` objeto que contém um design de formulário. (Consulte [Enviar documentos para o serviço do Forms](/help/forms/developing/passing-documents-forms-service.md)

Você pode realizar essas tarefas usando o serviço Forms:

* Renderizar PDF forms interativos. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Renderizar formulários no cliente. (Consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).)
* Renderizar formulários com base em fragmentos. (Consulte [Renderização do Forms com base em fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)
* Renderizar formulários ativados por direitos. (Consulte [Forms com direitos de renderização ativados](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Renderizar formulários como HTML. (Consulte [Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)
* Renderização do HTML Forms usando arquivos CSS personalizados ([Renderização do HTML Forms usando arquivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Manipule formulários enviados. (Consulte [Manuseio de Forms Enviado](/help/forms/developing/handling-submitted-forms.md).)
* Criação de documentos PDF com dados XML enviados. (Consulte [Criação de documentos PDF com dados XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Preencha os formulários previamente. (Consulte [Pré-preenchimento do Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Enviar documentos. (Consulte [Enviar documentos para o serviço do Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcule os dados do formulário. (Consulte [Cálculo dos dados de formulário](/help/forms/developing/calculating-form-data.md).)
* Otimizar um aplicativo. (Consulte [Otimizar o desempenho do serviço Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
