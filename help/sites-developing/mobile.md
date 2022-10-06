---
title: Criação de sites para dispositivos móveis
seo-title: Creating Sites for Mobile Devices
description: A criação de um site móvel é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes
seo-description: Creating a mobile site is similar to creating a standard site as it also involves creating templates and components
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
exl-id: 21b2037a-685a-441d-aecd-865884253e03
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3840'
ht-degree: 0%

---

# Criação de sites para dispositivos móveis{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A criação de um site móvel é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes. Para obter mais detalhes sobre como criar modelos e componentes, consulte as seguintes páginas: [Modelos](/help/sites-developing/templates.md), [Componentes](/help/sites-developing/components.md) e [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md). A principal diferença consiste em ativar as funcionalidades móveis integradas AEM no site. Isso é feito criando um modelo que depende do componente página móvel.

Você também deve considerar usar [design responsivo](/help/sites-developing/responsive.md), criando um único site que acomoda vários tamanhos de tela.

Para começar, consulte o **Site de demonstração móvel We.Retail** que está disponível em AEM.

Para criar um site para dispositivos móveis, proceda da seguinte maneira:

1. Crie o componente de página:

   * Defina as `sling:resourceSuperType` propriedade para `wcm/mobile/components/page`
Dessa forma, o componente depende do componente de página móvel.

   * Crie o `body.jsp` com a lógica específica do projeto.

1. Crie o modelo de página:

   * Defina as `sling:resourceType` propriedade para o componente de página recém-criado.
   * Defina as `allowedPaths` propriedade.

1. Crie a página de design do site.
1. Crie a página raiz do site abaixo da `/content` nó:

   * Defina as `cq:allowedTemplates` propriedade.
   * Defina as `cq:designPath` propriedade.

1. Nas propriedades de página da página raiz do site, defina os grupos de dispositivos na **Celular** guia .
1. Crie as páginas do site usando o novo modelo.

O componente de página móvel ( `/libs/wcm/mobile/components/page`):

* Adiciona o **Celular** para a caixa de diálogo propriedades da página.
* Através de `head.jsp`, ele recupera o grupo de dispositivos móveis atual da solicitação e, se um grupo de dispositivos for encontrado, usa o `drawHead()` para incluir o componente de inicialização do emulador associado do grupo de dispositivos (somente no modo de autor) e o CSS de renderização do grupo de dispositivos.

>[!NOTE]
>
>A página raiz do site móvel precisa estar no nível 1 da hierarquia de nó e recomenda-se que esteja abaixo do nó /content.

## Criar um site móvel com o gerenciador de vários sites {#creating-a-mobile-site-with-the-multi-site-manager}

Use o Multi Site Manager (MSM) para criar uma live copy móvel de um site padrão. O site padrão é transformado automaticamente em um site móvel: o site para dispositivos móveis tem todos os recursos dos sites para dispositivos móveis (por exemplo, edição dentro de um emulador) e pode ser gerenciado em sincronia com o site padrão. Consulte a seção [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm.md) na página Multi Site Manager .

## API móvel do lado do servidor {#server-side-mobile-api}

Os pacotes Java contendo as classes móveis são:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - define MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - define Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - define DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - define WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - define o MobileUtil, que fornece vários métodos de utilitário que giram em torno do WCM Mobile.

### Componentes móveis {#mobile-components}

O **Site de demonstração móvel We.Retail** utiliza os seguintes componentes móveis que estão abaixo `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nome</td>
   <td>Grupo</td>
   <td>Características</td>
  </tr>
  <tr>
   <td>mobilefooter</td>
   <td>oculto</td>
   <td>- rodapé</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>Móvel</td>
   <td>- com base no componente de base da imagem<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilelista</td>
   <td>Móvel</td>
   <td>- com base no componente de base da lista<br /> - listitem_teaser.jsp renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>oculto</td>
   <td>- com base no componente de fundação do logotipo<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilereferência</td>
   <td>Móvel</td>
   <td><p>- semelhante ao componente de base de referência</p> <p>- mapeia um componente de textimage para um mobiletextimage um e um componente de imagem para um mobileimage um</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Móvel</td>
   <td>- com base no componente de base textimage<br /> - renderiza uma imagem se o dispositivo for capaz</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>oculto</td>
   <td><p>- com base no componente da fundação de topnav</p> <p>- somente renderiza texto</p> </td>
  </tr>
 </tbody>
</table>

#### Criação de um componente móvel {#creating-a-mobile-component}

A estrutura móvel AEM permite desenvolver componentes sensíveis ao dispositivo que emite a solicitação. Os exemplos de código a seguir mostram como usar a API móvel AEM em um componente jsp e particularmente como:

* Obtenha o dispositivo da solicitação:
   `Device device = slingRequest.adaptTo(Device.class);`

* Obtenha o grupo de dispositivos:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Obtenha os recursos do grupo de dispositivos:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Obtenha os atributos do dispositivo (chave/valores de recurso brutos do banco de dados WURFL):
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Obtenha o agente do usuário do dispositivo:
   `String userAgent = device.getUserAgent();`

* Obtenha a lista de grupos de dispositivos (grupos de dispositivos atribuídos ao site pelo autor) da página atual:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Verifique se o grupo de dispositivos suporta imagens
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OU

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>Em um jsp, `slingRequest` está disponível por meio do `<sling:defineObjects>` e `currentPage` através da `<cq:defineObjects>` .

### Emuladores {#emulators}

A criação baseada em emulador fornece aos autores o meio de criar páginas de conteúdo destinadas a clientes móveis. A criação de conteúdo móvel segue o mesmo princípio de edição WYSIWYG no local. Para que os autores percebam a aparência da página em um dispositivo móvel, uma página de conteúdo móvel é editada usando um emulador de dispositivo.

Os emuladores de dispositivos móveis são baseados na estrutura de emulador genérica. Para obter mais detalhes, consulte a [Emuladores](/help/sites-developing/emulators.md) página.

O emulador de dispositivo exibe o dispositivo móvel na página, enquanto a edição normal (parsys, componentes) ocorre na tela do dispositivo. O emulador de dispositivo depende dos grupos de dispositivos configurados para o site. Vários emuladores podem ser atribuídos a um grupo de dispositivos. Todos os emuladores estão disponíveis na página de conteúdo. Por padrão, o primeiro emulador atribuído ao primeiro grupo de dispositivos atribuído ao site é exibido. Os emuladores podem ser trocados por meio do carrossel do emulador na parte superior da página ou por meio do botão de edição do Sidekick.

**Criação de um emulador**

Para criar um emulador, consulte o [Criando um emulador móvel personalizado](/help/sites-developing/emulators.md) na página Emuladores genéricos.

**Principais características dos emuladores móveis**

* Um grupo de dispositivos é composto por um de mais emuladores: a página de configuração do grupo de dispositivos, por exemplo /etc/mobile/groups/touch, contém a variável `emulators` abaixo da variável `jcr:content` nó .
Observação: embora seja possível que o mesmo emulador pertença a vários grupos de dispositivos, isso não faz muito sentido.

* Na caixa de diálogo de configuração do grupo de dispositivos, a variável `emulators` é definida com o caminho do(s) emulador(es) desejado(s). Por exemplo: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Os componentes do emulador (por exemplo, `/libs/wcm/mobile/components/emulators/iPhone4`) estender o componente emulador móvel básico ( `/libs/wcm/mobile/components/emulators/base`).

* Cada componente que estende o emulador móvel básico está disponível para seleção ao configurar um grupo de dispositivos. Os emuladores personalizados podem, assim, ser facilmente criados ou estendidos.
* No momento da solicitação no modo de edição, a implementação do emulador é usada para renderizar a página.
* Quando o modelo da página depende do componente de página móvel, as funcionalidades do emulador são integradas automaticamente na página (por meio do `head.jsp` do componente de página móvel).

### Grupos de dispositivos {#device-groups}

Os grupos de dispositivos móveis fornecem segmentação de dispositivos móveis com base nos recursos do dispositivo. Um grupo de dispositivos fornece as informações necessárias para a criação baseada em emulador na instância de autor e para a renderização correta do conteúdo na instância de publicação: depois que os autores adicionarem conteúdo à página móvel e a tiverem publicado, a página poderá ser solicitada na instância de publicação. Lá, em vez da exibição de edição do emulador, a página de conteúdo é renderizada usando um dos grupos de dispositivos configurados. A seleção do grupo de dispositivos ocorre com base em [detecção de dispositivo móvel](#devicedetection). O grupo de dispositivos correspondente fornece as informações de estilo necessárias.

Os grupos de dispositivos são definidos como páginas de conteúdo abaixo `/etc/mobile/devices` e use o **Grupo de dispositivos móveis** modelo . O modelo de grupo de dispositivos serve como um modelo de configuração para definições de grupos de dispositivos no formato de páginas de conteúdo. As suas principais características são:

* Local: `/libs/wcm/mobile/templates/devicegroup`
* Caminho permitido: `/etc/mobile/groups/*`
* Componente de Página: `wcm/mobile/components/devicegroup`

#### Atribuindo grupos de dispositivos ao seu site {#assigning-device-groups-to-your-site}

Ao criar um site móvel, você precisa atribuir grupos de dispositivos ao site. O AEM fornece três grupos de dispositivos, dependendo das capacidades de renderização do HTML e do JavaScript do dispositivo:

* **Recurso** telefones, para dispositivos de recursos como o Sony Ericsson W800 com suporte para HTML básico, mas sem suporte para imagens e JavaScript.
* **Smart** telefones, para dispositivos como o Blackberry com suporte para HTML e imagens básicas, mas sem suporte para JavaScript.

* **Toque** telefones, para dispositivos como o iPad com suporte total para HTML, imagens, JavaScript e rotação de dispositivos.

Como os emuladores podem ser associados a um grupo de dispositivos (consulte a seção [Criando um grupo de dispositivos](#creating-a-device-group)), atribuir um grupo de dispositivos a um site permite que os autores selecionem entre os emuladores associados ao grupo de dispositivos para editar a página.

Para atribuir um grupo de dispositivos ao site:

1. No seu navegador, acesse **Siteadmin** console.
1. Abra a página raiz do seu site móvel abaixo **Sites**.
1. Abra as propriedades da página.
1. Selecione o **Celular** guia :

   * Defina os grupos de dispositivos.
   * Clique em **OK**.

>[!NOTE]
>
>Quando os grupos de dispositivos tiverem sido definidos para um site, eles serão herdados de todas as páginas do site.

#### Filtros do grupo de dispositivos {#device-group-filters}

Os filtros de grupo de dispositivos definem critérios com base em capacidade para determinar se um dispositivo pertence ao grupo. Ao criar um grupo de dispositivos, você pode selecionar os filtros a serem usados para avaliar dispositivos.

Em tempo de execução, quando o AEM recebe uma solicitação HTTP de um dispositivo, cada filtro associado a um grupo compara os recursos do dispositivo com critérios específicos. O dispositivo é considerado como pertencente ao grupo quando tem todos os recursos necessários para os filtros. Os recursos são recuperados do banco de dados WURFL™.

Grupos de dispositivos podem usar zero ou mais filtros para detecção de capacidade. Além disso, um filtro pode ser usado com vários grupos de dispositivos. O AEM fornece um filtro padrão que determina se o dispositivo tem os recursos selecionados para um grupo:

* CSS
* Imagens JPG e PNG
* JavaScript
* Rotação do dispositivo

Se o grupo de dispositivos não usar um filtro, os recursos selecionados que são configurados para o grupo serão os únicos recursos necessários para um dispositivo.

Para obter mais informações, consulte [Criando Filtros de Grupo de Dispositivos](/help/sites-developing/groupfilters.md).

#### Criando um grupo de dispositivos {#creating-a-device-group}

Crie um grupo de dispositivos quando os grupos que AEM instalarem não atenderem aos seus requisitos.

1. No seu navegador, acesse **Ferramentas** console.
1. Crie uma nova página abaixo **Ferramentas** > **Celular** > **Grupos de dispositivos**. No **Criar página** caixa de diálogo:

   * As **Título** enter `Special Phones`.

   * As **Nome** enter `special`.

   * Selecione o **Modelo de Grupo de Dispositivos Móveis**.
   * Clique em **Criar**.

1. No CRXDE, adicione um **static.css** arquivo que contém os estilos do grupo de dispositivos abaixo do `/etc/mobile/groups/special` nó .

1. Abra o **Telefones especiais** página.
1. Para configurar o grupo de dispositivos, clique no botão **Editar** botão ao lado **Configurações**.
No **Geral** guia :

   * **Título**: o nome do grupo de dispositivos móveis.
   * **Descrição**: descrição do grupo.
   * **User-Agent**: sequência agente-usuário na qual os dispositivos são combinados. É opcional e pode ser um regex. Exemplo: `BlackBerryZ10`
   * **Capacidades**: define se o grupo pode manipular imagens, CSS, JavaScript ou rotação de dispositivo.
   * **Largura mínima da tela** e **Altura**
   * **Desativar Emulador**: para ativar/desativar o emulador durante a edição de conteúdo.

   No **Emuladores** guia :

   * **Emuladores**: selecione os emuladores atribuídos a este grupo de dispositivos.

   No **Filtros** guia :

   * Para adicionar um filtro, clique em Adicionar item e selecione um filtro na lista suspensa.
   * Os filtros são avaliados na ordem em que são exibidos. Quando um dispositivo não atende aos critérios de um filtro, os filtros subsequentes na lista não são avaliados.



1. Clique em OK.

A caixa de diálogo de configuração do grupo de dispositivos móveis tem a seguinte aparência:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS Personalizado por Grupo de Dispositivos {#custom-css-per-device-group}

Conforme descrito anteriormente, é possível associar um CSS personalizado a uma página de grupo de dispositivos, semelhante ao CSS de uma página de design. Esse CSS é usado para influenciar a renderização específica do grupo de dispositivos do conteúdo da página no autor e na publicação. Esse CSS é então incluído automaticamente:

* Na página da instância do autor, para cada emulador usado por esse grupo de dispositivos.
* Na página da instância de publicação, se o agente de usuário da solicitação corresponder a um dispositivo móvel nesse grupo de dispositivos específico.

## Detecção de dispositivos do lado do servidor {#server-side-device-detection}

Use filtros e uma biblioteca de especificações do dispositivo para determinar os recursos do dispositivo que executa a solicitação HTTP.

### Desenvolver filtros de grupo de dispositivos {#develop-device-group-filters}

Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo. Crie quantos filtros forem necessários para direcionar os grupos necessários de recursos do dispositivo.

Crie seus filtros para que você possa usar combinações deles para definir os grupos de recursos. Normalmente, há uma sobreposição dos recursos de diferentes grupos de dispositivos. Portanto, você pode usar alguns filtros com várias definições de grupo de dispositivos.

Depois de criar um filtro, você pode usá-lo na configuração do grupo.

Para obter mais informações, acesse [Criando Filtros de Grupo de Dispositivos](/help/sites-developing/groupfilters.md).

### Usando o banco de dados WURFL™ {#using-the-wurfl-database}

AEM usa uma versão truncada do [WURFL](https://wurfl.sourceforge.net/)Banco de dados ™ para consultar recursos do dispositivo, como resolução de tela ou suporte a javascript, com base no User-Agent do dispositivo.

O código XML do banco de dados WURFL™ é representado como nós abaixo `/var/mobile/devicespecs` ao analisar a `wurfl.xml`arquivo em `/libs/wcm/mobile/devicespecs/wurfl.xml.` A expansão para nós ocorre na primeira vez que a variável `cq-mobile-core` pacote iniciado.

Os recursos do dispositivo são armazenados como propriedades do nó, e os nós representam modelos do dispositivo. Você pode usar queries para recuperar os recursos de um dispositivo ou agente de usuário.

Como o banco de dados WURFL™ está evoluindo, talvez seja necessário personalizá-lo ou substituí-lo. Para atualizar o banco de dados de dispositivos móveis, você tem as seguintes opções:

* Substitua o arquivo pela versão mais recente, se você tiver uma licença que permita esse uso. Consulte Instalando um Banco de Dados WURFL Diferente.
* Use a versão disponível no AEM e configure um regexp que corresponda às suas strings User-Agent e aponte para um dispositivo WURFL™ existente. Consulte [Adicionar uma correspondência de agente de usuário baseada em regexp](#adding-a-regexp-based-user-agent-matching).

#### Teste do mapeamento de um agente de usuário para recursos WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando um dispositivo acessa seu site móvel, o AEM detecta o dispositivo, o mapeia para um grupo de dispositivos de acordo com seus recursos e envia uma visualização da página que corresponde ao grupo de dispositivos. O grupo de dispositivos correspondente fornece as informações de estilo necessárias. Os mapeamentos podem ser testados na Página de teste do agente de usuário móvel:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Instalando um banco de dados WURFL™ diferente {#installing-a-different-wurfl-database}

O banco de dados truncado WURFL™ instalado com AEM é uma versão anterior a 30 de agosto de 2011. Se sua versão do WURFL foi lançada depois de 30 de agosto de 2011, verifique se seu uso está em conformidade com sua licença.

Para instalar um banco de dados WURFL™:

1. No CRXDE Lite, crie a seguinte pasta: `/apps/wcm/mobile/devicespecs`
1. Copie o arquivo WURFL™ para a pasta .
1. Renomeie o arquivo como `wurfl.xml`.

AEM analisa automaticamente a variável `wurfl.xml` arquivo e atualiza os nós abaixo `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando o banco de dados WURFL™ completo estiver habilitado, a análise e a ativação poderão demorar alguns minutos. Você pode assistir aos logs para obter informações de progresso.

#### Adicionar uma correspondência de agente de usuário baseada em regexp {#adding-a-regexp-based-user-agent-matching}

Adicione um agente de usuário como uma expressão regular abaixo de /apps/wcm/mobile/devicespecs/wurfl/regexp para apontar para um tipo de dispositivo WURFL™ existente.

1. Em **CRXDE Lite**, crie um nó abaixo de /apps/wcm/mobile/devicespecs/regexp, por exemplo apple_ipad_ver1.
1. Adicione as seguintes propriedades ao nó :

   * **regexp**: expressão regular definindo agentes do usuário, por exemplo: .&#42;Mozilla.&#42;iPad.&#42;AppleWebKit.&#42;Safari.&#42;
   * **deviceId**: a ID do dispositivo, conforme definido no wurfl.xml, por exemplo: apple_ipad_ver1

A configuração acima faz com que os dispositivos para os quais o User-Agent corresponde a expressão regular fornecida sejam mapeados para a ID do dispositivo apple_ipad_ver1 WURFL™, se existir.

## Detecção de dispositivo do lado do cliente {#client-side-device-detection}

Esta seção descreve como usar a detecção de AEM do lado do cliente do dispositivo para otimizar a renderização da página ou para fornecer ao cliente versões de site alternativas.

O AEM suporta a detecção do lado do cliente do dispositivo com base em `BrowserMap`. `BrowserMap` é enviado no AEM como uma biblioteca do cliente em `/etc/clientlibs/browsermap`.

`BrowserMap` O fornece três estratégias que você pode usar para fornecer um site alternativo a um cliente, que é empregado na seguinte ordem:

1. [Links alternativos](#providing-alternate-links)
1. [URL Específico do Grupo de Dispositivos](#definingdevicegroupspecificurl)
1. [URL baseado no seletor](#defining-selector-based-urls)

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca de clientes, leia o [Usar bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md) seção.

### Fornecimento de links alternativos {#providing-alternate-links}

O `PageVariantsProvider` O serviço OSGi é capaz de gerar links alternativos para sites pertencentes à mesma família. Para configurar sites a serem considerados pelo serviço, um `cq:siteVariant` deve ser adicionado ao nó `jcr:content` nó da raiz do site.

O `cq:siteVariant` O nó precisa ter as seguintes propriedades:

* `cq:childNodesMapTo` - determina a que atributo do elemento de link os nós filhos serão mapeados; é recomendável organizar o conteúdo do site de maneira que os filhos do nó raiz representem a raiz de uma variante de idioma do site global (por exemplo, `/content/mysite/en`, `/content/mysite/de`), caso em que o valor da variável `cq:childNodesMapTo` deve ser `hreflang`;
* `cq:variantDomain` - indica o `Externalizer` domínio será usado para gerar as variantes de página com URLs absolutos; se esse valor não for definido, as variantes de página serão geradas usando links relativos;
* `cq:variantFamily` - indica a família de sítios Web a que este sítio pertence; As representações múltiplas específicas do mesmo sítio web devem pertencer à mesma família;
* `media` - armazena os valores do atributo media do elemento link; é recomendável usar o nome da variável `BrowserMap` registrado `DeviceGroups`, de modo que `BrowserMap` A biblioteca pode encaminhar automaticamente os clientes para a variante correta do site.

#### PageVariantsProvider e Externalizador {#pagevariantsprovider-and-externalizer}

Quando o valor da variável `cq:variantDomain` propriedade de um `cq:siteVariant` nó não está vazio, o `PageVariantsProvider` gerará links absolutos usando esse valor como um domínio configurado para o `Externalizer` serviço. Certifique-se de configurar o `Externalizer` para refletir sua configuração.

>[!NOTE]
>
>Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Definindo um URL específico de grupo de dispositivos {#defining-a-device-group-specific-url}

Se você não quiser usar links alternativos, poderá configurar um URL global para cada `DeviceGroup`. Recomendamos criar sua própria biblioteca de clientes que incorpora o `browsermap.standard` biblioteca do cliente, mas redefine os grupos de dispositivos.

O BrowserMap foi projetado de forma que as definições de Grupos de dispositivos possam ser substituídas, criando e adicionando um novo Grupo de dispositivos com o mesmo nome ao `BrowserMap` objeto da biblioteca personalizada do cliente.

>[!NOTE]
>
>Para obter mais detalhes, leia a [Mapa personalizado do navegador](#creatingacustomisedbrowsermap) seção.

### Definir URLs com base em seletor {#defining-selector-based-urls}

Se nenhum dos mecanismos anteriores tiver sido utilizado para indicar um local alternativo para `BrowserMap`, em seguida, seletores que usarão os nomes da `DeviceGroups` será adicionado ao `URL`s, nesse caso, você deve fornecer seus próprios servlets que resolverão as solicitações.

Por exemplo, um dispositivo navegando `www.example.com/index.html` identificado como `smartphone` por O BrowserMap é encaminhado para `www.example.com/index.smartphone.html.`

### Usar O BrowserMap Em Suas Páginas {#using-browsermap-on-your-pages}

Para usar a biblioteca de cliente padrão do BrowserMap em uma página, é necessário incluir a variável `/libs/wcm/core/browsermap/browsermap.jsp` arquivo usando um `cq:include`na página `head` seção.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Além de adicionar o `BrowserMap` biblioteca de clientes em seu `JSP` arquivos, também é necessário adicionar um `cq:deviceIdentificationMode` Propriedade da string definida como `client-side` para `jcr:content` abaixo da raiz do site.

### Substituição do comportamento padrão do BrowserMap {#overriding-browsermap-s-default-behaviour}

Se você deseja personalizar `BrowserMap` - substituindo `DeviceGroups` ou adicionar mais testes - você deve criar sua própria biblioteca do lado do cliente na qual você incorpora o `browsermap.standard`biblioteca do lado do cliente.

Além disso, é necessário chamar manualmente a função `BrowserMap.forwardRequest()` em seu `JavaScript` código.

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca de clientes, leia o [Usar bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md) seção.

Depois de criar o `BrowserMap` biblioteca do cliente, sugerimos a seguinte abordagem:

1. Crie um `browsermap.jsp` no seu aplicativo

   ```xml
   <%@include file="/libs/foundation/global.jsp" %>
   <%@ taglib prefix="c" uri="https://java.sun.com/jsp/jstl/core" %>
   <%@ page import="
       com.day.cq.wcm.api.variants.PageVariant,
       com.day.cq.wcm.api.variants.PageVariantsProvider,
       com.day.cq.wcm.api.devicedetection.DeviceIdentificationMode,
       com.day.cq.wcm.api.WCMMode"
   %>
   <%
       final PageVariantsProvider p = sling.getService(PageVariantsProvider.class);
       if(p == null) {
           throw new IllegalStateException("Missing PageVariantsProvider service");
       }
       for(PageVariant v : p.getVariants(currentPage, slingRequest)) {
           final String curVar = v.getAttributes().get("data-current-variant");
           String media = v.getAttributes().get("media");
           if (media != null) {
               media = media.replaceAll(" ", "");
           }
   %>
       <link
           rel="alternate"
           data-cq-role="site.variant"
           title="<%= xssAPI.encodeForHTMLAttr(v.getTitle()) %>"
           hreflang="<%= xssAPI.encodeForHTMLAttr(v.getAttributes().get("hreflang")) %>"
           media="<%= xssAPI.encodeForHTMLAttr(media) %>"
           href="<%= xssAPI.getValidHref(v.getURL()) %>"
           <% if(curVar != null) { %> data-current-variant="<%= curVar %>"<% } %>
       />
   <%
       }
       Boolean browserMapEnabled = true;
       final DeviceIdentificationMode dim = sling.getService(DeviceIdentificationMode.class);
       String[] selectors  = slingRequest.getRequestPathInfo().getSelectors();
       boolean isPortletRequest = false;
       for (int i = 0; i < selectors.length; i++) {
           if ("portlet".equals(selectors[i])) {
               isPortletRequest = true;
               break;
           }
       }
       if (isPortletRequest) {
           log.debug("Request was made by a portlet container - BrowserMap will not be embedded");
       } else {
           final WCMMode wcmMode = WCMMode.fromRequest(slingRequest);
           boolean shouldIncludeClientLib = false;
           if (WCMMode.EDIT != wcmMode && WCMMode.PREVIEW != wcmMode && WCMMode.DESIGN != wcmMode) {
               if (dim != null) {
                   final String mode = dim.getDeviceIdentificationModeForPage(currentPage);
                   shouldIncludeClientLib = DeviceIdentificationMode.CLIENT_SIDE.equals(mode);
                   if (shouldIncludeClientLib) {
                       browserMapEnabled = (Boolean) request.getAttribute("browsermap.enabled");
                       if (browserMapEnabled == null) {
                           browserMapEnabled = true;
                       }
                   }
               }
           }
   %>
           <c:if test="<%= !browserMapEnabled %>">
               <meta name="browsermap.enabled" content="false">
           </c:if>
           <c:if test="<%= shouldIncludeClientLib %>">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
               <cq:includeClientLib categories="browsermap.custom"/>
           </c:if>
   <%
       }
   %>
   ```

1. Inclua a `broswermap.jsp` na seção do cabeçalho.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Excluir o BrowserMap de determinadas páginas {#excluding-browsermap-from-certain-pages}

Se você quiser excluir a biblioteca do BrowserMap de algumas de suas páginas em que não precisa de detecção do cliente, é possível adicionar um atributo de solicitação:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

Isso fará com que `/libs/wcm/core/browsermap/browsermap.jsp` script para adicionar uma meta tag à página que fará `BrowserMap` para não executar nenhuma detecção:

```xml
<meta name="browsermap.enabled" content="false">
```

### Testando uma versão específica de um site {#testing-a-specific-version-of-a-web-site}

Normalmente, o script BrowserMap sempre redireciona os visitantes para a versão mais adequada do site, normalmente redirecionando os visitantes para o desktop ou para o site móvel quando necessário.

Você pode forçar o dispositivo de qualquer solicitação a testar uma versão específica de um site, adicionando a variável `device` para seu URL. O URL a seguir renderizará a versão móvel do site do Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>O `wcmmode` paratemer está definido como `disabled` para simular o comportamento de uma instância de publicação.

O valor substituído do dispositivo é armazenado em um cookie para que você possa navegar em seu site sem adicionar a variável `device` para cada `URL`.

Como consequência, você precisa chamar a mesma função `URL` com o `device` defina como `browser` para voltar à versão para desktop do site.

>[!NOTE]
>
>O BrowserMap armazena o valor substituído do dispositivo em um cookie chamado `BMAP_device`. A exclusão deste cookie garantirá que o CQ forneça a versão apropriada do site de acordo com seu dispositivo atual (por exemplo, desktop ou móvel).

## Processamento de solicitação móvel {#mobile-request-processing}

AEM processa uma solicitação emitida por um dispositivo móvel que pertence ao grupo de dispositivos de toque da seguinte maneira:

1. Um iPad envia uma solicitação para a instância de publicação do AEM, por exemplo `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determina se o site da página solicitada é um site móvel (verificando se a página de primeiro nível `/content/geometrixx_mobile` estende o componente página móvel ). Em caso afirmativo:
1. AEM pesquisa os recursos do dispositivo com base no Agente do usuário no cabeçalho da solicitação.
1. AEM mapeia os recursos do dispositivo para o grupo de dispositivos e define `touch` como o seletor de grupo de dispositivos.
1. AEM redireciona a solicitação para `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM envia a resposta para a iPad:

   * `products.touch.html` é renderizado da maneira usual e é armazenável em cache.
   * Os componentes de renderização usam seletores para adaptar a apresentação.
   * AEM adiciona automaticamente o seletor móvel a todos os links internos na página.

### Estatísticas {#statistics}

Você pode obter algumas estatísticas sobre o número de solicitações que foram feitas no servidor de AEM por dispositivos móveis. O número de solicitações pode ser detalhado:

* por grupo de dispositivos e dispositivo
* por ano, mês e dia

Para exibir as estatísticas:

1. Vá para o **Ferramentas** console.
1. Abra o **Estatísticas do dispositivo** página abaixo **Ferramentas** > **Celular**.
1. Clique no link para exibir as estatísticas de um ano, mês ou dia específico.

O **Estatísticas** página tem a seguinte aparência:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>O **Estatísticas** é criada na primeira vez que um dispositivo móvel acessa AEM e é detectado. Antes disso, não está disponível.

Se você precisar gerar uma entrada nas estatísticas, poderá proceder da seguinte maneira:

1. Use um dispositivo móvel ou um emulador (como por exemplo https://chrispederick.com/work/user-agent-switcher/ no Firefox).
1. Solicite uma página para dispositivos móveis na instância do autor desabilitando o modo de criação, por exemplo:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

O **Estatísticas** agora está disponível.

### Suporte ao armazenamento em cache de páginas para links &quot;enviar link para um amigo&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Geralmente, as páginas móveis podem ser armazenadas em cache no Dispatcher, pois as páginas renderizadas para um grupo de dispositivos são diferenciadas no URL da página pelo seletor de grupo de dispositivos, por exemplo `/content/mobilepage.touch.html`. Uma solicitação para uma página móvel sem um seletor nunca é armazenada em cache, como nesse caso, a detecção do dispositivo opera e finalmente redireciona para o grupo de dispositivos correspondente (ou &quot;nomatch&quot;, nesse caso). Uma página móvel renderizada com um seletor de grupo de dispositivos é processada pelo regravador de links, que regrava todos os links dentro da página para também conter o seletor de grupo de dispositivos, impedindo que a detecção de dispositivos seja executada novamente para cada clique em uma página já qualificada.

Portanto, você pode encontrar o seguinte cenário:

O usuário Alice é redirecionado para `coolpage.feature.html`e envia esse URL para um amigo Bob que o acessa com um cliente diferente que se enquadra no `touch` grupo de dispositivos.

If `coolpage.feature.html` O é disponibilizado a partir de um cache front-end, AEM não tem a oportunidade de analisar a solicitação para descobrir que o seletor móvel não corresponde ao novo User-Agent, e Bob obtém a representação errada.

Para resolvê-lo, você pode incluir uma interface de usuário de seleção simples nas páginas, onde os usuários finais podem substituir o grupo de dispositivos selecionado pelo AEM. No exemplo acima, um link (ou um ícone) na página permite que o usuário final alterne para `coolpage.touch.html` se ele acha que o dispositivo dele é bom o suficiente para isso.
