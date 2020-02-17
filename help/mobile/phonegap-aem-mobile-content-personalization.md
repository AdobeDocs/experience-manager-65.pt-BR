---
title: Personalização de conteúdo do AEM Mobile
seo-title: Personalização de conteúdo do AEM Mobile
description: Siga esta página para saber mais sobre o recurso de personalização de conteúdo do AEM Mobile que permite que autores do AEM personalizem conteúdo de aplicativos móveis aproveitando o Adobe Target.
seo-description: Siga esta página para saber mais sobre o recurso de personalização de conteúdo do AEM Mobile que permite que autores do AEM personalizem conteúdo de aplicativos móveis aproveitando o Adobe Target.
uuid: 9078edd1-8399-485f-8a63-a07e766f7ef9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c9c818dc-c5c4-4a96-94fe-9dc9fe75705b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personalização de conteúdo do AEM Mobile{#aem-mobile-content-personalization}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte do Guia de [introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md) , um ponto de partida recomendado para referência ao AEM Mobile.

O recurso de personalização de conteúdo do AEM Mobile permite que os autores [do](#author) AEM personalizem o conteúdo do aplicativo móvel ao utilizar o [Adobe Target](https://www.adobe.com/ca/marketing-cloud/testing-targeting.html). Isso permite a entrega de ofertas direcionadas para usuários de aplicativos móveis. O Adobe Experience Manager Mobile oferece a capacidade de criar, direcionar e fornecer conteúdo que fornecerá ao usuário conteúdo específico para seus próprios gostos individuais.

Como acontece frequentemente no AEM, para que os autores comecem a criar esse conteúdo, os administradores e desenvolvedores precisam primeiro preparar o ambiente.

[Os administradores](#administrator) do AEM precisam estabelecer uma conexão entre o AEM Mobile e o serviço da Adobe Target Cloud.

Enquanto isso, [os desenvolvedores](#developer) do AEM Mobile precisam modificar seus scripts existentes para facilitar a criação de conteúdo direcionado.

## Para administradores {#for-administrators}

Há várias etapas que precisam ser reunidas antes que os autores de conteúdo possam começar a gerar conteúdo direcionado para aplicativos móveis: Obtenha o conjunto correto de permissões para usuários e grupos, criando serviços em nuvem, configurando o aplicativo para a atividade e, por fim, gerando o conteúdo.

Este artigo o guiará pelo processo usado para configurar o aplicativo [de referência híbrido do](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile para definição de metas.

A presunção a partir de agora é que o aplicativo de referência híbrido do AEM Mobile foi implantado e acessível com êxito por meio do AEM Mobile Dashboard.

Antes que os autores possam gerar conteúdo direcionado dentro de um aplicativo, sua instância do AEM precisa ser [configurada com o serviço da Adobe Target Cloud.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Permissões {#permissions}

Os usuários que precisam acessar o console de personalização precisam fazer parte do `target-activity-authors` grupo.

Sugere-se que, como parte da configuração de usuários e grupos, o grupo de atividades-alvo seja adicionado ao grupo de administradores de aplicativos. Ao adicionar o grupo de autores-atividade-alvo, isso permitirá que os usuários possam ver a entrada do menu de navegação Personalização.

>[!NOTE]
>
>Esquecer de adicionar os usuários ou grupos aos quais você deseja ter acesso ao console de administração de personalização ao grupo de autores-atividade-alvo impedirá que os usuários vejam o console de personalização.

### Serviços em nuvem {#cloud-services}

Para obter conteúdo direcionado trabalhando para aplicativos móveis, há dois serviços que precisam ser configurados: O Adobe Target Service e o serviço Adobe Mobile Services. O Adobe Target Service fornece o mecanismo para processar solicitações de clientes e retornar o conteúdo personalizado. O serviço Adobe Mobile Services fornece a conexão entre os serviços da Adobe e o aplicativo móvel por meio do arquivo ADBMobileConfig.json, que é consumido pelo plug-in do Cordova do AMS. No AEM Mobile Dashboard, é possível configurar seu aplicativo adicionando os dois serviços.

No AEM Mobile Dashboard, localize os Serviços de gerenciamento em nuvem e clique no botão +.

![chlimage_1-38](assets/chlimage_1-38.png)

No assistente para Adicionar serviço em nuvem, selecione o cartão de serviço em nuvem &quot;Adobe Target&quot; e clique em Avançar.

![chlimage_1-39](assets/chlimage_1-39.png)

Na lista suspensa Selecionar uma configuração, é possível criar uma nova configuração ou selecionar uma configuração existente. Para criar uma nova configuração, selecione &quot;Criar configuração&quot; na lista suspensa. Insira um título para a configuração do Target. Insira o código do cliente, o email e a senha associados à sua conta do Target. Se você não souber os valores desses campos, entre em contato com o suporte do Adobe Target. Clique no botão &quot;Verificar&quot; para validar as credenciais. Depois de verificado, clique no botão Enviar para criar o serviço de nuvem.

>[!NOTE]
>
>O serviço de nuvem que é criado é automaticamente associado ao aplicativo móvel por meio do assistente. O valor da propriedade cq:cloudserviceconfigs é definido no nó jcr:content do nó de grupo de aplicativos. Para a amostra de aplicativo híbrido, ela é definida em /content/mobileapps/híbridos-reference-app/jcr:content com o valor apontando para o nó de estrutura gerado automaticamente localizado em /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. O nó da estrutura tem duas propriedades definidas por padrão, gênero e idade. A estrutura é usada apenas pela visualização do AEM e não tem nenhum impacto no dispositivo.

Após a conclusão do assistente, o bloco Gerenciar serviço em nuvem conterá o serviço em nuvem do Target, no entanto, ele contém um aviso sobre a falta de uma conta do Adobe Mobile Service.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

É necessário vincular uma conta do Adobe Mobile Services (AMS) ao aplicativo também, o serviço AMS fornece o arquivo ADBMobileConfig.json necessário que contém as informações do código do cliente do Target. Antes de criar uma associação com a conta AMS, a conta AMS precisa ser modificada por um usuário que tenha permissões para o AMS.

### Código do cliente {#client-code}

Para fazer logon nos serviços AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), selecione o aplicativo móvel e clique nas configurações. Localize o campo Opções do Target do SDK, coloque o código do cliente no campo e clique em Salvar.

![chlimage_1-41](assets/chlimage_1-41.png)

Agora que o código do cliente foi associado ao aplicativo móvel, quando o serviço de nuvem do AMS é configurado pelo Adobe Mobile Dashboard, as configurações do serviço serão fornecidas pelo arquivo ADBMobileConfig.json.

### Serviço da Adobe Mobile Service Cloud {#adobe-mobile-service-cloud-service}

Agora que o AMS foi configurado, é hora de associar o aplicativo móvel ao Adobe Mobile Dashboard. No AEM Mobile Dashboard, localize os Serviços de gerenciamento em nuvem e clique no botão +.

![chlimage_1-42](assets/chlimage_1-42.png)

Selecione o cartão Adobe Mobile Services e clique em Avançar.

![chlimage_1-43](assets/chlimage_1-43.png)

Na etapa do assistente Criar ou Selecionar, selecione o menu suspenso Mobile Service e selecione a entrada Criar configuração. Forneça um título, uma empresa, um nome de usuário, uma senha e selecione o centro de dados apropriado. Se você não souber esses valores, entre em contato com o administrador do Adobe Mobile Service para obtê-los. Depois que todos os campos tiverem sido preenchidos, clique no botão Verificar. O processo de verificação vai para o AMS e verifica as credenciais para a conta, e após a validação bem-sucedida, uma lista de Aplicativos móveis será preenchida onde você seleciona o aplicativo móvel associado na lista suspensa. Clique no botão Enviar para concluir o assistente. O processo pode levar algum tempo para obter os dados de configuração e qualquer análise associada ao aplicativo. Quando o processo estiver concluído, clique no botão Concluído no modal para retornar ao Adobe Mobile Dashboard.

Retornando ao Mobile Dashboard, o bloco Gerenciar serviços em nuvem conterá o serviço em nuvem do AMS. Você também observará que o bloco Analisar métricas será preenchido com relatórios de ciclo de vida.

![chlimage_1-44](assets/chlimage_1-44.png)

## Para autores {#for-authors}

**** Pré-requisito: Como mencionado acima, os administradores precisam configurar a conexão com o Adobe Target Service antes que os autores possam gerar novo conteúdo direcionado.

Depois que o Administrador tiver configurado os dois serviços em nuvem e o desenvolvedor tiver configurado o manipulador mobileappoffers, os autores de conteúdo poderão começar a gerar experiências direcionadas.

A criação de conteúdo direcionado em um aplicativo do AEM Mobile segue um procedimento semelhante ao da criação de sites do AEM:

Consulte aqui para obter uma visão geral completa sobre a [criação de conteúdo direcionado no AEM](/help/sites-authoring/personalization.md)

## Para desenvolvedores {#for-developers}

Os desenvolvedores do AEM que criam aplicativos para dispositivos móveis devem continuar a seguir os padrões comumente usados em todo o AEM ao desenvolver componentes. Aqui, nós o guiaremos pelas etapas necessárias para permitir que os autores de conteúdo criem conteúdo direcionado:

### Manipuladores do Adobe Target ContentSync {#adobe-target-contentsync-handlers}

Para fornecer conteúdo ao conteúdo do dispositivo do usuário, é gerado renderizando as ofertas criadas pelos autores de conteúdo do AEM. Para lidar com a renderização de ofertas de destino, há um novo manipulador de sincronização de conteúdo que processará as ofertas. Usando o aplicativo de referência híbrida como nossa amostra, o pacote de conteúdo en (inglês) contém o ContentSyncConfig com um manipulador [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) . O próximo passo é crucial para renderizar ofertas ao dispositivo. O manipulador mobileappoffers tem uma propriedade path que identifica o caminho para a atividade de personalização que deve ser usada para o aplicativo.

Por exemplo, se houver uma atividade localizada em */content/campaign/hybridref* , copie esse caminho e cole-o como o valor para a propriedade *path* do manipulador mobileappoffers.

>[!NOTE]
>
>Para o Aplicativo de referência híbrido existem dois processadores mobileappoffers, um para o dev e outro para as produções.

Depois que o caminho das atividades for definido na propriedade path do manipulador mobileappoffers, salve o manipulador. O manipulador agora estará pronto para iniciar a renderização de ofertas para nossos dispositivos móveis.

### Modo de renderização {#render-mode}

O manipulador mobileappoffers está configurado de forma diferente para configurações de publicação e desenvolvimento. Para configurações de publicação, há uma propriedade chamada *renderMode* com um valor de *publish* definido no nó cq:ContentSyncConfig. O manipulador mobileappoffers faz referência ao renderMode e, se definido para publicar, modificará a ID da mbox que é criada. Por padrão, as mboxes criadas pelo AEM têm um valor —author anexado à ID da mbox. Isso identifica que a atividade não foi publicada e deve usar a campanha não publicada para as resoluções da oferta.

Quando o conteúdo é preparado pelo Adobe Mobile Dashboard, o conteúdo preparado é considerado como conteúdo pronto para produção e é renderizado por meio da configuração de sincronização de conteúdo não dev. A renderização dessa maneira fará com que o —autor seja removido de todas as IDs de mbox e espera que uma atividade publicada esteja disponível no servidor Target. Antes de testar o conteúdo preparado, verifique se a atividade foi publicada.

### Desenvolvimento de aplicativos de personalização {#personalization-app-development}

#### Componentes {#components}

A base para qualquer conteúdo normalmente é um componente de página que estende um dos componentes básicos da página do AEM wcm/Foundation/components/page ou fundação/componentes/página, dependendo se você estiver usando HTL ou JSPs. A duração dessas etapas se concentrará no uso do wcm/base/componentes/componente de página. A estrutura básica do componente de página é dividida em vários scripts, com cada script fornecendo a finalidade específica de permitir que o desenvolvedor organize e substitua seu código, se necessário. Os dois scripts de interesse para a Personalização são head.html e body.html. Esses dois scripts fornecem uma área em que o código pode ser inserido para suportar a criação do Context Hub, dos Serviços em nuvem e do Mobile.

Esta é uma visão geral dos dois scripts principais usados para ativar a definição de metas de conteúdo.

#### head.html {#head-html}

Para fornecer ao autor a capacidade de direcionar seu conteúdo, o menu de destino precisa ser adicionado à página para que o autor possa alterar o contexto do modo de edição para o modo de definição de metas. Para ativar esse recurso, o desenvolvedor deve modificar o script head.html para incluir o seguinte trecho de código próximo à parte superior do elemento head.html ou o mais próximo possível do elemento &lt;title>&lt;/title>.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Observe que o script só deve ser incluído quando o Modo WCM não estiver desativado, de modo que quando o Modo WCM estiver desativado (consulte a seção do manipulador ContentSync para obter detalhes) o script não será incluído no código final do aplicativo.

Para fornecer aos autores a capacidade de visualizar o conteúdo direcionado, o editor precisa ser capaz de localizar a configuração do serviço em nuvem do Adobe Target. O bloco de código abaixo adiciona dois scripts importantes. A primeira adição da capacidade da página de localizar o serviço em nuvem do Target associado e realizar as chamadas para o Adobe Target. O segundo é a adição da categoria cq.apps.targeting.

A categoria **cq.apps.targeting** substitui o componente cq/personalização/componente/destino padrão e usa o componente mobileapps/components/target que renderiza ofertas especificamente para o consumo de aplicativos móveis. Mais detalhes sobre isso serão discutidos na seção Componente do Target.

O código deve ser adicionado em head.html e colocado logo antes do final do elemento &lt;/head>.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>Observe que o bloco de código está encapsulado em um modo WCM que não está sendo desativado, portanto, só entra em execução enquanto o autor do conteúdo está trabalhando na criação de conteúdo. Os scripts do serviço de nuvem não serão adicionados ao código de tempo de execução móvel gerado.

#### body.html {#body-html}

Para permitir que o autor do conteúdo possa testar diferentes personas, o script body.html precisa incluir o seguinte bloco de código como o primeiro filho do elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

O último pedaço de código necessário está na parte inferior do body.html. Esse pedaço de código procura o serviço de nuvem associado e injeta o código do mecanismo de direcionamento apropriado.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Pedido de referência {#reference-application}

Exemplos de head.html e body.html podem ser encontrados no aplicativo [de referência híbrida do](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile que mostra o desenvolvedor onde colocar os blocos de script dentro dos dois scripts.

### Manipuladores de sincronização de conteúdo {#content-sync-handlers}

Quando o autor do conteúdo terminar de criar conteúdo para o aplicativo móvel, a próxima etapa é baixar a fonte e criar o aplicativo ou preparar o conteúdo a ser publicado. Há várias etapas que o desenvolvedor está envolvido para fazer isso acontecer. Para auxiliar na renderização do conteúdo, o AEM Mobile utiliza manipuladores de sincronização de conteúdo para renderizar e empacotar o conteúdo. Um novo manipulador de sincronização de conteúdo foi introduzido para o caso de uso Personalização para renderizar o conteúdo direcionado. O manipulador &#39;mobileappoffers&#39; sabe como renderizar as ofertas de destino associadas que foram criadas pelo autor do conteúdo. O manipulador mobileappoffers estende o manipulador de atualização de páginas abstratas, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileappoffers têm as seguintes propriedades.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>regravar</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>A propriedade rewrite identifica como os caminhos no conteúdo devem ser regravados.</td>
  </tr>
  <tr>
   <td>includePageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>A propriedade includePageTypes é opcional, padronizando para páginas que têm tipos de recursos de cq/personalization/components/teaserpage e cq/personalization/components/offerproxy. Esses dois tipos de recurso são os tipos de recurso padrão usados quando o conteúdo é direcionado. Se tipos de recursos adicionais precisarem ser suportados, eles devem ser adicionados à lista de includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>A localização do aplicativo.</td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>mobileappoffers</td>
   <td>O nome do manipulador que está sendo mobileappoffers.</td>
  </tr>
  <tr>
   <td>seletor</td>
   <td>mão</td>
   <td>O seletor tandt é usado para renderizar o conteúdo direcionado. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>O diretório raiz onde o conteúdo renderizado deve ser mantido.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true| false</td>
   <td>Se verdadeiro, qualquer imagem incluída na oferta será renderizada. Se imagens falsas forem ignoradas.</td>
  </tr>
  <tr>
   <td>includeVideos</td>
   <td>true| false</td>
   <td>Se verdadeiro, qualquer vídeo incluído na oferta será renderizado. Se vídeos falsos forem ignorados.</td>
  </tr>
  <tr>
   <td>path</td>
   <td>/content/campaign/&lt;marca&gt;</td>
   <td>Aponta para a marca da campanha na qual as ofertas participam. Atualmente, todas as ofertas devem vir da mesma campanha.</td>
  </tr>
  <tr>
   <td>profundo</td>
   <td>true| false</td>
   <td>Se verdadeiro recursivamente renderizar todas as páginas secundárias, se falso não for recorrente. </td>
  </tr>
  <tr>
   <td>extensão</td>
   <td>html</td>
   <td>Define a extensão do recurso que está sendo renderizado. Defina para html de modo que as páginas tenham uma extensão .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O aplicativo [de referência híbrida do](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile tem a configuração padrão do manipulador mobileappoffer. A propriedade path na amostra está vazia, pois depende do local da campanha. Depois que um autor da Campanha criar uma Campanha, o administrador dos aplicativos deverá associar a Campanha ao manipulador especificando a propriedade path para apontar para a Campanha.

### Componente de destino {#target-component}

Para ajudar a renderizar conteúdo especificamente para aplicativos móveis, o AEM Mobile usa os aplicativos/componentes/componente de destino móveis. O componente de destino móvel estende o componente cq/personalization/components/target e substitui o script engine_tnt.jsp. Ao substituir o engine_tnt.jsp, isso permite que o AEM Mobile controle o HTML gerado para o caso de uso de aplicativos móveis. Para cada componente direcionado por um autor de conteúdo, uma mbox associada é criada pelo engine_tnt.jsp.

Para cada mbox, um atributo de direcionamento **do** cq é adicionado, permitindo que os desenvolvedores de aplicativos gravem um código personalizado para consumir e usar, como desejar. O aplicativo [de referência híbrido do](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) AEM Mobile tem um exemplo de diretiva angular que usa o atributo cq-targeting. O conceito de substituição de conteúdo quando e como é feito depende muito do desenvolvedor de aplicativos móveis. Há um SDK móvel disponibilizado via AEM /etc/clientlibs/mobileapps/js/mobileapps.js que fornece uma API para chamar o serviço Adobe Targeting. Cabe ao desenvolvedor do aplicativo especificar quando a chamada deve ser feita de acordo com o design de seu aplicativo.

## O que vem depois? {#what-s-next}

1. [Iniciar minha experiência com aplicativos do AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gerenciar o conteúdo do meu aplicativo](/help/mobile/phonegap-manage-app-content.md)
1. [Criar meu aplicativo](/help/mobile/building-app-mobile-phonegap.md)
1. [Acompanhar o desempenho do meu aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Fornecer uma experiência personalizada com o aplicativo Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensagens importantes para meus usuários](/help/mobile/phonegap-push-notifications.md)
