---
title: Criação de sites para dispositivos móveis
seo-title: Criação de sites para dispositivos móveis
description: A criação de um site móvel é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes
seo-description: A criação de um site móvel é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes
uuid: 6b19042c-03f1-4e33-970e-475f9fb8c5fb
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: 0aabfb0a-ef9c-4b06-b698-61cad101c3c1
docset: aem65
legacypath: /content/docs/en/aem/6-0/develop/mobile/mobile
translation-type: tm+mt
source-git-commit: b3e1493811176271ead54bae55b1cd0cf759fe71
workflow-type: tm+mt
source-wordcount: '3864'
ht-degree: 0%

---


# Criação de sites para dispositivos móveis{#creating-sites-for-mobile-devices}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

A criação de um site móvel é semelhante à criação de um site padrão, pois também envolve a criação de modelos e componentes. Para obter mais detalhes sobre como criar modelos e componentes, consulte as seguintes páginas: [Modelos](/help/sites-developing/templates.md), [Componentes](/help/sites-developing/components.md) e [Introdução ao Desenvolvimento do AEM Sites](/help/sites-developing/getting-started.md). A principal diferença consiste em ativar as funcionalidades móveis incorporadas AEM no site. Isso é feito criando um modelo que depende do componente de página móvel.

Você também deve considerar o uso de [design responsivo](/help/sites-developing/responsive.md), criando um único site que acomoda vários tamanhos de tela.

Para começar, você pode consultar o **Site de demonstração do We.Retail Mobile** disponível no AEM.

Para criar um site móvel, proceda da seguinte forma:

1. Crie o componente de página:

   * Defina a propriedade `sling:resourceSuperType` como `wcm/mobile/components/page`
Dessa forma, o componente depende do componente de página móvel.

   * Crie `body.jsp` com a lógica específica do projeto.

1. Crie o modelo de página:

   * Defina a propriedade `sling:resourceType` como o componente de página recém-criado.
   * Defina a propriedade `allowedPaths`.

1. Crie a página de design para o site.
1. Crie a página raiz do site abaixo do nó `/content`:

   * Defina a propriedade `cq:allowedTemplates`.
   * Defina a propriedade `cq:designPath`.

1. Nas propriedades da página raiz do site, defina os grupos de dispositivos na guia **Mobile**.
1. Crie as páginas do site usando o novo modelo.

O componente de página móvel ( `/libs/wcm/mobile/components/page`):

* Adiciona a guia **Mobile** à caixa de diálogo de propriedades da página.
* Por meio de `head.jsp`, recupera o grupo de dispositivos móveis atual da solicitação e, se um grupo de dispositivos for encontrado, usa o método `drawHead()` do grupo para incluir o componente de inicialização do emulador associado do grupo de dispositivos (somente no modo de autor) e o CSS de renderização do grupo de dispositivos.

>[!NOTE]
>
>A página raiz do site móvel precisa estar no nível 1 da hierarquia do nó e é recomendável estar abaixo do nó /content.

## Criação de um site móvel com o Multi Site Manager {#creating-a-mobile-site-with-the-multi-site-manager}

Use o Multi Site Manager (MSM) para criar uma live copy móvel de um site padrão. O site padrão é automaticamente transformado em um site móvel: o site móvel tem todos os recursos dos sites móveis (por exemplo, edição dentro de um emulador) e pode ser gerenciado em sincronia com o site padrão. Consulte a seção [Criação de uma Live Copy para Canais diferentes](/help/sites-administering/msm.md) na página do Multi Site Manager.

## API móvel do lado do servidor {#server-side-mobile-api}

Os pacotes Java que contêm as classes móveis são:

* [com.day.cq.wcm.mobile.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html)  - define MobileConstants.
* [com.day.cq.wcm.mobile.api.device](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/package-summary.html) - define Device, DeviceGroup e DeviceGroupList.
* [com.day.cq.wcm.mobile.api.device.feature](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/api/device/capability/package-summary.html) - define DeviceCapability.
* [com.day.cq.wcm.mobile.api.wurfl](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/workflow/api/package-summary.html) - define WurflQueryEngine.
* [com.day.cq.wcm.mobile.core](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/mobile/core/package-summary.html) - define o MobileUtil, que fornece vários métodos de utilitários girando em torno do WCM Mobile.

### Componentes móveis {#mobile-components}

O **Site de demonstração do We.Retail Mobile** usa os seguintes componentes móveis localizados abaixo de `/libs/foundation/components`:

<table>
 <tbody>
  <tr>
   <td>Nome</td>
   <td>Grupo</td>
   <td>Características</td>
  </tr>
  <tr>
   <td>mobilefoter</td>
   <td>oculto</td>
   <td>- rodapé</td>
  </tr>
  <tr>
   <td>mobileimage</td>
   <td>Móvel</td>
   <td>- com base no componente de base de imagem<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilizista</td>
   <td>Móvel</td>
   <td>- com base no componente de fundação de lista<br /> - listitem_teaser.jsp renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilelogo</td>
   <td>oculto</td>
   <td>- com base no componente de base do logotipo<br /> - renderiza uma imagem se o dispositivo for capaz<br /> </td>
  </tr>
  <tr>
   <td>mobilereference</td>
   <td>Móvel</td>
   <td><p>- semelhante ao componente de alicerce de referência</p> <p>- mapeia um componente de texttimage para um mobiletextimage um e um componente de imagem para um mobileimage one</p> </td>
  </tr>
  <tr>
   <td>mobiletextimage</td>
   <td>Móvel</td>
   <td>- com base no componente de fundação da textimage<br /> - renderiza uma imagem se o dispositivo for capaz de</td>
  </tr>
  <tr>
   <td>mobiletopnav</td>
   <td>oculto</td>
   <td><p>- com base na componente da fundação de topnav</p> <p>- somente renderiza o texto</p> </td>
  </tr>
 </tbody>
</table>

#### Criação de um componente móvel {#creating-a-mobile-component}

A estrutura móvel AEM permite desenvolver componentes sensíveis ao dispositivo que emite a solicitação. Os exemplos de código a seguir mostram como usar a API móvel AEM em um componente jsp e, em particular, como:

* Obtenha o dispositivo da solicitação:
   `Device device = slingRequest.adaptTo(Device.class);`

* Obtenha o grupo de dispositivos:
   `DeviceGroup deviceGroup = device.getDeviceGroup();`

* Obtenha os recursos do grupo de dispositivos:
   `Collection<DeviceCapability> capabilities = deviceGroup.getCapabilities();`

* Obtenha os atributos do dispositivo (chave/valores do recurso bruto do banco de dados WURFL):
   `Map<String,String> deviceAttributes = device.getAttributes();`

* Obtenha o agente do usuário do dispositivo:
   `String userAgent = device.getUserAgent();`

* Obtenha a lista do grupo de dispositivos (grupos de dispositivos atribuídos ao site pelo autor) da página atual:
   `DeviceGroupList deviceGroupList = currentPage.adaptTo(DeviceGroupList.class);`

* Verifique se o grupo de dispositivos suporta imagens
   `if (deviceGroup.hasCapability(DeviceCapability.CAPABILITY_IMAGES)) {`
...
OU

...   `if MobileUtil.hasCapability(request, DeviceCapability.CAPABILITY_IMAGES) {`
...

>[!NOTE]
>
>Em um jsp, `slingRequest` está disponível por meio da tag `<sling:defineObjects>` e `currentPage` pela tag `<cq:defineObjects>`.

### Emuladores {#emulators}

A criação baseada no emulador fornece aos autores os meios de criar páginas de conteúdo destinadas a clientes móveis. A criação de conteúdo móvel segue o mesmo princípio da edição WYSIWYG no local. Para que os autores percebam a aparência da página em um dispositivo móvel, uma página de conteúdo móvel é editada usando um emulador de dispositivo.

Os emuladores de dispositivos móveis são baseados na estrutura de emulador genérica. Para obter mais detalhes, consulte a página [Emuladores](/help/sites-developing/emulators.md).

O emulador do dispositivo exibe o dispositivo móvel na página, enquanto a edição habitual (parsys, componentes) ocorre na tela do dispositivo. O emulador do dispositivo depende dos grupos de dispositivos configurados para o site. Vários emuladores podem ser atribuídos a um grupo de dispositivos. Todos os emuladores ficam disponíveis na página de conteúdo. Por padrão, o primeiro emulador atribuído ao primeiro grupo de dispositivos atribuído ao site é exibido. Os emuladores podem ser comutados pelo carrossel do emulador na parte superior da página ou pelo botão de edição do Sidekick.

**Criação de um emulador**

Para criar um emulador, consulte a seção [Criação de um emulador móvel personalizado](/help/sites-developing/emulators.md) na página Emuladores genéricos.

**Principais características dos emuladores móveis**

* Um grupo de dispositivos é composto por um de mais emuladores: a página de configuração do grupo de dispositivos, por exemplo, /etc/mobile/groups/touch, contém a propriedade `emulators` abaixo do nó `jcr:content`.
Observação: embora seja possível que o mesmo emulador pertença a vários grupos de dispositivos, não faz muito sentido.

* Pela caixa de diálogo de configuração do grupo de dispositivos, a propriedade `emulators` é definida com o caminho dos emuladores desejados. Por exemplo: `/libs/wcm/mobile/components/emulators/iPhone4`.

* Os componentes do emulador (por exemplo, `/libs/wcm/mobile/components/emulators/iPhone4`) estende o componente emulador móvel básico ( `/libs/wcm/mobile/components/emulators/base`).

* Cada componente que estende o emulador móvel básico está disponível para seleção ao configurar um grupo de dispositivos. Os emuladores personalizados podem ser facilmente criados ou estendidos.
* No momento da solicitação no modo de edição, a implementação do emulador é usada para renderizar a página.
* Quando o modelo da página depende do componente de página móvel, as funcionalidades do emulador são automaticamente integradas na página (por meio de `head.jsp` do componente de página móvel).

### Grupos de dispositivos {#device-groups}

Os grupos de dispositivos móveis fornecem segmentação de dispositivos móveis com base nos recursos do dispositivo. Um grupo de dispositivos fornece as informações necessárias para a criação baseada em emulador na instância do autor e para a renderização correta do conteúdo na instância de publicação: depois que os autores adicionarem conteúdo à página móvel e a tiverem publicado, a página poderá ser solicitada na instância de publicação. Ali, em vez da visualização de edição do emulador, a página de conteúdo é renderizada usando um dos grupos de dispositivos configurados. A seleção do grupo de dispositivos ocorre com base em [detecção de dispositivos móveis](#devicedetection). O grupo de dispositivos correspondente fornece as informações de estilo necessárias.

Os grupos de dispositivos são definidos como páginas de conteúdo abaixo de `/etc/mobile/devices` e usam o modelo **Mobile Device Group**. O modelo de grupo de dispositivos serve como um modelo de configuração para definições de grupos de dispositivos na forma de páginas de conteúdo. As suas principais características são:

* Local: `/libs/wcm/mobile/templates/devicegroup`
* Caminho Permitido: `/etc/mobile/groups/*`
* Componente da página: `wcm/mobile/components/devicegroup`

#### Atribuindo grupos de dispositivos ao seu site {#assigning-device-groups-to-your-site}

Ao criar um site móvel, é necessário atribuir grupos de dispositivos ao site. AEM fornece três grupos de dispositivos, dependendo das capacidades de renderização de HTML e JavaScript do dispositivo:

* **** Featurephones, para dispositivos de recursos como o Sony Ericsson W800 com suporte para HTML básico, mas sem suporte para imagens e JavaScript.
* **** Smartphones, para dispositivos como o Blackberry com suporte para HTML e imagens básicas, mas sem suporte para JavaScript.

* **** Touchphones, para dispositivos como o iPad com suporte total para HTML, imagens, JavaScript e rotação de dispositivos.

Como os emuladores podem ser associados a um grupo de dispositivos (consulte a seção [Criação de um grupo de dispositivos](#creating-a-device-group)), atribuir um grupo de dispositivos a um site permite que os autores selecionem entre os emuladores associados ao grupo de dispositivos para editar a página.

Para atribuir um grupo de dispositivos ao site:

1. No seu navegador, vá para o console **Siteadmin**.
1. Abra a página raiz do site móvel abaixo de **Sites**.
1. Abra as propriedades da página.
1. Selecione a guia **Móvel**:

   * Defina os grupos de dispositivos.
   * Clique em **OK**.

>[!NOTE]
>
>Quando os grupos de dispositivos tiverem sido definidos para um site, eles serão herdados por todas as páginas do site.

#### Filtros do grupo de dispositivos {#device-group-filters}

Os filtros de grupos de dispositivos definem critérios baseados em recursos para determinar se um dispositivo pertence ao grupo. Ao criar um grupo de dispositivos, você pode selecionar os filtros a serem usados para avaliar dispositivos.

Em tempo de execução quando AEM receber uma solicitação HTTP de um dispositivo, cada filtro associado a um grupo compara os recursos do dispositivo com critérios específicos. Considera-se que o dispositivo pertence ao grupo quando tem todos os recursos necessários para os filtros. Os recursos são recuperados do banco de dados WURFL™.

Os grupos de dispositivos podem usar zero ou mais filtros para detecção de capacidade. Além disso, um filtro pode ser usado com vários grupos de dispositivos. AEM fornece um filtro padrão que determina se o dispositivo tem os recursos selecionados para um grupo:

* CSS
* Imagens JPG e PNG
* JavaScript
* Rotação do dispositivo

Se o grupo de dispositivos não usar um filtro, os recursos selecionados que estão configurados para o grupo são os únicos recursos que um dispositivo requer.

Para obter mais informações, consulte [Criando Filtros de Grupo de Dispositivos](/help/sites-developing/groupfilters.md).

#### Criando um grupo de dispositivos {#creating-a-device-group}

Crie um grupo de dispositivos quando os grupos que AEM instalados não atenderem aos seus requisitos.

1. No seu navegador, vá para o console **Ferramentas**.
1. Crie uma nova página abaixo de **Ferramentas** > **Dispositivo Móvel** > **Grupos de Dispositivos**. Na caixa de diálogo **Criar página**:

   * Como **Título**, digite `Special Phones`.

   * Como **Nome** digite `special`.

   * Selecione **Modelo de Grupo de Dispositivos Móveis**.
   * Clique em **Criar**.

1. No CRXDE, adicione um arquivo **static.css** contendo os estilos para o grupo de dispositivos abaixo do nó `/etc/mobile/groups/special`.

1. Abra a página **Telefones especiais**.
1. Para configurar o grupo de dispositivos, clique no botão **Editar** ao lado de **Definições**.
Na guia **Geral**:

   * **Título**: o nome do grupo de dispositivos móveis.
   * **Descrição**: descrição do grupo.
   * **Agente** do usuário: sequência user-agent em que os dispositivos são combinados. É opcional e pode ser um regex. Exemplo: `BlackBerryZ10`
   * **Recursos**: define se o grupo pode lidar com imagens, CSS, JavaScript ou rotação de dispositivos.
   * **Largura****e altura mínimas da tela**
   * **Desativar Emulador**: para ativar/desativar o emulador durante a edição de conteúdo.

   Na guia **Emuladores**:

   * **Emuladores**: selecione os emuladores atribuídos a este grupo de dispositivos.

   Na guia **Filtros**:

   * Para adicionar um filtro, clique em Adicionar item e selecione um filtro na lista suspensa.
   * Os filtros são avaliados na ordem em que são exibidos. Quando um dispositivo não atende aos critérios de um filtro, os filtros subsequentes na lista não são avaliados.



1. Clique em OK.

A caixa de diálogo de configuração de grupo de dispositivos móveis é exibida da seguinte maneira:

![screen_shot_2012-02-01at22043pm](assets/screen_shot_2012-02-01at22043pm.png)

#### CSS personalizado por grupo de dispositivos {#custom-css-per-device-group}

Conforme descrito anteriormente, é possível associar um CSS personalizado a uma página de grupo de dispositivos, como o CSS de uma página de design. Esse CSS é usado para influenciar a renderização específica do grupo de dispositivos do conteúdo da página no autor e na publicação. Esse CSS é incluído automaticamente:

* Na página da instância do autor para cada emulador usado por esse grupo de dispositivos.
* Na página da instância de publicação, se o agente do usuário da solicitação corresponder a um dispositivo móvel nesse grupo de dispositivos específico.

## Detecção de dispositivo do lado do servidor {#server-side-device-detection}

Use filtros e uma biblioteca de especificações de dispositivos para determinar os recursos do dispositivo que executa a solicitação HTTP.

### Filtros do grupo de dispositivos de revelação {#develop-device-group-filters}

Crie um filtro de grupo de dispositivos para definir um conjunto de requisitos de capacidade do dispositivo. Crie quantos filtros forem necessários para público alvo dos grupos necessários de recursos do dispositivo.

Projete seus filtros para que você possa usar combinações deles para definir os grupos de recursos. Normalmente, há sobreposição dos recursos de diferentes grupos de dispositivos. Portanto, você pode usar alguns filtros com várias definições de grupos de dispositivos.

Depois de criar um filtro, você pode usá-lo na configuração do grupo.

Para obter informações, acesse [Criando Filtros de Grupo de Dispositivos](/help/sites-developing/groupfilters.md).

### Usando o banco de dados WURFL™ {#using-the-wurfl-database}

AEM usa uma versão truncada do banco de dados [WURFL](https://wurfl.sourceforge.net/)™ para query de recursos do dispositivo, como resolução de tela ou suporte a javascript, com base no User-Agent do dispositivo.

O código XML do banco de dados WURFL™ é representado como nós abaixo `/var/mobile/devicespecs` analisando o arquivo `wurfl.xml`em `/libs/wcm/mobile/devicespecs/wurfl.xml.` A expansão para nós ocorre na primeira vez que o pacote `cq-mobile-core` é iniciado.

Os recursos do dispositivo são armazenados como propriedades do nó, e os nós representam modelos do dispositivo. Você pode usar query para recuperar os recursos de um dispositivo ou agente do usuário.

Como o banco de dados WURFL™ está evoluindo, talvez seja necessário personalizá-lo ou substituí-lo. Para atualizar o banco de dados de dispositivos móveis, você tem as seguintes opções:

* Substitua o arquivo pela versão mais recente, se você tiver uma licença que permita esse uso. Consulte Instalação de um banco de dados WURFL diferente.
* Use a versão que está disponível no AEM e configure um regexp que corresponda às suas sequências de caracteres User-Agent e aponte para um dispositivo WURFL™ existente. Consulte [Adicionando um agente-usuário baseado em regexp Correspondente](#adding-a-regexp-based-user-agent-matching).

#### Testando o mapeamento de um agente do usuário para recursos WURFL™ {#testing-the-mapping-of-a-user-agent-to-wurfl-capabilities}

Quando um dispositivo acessa seu site móvel, AEM detecta o dispositivo, mapeia-o para um grupo de dispositivos de acordo com seus recursos e envia uma visualização da página que corresponde ao grupo de dispositivos. O grupo de dispositivos correspondente fornece as informações de estilo necessárias. Os mapeamentos podem ser testados na Página de teste do agente do usuário móvel:

`https://localhost:4502/etc/mobile/useragent-test.html`

#### Instalando um banco de dados WURFL™ diferente {#installing-a-different-wurfl-database}

O banco de dados WURFL™ truncado instalado com AEM é uma versão que pré-atualiza
30 de agosto de 2011. Se sua versão do WURFL foi lançada após 30 de agosto de 2011, verifique se seu uso está em conformidade com sua licença.

Para instalar um banco de dados WURFL™:

1. No CRXDE Lite, crie a seguinte pasta: `/apps/wcm/mobile/devicespecs`
1. Copie o arquivo WURFL™ para a pasta.
1. Renomeie o arquivo como `wurfl.xml`.

AEM analisa automaticamente o arquivo `wurfl.xml` e atualiza os nós abaixo de `/var/mobile/devicespecs`.

>[!NOTE]
>
>Quando o banco de dados WURFL™ completo estiver ativado, a análise e a ativação podem levar alguns minutos. Você pode observar os registros para obter informações sobre o progresso.

#### Adicionando uma correspondência User-Agent baseada em regexp {#adding-a-regexp-based-user-agent-matching}

Adicione um agente de usuário como uma expressão regular abaixo de /apps/wcm/mobile/devicespecs/wurfl/regexp para apontar para um tipo de dispositivo WURFL™ existente.

1. Em **CRXDE Lite**, crie um nó abaixo de /apps/wcm/mobile/devicespecs/regexp, por exemplo, apple_ipad_ver1.
1. Adicione as seguintes propriedades ao nó:

   * **regexp**: expressão regular definindo agentes de usuário, por exemplo: .*Mozilla.*iPad.*AppleWebKit.*Safari.*
   * **deviceId**: a ID do dispositivo, conforme definido em wurfl.xml, por exemplo: apple_ipad_ver1

A configuração acima faz com que os dispositivos para os quais o User-Agent corresponde a expressão regular fornecida sejam mapeados para a ID do dispositivo apple_ipad_ver1 WURFL™, se ela existir.

## Detecção de dispositivo do lado do cliente {#client-side-device-detection}

Esta seção descreve como usar a detecção de AEM do lado do cliente do dispositivo para otimizar a renderização da página ou fornecer ao cliente versões alternativas do site.

AEM suporta a detecção do lado do cliente do dispositivo com base em `BrowserMap`. `BrowserMap` é enviado em AEM como uma biblioteca cliente em  `/etc/clientlibs/browsermap`.

`BrowserMap` fornece três estratégias que podem ser usadas para fornecer um site alternativo a um cliente, que são empregadas na seguinte ordem:

1. [Links alternativos](#providing-alternate-links)
1. [URL Específico do Grupo de Dispositivos](#definingdevicegroupspecificurl)
1. [URL baseado em seletor](#defining-selector-based-urls)

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca do cliente, leia a seção [Usando bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md).

### Fornecimento de links alternativos {#providing-alternate-links}

O serviço `PageVariantsProvider` OSGi é capaz de gerar links alternativos para sites pertencentes à mesma família. Para configurar sites a serem considerados pelo serviço, um nó `cq:siteVariant` deve ser adicionado ao nó `jcr:content` da raiz do site.

O nó `cq:siteVariant` precisa ter as seguintes propriedades:

* `cq:childNodesMapTo` - determina a que atributo do elemento de ligação os nós subordinados serão mapeados; é recomendável organizar o conteúdo do site de tal forma que os filhos do nó raiz representem a raiz de uma variante de idioma do site global (por exemplo,  `/content/mysite/en`,  `/content/mysite/de`), caso em que o valor do  `cq:childNodesMapTo` deve ser  `hreflang`;
* `cq:variantDomain` - indica que  `Externalizer` domínio será usado para gerar as variáveis de página URLs absolutas; se esse valor não for definido, as variantes de página serão geradas usando links relativos;
* `cq:variantFamily` - indica a que família de sítios web pertence este sítio; As representações múltiplas específicas do mesmo sítio web devem pertencer à mesma família;
* `media` - armazena os valores do atributo media do elemento link; é recomendável usar o nome do  `BrowserMap` registrado  `DeviceGroups`, para que a  `BrowserMap` biblioteca possa encaminhar automaticamente os clientes para a variante correta do site.

#### PageVariantsProvider e Externalizer {#pagevariantsprovider-and-externalizer}

Quando o valor da propriedade `cq:variantDomain` de um nó `cq:siteVariant` não estiver vazio, o serviço `PageVariantsProvider` gerará links absolutos usando esse valor como um domínio configurado para o serviço `Externalizer`. Certifique-se de configurar o serviço `Externalizer` para refletir sua configuração.

>[!NOTE]
>
>Ao trabalhar com AEM existem vários métodos de gestão das definições de configuração para esses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

### Definindo um URL Específico do Grupo de Dispositivos {#defining-a-device-group-specific-url}

Se não quiser usar links alternativos, configure um URL global para cada `DeviceGroup`. Recomendamos a criação de sua própria biblioteca de cliente que incorpora a biblioteca `browsermap.standard` de cliente, mas redefine os grupos de dispositivos.

O BrowserMap foi projetado de modo que as definições de Grupos de dispositivos possam ser substituídas criando e adicionando um novo Grupo de dispositivos com o mesmo nome ao objeto `BrowserMap` da biblioteca de cliente personalizada.

>[!NOTE]
>
>Para obter mais detalhes, leia a seção [MapaNavegador Personalizado](#creatingacustomisedbrowsermap).

### Definindo URLs com base em seletor {#defining-selector-based-urls}

Se nenhum dos mecanismos anteriores tiver sido empregado para indicar um site alternativo para `BrowserMap`, os seletores que usarão os nomes de `DeviceGroups` serão adicionados aos `URL`s, caso em que você deverá fornecer seus próprios servlets que lidarão com as solicitações.

Por exemplo, um dispositivo que navega `www.example.com/index.html` identificado como `smartphone` por BrowserMap é encaminhado para `www.example.com/index.smartphone.html.`

### Usando o BrowserMap em suas páginas {#using-browsermap-on-your-pages}

Para usar a biblioteca de cliente padrão do BrowserMap em uma página, é necessário incluir o arquivo `/libs/wcm/core/browsermap/browsermap.jsp` usando uma tag `cq:include`na seção `head` da página.

```xml
<cq:include script="/libs/wcm/core/browsermap/browsermap.jsp" />
```

Além de adicionar a biblioteca do cliente `BrowserMap` nos arquivos `JSP`, também é necessário adicionar uma propriedade `cq:deviceIdentificationMode` String definida como `client-side` ao nó `jcr:content` abaixo da raiz do site.

### Substituição do comportamento padrão do BrowserMap {#overriding-browsermap-s-default-behaviour}

Se você deseja personalizar `BrowserMap` - substituindo `DeviceGroups` ou adicionando mais testes -, você deve criar sua própria biblioteca do lado do cliente na qual você incorpora a `browsermap.standard`biblioteca do lado do cliente.

Além disso, é necessário chamar manualmente o método `BrowserMap.forwardRequest()` no código `JavaScript`.

>[!NOTE]
>
>Para obter mais informações sobre a integração da Biblioteca do cliente, leia a seção [Usando bibliotecas HTML do lado do cliente](/help/sites-developing/clientlibs.md).

Depois de criar sua biblioteca de clientes personalizada `BrowserMap`, sugerimos a seguinte abordagem:

1. Crie um arquivo `browsermap.jsp` em seu aplicativo

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

1. Inclua o arquivo `broswermap.jsp` na seção de cabeçalho.

   ```xml
   <cq:include script="browsermap.jsp" />
   ```

### Excluindo o BrowserMap de determinadas páginas {#excluding-browsermap-from-certain-pages}

Se você deseja excluir a biblioteca do BrowserMap de algumas de suas páginas em que não é necessário detectar o cliente, é possível adicionar um atributo de solicitação:

```xml
<%
request.setAttribute("browsermap.enabled", false);
%>
```

Isso fará com que o script `/libs/wcm/core/browsermap/browsermap.jsp` adicione uma tag meta à página que fará com que `BrowserMap` não execute nenhuma detecção:

```xml
<meta name="browsermap.enabled" content="false">
```

### Testando uma versão específica de um site {#testing-a-specific-version-of-a-web-site}

Normalmente, o script BrowserMap sempre redireciona os visitantes para a versão mais adequada do site, geralmente redirecionando visitantes para a área de trabalho ou para o site móvel quando necessário.

Você pode forçar o dispositivo de qualquer solicitação a testar uma versão específica de um site adicionando o parâmetro `device` ao seu URL. O URL a seguir renderizará a versão móvel do site do Geometrixx Outdoors.

`https://localhost:4502/content/geometrixx-outdoors/en.html?wcmmode=disabled&device=smartphone`

>[!NOTE]
>
>O parâmetro `wcmmode` está definido como `disabled` para simular o comportamento de uma instância de publicação.

O valor do dispositivo substituído é armazenado em um cookie para que você possa navegar em seu site sem adicionar o parâmetro `device` a cada `URL`.

Como consequência, você precisa chamar o mesmo `URL` com o `device` definido como `browser` para voltar à versão para desktop do site.

>[!NOTE]
>
>O BrowserMap armazena o valor do dispositivo substituído em um cookie chamado `BMAP_device`. A exclusão desse cookie garantirá que o CQ disponibilizará a versão apropriada do site de acordo com o dispositivo atual (por exemplo, desktop ou dispositivo móvel).

## Processamento de solicitação móvel {#mobile-request-processing}

AEM processa uma solicitação emitida por um dispositivo móvel que pertence ao grupo de dispositivos de toque da seguinte forma:

1. Um iPad envia uma solicitação para a instância de publicação AEM, por exemplo, `https://localhost:4503/content/geometrixx_mobile/en/products.html`
1. AEM determina se o site da página solicitada é um site móvel (verificando se a página de primeiro nível `/content/geometrixx_mobile` estende o componente de página móvel). Em caso afirmativo:
1. AEM procura os recursos do dispositivo com base no User-Agent no cabeçalho da solicitação.
1. AEM mapeia os recursos do dispositivo para o grupo de dispositivos e define `touch` como o seletor de grupo de dispositivos.
1. AEM redireciona a solicitação para `https://localhost:4503/content/geometrixx_mobile/en/products.touch.html.`
1. AEM envia a resposta para o iPad:

   * `products.touch.html` é renderizado da maneira habitual e é cátil.
   * Os componentes de renderização usam seletores para adaptar a apresentação.
   * AEM adiciona automaticamente o seletor móvel a todos os links internos na página.

### Estatísticas {#statistics}

Você pode obter algumas estatísticas sobre o número de solicitações feitas ao servidor AEM por dispositivos móveis. O número de solicitações pode ser detalhado:

* por grupo de dispositivos e dispositivo
* por ano, mês e dia

Para visualização das estatísticas:

1. Vá para o console **Ferramentas**.
1. Abra a página **Estatísticas do dispositivo** abaixo de **Ferramentas** > **Dispositivo móvel**.
1. Clique no link para visualização das estatísticas de um ano, mês ou dia específico.

A página **Estatísticas** tem a seguinte aparência:

![screen_shot_2012-02-01at24353pm](assets/screen_shot_2012-02-01at24353pm.png)

>[!NOTE]
>
>A página **Statistics** é criada na primeira vez que um dispositivo móvel acessa AEM e é detectado. Antes disso, não está disponível.

Se precisar gerar uma entrada nas estatísticas, você pode continuar da seguinte maneira:

1. Use um dispositivo móvel ou um emulador (por exemplo, https://chrispederick.com/work/user-agent-switcher/ no Firefox).
1. Solicite uma página móvel na instância do autor desativando o modo de criação, por exemplo:
   `https://localhost:4502/content/geometrixx_mobile/en/products.html?wcmmode=disabled`

A página **Estatísticas** agora está disponível.

### Suporte ao cache de páginas para links &quot;enviar link para um amigo&quot; {#supporting-page-caching-for-send-link-to-a-friend-links}

Geralmente, as páginas móveis podem ser armazenadas em cache no Dispatcher, pois as páginas renderizadas para um grupo de dispositivos são diferenciadas no URL da página pelo seletor de grupo de dispositivos, por exemplo `/content/mobilepage.touch.html`. Uma solicitação para uma página móvel sem um seletor nunca é armazenada em cache, como neste caso, a detecção do dispositivo opera e, por fim, redireciona para o grupo de dispositivos correspondente (ou &quot;nomatch&quot;, nesse caso). Uma página móvel renderizada com um seletor de grupo de dispositivos é processada pela regravadora de links, que regrava todos os links dentro da página para também conter o seletor de grupo de dispositivos, impedindo a repetição da detecção de dispositivos para cada clique em uma página já qualificada.

Portanto, você pode encontrar o seguinte cenário:

O usuário Alice é redirecionado para `coolpage.feature.html` e envia esse URL para um amigo Bob que o acessa com um cliente diferente que se enquadra no grupo de dispositivos `touch`.

Se `coolpage.feature.html` for servido a partir de um cache front-end, AEM não terá a oportunidade de analisar a solicitação para descobrir que o seletor móvel não corresponde ao novo User-Agent, e Bob obtém a representação errada.

Para resolvê-la, você pode incluir uma interface de usuário de seleção simples nas páginas, onde os usuários finais podem substituir o grupo de dispositivos selecionado pela AEM. No exemplo acima, um link (ou um ícone) na página permite que o usuário final alterne para `coolpage.touch.html` se ele achar que seu dispositivo é bom o suficiente para isso.
