---
title: Notificações push
seo-title: Push Notifications
description: Siga esta página para saber mais sobre como usar as notificações por push em um aplicativo AEM Mobile.
seo-description: Follow this page to learn about how to use push notifications in an AEM Mobile app.
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '3273'
ht-degree: 1%

---

# Notificações push{#push-notifications}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

Ser capaz de alertar instantaneamente os usuários do aplicativo AEM Mobile com notificações importantes é fundamental para o valor de um aplicativo móvel e de suas campanhas de marketing. Aqui, descrevemos as etapas que precisam ser seguidas para permitir que seu aplicativo receba notificações por push e como configurar e enviar push do AEM Mobile para o aplicativo instalado no telefone. Além disso, esta seção descreve como configurar a variável [Deep Linking](#deeplinking) recurso para suas notificações por push.

>[!NOTE]
>
>*A entrega das notificações por push não é garantida; são mais como anúncios. É feito um melhor esforço para garantir que todos os recebam, mas não sejam um mecanismo de entrega garantido. Além disso, o tempo para enviar uma notificação por push pode variar de menos de um segundo a até meia hora.*

O uso de notificações por push com AEM requer algumas tecnologias diferentes. Primeiro, um provedor de serviço de notificação por push deve ser usado para gerenciar notificações e dispositivos (AEM ainda não faz isso). Dois provedores são configurados prontos para uso com AEM: [Serviço de Notificação Simples da Amazon](https://aws.amazon.com/sns/) (ou SNS), e [Pushwoosh](https://www.pushwoosh.com/). Em segundo lugar, a tecnologia de push para o SO móvel em questão deve passar pelo serviço apropriado — Apple Push Notification Service (ou APNS) para dispositivos iOS; e Google Cloud Messaging (ou GCM) para dispositivos Android. Embora o AEM não se comunique diretamente com esses serviços específicos da plataforma, algumas informações de configuração relacionadas devem ser fornecidas pelo AEM juntamente com as notificações para que esses serviços executem o push.

Depois de instalado e configurado (conforme explicado abaixo), ele funciona assim:

1. Uma notificação por push é criada no AEM e enviada para o provedor de serviços (Amazon SNS ou Pushwoosh).
1. O provedor de serviços o recebe e o envia para o provedor principal (APNS ou GCM).
1. O provedor principal envia a notificação para todos os dispositivos registrados para esse push. Para cada dispositivo, ele usa a rede de dados celulares ou WiFi, o que estiver disponível no momento no dispositivo.
1. A notificação é exibida no dispositivo se o aplicativo para o qual está registrado não estiver em execução. Um usuário que tocar na notificação iniciará o aplicativo e exibirá a notificação dentro dele. Se o aplicativo já estiver em execução, somente a notificação no aplicativo será exibida.

Esta versão do AEM é compatível com dispositivos móveis iOS e Android.

## Visão geral e procedimento {#overview-and-procedure}

Para usar notificações por push em um aplicativo AEM Mobile, as seguintes etapas de alto nível devem ser realizadas.

Normalmente, um Desenvolvedor de AEM irá:

1. Registrar-se nos serviços de mensagens da Apple e da Google
1. Registre-se com um serviço de mensagens por push e configure-o
1. Adicionar suporte por push ao aplicativo
1. Preparar um telefone para testar

Enquanto um Administrador AEM irá:

1. Configurar push em aplicativos AEM
1. Criar e implantar o aplicativo
1. Enviar uma notificação por push
1. Configurar deep linking *(opcional)*

### Etapa 1: Registrar-se nos serviços de mensagens da Apple e da Google {#step-register-with-apple-and-google-messaging-services}

#### Uso do Serviço de Notificação por Push da Apple (APNS) {#using-the-apple-push-notification-service-apns}

Vá para a página do Apple [here](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) para se familiarizar com o serviço de notificação por push da Apple.

Para usar o APNS, você precisará de um **Certificado** arquivo (um arquivo .cer), um push **Chave de privacidade** (um arquivo .p12) e um **Senha da chave privada** do Apple. Instruções sobre como fazer isso podem ser encontradas [here](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### Uso do serviço Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>A Google está substituindo o GCM por um serviço semelhante chamado Firebase Cloud Messaging (FCM). Para obter mais informações sobre o FCM, clique em [here](https://developers.google.com/cloud-messaging/faq).

Vá para a página do Google [here](https://developer.android.com/google/gcm/index.html) para se familiarizar com o Google Cloud Messaging for Android.

Você precisará seguir as etapas [here](https://developer.android.com/google/gcm/gs.html) para **Criar um projeto de API do Google**, **Ativar o serviço GCM** e **Obter uma chave de API**. Você precisará do **Chave da API** para enviar notificações por push para dispositivos Android. Além disso, registre seu **Número do projeto**, que por vezes também é chamada de **Id do Remetente GCM**.

As etapas a seguir mostram um método diferente de criação de chaves de API do GCM:

1. Faça logon no google e acesse o [Página do desenvolvedor do Google](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Escolha seu aplicativo na lista (ou crie um novo).
1. Em Nome do pacote do Android, digite a ID do aplicativo, ou seja, `com.adobe.cq.mobile.weretail.outdoorsapp`. (Se isso não funcionar, tente novamente com &quot;test.test&quot;.)
1. Clique em **Continuar a escolher e configurar serviços**
1. Selecione Cloud Messaging e clique em **Ativar o Google Cloud Messaging**.
1. A nova Chave da API do servidor e a ID do remetente (nova ou existente) serão exibidas.

>[!NOTE]
>
>Registre a chave da API do servidor. Esse valor é inserido no site do provedor de push.

### Etapa 2: Registrar e configurar um serviço de mensagens de push {#step-register-and-configure-a-push-messaging-service}

AEM está configurado para usar um dos três serviços para notificações por push:

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*Amazon SNS* e *Pushwoosh* As configurações permitirão enviar empacotado de dentro AEM telas.

*Adobe Mobile Services* A configuração do permite configurar e enviar notificações por push do Adobe Mobile Services usando uma conta do Adobe Analytics (mas o aplicativo precisa ser criado com esse conjunto de configurações para ativar as notificações por push do AMS).

#### Usar o serviço de mensagens SNS do Amazon {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*É possível encontrar informações sobre o Amazon SNS e um link para criar uma nova conta do AWS [here](https://aws.amazon.com/sns/). Você pode obter uma conta gratuita por um ano.*

Se você não quiser usar o Amazon SNS, ignore essas etapas.

Siga estas etapas para configurar o Amazon SNS para notificações por push:

1. **Registrar-se no Amazon SNS**

   1. Registre sua ID de conta. O formato deve ter doze dígitos sem espaços ou traços, ou seja, &quot;123456789012&quot;.
   1. Certifique-se de estar na região &quot;us-East&quot; ou &quot;eu&quot;, já que uma etapa posterior (Criação do pool de identidade) requer uma dessas opções.
   1. Depois de se registrar, faça logon no console de gerenciamento e selecione [SNS](https://console.aws.amazon.com/sns/) (Serviço de notificações por push). Clique em &quot;Introdução&quot; se for exibido.

1. **Criar chave de acesso e ID**

   1. Clique no nome de logon no canto superior direito da tela e escolha Credenciais de segurança no menu.
   1. Clique em Chaves de acesso e, no espaço abaixo, clique em **Criar nova chave de acesso**.
   1. Clique em **Mostrar chave de acesso** e copie e salve a ID da chave de acesso e a chave de acesso secreta mostradas. Se você escolher a opção para baixar as chaves, você receberá um arquivo csv que contém esses mesmos valores.
   1. Outros certificados relacionados à segurança e outros podem ser gerenciados nesta página.

   >[!NOTE]
   >
   >Uma Chave de acesso pode ser usada para vários aplicativos.

   Para organizações que usam uma conta de &quot;sandbox da AWS&quot;, as etapas são muito semelhantes e descritas abaixo:

   1. Clique no nome de logon no canto superior direito da tela e escolha Minhas credenciais de segurança no menu.
   1. Clique em Usuários na lista esquerda de ações e escolha seu nome de usuário.
   1. Clique na guia Credenciais de segurança .
   1. Aqui você vê suas chaves e cria novas chaves. Salve as chaves para uso posterior.


1. **Criar um tópico**

   1. Clique em **Criar tópico** e escolha um nome de tópico. Registre todos os campos, como Tópico ARN, Proprietário do Tópico, Região, Nome de exibição.
   1. Clique em **Outras ações de tópico** > **Editar Política de Tópico**. Em **Permitir que esses usuários assinem este tópico**, selecione **Todos.**
   1. Clique em **Política de atualização**.

   >[!NOTE]
   >
   >Você pode criar vários tópicos para diferentes cenários, como desenvolvimento, teste, demonstração e assim por diante. O restante da configuração do SNS pode permanecer o mesmo. Crie o aplicativo com um tópico diferente; as notificações por push enviadas para esse tópico serão recebidas somente pelo aplicativo criado com esse tópico.

1. **Criar aplicativos da plataforma**

   1. Clique em Aplicativos e, em seguida, em Criar aplicativo da plataforma. Escolha um nome e selecione uma plataforma (APNS para iOS, GCM para Android). Dependendo da plataforma, outros campos precisarão ser preenchidos:

      1. Para APNS, um arquivo P12, uma senha, um certificado e uma chave privada devem ser inseridos. Estes deveriam ter sido obtidos na etapa seguinte *Uso do Serviço de Notificação por Push da Apple (APNS)* acima.
      1. Para o GCM, é necessário inserir uma Chave de API. Isso deveria ter sido feito na etapa seguinte *Uso do serviço Google Cloud Messaging (GCM)* acima.
   1. Repita a etapa acima uma vez para cada plataforma que você vai suportar. Para enviar para o iOS e Android, dois aplicativos da plataforma devem ser criados.


1. **Criar um pool de identidade**

   1. Use [Cognito](https://console.aws.amazon.com/cognito) para criar um Pool de Identidades, que armazenará dados básicos de usuários não autenticados. Observe que somente as regiões &quot;us-East&quot; e &quot;eu&quot; são compatíveis com o Amazon Cognito no momento.
   1. Nomeie e marque a caixa &quot;Habilitar acesso a identidades não autenticadas&quot;.
   1. Na próxima página (&quot;*Suas identidades Cognito exigem acesso aos seus recursos*&quot;) clique em Permitir.
   1. No canto superior direito da página, clique no link &quot;*Editar pool de identidade&quot;*. A ID do pool de identidade é exibida. Salve este texto para mais tarde.
   1. Na mesma página, escolha a lista suspensa ao lado de &quot;Função não autenticada&quot; e verifique se ela tem a função Cognito_&lt;pool name=&quot;&quot;>UnauthRole selecionada. Salve as alterações.

1. **Configurar acesso**

   1. Faça logon em [Gerenciamento de identidade e acesso](https://console.aws.amazon.com/iam/home) (IAM)
   1. Selecionar funções
   1. Clique na função criada na etapa anterior, chamada Cognito_&lt;youridentitypoolname>Unauth_Role. Registre a &quot;Função ARN&quot; exibida.
   1. Abra &quot;Políticas em linha&quot; se ele ainda não estiver aberto. Você deve ver uma política com um nome como oneClick_Cognito_&lt;youridentitypoolname>Unauth_Role_1234567890123.
   1. Clique em &quot;Editar política&quot;. Substitua o conteúdo do Documento de política por este snippet do JSON:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Versão": "2012-10-17",</p> <p> "Declaração": [</p> <p> {</p> <p> "Ação": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Efeito": "Permitir",</p> <p> "Recurso": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Clique em **Aplicar política**


#### Usar o serviço de mensagens Pushwoosh {#using-the-pushwoosh-messaging-service}

Se não quiser usar o Pushwoosh, ignore esta etapa.

Para utilizar Pushwoosh:

1. **Inscreva-se no Pushwoosh**

   1. Acesse pushwoosh.com e crie uma nova conta.

1. **Criar um token de acesso à API**

   1. No site Encaminhar, vá para o item de menu Acesso à API para gerar um Token de acesso à API. Você precisará gravar isso com segurança.

1. **Criar um novo aplicativo**

   1. Para obter suporte ao Android, é necessário fornecer a chave de API GCM.
   1. Ao configurar o aplicativo, escolha Cordova como a estrutura.
   1. Para obter suporte do iOS, você precisa fornecer o arquivo de certificado (.cer), o certificado push (.p12) e a senha da chave privada; eles devem ter sido obtidos no site APNS da Apple. Para Framework, escolha Cordova.
   1. O Pushwoosh gerará uma ID de aplicativo para esse aplicativo, no formato &quot;XXXXX-XXXXX&quot;, em que cada X é um valor hexadecimal (0 a F).

>[!NOTE]
>
>*Se um segundo aplicativo for configurado no AEM com a mesma ID de aplicativo (e outros valores relacionados): Token de acesso à API e ID do GCM), todas as notificações por push enviadas por meio do segundo aplicativo no AEM serão enviadas para qualquer outro aplicativo com essa ID do aplicativo.*

### Etapa 3: Adicionar suporte por push ao aplicativo {#step-add-push-support-to-the-app}

#### Adicionar configuração do ContentSync {#add-contentsync-configuration}

Crie dois nós de conteúdo (um em app-config e um em app-config-dev) chamados de notificationsConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Com essas propriedades (arquivos .content.xml) :
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot; jcr:primaryType=&quot;nt:unstructured&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;../../../..&quot;
[
targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>O manipulador de sincronização de conteúdo procura esses nós e, se eles não estiverem lá, ele não grava o arquivo page-notifications-config.json.

#### Adicionar bibliotecas de clientes {#add-client-libraries}

As bibliotecas de clientes de notificação por push devem ser adicionadas ao aplicativo seguindo estas etapas:

No CRXDE Lite:

1. Navegar para */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall.*
1. Clique duas vezes na seção incorporada no painel de propriedades.
1. Na caixa de diálogo exibida, adicione uma nova biblioteca do cliente clicando no botão +.
1. No novo campo de texto, adicione &quot;cq.mobile.push&quot; e clique em OK.
1. Adicione mais um chamado cq.mobile.push.amazon e clique em OK.
1. Salve as alterações.

>[!NOTE]
>
>Se as notificações por push forem removidas ou não forem usadas, por considerações de espaço no aplicativo e para evitar mensagens de erro do console, remova essas clientlibs do aplicativo.

### Etapa 4: Preparar um telefone para teste {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*Para notificações por push, é necessário testar em um dispositivo real, já que os emuladores não podem receber notificações por push.*

#### iOS {#ios}

Para o iOS, você precisará usar um computador Mac OS e será necessário associar-se à [Programa para desenvolvedores do iOS](https://developer.apple.com/programs/ios/). Algumas empresas têm licenças corporativas que podem estar disponíveis para todos os desenvolvedores.

Com o XCode 8.1, antes de usar notificações por push, você deve ir para a guia Recursos no seu projeto e ativar as notificações por push.

#### Android {#android}

Para instalar o aplicativo em um telefone Android usando a CLI (veja abaixo: **Etapa 6 - Criar e implantar o aplicativo**), primeiro você deve colocar o telefone no &quot;modo desenvolvedor&quot;. Consulte [Ativação das opções do desenvolvedor no dispositivo](https://developer.android.com/tools/device.html#developer-device-options) para obter detalhes sobre como fazer isso.

### Etapa 5: Configurar push em aplicativos AEM {#step-configure-push-on-aem-apps}

Antes de criar e implantar no dispositivo móvel configurado, é necessário definir as configurações de notificação do serviço de mensagens que você decidiu usar.

1. Crie os grupos de autorização apropriados para notificações por push.
1. Faça logon no AEM como o usuário apropriado, clique na guia Aplicativos .
1. Clique no aplicativo.
1. Localize o bloco Gerenciar Cloud Services e clique no lápis para modificar as configurações de nuvem.
1. Selecione Amazon SNS Connection, Pushwoosh Connection ou Adobe Mobile Services, como a configuração de notificação.
1. Insira as propriedades do provedor, clique em Enviar para salvá-las e em Concluído. Eles não são verificados remotamente nessa etapa, exceto no caso do AMS.
1. Agora você deve ver a configuração inserida no bloco Gerenciar Cloud Services.

### Etapa 6: Criar e implantar o aplicativo {#step-build-and-deploy-the-app}

**Observação:** Consulte também as nossas instruções [here](/help/mobile/building-app-mobile-phonegap.md) sobre como criar aplicativos PhoneGap.

Há duas maneiras de criar e implantar seu aplicativo usando o PhoneGap.

**Observação:** Para testes de notificação por push, os emuladores não serão suficientes porque as notificações por push usam um protocolo distinto entre o provedor por push (Apple ou Google) e o dispositivo. O hardware e emuladores atuais de Mac/PC não suportam isso.

1. *PhoneGap Build* O é um serviço oferecido pelo PhoneGap que criará seu aplicativo para você em seus servidores e permitirá que você o baixe diretamente no dispositivo. Consulte a [Documentação do PhoneGap Build](https://build.phonegap.com/) para saber como configurar e usar o PhoneGap Build.

1. *Interface da Linha de Comando PhoneGap* (CLI) permite usar um conjunto avançado de comandos do PhoneGap na linha de comando para criar, depurar e implantar seu aplicativo. Consulte a [Documentação do desenvolvedor do PhoneGap](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) para saber como configurar e usar a CLI do PhoneGap.

### Etapa 7: Enviar uma notificação por push {#step-send-a-push-notification}

Para criar uma nova notificação e enviá-la, siga estas etapas.

1. Criar uma nova notificação

   * No painel do aplicativo AEM Mobile, localize o bloco Notificações por push .
   * No menu no canto superior direito, escolha &quot;Criar&quot;. Observe que esse botão não estará disponível até que a configuração da nuvem seja definida pela primeira vez.
   * No Assistente para Criar Notificação, insira um título e uma mensagem e clique no botão &quot;Criar&quot;. Sua notificação agora está pronta para ser enviada imediatamente ou posteriormente. Ele pode ser editado e a mensagem e/ou o título podem ser alterados e salvos.

1. Enviar a notificação

   * No painel Aplicativos, localize o bloco Notificações por push .
   * Selecione a notificação ou clique no botão de detalhes na parte inferior direita (. . .), para mostrar a lista de notificações. Essa lista também indica se uma notificação está pronta para ser enviada, já foi enviada ou se ocorreu um erro durante o envio.
   * Marque a caixa de seleção de uma notificação (somente) e clique no botão &quot;Enviar notificação&quot; acima da lista. Você terá uma chance de &quot;Cancelar&quot; ou &quot;Enviar&quot; a notificação na caixa de diálogo exibida.

1. Lidar com os resultados

   * Se o serviço de notificação por push (Amazon SNS ou Pushwoosh) receber a solicitação Send , confirmá-la como válida e enviá-la aos provedores nativos (APNS e GCM) com êxito, a caixa de diálogo Send será fechada sem mensagem. Na lista de notificações, o status dessa notificação será listado como Enviado.
   * Se o envio por push falhar, a caixa de diálogo mostrará uma mensagem indicando o problema. Na lista de notificações, o status dessa notificação será listado como Erro, mas se o problema for corrigido, a notificação poderá ser enviada novamente. No caso de um erro, informações adicionais sobre o erro devem aparecer no log de erros do servidor.
   * Observe que há algumas diferenças de plataforma entre as notificações por push do iOS e do Android. Entre eles:

      * Ao criar com a CLI, o aplicativo será iniciado após a implantação no Android. No iOS, é necessário iniciá-lo manualmente. Como a etapa de registro de push acontece na inicialização, os aplicativos Android podem receber notificações de push imediatamente (já que ela será iniciada e registrada), enquanto os aplicativos iOS não receberão.
      * No Android, o texto do botão OK está em maiúsculas (e em qualquer outro botão adicionado na notificação no aplicativo), enquanto no iOS não está.

Para notificações por push do AMS, as notificações devem ser compostas e enviadas pelo servidor AMS. O AMS fornece recursos adicionais de notificação por push além daqueles fornecidos pelas notificações de AEM com o AWS e o Pushwoosh.

>[!NOTE]
>
>*A entrega das notificações por push não é garantida; são mais como anúncios. É feito um melhor esforço para garantir que todos ouçam, mas não são um mecanismo de entrega garantido. Além disso, o tempo para enviar uma notificação por push pode variar de menos de um segundo a até meia hora.*

### Configuração de deep linking com notificações por push {#configuring-deep-linking-with-push-notifications}

O que é Deep Linking? No contexto de uma notificação por push, é um meio de permitir que um aplicativo seja aberto ou direcionado (se aberto) para um local especificado dentro do aplicativo.

Como funciona? O autor de uma notificação por push adiciona opcionalmente um rótulo de botão (ou seja, &quot;Mostre-me!&quot;) à notificação e escolhe a página que deseja vincular na notificação, por meio de um navegador de caminho visual. Quando enviado, o push ocorre normalmente, exceto que na mensagem no aplicativo, o botão OK é substituído por um botão &quot;Dispensar&quot; e o novo botão é especificado (&quot;Mostrar-me!&quot;) também é exibido. Clicar no novo botão fará com que o aplicativo vá para a página especificada no aplicativo. Clicar em Dispensar apenas ignorará a mensagem.

Se o aplicativo não estiver aberto, a sombra aparecerá normalmente. Realizar uma ação na notificação à sombra abrirá o aplicativo e apresentará ao usuário os botões de deep link com base no que foi configurado na notificação por push.

Crie a notificação, adicione um texto de botão e um caminho de link para o deep link opcional:

>[!CAUTION]
>
>.Para acessar o bloco Notificação por push no painel, siga as etapas abaixo.

1. Clique na edição no canto superior direito do **Gerenciar Cloud Services** mosaico.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Selecione o **Conexão Pushwoosh**. Clique em **Avançar**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Insira os detalhes das propriedades e clique em **Enviar**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   Depois de enviar sua configuração, a variável **Notificações por push** é exibido no painel.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Criar assistente de notificação {#create-notification-wizard}

Uma vez **Notificações por push** bloco exibido no painel, use o assistente criar notificação para adicionar o conteúdo:

1. Clique no símbolo de adição no canto superior direito do **Notificações por push** bloco para abrir o **Criar Assistente de Notificação**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Clicar no ícone de navegação no caminho do link apresenta ao usuário a estrutura de conteúdo do aplicativo.

   Depois de selecionar o caminho, clique no ícone de verificação.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >O Texto do botão de link é limitado a 20 caracteres.
   >
   >Se o usuário final não tiver a versão mais recente do aplicativo e o caminho vinculado não estiver disponível, confirmar a ação do deep link trará o usuário para a página principal do aplicativo.

1. Insira o **Detalhes do texto** no **Criar Assistente de Notificação** e clique em **Criar**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Abra os detalhes clicando na notificação por push criada no **Notificações por push** mosaico.

   É possível editar propriedades, enviar notificações ou excluir a notificação.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Informações adicionais**:
>
>O Pushwoosh e o Amazon SNS não serão suportados após a versão 6.4 e estarão disponíveis como um complemento do compartilhamento de pacotes.

### Próximas etapas {#the-next-steps}

Assim que entender os detalhes sobre notificações por push para seu aplicativo, consulte [Personalização de conteúdo do AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md).
