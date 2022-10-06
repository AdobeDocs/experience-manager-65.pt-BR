---
title: Renderizar o Forms como HTML
seo-title: Rendering Forms as HTML
description: Use o serviço Forms para renderizar formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Você pode usar a API Java e a API de serviço da Web para renderizar formulários como HTML.
seo-description: Use the Forms service to render forms as HTML in response to an HTTP request from a web browser. You can use the Java API and Web Service API to render forms as HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Developer
exl-id: e6887e45-a472-41d4-9620-c56fd5b72b4c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '4150'
ht-degree: 1%

---

# Renderizar o Forms como HTML {#rendering-forms-as-html}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms renderiza formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Um benefício de renderizar um formulário como HTML é que o computador no qual o navegador da Web do cliente está localizado não requer Adobe Reader, Acrobat ou Flash Player (para Guias de formulário (obsoleto)).

Para renderizar um formulário como HTML, o design de formulário deve ser salvo como um arquivo XDP. Um design de formulário salvo como um arquivo PDF não pode ser renderizado como HTML. Ao desenvolver um design de formulário no Designer que será renderizado como HTML, considere os seguintes critérios:

* Não use as propriedades de borda de um objeto para desenhar linhas, caixas ou grades no seu formulário. Talvez alguns navegadores não alinhem bordas exatamente como elas aparecem em uma visualização do Objetos podem aparecer em camadas ou empurrar outros objetos para fora das posições desejadas.
* Você pode usar linhas, retângulos e círculos para definir o plano de fundo.
* Desenhar texto um pouco maior do que o que parece ser necessário para acomodar o texto. Alguns navegadores da Web não exibem o texto de forma legível.

>[!NOTE]
>
>Ao renderizar um formulário que contenha imagens de TIFF usando o `FormServiceClient` do objeto `(Deprecated) renderHTMLForm` e `renderHTMLForm2` métodos, as imagens do TIFF não são visíveis no formulário HTML renderizado exibido no Internet Explorer ou no Mozilla Firefox. Esses navegadores não fornecem suporte nativo para imagens TIFF.

## HTML pages {#html-pages}

Quando um design de formulário é renderizado como um formulário HTML, cada subformulário de segundo nível é renderizado como uma página HTML (painel). É possível exibir a hierarquia de um subformulário no Designer. Subformulários filho que pertencem ao subformulário raiz (o nome padrão de um subformulário raiz é form1) são os subformulários do painel. O exemplo a seguir mostra os subformulários de um design de formulário.

```java
     form1
         Master Pages
         PanelSubform1
             NestedDynamicSubform
                 TextEdit1
         PanelSubform2
             TextEdit1
         PanelSubform3
             TextEdit1
         PanelSubform4
             TextEdit1
```

Quando designs de formulário são renderizados como HTML forms, os painéis não ficam restritos a qualquer tamanho de página específico. Caso tenha subformulários dinâmicos, eles devem ser aninhados dentro do subformulário do painel. Os subformulários dinâmicos podem se expandir para um número infinito de páginas de HTML.

Quando um formulário é renderizado como HTML, os tamanhos de página (necessários para paginar formulários renderizados como PDF) não têm significado. Como um formulário com layout flutuante pode expandir para um número infinito de páginas HTML, é importante evitar rodapés na página principal. Um rodapé abaixo da área de conteúdo em uma página principal pode substituir o conteúdo de HTML que continua além do limite da página.

Você deve mover-se explicitamente do painel para o painel usando o `xfa.host.pageUp` e `xfa.host.pageDown` métodos. Você altera páginas enviando um formulário para o serviço Forms e fazendo com que o serviço Forms renderize o formulário de volta para o dispositivo cliente, normalmente um navegador da Web.

>[!NOTE]
>
>O processo de envio de um formulário para o serviço Forms e, em seguida, a renderização do formulário pelo serviço Forms para o dispositivo cliente é chamado de dados de recorte arredondado para o servidor.

>[!NOTE]
>
>Se você quiser personalizar a aparência do botão Assinatura digital do HTML em um formulário HTML, altere as seguintes propriedades no arquivo fscdigsig.css (no arquivo adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Essa folha de estilos é aplicável no caso de um campo de sinal em branco.

**.fsc-ds-ssv**: Essa folha de estilos é aplicável no caso de um campo de sinal válido.

**.fsc-ds-ssc**: Essa folha de estilos é aplicável no caso de um campo de sinal válido, mas os dados foram alterados.

**.fsc-ds-ssi**: Essa folha de estilos é aplicável no caso de um campo de sinal inválido.

**.fsc-ds-popup-bg**: Esta propriedade da folha de estilos não está sendo usada.

**.fsc-ds-popup-btn**: Esta propriedade da folha de estilos não está sendo usada.

## Execução de scripts {#running-scripts}

Um autor de formulário especifica se um script é executado no servidor ou no cliente. O serviço Forms cria um ambiente de processamento de evento distribuído para a execução da inteligência de formulário que pode ser distribuído entre o cliente e o servidor usando o `runAt` atributo. Para obter informações sobre esse atributo ou criar scripts em designs de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

O serviço Forms pode executar scripts enquanto o formulário é renderizado. Como resultado, é possível pré-preencher um formulário com dados ao conectar-se a um banco de dados ou a serviços da Web que podem não estar disponíveis no cliente. Também é possível definir um botão `Click` para ser executado no servidor, de modo que o cliente faça o percurso de dados para o servidor. Isso permite que o cliente execute scripts que possam exigir recursos do servidor, como um banco de dados corporativo, enquanto um usuário interage com um formulário. Para formulários HTML, os scripts formcalc podem ser executados somente no servidor. Como resultado, é necessário marcar esses scripts para serem executados em `server` ou `both`.

Você pode criar formulários que se movem entre páginas (painéis) ao chamar `xfa.host.pageUp` e `xfa.host.pageDown` métodos. Esse script é colocado em um botão `Click` e o `runAt` está definido como `Both`. O motivo escolhido `Both` O é configurado de forma que o Adobe Reader ou o Acrobat (para formulários renderizados como PDF) possam alterar páginas sem ir para o servidor e os formulários HTML possam alterar as páginas ao arredondar os dados para o servidor. Ou seja, um formulário é enviado para o serviço Forms e um formulário é renderizado novamente como HTML com a nova página exibida.

É recomendável não fornecer variáveis de script e campos de formulário com os mesmos nomes, como item. Alguns navegadores da Web, como o Internet Explorer, podem não inicializar uma variável com o mesmo nome de um campo de formulário que resulta em um erro de script. Convém fornecer campos de formulário e variáveis de script nomes diferentes.

Ao renderizar formulários HTML que contenham a funcionalidade de navegação de página e scripts de formulário (por exemplo, suponha que um script recupere dados de campo de um banco de dados toda vez que o formulário for renderizado), verifique se o script de formulário está localizado no evento form:calculate em vez de no evento form:ready .

Os scripts de formulário localizados no evento form:ready são executados apenas uma vez durante a renderização inicial do formulário e não são executados para recuperações de página subsequentes. Por outro lado, o evento form:calculate é executado para cada navegação de página em que o formulário é renderizado.

>[!NOTE]
Em um formulário multipáginas, as alterações feitas pelo JavaScript em uma página não são retidas se você mudar para uma página diferente.

Você pode invocar scripts personalizados antes de enviar um formulário. Esse recurso funciona em todos os navegadores disponíveis. No entanto, ele pode ser usado somente quando usuários renderizarem o formulário HTML que tem `Output Type` propriedade definida como `Form Body`. Não funcionará quando a variável `Output Type` é `Full HTML`. Consulte Configuração de formulários na ajuda de administração para obter as etapas para configurar esse recurso.

Primeiro, é necessário definir uma função de retorno de chamada que seja chamada antes de enviar o formulário, onde o nome da função é `_user_onsubmit`. Pressupõe-se que a função não lançará nenhuma exceção ou, se isso ocorrer, a exceção será ignorada. Recomenda-se colocar a função JavaScript na seção head do html; no entanto, você pode declará-la em qualquer lugar antes do fim das tags de script que incluem `xfasubset.js`.

Quando o formserver renderiza um XDP que contém uma lista suspensa, além de criar a lista suspensa, ele também cria dois campos de texto ocultos. Esses campos de texto armazenam os dados da lista suspensa (um armazena o nome de exibição das opções e outro armazena o valor das opções). Portanto, toda vez que um usuário enviar o formulário, todos os dados da lista suspensa serão enviados. Supondo que você não queira enviar tantos dados toda vez, você pode gravar um script personalizado para desativar isso. Por exemplo: O nome da lista suspensa é `drpOrderedByStateProv` e é encapsulado sob o cabeçalho do subformulário. O nome do elemento de entrada do HTML será `header[0].drpOrderedByStateProv[0]`. O nome dos campos ocultos que armazenam e enviam os dados da lista suspensa tem os seguintes nomes: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

Você pode desativar esses elementos de entrada da seguinte maneira se não quiser publicar os dados. `var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature function _user_onsubmit() { var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]"); elems[0].disabled = true; elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]"); elems[0].disabled = true; }`

```java
header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]
```

```java
var __CUSTOM_SCRIPTS_VERSION = 1; //enabling the feature
    function _user_onsubmit() {
    var elems = document.getElementsByName("header[0].drpOrderedByStateProv_DISPLAYITEMS_[0]");
    elems[0].disabled = true;
    elems = document.getElementsByName("header[0].drpOrderedByStateProv_VALUEITEMS_[0]");
    elems[0].disabled = true;
    }
```

## Subconjuntos XFA {#xfa-subsets}

Ao criar designs de formulário para renderizar como HTML, você deve restringir seus scripts ao subconjunto XFA para scripts na linguagem JavaScript.

Os scripts que são executados no cliente ou executados no cliente e no servidor devem ser gravados no subconjunto XFA. Os scripts executados no servidor podem usar o modelo de script XFA completo e também usar FormCalc. Para obter informações sobre o uso do JavaScript, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Ao executar scripts no cliente, somente o painel atual exibido pode usar o script; por exemplo, não é possível criar scripts para campos localizados no painel A quando o painel B é exibido. Ao executar scripts no servidor, todos os painéis podem ser acessados.

Você também deve tomar cuidado ao usar expressões SOM (Modelo de objeto de script) em scripts executados no cliente. Somente um subconjunto simplificado de expressões SOM é suportado por scripts executados no cliente.

## Tempo do evento {#event-timing}

O subconjunto XFA define os eventos XFA que são mapeados para eventos HTML. Há uma pequena diferença no comportamento no tempo dos eventos calculate e validate. Em um navegador da Web, um evento de cálculo completo é executado ao sair de um campo. Os eventos de cálculo não são executados automaticamente quando você faz uma alteração no valor de um campo. Você pode forçar um evento calculate chamando a função `xfa.form.execCalculate` método .

Em um navegador da Web, validar eventos só são executados ao sair de um campo ou enviar um formulário. Você pode forçar um evento de validação usando o `xfa.form.execValidate` método .

O Forms exibido em um navegador da Web (em vez do Adobe Reader ou Acrobat) está em conformidade com o teste nulo XFA (erros ou avisos) para campos obrigatórios.

* Se o teste nulo gerar um erro e você sair de um campo sem especificar um valor, uma caixa de mensagem será exibida e você será reposicionado ao campo depois de clicar em OK.
* Se um teste nulo gerar um aviso e você sair de um campo sem especificar um valor, será solicitado que clique em OK ou Cancelar, dando a você a opção de continuar sem especificar um valor ou retornar ao campo para inserir um valor.

Para obter mais informações sobre um teste nulo, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botões de formulário {#form-buttons}

Clicar em um botão Enviar envia dados de formulário para o serviço da Forms e representa o fim do processamento do formulário. O `preSubmit` pode ser definido para ser executado no cliente ou servidor. O `preSubmit` é executado antes do envio do formulário, se estiver configurado para execução no cliente. Caso contrário, a variável `preSubmit` é executado no servidor durante o envio do formulário. Para obter mais informações sobre o `preSubmit` , consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se um botão não tiver um script do lado do cliente associado a ele, os dados serão enviados para o servidor, os cálculos serão executados no servidor e o formulário HTML será gerado novamente. Se um botão contiver um script do lado do cliente, os dados não serão enviados para o servidor e o script do lado do cliente será executado no navegador da Web.

## Navegador da Web do HTML 4.0 {#html-4-0-web-browser}

Um navegador da Web que suporta apenas o HTML 4.0 não pode suportar o modelo de script de cliente do subconjunto XFA. Ao criar um design de formulário para funcionar no HTML 4.0 e no MSDHTML ou CSS2HTML, um script marcado para ser executado no cliente será executado no servidor. Por exemplo, suponha que um usuário clique em um botão localizado em um formulário exibido em um navegador da Web do HTML 4.0. Nessa situação, os dados do formulário são enviados para o servidor em que o script do cliente é executado.

É recomendável colocar a lógica do formulário em eventos calculate, que são executados no servidor no HTML 4.0 e no cliente para MSDHTML ou CSS2HTML.

## Manutenção de alterações de apresentação {#maintaining-presentation-changes}

À medida que você se move entre HTML pages (painéis), somente o estado dos dados é mantido. Configurações, como cor do plano de fundo ou configurações obrigatórias do campo, não são mantidas (se forem diferentes das configurações iniciais). Para manter o estado da apresentação, você deve criar campos (geralmente ocultos) que representem o estado da apresentação dos campos. Se você adicionar um script ao `Calculate` Caso altere a apresentação com base em valores de campo ocultos, é possível preservar o estado da apresentação conforme você move para frente e para trás entre HTML pages (painéis).

O script a seguir mantém a variável `fillColor` de um campo com base no valor de `hiddenField`. Suponha que esse script esteja localizado em um campo `Calculate` evento.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Os objetos estáticos não são exibidos em um formulário HTML renderizado quando aninhados dentro de uma célula de tabela. Por exemplo, um círculo e um retângulo aninhados dentro de uma célula de tabela não são exibidos em um formulário de HTML de renderização. No entanto, esses mesmos objetos estáticos são exibidos corretamente quando localizados fora da tabela.

## Assinatura digital de formulários HTML {#digitally-signing-html-forms}

Não é possível assinar um formulário HTML que contenha um campo de assinatura digital se o formulário for renderizado como uma das seguintes transformações de HTML:

* AHTML
* HTML 4
* StaticHTML
* NoScriptXHTML

Para obter informações sobre como assinar digitalmente um documento, consulte [Assinar e certificar documentos digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md)

## Renderização de um formulário XHTML compatível com diretrizes de acessibilidade {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

É possível renderizar um formulário HTML completo em conformidade com as diretrizes de acessibilidade. Ou seja, o formulário é renderizado em tags HTML completas, em vez do formulário HTML ser renderizado em tags body (não em uma HTML page completa).

## Validação de dados de formulário {#validating-form-data}

É recomendável limitar o uso de regras de validação para campos de formulário ao renderizar o formulário como um formulário HTML. Algumas regras de validação podem não ser compatíveis com formulários HTML. Por exemplo, quando um padrão de validação de MM-DD-AAAA é aplicado a um `Date/Time` que está localizado em um design de formulário renderizado como formulário HTML, ele não funciona corretamente, mesmo que a data seja digitada corretamente. No entanto, esse padrão de validação funciona corretamente em formulários renderizados como PDF.

>[!NOTE]
Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para o AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Defina as opções de tempo de execução do HTML.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de poder importar dados de forma programática para uma API do PDF formClient, é necessário criar um cliente de serviço de Integração de dados de formulário . Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Definir opções de tempo de execução HTML**

Você define opções de HTML de run-time ao renderizar um formulário HTML. Por exemplo, é possível adicionar uma barra de ferramentas a um formulário HTML para permitir que os usuários selecionem anexos de arquivos localizados no computador cliente ou recuperem anexos de arquivos renderizados com o formulário HTML. Por padrão, uma barra de ferramentas HTML está desativada. Para adicionar uma barra de ferramentas a um formulário HTML, é necessário definir programaticamente as opções de tempo de execução. Por padrão, uma barra de ferramentas HTML consiste nos seguintes botões:

* `Home`: Fornece um link para a raiz da Web do aplicativo.
* `Upload`: Fornece uma interface de usuário para selecionar arquivos a serem anexados ao formulário atual.
* `Download`: Fornece uma interface de usuário para exibir os arquivos anexados.

Quando uma barra de ferramentas HTML aparece em um formulário HTML, o usuário pode selecionar no máximo dez arquivos para enviar junto com os dados do formulário. Depois que os arquivos forem enviados, o serviço Forms poderá recuperar os arquivos.

Ao renderizar um formulário como HTML, é possível especificar um valor agente-usuário. Um valor agente-usuário fornece informações do navegador e do sistema. Esse é um valor opcional e você pode passar um valor de string vazio. A guia Rendering an HTML using the Java API quick start mostra como obter um valor de agente do usuário e usá-lo para renderizar um formulário como HTML.

Os URLs HTTP para onde os dados do formulário são publicados podem ser especificados pela configuração do URL de destino usando a API do cliente de serviço do Forms ou podem ser especificados no botão Enviar contido no design de formulário XDP. Se o URL de destino for especificado no design de formulário, não defina um valor usando a API do cliente de serviço do Forms.

>[!NOTE]
A renderização de um formulário HTML com uma barra de ferramentas é opcional.

>[!NOTE]
Se um formulário AHTML for renderizado, é recomendável não adicionar uma barra de ferramentas ao formulário.

**Renderizar um formulário de HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo HTML transformation que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web cliente, o formulário HTML fica visível para o usuário.

**Consulte também**

[Renderizar um formulário como HTML usando a API do Java](#render-a-form-as-html-using-the-java-api)

[Renderizar um formulário como HTML usando a API do serviço da Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do HTML Forms com barras de ferramentas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário como HTML usando a API do Java {#render-a-form-as-html-using-the-java-api}

Renderize um formulário HTML usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um `ServiceClientFactory` objeto que contém propriedades de conexão.
   * Crie um `FormsServiceClient` usando seu construtor e passando o `ServiceClientFactory` objeto.

1. Definir opções de tempo de execução HTML

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o `HTMLRenderSpec` do objeto `setHTMLToolbar` e passar um `HTMLToolbar` valor de enum. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o `HTMLRenderSpec` do objeto `setLocale` e transmita um valor de string que especifica o valor de localidade. (Essa é uma configuração opcional.)
   * Para renderizar o formulário HTML dentro de tags HTML completas, chame a função `HTMLRenderSpec` do objeto `setOutputType` método e pass `OutputType.FullHTMLTags`. (Essa é uma configuração opcional.)

   >[!NOTE]
   O Forms não é renderizado com êxito no HTML quando a variável `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o `ApplicationWebRoot` é especificado usando a variável `URLSpec` objeto passado para o `FormsServiceClient` do objeto `(Deprecated) renderHTMLForm` método ). Quando a variável `ApplicationWebRoot` for outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário de HTML

   Chame o `FormsServiceClient` do objeto `(Deprecated) renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` objeto que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um vazio `com.adobe.idp.Document` objeto.
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor do cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML.
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O `(Deprecated) renderHTMLForm` método retorna um `FormsResult` objeto que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `com.adobe.idp.Document` chamando o `FormsResult` objeto &quot;s `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `com.adobe.idp.Document` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `com.adobe.idp.Document` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie um `java.io.InputStream` chamando o `com.adobe.idp.Document` do objeto `getInputStream` método .
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderizar o Forms como HTML](#rendering-forms-as-html)

[Início rápido (modo SOAP): Renderização de um formulário HTML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário como HTML usando a API do serviço da Web {#render-a-form-as-html-using-the-web-service-api}

Renderize um formulário HTML usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um `FormsService` e definir valores de autenticação.

1. Definir opções de tempo de execução HTML

   * Crie um `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o `HTMLRenderSpec` do objeto `setHTMLToolbar` e passar um `HTMLToolbar` valor de enum. Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor de localidade para o formulário HTML, chame o `HTMLRenderSpec` do objeto `setLocale` e transmita um valor de string que especifica o valor de localidade. Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para renderizar o formulário HTML dentro de tags HTML completas, chame a função `HTMLRenderSpec` do objeto `setOutputType` método e pass `OutputType.FullHTMLTags`.

   >[!NOTE]
   O Forms não é renderizado com êxito no HTML quando a variável `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o `ApplicationWebRoot` é especificado usando a variável `URLSpec` objeto passado para o `FormsServiceClient` do objeto `(Deprecated) renderHTMLForm` método ). Quando a variável `ApplicationWebRoot` for outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário de HTML

   Chame o `FormsService` do objeto `(Deprecated) renderHTMLForm` e transmita os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` valor enum que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com o HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * A `BLOB` objeto que contém dados para mesclar com o formulário. Se você não deseja mesclar dados, use `null`. (Consulte [Pré-preenchimento do Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * O `HTMLRenderSpec` objeto que armazena opções de tempo de execução HTML.
   * Um valor de string que especifica a variável `HTTP_USER_AGENT` valor do cabeçalho; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * A `URLSpec` objeto que armazena valores de URI necessários para renderizar um formulário HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * A `java.util.HashMap` que armazena anexos de arquivo. Este é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário. (Consulte [Anexar arquivos ao formulário](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Esse valor de parâmetro armazena o formulário renderizado.
   * Um vazio `com.adobe.idp.services.holders.BLOBHolder` objeto preenchido pelo método . Esse parâmetro armazenará os dados XML de saída.
   * Um vazio `javax.xml.rpc.holders.LongHolder` objeto preenchido pelo método . Esse argumento armazenará o número de páginas no formulário.
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . Esse argumento armazenará o valor da localidade.
   * Um vazio `javax.xml.rpc.holders.StringHolder` objeto preenchido pelo método . Esse argumento armazenará o valor de renderização de HTML usado.
   * Um vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O `(Deprecated) renderHTMLForm` O método preenche a variável `com.adobe.idp.services.holders.FormsResultHolder` objeto que é passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um `FormResult` obtendo o valor da variável `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value` membro de dados.
   * Crie um `BLOB` objeto que contém dados de formulário chamando o `FormsResult` do objeto `getOutputContent` método .
   * Obtenha o tipo de conteúdo da variável `BLOB` ao invocar seu `getContentType` método .
   * Defina as `javax.servlet.http.HttpServletResponse` tipo de conteúdo do objeto, chamando seu `setContentType` e a transmissão do tipo de conteúdo do `BLOB` objeto.
   * Crie um `javax.servlet.ServletOutputStream` objeto usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream` método .
   * Crie uma matriz de bytes e preencha-a chamando a variável `BLOB` do objeto `getBinaryData` método . Essa tarefa atribui o conteúdo da `FormsResult` para a matriz de bytes.
   * Chame o `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Transmita a matriz de bytes para a `write` método .

**Consulte também**

[Renderizar o Forms como HTML](#rendering-forms-as-html)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
