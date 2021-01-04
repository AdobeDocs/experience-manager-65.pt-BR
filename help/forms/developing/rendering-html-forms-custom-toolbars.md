---
title: Renderização de HTML Forms com barras de ferramentas personalizadas
seo-title: Renderização de HTML Forms com barras de ferramentas personalizadas
description: Use o serviço Forms para personalizar uma barra de ferramentas que é renderizada com um formulário HTML. Você pode renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java e uma API de serviço da Web.
seo-description: Use o serviço Forms para personalizar uma barra de ferramentas que é renderizada com um formulário HTML. Você pode renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java e uma API de serviço da Web.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2370'
ht-degree: 0%

---


# Renderização de HTML Forms com barras de ferramentas personalizadas {#rendering-html-forms-with-customtoolbars}

## Renderização de HTML Forms com barras de ferramentas personalizadas {#rendering-html-forms-with-custom-toolbars}

O serviço Forms permite personalizar uma barra de ferramentas que é renderizada com um formulário HTML. Uma barra de ferramentas pode ser personalizada para alterar sua aparência, substituindo os estilos CSS padrão e para adicionar comportamento dinâmico, substituindo scripts Java. Uma barra de ferramentas é personalizada usando um arquivo XML chamado fscmenu.xml. Por padrão, o serviço Forms recupera esse arquivo de um local de URI especificado internamente.

>[!NOTE]
>
>Esse local de URI está localizado no arquivo adobe-forms-core.jar, localizado no arquivo adobe-forms-dsc.jar. O arquivo adobe-forms-dsc.jar está localizado em C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Você pode usar uma ferramenta de extração de arquivos, como Win RAR, para abrir a adobe.

Você pode copiar o fscmenu.xml desse local, modificá-lo para atender aos seus requisitos e colocá-lo em um local de URI personalizado. Em seguida, usando a API de serviço do Forms, defina as opções de tempo de execução que resultam no serviço do Forms usando o arquivo fscmenu.xml do local especificado. Essas ações resultam na renderização de um formulário HTML pelo serviço Forms com uma barra de ferramentas personalizada.

Além do arquivo fscmenu.xml, também é necessário obter os seguintes arquivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS é o script Java associado a cada nó. É necessário fornecer um para o nó `div#fscmenu` e opcionalmente para os nós `ul#fscmenuItem`. Os arquivos JS implementam a funcionalidade principal da barra de ferramentas e os arquivos padrão funcionam.

fscCSS é uma folha de estilos associada a um nó específico. Os estilos nos arquivos CSS especificam a aparência da barra de ferramentas. ** fscVCSS é uma folha de estilos para uma barra de ferramentas vertical, que é exibida à esquerda do formulário HTML renderizado. ** fscIECSS é uma folha de estilos usada para formulários HTML renderizados no Internet Explorer.

Verifique se todos os arquivos acima estão referenciados no arquivo fscmenu.xml. Ou seja, no arquivo fscmenu.xml, especifique os locais de URI para apontar para esses arquivos para que o serviço Forms possa localizá-los. Por padrão, esses arquivos estão disponíveis em locais de URI que começam com palavras-chave internas `FSWebRoot` ou `ApplicationWebRoot`.

Para personalizar a barra de ferramentas, substitua as palavras-chave usando a palavra-chave externa `FSToolBarURI`. Esta palavra-chave representa o URI passado ao serviço Forms em tempo de execução (esta abordagem é mostrada posteriormente nesta seção).

Você também pode especificar os locais absolutos desses arquivos JS e CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. Nessa situação, não é necessário usar a palavra-chave `FSToolBarURI`.

>[!NOTE]
>
>Não é recomendável misturar as formas como esses arquivos são referenciados. Ou seja, todos os URIs devem ser referenciados usando a palavra-chave `FSToolBarURI` ou um local absoluto.

Você pode obter os arquivos JS e CSS abrindo o arquivo adobe-forms-&lt;appserver>.ear. Dentro desse arquivo, abra o adobe-forms-res.war. Todos esses arquivos estão localizados no arquivo WAR. O arquivo adobe-forms-&lt;appserver>.ear está localizado na pasta de instalação de formulários AEM (C:\ is the installation directory). Você pode abrir o adobe-forms-&lt;appserver>.ear usando uma ferramenta de extração de arquivos como WinRAR.

A sintaxe XML a seguir mostra um exemplo de arquivo fscmenu.xml.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>O texto em negrito representa os URIs para os arquivos CSS e JS que devem ser referenciados.

Os itens a seguir descrevem como personalizar uma barra de ferramentas:

* Altere os valores dos atributos `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` (no arquivo fscmenu.xml) para refletir os locais personalizados dos arquivos referenciados usando um dos métodos descritos nesta seção (por exemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Todos os arquivos CSS e JS devem ser especificados. Se nenhum dos arquivos for modificado, forneça o padrão no local personalizado. Você pode obter os arquivos padrão abrindo vários arquivos, conforme descrito nesta seção.
* É permitida a disponibilização de uma referência absoluta (por exemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para qualquer arquivo.
* Os arquivos JS e CSS exigidos pelo nó `div#fscmenu` são essenciais para a funcionalidade da barra de ferramentas. Nós `ul#fscmenuItem` individuais podem ou não ter arquivos JS ou CSS com suporte.

**Alteração do valor local**

Como parte da personalização de uma barra de ferramentas, é possível alterar o valor de local da barra de ferramentas. Ou seja, você pode exibi-la em outra língua. A ilustração a seguir mostra uma barra de ferramentas personalizada exibida em francês.

>[!NOTE]
>
>Não é possível criar uma barra de ferramentas personalizada em mais de um idioma. As barras de ferramentas não podem usar arquivos XML diferentes com base nas configurações de localidade.

Para alterar o valor de localidade de uma barra de ferramentas, verifique se o arquivo fscmenu.xml contém o idioma que você deseja exibir. A sintaxe XML a seguir mostra o arquivo fscmenu.xml usado para exibir uma barra de ferramentas em francês.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>Os Start rápidos associados a esta seção usam esse arquivo XML para exibir uma barra de ferramentas personalizada francesa, como mostrado na ilustração anterior.

Além disso, especifique um valor de localidade válido chamando o método `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor de localidade. Por exemplo, passe `fr_FR` para especificar francês. O serviço Forms é fornecido com barras de ferramentas localizadas.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que usa uma barra de ferramentas personalizada, é necessário saber como os formulários HTML são renderizados. (Consulte [Renderizando o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que contenha uma barra de ferramentas personalizada, execute estas tarefas:

1. Incluir arquivos de projeto.
1. Crie um objeto Forms Java API.
1. Faça referência a um arquivo XML fscmenu personalizado.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web do cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto da API Java Forms**

Antes de executar programaticamente uma operação compatível com o serviço Forms, é necessário criar um objeto cliente Forms.

**Referência a um arquivo XML fscmenu personalizado**

Para renderizar um formulário HTML que contenha uma barra de ferramentas personalizada, consulte um arquivo XML fscmenu que descreve a barra de ferramentas. (Esta seção fornece dois exemplos de um arquivo XML fscmenu.) Além disso, verifique se o arquivo fscmenu.xml especifica os locais de todos os arquivos referenciados corretamente. Conforme mencionado anteriormente nesta seção, verifique se todos os arquivos são referenciados pela palavra-chave `FSToolBarURI` ou seus locais absolutos.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, especifique um design de formulário criado no Designer e salvo como um arquivo XDP. Selecione também um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web do cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web do cliente para tornar o formulário HTML visível aos usuários.

**Consulte também:**

[Renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Como renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API de serviço da Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Start rápidos da API de serviço da Forms](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizando Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de Aplicações web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Renderize um formulário HTML que contenha uma barra de ferramentas personalizada usando a API de serviço da Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API Java Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Referência a um arquivo XML fscmenu personalizado

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e transmita um valor de enumeração `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu chamando o método `HTMLRenderSpec` do objeto `setToolbarURI` e transmitindo um valor de string que especifica o local do URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando o método `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor da localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >Os Start Rápidos associados a esta seção definem esse valor como `fr_FR`*.*

1. Renderizar um formulário HTML

   Chame o método `FormsServiceClient` do objeto `renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` que seja usado para gravar o fluxo de dados do formulário no navegador da Web do cliente chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` invocando o método `com.adobe.idp.Document` do objeto `getInputStream`.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Start rápido (modo SOAP): Como renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Incluindo arquivos da biblioteca Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Como renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API de serviço da Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Renderize um formulário HTML que contenha uma barra de ferramentas personalizada usando a Forms Service API (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o serviço Forms WSDL.
   * Inclua as classes proxy Java no seu caminho de classe.

1. Criar um objeto da API Java Forms

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Referência a um arquivo XML fscmenu personalizado

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e transmita um valor de enumeração `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu chamando o método `HTMLRenderSpec` do objeto `setToolbarURI` e transmitindo um valor de string que especifica o local do URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando o método `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor da localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >Os Start Rápidos associados a esta seção definem esse valor como `fr_FR`*.*

1. Renderizar um formulário HTML

   Chame o método `FormsService` do objeto `renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão do nome do arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor de enumeração `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados a serem unidos ao formulário. Se você não quiser unir dados, passe `null`.
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse parâmetro é opcional e você pode especificar `null` se não pretende anexar arquivos ao formulário.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método `renderHTMLForm`. Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método `renderHTMLForm`. Esse parâmetro armazena os dados XML de saída.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método `renderHTMLForm`. Esse argumento armazena o número de páginas no formulário.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método `renderHTMLForm`. Este argumento armazena o valor de localidade.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método `renderHTMLForm`. Esse argumento armazena o valor de renderização HTML usado.
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` transmitido como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web do cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e transmitindo o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` que seja usado para gravar o fluxo de dados do formulário no navegador da Web do cliente chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web do cliente. Passe a matriz de bytes para o método `write`.

**Consulte também:**

[Invocar o AEM Forms usando a codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
