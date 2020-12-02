---
title: Configuração do Adobe Target Cloud Service
seo-title: Configuração do Adobe Target Cloud Service
description: Siga esta página para entender como obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e finalmente gerar o conteúdo.
seo-description: Siga esta página para entender como obter o conjunto correto de permissões para usuários e grupos, criar serviços em nuvem, configurar o aplicativo para a atividade e finalmente gerar o conteúdo.
uuid: 569f9c6d-f521-488a-9e51-f43b7a214dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 8cd6480f-cb4f-40dd-a444-8ba463b78604
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 0%

---


# Configuração do Adobe Target Cloud Service {#configuring-adobe-target-cloud-service}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Este documento faz parte do [Guia de introdução ao AEM Mobile](/help/mobile/getting-started-aem-mobile.md), um ponto de partida recomendado para referência ao AEM Mobile.

Há várias etapas que precisam ser reunidas antes que os autores de conteúdo possam gerar start de conteúdo direcionado para aplicativos móveis: Há o conjunto correto de permissões para usuários e grupos, a criação de serviços em nuvem, a configuração do aplicativo para a atividade e, por fim, a geração do conteúdo.

A suposição a seguir é que o [Aplicativo de Referência Híbrida da AEM Mobile](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference) foi implantado e acessível com êxito por meio do Painel AEM Mobile.

## Permissões  {#permissions}

Os usuários que precisam de acesso ao console de personalização precisam fazer parte do grupo `target-activity-authors`. Sugere-se que, como parte da configuração de usuários e grupos, o público alvo-atividade-grupo seja adicionado ao grupo apps-admins. Ao adicionar o grupo públicos alvos-atividades-autores, isso permitirá que os usuários possam ver a entrada do menu de navegação Personalização.

Esquecer de adicionar os usuários ou grupos aos quais você deseja ter acesso ao console de administração de personalização ao grupo públicos alvos-atividades-autores impedirá que os usuários vejam o console de personalização.

## Cloud Services {#cloud-services}

Para obter conteúdo direcionado trabalhando para aplicativos móveis, há dois serviços que precisam ser configurados: O serviço Adobe Target e o serviço Adobe Mobile Services. O Adobe Target Service fornece o mecanismo para processar solicitações de clientes e retornar o conteúdo personalizado. O serviço Adobe Mobile Services fornece a conexão entre os serviços do Adobe e o aplicativo móvel por meio do arquivo ADBMobileConfig.json, que é consumido pelo plug-in do Cordova do AMS. No Painel AEM Mobile, você pode configurar seu aplicativo adicionando os dois serviços.

## Adobe Target Cloud Service {#adobe-target-cloud-service}

No Painel AEM Mobile, localize os Cloud Services Manage e clique no botão +.

![chlimage_1-8](assets/chlimage_1-8.png)

No assistente Adicionar Cloud Service, selecione a placa de serviço em nuvem &quot;Adobe Target&quot; e clique em Avançar.

![chlimage_1-9](assets/chlimage_1-9.png)

Na lista suspensa Selecionar uma configuração, é possível criar uma nova configuração ou selecionar uma configuração existente. Para criar uma nova configuração, selecione &quot;Criar configuração&quot; na lista suspensa. Digite um título para a configuração do Público alvo. Insira o código do cliente, o email e a senha associados à sua conta do Público alvo. Se você não souber os valores desses campos, entre em contato com o suporte da Adobe Target. Clique no botão &quot;Verificar&quot; para validar as credenciais. Depois de verificado, clique no botão Enviar para criar o serviço de nuvem.

O serviço de nuvem que é criado é automaticamente associado ao aplicativo móvel por meio do assistente. O valor da propriedade cq:cloudserviceconfigs é definido no nó jcr:content do nó de grupo de aplicativos. Para a amostra de aplicativo híbrido, ela é definida em /content/mobileapps/híbridos-reference-app/jcr:content com o valor apontando para o nó de estrutura gerado automaticamente localizado em /etc/cloudservices/testandtarget/adobe-público alvo—aem-apps/framework. O nó da estrutura tem duas propriedades definidas por padrão, gênero e idade. A estrutura é usada apenas pela visualização AEM e não tem nenhum impacto no dispositivo.

Após a conclusão do assistente, o bloco Gerenciar Cloud Service conterá o serviço de nuvem do Público alvo, no entanto, ele contém um aviso sobre a falta de uma conta do Adobe Mobile Service.

![chlimage_1-10](assets/chlimage_1-10.png)

## Adobe Mobile Service {#adobe-mobile-service}

É necessário vincular uma conta do Adobe Mobile Services (AMS) ao aplicativo também, o serviço AMS fornece o arquivo ADBMobileConfig.json necessário que contém as informações do código do cliente do Público alvo. Antes de criar uma associação com a conta AMS, a conta AMS precisa ser modificada por um usuário que tenha permissões para o AMS.

### Código do cliente {#client-code}

Para fazer logon nos serviços AMS, visite [https://mobilemarketing.adobe.com](https://mobilemarketing.adobe.com/), selecione o aplicativo móvel e clique nas configurações. Localize o campo Opções de Público alvo do SDK, coloque o código do cliente no campo e clique em Salvar.

![chlimage_1-11](assets/chlimage_1-11.png)

Agora que o código do cliente foi associado ao aplicativo móvel, quando o serviço de nuvem do AMS é configurado por meio do Painel Adobe Mobile, as configurações do serviço serão fornecidas por meio do arquivo ADBMobileConfig.json.

### Serviço Adobe Mobile Service Poderia Service {#adobe-mobile-service-could-service}

Agora que o AMS foi configurado, é hora de associar o aplicativo móvel ao Painel Adobe Mobile. No Painel AEM Mobile, localize os Cloud Services Manage e clique no botão +.

![chlimage_1-12](assets/chlimage_1-12.png)

Selecione o cartão Adobe Mobile Services e clique em Avançar.

![chlimage_1-13](assets/chlimage_1-13.png)

Na etapa do assistente Criar ou Selecionar, selecione o menu suspenso Mobile Service e selecione a entrada Criar configuração. Forneça um título, empresa, nome de usuário, senha e selecione o centro de dados apropriado. Se você não souber esses valores, entre em contato com o administrador do Adobe Mobile Service para obtê-los. Depois que todos os campos tiverem sido preenchidos, clique no botão Verificar. O processo de verificação vai para o AMS e verifica as credenciais para a conta, e, após a validação bem-sucedida, uma lista de Aplicativos Móveis será preenchida onde você seleciona o aplicativo móvel associado na lista suspensa. Clique no botão Enviar para concluir o assistente. O processo pode levar algum tempo para obter os dados de configuração e qualquer análise associada ao aplicativo. Quando o processo estiver concluído, clique no botão Concluído do modal para retornar ao Painel Adobe Mobile.

Retornando ao Painel móvel, o bloco Gerenciar Cloud Services conterá o serviço de nuvem AMS. Você também observará que o bloco Analisar métricas será preenchido com relatórios de ciclo de vida.

![chlimage_1-14](assets/chlimage_1-14.png)

## Manipuladores de sincronização de conteúdo do público alvo {#target-content-sync-handlers}

Para fornecer conteúdo ao conteúdo do dispositivo do usuário, é gerado renderizando as ofertas criadas por autores de conteúdo AEM. Para lidar com a renderização do público alvo oferta, há um novo manipulador de sincronização de conteúdo que processará o oferta. Usando o Aplicativo de referência híbrido como nossa amostra, o pacote de conteúdo en (inglês) contém o ContentSyncConfig com um manipulador [mobileappoffers](https://github.com/Adobe-Marketing-Cloud-Apps/aem-mobile-hybrid-reference/blob/master/aem-package/content-author/src/main/content/jcr_root/content/mobileapps/hybrid-reference-app/en/_jcr_content/pge-app/app-config-dev/targetOffers/.content.xml). A próxima etapa é crucial para renderizar ofertas ao dispositivo. O manipulador mobileappoffers tem uma propriedade path que identifica o caminho para a atividade de personalização a ser usada para o aplicativo.

Por exemplo, se houver uma atividade localizada em */content/campanha/hybridref* copie esse caminho e cole-o como o valor para a propriedade *path* do manipulador mobileappoffers.

Para o Aplicativo de referência híbrido existem dois processadores mobileappoffers, um para o dev e outro para as produções.

Depois que o caminho do atividade for definido na propriedade path do manipulador mobileappoffers, salve o manipulador. O manipulador agora estará pronto para start de ofertas de renderização para nossos dispositivos móveis.

### Modo de renderização {#render-mode}

O manipulador mobileappoffers está configurado de forma diferente para configurações de publicação e desenvolvimento. Para configurações de publicação, há uma propriedade chamada *renderMode* com um valor de *publish* definido no nó cq:ContentSyncConfig. O manipulador mobileappoffers faz referência ao renderMode e, se definido para publicar, modificará a ID da mbox que é criada. Por padrão, as mboxes criadas por AEM têm um valor —author anexado à ID da mbox. Isso identifica que a atividade não foi publicada e deve usar a campanha não publicada para resoluções de oferta.

Quando o conteúdo é preparado por meio do Painel Adobe Mobile, o conteúdo preparado é considerado como conteúdo pronto para produção e é renderizado por meio da configuração de sincronização de conteúdo não dev. A renderização dessa forma fará com que o —autor seja removido de todas as IDs da mbox e espera que uma atividade publicada esteja disponível no servidor do Público alvo. Antes de testar o conteúdo preparado, verifique se a atividade foi publicada.

## Criação de conteúdo {#creating-content}

Agora que os serviços em nuvem foram criados e o manipulador mobileappoffers foi configurado, os autores de conteúdo agora podem gerar start gerando experiências direcionadas.
