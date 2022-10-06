---
title: Renderização do HTML Forms com CustomToolbars
seo-title: Rendering HTML Forms with CustomToolbars
description: Use o serviço Forms para personalizar uma barra de ferramentas renderizada com um formulário HTML. É possível renderizar um Formulário do HTML com uma barra de ferramentas personalizada usando a API do Java e uma API do serviço da Web.
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 0%

---

# Renderização do HTML Forms com CustomToolbars {#rendering-html-forms-with-customtoolbars}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

## Renderização do HTML Forms com barras de ferramentas personalizadas {#rendering-html-forms-with-custom-toolbars}

O serviço Forms permite personalizar uma barra de ferramentas renderizada com um formulário HTML. Uma barra de ferramentas pode ser personalizada para alterar sua aparência, substituindo estilos CSS padrão e adicionar comportamento dinâmico, substituindo scripts Java. Uma barra de ferramentas é personalizada usando um arquivo XML chamado fscmenu.xml. Por padrão, o serviço Forms recupera esse arquivo de um local de URI especificado internamente.

>[!NOTE]
>
>Esse local do URI está localizado no arquivo adobe-forms-core.jar, que está localizado no arquivo adobe-forms-dsc.jar. O arquivo adobe-forms-dsc.jar está localizado em C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory). Você pode usar uma ferramenta de extração de arquivos, como Win RAR, para abrir a adobe.

Você pode copiar o fscmenu.xml desse local, modificá-lo para atender aos seus requisitos e, em seguida, colocá-lo em um local de URI personalizado. Em seguida, usando a API de serviço do Forms, defina as opções de tempo de execução que resultam no serviço Forms usando o arquivo fscmenu.xml do local especificado. Essas ações resultam na renderização de um formulário HTML pelo serviço Forms com uma barra de ferramentas personalizada.

Além do arquivo fscmenu.xml, também é necessário obter os seguintes arquivos:

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS é o script Java associado a cada nó. É necessário fornecer um para a variável `div#fscmenu` nó e, opcionalmente, para `ul#fscmenuItem` nós. Os arquivos JS implementam a funcionalidade principal da barra de ferramentas e os arquivos padrão funcionam.

fscCSS é uma folha de estilos associada a um nó específico. Os estilos nos arquivos CSS especificam a aparência da barra de ferramentas. *fscVCSS* é uma folha de estilos para uma barra de ferramentas vertical, que é exibida à esquerda do formulário HTML renderizado. *fscIECSS* é uma folha de estilos usada para formulários HTML que são renderizados no Internet Explorer.

Certifique-se de que todos os arquivos acima sejam referenciados no arquivo fscmenu.xml. Ou seja, no arquivo fscmenu.xml, especifique os locais de URI para apontar para esses arquivos para que o serviço Forms possa localizá-los. Por padrão, esses arquivos estão disponíveis em locais de URI que começam com palavras-chave internas `FSWebRoot` ou `ApplicationWebRoot`.

Para personalizar a barra de ferramentas, substitua as palavras-chave usando a palavra-chave externa `FSToolBarURI`. Essa palavra-chave representa o URI passado para o serviço Forms em tempo de execução (essa abordagem é mostrada posteriormente nesta seção).

Você também pode especificar os locais absolutos desses arquivos JS e CSS, como https://www.mycompany.com/scripts/misc/fscmenu.js. Nessa situação, não é necessário usar a variável `FSToolBarURI` palavra-chave.

>[!NOTE]
>
>Não é recomendável misturar as maneiras pelas quais esses arquivos são referenciados. Ou seja, todos os URIs devem ser referenciados usando a variável `FSToolBarURI` palavra-chave ou um local absoluto.

Você pode obter os arquivos JS e CSS abrindo os adobe-forms-&lt;appserver>Arquivo .ear. Nesse arquivo, abra o adobe-forms-res.war. Todos esses arquivos estão localizados no arquivo WAR. Os formulários da adobe-&lt;appserver>O arquivo .ear está localizado na pasta de instalação dos formulários AEM (C:\ is the installation directory). Você pode abrir os adobe-forms-&lt;appserver>.ear usando uma ferramenta de extração de arquivos, como WinRAR.

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

* Altere os valores de `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` atributos (no arquivo fscmenu.xml) para refletir os locais personalizados dos arquivos referenciados usando um dos métodos descritos nesta seção (por exemplo, `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* Todos os arquivos CSS e JS devem ser especificados. Se nenhum dos arquivos for modificado, forneça o padrão no local personalizado. Você pode obter os arquivos padrão abrindo vários arquivos conforme descrito nesta seção.
* É permitido fornecer uma referência absoluta (por exemplo, https://www.example.com/scripts/custom-vertical-fscmenu.css) para qualquer arquivo.
* Os arquivos JS e CSS que a variável `div#fscmenu` são essenciais para a funcionalidade da barra de ferramentas. Individual `ul#fscmenuItem` nós podem ou não ter arquivos JS ou CSS de suporte.

**Alteração do valor local**

Como parte da personalização de uma barra de ferramentas, é possível alterar o valor do local da barra de ferramentas. Ou seja, você pode exibi-lo em outro idioma. A ilustração a seguir mostra uma barra de ferramentas personalizada exibida em francês.

>[!NOTE]
>
>Não é possível criar uma barra de ferramentas personalizada em mais de um idioma. As barras de ferramentas não podem usar arquivos XML diferentes com base nas configurações de localidade.

Para alterar o valor do local de uma barra de ferramentas, verifique se o arquivo fscmenu.xml contém o idioma que deseja exibir. A sintaxe XML a seguir mostra o arquivo fscmenu.xml usado para exibir uma barra de ferramentas em francês.

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
>Os Inícios rápidos associados a esta seção usam este arquivo XML para exibir uma barra de ferramentas personalizada em francês, como mostrado na ilustração anterior.

Além disso, especifique um valor de local válido chamando a variável `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor de localidade. Por exemplo, passar `fr_FR` para especificar francês. O serviço Forms é fornecido com barras de ferramentas localizadas.

>[!NOTE]
>
>Antes de renderizar um formulário HTML que use uma barra de ferramentas personalizada, é necessário saber como os formulários HTML são renderizados. (Consulte [Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md).)

Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML que contenha uma barra de ferramentas personalizada, execute estas tarefas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API Java do Forms.
1. Faça referência a um arquivo XML fscmenu personalizado.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, inclua os arquivos proxy.

**Criar um objeto da API Java do Forms**

Antes de executar programaticamente uma operação compatível com o serviço Forms, é necessário criar um objeto cliente Forms.

**Referência a um arquivo XML fscmenu personalizado**

Para renderizar um formulário HTML que contenha uma barra de ferramentas personalizada, consulte um arquivo XML fscmenu que descreve a barra de ferramentas. (Esta seção fornece dois exemplos de um arquivo XML fscmenu.) Além disso, verifique se o arquivo fscmenu.xml especifica os locais de todos os arquivos referenciados corretamente. Como mencionado anteriormente nesta seção, verifique se todos os arquivos são referenciados pela variável `FSToolBarURI` palavra-chave ou seus locais absolutos.

**Renderizar um formulário de HTML**

Para renderizar um formulário HTML, especifique um design de formulário que foi criado no Designer e salvo como um arquivo XDP. Selecione também um tipo de transformação HTML. Por exemplo, você pode especificar o tipo HTML transformation que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que você deve gravar no navegador da Web cliente para tornar o formulário HTML visível para os usuários.

**Consulte também**

[Renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API do Java](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API de serviço da Web](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderizar o Forms como HTML](/help/forms/developing/rendering-forms-html.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Renderizar um formulário HTML com uma barra de ferramentas personalizada usando a API do Java {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Renderize um Formulário HTML que contém uma barra de ferramentas personalizada usando a API de serviço do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto da API Java do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Referência a um arquivo XML fscmenu personalizado

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o `HTMLRenderSpec` do objeto `setHTMLToolbar` e passar um `HTMLToolbar` valor de enum. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu chamando o `HTMLRenderSpec` do objeto `setToolbarURI` e transmitindo um valor de string que especifica a localização do URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando a variável `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor de localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >O Início Rápido associado a esta seção define este valor como `fr_FR`*.*

1. Renderizar um formulário de HTML

   Chame o `FormsServiceClient` do objeto `renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor de cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `renderHTMLForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Início rápido (modo SOAP): Renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API do Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Renderização de um formulário HTML com uma barra de ferramentas personalizada usando a API de serviço da Web {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Renderize um formulário HTML que contenha uma barra de ferramentas personalizada usando a API de serviço do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto da API Java do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Referência a um arquivo XML fscmenu personalizado

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o `HTMLRenderSpec` do objeto `setHTMLToolbar` e passar um `HTMLToolbar` valor de enum. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Especifique o local do arquivo XML fscmenu chamando o `HTMLRenderSpec` do objeto `setToolbarURI` e transmitindo um valor de string que especifica a localização do URI do arquivo XML.
   * Se aplicável, defina o valor da localidade chamando a variável `HTMLRenderSpec` do objeto `setLocale` e transmitindo um valor de string que especifica o valor de localidade. O valor padrão é inglês.

   >[!NOTE]
   >
   >O Início Rápido associado a esta seção define este valor como `fr_FR`*.*

1. Renderizar um formulário de HTML

   Chame o `FormsService` do objeto `renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`.
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor de cabeçalho, como `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). Você pode passar uma string vazia se não quiser definir esse valor.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` que armazena anexos de arquivo. Esse parâmetro é opcional e você pode especificar `null` se você não pretende anexar arquivos ao formulário.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pela variável `renderHTMLForm` método . Esse valor de parâmetro armazena o formulário renderizado.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pela variável `renderHTMLForm` método . Esse parâmetro armazena os dados XML de saída.
   * Um vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pela variável `renderHTMLForm` método . Esse argumento armazena o número de páginas no formulário.
   * Um vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pela variável `renderHTMLForm` método . Esse argumento armazena o valor da localidade.
   * Um vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pela variável `renderHTMLForm` método . Esse argumento armazena o valor de renderização de HTML usado.
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `renderHTMLForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `BLOB` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
