---
title: Personalização de conteúdo do Adobe Experience Manager Mobile
description: Siga esta página para saber mais sobre o recurso de personalização de conteúdo móvel do Adobe Experience Manager (AEM) que permite aos autores do AEM personalizar o conteúdo de aplicativos móveis usando o Adobe Target.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 70d7ee0d-2f6d-4f97-a6e2-b02d84a0ca42
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2550'
ht-degree: 0%

---

# Personalização de conteúdo do AEM Mobile{#aem-mobile-content-personalization}

{{ue-over-mobile}}

>[!NOTE]
>
>Este documento faz parte do [Guia de Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md), um ponto de partida recomendado para referência do AEM Mobile.

O recurso de personalização de conteúdo do AEM Mobile permite que os [Criadores de AEM](#author) personalizem o conteúdo do aplicativo móvel usando o [Adobe Target](https://business.adobe.com/products/target/adobe-target.html). Isso permite a entrega de ofertas direcionadas aos usuários de aplicativos móveis. O Adobe Experience Manager Mobile oferece a capacidade de criar, direcionar e fornecer conteúdo que fornecerá ao usuário conteúdo específico para suas preferências individuais.

No AEM, para que os autores comecem a criar esse conteúdo, administradores e desenvolvedores devem primeiro preparar o ambiente.

[Administradores do AEM](#administrator) são necessários para estabelecer uma conexão entre o AEM Mobile e o Cloud Service Adobe Target.

Enquanto isso, os [desenvolvedores](#developer) do AEM Mobile devem editar seus scripts existentes para facilitar a criação de conteúdo direcionado.

## Para administradores {#for-administrators}

Há várias etapas que devem ser seguidas antes que os autores de conteúdo possam começar a gerar conteúdo direcionado para aplicativos móveis: é preciso obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e, por fim, gerar o conteúdo.

Este artigo orienta você pelo processo usado para configurar o [Aplicativo de Referência Híbrida do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) para direcionamento.

A suposição a partir de agora é que o aplicativo de referência híbrida do AEM Mobile foi implantado e está acessível com sucesso por meio do painel do AEM Mobile.

Para que os autores possam gerar conteúdo direcionado em um aplicativo, a instância do AEM deve ser [configurada com o Cloud Service do Adobe Target.](/help/mobile/aem-mobile-configuring-cloud-service.md)

### Permissões {#permissions}

Os usuários que precisam de acesso ao console de personalização devem fazer parte do grupo `target-activity-authors`.

Sugere-se que, como parte da configuração de usuários e grupos, o grupo de atividades de destino seja adicionado ao grupo de aplicativos-administradores. Ao adicionar o grupo target-activity-author, os usuários poderão ver a entrada do menu de navegação do Personalization.

>[!NOTE]
>
>Esquecer de adicionar os usuários ou grupos que deseja ter acesso ao Admin Console de personalização ao grupo target-activity-author impede que os usuários vejam o console de personalização.

### Cloud Services {#cloud-services}

Para que o conteúdo direcionado funcione nos aplicativos móveis, há dois serviços que precisam ser configurados: o Adobe Target Service e o Adobe Mobile Services. O Serviço do Adobe Target fornece o mecanismo para processar solicitações de clientes e retornar o conteúdo personalizado. O serviço Adobe Mobile Services fornece a conexão entre os serviços da Adobe e o aplicativo móvel por meio do arquivo ADBMobileConfig.json, que é consumido pelo plug-in AMS Cordova. No Painel do AEM Mobile, é possível configurar o aplicativo adicionando os dois serviços.

No Painel do AEM Mobile, localize Gerenciar Cloud Service e clique no botão +.

![chlimage_1-38](assets/chlimage_1-38.png)

No assistente Adicionar Cloud Service, selecione o cartão de serviço na nuvem &quot;Adobe Target&quot; e clique em Avançar.

![chlimage_1-39](assets/chlimage_1-39.png)

No menu suspenso Selecionar uma configuração, é possível criar uma configuração ou selecionar uma existente. Para criar uma configuração, selecione &quot;Criar configuração&quot; na lista suspensa. Insira um título para a configuração do Target. Insira o código de cliente, email e senha associados à sua conta Target. Se você não souber os valores desses campos, entre em contato com o suporte da Adobe Target. Clique no botão &quot;Verificar&quot; para validar as credenciais. Depois de verificado, clique no botão Submit para criar o serviço na nuvem.

>[!NOTE]
>
>O serviço de nuvem criado é associado automaticamente ao aplicativo móvel por meio do assistente. O valor da propriedade cq:cloudserviceconfigs é definido no nó jcr:content do nó do grupo de aplicativos. Para a amostra de aplicativo híbrido, ela é definida em /content/mobileapps/hybrid-reference-app/jcr:content com o valor apontando para o nó de estrutura gerado automaticamente em /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. O nó de estrutura tem duas propriedades definidas por padrão, gênero e idade. A estrutura é usada apenas pela visualização do AEM e não tem impacto no dispositivo.

Após a conclusão do assistente, o bloco Gerenciar Cloud Service conterá o serviço de nuvem do Target. No entanto, contém um aviso sobre a falta de uma conta do Adobe Mobile Service.

![chlimage_1-40](assets/chlimage_1-40.png)

### Adobe Mobile Services {#adobe-mobile-services}

É necessário vincular uma conta do Adobe Mobile Services (AMS) ao aplicativo também, o serviço AMS fornece o arquivo ADBMobileConfig.json necessário, que contém as informações do código de cliente do Target. Antes de criar uma associação com a conta do AMS, a conta do AMS deve ser modificada por um usuário que tenha permissões para o AMS.

### Código do cliente {#client-code}

Para fazer logon nos serviços AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), selecione o aplicativo para dispositivos móveis e clique nas configurações. Localize o campo Opções do SDK Target, coloque o código de cliente no campo e clique em Salvar.

![chlimage_1-41](assets/chlimage_1-41.png)

Agora que o código do cliente foi associado ao aplicativo móvel, quando o serviço em nuvem AMS é configurado por meio do Painel do Adobe Mobile, as configurações do serviço são entregues por meio do arquivo ADBMobileConfig.json.

### Cloud Service do Adobe Mobile Service {#adobe-mobile-service-cloud-service}

Agora que o AMS está configurado, é hora de associar o aplicativo móvel no Painel do Adobe Mobile. No Painel do AEM Mobile, localize Gerenciar Cloud Service e clique no botão +.

![chlimage_1-42](assets/chlimage_1-42.png)

Selecione o cartão Adobe Mobile Services e clique em Avançar.

![chlimage_1-43](assets/chlimage_1-43.png)

Na etapa Criar ou selecionar assistente, selecione o menu suspenso Mobile Service e selecione a entrada Criar configuração. Forneça o título, a empresa, o nome de usuário, a senha e selecione o data center apropriado. Se você não souber esses valores, entre em contato com o administrador do Adobe Mobile Service para obtê-los. Depois que todos os campos forem preenchidos, clique em **Verificar**. O processo de verificação vai para o AMS e verifica as credenciais da conta. Após a validação bem-sucedida, uma lista de Aplicativos móveis é preenchida, onde você seleciona o aplicativo móvel associado na lista suspensa. Clique em **Enviar** para concluir o assistente. O processo pode levar algum tempo para obter os dados de configuração e qualquer análise associada ao aplicativo. Após a conclusão do processo, clique em **Concluído** para voltar para o Painel do Adobe Mobile.

Voltando ao Painel de publicação de conteúdo para dispositivos móveis, o bloco Gerenciar Cloud Service contém o serviço de nuvem AMS. Além disso, o bloco Analisar métricas é preenchido com relatórios de ciclo de vida.

![chlimage_1-44](assets/chlimage_1-44.png)

## Para autores {#for-authors}

**Pré-requisito:** Conforme mencionado acima, os administradores devem configurar a conexão com o Serviço Adobe Target antes que os autores possam gerar novo conteúdo direcionado.

Depois que o administrador configurar os dois serviços em nuvem e o desenvolvedor configurar o manipulador mobileapproffers, os autores de conteúdo poderão começar a gerar experiências direcionadas.

A criação de conteúdo direcionado em um aplicativo do AEM Mobile segue um procedimento semelhante à criação do AEM Sites:

Clique aqui para obter uma visão geral completa sobre [Criação de conteúdo direcionado no AEM](/help/sites-authoring/personalization.md)

## Para desenvolvedores {#for-developers}

Os desenvolvedores de AEM que criam aplicativos móveis devem continuar a seguir os padrões comumente usados no AEM ao desenvolver componentes. Aqui, o Adobe orienta você pelas etapas necessárias para permitir que os autores de conteúdo criem conteúdo direcionado:

### Manipuladores do Adobe Target ContentSync {#adobe-target-contentsync-handlers}

Para entregar conteúdo ao dispositivo do usuário, o conteúdo é gerado por meio da renderização das ofertas criadas por autores de conteúdo AEM. Para lidar com a renderização de ofertas de destino, há um novo manipulador de sincronização de conteúdo que processa as ofertas. Usando o Aplicativo de Referência Híbrida como amostra, o pacote de conteúdo en (inglês) contém o ContentSyncConfig com um manipulador [mobileapproffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). A próxima etapa é crucial para renderizar ofertas para o dispositivo. O manipulador mobileapproffers tem uma propriedade path que identifica o caminho para a atividade de personalização que deve ser usada para o aplicativo.

Por exemplo, se houver uma atividade em */content/campaigns/hybridref*, copie este caminho e cole-o como o valor na propriedade *path* do manipulador mobileapproffers.

>[!NOTE]
>
>Para o Aplicativo de Referência Híbrido, há dois manipuladores mobileapproffers, um para o desenvolvimento e outro para produções.

Depois que o caminho das atividades for definido na propriedade path do manipulador mobileapproffers, salve o manipulador. O manipulador agora está pronto para iniciar a renderização de ofertas para dispositivos móveis.

### Modo de renderização {#render-mode}

O manipulador mobileapproffers é configurado de forma diferente para configurações de publicação e desenvolvimento. Para configurações de publicação, há uma propriedade chamada *renderMode* com um valor de *publish* definido no nó cq:ContentSyncConfig. O manipulador mobileapproffers faz referência a renderMode e, se definido para publicar, edita a id da mbox que é criada. Por padrão, as mboxes criadas por AEM têm um valor —author anexado à id da mbox. Isso identifica que a atividade não foi publicada e deve usar a campanha não publicada para resoluções de oferta.

Quando o conteúdo é preparado por meio do Painel do Adobe Mobile, o conteúdo preparado é considerado conteúdo pronto para produção e é renderizado por meio da Configuração de sincronização de conteúdo não-desenvolvimento. A renderização desta forma fará com que o — author seja removido de todas as ids de mbox e espera que uma atividade publicada esteja disponível no servidor Target. Antes de testar o conteúdo por etapa, verifique se a atividade já está publicada.

### Desenvolvimento de aplicativos Personalization {#personalization-app-development}

#### Componentes {#components}

A base para qualquer conteúdo geralmente é um componente de página que estende um dos componentes básicos da página do AEM wcm/foundation/components/page ou foundation/components/page, dependendo se você estiver usando HTL ou JSPs. A duração dessas etapas se concentra no uso do componente wcm/foundation/components/page. A estrutura básica do componente de página é dividida em vários scripts, com cada script fornecendo a finalidade específica de permitir que o desenvolvedor organize e substitua seu código, se necessário. Os dois scripts de interesse do Personalization são head.html e body.html. Esses dois scripts fornecem uma área em que o código pode ser inserido para oferecer suporte à criação do Context Hub, Cloud Service e Mobile.

Esta é uma visão geral dos dois scripts principais usados para ativar o direcionamento de conteúdo.

#### head.html {#head-html}

Para fornecer ao autor a capacidade de direcionar seu conteúdo, o menu de direcionamento deve ser adicionado à página para que o autor possa alterar o contexto do modo de edição para o modo de direcionamento. Para ativar esse recurso, o desenvolvedor deve modificar o script head.html para incluir o seguinte trecho de código próximo à parte superior do head.html ou o mais próximo possível do elemento &lt;title>&lt;/title>.

```xml
<meta data-sly-test="${!wcmmode.disabled}">
    <div data-sly-call="${clientLib.all @ categories='personalization.kernel'}" data-sly-unwrap></div>
    <div data-sly-resource="${'config' @ resourceType='cq/personalization/components/clientcontext_optimized/config'}" data-sly-unwrap></div>
    <div data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}" data-sly-unwrap></div>
</meta>
```

>[!NOTE]
>
>Inclua o script somente quando o Modo WCM estiver desativado, de modo que, quando o Modo WCM estiver desativado (consulte a seção do manipulador ContentSync para obter detalhes), o script não será incluído no código final do aplicativo.

Para fornecer aos autores a capacidade de pré-visualizar o conteúdo direcionado, o editor deve ser capaz de localizar a configuração do Adobe Target Cloud Service. O bloco de código abaixo adiciona dois scripts importantes. A primeira adicionando a capacidade da página de localizar o serviço de nuvem do Target associado e fazer as chamadas para a Adobe Target. A segunda é a adição da categoria cq.apps.targeting.

A categoria **cq.apps.targeting** substitui o componente padrão cq/personalization/component/target e usa o componente mobileapps/components/target que renderiza ofertas especificamente para consumo do aplicativo móvel. Mais detalhes serão discutidos na seção Componente de direcionamento.

O código deve ser adicionado em head.html e colocado antes do final do elemento &lt;/head>.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-include="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp" data-sly-unwrap></div>
    <meta data-sly-call="${clientLib.all @ categories='cq.apps.targeting'}" data-sly-unwrap></meta>
</div>
```

>[!NOTE]
>
>O bloco de código é colocado em um Modo WCM que não é desativado, portanto, entra em ação somente enquanto o autor de conteúdo está trabalhando na criação do conteúdo. Os scripts do serviço de nuvem não são adicionados ao código de tempo de execução móvel gerado.

#### body.html {#body-html}

Para conceder ao autor de conteúdo a capacidade de testar personas diferentes, o script body.html deve incluir o seguinte bloco de código como o primeiro filho do elemento body.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'clientcontext' @ resourceType='cq/personalization/components/clientcontext_optimized'}" data-sly-unwrap></div>
</div>
```

O último bit de código necessário está na parte inferior do body.html. Esse bit de código procura o serviço de nuvem associado e injeta o código do mecanismo de direcionamento apropriado.

```xml
<div data-sly-test="${!wcmmode.disabled}">
    <div data-sly-resource="${'cloudservices' @ resourceType='cq/cloudserviceconfigs/components/servicecomponents'}" data-sly-unwrap></div>
</div>
```

### Aplicativo de referência {#reference-application}

Exemplos de head.html e body.html podem ser encontrados no [Aplicativo de Referência Híbrida do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) mostrando ao desenvolvedor onde colocar os blocos de script dentro dos dois scripts.

### Manipuladores de sincronização de conteúdo {#content-sync-handlers}

Quando o autor de conteúdo terminar de criar o conteúdo para o aplicativo móvel, a próxima etapa é baixar a origem e criar o aplicativo ou preparar o conteúdo a ser publicado. Há várias etapas com as quais o desenvolvedor está envolvido para fazer isso acontecer. Para auxiliar na renderização do conteúdo, o AEM Mobile usa manipuladores de sincronização de conteúdo para renderizar e empacotar o conteúdo. Um novo manipulador de sincronização de conteúdo foi introduzido para o caso de uso do Personalization para renderizar conteúdo direcionado. O manipulador &quot;mobileapproffers&quot; sabe como renderizar as ofertas de público-alvo associadas que foram criadas pelo autor de conteúdo. O manipulador mobileapproffers estende o manipulador de atualização de páginas abstratas, portanto, muitas das propriedades são semelhantes. Os detalhes do manipulador mobileapproffers têm as seguintes propriedades.

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>reescrever</td>
   <td>+ relativeParentPath<p> - "/"</p> </td>
   <td>A propriedade rewrite identifica como os caminhos no conteúdo devem ser reescritos.</td>
  </tr>
  <tr>
   <td>includedPageTypes</td>
   <td><p>"cq/personalization/components/teaserpage",</p> <p>"cq/personalization/components/offerproxy"</p> </td>
   <td>A propriedade includePageTypes é opcional, padronizando páginas que têm tipos de recursos de cq/personalization/components/teaserpage e cq/personalization/components/offerproxy. Esses dois tipos de recursos são os tipos de recursos padrão usados quando o conteúdo é direcionado. Se outros tipos de recursos tiverem de ser suportados, adicione-os à lista de includePageTypes.</td>
  </tr>
  <tr>
   <td>locationRoot</td>
   <td>/content/mobileapps/&lt;app&gt;</td>
   <td>A localização do aplicativo.</td>
  </tr>
  <tr>
   <td>tipo</td>
   <td>mobileapproffers</td>
   <td>O nome do manipulador que está sendo mobileapproffers.</td>
  </tr>
  <tr>
   <td>seletor</td>
   <td>tandt</td>
   <td>O seletor de tendência é usado para renderizar o conteúdo direcionado. </td>
  </tr>
  <tr>
   <td>targetRootDirectory</td>
   <td>www</td>
   <td>O diretório raiz onde manter o conteúdo renderizado.</td>
  </tr>
  <tr>
   <td>includeImages</td>
   <td>true | false</td>
   <td>Se verdadeiro, todas as imagens incluídas na oferta serão renderizadas. Se false, as imagens serão ignoradas.</td>
  </tr>
  <tr>
   <td>includeVídeos</td>
   <td>true | false</td>
   <td>Se verdadeiro, todos os vídeos incluídos na oferta serão renderizados. Se false, os vídeos são ignorados.</td>
  </tr>
  <tr>
   <td>caminho</td>
   <td>/content/campaigns/&lt;brand&gt;</td>
   <td>Aponta para a marca da campanha da qual as ofertas participam. Atualmente, todas as ofertas devem vir da mesma campanha.</td>
  </tr>
  <tr>
   <td>profundo</td>
   <td>true | false</td>
   <td>Se verdadeiro, renderiza recursivamente todas as páginas secundárias; se falso, não repete. </td>
  </tr>
  <tr>
   <td>extensão</td>
   <td>html</td>
   <td>Define a extensão do recurso que está sendo renderizado. Defina como html de modo que as páginas tenham uma extensão .html.</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O [Aplicativo de Referência Híbrida do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tem a configuração padrão do manipulador mobileappoffer. A propriedade path na amostra está vazia, pois depende do local da campanha. Depois que um autor do Campaign cria uma Campanha, o administrador de aplicativos deve associar a Campanha ao manipulador especificando a propriedade do caminho para apontar para a Campanha.

### Componente do Target {#target-component}

Para ajudar a renderizar conteúdo especificamente para aplicativos móveis, o AEM Mobile usa o componente mobileapps/components/target. O componente de destino móvel estende o componente cq/personalization/components/target e substitui o script engine_tnt.jsp. Ao substituir o engine_tnt.jsp, isso permite que a AEM Mobile controle o HTML gerado para o caso de uso de aplicativos para dispositivos móveis. Para cada componente direcionado por um autor de conteúdo, uma mbox associada é criada pelo engine_tnt.jsp.

Para cada mbox, um atributo de **cq-targeting** é adicionado permitindo que os desenvolvedores de aplicativos gravem código personalizado para consumir e usar da maneira que quiserem. O [Aplicativo de Referência Híbrida do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) tem um exemplo de uma diretiva de Angular que usa o atributo cq-targeting. O conceito de substituição de conteúdo, quando e como ele é feito, depende do desenvolvedor de aplicativos móveis. Existe um SDK para dispositivos móveis fornecido pelo AEM /etc/clientlibs/mobileapps/js/mobileapps.js que fornece uma API para chamar o serviço de Direcionamento de Adobe. Cabe ao desenvolvedor do aplicativo especificar quando essa chamada deve ser feita de acordo com o design do aplicativo.

## O que está por vir? {#what-s-next}

1. [Iniciar minha experiência com o aplicativo AEM Mobile](/help/mobile/starting-aem-phonegap-app.md)
1. [Gerenciar o conteúdo do meu aplicativo](/help/mobile/phonegap-manage-app-content.md)
1. [Criar meu aplicativo](/help/mobile/building-app-mobile-phonegap.md)
1. [Acompanhe o desempenho do meu aplicativo com o Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Ofereça uma experiência de aplicativo personalizada com o Adobe Target](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [Enviar mensagens importantes aos meus usuários](/help/mobile/phonegap-push-notifications.md)
