---
title: Gerenciar ativos de vídeo
description: Fazer upload, visualizar, anotar e publicar ativos de vídeo em [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '5499'
ht-degree: 8%

---

# Gerenciar ativos de vídeo {#manage-video-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. [!DNL Adobe Experience Manager] O oferece ofertas e recursos maduros para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo em [!DNL Adobe Experience Manager Assets]. A codificação e a transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando [!DNL Dynamic Media] integração.

## Fazer upload e visualizar ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera visualizações para ativos de vídeo com a extensão MP4. Se o formato do ativo não for MP4, instale o FFmpeg pack para gerar uma pré-visualização. FFmpeg cria representações de vídeo do tipo OGG e MP4. Você pode visualizar as representações no [!DNL Assets] interface do usuário.

1. Na pasta ou nas subpastas de ativos digitais, navegue até o local onde deseja adicionar ativos digitais.
1. Para fazer upload do ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo na interface do usuário do . Consulte [fazer upload de ativos](manage-assets.md#uploading-assets) para obter detalhes.
1. Para visualizar um vídeo na exibição de Cartão, clique no botão **[!UICONTROL Reproduzir]** ![opção de reprodução](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo somente na exibição de cartão. O [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na exibição de lista.

1. Para visualizar o vídeo na página de detalhes do ativo, clique em **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no player de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela cheia.

   ![Controles de reprodução de vídeo](assets/video-playback-controls.png)

## Configuração para fazer upload de ativos com mais de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Por padrão, [!DNL Assets] O não permite fazer upload de ativos com mais de 2 GB por causa de um limite de tamanho de arquivo. No entanto, é possível substituir esse limite indo até o CRXDE Lite e criando um nó sob o `/apps` diretório. O nó deve ter o mesmo nome de nó, estrutura de diretório e propriedades de nó comparáveis da ordem.

Além de [!DNL Assets] altere as seguintes configurações para fazer upload de ativos grandes:

* Aumente o tempo de expiração do token. Consulte [!UICONTROL Servlet CSRF do Adobe Granite] no Console da Web em `https://[aem_server]:[port]/system/console/configMgr`. Para obter mais informações, consulte [Proteção CSRF](/help/sites-developing/csrf-protection.md).
* Aumente o `receiveTimeout` na configuração do Dispatcher. Para obter mais informações, consulte [Configuração do Dispatcher do Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#renders-options).

>[!NOTE]
>
>O [!DNL Experience Manager] A interface de usuário clássica não tem uma restrição de limite de tamanho de arquivo de 2 GB. Além disso, o fluxo de trabalho completo para vídeo grande não é totalmente compatível.

Para configurar um limite de tamanho de arquivo mais alto, execute as seguintes etapas no `/apps` diretório.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No CRXDE Lite, navegue até `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver a janela do diretório, clique no botão `>>`.
1. Na barra de ferramentas, clique no botão **[!UICONTROL Nó de sobreposição]**. Como alternativa, selecione **[!UICONTROL Sobrepor nó]** no menu de contexto.
1. No **[!UICONTROL Nó de sobreposição]** , clique em **[!UICONTROL OK]**.

   ![Nó de sobreposição](assets/overlay-node-path.png)

1. Atualize o navegador. O nó de sobreposição `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está selecionada.
1. No **[!UICONTROL Propriedades]** , insira o valor apropriado em bytes para aumentar o limite de tamanho para o tamanho desejado. Por exemplo, para aumentar o limite de tamanho para 30 GB, insira `32212254720` valor.

1. Na barra de ferramentas, clique em **[!UICONTROL Salvar tudo]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. No [!DNL Adobe Experience Manager] [!UICONTROL Pacotes do Console da Web] na coluna Nome da tabela, localize e clique em **[!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite]**.
1. No [!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite] , defina os segundos para ambos **[!UICONTROL Tempo limite padrão]** e **[!UICONTROL Tempo limite máximo]** campos para `18000` (cinco horas). Clique em **[!UICONTROL Salvar]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho , selecione **[!UICONTROL Codificar vídeo no Dynamic Media]**, depois clique em **[!UICONTROL Editar]**.
1. Na página do fluxo de trabalho , clique duas vezes no botão **[!UICONTROL Processo de serviço de vídeo do Dynamic Media]** componente.
1. Na caixa de diálogo [!UICONTROL Propriedades da etapa], na guia **[!UICONTROL Comum]**, expanda **Configurações avançadas**.
1. No **[!UICONTROL Tempo limite]** , especifique um valor de `18000`, depois clique em **[!UICONTROL OK]** para retornar ao **[!UICONTROL Codificar vídeo no Dynamic Media]** página do fluxo de trabalho.
1. Próximo à parte superior da página, abaixo do [!UICONTROL Codificar vídeo no Dynamic Media] título da página, clique em **[!UICONTROL Salvar]**.

## Publicar ativos de vídeo {#publish-video-assets}

Após a publicação, é possível incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar ativos do Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Publicar vídeos no YouTube {#publishing-videos-to-youtube}

Você pode publicar ativos de vídeo no local Experience Manager diretamente em um canal YouTube criado anteriormente.

Para publicar ativos de vídeo no YouTube, configure o Experience Manager Assets com tags. Você associa essas tags a um canal YouTube. Se a tag de um ativo de vídeo corresponder à tag de um canal de YouTube, o vídeo será publicado no YouTube. Publicar no YouTube ocorre junto com uma publicação normal do vídeo, desde que uma tag associada seja usada.

O YouTube faz sua própria codificação. Dessa forma, o arquivo de vídeo original que foi carregado no Experience Manager é publicado no YouTube em vez de qualquer representação de vídeo criada pela codificação do Dynamic Media. Embora não seja necessário processar vídeos usando o Dynamic Media, espera-se que eles o façam caso uma predefinição do visualizador seja necessária para reprodução.

Ao ignorar o perfil de processamento de vídeo e publicar diretamente no YouTube, isso significa apenas que o ativo de vídeo no Experience Manager Asset não obtém uma miniatura visualizável. Isso também significa que se você executar o `dynamicmedia` ou `dynamicmedia_scene7` modos de execução, vídeos que não são codificados não funcionam com nenhum dos tipos de ativos do Dynamic Media.

A publicação de ativos de vídeo em servidores da YouTube envolve a conclusão das seguintes tarefas para garantir a autenticação segura de servidor para servidor com o YouTube:

1. [Definir as configurações da Google Cloud](#configuring-google-cloud-settings)
1. [Criar um canal YouTube](#creating-a-youtube-channel)
1. [Adicionar tags para publicação](#adding-tags-for-publishing)
1. [Ativar o agente YouTube Publish Replication](#enabling-the-youtube-publish-replication-agent)
1. [Configurar YouTube no Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatize a configuração das propriedades padrão do YouTube para seus vídeos carregados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Publicar vídeos no seu canal do YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verificar o vídeo publicado no YouTube](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincular URLs do YouTube à sua aplicação web](#linking-youtube-urls-to-your-web-application)

Você também pode [cancelar a publicação de vídeos para removê-los do YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Definir as configurações da Google Cloud {#configuring-google-cloud-settings}

Para publicar no YouTube, você precisa de uma conta do Google. Se tiver uma conta GMAIL, você já terá uma conta Google; se você não tiver uma conta do Google, poderá criar uma facilmente. Você precisa da conta, pois precisa de credenciais para publicar ativos de vídeo no YouTube. Se você já tiver uma conta criada, ignore esta tarefa e prossiga diretamente para [Criar um canal YouTube](#creating-a-youtube-channel).

A conta usada com a Google Cloud e a conta da Google usada para o YouTube não precisam ser a mesma.

O Google altera periodicamente sua interface do usuário. Dessa forma, as etapas para publicar vídeos no YouTube podem variar um pouco do que está documentado abaixo. Esse aviso também se aplica ao YouTube quando você tenta verificar se os vídeos foram carregados nele.

>[!NOTE]
>
>As etapas a seguir foram precisas no momento da escrita. No entanto, o Google atualiza periodicamente seus sites sem aviso prévio. Dessa forma, essas etapas podem ser um pouco diferentes.

Para definir as configurações da Google Cloud:

1. Crie uma conta do Google.
   [https://accounts.google.com/SignUp?service=mail](https://accounts.google.com/SignUp?service=mail)

   Se você já tiver uma conta do Google, pule para a próxima etapa.

1. Ir para [https://cloud.google.com/](https://cloud.google.com/).
1. Na página do Google Cloud, próximo ao canto superior direito, clique em **[!UICONTROL Console]**.

   Se necessário, **[!UICONTROL Fazer logon]** usando as credenciais da conta do Google para visualizar o **[!UICONTROL Console]** opção.

1. Na página Painel , à direita de **[!UICONTROL Google Cloud Platform]**, clique na lista suspensa Projeto para abrir a caixa de diálogo Selecionar um projeto .
1. Na caixa de diálogo Selecionar um projeto, toque em **[!UICONTROL Novo projeto]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. Na caixa de diálogo Novo projeto , no campo Nome do projeto , digite o nome do novo projeto.

   A ID do projeto é baseada no nome do projeto. Como tal, escolha cuidadosamente o nome do projeto; ele não pode ser alterado após ser criado. Além disso, você deve inserir a mesma ID de projeto novamente ao configurar o YouTube no Experience Manager posteriormente; considere anotá-lo.

1. Clique em **[!UICONTROL Criar]**.

1. Siga um destes procedimentos:

   * No Painel do projeto, no cartão Introdução , toque em **[!UICONTROL Explorar e ativar APIs]**.
   * No Painel do projeto, no cartão APIs , toque em **[!UICONTROL Visão geral das APIs]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. Próximo à parte superior da página APIs e serviços, toque em **[!UICONTROL Ativar APIs e serviços]**.
1. Na página Biblioteca de API, no lado esquerdo, em **[!UICONTROL Categoria]**, toque em **[!UICONTROL YouTube]**. No lado direito da página, toque em **[!UICONTROL API de dados do YouTube]**.
1. Na página da API de dados do YouTube v3, toque em **[!UICONTROL Habilitar]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Para usar a API, você precisa de credenciais. Se necessário, clique em **[!UICONTROL Criar credenciais]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. No **[!UICONTROL Adicionar credenciais ao projeto]** na página, etapa 1, faça o seguinte:

   * No **[!UICONTROL Qual API você está usando?]** , selecione **[!UICONTROL API de dados do YouTube v3]**.

   * No **[!UICONTROL De onde você está chamando a API?]** , selecione **[!UICONTROL Servidor da Web (por exemplo, node.js, Tomcat)]**

   * No **[!UICONTROL Que dados você está acessando?]** lista suspensa, toque em **[!UICONTROL Dados do usuário]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Toque **[!UICONTROL Quais credenciais são necessárias?]**
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 2, no cabeçalho **[!UICONTROL Criar uma ID de cliente do OAuth 2.0]**, no campo Nome, digite um nome exclusivo, se desejar. Ou você pode usar o nome padrão especificado pelo Google.
1. Em **[!UICONTROL Origens JavaScript autorizadas]** no campo de texto, digite o seguinte caminho, substituindo seu próprio domínio e número da porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>`

   Por exemplo, `https://1a2b3c.mycompany.com:4321`

   **Observação**: O exemplo de caminho acima destina-se somente a fins de demonstração.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. Em **[!UICONTROL URIs de redirecionamento autorizados]** no campo de texto, digite o seguinte caminho, substituindo seu próprio domínio e número da porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por exemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **Observação**: O exemplo de caminho acima destina-se somente a fins de demonstração.

1. Clique em **[!UICONTROL Criar ID de cliente OAuth]**.
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 3, no cabeçalho **[!UICONTROL Configurar a tela de consentimento do OAuth 2.0]**, selecione o endereço de email do Gmail que você está usando no momento.

   ![6_5_googleaccount-apis-createcredentials-consent-tela de consentimento](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. Em **[!UICONTROL Nome do produto exibido aos usuários]** , no campo de texto, digite o que deseja mostrar na tela de consentimento.

   A tela de consentimento é exibida para o administrador do Experience Manager quando eles são autenticados para o YouTube; O Experience Manager entra em contato com a YouTube para obter permissão.

1. Clique em **[!UICONTROL Continuar]**.
1. Na página Adicionar credenciais ao projeto, etapa 4, no cabeçalho **[!UICONTROL Baixar credenciais]**, toque em **[!UICONTROL Download]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Salve as `client_id.json` arquivo.

   Esse arquivo json é necessário quando você configura o YouTube no Adobe Experience Manager posteriormente.

1. Clique em **[!UICONTROL Concluído]**.

   Faça logoff de sua conta do Google. Agora crie um canal YouTube.

### Criar um canal YouTube {#creating-a-youtube-channel}

A publicação de vídeos no YouTube requer um ou mais canais. Caso já tenha criado um canal YouTube, ignore esta tarefa e vá para [Adicionar tags para publicação](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>Certifique-se de que você já configurou um ou mais canais no YouTube *before* você adiciona canais em Configurações do YouTube no Experience Manager (consulte [Configurar YouTube no Experience Manager](#setting-up-youtube-in-aem) abaixo). Se não conseguir configurar um ou mais canais, você não será avisado de canais inexistentes. No entanto, a autenticação da Google ainda ocorre ao adicionar um canal, mas não há uma opção para escolher qual canal o vídeo será enviado.

**Para criar um canal YouTube:**

1. Ir para [https://www.youtube.com](https://www.youtube.com/) e faça logon usando suas credenciais de conta do Google.
1. No canto superior direito da página do YouTube, clique na imagem do perfil (também pode aparecer como uma letra dentro de um círculo colorido sólido) e clique em **[!UICONTROL Configurações do YouTube]** (ícone de engrenagem arredondada).
1. Na página Visão geral , no cabeçalho Recursos adicionais, clique em **[!UICONTROL Ver todos os meus canais ou criar um canal]**.
1. Na página Canais , clique em **[!UICONTROL Criar um novo canal]**.
1. Na página Conta de marca , no campo Nome da conta de marca , digite um nome de empresa ou qualquer outro nome de canal que você escolher onde deseja publicar seus ativos de vídeo e, em seguida, clique em **[!UICONTROL Criar]**.

   Lembre-se do nome inserido aqui, pois é necessário inseri-lo novamente ao configurar o YouTube no Experience Manager.

1. (Opcional) Se necessário, adicione mais canais.

   Agora, adicione tags para publicação.

### Adicionar tags para publicação {#adding-tags-for-publishing}

Para publicar seus vídeos no YouTube, o Experience Manager associa as tags a um ou mais canais do YouTube. Para adicionar tags para publicação, consulte [Administrar tags](/help/sites-administering/tags.md).

Ou, se você pretende usar as tags padrão no Experience Manager, pode ignorar esta tarefa e acessar [Ativar o agente de replicação do YouTube Publish](#enabling-the-youtube-publish-replication-agent).

### Ativar o agente de replicação do YouTube Publish {#enabling-the-youtube-publish-replication-agent}

Depois de ativar o agente de replicação do YouTube Publish , se quiser testar a conexão com a conta do Google Cloud, toque em **[!UICONTROL Testar conexão]**. Uma guia do navegador exibe os resultados da conexão. Se você tiver adicionado os Canais do YouTube, uma lista deles será exibida como parte do teste.

1. No canto superior esquerdo do Experience Manager, clique no logotipo do Experience Manager e, em seguida, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no autor]**.
1. Na página Agentes do autor , clique em **[!UICONTROL Publicação no YouTube]**.
1. Na barra de ferramentas, à direita de Configurações, clique em **[!UICONTROL Editar]**.
1. Selecione o **[!UICONTROL Ativado]** caixa de seleção para que você possa ativar o agente de replicação.
1. Clique em **[!UICONTROL OK]**.

   Agora, configure o YouTube no Experience Manager.

### Configurar YouTube no Experience Manager {#setting-up-youtube-in-aem}

A partir do Experience Manager 6.4, um novo método de interface de toque foi introduzido para configurar a publicação do YouTube no Experience Manager. Com base na instância instalada do Experience Manager que você está usando, execute um dos seguintes procedimentos:

* Para configurar o YouTube no Experience Manager antes da versão 6.4, consulte [Configurar o YouTube no Experience Manager antes da versão 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Para configurar o YouTube no Experience Manager 6.4 ou posterior, consulte [Configure o YouTube no Experience Manager 6.4 e posterior](#setting-up-youtube-in-aem-and-later).

#### Configure o YouTube no Experience Manager 6.4 e posterior {#setting-up-youtube-in-aem-and-later}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.
1. No canto superior esquerdo, toque no logotipo Experience Manager e, em seguida, no painel à esquerda, toque em **[!UICONTROL Ferramentas]**(ícone de martelo) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração de publicação do YouTube]**.
1. Toque **[!UICONTROL global]** (não selecione).

1. Próximo ao canto superior direito da página global, toque em **[!UICONTROL Criar]**.
1. Na página Criar configuração do YouTube, em Configurações da Google Cloud Platform, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto quando definiu as configurações da Google Cloud anteriormente.
Deixe a página Criar configuração do YouTube aberta; dentro de instantes, você voltará a ela.

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa [Definir as configurações da Google Cloud](/help/assets/video.md#configuring-google-cloud-settings).
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Salvar]**.

   Agora, configure os canais YouTube no Experience Manager.

1. Toque **[!UICONTROL Adicionar canal]**.
1. No campo Nome do canal , digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Toque **[!UICONTROL Adicionar]**.
1. Autenticação YouTube/Google é exibida. Se você ainda não estiver conectado à conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, toque em **[!UICONTROL Aceitar]** para permitir o acesso a este canal.

1. Toque **[!UICONTROL Permitir]**.

   Agora, configure as tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]** - Na página Cloud Services > YouTube , toque no ícone de lápis para editar a lista de tags que deseja usar.
1. Toque no ícone da lista suspensa (sinal de interpolação) para exibir a lista de tags disponíveis no Experience Manager.
1. Toque em uma ou mais tags para adicioná-las.

   Para excluir uma tag adicionada, selecione-a e toque em **[!UICONTROL X]**.

1. Quando terminar de adicionar as tags desejadas, toque em **[!UICONTROL Salvar]**.

   Agora você publica vídeos no seu canal do YouTube.

#### Configurar o YouTube no Experience Manager antes da versão 6.4 {#setting-up-youtube-in-aem-before}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como um administrador.

1. No canto superior esquerdo, toque no logotipo Experience Manager e, em seguida, no painel à esquerda, toque em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Services]**.
1. No cabeçalho Serviços de terceiros , em YouTube, toque em **[!UICONTROL Configurar agora]**.
1. Na caixa de diálogo Criar configuração , digite um título (obrigatório) e um nome (opcional) nos respectivos campos.
1. Toque **[!UICONTROL Criar]**.
1. Na caixa de diálogo Configurações da conta do YouTube, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao iniciar [configurações da Google Cloud](/help/assets/video.md#configuring-google-cloud-settings) anteriormente.
Deixe a caixa de diálogo Configuração da conta do YouTube aberta; você vai voltar a ela daqui a pouco.

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa Configuração das configurações da Google Cloud.
1. Selecione e copie o texto JSON inteiro.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Toque **[!UICONTROL OK]**.

   Agora, configure os canais YouTube no Experience Manager.

1. À direita de **[!UICONTROL Canais disponíveis]**, toque em **+** (ícone de adição).
1. Na caixa de diálogo Configurações do canal do YouTube, no campo Título, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejar.

1. Toque **[!UICONTROL OK]**.
1. Autenticação YouTube/Google é exibida. Se você ainda não estiver conectado à conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem para ver dois ou mais itens. Selecione um canal. Não selecionar o endereço de correio eletrônico; não é um canal.
   * Na próxima página, toque em **[!UICONTROL Aceitar]** para permitir o acesso a este canal.

1. Toque **[!UICONTROL Permitir]**.

   Agora, configure as tags para publicação.

1. **[!UICONTROL Configuração de tags para publicação]** - Na página Cloud Services > YouTube , toque no ícone de lápis para editar a lista de tags que deseja usar.
1. Toque no ícone da lista suspensa (sinal de interpolação) para exibir a lista de tags disponíveis no Experience Manager.
1. Toque em uma ou mais tags para adicioná-las.

   Para excluir uma tag adicionada, selecione-a e toque em **X**.

1. Quando terminar de adicionar as tags desejadas, toque em **[!UICONTROL OK]**.

   Agora você publica vídeos no seu canal do YouTube.

### (Opcional) Automatize a configuração das propriedades padrão do YouTube para seus vídeos carregados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Opcionalmente, é possível automatizar a configuração das propriedades do YouTube ao fazer upload dos vídeos, criando um perfil de processamento de metadados no Experience Manager.

Para criar o perfil de processamento de metadados, você primeiro copiará valores dos campos **[!UICONTROL Rótulo do campo]**, **[!UICONTROL Mapear para a propriedade]** e **[!UICONTROL Opções]**, todos encontrados nos Esquemas de metadados do vídeo. Em seguida, crie seu perfil de processamento de metadados de vídeo do YouTube adicionando esses valores a ele.

Para automatizar a configuração das propriedades padrão do YouTube para os vídeos carregados:

1. No canto superior esquerdo, toque no logotipo Experience Manager e, em seguida, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Esquemas de metadados]**.
1. Clique em **[!UICONTROL default]**. (Não adicione uma marca de seleção à caixa de seleção à esquerda de &quot;padrão&quot;.)
1. No **[!UICONTROL default]** marque a caixa à esquerda de **[!UICONTROL vídeo]** e toque em **[!UICONTROL Editar]**.
1. Na página Editor de esquema de metadados , toque no **[!UICONTROL Avançado]** guia .
1. No cabeçalho Publicação no YouTube, clique em **[!UICONTROL Categoria do YouTube]**.
1. No lado direito da página, em **[!UICONTROL Configurações]** , faça o seguinte:

   * No **[!UICONTROL Mapear para propriedade]** , selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar (como People &amp; Blogs ou Science &amp; Technology).
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. No cabeçalho Publicação no YouTube, toque em **[!UICONTROL Privacidade da YouTube]**.
1. No lado direito da página, em **[!UICONTROL Configurações]** , faça o seguinte:

   * No **[!UICONTROL Mapear para propriedade]** , selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar. Observe que as Opções são agrupadas em pares de dois. O campo inferior do par é o valor padrão que você deseja copiar, como público, não listado ou privado.
Cole o valor copiado no editor de texto aberto. Você precisará desse valor posteriormente ao criar seu perfil de processamento de metadados. Deixe o editor de texto aberto.

1. Próximo ao canto superior direito da página Editor de esquema de metadados, clique em **[!UICONTROL Cancelar]**.
1. No canto superior esquerdo do Experience Manager, toque no logotipo do Experience Manager e, em seguida, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de metadados]**.

1. Na página Perfis de metadados , próximo ao canto superior direito da página, clique em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Adicionar perfil de metadados, no campo de texto **[!UICONTROL Título do perfil]**, digite o nome `YouTube Video` e clique em **[!UICONTROL Criar]**.
1. Na página Editor de perfil de metadados , clique no **[!UICONTROL Avanço]** guia .
1. Adicione os valores copiados de Publicação no YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, clique no botão **[!UICONTROL Criar formulário]** guia .
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** à esquerda e solte-a na área do formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Publishing`.
   * Clique no botão **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do **[!UICONTROL Publicação no YouTube]** cabeçalho criado por você.

   * Clique em **[!UICONTROL Rótulo do campo]** assim, o componente é selecionado.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Adicione os valores copiados da Privacidade do YouTube ao perfil, fazendo o seguinte:

   * No lado direito da página, clique no botão **[!UICONTROL Criar formulário]** guia .
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** à esquerda e solte-a na área do formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações , no campo de texto Rótulo do campo , digite `YouTube Privacy`.
   * Clique no botão **[!UICONTROL Criar formulário]** e arraste o componente rotulado **[!UICONTROL Texto de vários valores]** e solte-o abaixo do **[!UICONTROL Privacidade da YouTube]** cabeçalho criado por você.

   * Clique em **[!UICONTROL Rótulo do campo]** assim, o componente é selecionado.
   * No lado direito da página, na guia Configurações , cole os valores de Publicação do YouTube (valor do Rótulo do campo e Mapear para o valor da propriedade) que você copiou anteriormente, em seus respectivos campos no formulário. Cole o valor Choices no campo Default Value .

1. Ao lado do canto superior direito da página, clique em **[!UICONTROL Salvar]**.
1. Aplique o perfil de metadados de Publicação do YouTube às pastas onde você fará upload de vídeos. Você deve ter o Perfil de metadados e o Perfil de vídeo definidos.

   Consulte [Perfis de metadados](/help/assets/metadata-config.md#metadata-profiles) e [Perfis de vídeo](/help/assets/video-profiles.md).

### Publicar vídeos no seu canal do YouTube {#publishing-videos-to-your-youtube-channel}

Agora, associe as tags adicionadas anteriormente aos ativos de vídeo. Esse processo permite que o Experience Manager saiba quais ativos serão publicados no canal do YouTube.

>[!NOTE]
>
>Ao executar o no modo Dynamic Media - Scene7, a publicação imediata não é publicada automaticamente no YouTube. Quando o modo Dynamic Media - Scene7 estiver configurado, há duas opções de publicação para escolher: **[!UICONTROL Imediatamente]** ou **[!UICONTROL Após ativação]**.
>
>**[!UICONTROL Publicar imediatamente]** significa que o ativo carregado — depois de sincronizado com o IPS — é publicado automaticamente no sistema de delivery. Embora isso seja verdade para o Dynamic Media, não é verdadeiro para o YouTube. Para publicar no YouTube, você deve publicar por meio do Experience Manager Author.

>[!NOTE]
>
>Para publicar conteúdo do YouTube, o Experience Manager usa a variável **[!UICONTROL Publicar no YouTube]** , que permite monitorar o progresso e exibir as informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obter informações de progresso mais detalhadas, você pode monitorar o log do YouTube em replicação. Esteja ciente, no entanto, de que esse monitoramento requer acesso de administrador.

**Para publicar vídeos no seu canal do YouTube:**

1. No Experience Manager, navegue até um ativo de vídeo que deseja publicar no canal do YouTube.
1. Selecione o ativo de vídeo (o conjunto de vídeos adaptáveis).
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Na guia Básico , abaixo do cabeçalho Metadados , clique em **[!UICONTROL Abrir caixa de diálogo de seleção]** à direita do campo Tags .
1. Na página Selecionar tags , navegue até as tags que deseja usar e selecione uma ou mais tags.

   Lembre-se de que as tags devem ser associadas ao canal do YouTube.

1. No canto superior direito da página, clique em **[!UICONTROL Selecionar]**.
1. No canto superior direito da página de propriedades do vídeo, clique em **[!UICONTROL Salvar e fechar]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Publicação rápida]**.

   Consulte também [Uso do Gerenciamento de publicação com o Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html).

   Opcionalmente, é possível verificar o vídeo publicado no canal do YouTube.

### (Opcional) Verificar o vídeo publicado no YouTube {#optional-verifying-the-published-video-on-youtube}

Opcionalmente, é possível monitorar o progresso da publicação (ou desfazer a publicação) do YouTube.

Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Os tempos de publicação podem variar bastante, dependendo de vários fatores que incluem o formato do vídeo de origem primária, o tamanho do arquivo e o tráfego de upload. O processo de publicação pode levar de alguns minutos a várias horas. Além disso, os formatos de resolução mais alta são renderizados muito mais lentamente. Por exemplo, 720p e 1080p levam mais tempo para serem exibidas do que 480p.

Após oito horas, se você ainda vir uma mensagem de status que diz **[!UICONTROL Carregado (processando, aguarde)]**, tente remover o vídeo do site do Adobe e carregá-lo novamente.

### Vincular URLs do YouTube ao aplicativo da Web {#linking-youtube-urls-to-your-web-application}

Você pode obter uma string de URL do YouTube gerada pelo Dynamic Media após publicar o vídeo. Ao copiar o URL do YouTube, ele chega à Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL do YouTube não está disponível para cópia até que você tenha publicado o ativo de vídeo no YouTube.

**Para vincular URLs do YouTube ao seu aplicativo da Web:**

1. Navegue até o *YouTube publicado* ativo de vídeo cujo URL você deseja copiar e, em seguida, selecioná-lo.

   Lembre-se de que os URLs do YouTube só estão disponíveis para cópia *after* você tem primeiro *publicado* os ativos de vídeo para a YouTube.

1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Clique no botão **[!UICONTROL Avançado]** guia .
1. No cabeçalho Publicação do YouTube, na Lista de URLs do YouTube, selecione e copie o texto do URL para o navegador da Web para visualizar o ativo ou adicionar à página de conteúdo da Web.

### Cancelar a publicação de vídeos para que você possa removê-los do YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Ao cancelar a publicação de um ativo de vídeo no Experience Manager, o vídeo é removido do YouTube.

>[!CAUTION]
>
>Se você remover um vídeo diretamente do YouTube, o Experience Manager não estará ciente e continuará a se comportar como se o vídeo ainda estivesse publicado no YouTube. Sempre desfaça a publicação de um ativo de vídeo do YouTube por meio do Experience Manager.

>[!NOTE]
>
>Para remover o conteúdo do YouTube, o Experience Manager usa a variável **[!UICONTROL Cancelar publicação do YouTube]** , que permite monitorar o progresso e exibir as informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para cancelar a publicação de vídeos para removê-los do YouTube:**

1. Navegue até os ativos de vídeo que você deseja cancelar a publicação por meio do canal do YouTube.
1. Em um modo de seleção de ativo, selecione um ou mais ativos de vídeo publicados.
1. Na barra de ferramentas, clique em **[!UICONTROL Gerenciar publicação]**. Toque no ícone de três pontos (. . .) na barra de ferramentas para **[!UICONTROL Gerenciar publicação]** é aberto.
1. Na página Gerenciar publicação , toque em **[!UICONTROL Cancelar publicação]**.
1. No canto superior direito da página, toque em **[!UICONTROL Próximo]**.
1. No canto superior direito da página, toque em **[!UICONTROL Cancelar publicação]**.

## Monitorar o progresso da codificação de vídeo e da publicação no YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Ao fazer upload de um novo vídeo para uma pasta com codificação de vídeo aplicada, ou ao publicar seu vídeo no YouTube, você pode monitorar o progresso da codificação de vídeo/publicação do Youtube. O progresso real da publicação do YouTube só está disponível por meio dos logs. No entanto, sua falha ou sucesso é listado de formas adicionais descritas no procedimento a seguir. Além disso, você recebe notificações por email quando um fluxo de trabalho de publicação ou codificação de vídeo do YouTube é concluído ou interrompido.

### Monitorar progresso {#monitoring-progress}

1. Exibir o progresso da codificação de vídeo na pasta de ativos:

   * Na exibição de cartão, o progresso da codificação de vídeo é exibido no ativo por porcentagem. Se houver um erro, essas informações também serão exibidas no ativo.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * Na exibição em lista, o progresso da codificação do vídeo é exibido na **[!UICONTROL Status do processamento]** coluna. Se houver um erro, essa mensagem será exibida nessa mesma coluna.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Essa coluna não é exibida por padrão. Para ativar a coluna, selecione **[!UICONTROL Configurações de exibição]** no menu suspenso de exibições e adicione a coluna **[!UICONTROL Status de processamento]** e toque ou clique em **[!UICONTROL Atualizar]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. Exibir o progresso nos detalhes do ativo. Ao tocar ou clicar em um ativo, abra o menu suspenso e selecione **[!UICONTROL Linha do tempo]**. Para restringi-lo a atividades de fluxo de trabalho, como codificação ou publicação no YouTube, selecione **[!UICONTROL Fluxos de trabalho]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   Qualquer informação do fluxo de trabalho, como codificação, é exibida na linha do tempo. Para publicação do YouTube, a linha do tempo do Fluxo de trabalho também inclui o nome do canal do YouTube e o URL do vídeo do YouTube. Além disso, você vê notificações de falha na linha do tempo do fluxo de trabalho depois que a publicação é concluída.

   >[!NOTE]
   >
   >Pode levar muito tempo para que as mensagens de erro/falha sejam gravadas devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >    * Configuração da fila de trabalhos do Apache Sling
   >    * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   >    * Fila de tempo limite do fluxo de trabalho do Granite

   >
   >Pode ajustar a variável **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** nessas configurações.

1. Nos fluxos de trabalho em andamento, consulte Instâncias de fluxo de trabalho disponíveis em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Instâncias]**.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Selecione a instância e toque em **[!UICONTROL Abrir Histórico]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   Na área Instâncias do fluxo de trabalho , também é possível suspender, encerrar ou renomear fluxos de trabalho. Consulte [Administração de fluxos de trabalho](/help/sites-administering/workflows-administering.md) para obter mais informações.

1. Em tarefas com falha, consulte Falhas de fluxo de trabalho, disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Falhas]**. A **[!UICONTROL Falha do fluxo de trabalho]** lista todas as atividades do fluxo de trabalho com falha.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Pode levar muito tempo para que a mensagem de erro seja gravada devido a várias configurações de workflow em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** from [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >
   >
   >    * Configuração da fila de trabalhos do Apache Sling
   >    * Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite
   >    * Fila de tempo limite do fluxo de trabalho do Granite

   >
   >
   >Pode ajustar a variável **[!UICONTROL tentativas]**, **[!UICONTROL atraso de nova tentativa]** e **[!UICONTROL timeout]** nessas configurações.

1. Em fluxos de trabalho concluídos, consulte Arquivo de fluxo de trabalho disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Arquivar]**. O **[!UICONTROL Arquivo de fluxo de trabalho]** lista todas as atividades de fluxo de trabalho concluídas.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Você recebe notificações por email sobre trabalhos de fluxo de trabalho abortados ou com falha. Essas notificações por email podem ser configuradas por um administrador. Consulte [Configurar notificações por email](#configuring-e-mail-notifications).

#### Configurar notificações por email {#configuring-e-mail-notifications}

>[!NOTE]
>
>Você precisa de direitos administrativos para acessar o **[!UICONTROL Ferramentas]** menu.

A forma como você configura a notificação depende se você deseja notificações para codificar trabalhos ou trabalhos de publicação do YouTube:

* Para tarefas de codificação, você pode acessar a página de configuração de todas as notificações por email do fluxo de trabalho do Experience Manager em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e procurando por **[!UICONTROL Serviço de Notificação por Email do Workflow CQ Dia]**. Consulte [Configurar notificação por email no Experience Manager](/help/sites-administering/notification.md). Você pode marcar ou desmarcar as caixas de seleção para **[!UICONTROL Notificar sobre Abortar]** ou **[!UICONTROL Notificar quando Concluído]** em conformidade.

* Para trabalhos de publicação do YouTube, faça o seguinte:

1. No Experience Manager, toque em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho , selecione **[!UICONTROL Publicar no YouTube]** e toque em **[!UICONTROL Editar]** na barra de ferramentas.
1. Próximo ao canto superior direito da página do fluxo de trabalho Publicar no YouTube , toque em **[!UICONTROL Editar]**.
1. Passe o mouse sobre o componente Upload do YouTube e toque uma vez para exibir a barra de ferramentas em linha.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. Na barra de ferramentas em linha, toque no ícone Configuração (chave). Clique no botão **[!UICONTROL Argumentos]** guia .

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. Na caixa de diálogo Processo de upload do YouTube - Propriedades da etapa , toque no **[!UICONTROL Argumentos]** guia .

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. Você pode marcar ou desmarcar as seguintes caixas de seleção:

   * Início da publicação
   * Falha na publicação
   * Conclusão de publicação - inclui informações sobre canais e URLs

   Limpar uma caixa de seleção significa que você não recebe a notificação por email especificada do fluxo de trabalho de Publicação do YouTube .

   >[!NOTE]
   >
   >Esses emails são específicos do YouTube e, além das notificações por email de workflow genéricas. Como resultado, você pode receber dois conjuntos de notificações por email - a notificação genérica disponível no **[!UICONTROL Serviço de Notificação por Email do Workflow CQ Dia]** e uma específica para o YouTube, dependendo das configurações.

1. Quando terminar, próximo ao canto superior direito da caixa de diálogo, toque no **[!UICONTROL Concluído]** ícone (marca de seleção).
1. Na página de fluxo de trabalho Publicar no YouTube , próximo ao canto superior direito, toque em **[!UICONTROL Sincronizar]**.

## Anotar ativos de vídeo {#annotate-video-assets}

1. No [!DNL Assets] , selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Visualizar]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao fazer anotações, você pode desenhar na tela e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotação, clique em **[!UICONTROL Fechar]**.

   ![Desenhar e anotar em um quadro de vídeo](assets/annotate-video.png)

1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.

   ![Procure um horário em um vídeo para ignorar em segundos específicos](assets/seek-in-video.png)

1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

   ![Exibir anotações e detalhes na linha do tempo](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gerenciar ativos digitais no Experience Manager Assets](/help/assets/manage-assets.md)
>* [Gerenciar coleções no Experience Manager Assets](/help/assets/manage-collections.md)
>* [Documentação de vídeo do Dynamic Media](/help/assets/video.md).

