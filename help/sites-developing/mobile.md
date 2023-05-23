---
title: Criação de sites para dispositivos móveis
seo-title: Creating Sites for Mobile Devices
description: Criar um site para dispositivos móveis é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes
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
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

A criação de um site para dispositivos móveis é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes. Para obter mais detalhes sobre a criação de modelos e componentes, consulte as seguintes páginas: [Modelos](/help/sites-developing/templates.md), [Componentes](/help/sites-developing/components.md) e [Introdução ao desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md). A principal diferença consiste em habilitar as funcionalidades móveis integradas do AEM no site. Isso é feito criando um modelo que depende do componente de página para dispositivos móveis.

Considere também usar [design responsivo](/help/sites-developing/responsive.md), criando um único site que acomoda vários tamanhos de tela.

Para começar, você pode dar uma olhada no **Site de demonstração móvel do We.Retail** que está disponível no AEM.

Para criar um site para dispositivos móveis, proceda da seguinte maneira:

1. Crie o componente de página:

   * Defina o `sling:resourceSuperType` propriedade para `wcm/mobile/components/page`
Dessa forma, o componente depende do componente de página móvel.

   * Crie o `body.jsp` com a lógica específica do projeto.

1. Crie o modelo de página:

   * Defina o `sling:resourceType` para o componente de página recém-criado.
   * Defina o `allowedPaths` propriedade.

1. Crie a página de design do site.
1. Crie a página raiz do site abaixo de `/content` nó:

   * Defina o `cq:allowedTemplates` propriedade.
   * Defina o `cq:designPath` propriedade.

1. Nas propriedades de página da página raiz do site, defina os grupos de dispositivos na **Dispositivo móvel** guia.
1. Crie as páginas do site usando o novo modelo.

O componente de página móvel ( `/libs/wcm/mobile/components/page`):

* Adiciona o **Dispositivo móvel** para a caixa de diálogo de propriedades da página.
* Através da sua `head.jsp`, ele recupera o grupo de dispositivos móveis atual da solicitação e, se um grupo de dispositivos for encontrado, usa o da `drawHead()` método para incluir o componente init do emulador associado ao grupo de dispositivos (somente no modo autor) e o CSS de renderização do grupo de dispositivos.

>[!NOTE]
>
>A página raiz do site móvel precisa estar no nível 1 da hierarquia de nó e é recomendável estar abaixo do nó /content.

## Criação de um site móvel com o Gerenciador de vários sites {#creating-a-mobile-site-with-the-multi-site-manager}

Use o Gerenciador de vários sites (MSM) para criar uma live copy para dispositivos móveis a partir de um site padrão. O site padrão é transformado automaticamente em um site móvel: o site móvel tem todos os recursos dos sites móveis (por exemplo, edição em um emulador) e pode ser gerenciado em sincronia com o site padrão. Consulte a seção [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm.md) na página Gerenciamento de vários sites.

## API móvel do lado do servidor {#server-side-mobile-api}

Os pacotes Java que contêm as classes móveis são:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - define MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - define Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.capability](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - define DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - define WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - define MobileUtil, que fornece vários métodos de utilitário que giram em torno do WCM Mobile.

### Componentes para portáteis {#mobile-components}

A variável **Site de demonstração móvel do We.Retail** usa os seguintes componentes móveis localizados abaixo `/libs/foundation/components`:

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
   <td>mobileiimage</td>
   <td>Móvel</td>
   <td>- com base no componente de base da imagem<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilelist</td>
   <td>Móvel</td>
   <td>- com base no componente de base da lista<br /> - listitem_teaser.jsp renderiza uma imagem se o dispositivo for compatível<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>oculto</td>
   <td>- baseado no componente logo foundation<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>Móvel</td>
   <td><p>- semelhante ao componente de base de referência</p> <p>- mapeia um componente textimage para um mobiletextimage e um componente de imagem para um mobiletextimage</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Móvel</td>
   <td>- com base no componente textimage foundation<br /> - renderiza uma imagem se o dispositivo for capaz</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>oculto</td>
   <td><p>- com base no componente de fundação topnav</p> <p>- apenas renderiza texto</p> </td>
  </tr>
 </tbody>
</table>

#### Criação de um componente para dispositivos móveis {#creating-a-mobile-component}

A estrutura móvel AEM permite desenvolver componentes sensíveis ao dispositivo que emite a solicitação. Os exemplos de código a seguir mostram como usar a API móvel do AEM em um componente jsp e, em particular, como:

* Obter o dispositivo da solicitação:
   `Device device = slingRequest.adaptTo(Device.class);`

* Obter o grupo de dispositivos:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Obter os recursos do grupo de dispositivos:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Obtenha os atributos do dispositivo (chave/valores de recurso bruto do banco de dados WURFL):
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Obter o agente do usuário do dispositivo:
   `String userAgent = device.getUserAgent();`

* Obtenha a lista de grupos de dispositivos (grupos de dispositivos atribuídos ao site pelo autor) da página atual:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Verificar se o grupo de dispositivos dá suporte a imagens
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OU

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>Em um jsp, `slingRequest` está disponível por meio da `<sling:defineObjects>` tag e `currentPage` por meio da `<cq:defineObjects>` tag.

### Emuladores {#emulators}

A criação baseada em emulador fornece aos autores os meios de criar páginas de conteúdo destinadas a clientes móveis. A criação de conteúdo móvel segue o mesmo princípio de edição WYSIWYG no local. Para que os autores percebam a aparência da página em um dispositivo móvel, uma página de conteúdo móvel é editada usando um emulador de dispositivo.

Os emuladores de dispositivos móveis são baseados na estrutura de emulador genérico. Para obter mais detalhes, consulte [Emuladores](/help/sites-developing/emulators.md) página.

O emulador de dispositivo exibe o dispositivo móvel na página, enquanto a edição normal (parsys, componentes) ocorre na tela do dispositivo. O emulador de dispositivo depende dos grupos de dispositivos configurados para o site. Vários emuladores podem ser atribuídos a um grupo de dispositivos. Todos os emuladores ficam disponíveis na página de conteúdo. Por padrão, o primeiro emulador atribuído ao primeiro grupo de dispositivos atribuído ao site é exibido. Os emuladores podem ser alternados pelo carrossel do emulador na parte superior da página ou pelo botão de edição do Sidekick.

**Criando um emulador**

Para criar um emulador, consulte [Criação de um emulador móvel personalizado](/help/sites-developing/emulators.md) na página Emuladores genéricos.

**Características principais de emuladores móveis**

* Um grupo de dispositivos é composto de um ou mais emuladores: a página de configuração do grupo de dispositivos, por exemplo, /etc/mobile/groups/touch, contém a variável `emulators` abaixo do `jcr:content` nó.
Observação: embora seja possível que o mesmo emulador pertença a vários grupos de dispositivos, isso não faz muito sentido.

* Por meio da caixa de diálogo de configuração do grupo de dispositivos, a variável `emulators` A propriedade é definida com o caminho dos emuladores desejados. Por exemplo: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Os componentes do emulador (por exemplo, `/libs/wcm/mobile/components/emulators/iPhone4`) estender o componente base do emulador móvel ( `/libs/wcm/mobile/components/emulators/base`).

* Todos os componentes que estendem o emulador móvel básico estão disponíveis para seleção ao configurar um grupo de dispositivos. Os emuladores personalizados podem, portanto, ser facilmente criados ou estendidos.
* Quando solicitado, no modo de edição, a implementação do emulador é usada para renderizar a página.
* Quando o modelo da página depende do componente de página móvel, as funcionalidades do emulador são integradas automaticamente na página (por meio do `head.jsp` do componente de página móvel).

### Grupos de dispositivos {#device-groups}

Os grupos de dispositivos móveis fornecem segmentação de dispositivos móveis com base nos recursos do dispositivo. Um grupo de dispositivos fornece as informações necessárias para a criação baseada em emulador na instância de autor e para a renderização correta do conteúdo na instância de publicação: depois que os autores adicionam conteúdo à página móvel e a publicam, a página pode ser solicitada na instância de publicação. Lá, em vez do modo de exibição de edição do emulador, a página de conteúdo é renderizada usando um dos grupos de dispositivos configurados. A seleção do grupo de dispositivos ocorre com base em [detecção de dispositivo móvel](#devicedetection). O grupo de dispositivos correspondente fornece as informações de estilo necessárias.

Os grupos de dispositivos são definidos como páginas de conteúdo abaixo `/etc/mobile/devices` e use o **Grupo de dispositivos móveis** modelo. O modelo de grupo de dispositivos serve como um modelo de configuração para definições de grupo de dispositivos na forma de páginas de conteúdo. Suas principais características são:

* Local: `/libs/wcm/mobile/templates/devicegroup`
* Caminho permitido: `/etc/mobile/groups/*`
* Componente de Página: `wcm/mobile/components/devicegroup`

#### Atribuindo Grupos de Dispositivos ao Site {#assigning-device-groups-to-your-site}

Ao criar um site para dispositivos móveis, você precisa atribuir grupos de dispositivos ao seu site. O AEM fornece três grupos de dispositivos, dependendo do HTML do dispositivo e das capacidades de renderização do JavaScript:

* **Recurso** telefones, para dispositivos de recursos como o Sony Ericsson W800 com suporte para HTML básico, mas sem suporte para imagens e JavaScript.
* **Smart** telefones, para dispositivos como o Blackberry, com suporte para HTML e imagens básicas, mas sem suporte para JavaScript.

* **Toque** telefones, para dispositivos como o iPad, com suporte total para HTML, imagens, JavaScript e rotação de dispositivo.

Como os emuladores podem ser associados a um grupo de dispositivos (consulte a seção [Criando um grupo de dispositivos](#creating-a-device-group)), atribuir um grupo de dispositivos a um site permite que os autores selecionem entre os emuladores associados ao grupo de dispositivos para editar a página.

Para atribuir um grupo de dispositivos ao site:

1. No navegador, acesse o menu **Siteadmin** console.
1. Abra a página raiz do seu site para dispositivos móveis abaixo **Sites**.
1. Abra as propriedades da página.
1. Selecione o **Dispositivo móvel** guia:

   * Defina os grupos de dispositivos.
   * Clique em **OK**.

>[!NOTE]
>
>Quando os grupos de dispositivos tiverem sido definidos para um site, eles serão herdados por todas as páginas do site.

#### Filtros do grupo de dispositivos {#device-group-filters}

Os filtros de grupo de dispositivos definem critérios baseados em recursos para determinar se um dispositivo pertence ao grupo. Ao criar um grupo de dispositivos, você pode selecionar os filtros a serem usados para avaliar dispositivos.

No tempo de execução quando o AEM recebe uma solicitação HTTP de um dispositivo, cada filtro associado a um grupo compara os recursos do dispositivo com critérios específicos. O dispositivo é considerado como pertencente ao grupo quando tem todos os recursos que os filtros exigem. Os recursos são recuperados do banco de dados WURFL™.

Os grupos de dispositivos podem usar zero ou mais filtros para a detecção de recursos. Além disso, um filtro pode ser usado com vários grupos de dispositivos. O AEM fornece um filtro padrão que determina se o dispositivo tem os recursos selecionados para um grupo:

* CSS
* Imagens JPG e PNG
* JavaScript
* Rotação do dispositivo

Se o grupo de dispositivos não usar um filtro, os recursos selecionados que são configurados para o grupo serão os únicos recursos exigidos por um dispositivo.

Para obter mais informações, consulte [Criando filtros do grupo de dispositivos](/help/sites-developing/groupfilters.md).

#### Criando um grupo de dispositivos {#creating-a-device-group}

Crie um grupo de dispositivos quando os grupos instalados pelo AEM não atenderem aos seus requisitos.

1. No navegador, acesse o menu **Ferramentas** console.
1. Criar uma nova página abaixo **Ferramentas** > **Dispositivo móvel** > **Grupos de dispositivos**. No **Criar página** diálogo:

   * Como **Título** inserir `Special Phones`.

   * Como **Nome** inserir `special`.

   * Selecione o **Modelo do grupo de dispositivos móveis**.
   * Clique em **Criar**.

1. No CRXDE, adicione um **static.css** arquivo que contém os estilos do grupo de dispositivos abaixo de `/etc/mobile/groups/special` nó.

1. Abra o **Telefones especiais** página.
1. Para configurar o grupo de dispositivos, clique no link **Editar** botão ao lado **Configurações**.
No **Geral** guia:

   * **Título**: o nome do grupo de dispositivos móveis.
   * **Descrição**: descrição do grupo.
   * **User-Agent**: sequência user-agent com a qual os dispositivos são comparados. É opcional e pode ser um regex. Exemplo: `BlackBerryZ10`
   * **Capacidades**: define se o grupo pode lidar com imagens, CSS, JavaScript ou rotação de dispositivo.
   * **Largura mínima da tela** e **Altura**
   * **Desativar emulador**: para ativar/desativar o emulador durante a edição de conteúdo.

   No **Emuladores** guia:

   * **Emuladores**: selecione os emuladores atribuídos a esse grupo de dispositivos.

   No **Filtros** guia:

   * Para adicionar um filtro, clique em Add Item e selecione um filtro na lista suspensa.
   * Os filtros são avaliados na ordem em que são exibidos. Quando um dispositivo não atende aos critérios de um filtro, os filtros subsequentes da lista não são avaliados.



1. Clique em OK.

A caixa de diálogo de configuração do grupo de dispositivos móveis tem a seguinte aparência:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personalizado por grupo de dispositivos {#custom-css-per-device-group}

Como descrito anteriormente, é possível associar um CSS personalizado a uma página de grupo de dispositivos, de modo semelhante ao CSS de uma página de design. Esse CSS é usado para influenciar a renderização específica do grupo de dispositivos do conteúdo da página no autor e na publicação. Esse CSS é então incluído automaticamente:

* Na página na instância do autor de cada emulador usado por esse grupo de dispositivos.
* Na página da instância de publicação, se o agente de usuário da solicitação corresponder a um dispositivo móvel nesse grupo de dispositivos específico.

## Detecção de dispositivo do lado do servidor {#server-side-device-detection}

Use filtros e uma biblioteca de especificações de dispositivo para determinar os recursos do dispositivo que executa a solicitação HTTP.

### Desenvolver filtros do grupo de dispositivos {#develop-device-group-filters}

Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de recursos do dispositivo. Crie quantos filtros forem necessários para direcionar os grupos necessários de recursos do dispositivo.

Crie seus filtros para poder usar combinações deles para definir os grupos de recursos. Normalmente, há uma sobreposição das capacidades de diferentes grupos de dispositivos. Portanto, você pode usar alguns filtros com várias definições de grupo de dispositivos.

Depois de criar um filtro, você pode usá-lo na configuração do grupo.

Para obter mais informações, acesse [Criando filtros do grupo de dispositivos](/help/sites-developing/groupfilters.md).

### Usando o banco de dados WURFL™ {#using-the-wurfl-database}

O AEM usa uma versão truncada do [WURFL](https://wurfl.sourceforge.net/)™ para consultar os recursos do dispositivo, como a resolução de tela ou o suporte a javascript, com base no usuário-agente do dispositivo.

O código XML do banco de dados WURFL™ é representado como nós abaixo `/var/mobile/devicespecs` analisando o `wurfl.xml`arquivo em `/libs/wcm/mobile/devicespecs/wurfl.xml.` A expansão para nós ocorre na primeira vez que a variável `cq-mobile-core` o pacote foi iniciado.

Os recursos do dispositivo são armazenados como propriedades do nó, e os nós representam modelos de dispositivo. Você pode usar as consultas para recuperar os recursos de um dispositivo ou agente do usuário.

Como o banco de dados WURFL™ está evoluindo, talvez seja necessário personalizá-lo ou substituí-lo. Para atualizar o banco de dados de dispositivos móveis, você tem as seguintes opções:

* Substitua o arquivo pela versão mais recente, se você tiver uma licença que permita esse uso. Consulte Instalação de um Banco de Dados WURFL Diferente.
* Use a versão disponível no AEM e configure um regexp que corresponda às strings do usuário-agente e aponte para um dispositivo WURFL™ existente. Consulte [Adicionar uma correspondência usuário-agente baseada em regexp](#adding-a-regexp-based-user-agent-matching).

#### Teste do mapeamento de um usuário-agente para recursos WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando um dispositivo acessa o site móvel, o AEM detecta o dispositivo, mapeia-o para um grupo de dispositivos de acordo com seus recursos e envia uma visualização da página que corresponde ao grupo de dispositivos. O grupo de dispositivos correspondente fornece as informações de estilo necessárias. Os mapeamentos podem ser testados na página Teste de usuário-agente móvel:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Instalando um Banco de Dados WURFL™ Diferente {#installing-a-different-wurfl-database}

O banco de dados truncado WURFL™ instalado com AEM é uma versão anterior a 30 de agosto de 2011. Se sua versão do WURFL foi lançada após 30 de agosto de 2011, verifique se seu uso está em conformidade com sua licença.

Para instalar um banco de dados WURFL™:

1. No CRXDE Lite, crie a seguinte pasta: `/apps/wcm/mobile/devicespecs`
1. Copie o arquivo WURFL™ para a pasta.
1. Renomear o arquivo como `wurfl.xml`.

O AEM analisa automaticamente a variável `wurfl.xml` arquivo e atualiza os nós abaixo `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando o banco de dados WURFL™ completo estiver habilitado, a análise e a ativação poderão levar alguns minutos. Você pode observar os logs para obter informações sobre o progresso.

#### Adicionar uma correspondência usuário-agente baseada em regexp {#adding-a-regexp-based-user-agent-matching}

Adicione um user-agent como uma expressão regular abaixo /apps/wcm/mobile/devicspecs/wurfl/regexp para apontar para um tipo de dispositivo WURFL™ existente.

1. Entrada **CRXDE Lite**, crie um nó abaixo /apps/wcm/mobile/devices/regexp, por exemplo, apple_ipad_ver1.
1. Adicione as seguintes propriedades ao nó:

   * **regexp**: expressão regular que define agentes do usuário, por exemplo: .&#42;Mozilla.&#42;iPad.&#42;AppleWebKit.&#42;Safari.&#42;
   * **deviceId**: a ID do dispositivo conforme definida no wurfl.xml, por exemplo: apple_ipad_ver1

A configuração acima faz com que os dispositivos para os quais o usuário-agente corresponde à expressão regular fornecida sejam mapeados para a ID de dispositivo apple_ipad_ver1 WURFL™, se existir.

## Detecção de dispositivo no lado do cliente {#client-side-device-detection}

Esta seção descreve como usar a detecção do AEM no lado do cliente do dispositivo para otimizar a renderização da página ou fornecer ao cliente versões alternativas do site.

O AEM oferece suporte à detecção do lado do cliente do dispositivo com base em `BrowserMap`. `BrowserMap` é enviado no AEM como uma biblioteca do cliente em `/etc/clientlibs/browsermap`.

`BrowserMap` O fornece três estratégias que você pode usar para fornecer um site alternativo a um cliente, que são empregadas na seguinte ordem:

1. [Links alternativos](#providing-alternate-links)
1. [URL específico do grupo de dispositivos](#definingdevicegroupspecificurl)
1. [URL com base no seletor](#defining-selector-based-urls)

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca do cliente, leia a [Uso de bibliotecas de HTML do lado do cliente](/help/sites-developing/clientlibs.md) seção.

### Fornecer links alternativos {#providing-alternate-links}

A variável `PageVariantsProvider` O serviço OSGi é capaz de gerar links alternativos para sites pertencentes à mesma família. Para configurar sites que serão considerados pelo serviço, um `cq:siteVariant` O nó deve ser adicionado à `jcr:content` da raiz do site.

A variável `cq:siteVariant` precisa ter as seguintes propriedades:

* `cq:childNodesMapTo` - determina para qual atributo do elemento do link os nós filhos serão mapeados; é recomendável organizar o conteúdo do site de maneira que os filhos do nó raiz representem a raiz de uma variante de idioma do site global (por exemplo, `/content/mysite/en`, `/content/mysite/de`), caso em que o valor de `cq:childNodesMapTo` deve ser `hreflang`;
* `cq:variantDomain` - indica o que `Externalizer` o domínio será usado para gerar os URLs absolutos das variantes de página; se esse valor não for definido, as variantes de página serão geradas usando links relativos;
* `cq:variantFamily` - indica a qual família de sites este site pertence; várias representações específicas de dispositivos do mesmo site devem pertencer à mesma família;
* `media` - armazena os valores do atributo media do elemento link; é recomendável usar o nome do `BrowserMap` registrado `DeviceGroups`, para que o `BrowserMap` A biblioteca do pode encaminhar os clientes automaticamente para a variante correta do site.

#### PageVariantsProvider e Externalizador {#pagevariantsprovider-and-externalizer}

Quando o valor de `cq:variantDomain` propriedade de um `cq:siteVariant` não estiver vazio, a variável `PageVariantsProvider` serviço gerará links absolutos usando esse valor como um domínio configurado para o `Externalizer` serviço. Certifique-se de configurar o `Externalizer` serviço para refletir sua configuração.

>[!NOTE]
>
>Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Definindo um URL específico do Grupo de dispositivos {#defining-a-device-group-specific-url}

Se você não quiser usar links alternativos, poderá configurar um URL global para cada `DeviceGroup`. Recomendamos criar sua própria biblioteca do cliente que incorpore a `browsermap.standard` biblioteca cliente, mas redefine os grupos de dispositivos.

O BrowserMap é projetado de forma que as definições de Grupos de Dispositivos possam ser substituídas criando e adicionando um novo Grupo de Dispositivos com o mesmo nome à variável `BrowserMap` da sua biblioteca personalizada de clientes.

>[!NOTE]
>
>Para obter mais detalhes, leia o [Mapa de navegador personalizado](#creatingacustomisedbrowsermap) seção.

### Definição de URLs com base em seletor {#defining-selector-based-urls}

Se nenhum dos mecanismos anteriores tiver sido empregado para indicar um local alternativo para `BrowserMap`, em seguida, os seletores que usarão os nomes das `DeviceGroups` será adicionado à `URL`s, nesse caso, você deve fornecer seus próprios servlets que lidarão com as solicitações.

Por exemplo, uma navegação de dispositivo `www.example.com/index.html` identificado como `smartphone` por Mapa de navegador é encaminhado para `www.example.com/index.smartphone.html.`

### Utilização Do Mapa De Navegador Em Suas Páginas {#using-browsermap-on-your-pages}

Para usar a biblioteca padrão do cliente BrowserMap em uma página, é necessário incluir a variável `/libs/wcm/core/browsermap/browsermap.jsp` arquivo usando um `cq:include`tag na página `head` seção.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Além de adicionar o `BrowserMap` biblioteca do cliente no seu `JSP` arquivos, também é necessário adicionar um `cq:deviceIdentificationMode` Propriedade de string definida como `client-side` para o `jcr:content` abaixo da raiz do site.

### Substituição do comportamento padrão do BrowserMap {#overriding-browsermap-s-default-behaviour}

Se você quiser personalizar `BrowserMap` - substituindo o `DeviceGroups` ou adicionar mais testes - em seguida, você deve criar sua própria biblioteca do lado do cliente na qual incorpora o `browsermap.standard`biblioteca do lado do cliente.

Além disso, é necessário chamar manualmente a variável `BrowserMap.forwardRequest()` método no seu `JavaScript` código.

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca do cliente, leia a [Uso de bibliotecas de HTML do lado do cliente](/help/sites-developing/clientlibs.md) seção.

Depois de criar o seu personalizado `BrowserMap` biblioteca cliente, sugerimos a seguinte abordagem:

1. Criar um `browsermap.jsp` arquivo no seu aplicativo

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

1. Inclua o `broswermap.jsp` arquivo na seção head.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Excluir O Mapa De Navegador De Determinadas Páginas {#excluding-browsermap-from-certain-pages}

Se você quiser excluir a biblioteca do Mapa de navegador de algumas de suas páginas, onde não é necessária a detecção do cliente, poderá adicionar um atributo de solicitação:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

Isso tornará o `/libs/wcm/core/browsermap/browsermap.jsp` script para adicionar uma meta tag à página que tornará `BrowserMap` para não executar nenhuma detecção:

```xml
<meta name="browsermap.enabled" content="false">
```

### Testando uma Versão Específica de um Site {#testing-a-specific-version-of-a-web-site}

Normalmente, o script BrowserMap sempre redireciona os visitantes para a versão mais adequada do site, normalmente redirecionando visitantes para o desktop ou para o site móvel quando necessário.

Você pode forçar o dispositivo de qualquer solicitação para testar uma versão específica de um site adicionando o `device` para o URL. O URL a seguir renderizará a versão móvel do site do Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>A variável `wcmmode` parâmetro está definido como `disabled` para simular o comportamento de uma instância de publicação.

O valor do dispositivo substituído é armazenado em um cookie para que você possa navegar no site sem adicionar o `device` parâmetro para cada `URL`.

Como consequência, você precisa chamar o mesmo `URL` com o `device` definir como `browser` para voltar à versão para desktop do site.

>[!NOTE]
>
>BrowserMap armazena o valor de dispositivo substituído em um cookie chamado `BMAP_device`. A exclusão desse cookie garantirá que o CQ disponibilizará a versão apropriada do site de acordo com seu dispositivo atual (por exemplo, desktop ou dispositivo móvel).

## Processamento de solicitação móvel {#mobile-request-processing}

O AEM processa uma solicitação emitida por um dispositivo móvel que pertence ao grupo do dispositivo de toque da seguinte maneira:

1. Um iPad envia uma solicitação para a instância de publicação AEM, por exemplo. `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. O AEM determina se o site da página solicitada é um site móvel (verificando se a página de primeiro nível `/content/geometrixx_mobile` estende o componente página móvel). Em caso afirmativo:
1. O AEM pesquisa os recursos do dispositivo com base no usuário-agente no cabeçalho da solicitação.
1. O AEM mapeia os recursos do dispositivo para o grupo e define `touch` como o seletor de grupo de dispositivos.
1. O AEM redireciona a solicitação para `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. O AEM envia a resposta para a iPad:

   * `products.touch.html` é renderizado da maneira usual e pode ser armazenado em cache.
   * Os componentes de renderização usam seletores para adaptar a apresentação.
   * O AEM adiciona automaticamente o seletor de dispositivos móveis a todos os links internos na página.

### Estatísticas {#statistics}

Você pode obter algumas estatísticas sobre o número de solicitações feitas ao servidor AEM por dispositivos móveis. O número de solicitações pode ser detalhado:

* por grupo de dispositivos e dispositivo
* por ano, mês e dia

Para exibir as estatísticas:

1. Vá para a **Ferramentas** console.
1. Abra o **Estatísticas do dispositivo** página abaixo **Ferramentas** > **Dispositivo móvel**.
1. Clique no link para exibir as estatísticas de um ano, mês ou dia específico.

A variável **Estatísticas** tem a seguinte aparência:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>A variável **Estatísticas** é criada na primeira vez que um dispositivo móvel acessa o AEM e é detectado. Antes disso, não está disponível.

Se você precisar gerar uma entrada nas estatísticas, proceda da seguinte maneira:

1. Use um dispositivo móvel ou um emulador (como por exemplo https://chrispederick.com/work/user-agent-switcher/ no Firefox).
1. Solicite uma página móvel na instância do autor desativando o modo de criação, por exemplo:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

A variável **Estatísticas** agora está disponível.

### Cache de página de suporte para links &quot;enviar link para um amigo&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

As páginas móveis geralmente podem ser armazenadas em cache no Dispatcher, pois as páginas renderizadas para um grupo de dispositivos são diferenciadas no URL da página pelo seletor de grupo de dispositivos, por exemplo `/content/mobilepage.touch.html`. Uma solicitação para uma página móvel sem um seletor nunca é armazenada em cache, como neste caso, a detecção de dispositivo opera e finalmente redireciona para o grupo de dispositivos correspondente (ou &quot;nomatch&quot; para esse assunto). Uma página móvel renderizada com um seletor de grupo de dispositivos é processada pelo reescritor de links, que reescreve todos os links na página para também conter o seletor de grupo de dispositivos, impedindo a execução da detecção de dispositivos novamente para cada clique em uma página já qualificada.

Portanto, você pode encontrar o seguinte cenário:

A usuário Alice é redirecionada para `coolpage.feature.html`, e envia esse URL a um amigo Bob que o acessa com um cliente diferente que esteja no estado `touch` grupo de dispositivos.

Se `coolpage.feature.html` O é disponibilizado por um cache de front-end, o AEM não tem a chance de analisar a solicitação para descobrir que o seletor de dispositivos móveis não corresponde ao novo usuário-agente e Bob recebe a representação errada.

Para resolvê-lo, inclua uma interface de seleção simples nas páginas, em que os usuários finais possam substituir o grupo de dispositivos selecionado pelo AEM. No exemplo acima, um link (ou um ícone) na página permite que o usuário final alterne para `coolpage.touch.html` se ele acha que seu dispositivo é bom o suficiente para isso.
