---
title: Renderização do Forms
seo-title: Rendering Forms
description: Use o serviço Forms para criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e fornecem formulários normalmente criados no Designer. Os autores de formulários podem desenvolver um único design de formulário que o serviço Forms renderiza em PDF, SWF ou HTML em vários ambientes do navegador.
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Renderização do Forms {#rendering-forms}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

**Sobre o serviço Forms**

O serviço Forms permite criar aplicativos cliente de captura de dados interativos que validam, processam, transformam e fornecem formulários normalmente criados no Designer. Os autores de formulários podem desenvolver um único design de formulário que o serviço Forms renderiza em PDF, SWF ou HTML em vários ambientes do navegador.

Quando um usuário final solicita um formulário, um aplicativo cliente envia a solicitação ao serviço do Forms, que retorna o formulário em um formato apropriado. Assim que o serviço Forms recebe uma solicitação, ele mescla dados com um design de formulário e entrega o formulário no formato desejado. A saída do serviço de formulário é um formulário interativo, geralmente um documento PDF. Um formulário interativo permite que os usuários preencham os campos localizados no formulário.

Dependendo do tipo de aplicativo cliente, você pode gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web pode gravar o formulário no navegador da Web. Um aplicativo de desktop pode salvar o formulário como um arquivo PDF. Para demonstrar como gravar em um navegador da Web e em um arquivo PDF, o início rápido é no *Renderização do Forms* estão organizados da seguinte maneira:

* Os exemplos fortemente tipados da API Java (modo SOAP) são um servlet Java.
* Os exemplos de serviço Web (Java Base64) são um servlet Java.
* Os exemplos de serviço Web (MTOM) são um aplicativo de console (nem todos os inícios rápidos têm um exemplo de MTOM).

>[!NOTE]
>
>Para obter informações sobre como criar uma aplicação Web que use servlets java para chamar o serviço Forms, consulte [Criação de aplicações Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

Você pode passar um design de formulário (um arquivo XDP) ou um documento PDF para o serviço Forms usando uma das duas formas a seguir:

* Você pode fazer referência ao design do formulário usando um valor de URL. Esta abordagem envolve a utilização de uma `URLSpec` objeto. A raiz do conteúdo é passada para o serviço Forms usando o `URLSpec` do objeto `setContentRootURI` método. O nome do design do formulário ( `formQuery`) é passado como um parâmetro separado. Os dois valores são concatenados para obter a referência absoluta para o design do formulário. (A maioria dos inícios rápidos no *Renderização do Forms* use esta abordagem.)
* Você pode passar um `com.adobe.idp.Document` que contém o design do formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitar um `com.adobe.idp.Document` objeto que contém um design de formulário. (Consulte [Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md)

É possível realizar essas tarefas usando o serviço Forms:

* Renderizar PDF forms interativos. (Consulte [Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Renderizar formulários no cliente. (Consulte [Renderização do Forms no cliente](/help/forms/developing/rendering-forms-client.md).)
* Renderizar formulários com base em fragmentos. (Consulte [Renderização do Forms com base em fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)
* Renderizar formulários habilitados por direitos. (Consulte [Renderização do Forms com direitos ativados](/help/forms/developing/rendering-rights-enabled-forms.md).)
* Renderizar formulários como HTML. (Consulte [Renderização do Forms como HTML](/help/forms/developing/rendering-forms-html.md).)
* Renderização do HTML Forms usando arquivos CSS personalizados ([Renderização do HTML Forms usando arquivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Manipular formulários enviados. (Consulte [Manuseio de Forms enviado](/help/forms/developing/handling-submitted-forms.md).)
* Criação de Documentos PDF com Dados XML Enviados. (Consulte [Criação de documentos PDF com dados XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Preencher formulários previamente. (Consulte [Pré-preenchimento do Forms com layouts fluíveis](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Envio de documentos. (Consulte [Passar documentos para o serviço da Forms](/help/forms/developing/passing-documents-forms-service.md)
* Calcular dados do formulário. (Consulte [Cálculo de dados de formulário](/help/forms/developing/calculating-form-data.md).)
* Otimizar um aplicativo. (Consulte [Otimização do desempenho do serviço Forms](/help/forms/developing/optimizing-performance-forms-service.md).)
