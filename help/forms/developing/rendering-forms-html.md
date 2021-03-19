---
title: Renderização do Forms como HTML
seo-title: Renderização do Forms como HTML
description: Use o serviço Forms para renderizar formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Você pode usar a API do Java e a API do serviço da Web para renderizar formulários como HTML.
seo-description: Use o serviço Forms para renderizar formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Você pode usar a API do Java e a API do serviço da Web para renderizar formulários como HTML.
uuid: bd8edb6f-333b-4ceb-9877-618f5377f56f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 669ede46-ea55-444b-a23f-23a86e5aff8e
role: Desenvolvedor
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '4189'
ht-degree: 1%

---


# Renderizar Forms como HTML {#rendering-forms-as-html}

**Exemplos e exemplos neste documento são apenas para o AEM Forms no ambiente JEE.**

O serviço Forms renderiza formulários como HTML em resposta a uma solicitação HTTP de um navegador da Web. Uma vantagem de renderizar um formulário como HTML é que o computador no qual o navegador da Web do cliente está localizado não requer Adobe Reader, Acrobat ou Flash Player (para Guias de formulário (obsoleto)).

Para renderizar um formulário como HTML, o design de formulário deve ser salvo como um arquivo XDP. Um design de formulário que é salvo como um arquivo PDF não pode ser renderizado como HTML. Ao desenvolver um design de formulário no Designer que será renderizado como HTML, considere os seguintes critérios:

* Não use as propriedades de borda de um objeto para desenhar linhas, caixas ou grades no seu formulário. Talvez alguns navegadores não alinhem bordas exatamente como elas aparecem em uma visualização do Objetos podem aparecer em camadas ou empurrar outros objetos para fora das posições desejadas.
* Você pode usar linhas, retângulos e círculos para definir o plano de fundo.
* Desenhar texto um pouco maior do que o que parece ser necessário para acomodar o texto. Alguns navegadores da Web não exibem o texto de forma legível.

>[!NOTE]
>
>Ao renderizar um formulário que contém imagens TIFF usando os métodos `FormServiceClient` e `renderHTMLForm2` do objeto, as imagens TIFF não são visíveis no formulário HTML renderizado exibido nos navegadores Internet Explorer ou Mozilla Firefox. `(Deprecated) renderHTMLForm` Esses navegadores não fornecem suporte nativo para imagens TIFF.

## Páginas HTML {#html-pages}

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

Quando designs de formulário são renderizados como formulários HTML, os painéis não são restritos a qualquer tamanho de página específico. Caso tenha subformulários dinâmicos, eles devem ser aninhados dentro do subformulário do painel. Os subformulários dinâmicos podem se expandir para um número infinito de páginas HTML.

Quando um formulário é renderizado como um formulário HTML, os tamanhos de página (necessários para paginar formulários renderizados como PDF) não têm significado. Como um formulário com layout flutuante pode expandir para um número infinito de páginas HTML, é importante evitar rodapés na página principal. Um rodapé abaixo da área de conteúdo em uma página principal pode substituir o conteúdo HTML que continua além do limite da página.

Você deve mover-se explicitamente do painel para o painel usando os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Você altera páginas enviando um formulário para o serviço Forms e fazendo com que o serviço Forms renderize o formulário de volta para o dispositivo cliente, normalmente um navegador da Web.

>[!NOTE]
>
>O processo de envio de um formulário para o serviço Forms e, em seguida, a renderização do formulário pelo serviço Forms para o dispositivo cliente é chamado de dados de recorte arredondado para o servidor.

>[!NOTE]
>
>Se você quiser personalizar a aparência do botão Assinatura digital de HTML em um formulário HTML, altere as seguintes propriedades no arquivo fscdigsig.css (no arquivo adobe-forms-ds.ear > adobe-forms-ds.war):

**.fsc-ds-ssb**: Essa folha de estilos é aplicável no caso de um campo de sinal em branco.

**.fsc-ds-ssv**: Essa folha de estilos é aplicável no caso de um campo de sinal válido.

**.fsc-ds-ssc**: Essa folha de estilos é aplicável no caso de um campo de sinal válido, mas os dados foram alterados.

**.fsc-ds-ssi**: Essa folha de estilos é aplicável no caso de um campo de sinal inválido.

**.fsc-ds-popup-bg**: Esta propriedade da folha de estilos não está sendo usada.

**.fsc-ds-popup-btn**: Esta propriedade da folha de estilos não está sendo usada.

## Execução de scripts {#running-scripts}

Um autor de formulário especifica se um script é executado no servidor ou no cliente. O serviço Forms cria um ambiente de processamento de evento distribuído para a execução da inteligência de formulário que pode ser distribuído entre o cliente e o servidor usando o atributo `runAt`. Para obter informações sobre esse atributo ou criar scripts em designs de formulário, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)

O serviço Forms pode executar scripts enquanto o formulário é renderizado. Como resultado, é possível pré-preencher um formulário com dados ao conectar-se a um banco de dados ou a serviços da Web que podem não estar disponíveis no cliente. Você também pode definir o evento `Click` de um botão para ser executado no servidor, para que o cliente faça o roteamento de dados para o servidor. Isso permite que o cliente execute scripts que possam exigir recursos do servidor, como um banco de dados corporativo, enquanto um usuário interage com um formulário. Para formulários HTML, scripts formcalc podem ser executados somente no servidor. Como resultado, você deve marcar esses scripts para serem executados em `server` ou `both`.

Você pode criar formulários que se movem entre páginas (painéis) ao chamar os métodos `xfa.host.pageUp` e `xfa.host.pageDown`. Esse script é colocado em um evento `Click` de botão e o atributo `runAt` é definido como `Both`. O motivo pelo qual você escolhe `Both` é para que o Adobe Reader ou Acrobat (para formulários renderizados como PDF) possam alterar páginas sem ir para o servidor e os formulários HTML podem alterar páginas ao arredondar os dados para o servidor. Ou seja, um formulário é enviado para o serviço Forms e um formulário é renderizado como HTML com a nova página exibida.

É recomendável não fornecer variáveis de script e campos de formulário com os mesmos nomes, como item. Alguns navegadores da Web, como o Internet Explorer, podem não inicializar uma variável com o mesmo nome de um campo de formulário que resulta em um erro de script. Convém fornecer campos de formulário e variáveis de script nomes diferentes.

Ao renderizar formulários HTML que contenham a funcionalidade de navegação de página e scripts de formulário (por exemplo, suponha que um script recupere dados de campo de um banco de dados toda vez que o formulário for renderizado), verifique se o script de formulário está localizado no evento form:calculate em vez de no evento form:ready .

Os scripts de formulário localizados no evento form:ready são executados apenas uma vez durante a renderização inicial do formulário e não são executados para recuperações de página subsequentes. Por outro lado, o evento form:calculate é executado para cada navegação de página em que o formulário é renderizado.

>[!NOTE]
Em um formulário multipáginas, as alterações feitas pelo JavaScript em uma página não são retidas se você mudar para uma página diferente.

Você pode invocar scripts personalizados antes de enviar um formulário. Esse recurso funciona em todos os navegadores disponíveis. No entanto, ele só pode ser usado quando usuários renderizarem o formulário HTML que tem sua propriedade `Output Type` definida como `Form Body`. Ele não funcionará quando `Output Type` for `Full HTML`. Consulte Configuração de formulários na ajuda de administração para obter as etapas para configurar esse recurso.

Primeiro, é necessário definir uma função de retorno de chamada que seja chamada antes de enviar o formulário, onde o nome da função é `_user_onsubmit`. Pressupõe-se que a função não lançará nenhuma exceção ou, se isso ocorrer, a exceção será ignorada. Recomenda-se colocar a função JavaScript na seção head do html; no entanto, você pode declará-lo em qualquer lugar antes do fim das tags de script que incluem `xfasubset.js`.

Quando o formserver renderiza um XDP que contém uma lista suspensa, além de criar a lista suspensa, ele também cria dois campos de texto ocultos. Esses campos de texto armazenam os dados da lista suspensa (um armazena o nome de exibição das opções e outro armazena o valor das opções). Portanto, toda vez que um usuário enviar o formulário, todos os dados da lista suspensa serão enviados. Supondo que você não queira enviar tantos dados toda vez, você pode gravar um script personalizado para desativar isso. Por exemplo: O nome da lista suspensa é `drpOrderedByStateProv` e é colocado sob o cabeçalho do subformulário. O nome do elemento de entrada HTML será `header[0].drpOrderedByStateProv[0]`. O nome dos campos ocultos que armazenam e enviam os dados da lista suspensa tem os seguintes nomes: `header[0].drpOrderedByStateProv_DISPLAYITEMS_[0] header[0].drpOrderedByStateProv_VALUEITEMS_[0]`

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

O subconjunto XFA define os eventos XFA que são mapeados para eventos HTML. Há uma pequena diferença no comportamento no tempo dos eventos calculate e validate. Em um navegador da Web, um evento de cálculo completo é executado ao sair de um campo. Os eventos de cálculo não são executados automaticamente quando você faz uma alteração no valor de um campo. Você pode forçar um evento calculate chamando o método `xfa.form.execCalculate`.

Em um navegador da Web, validar eventos só são executados ao sair de um campo ou enviar um formulário. Você pode forçar um evento de validação usando o método `xfa.form.execValidate`.

O Forms exibido em um navegador da Web (em vez do Adobe Reader ou Acrobat) está em conformidade com o teste nulo XFA (erros ou avisos) para campos obrigatórios.

* Se o teste nulo gerar um erro e você sair de um campo sem especificar um valor, uma caixa de mensagem será exibida e você será reposicionado ao campo depois de clicar em OK.
* Se um teste nulo gerar um aviso e você sair de um campo sem especificar um valor, será solicitado que clique em OK ou Cancelar, dando a você a opção de continuar sem especificar um valor ou retornar ao campo para inserir um valor.

Para obter mais informações sobre um teste nulo, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

## Botões de formulário {#form-buttons}

Clicar em um botão Enviar envia dados de formulário para o serviço da Forms e representa o fim do processamento do formulário. O evento `preSubmit` pode ser definido para ser executado no cliente ou servidor. O evento `preSubmit` é executado antes do envio do formulário, se ele estiver configurado para execução no cliente. Caso contrário, o evento `preSubmit` será executado no servidor durante o envio do formulário. Para obter mais informações sobre o evento `preSubmit`, consulte [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63).

Se um botão não tiver um script do lado do cliente associado a ele, os dados serão enviados para o servidor, os cálculos serão executados no servidor e o formulário HTML será gerado novamente. Se um botão contiver um script do lado do cliente, os dados não serão enviados para o servidor e o script do lado do cliente será executado no navegador da Web.

## Navegador da Web HTML 4.0 {#html-4-0-web-browser}

Um navegador da Web que suporta apenas o HTML 4.0 não pode suportar o modelo de script de cliente do subconjunto XFA. Ao criar um design de formulário para funcionar no HTML 4.0 e no MSDHTML ou CSS2HTML, um script marcado para ser executado no cliente será executado no servidor. Por exemplo, suponha que um usuário clique em um botão localizado em um formulário exibido em um navegador da Web HTML 4.0. Nessa situação, os dados do formulário são enviados para o servidor em que o script do cliente é executado.

É recomendável colocar a lógica do formulário em eventos calculate, que são executados no servidor em HTML 4.0 e no cliente para MSDHTML ou CSS2HTML.

## Manter alterações de apresentação {#maintaining-presentation-changes}

À medida que você se move entre páginas HTML (painéis), somente o estado dos dados é mantido. Configurações, como cor do plano de fundo ou configurações obrigatórias do campo, não são mantidas (se forem diferentes das configurações iniciais). Para manter o estado da apresentação, você deve criar campos (geralmente ocultos) que representem o estado da apresentação dos campos. Se você adicionar um script ao evento `Calculate` de um campo que altera a apresentação com base em valores de campo ocultos, será possível preservar o estado da apresentação conforme você se move para frente e para trás entre as páginas HTML (painéis).

O script a seguir mantém o `fillColor` de um campo com base no valor de `hiddenField`. Suponha que esse script esteja localizado em um evento `Calculate` de campo.

```java
     If (hiddenField.rawValue == 1)
         this.fillColor = "255,0,0"
     else
         this.fillColor = "0,255,0"
```

>[!NOTE]
Os objetos estáticos não são exibidos em um formulário HTML renderizado quando aninhados dentro de uma célula de tabela. Por exemplo, um círculo e um retângulo aninhados dentro de uma célula de tabela não são exibidos em um formulário HTML de renderização. No entanto, esses mesmos objetos estáticos são exibidos corretamente quando localizados fora da tabela.

## Assinatura digital de formulários HTML {#digitally-signing-html-forms}

Não é possível assinar um formulário HTML que contenha um campo de assinatura digital se o formulário for renderizado como uma das seguintes transformações HTML:

* AHTML
* HTML 4
* StaticHTML
* NoScriptXHTML

Para obter informações sobre como assinar digitalmente um documento, consulte [Assinando e certificando documentos digitalmente](/help/forms/developing/digitally-signing-certifying-documents.md)

## Renderização de um formulário XHTML compatível com diretrizes de acessibilidade {#rendering-an-accessibility-guidelines-compliant-xhtml-form}

É possível renderizar um formulário HTML completo em conformidade com as diretrizes de acessibilidade. Ou seja, o formulário é renderizado em tags HTML completas, em vez do formulário HTML ser renderizado em tags de corpo (não em uma página HTML completa).

## Validação de dados de formulário {#validating-form-data}

É recomendável limitar o uso de regras de validação para campos de formulário ao renderizar o formulário como um formulário HTML. Algumas regras de validação podem não ser compatíveis com formulários HTML. Por exemplo, quando um padrão de validação MM-DD-AAAA é aplicado a um campo `Date/Time` localizado em um design de formulário renderizado como um formulário HTML, ele não funciona corretamente, mesmo se a data for digitada corretamente. No entanto, esse padrão de validação funciona corretamente em formulários renderizados como PDF.

>[!NOTE]
Para obter mais informações sobre o serviço Forms, consulte [Referência de serviços para AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Resumo das etapas {#summary-of-steps}

Para renderizar um formulário HTML, execute as seguintes etapas:

1. Inclua arquivos de projeto.
1. Crie um objeto da API do cliente do Forms.
1. Defina as opções de tempo de execução HTML.
1. Renderize um formulário HTML.
1. Grave o fluxo de dados do formulário no navegador da Web cliente.

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um objeto de API do cliente do Forms**

Antes de poder importar dados de forma programática para uma API do cliente de formulário PDF, é necessário criar um cliente de serviço de Integração de dados de formulário. Ao criar um cliente de serviço, você define as configurações de conexão necessárias para chamar um serviço.

**Definir opções de tempo de execução HTML**

Você define opções de tempo de execução HTML ao renderizar um formulário HTML. Por exemplo, é possível adicionar uma barra de ferramentas a um formulário HTML para permitir que os usuários selecionem anexos de arquivo localizados no computador cliente ou recuperem anexos de arquivo renderizados com o formulário HTML. Por padrão, uma barra de ferramentas HTML é desativada. Para adicionar uma barra de ferramentas a um formulário HTML, você deve definir programaticamente as opções de tempo de execução. Por padrão, uma barra de ferramentas HTML consiste nos seguintes botões:

* `Home`: Fornece um link para a raiz da Web do aplicativo.
* `Upload`: Fornece uma interface de usuário para selecionar arquivos a serem anexados ao formulário atual.
* `Download`: Fornece uma interface de usuário para exibir os arquivos anexados.

Quando uma barra de ferramentas HTML é exibida em um formulário HTML, o usuário pode selecionar no máximo dez arquivos para enviar junto com os dados do formulário. Depois que os arquivos forem enviados, o serviço Forms poderá recuperar os arquivos.

Ao renderizar um formulário como HTML, você pode especificar um valor agente-usuário. Um valor agente-usuário fornece informações do navegador e do sistema. Esse é um valor opcional e você pode passar um valor de string vazio. A opção Rendering an HTML form using the Java API quick start mostra como obter um valor de agente do usuário e usá-lo para renderizar um formulário como HTML.

Os URLs HTTP para onde os dados do formulário são publicados podem ser especificados pela configuração do URL de destino usando a API do cliente de serviço do Forms ou podem ser especificados no botão Enviar contido no design de formulário XDP. Se o URL de destino for especificado no design de formulário, não defina um valor usando a API do cliente de serviço do Forms.

>[!NOTE]
A renderização de um formulário HTML com uma barra de ferramentas é opcional.

>[!NOTE]
Se um formulário AHTML for renderizado, é recomendável não adicionar uma barra de ferramentas ao formulário.

**Renderizar um formulário HTML**

Para renderizar um formulário HTML, você deve especificar um design de formulário criado no Designer e salvo como um arquivo XDP. Você também deve selecionar um tipo de transformação HTML. Por exemplo, você pode especificar o tipo de transformação HTML que renderiza um HTML dinâmico para o Internet Explorer 5.0 ou posterior.

A renderização de um formulário HTML também requer valores, como valores de URI necessários para renderizar outros tipos de formulário.

**Gravar o fluxo de dados do formulário no navegador da Web cliente**

Quando o serviço Forms renderiza um formulário HTML, ele retorna um fluxo de dados de formulário que deve ser gravado no navegador da Web cliente. Quando gravado no navegador da Web do cliente, o formulário HTML é visível para o usuário.

**Consulte também:**

[Renderizar um formulário como HTML usando a API do Java](#render-a-form-as-html-using-the-java-api)

[Renderizar um formulário como HTML usando a API do serviço da Web](#render-a-form-as-html-using-the-web-service-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Início rápido da API do Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Renderização de PDF forms interativos](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Renderização do HTML Forms com barras de ferramentas personalizadas](/help/forms/developing/rendering-html-forms-custom-toolbars.md)

[Criação de aplicativos Web que renderizam o Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Renderizar um formulário como HTML usando a API Java {#render-a-form-as-html-using-the-java-api}

Renderize um formulário HTML usando a API do Forms (Java):

1. Incluir arquivos de projeto

   Inclua arquivos JAR do cliente, como adobe-forms-client.jar, no caminho de classe do seu projeto Java.

1. Criar um objeto de API do cliente do Forms

   * Crie um objeto `ServiceClientFactory` que contenha propriedades de conexão.
   * Crie um objeto `FormsServiceClient` usando seu construtor e transmitindo o objeto `ServiceClientFactory`.

1. Definir opções de tempo de execução HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e passe um valor enum `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor da localidade para o formulário HTML, chame o método `HTMLRenderSpec` do objeto e passe um valor de string que especifique o valor da localidade. `setLocale` (Essa é uma configuração opcional.)
   * Para renderizar o formulário HTML em tags HTML completas, chame o método `HTMLRenderSpec` do objeto e passe `OutputType.FullHTMLTags`. `setOutputType` (Essa é uma configuração opcional.)

   >[!NOTE]
   Os Forms não são renderizados com êxito em HTML quando a opção `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` que é passado para o método `FormsServiceClient` do objeto). `(Deprecated) renderHTMLForm` Quando `ApplicationWebRoot` é outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário HTML

   Chame o método `FormsServiceClient` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor enum `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `com.adobe.idp.Document` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe um objeto `com.adobe.idp.Document` vazio.
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML.
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário.

   O método `(Deprecated) renderHTMLForm` retorna um objeto `FormsResult` que contém um fluxo de dados de formulário que pode ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um objeto `com.adobe.idp.Document` chamando o método `FormsResult` object &#39;s `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `com.adobe.idp.Document` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e passando o tipo de conteúdo do objeto `com.adobe.idp.Document`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie um objeto `java.io.InputStream` chamando o método `com.adobe.idp.Document` `getInputStream` do objeto.
   * Crie uma matriz de bytes e preencha-a com o fluxo de dados do formulário, chamando o método `InputStream` do objeto `read` e transmitindo a matriz de bytes como um argumento.
   * Chame o método `javax.servlet.ServletOutputStream` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**

[Renderização do Forms como HTML](#rendering-forms-as-html)

[Início rápido (modo SOAP): Renderização de um formulário HTML usando a API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-using-the-java-api)

[Inclusão de arquivos da biblioteca Java do AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Configuração das propriedades de conexão](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Renderizar um formulário como HTML usando a API do serviço da Web {#render-a-form-as-html-using-the-web-service-api}

Renderize um formulário HTML usando a API do Forms (serviço da Web):

1. Incluir arquivos de projeto

   * Crie classes proxy Java que consomem o WSDL do serviço Forms.
   * Inclua as classes proxy Java no caminho da classe.

1. Criar um objeto de API do cliente do Forms

   Crie um objeto `FormsService` e defina os valores de autenticação.

1. Definir opções de tempo de execução HTML

   * Crie um objeto `HTMLRenderSpec` usando seu construtor.
   * Para renderizar um formulário HTML com uma barra de ferramentas, chame o método `HTMLRenderSpec` do objeto e passe um valor enum `HTMLToolbar`. `setHTMLToolbar` Por exemplo, para exibir uma barra de ferramentas HTML vertical, passe `HTMLToolbar.Vertical`.
   * Para definir o valor da localidade para o formulário HTML, chame o método `HTMLRenderSpec` do objeto e passe um valor de string que especifique o valor da localidade. `setLocale` Para obter mais informações, consulte [Referência da API do AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Para renderizar o formulário HTML em tags HTML completas, chame o método `HTMLRenderSpec` do objeto e passe `OutputType.FullHTMLTags`.`setOutputType`

   >[!NOTE]
   Os Forms não são renderizados com êxito em HTML quando a opção `StandAlone` é `true` e `ApplicationWebRoot` faz referência a um servidor diferente do servidor de aplicativos J2EE que hospeda o AEM Forms (o valor `ApplicationWebRoot` é especificado usando o objeto `URLSpec` que é passado para o método `FormsServiceClient` do objeto). `(Deprecated) renderHTMLForm` Quando `ApplicationWebRoot` é outro servidor do que hospeda o AEM Forms, o valor do URI raiz da Web no console de administração precisa ser definido como o valor do URI do aplicativo da Web do Formulário. Isso pode ser feito fazendo logon no console de administração, clicando em Serviços > Forms e definindo o URI raiz da Web como https://server-name:port/FormServer. Em seguida, salve as configurações.

1. Renderizar um formulário HTML

   Chame o método `FormsService` do objeto `(Deprecated) renderHTMLForm` e passe os seguintes valores:

   * Um valor de string que especifica o nome do design de formulário, incluindo a extensão de nome de arquivo. Se você fizer referência a um design de formulário que faz parte de um aplicativo Forms, especifique o caminho completo, como `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * Um valor enum `TransformTo` que especifica o tipo de preferência HTML. Por exemplo, para renderizar um formulário HTML compatível com HTML dinâmico para o Internet Explorer 5.0 ou posterior, especifique `TransformTo.MSDHTML`.
   * Um objeto `BLOB` que contém dados para mesclar com o formulário. Se não quiser mesclar dados, passe `null`. (Consulte [Pré-preencher o Forms com layouts flutuantes](/help/forms/developing/prepopulating-forms-flowable-layouts.md#prepopulating-forms-with-flowable-layouts).)
   * O objeto `HTMLRenderSpec` que armazena as opções de tempo de execução HTML.
   * Um valor de string que especifica o valor do cabeçalho `HTTP_USER_AGENT`; por exemplo, `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. Você pode passar uma string vazia se não quiser definir esse valor.
   * Um objeto `URLSpec` que armazena valores de URI necessários para renderizar um formulário HTML. (Consulte [Especificar valores de URI](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto `java.util.HashMap` que armazena anexos de arquivo. Esse é um parâmetro opcional e você pode especificar `null` se não quiser anexar arquivos ao formulário. (Consulte [Anexar arquivos ao formulário](/help/forms/developing/rendering-interactive-pdf-forms.md).)
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método . Esse valor de parâmetro armazena o formulário renderizado.
   * Um objeto vazio `com.adobe.idp.services.holders.BLOBHolder` que é preenchido pelo método . Esse parâmetro armazenará os dados XML de saída.
   * Um objeto vazio `javax.xml.rpc.holders.LongHolder` que é preenchido pelo método . Esse argumento armazenará o número de páginas no formulário.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método . Esse argumento armazenará o valor da localidade.
   * Um objeto vazio `javax.xml.rpc.holders.StringHolder` que é preenchido pelo método . Esse argumento armazenará o valor de renderização HTML usado.
   * Um objeto vazio `com.adobe.idp.services.holders.FormsResultHolder` que conterá os resultados desta operação.

   O método `(Deprecated) renderHTMLForm` preenche o objeto `com.adobe.idp.services.holders.FormsResultHolder` passado como o último valor do argumento com um fluxo de dados de formulário que deve ser gravado no navegador da Web do cliente.

1. Gravar o fluxo de dados do formulário no navegador da Web cliente

   * Crie um objeto `FormResult` obtendo o valor do membro de dados `com.adobe.idp.services.holders.FormsResultHolder` do objeto `value`.
   * Crie um objeto `BLOB` que contenha dados de formulário chamando o método `FormsResult` do objeto `getOutputContent`.
   * Obtenha o tipo de conteúdo do objeto `BLOB` chamando seu método `getContentType`.
   * Defina o tipo de conteúdo do objeto `javax.servlet.http.HttpServletResponse` chamando seu método `setContentType` e passando o tipo de conteúdo do objeto `BLOB`.
   * Crie um objeto `javax.servlet.ServletOutputStream` usado para gravar o fluxo de dados do formulário no navegador da Web cliente, chamando o método `javax.servlet.http.HttpServletResponse` do objeto `getOutputStream`.
   * Crie uma matriz de bytes e preencha-a chamando o método `BLOB` do objeto `getBinaryData`. Essa tarefa atribui o conteúdo do objeto `FormsResult` à matriz de bytes.
   * Chame o método `javax.servlet.http.HttpServletResponse` do objeto `write` para enviar o fluxo de dados do formulário para o navegador da Web cliente. Passe a matriz de bytes para o método `write` .

**Consulte também:**

[Renderização do Forms como HTML](#rendering-forms-as-html)

[Chamada de AEM Forms usando codificação Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

