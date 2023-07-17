---
title: Configuração do Cloud Service Adobe Target
description: Siga esta página para entender como obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e, finalmente, gerar o conteúdo.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: d370d772-ef4d-4f38-826c-e90d07735822
source-git-commit: 96e2e945012046e6eac878389b7332985221204e
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---

# Configuração do Cloud Service Adobe Target {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte da [Introdução ao Adobe Experience Manager (AEM) Mobile](/help/mobile/getting-started-aem-mobile.md) Guia do, um ponto de partida recomendado para referência do AEM Mobile.

Há várias etapas que devem ser seguidas antes que os autores de conteúdo possam começar a gerar conteúdo direcionado para aplicativos móveis: é preciso obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e, por fim, gerar o conteúdo.

Pressupõe-se que a [Aplicativo de referência híbrida do AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) O foi implantado e pode ser acessado com êxito por meio do Painel do AEM Mobile.

## Permissões {#permissions}

Os usuários que precisam de acesso ao console de personalização devem fazer parte da `target-activity-authors` grupo. Sugere-se que, como parte da configuração de usuários e grupos, o grupo de atividades de destino seja adicionado ao grupo de aplicativos-administradores. Ao adicionar o grupo target-activity-author, os usuários poderão ver a entrada do menu de navegação Personalização.

Esquecer de adicionar os usuários ou grupos que deseja ter acesso ao Admin Console de personalização ao grupo target-activity-author impede que os usuários vejam o console de personalização.

## Cloud Services {#cloud-services}

Para que o conteúdo direcionado funcione nos aplicativos móveis, há dois serviços que precisam ser configurados: o Adobe Target Service e o Adobe Mobile Services. O Serviço do Adobe Target fornece o mecanismo para processar solicitações de clientes e retornar o conteúdo personalizado. O serviço Adobe Mobile Services fornece a conexão entre os serviços da Adobe e o aplicativo móvel por meio do arquivo ADBMobileConfig.json, que é consumido pelo plug-in AMS Cordova. No Painel do AEM Mobile, é possível configurar o aplicativo adicionando os dois serviços.

## Cloud Service Adobe Target {#adobe-target-cloud-service}

No Painel do AEM Mobile, localize Gerenciar Cloud Services e clique no botão +.

![chlimage_1-8](assets/chlimage_1-8.png)

No assistente Adicionar Cloud Service, selecione o cartão de serviço na nuvem &quot;Adobe Target&quot; e clique em Avançar.

![chlimage_1-9](assets/chlimage_1-9.png)

No menu suspenso Selecionar uma configuração, é possível criar uma configuração ou selecionar uma existente. Para criar uma configuração, selecione &quot;Criar configuração&quot; na lista suspensa. Insira um título para a configuração do Target. Insira o código de cliente, email e senha associados à sua conta Target. Se você não souber os valores desses campos, entre em contato com o suporte da Adobe Target. Clique no botão &quot;Verificar&quot; para validar as credenciais. Depois de verificado, clique no botão Submit para criar o serviço na nuvem.

O serviço de nuvem criado é associado automaticamente ao aplicativo móvel por meio do assistente. O valor da propriedade cq:cloudserviceconfigs é definido no nó jcr:content do nó do grupo de aplicativos. Para a amostra de aplicativo híbrido, ele é definido em /content/mobileapps/hyper-reference-app/jcr:content com o valor apontando para o nó de estrutura gerado automaticamente em /etc/cloudservices/testandtarget/adobe-target—aem-apps/framework. O nó de estrutura tem duas propriedades definidas por padrão, gênero e idade. A estrutura é usada apenas pela visualização do AEM e não tem impacto no dispositivo.

Após a conclusão do assistente, o bloco Gerenciar Cloud Service contém o serviço de nuvem do Target, no entanto, contém um aviso sobre uma conta ausente do Adobe Mobile Service.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

É necessário vincular uma conta do Adobe Mobile Services (AMS) ao aplicativo também, o serviço AMS fornece o arquivo ADBMobileConfig.json necessário, que contém as informações do código de cliente do Target. Antes de criar uma associação com a conta do AMS, a conta do AMS deve ser modificada por um usuário que tenha permissões para o AMS.

### Código do cliente {#client-code}

Para fazer logon na visita de serviços do AMS [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), selecione o aplicativo para dispositivos móveis e clique nas configurações. Localize o campo Opções de destino do SDK, coloque o código de cliente no campo e clique em Salvar.

![chlimage_1-11](assets/chlimage_1-11.png)

Agora que o código do cliente foi associado ao aplicativo móvel, quando o serviço em nuvem AMS é configurado por meio do Painel do Adobe Mobile, as configurações do serviço são entregues por meio do arquivo ADBMobileConfig.json.

### Serviço Móvel Adobe Pode Servir {#adobe-mobile-service-could-service}

Agora que o AMS foi configurado, é hora de associar o aplicativo móvel no Painel do Adobe Mobile. No Painel do AEM Mobile, localize Gerenciar Cloud Services e clique no botão +.

![chlimage_1-12](assets/chlimage_1-12.png)

Selecione o cartão Adobe Mobile Services e clique em Avançar.

![chlimage_1-13](assets/chlimage_1-13.png)

Na etapa Criar ou selecionar assistente, selecione o menu suspenso Mobile Service e selecione a entrada Criar configuração. Forneça o título, a empresa, o nome de usuário, a senha e selecione o data center apropriado. Se você não souber esses valores, entre em contato com o administrador do Adobe Mobile Service para obtê-los. Depois que todos os campos forem preenchidos, clique em **Verificar**. O processo de verificação vai para o AMS e verifica as credenciais da conta. Após a validação bem-sucedida, uma lista de Aplicativos móveis será preenchida, onde você selecionará o aplicativo móvel associado na lista suspensa. Clique no botão Enviar para concluir o assistente. O processo pode levar algum tempo para obter os dados de configuração e qualquer análise associada ao aplicativo. Após a conclusão do processo, clique em **Concluído** no modal para retornar ao Painel do Adobe Mobile.

Voltando ao Painel de publicação de conteúdo para dispositivos móveis, o bloco Gerenciar Cloud Services contém o serviço de nuvem AMS. Observe também que o bloco Analisar métricas é preenchido com relatórios de ciclo de vida.

![chlimage_1-14](assets/chlimage_1-14.png)

## Manipuladores de sincronização de conteúdo do Target {#target-content-sync-handlers}

Para entregar conteúdo ao dispositivo do usuário, o conteúdo é gerado por meio da renderização das ofertas criadas por autores de conteúdo AEM. Para lidar com a renderização de ofertas de destino, há um novo manipulador de sincronização de conteúdo que processa as ofertas. Usando o aplicativo de referência híbrida como amostra, o pacote de conteúdo en (inglês) contém o ContentSyncConfig com um [mobileapproffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml) manipulador. A próxima etapa é crucial para renderizar ofertas para o dispositivo. O manipulador mobileapproffers tem uma propriedade path que identifica o caminho para a atividade de personalização usada para o aplicativo.

Por exemplo, se houver uma atividade em */content/campaigns/hybridref*, copie esse caminho e cole-o como o valor no campo *caminho* propriedade do manipulador mobileapproffers.

Para o Aplicativo de Referência Híbrido, há dois manipuladores mobileapproffers, um para o desenvolvimento e outro para produções.

Depois que o caminho das atividades for definido na propriedade path do manipulador mobileapproffers, salve o manipulador. O manipulador agora está pronto para iniciar a renderização de ofertas para dispositivos móveis.

### Modo de renderização {#render-mode}

O manipulador mobileapproffers é configurado de forma diferente para configurações de publicação e desenvolvimento. Para configurações de publicação, há uma propriedade chamada *renderMode* com um valor de *publicar* definido no nó cq:ContentSyncConfig. O manipulador mobileapproffers faz referência a renderMode e, se definido para publicar, edita a id da mbox que é criada. Por padrão, as mboxes criadas por AEM têm um valor —author anexado à id da mbox. Isso identifica que a atividade não foi publicada e deve usar a campanha não publicada para resoluções de oferta.

Quando o conteúdo é preparado por meio do Painel do Adobe Mobile, o conteúdo preparado é considerado conteúdo pronto para produção e é renderizado por meio da Configuração de sincronização de conteúdo não-desenvolvimento. A renderização desta forma faz com que o — author seja removido de todas as IDs de mbox e espera que uma atividade publicada esteja disponível no servidor Target. Antes de testar o conteúdo por etapa, verifique se a atividade foi publicada.

## Criação de conteúdo {#creating-content}

Agora que os serviços em nuvem foram criados e o manipulador mobileapproffers foi configurado, os autores de conteúdo podem começar a gerar experiências direcionadas.
