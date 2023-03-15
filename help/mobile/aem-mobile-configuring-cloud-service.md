---
title: Configuração do Adobe Target Cloud Service
seo-title: Configuring Adobe Target Cloud Service
description: Siga esta página para entender como obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e finalmente gerar o conteúdo.
seo-description: Follow this page to understand how to get right set of permissions for users and groups, creating cloud services, configuring the application for the activity, and finally generating the content.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# Configuração do Adobe Target Cloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte do [Introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md) Guia, um ponto de partida recomendado para referência do AEM Mobile.

Há várias etapas que precisam ser reunidas para que os autores de conteúdo possam começar a gerar conteúdo direcionado para aplicativos móveis: Está recebendo o conjunto correto de permissões para usuários e grupos, criando serviços em nuvem, configurando o aplicativo para a atividade e finalmente gerando o conteúdo.

A suposição que se segue é que a variável [Aplicativo de referência híbrido do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) O foi implantado e acessível com êxito por meio do AEM Mobile Dashboard.

## Permissões {#permissions}

Os usuários que precisam de acesso ao console de personalização precisam fazer parte do `target-activity-authors` grupo. Sugere-se que, como parte da configuração de usuários e grupos, o grupo de atividades do target seja adicionado ao grupo de apps-admins. Ao adicionar o grupo target-activity-authors, isso permitirá que os usuários possam ver a entrada do menu Personalization navigation .

Esquecer de adicionar os usuários ou grupos que você deseja que tenham acesso ao Admin Console de personalização ao grupo de autores de atividades de direcionamento impedirá que os usuários vejam o console de personalização.

## Cloud Services {#cloud-services}

Para obter conteúdo direcionado funcionando para aplicativos móveis, há dois serviços que precisam ser configurados: O serviço Adobe Target e o serviço Adobe Mobile Services. O Adobe Target Service fornece o mecanismo para processar solicitações de clientes e retornar o conteúdo personalizado. O serviço Adobe Mobile Services fornece a conexão entre os serviços da Adobe e o aplicativo móvel por meio do arquivo ADBMobileConfig.json que é consumido pelo plug-in AMS Cordova. No AEM Mobile Dashboard, é possível configurar o aplicativo adicionando os dois serviços.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

No painel do AEM Mobile, localize a caixa Gerenciar Cloud Services e clique no botão + .

![chlimage_1-8](assets/chlimage_1-8.png)

No assistente Adicionar Cloud Service, selecione o cartão de serviço em nuvem &quot;Adobe Target&quot; e clique em Avançar.

![chlimage_1-9](assets/chlimage_1-9.png)

Na lista suspensa Selecionar uma configuração , é possível criar uma nova configuração ou selecionar uma existente. Para criar uma nova configuração, selecione &quot;Criar configuração&quot; na lista suspensa. Insira um título para a configuração do Target. Insira o código de cliente, email e senha associados à conta do Target. Caso não saiba os valores desses campos, entre em contato com o suporte do Adobe Target. Clique no botão &quot;Verificar&quot; para validar as credenciais. Depois de verificado, clique no botão Submit para criar o serviço de nuvem.

O serviço em nuvem criado é associado automaticamente ao aplicativo móvel por meio do assistente. O valor da propriedade cq:cloudserviceconfigs é definido no nó jcr:content do nó do grupo de aplicativos. Para o exemplo de aplicativo híbrido, ele é definido em /content/mobileapps/brid-reference-app/jcr:content com o valor apontando para o nó de estrutura gerado automaticamente localizado em /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. O nó da estrutura tem duas propriedades definidas por padrão, gênero e idade. A estrutura é usada apenas pela pré-visualização AEM e não tem impacto no dispositivo.

Após a conclusão do assistente, o bloco Gerenciar Cloud Service conterá o serviço de nuvem do Target, no entanto, ele contém um aviso sobre uma conta ausente do Adobe Mobile Service.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

É necessário vincular uma conta do Adobe Mobile Services (AMS) ao aplicativo, o serviço AMS fornece o arquivo ADBMobileConfig.json necessário, que contém as informações do código de cliente do Target. Antes de criar uma associação com a conta AMS, a conta AMS precisa ser modificada por um usuário com permissões para o AMS.

### Código do cliente {#client-code}

Para fazer logon nos serviços do AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), selecione o aplicativo móvel e clique nas configurações. Localize o campo Opções de meta do SDK , coloque o código do cliente no campo e clique em Salvar.

![chlimage_1-11](assets/chlimage_1-11.png)

Agora que o código de cliente foi associado ao aplicativo móvel, quando o serviço de nuvem AMS é configurado por meio do painel do Adobe Mobile, as configurações do serviço serão fornecidas por meio do arquivo ADBMobileConfig.json .

### Serviço Adobe Mobile Poderia {#adobe-mobile-service-could-service}

Agora que o AMS foi configurado, é hora de associar o aplicativo móvel no Adobe Mobile Dashboard. No painel do AEM Mobile, localize a caixa Gerenciar Cloud Services e clique no botão + .

![chlimage_1-12](assets/chlimage_1-12.png)

Selecione o cartão do Adobe Mobile Services e clique em Avançar.

![chlimage_1-13](assets/chlimage_1-13.png)

Na etapa Criar ou selecionar assistente , selecione a lista suspensa Mobile Service e selecione a entrada Criar configuração . Forneça um título, empresa, nome de usuário, senha e selecione o data center apropriado. Se não souber esses valores, entre em contato com o administrador do Adobe Mobile Service para obtê-los. Depois que todos os campos tiverem sido preenchidos, clique no botão Verify (Verificar). O processo de verificação vai para o AMS e verifica as credenciais da conta, e, após a validação bem-sucedida, uma lista de Aplicativos móveis será preenchida, onde você seleciona o aplicativo móvel associado na lista suspensa. Clique no botão Enviar para concluir o assistente. O processo pode levar algum tempo para obter os dados de configuração e qualquer análise associada com o aplicativo. Quando o processo estiver concluído, clique no botão Concluído no modal para retornar ao Painel do Adobe Mobile.

Retornando ao painel do Mobile, o bloco Gerenciar Cloud Services conterá o serviço de nuvem do AMS. Você também observará que o bloco Analisar métricas será preenchido com relatórios de ciclo de vida.

![chlimage_1-14](assets/chlimage_1-14.png)

## Manipuladores de sincronização de conteúdo do Target {#target-content-sync-handlers}

Para fornecer conteúdo ao conteúdo do dispositivo do usuário, é gerado renderizando as ofertas criadas por AEM autores de conteúdo. Para lidar com a renderização das ofertas de destino, há um novo manipulador de sincronização de conteúdo que processará as ofertas. Usando o Aplicativo de referência híbrido como nossa amostra, o pacote de conteúdo en (inglês) contém ContentSyncConfig com um [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) manipulador. A próxima etapa é crucial para renderizar ofertas para o dispositivo. O manipulador mobileappoffers tem uma propriedade path que identifica o caminho para a atividade de personalização que deve ser usada para o aplicativo.

Por exemplo, se houver uma atividade localizada em */content/campanhas/hybridref* copie esse caminho e cole-o como o valor na *caminho* propriedade do manipulador mobileappoffers.

Para o Aplicativo de referência híbrido há dois processadores mobileappoffers, um para o desenvolvimento e outro para produções.

Depois que o caminho das atividades for definido na propriedade de caminho do manipulador mobileappoffers, salve o manipulador. O manipulador agora estará pronto para iniciar as ofertas de renderização para nossos dispositivos móveis.

### Modo de renderização {#render-mode}

O manipulador de mobileappoffers é configurado de forma diferente para configurações de publicação e desenvolvimento. Para configurações de publicação, há uma propriedade chamada *renderMode* com um valor de *publicar* definido no nó cq:ContentSyncConfig . O manipulador de mobileappoffers faz referência ao renderMode e, se definido como publicar, modificará a id da mbox que é criada. Por padrão, as mboxes criadas por AEM têm um valor —author anexado à id da mbox. Isso identifica que a atividade não foi publicada e deve usar a campanha não publicada para resoluções de oferta.

Quando o conteúdo é preparado por meio do Adobe Mobile Dashboard, o conteúdo de preparo é considerado conteúdo pronto para produção e é renderizado por meio da Configuração de sincronização de conteúdo não dev. Renderizar dessa forma fará com que o autor do — seja removido de todas as IDs da mbox e espere que uma atividade publicada esteja disponível no servidor do Target. Antes de testar o conteúdo preparado, verifique se a atividade foi publicada.

## Criação de conteúdo {#creating-content}

Agora que os serviços em nuvem foram criados e o manipulador mobileappoffers foi configurado, os autores de conteúdo agora podem começar a gerar experiências direcionadas.
