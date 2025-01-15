---
title: Notificações push
description: Siga esta página para saber mais sobre como usar notificações por push em um aplicativo Adobe Experience Manager Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '3135'
ht-degree: 0%

---

# Notificações push{#push-notifications}

{{ue-over-mobile}}

Ser capaz de alertar instantaneamente seus usuários de aplicativo móvel Adobe Experience Manager (AEM) com notificações importantes é fundamental para o valor de um aplicativo móvel e suas campanhas de marketing. Aqui, as etapas são descritas para permitir que seu aplicativo receba notificações por push. Você também aprenderá a configurar e enviar mensagens de push do AEM Mobile para o aplicativo instalado no telefone. Além disso, esta seção descreve como configurar o recurso de [Deep Linking](#deeplinking) para suas notificações por push.

>[!NOTE]
>
>*A entrega das notificações por push não é garantida; elas se assemelham mais a anúncios. É feito o melhor esforço para garantir que todos os usuários os recebam, mas eles não sejam um mecanismo de entrega garantido. Além disso, o tempo para entregar um push pode variar de menos de um segundo até meia hora.*

O uso de notificações por push com AEM requer algumas tecnologias diferentes. Primeiro, um provedor de serviços de notificação por push deve ser usado para gerenciar notificações e dispositivos (o AEM ainda não faz isso). Dois provedores estão configurados com AEM: [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (ou SNS) e [Pushwoosh](https://www.pushwoosh.com/). Em segundo lugar, a tecnologia de push para determinado SO móvel deve passar pelo serviço apropriado — Serviço de notificação por push (ou APNS) da Apple para dispositivos iOS e Google Cloud Messaging (ou GCM) para dispositivos Android™. Embora o AEM não se comunique diretamente com esses serviços específicos da plataforma, algumas informações de configuração relacionadas devem ser fornecidas pelo AEM junto com as notificações para que esses serviços executem o push.

Depois de instalado e configurado (conforme explicado abaixo), ele funciona assim:

1. Uma notificação por push é criada no AEM e enviada ao provedor de serviços (Amazon SNS ou Pushwoosh).
1. O provedor de serviços o recebe e o envia para o provedor principal (APNS ou GCM).
1. O provedor principal envia a notificação para todos os dispositivos registrados para esse envio. Para cada dispositivo, ele usa a rede de dados celular ou WiFi, o que estiver disponível no dispositivo.
1. A notificação é exibida no dispositivo se o aplicativo para o qual ele está registrado não estiver em execução. Um usuário que tocar na notificação inicia o aplicativo e exibe a notificação no aplicativo. No caso de o aplicativo já estar em execução, somente a notificação no aplicativo é exibida.

Essa versão do AEM é compatível com dispositivos móveis iOS e Android™.

## Visão geral e procedimento {#overview-and-procedure}

Para usar notificações por push em um aplicativo AEM Mobile, as seguintes etapas de alto nível devem ser executadas.

Normalmente, um desenvolvedor de Experience Manager faz o seguinte:

1. Registre-se nos serviços de mensagens da Apple e da Google
1. Registrar com um serviço de mensagens por push e configurá-lo
1. Adicionar suporte de push ao aplicativo
1. Preparar um telefone para teste

Enquanto um Administrador de Experience Manager faz o seguinte:

1. Configurar push em aplicativos AEM
1. Criar e implantar o aplicativo
1. Enviar uma notificação por push
1. Configurar deep linking *(opcional)*

### Etapa 1: Registrar-se nos serviços de mensagens do Apple e Google {#step-register-with-apple-and-google-messaging-services}

#### Uso do Serviço de notificação por push da Apple (APNS) {#using-the-apple-push-notification-service-apns}

Acesse a página do Apple [aqui](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) para se familiarizar com o Serviço de Notificação por Push da Apple.

Para usar APNs, você precisa de um arquivo **Certificado** (um arquivo .cer), um push **Chave privada** (um arquivo .p12) e uma **Senha de Chave Privada** da Apple. As instruções sobre como fazer isso podem ser encontradas [aqui](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### Uso do serviço Google Cloud Messaging (GCM) {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>O Google está substituindo o GCM por um serviço semelhante chamado Firebase Cloud Messaging (FCM). Para obter mais informações sobre o FCM, clique [aqui](https://firebase.google.com/docs/cloud-messaging/).

Acesse a página do Google [aqui](https://developer.android.com/google/gcm/index.html) para se familiarizar com o Google Cloud Messaging for Android™.

[Siga estas etapas](https://developer.android.com/google/gcm/gs.html) para **Criar um projeto de API do Google**, **Habilitar o Serviço GCM** e **Obter uma Chave de API**. Você precisa da **Chave de API** para enviar notificações por push para dispositivos Android™. Além disso, registre seu **Número do Projeto**, que às vezes também é chamado de **ID de Remetente do GCM**.

As etapas a seguir mostram um método diferente de criação de chaves de API do GCM:

1. Faça logon no google e acesse a [página Desenvolvedor da Google](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. Escolha seu aplicativo na lista (ou crie um).
1. Em Nome do Pacote da Android™, digite a ID do aplicativo, ou seja, `com.adobe.cq.mobile.weretail.outdoorsapp`. (Se isso não funcionar, tente novamente com &quot;test.test&quot;.)
1. Clique em **Continuar para Escolher e configurar serviços**
1. Selecione Cloud Messaging e clique em **Habilitar o Google Cloud Messaging**.
1. A nova Chave da API do servidor e a ID do remetente (nova ou existente) serão exibidas.

>[!NOTE]
>
>Registre a chave da API do servidor. Este valor é inserido no site do seu provedor de push.

### Etapa 2: Registrar e configurar um serviço de mensagens por push {#step-register-and-configure-a-push-messaging-service}

O AEM está configurado para usar um dos três serviços para notificações por push:

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

As configurações do *Amazon SNS* e do *Pushwoosh* permitem enviar mensagens enviadas por push de dentro das telas AEM.

A configuração do *Adobe Mobile Services* permite configurar e enviar notificações por push de dentro do Adobe Mobile Services usando uma conta Adobe Analytics (mas o aplicativo deve ser criado com esse conjunto de configurações para habilitar notificações por push do AMS).

#### Uso do serviço de mensagens Amazon SNS {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Informações sobre o Amazon SNS e um link para criar uma conta do AWS podem ser encontradas [aqui](https://aws.amazon.com/sns/). Você pode obter uma conta gratuita por um ano.*

Se você não quiser usar o Amazon SNS, ignore essas etapas.

Siga estas etapas para configurar o Amazon SNS para notificações por push:

1. **Registrar-se no Amazon SNS**

   1. Registre sua ID de conta. O formato deve ser de 12 dígitos sem espaços ou traços, ou seja, &quot;123456789012&quot;.
   1. Verifique se você está na região &quot;us-east&quot; ou &quot;eu&quot;, pois uma etapa posterior (Criação do pool de identidade) exigirá uma dessas.
   1. Depois de se registrar, faça logon no console de gerenciamento e selecione [SNS](https://console.aws.amazon.com/sns/) (Serviço de Notificação por Push). Clique em &quot;Introdução&quot; se for exibido.

1. **Criar Chave e ID de Acesso**

   1. Clique no nome de login no canto superior direito da tela e escolha Credenciais de segurança no menu.
   1. Clique em Teclas de Acesso e, no espaço abaixo, clique em **Criar Nova Tecla de Acesso**.
   1. Clique em **Mostrar Chave de Acesso**, copie e salve a ID da Chave de Acesso e a Chave de Acesso Secreta exibidas. Se você escolher a opção para baixar as chaves, obterá um arquivo csv que contém esses mesmos valores.
   1. Outros certificados relacionados à segurança e alguns outros, podem ser gerenciados nesta página.

   >[!NOTE]
   >
   >Uma Chave de Acesso pode ser usada para vários aplicativos.

   Para organizações que usam uma conta &quot;AWS Sandbox&quot;, as etapas são semelhantes e descritas aqui:

   1. Clique no nome de login no canto superior direito da tela e escolha Minhas credenciais de segurança no menu.
   1. Clique em Usuários na lista de ações à esquerda e escolha seu nome de usuário.
   1. Clique na guia Credenciais de segurança.
   1. Aqui, você verá suas chaves e criará novas chaves. Salve as chaves para uso posterior.

1. **Criar um Tópico**

   1. Clique em **Criar tópico** e escolha um nome de tópico. Registre todos os campos, como Tópico ARN, Proprietário do tópico, Região, Nome de exibição.
   1. Clique em **Outras ações de tópico** > **Editar política de tópico**. Em **Permitir que esses usuários assinem este tópico**, selecione **Todos.**
   1. Clique em **Atualizar Política**.

   >[!NOTE]
   >
   >Você pode criar vários tópicos para diferentes cenários, como desenvolvimento, teste e demonstração. O restante da configuração do SNS pode permanecer o mesmo. Crie o aplicativo com um tópico diferente; as notificações por push enviadas para esse tópico serão recebidas somente pelo aplicativo criado com esse tópico.

1. **Criar Aplicativos de Plataforma**

   1. Clique em Aplicativos e, em seguida, em Criar Aplicativo de Plataforma. Escolha um nome e selecione uma plataforma (APNS para iOS, GCM para Android™). Dependendo da plataforma. outros campos devem ser preenchidos:

      1. Para APNS, um arquivo P12, uma Senha, um Certificado e uma Chave privada devem ser inseridos. Estes devem ter sido obtidos na etapa *Usando o Serviço de Notificação por Push (APNS) da Apple* acima.
      1. Para o GCM, uma chave de API deve ser inserida. Isso deveria ter sido obtido na etapa *Uso do serviço Google Cloud Messaging (GCM)* acima.

   1. Repita a etapa acima uma vez para cada plataforma que você estiver suportando. Para enviar para o iOS e o Android™, dois aplicativos de plataforma devem ser criados.

1. **Criar um Pool de Identidade**

   1. Use o [Conector](https://console.aws.amazon.com/cognito) para criar um Pool de Identidade, que armazenará dados básicos de usuários não autenticados. No momento, somente as regiões &quot;us-east&quot; e &quot;eu&quot; são compatíveis com o Amazon Cognito.
   1. Nomeie-o e marque a caixa &quot;Habilitar acesso a identidades não autenticadas&quot;.
   1. Na próxima página (&quot;*Suas identidades Cognito exigem acesso aos seus recursos*&quot;) clique em Permitir.
   1. Na parte superior direita da página, clique no link &quot;*Editar pool de identidades&quot;*. A ID do pool de identidade é exibida. Salvar este texto para mais tarde.
   1. Na mesma página, escolha a lista suspensa ao lado de &quot;Função não autenticada&quot; e verifique se ela tem a função Cognito_&lt;pool name>UnauthRole selecionada. Salve as alterações.

1. **Configurar Acesso**

   1. Faça logon no [Identity and Access Management](https://console.aws.amazon.com/iam/home) (IAM).
   1. Selecione Funções.
   1. Clique na função criada na etapa anterior, chamada Cognito_&lt;yourIdentityPoolName>Unauth_Role. Registre o &quot;Role ARN&quot; exibido.
   1. Abra &quot;Políticas em linha&quot; se ainda não estiver aberto. Você deve ver uma política com um nome como oneClick_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123.
   1. Clique em &quot;Editar política&quot;. Substitua o conteúdo do Documento de política por este trecho de JSON:

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Version": "10-17-2012",</p> <p> "Declaração": [</p> <p> {</p> <p> "Ação": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Assinar"</p> <p> ],</p> <p> "Effect": "Allow",</p> <p> "Resource": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. Clique em **Aplicar política**.

#### Uso do serviço de mensagens Pushwoosh {#using-the-pushwoosh-messaging-service}

Se você não quiser usar o Pushwoosh, ignore esta etapa.

Para usar Pushwoosh:

1. **Registrar-se no Pushwoosh**

   1. Acesse pushwoosh.com e crie uma conta.

1. **Criar um token de acesso de API**

   1. No site Pushwoosh, acesse o item de menu Acesso à API para gerar um Token de acesso à API. Grave este token com segurança.

1. **Criar um aplicativo**

   1. Para obter suporte da Android™, você deve fornecer sua chave de API GCM.
   1. Ao configurar o aplicativo, escolha Cordova como a estrutura.
   1. Para obter suporte ao iOS, você deve fornecer o arquivo de certificado (.cer), o certificado push (.p12) e a senha da chave privada; eles devem ter sido obtidos no site APNS da Apple. Para Estrutura, escolha Cordova.
   1. O Pushwoosh gerará uma ID do aplicativo para ele, no formato &quot;XXXXX-XXXXX&quot;, em que cada X é um valor hexadecimal (0 a F).

>[!NOTE]
>
>*Se um segundo aplicativo estiver configurado no AEM com a mesma ID de aplicativo (e outros valores relacionados: Token de acesso da API e ID do GCM), todas as notificações por push enviadas por meio do segundo aplicativo no AEM irão para qualquer outro aplicativo com essa ID de aplicativo.*

### Etapa 3: adicionar suporte por push ao aplicativo {#step-add-push-support-to-the-app}

#### Adicionar configuração ContentSync {#add-contentsync-configuration}

Crie dois nós de conteúdo (um no app-config e um no app-config-dev) chamados notificationsConfig:

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

Com estas propriedades (arquivos .content.xml) :
&lt;jcr:root xmlns:jcr=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns:nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot;
jcr:primaryType=&quot;nt:unstructured&quot;
excludeProperties=&quot;[appAPIAccessToken]&quot;
path=&quot;../../../..&quot;
targetRootDirectory=&quot;www&quot;
type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>O manipulador de sincronização de conteúdo procura esses nós e, se eles não estiverem lá, ele não gravará o arquivo pge-notifications-config.json.

#### Adicionar bibliotecas de clientes {#add-client-libraries}

As bibliotecas de clientes de notificação por push devem ser adicionadas ao aplicativo seguindo estas etapas:

CRXDE Lite:

1. Navegue até */etc/designs/phonegap/&lt;app name>/clientlibsall.*
1. Clique duas vezes na seção incorporada no painel de propriedades.
1. Na caixa de diálogo exibida, adicione uma biblioteca do cliente clicando no botão +.
1. No novo campo de texto, adicione &quot;cq.mobile.push&quot; e clique em OK.
1. Adicione mais um chamado cq.mobile.push.amazon e clique em OK.
1. Salve as alterações.

>[!NOTE]
>
>Se as notificações por push forem removidas ou não forem usadas, por questões de espaço no aplicativo e para evitar mensagens de erro do console, remova essas clientlibs do aplicativo.

### Etapa 4: Preparar um telefone para teste {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*Para notificações por push, você deve testar em um dispositivo real, pois os emuladores não podem receber notificações por push.*

#### IOS {#ios}

Para o iOS, use um computador macOS e participe do [iOS Developer Program](https://developer.apple.com/programs/ios/). Algumas corporações têm licenças corporativas que podem estar disponíveis para todos os desenvolvedores.

Com o XCode 8.1, antes de usar notificações por push, você deve ir para a guia Recursos em seu projeto e ativar ou desativar as notificações por push.

#### Android™ {#android}

Para instalar o aplicativo em um telefone Android™ usando a CLI (veja abaixo: **Etapa 6 - Criar e implantar o aplicativo**), primeiro coloque o telefone no &quot;modo de desenvolvedor&quot;. Consulte [Habilitando opções de desenvolvedor no dispositivo](https://developer.android.com/tools/device.html#developer-device-options) para obter detalhes sobre como fazer isso.

### Etapa 5: configurar o push em aplicativos AEM {#step-configure-push-on-aem-apps}

Antes de criar e implantar em seu dispositivo móvel configurado, você deve definir as configurações de notificação para o serviço de mensagens que decidiu usar.

1. Crie os grupos de autorização apropriados para notificações por push.
1. Faça logon no AEM como o usuário apropriado, clique na guia Aplicativos.
1. Clique no aplicativo.
1. Localize o bloco Gerenciar Cloud Service e clique no lápis para modificar as configurações de nuvem.
1. Selecione Amazon SNS Connection, Pushwoosh Connection ou Adobe Mobile Services, como a configuração de notificação.
1. Insira as propriedades do provedor e clique em Enviar para salvá-las e em Concluído. Eles não são verificados remotamente nesse estágio, exceto se houver AMS.
1. Agora você deve ver a configuração inserida no bloco Gerenciar Cloud Service.

### Etapa 6: criar e implantar o aplicativo {#step-build-and-deploy-the-app}

**Observação:** veja as instruções [aqui](/help/mobile/building-app-mobile-phonegap.md) sobre como criar aplicativos PhoneGap.

Há duas maneiras de criar e implantar seu aplicativo usando o PhoneGap.

**Observação:** para testes de notificação por push, os emuladores não serão suficientes porque as notificações por push usam um protocolo distinto entre o provedor de push (Apple ou Google) e o dispositivo. Os emuladores e o hardware atuais do Mac/PC não suportam esse recurso.

1. O *PhoneGap Build* é um serviço oferecido pelo PhoneGap que criará seu aplicativo nos servidores deles e permitirá que você o baixe diretamente no seu dispositivo. Consulte a documentação de PhoneGap Build em `https://build.phonegap.com/` para saber como configurar e usar o PhoneGap Build.

1. A *Interface de Linha de Comando do PhoneGap* (CLI) permite usar um conjunto avançado de comandos do PhoneGap na linha de comando para compilar, depurar e implantar seu aplicativo. Consulte a documentação do desenvolvedor do PhoneGap (`https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface`) para saber como configurar e usar a CLI do PhoneGap.

### Etapa 7: enviar uma notificação por push {#step-send-a-push-notification}

Para criar uma notificação e enviá-la, siga estas etapas.

1. Criar uma notificação

   * No painel do aplicativo AEM Mobile, localize o bloco Notificações por push.
   * No menu no canto superior direito, escolha &quot;Criar&quot;. Esse botão não estará disponível até que a configuração na nuvem seja definida pela primeira vez.
   * No Assistente de criação de notificações, digite um título e uma mensagem e clique no botão &quot;Criar&quot;. Sua notificação agora está pronta para ser enviada imediatamente ou mais tarde. Ele pode ser editado e a mensagem e/ou o título podem ser alterados e salvos.

1. Enviar a notificação

   * No painel Aplicativos, localize o bloco Notificações por push.
   * Selecione a notificação ou clique no botão de detalhes na parte inferior direita (. . .), para mostrar a lista de notificações. Essa lista também indica se uma notificação está pronta para ser enviada, se já foi enviada ou se ocorreu um erro durante o envio.
   * Marque a caixa de seleção de uma notificação (apenas) e clique no botão &quot;Enviar notificação&quot; acima da lista. Você tem uma chance de &quot;Cancelar&quot; ou &quot;Enviar&quot; a notificação na caixa de diálogo exibida.

1. Tratamento dos resultados

   * Se o serviço de notificação por push (Amazon SNS ou Pushwoosh) receber a solicitação de envio, confirmá-la como válida e enviá-la aos provedores nativos (APNS e GCM) com êxito, a caixa de diálogo de envio será fechada sem nenhuma mensagem. Na lista de notificações, o status dessa notificação é listado como Enviado.
   * Se o envio por push falhar, a caixa de diálogo mostrará uma mensagem indicando o problema. Na lista de notificações, o status dessa notificação é listado como Erro, mas se o problema for retificado, a notificação poderá ser enviada novamente. Se houver um erro, informações adicionais sobre o erro deverão aparecer no log de erros do servidor.
   * Observe que há algumas diferenças de plataforma entre as notificações por push do iOS e do Android™. Entre eles:

      * A compilação com CLI iniciará o aplicativo após a implantação no Android™. No iOS, é necessário iniciá-lo manualmente. Como a etapa de registro por push ocorre na inicialização, os aplicativos Android™ podem receber notificações por push imediatamente (porque já foram iniciados e registrados), enquanto os aplicativos iOS não podem.
      * No Android™, o texto do botão OK está em maiúsculas (e em qualquer outro botão adicionado à notificação no aplicativo), enquanto no iOS não está.

Para notificações por push do AMS, as notificações devem ser compostas e enviadas do servidor AMS. O AMS fornece recursos adicionais de notificação por push além daqueles fornecidos pelas notificações do AEM com o AWS e o Pushwoosh.

>[!NOTE]
>
>*A entrega das notificações por push não é garantida; elas se assemelham mais a anúncios. É feito o melhor esforço para garantir que todos ouçam, mas eles não sejam um mecanismo de entrega garantido. Além disso, o tempo para entregar um push pode variar de menos de um segundo até meia hora.*

### Configuração de deep linking com notificações por push {#configuring-deep-linking-with-push-notifications}

O que é Deep Linking? No contexto de uma notificação por push, é um meio de permitir que um aplicativo seja aberto ou direcionado (se estiver aberto) para um local especificado dentro do aplicativo.

Como funciona? O autor de uma notificação por push adiciona opcionalmente um rótulo de botão (ou seja, &quot;Mostre-me!&quot;) à notificação e escolhe a página que gostaria de vincular na notificação, por meio de um navegador de caminho visual. Quando enviado, o push ocorre normalmente, exceto que na mensagem no aplicativo, o botão OK é substituído por um botão &quot;Dispensar&quot; e o novo botão é especificado (&quot;Mostrar-me!&quot;) também é exibida. Clicar no botão new faz com que o aplicativo vá para a página especificada no aplicativo. Clicar em Dispensar elimina a mensagem.

Se o aplicativo não estiver aberto, a sombra será exibida normalmente. Realizar uma ação na notificação na sombra abre o aplicativo e, em seguida, apresenta ao usuário os botões de deep link com base no que foi configurado na notificação por push.

Crie a notificação, adicione um texto de botão e um caminho de link para o deep link opcional:

>[!CAUTION]
>
>Para acessar o bloco Notificações por push no painel, siga as etapas abaixo.

1. Clique na edição no canto superior direito do bloco **Gerenciar Cloud Service**.

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. Selecione a **Conexão Pushwoosh**. Clique em **Avançar**.

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. Insira os detalhes das propriedades e clique em **Enviar**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   Depois de enviar a configuração, o bloco **Notificações por push** será exibido no painel.

   ![chlimage_1-111](assets/chlimage_1-111.png)

### Criar assistente de notificação {#create-notification-wizard}

Depois que o bloco **Notificações por push** for exibido no painel, use o assistente de criação de notificações para adicionar o conteúdo:

1. Clique no símbolo de adição no canto superior direito do bloco **Notificações por push** para abrir o **Assistente de Criação de Notificações**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. Clicar no ícone de navegação no caminho do link apresenta ao usuário a estrutura de conteúdo do aplicativo.

   Depois de selecionar o caminho, clique no ícone de verificação.

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >O texto do botão Link é limitado a 20 caracteres.
   >
   >Se o usuário final não tiver a versão mais recente do aplicativo e o caminho vinculado não estiver disponível, confirmar a ação do deep link levará o usuário para a página principal do aplicativo.

1. Insira os **Detalhes do Texto** no **Assistente de Criação de Notificações** e clique em **Criar**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   Abra os detalhes clicando na notificação por push criada a partir do bloco **Notificações por push**.

   Você pode editar propriedades, enviar notificações ou excluir a notificação.

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**Informações Adicionais**:
>
>O Pushwoosh e o Amazon SNS não serão compatíveis após a versão 6.4 e estarão disponíveis como um complemento do Compartilhamento de pacotes.

### Próximas etapas {#the-next-steps}

Assim que você entender os detalhes sobre notificações por push para seu aplicativo, consulte [AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).
