---
title: Renderizando Forms
seo-title: Renderizando Forms
description: 'null'
seo-description: nulo
uuid: 68d7b7bc-7730-4a83-b7b9-ebe2a29d6c51
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/performing_service_operations_using_apis
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: f8749793-e53f-4812-a093-8278f480e6a8
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Renderizando Forms {#rendering-forms}

**Sobre o serviço Forms**

O serviço Forms permite que você crie aplicativos clientes de captura de dados interativos que validam, processam, transformam e entregam formulários normalmente criados no Designer. Os autores de formulários podem desenvolver um único design de formulário que o serviço Forms renderiza em PDF, SWF ou HTML em vários ambientes de navegador.

Quando um usuário final solicita um formulário, um aplicativo cliente envia a solicitação para o serviço Forms, que retorna o formulário no formato apropriado. Assim que o serviço Forms receber uma solicitação, ele mesclará os dados com um design de formulário e, em seguida, fornecerá o formulário no formato desejado. A saída do serviço de formulário é um formulário interativo, geralmente um documento PDF. Um formulário interativo permite que os usuários preencham campos localizados no formulário.

Dependendo do tipo de aplicativo cliente, é possível gravar o formulário em um navegador da Web cliente ou salvá-lo como um arquivo PDF. Um aplicativo baseado na Web pode gravar o formulário no navegador da Web. Um aplicativo de desktop pode salvar o formulário como um arquivo PDF. Para demonstrar como gravar em um navegador da Web e em um arquivo PDF, os start rápidos localizados na seção *Renderização do Forms* são organizados da seguinte maneira:

* Os exemplos de API Java fortemente digitados (modo SOAP) são um servlet Java.
* Os exemplos do serviço da Web (Java Base64) são um servlet Java.
* Os exemplos do serviço da Web (MTOM) são um aplicativo de console (nem todos os start rápidos têm um exemplo MTOM).

>[!NOTE]
>
>Para obter informações sobre como criar um aplicativo da Web que usa servlets java para chamar o serviço Forms, consulte [Criação de Aplicações web que renderiza Forms](/help/forms/developing/creating-web-applications-renders-forms.md).

É possível enviar um design de formulário (um arquivo XDP) ou um documento PDF para o serviço Forms de uma das duas maneiras:

* É possível fazer referência ao design de formulário usando um valor de URL. Essa abordagem envolve o uso de um objeto `URLSpec`. A raiz do conteúdo é passada para o serviço Forms usando o método `URLSpec` do objeto `setContentRootURI`. O nome do design de formulário ( `formQuery`) é transmitido como um parâmetro separado. Os dois valores são concatenados para obter a referência absoluta ao design de formulário. (A maioria dos start rápidos localizados na seção *Renderizar Forms* usam essa abordagem.)
* Você pode enviar um `com.adobe.idp.Document` que contenha o design de formulário para o serviço Forms. Dois novos métodos chamados `renderPDFForm2` e `renderHTMLForm2` aceitam um objeto `com.adobe.idp.Document` que contém um design de formulário. (Consulte [Passando Documentos para o Forms Service](/help/forms/developing/passing-documents-forms-service.md)

É possível realizar essas tarefas usando o serviço Forms:

* Renderizar PDF forms interativos. (Consulte [Renderizando PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md).)
* Renderize formulários no cliente. (Consulte [Renderizando o Forms no Client](/help/forms/developing/rendering-forms-client.md).)
* Renderize formulários com base em fragmentos. (Consulte [Renderizando o Forms com base em fragmentos](/help/forms/developing/rendering-forms-based-fragments.md).)
* Renderizar formulários habilitados por direitos. (Consulte [Renderizando o Forms](/help/forms/developing/rendering-rights-enabled-forms.md) habilitado para direitos.)
* Renderize formulários como HTML. (Consulte [Renderizando o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)
* Renderizando HTML Forms usando arquivos CSS personalizados ([Renderizando HTML Forms usando arquivos CSS personalizados](/help/forms/developing/rendering-html-forms-using-custom.md).)
* Manipule formulários enviados. (Consulte [Manuseio do Forms](/help/forms/developing/handling-submitted-forms.md) submetido.)
* Criação de Documentos PDF com dados XML enviados. (Consulte [Criação de Documentos PDF com dados XML enviados](/help/forms/developing/creating-pdf-documents-submitted-xml.md).)
* Pré-preencher formulários. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md).)
* Passando Documentos. (Consulte [Passando Documentos para o Forms Service](/help/forms/developing/passing-documents-forms-service.md)
* Calcule os dados do formulário. (Consulte [Calculando Dados de Formulário](/help/forms/developing/calculating-form-data.md).)
* Otimizar um aplicativo. (Consulte [Otimizando o desempenho do serviço Forms](/help/forms/developing/optimizing-performance-forms-service.md).)

   ***Dica **: O site do Adobe Developer contém o seguinte artigo que discute como criar um aplicativo ASP.NET que chama o serviço Forms e renderiza formulários. Consulte [Criação de aplicativos ASP.NET de renderização de formulário](https://www.adobe.com/devnet/livecycle/articles/asp_net.html).*

