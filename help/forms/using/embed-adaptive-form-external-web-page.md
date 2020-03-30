---
title: Incorporar formulário adaptável na página da Web externa
seo-title: Incorporar formulário adaptável na página da Web externa
description: Saiba como incorporar um formulário adaptável em uma página da Web externa
seo-description: Saiba como incorporar um formulário adaptável em uma página da Web HTML externa
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Incorporar formulário adaptável na página da Web externa{#embed-adaptive-form-in-external-web-page}

Você pode [incorporar formulários adaptáveis em uma página](/help/forms/using/embed-adaptive-form-aem-sites.md) do AEM Sites ou em uma página da Web hospedada fora do AEM. O formulário adaptativo incorporado está totalmente funcional e os usuários podem preencher e enviar o formulário sem sair da página. Ajuda o usuário a permanecer no contexto de outros elementos na página da Web e a interagir simultaneamente com o formulário.

## Pré-requisitos {#prerequisites}

Execute as seguintes etapas antes de incorporar um formulário adaptável a um site externo

* Publique o formulário adaptável a ser incorporado à instância de publicação do servidor de formulários AEM.
* Crie ou identifique uma página da Web em seu site para hospedar o formulário adaptável. Certifique-se de que a página da Web possa [ler arquivos jQuery de um CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) ou tenha uma cópia local do jQuery incorporada. jQuery é necessário para renderizar um formulário adaptável.
* Quando o servidor AEM e a página da Web estiverem em domínios diferentes, execute as etapas listadas na seção, [ative o AEM Forms para fornecer formulários adaptáveis a um site](#cross-site)entre domínios.

## Incorporar formulário adaptativo {#embed-adaptive-form}

É possível incorporar um formulário adaptável inserindo algumas linhas do JavaScript na página da Web. A API no código envia uma solicitação HTTP ao servidor AEM para recursos de formulário adaptável e injeta o formulário adaptável no container de formulário especificado.

Para incorporar o formulário adaptativo:

1. Crie uma página da Web em seu site com o seguinte código:

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. No código incorporado:

   * Altere o valor da variável *options.path* com o caminho do URL de publicação do formulário adaptável. Se o servidor AEM estiver sendo executado em um caminho de contexto, verifique se o URL inclui o caminho de contexto. Por exemplo, o código acima e o adaptador de reside no mesmo servidor de formulários aem, de modo que o exemplo usa o caminho de contexto do formulário adaptável /content/forms/af/locbasic.html.
   * Substitua *options.dataRef* por atributos a serem passados pelo URL. É possível usar a variável dataref para [preencher previamente um formulário](/help/forms/using/prepopulate-adaptive-form-fields.md)adaptável.
   * Substitua *options.subjectPath* pelo caminho para um tema diferente do configurado no formulário adaptável. Como alternativa, você pode especificar o caminho do tema usando o atributo de solicitação.
   * CSS_Seletor é o seletor de CSS do container de formulário no qual o formulário adaptável está incorporado. Por exemplo, a classe css .customafsection é o seletor de CSS no exemplo acima.

O formulário adaptável é incorporado na página da Web. Observe o seguinte na forma adaptativa incorporada:

* O cabeçalho e o rodapé no formulário adaptativo original não estão incluídos no formulário incorporado.
* Os rascunhos e formulários enviados estão disponíveis na guia Rascunhos e envios no Portal de formulários.
* A ação Enviar configurada no formulário adaptável original é retida no formulário incorporado.
* As regras de formulário adaptável são retidas e totalmente funcionais no formulário incorporado.
* O direcionamento de experiência e os testes A/B configurados no formulário adaptativo original não funcionam no formulário incorporado.
* Se o Adobe Analytics estiver configurado no formulário original, os dados de análise serão capturados no servidor do Adobe Analytics. No entanto, ele não está disponível no relatório de análise do Forms.

## Topologia de amostra {#sample-topology}

A página da Web externa que incorpora o formulário adaptativo envia solicitações ao servidor AEM, que normalmente fica atrás do firewall em uma rede privada. Para garantir que as solicitações sejam direcionadas com segurança para o servidor AEM, é recomendável configurar um servidor proxy reverso.

Vamos ver um exemplo de como você pode configurar um servidor proxy reverso Apache 2.4 sem despachante. Neste exemplo, você hospedará o servidor AEM com o caminho de `/forms` contexto e mapeará `/forms` o proxy reverso. Ela garante que qualquer solicitação para `/forms` o servidor Apache seja direcionada para a instância do AEM. Essa topologia ajuda a reduzir o número de regras na camada do despachante, já que todas as solicitações com prefixo `/forms` de rota para o servidor AEM.

1. Abra o arquivo de `httpd.conf` configuração e exclua as barras de comentário das seguintes linhas de código. Como alternativa, você pode adicionar essas linhas de código no arquivo.

   ```
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Configure as regras de proxy adicionando as seguintes linhas de código no arquivo de `httpd-proxy.conf` configuração.

   ```
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Substitua `[AEM_Instance`] pelo URL de publicação do servidor AEM nas regras.

Se você não montar o servidor AEM em um caminho de contexto, as regras de proxy na camada Apache serão as seguintes:

```java
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>Se você configurar qualquer outra topologia, certifique-se de adicionar a lista de permissão Enviar, Preencher e outros URLs na camada do dispatcher.

## Best practices {#best-practices}

Ao incorporar um formulário adaptável em uma página da Web, considere as seguintes práticas recomendadas:

* Certifique-se de que as regras de estilização definidas na página da Web CSS não entrem em conflito com o objeto de formulário CSS. Para evitar conflitos, é possível reutilizar a página da Web CSS no tema do formulário adaptável usando a biblioteca do cliente AEM. Para obter informações sobre como usar a biblioteca do cliente em temas de formulário adaptáveis, consulte [Temas no AEM Forms](../../forms/using/themes.md).
* Faça com que o container de formulário na página da Web use toda a largura da janela. Isso garante que as regras de CSS configuradas para dispositivos móveis funcionem sem alterações. Se o container de formulário não tiver a largura total da janela, será necessário gravar um CSS personalizado para fazer com que o formulário se adapte a diferentes dispositivos móveis.
* Use a `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API para obter a representação XML ou JSON dos dados do formulário no cliente.
* Use a `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API para descarregar o formulário adaptável do DOM HTML.
* Configure o cabeçalho access-control-origem ao enviar resposta do servidor AEM.

## Ativar o AEM Forms para servir formulários adaptáveis a um site entre domínios {#cross-site}

1. Na instância do autor de AEM, vá para Gerenciador de configuração do console da Web de AEM em `https://'[server]:[port]'/system/console/configMgr`.
1. Localize e abra a configuração do Filtro **** de Quem indicou Apache Sling.
1. No campo Hosts permitidos, especifique o domínio em que a página da Web reside. Ela permite que o host faça solicitações POST ao servidor AEM. Também é possível usar expressão regular para especificar uma série de domínios externos de aplicativos.

