---
title: Gerenciar ativos de vídeo
description: Carregar, visualizar, anotar e publicar ativos de vídeo no [!DNL Adobe Experience Manager].
contentOwner: AG
role: User
feature: Asset Management
exl-id: 21d3e0bd-5955-470a-8ca2-4d995c17eb4c
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '5466'
ht-degree: 7%

---

# Gerenciar ativos de vídeo {#manage-video-assets}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/manage-video-assets.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

O formato de vídeo é uma parte essencial dos ativos digitais de uma organização. O [!DNL Adobe Experience Manager] oferece ofertas e recursos completos para gerenciar todo o ciclo de vida dos ativos de vídeo após sua criação.

Saiba como gerenciar e editar os ativos de vídeo no [!DNL Adobe Experience Manager Assets]. A codificação e transcodificação de vídeo, por exemplo, a transcodificação FFmpeg, é possível usando a integração [!DNL Dynamic Media].

## Fazer upload e pré-visualizar ativos de vídeo {#upload-and-preview-video-assets}

[!DNL Adobe Experience Manager Assets] gera visualizações para ativos de vídeo com a extensão MP4. Se o formato do ativo não for MP4, instale o pacote FFmpeg para gerar uma pré-visualização. O FFmpeg cria representações de vídeo do tipo OGG e MP4. Você pode visualizar as representações na interface do usuário do [!DNL Assets].

1. Na pasta ou subpastas de ativos digitais, navegue até o local em que deseja adicionar ativos digitais.
1. Para carregar o ativo, clique em **[!UICONTROL Criar]** na barra de ferramentas e escolha **[!UICONTROL Arquivos]**. Como alternativa, arraste um arquivo para a interface do usuário. Consulte [carregar ativos](manage-assets.md#uploading-assets) para obter detalhes.
1. Para visualizar um vídeo no modo de exibição de Cartão, clique na opção **[!UICONTROL Reproduzir]** ![reproduzir](assets/do-not-localize/play.png) no ativo de vídeo. Você pode pausar ou reproduzir vídeo somente na exibição de cartão. As opções [!UICONTROL Reproduzir] e [!UICONTROL Pausar] não estão disponíveis na exibição de lista.

1. Para visualizar o vídeo na página de detalhes do ativo, clique em **[!UICONTROL Editar]** no cartão. O vídeo é reproduzido no reprodutor de vídeo nativo do navegador. Você pode reproduzir, pausar, controlar o volume e aplicar zoom ao vídeo em tela inteira.

   ![Controles de reprodução de vídeo](assets/video-playback-controls.png)

## Configuração para carregar ativos com mais de 2 GB {#configuration-to-upload-assets-that-are-larger-than-gb}

Por padrão, o [!DNL Assets] não permite carregar nenhum ativo com mais de 2 GB devido a um limite de tamanho de arquivo. No entanto, você pode substituir esse limite acessando o CRXDE Lite e criando um nó sob o diretório `/apps`. O nó deve ter o mesmo nome de nó, estrutura de diretório e propriedades de nó comparáveis.

Além da configuração do [!DNL Assets], altere as seguintes configurações para carregar ativos grandes:

* Aumente o tempo de expiração do token. Consulte [!UICONTROL Servlet CSRF do Adobe Granite] no Console da Web em `https://[aem_server]:[port]/system/console/configMgr`. Para obter mais informações, consulte [Proteção CSRF](/help/sites-developing/csrf-protection.md).
* Aumente o `receiveTimeout` na configuração do Dispatcher. Para obter mais informações, consulte [configuração do Experience Manager Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#renders-options).

>[!NOTE]
>
>A interface do usuário do [!DNL Experience Manager] Classic não tem uma restrição de limite de tamanho de arquivo de 2 GB. Além disso, o fluxo de trabalho completo para vídeos grandes não é totalmente compatível.

Para configurar um limite de tamanho de arquivo mais alto, execute as etapas a seguir no diretório `/apps`.

1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No CRXDE Lite, navegue até `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`. Para ver a janela do diretório, clique em `>>`.
1. Na barra de ferramentas, clique em **[!UICONTROL Sobrepor Nó]**. Como alternativa, selecione **[!UICONTROL Sobrepor nó]** no menu de contexto.
1. Na caixa de diálogo **[!UICONTROL Sobrepor Nó]**, clique em **[!UICONTROL OK]**.

   ![Sobrepor nó](assets/overlay-node-path.png)

1. Atualize o navegador. O nó de sobreposição `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload` está selecionado.
1. Na guia **[!UICONTROL Propriedades]**, insira o valor apropriado em bytes para aumentar o limite de tamanho para o tamanho desejado. Por exemplo, para aumentar o limite de tamanho para 30 GB, insira o valor `32212254720`.

1. Na barra de ferramentas, clique em **[!UICONTROL Salvar tudo]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
1. Na página [!DNL Adobe Experience Manager] [!UICONTROL Pacotes de Console da Web], na coluna Nome da tabela, localize e clique em **[!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite]**.
1. Na página [!UICONTROL Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite], defina os segundos para os campos **[!UICONTROL Tempo limite padrão]** e **[!UICONTROL Tempo limite máximo]** como `18000` (cinco horas). Clique em **[!UICONTROL Salvar]**.
1. Em [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho, selecione **[!UICONTROL Codificação de vídeo do Dynamic Media]** e clique em **[!UICONTROL Editar]**.
1. Na página de fluxo de trabalho, clique duas vezes no **[!UICONTROL Processo de serviço de vídeo]** do Dynamic Media.
1. Na caixa de diálogo [!UICONTROL Propriedades da etapa], na guia **[!UICONTROL Comum]**, expanda **Configurações avançadas**.
1. No campo **[!UICONTROL Tempo limite]**, especifique um valor de `18000` e clique em **[!UICONTROL OK]** para retornar à página de fluxo de trabalho **[!UICONTROL Codificação de vídeo Dynamic Media]**.
1. Próximo à parte superior da página, abaixo do título da página [!UICONTROL Codificação de vídeo do Dynamic Media], clique em **[!UICONTROL Salvar]**.

## Ativos de vídeo do Publish {#publish-video-assets}

Após a publicação, você pode incluir os ativos de vídeo em uma página da Web como um URL ou incorporar diretamente os ativos. Para obter detalhes, consulte [publicar ativos do Dynamic Media](/help/assets/publishing-dynamicmedia-assets.md).

## Vídeos do Publish para o YouTube {#publishing-videos-to-youtube}

Você pode publicar ativos de vídeo de Experience Manager local diretamente em um canal do YouTube criado anteriormente.

Para publicar ativos de vídeo no YouTube, você configurou o Experience Manager Assets com tags. Você associa essas tags a um canal do YouTube. Se a tag de um ativo de vídeo corresponder à tag de um canal do YouTube, o vídeo será publicado no YouTube. O Publish para o YouTube ocorre junto com uma publicação normal do vídeo, desde que uma tag associada seja usada.

O YouTube faz sua própria codificação. Dessa forma, o arquivo de vídeo original carregado no Experience Manager é publicado no YouTube, em vez de qualquer representação de vídeo criada pela codificação do Dynamic Media. Embora não seja necessário processar vídeos usando o Dynamic Media, espera-se que eles façam isso caso uma predefinição do visualizador seja necessária para a reprodução.

Ao ignorar o perfil de processamento de vídeo e publicar diretamente no YouTube, isso significa simplesmente que o ativo de vídeo no Experience Manager Asset não obtém uma miniatura visualizável. Também significa que, se você executar no modo de execução `dynamicmedia` ou `dynamicmedia_scene7`, os vídeos não codificados não funcionarão com nenhum dos tipos de ativos do Dynamic Media.

A publicação de ativos de vídeo em servidores da YouTube envolve a conclusão das seguintes tarefas para garantir uma autenticação segura de servidor para servidor com o YouTube:

1. [Definir configurações da Google Cloud](#configuring-google-cloud-settings)
1. [Criar um canal do YouTube](#creating-a-youtube-channel)
1. [Adicionar tags para publicação](#adding-tags-for-publishing)
1. [Ativar o agente de replicação do YouTube Publish](#enabling-the-youtube-publish-replication-agent)
1. [Configurar o YouTube no Experience Manager](#setting-up-youtube-in-aem)
1. [(Opcional) Automatize a configuração das propriedades padrão do YouTube para os vídeos carregados](#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos)
1. [Vídeos do Publish para o canal do YouTube](#publishing-videos-to-your-youtube-channel)
1. [(Opcional) Verifique o vídeo publicado no YouTube](/help/assets/video.md#optional-verifying-the-published-video-on-youtube)
1. [Vincular URLs do YouTube à sua aplicação web](#linking-youtube-urls-to-your-web-application)

Você também pode [cancelar a publicação de vídeos para removê-los do YouTube](#unpublishing-videos-to-remove-them-from-youtube).

### Definir configurações da Google Cloud {#configuring-google-cloud-settings}

Para publicar no YouTube, você precisa de uma conta do Google. Se você tiver uma conta do GMAIL, já terá uma conta do Google; se não tiver uma conta do Google, poderá criar facilmente uma. Você precisa da conta porque precisa de credenciais para publicar ativos de vídeo no YouTube. Se você tiver uma conta já criada, ignore esta tarefa e prossiga diretamente para [Criar um canal de YouTube](#creating-a-youtube-channel).

A conta usada com a Google Cloud e a conta do Google usada para o YouTube não precisam ser a mesma.

A Google altera periodicamente a interface do usuário. Dessa forma, as etapas para publicar vídeos no YouTube podem variar um pouco do que está documentado abaixo. Esse aviso também se aplica ao YouTube quando você tenta verificar se os vídeos foram carregados para ele.

>[!NOTE]
>
>As etapas a seguir eram precisas no momento da redação deste documento. No entanto, a Google atualiza os sites periodicamente sem aviso prévio. Dessa forma, essas etapas podem ser um pouco diferentes.

Para definir as configurações da Google Cloud:

1. Crie uma conta do Google.

   Se você já tiver uma conta do Google, pule para a próxima etapa.

1. Ir para [https://cloud.google.com/](https://cloud.google.com/).
1. Na página do Google Cloud, próximo ao canto superior direito, clique em **[!UICONTROL Console]**.

   Se necessário, **[!UICONTROL Entre]** usando suas credenciais de conta da Google para ver a opção **[!UICONTROL Console]**.

1. Na página Painel, à direita de **[!UICONTROL Google Cloud Platform]**, clique na lista suspensa Projeto para abrir a caixa de diálogo Selecionar um projeto.
1. Na caixa de diálogo Selecionar um projeto, selecione **[!UICONTROL Novo Projeto]**.

   ![6_5_googleaccount-newproject](assets/6_5_googleaccount-newproject.png)

1. Na caixa de diálogo Novo projeto, no campo Nome do projeto, digite o nome do novo projeto.

   A ID do projeto é baseada no nome do projeto. Sendo assim, escolha o nome do projeto com cuidado; ele não poderá ser alterado após sua criação. Além disso, você deve inserir a mesma ID de projeto novamente ao configurar o YouTube no Experience Manager posteriormente; considere anotá-la.

1. Clique em **[!UICONTROL Criar]**.

1. Siga um destes procedimentos:

   * No painel do seu projeto, no cartão Introdução, selecione **[!UICONTROL Explorar e habilitar APIs]**.
   * No Painel do seu projeto, no cartão APIs, selecione **[!UICONTROL Ir para a visão geral das APIs]**.

   ![6_5_googleaccount-apis-enable2](assets/6_5_googleaccount-apis-enable2.png)

1. Próximo à parte superior da página APIs e Serviços, selecione **[!UICONTROL Habilitar APIs e Serviços]**.
1. Na página Biblioteca de API, no lado esquerdo, em **[!UICONTROL Categoria]**, selecione **[!UICONTROL YouTube]**. No lado direito da página, selecione **[!UICONTROL API de dados do YouTube]**.
1. Na página API v3 de dados do YouTube, selecione **[!UICONTROL Habilitar]**.

   ![6_5_googleaccount-apis-enable3](assets/6_5_googleaccount-apis-enable3.png)

1. Para usar a API, você precisa de credenciais. Se necessário, clique em **[!UICONTROL Criar credenciais]**.

   ![6_5_googleaccount-apis-createcredentials](assets/6_5_googleaccount-apis-createcredentials.png)

1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 1, faça o seguinte:

   * Na **[!UICONTROL Qual API você está usando?Na lista suspensa]**, selecione **[!UICONTROL API de Dados do YouTube v3]**.

   * No **[!UICONTROL De onde você está chamando a API?na lista suspensa]**, selecione **[!UICONTROL Servidor Web (por exemplo, node.js, Tomcat)]**

   * No **[!UICONTROL Que dados você está acessando?]**, selecione **[!UICONTROL Dados do usuário]**.

   ![6_5_googleaccount-apis-createcredentials2](assets/6_5_googleaccount-apis-createcredentials2.png)

1. Selecionar **[!UICONTROL Quais credenciais são necessárias?]**
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 2, no cabeçalho **[!UICONTROL Criar uma ID de cliente do OAuth 2.0]**, no campo Nome, digite um nome exclusivo, se desejar. Ou você pode usar o nome padrão especificado pelo Google.
1. No cabeçalho **[!UICONTROL Origens autorizadas do JavaScript]**, no campo de texto, digite o seguinte caminho, substituindo seu próprio domínio e número de porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>`

   Por exemplo, `https://1a2b3c.mycompany.com:4321`

   **Observação**: o exemplo de caminho acima destina-se somente a fins de demonstração.

   ![6_5_googleaccount-apis-createcredentials-oauth](assets/6_5_googleaccount-apis-createcredentials-oauth.png)

1. No cabeçalho **[!UICONTROL URIs de redirecionamento autorizados]**, no campo de texto, insira o seguinte caminho, substituindo seu próprio domínio e número de porta no caminho, e pressione **[!UICONTROL Enter]** para adicionar o caminho à lista:

   `https://<servername.domain>:<port_number>/etc/cloudservices/youtube.youtubecredentialcallback.json`

   Por exemplo, `https://1a2b3c.mycompany.com:4321/etc/cloudservices/youtube.youtubecredentialcallback.json`

   **Observação**: o exemplo de caminho acima destina-se somente a fins de demonstração.

1. Clique em **[!UICONTROL Criar ID do cliente OAuth]**.
1. Na página **[!UICONTROL Adicionar credenciais ao projeto]**, etapa 3, no cabeçalho **[!UICONTROL Configurar a tela de consentimento do OAuth 2.0]**, selecione o endereço de email do Gmail que você está usando no momento.

   ![6_5_googleaccount-apis-createcredentials-consentscreen](assets/6_5_googleaccount-apis-createcredentials-consentscreen.png)

1. No cabeçalho **[!UICONTROL Nome do produto mostrado aos usuários]**, no campo de texto, digite o que você deseja mostrar na tela de consentimento.

   A tela de consentimento é exibida ao administrador de Experience Manager quando ele se autentica no YouTube; o Experience Manager entra em contato com a YouTube para obter permissão.

1. Clique em **[!UICONTROL Continuar]**.
1. Na página Adicionar credenciais ao projeto, etapa 4, no cabeçalho **[!UICONTROL Baixar credenciais]**, selecione **[!UICONTROL Baixar]**.

   ![6_5_googleaccount-apis-createcredentials-downloadcredentials](assets/6_5_googleaccount-apis-createcredentials-downloadcredentials.png)

1. Salve o arquivo `client_id.json`.

   Você precisará desse arquivo json baixado ao configurar o YouTube no Adobe Experience Manager posteriormente.

1. Clique em **[!UICONTROL Concluído]**.

   Faça logout da sua conta da Google. Agora crie um canal do YouTube.

### Criar um canal do YouTube {#creating-a-youtube-channel}

Para publicar vídeos no YouTube, você precisa ter um ou mais canais. Se você já criou um canal YouTube, ignore esta tarefa e vá para [Adicionar marcas para publicação](/help/assets/video.md#adding-tags-for-publishing).

>[!WARNING]
>
>Certifique-se de já ter configurado um ou mais canais no YouTube *antes* de adicionar canais nas Configurações do YouTube no Experience Manager (consulte [Configurar o YouTube no Experience Manager](#setting-up-youtube-in-aem) abaixo). Se você não configurar um ou mais canais, não será avisado de canais inexistentes. No entanto, a autenticação do Google ainda ocorre ao adicionar um canal, mas não há a opção de escolher qual canal o vídeo é enviado.

**Para criar um canal do YouTube:**

1. Vá para [https://www.youtube.com](https://www.youtube.com/) e entre usando suas credenciais de conta da Google.
1. No canto superior direito da página do YouTube, clique na imagem do seu perfil (ela também pode aparecer como uma letra dentro de um círculo de cores sólidas) e clique em **[!UICONTROL Configurações do YouTube]** (ícone de roda dentada).
1. Na página Visão Geral, no cabeçalho Recursos Adicionais, clique em **[!UICONTROL Ver todos os meus canais ou criar um canal]**.
1. Na página Canais, clique em **[!UICONTROL Criar um novo canal]**.
1. Na página Conta da Marca, no campo Nome da Conta da Marca, digite um nome comercial ou qualquer outro nome de canal que você escolher onde deseja publicar seus ativos de vídeo e clique em **[!UICONTROL Criar]**.

   Lembre-se do nome inserido aqui porque você deve inseri-lo novamente ao configurar o YouTube no Experience Manager.

1. (Opcional) Se necessário, adicione mais canais.

   Agora adicione tags para publicação.

### Adicionar tags para publicação {#adding-tags-for-publishing}

Para publicar seus vídeos no YouTube, o Experience Manager associa tags a um ou mais canais da YouTube. Para adicionar marcas para publicação, consulte [Administrar marcas](/help/sites-administering/tags.md).

Ou, se você pretende usar as marcas padrão no Experience Manager, ignore esta tarefa e vá para [Habilitar o agente de replicação do YouTube Publish](#enabling-the-youtube-publish-replication-agent).

### Habilitar o agente de replicação do YouTube Publish {#enabling-the-youtube-publish-replication-agent}

Depois de habilitar o agente de replicação do YouTube Publish, se quiser testar a conexão com a conta da Google Cloud, selecione **[!UICONTROL Testar Conexão]**. Uma guia do navegador exibe os resultados da conexão. Se você tiver adicionado Canais do YouTube, uma lista deles será exibida como parte do teste.

1. No canto superior esquerdo do Experience Manager, clique no logotipo do Experience Manager e, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Implantação]** > **[!UICONTROL Replicação]** > **[!UICONTROL Agentes no Autor]**.
1. Na página Agentes do autor, clique em **[!UICONTROL YouTube Publish]**.
1. Na barra de ferramentas, à direita de Configurações, clique em **[!UICONTROL Editar]**.
1. Marque a caixa de seleção **[!UICONTROL Habilitado]** para poder ativar o agente de replicação.
1. Clique em **[!UICONTROL OK]**.

   Agora, configure o YouTube no Experience Manager.

### Configurar o YouTube no Experience Manager {#setting-up-youtube-in-aem}

A partir do Experience Manager 6.4, um novo método de interface do usuário de toque foi introduzido para configurar a publicação do YouTube no Experience Manager. Com base na instância instalada do Experience Manager que você está usando, execute um dos procedimentos a seguir:

* Para configurar o YouTube no Experience Manager anterior a 6.4, consulte [Configurar o YouTube no Experience Manager anterior a 6.4](/help/assets/video.md#setting-up-youtube-in-aem-before).
* Para configurar o YouTube no Experience Manager 6.4 ou posterior, consulte [Configurar o YouTube no Experience Manager 6.4 e posterior](#setting-up-youtube-in-aem-and-later).

#### Configurar o YouTube no Experience Manager 6.4 e mais recente {#setting-up-youtube-in-aem-and-later}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como Administrador.
1. No canto superior esquerdo, selecione o logotipo do Experience Manager e, no painel à esquerda, selecione **[!UICONTROL Ferramentas]**(ícone de martelo) > **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuração de publicação do YouTube]**.
1. Selecionar **[!UICONTROL global]** (não o selecione).

1. Próximo ao canto superior direito da página global, selecione **[!UICONTROL Criar]**.
1. Na página Criar configuração do YouTube, em Configurações da Google Cloud Platform, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao definir as configurações da Google Cloud anteriormente.
Deixe a página Criar configuração do YouTube aberta; em breve, você retornará a ela.

   ![6_5_youtubepublish-createyoutubeconfiguration](assets/6_5_youtubepublish-createyoutubeconfiguration.png)

1. Usando um editor de texto simples, abra o arquivo JSON que você baixou e salvou anteriormente na tarefa [Definir configurações da Google Cloud](/help/assets/video.md#configuring-google-cloud-settings).
1. Selecione e copie todo o texto JSON.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

   Agora, configure os canais do YouTube no Experience Manager.

1. Selecione **[!UICONTROL Adicionar Canal]**.
1. No campo Nome do Canal, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejado.

1. Selecione **[!UICONTROL Adicionar]**.
1. A autenticação do YouTube/Google é exibida. Se você ainda não tiver feito logon na conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem, você verá dois ou mais itens. Selecione um canal. Não selecione o endereço de e-mail; ele não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir acesso a este canal.

1. Selecione **[!UICONTROL Permitir]**.

   Agora, configure tags para publicação.

1. **[!UICONTROL Configurando marcas para publicação]** - Na página Cloud Service > YouTube, selecione o ícone de lápis para editar a lista de marcas que deseja usar.
1. Selecione o ícone da lista suspensa (cursor invertido) para que você possa exibir a lista de tags disponíveis no Experience Manager.
1. Selecione uma ou mais tags para adicioná-las.

   Para excluir uma marca adicionada, selecione-a e selecione **[!UICONTROL X]**.

1. Quando terminar de adicionar as marcas desejadas, selecione **[!UICONTROL Salvar]**.

   Agora você publica vídeos no seu canal do YouTube.

#### Configurar o YouTube no Experience Manager anterior a 6.4 {#setting-up-youtube-in-aem-before}

1. Certifique-se de fazer logon na sua instância do Dynamic Media como Administrador.

1. No canto superior esquerdo, selecione o logotipo Experience Manager e, no painel à esquerda, selecione **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Implantação]** > **[!UICONTROL Cloud Service]**.
1. No cabeçalho Serviços de terceiros, em YouTube, selecione **[!UICONTROL Configurar agora]**.
1. Na caixa de diálogo Criar configuração, insira um título (obrigatório) e nome (opcional) nos respectivos campos.
1. Selecione **[!UICONTROL Criar]**.
1. Na caixa de diálogo Configurações da conta do YouTube, no campo **[!UICONTROL Nome do aplicativo]**, digite a ID do projeto do Google.

   Você especificou a ID do projeto ao [definir inicialmente as configurações da Google Cloud](/help/assets/video.md#configuring-google-cloud-settings).
Deixe aberta a caixa de diálogo Configuração de conta do YouTube; você retornará a ela em alguns instantes.

1. Usando um editor de texto simples, abra o arquivo JSON baixado e salvo anteriormente na tarefa Definição das configurações da Google Cloud.
1. Selecione e copie todo o texto JSON.
1. Retorne à caixa de diálogo Configurações da conta do YouTube. No campo **[!UICONTROL Configuração JSON]**, cole o texto JSON.
1. Selecione **[!UICONTROL OK]**.

   Agora, configure os canais do YouTube no Experience Manager.

1. À direita de **[!UICONTROL Canais disponíveis]**, selecione **+** (ícone de adição).
1. Na caixa de diálogo Configurações do canal do YouTube, no campo Título, digite o nome do canal criado na tarefa **[!UICONTROL Adicionar um ou mais canais ao YouTube]** anteriormente.

   Opcionalmente, é possível adicionar uma descrição, se desejado.

1. Selecione **[!UICONTROL OK]**.
1. A autenticação do YouTube/Google é exibida. Se você ainda não tiver feito logon na conta da Google Cloud, ignore esta etapa.

   * Insira o nome de usuário e a senha do Google associados à ID do projeto do Google e o texto JSON acima.
   * Dependendo de quantos canais sua conta tem, você verá dois ou mais itens. Selecione um canal. Não selecione o endereço de e-mail; ele não é um canal.
   * Na próxima página, selecione **[!UICONTROL Aceitar]** para permitir acesso a este canal.

1. Selecione **[!UICONTROL Permitir]**.

   Agora, configure tags para publicação.

1. **[!UICONTROL Configurando marcas para publicação]** - Na página Cloud Service > YouTube, selecione o ícone de lápis para editar a lista de marcas que deseja usar.
1. Selecione o ícone da lista suspensa (cursor invertido) para que você possa exibir a lista de tags disponíveis no Experience Manager.
1. Selecione uma ou mais tags para adicioná-las.

   Para excluir uma marca adicionada, selecione-a e selecione **X**.

1. Quando terminar de adicionar as marcas desejadas, selecione **[!UICONTROL OK]**.

   Agora você publica vídeos no seu canal do YouTube.

### (Opcional) Automatize a configuração das propriedades padrão do YouTube para os vídeos carregados {#optional-automating-the-setting-of-default-youtube-properties-for-your-uploaded-videos}

Como opção, é possível automatizar a configuração das propriedades do YouTube no upload de seus vídeos criando um perfil de processamento de metadados no Experience Manager.

Para criar o perfil de processamento de metadados, você primeiro copiará valores dos campos **[!UICONTROL Rótulo do campo]**, **[!UICONTROL Mapear para a propriedade]** e **[!UICONTROL Opções]**, todos encontrados nos Esquemas de metadados do vídeo. Em seguida, crie seu perfil de processamento de metadados de vídeo do YouTube adicionando esses valores a ele.

Para automatizar a configuração das propriedades padrão do YouTube para os vídeos carregados:

1. No canto superior esquerdo, selecione o logotipo do Experience Manager e, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Assets]** > **[!UICONTROL Esquemas de metadados]**.
1. Clique em **[!UICONTROL padrão]**. (Não adicione uma marca de seleção à caixa de seleção à esquerda de &quot;padrão&quot;.)
1. Na página **[!UICONTROL padrão]**, marque a caixa à esquerda de **[!UICONTROL vídeo]** e selecione **[!UICONTROL Editar]**.
1. Na página Editor de esquema de metadados, selecione a guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação no YouTube, clique em **[!UICONTROL Categoria do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Configurações]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para a propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar (como Pessoas e Blogs ou Ciência e Tecnologia).
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

1. No cabeçalho Publicação no YouTube, selecione **[!UICONTROL Privacidade do YouTube]**.
1. No lado direito da página, na guia **[!UICONTROL Configurações]**, faça o seguinte:

   * No campo de texto **[!UICONTROL Mapear para a propriedade]**, selecione e copie o valor.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

   * Em **[!UICONTROL Opções]**, selecione e copie o valor padrão que deseja usar. Observe que as Opções são agrupadas em pares de dois. O campo inferior no par é o valor padrão que você deseja copiar, como público, não listado ou privado.
Cole o valor copiado no editor de texto aberto. Esse valor será necessário posteriormente ao criar o perfil de processamento de metadados. Deixe o editor de texto aberto.

1. Próximo ao canto superior direito da página Editor de esquema de metadados, clique em **[!UICONTROL Cancelar]**.
1. No canto superior esquerdo do Experience Manager, selecione o logotipo Experience Manager e, no painel à esquerda, clique em **[!UICONTROL Ferramentas]** (ícone de martelo) > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de metadados]**.

1. Na página Perfis de metadados, próximo ao canto superior direito da página, clique em **[!UICONTROL Criar]**.
1. Na caixa de diálogo Adicionar perfil de metadados, no campo de texto **[!UICONTROL Título do perfil]**, digite o nome `YouTube Video` e clique em **[!UICONTROL Criar]**.
1. Na página Editor de perfil de metadados, clique na guia **[!UICONTROL Avanço]**.
1. Adicione os valores copiados do YouTube Publishing ao perfil fazendo o seguinte:

   * No lado direito da página, clique na guia **[!UICONTROL Criar Formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área de formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações, no campo de texto Rótulo do Campo, digite `YouTube Publishing`.
   * Clique na guia **[!UICONTROL Criar Formulário]** e arraste o componente rotulado **[!UICONTROL Texto de Vários Valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Publicação do YouTube]** que você criou.

   * Clique em **[!UICONTROL Rótulo do campo]** para que o componente seja selecionado.
   * No lado direito da página, na guia Configurações, cole os valores de Publicação do YouTube (valor Rótulo do campo e valor Mapear para a propriedade ) que você copiou anteriormente, nos respectivos campos no formulário. Cole o valor de Choices no campo Default Value.

1. Adicione os valores copiados de Privacidade do YouTube ao perfil da seguinte maneira:

   * No lado direito da página, clique na guia **[!UICONTROL Criar Formulário]**.
   * (Opcional) Arraste o componente rotulado **[!UICONTROL Cabeçalho da seção]** para a esquerda e solte-o na área de formulário.
   * (Opcional) Clique em **[!UICONTROL Rótulo do campo]** para selecionar o componente.
   * (Opcional) No lado direito da página, na guia Configurações, no campo de texto Rótulo do Campo, digite `YouTube Privacy`.
   * Clique na guia **[!UICONTROL Criar Formulário]** e arraste o componente rotulado **[!UICONTROL Texto de Vários Valores]** e solte-o abaixo do cabeçalho **[!UICONTROL Privacidade do YouTube]** que você criou.

   * Clique em **[!UICONTROL Rótulo do campo]** para que o componente seja selecionado.
   * No lado direito da página, na guia Configurações, cole os valores de Publicação do YouTube (valor Rótulo do campo e valor Mapear para a propriedade ) que você copiou anteriormente, nos respectivos campos no formulário. Cole o valor de Choices no campo Default Value.

1. Ao lado do canto superior direito da página, clique em **[!UICONTROL Salvar]**.
1. Aplique o perfil de metadados de Publicação do YouTube às pastas nas quais você fará upload dos vídeos. Você deve ter o Perfil de metadados e o Perfil de vídeo definidos.

   Consulte [Perfis de metadados](/help/assets/metadata-config.md#metadata-profiles) e [Perfis de vídeo](/help/assets/video-profiles.md).

### Vídeos do Publish para o canal do YouTube {#publishing-videos-to-your-youtube-channel}

Agora você associa as tags adicionadas anteriormente aos ativos de vídeo. Esse processo permite que o Experience Manager saiba quais ativos publicar no canal do YouTube.

>[!NOTE]
>
>Ao ser executado no modo Dynamic Media - Scene7, a publicação imediata não publica automaticamente no YouTube. Quando o modo Dynamic Media - Scene7 estiver configurado, há duas opções de publicação para escolher: **[!UICONTROL Imediatamente]** ou **[!UICONTROL Na Ativação]**.
>
>**[!UICONTROL Publish Imediatamente]** significa que o ativo carregado, após ser sincronizado com o IPS, é publicado automaticamente no sistema de entrega. Embora isso seja verdade para o Dynamic Media, não é verdade para o YouTube. Para publicar no YouTube, você deve publicar por meio do Experience Manager Author.

>[!NOTE]
>
>Para publicar conteúdo do YouTube, o Experience Manager usa o fluxo de trabalho **[!UICONTROL Publish no YouTube]**, que permite monitorar o progresso e exibir informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).
>
>Para obter informações mais detalhadas sobre o progresso, é possível monitorar o log do YouTube em replicação. No entanto, esteja ciente de que esse monitoramento requer acesso de administrador.

**Para publicar vídeos no seu canal do YouTube:**

1. No Experience Manager, navegue até um ativo de vídeo que deseja publicar no canal do YouTube.
1. Selecione o ativo de vídeo (o conjunto de vídeos adaptáveis).
1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Na guia Básico, no cabeçalho Metadados, clique em **[!UICONTROL Abrir Caixa de Diálogo de Seleção]** à direita do campo Marcas.
1. Na página Selecionar tags, navegue até as tags que deseja usar e selecione uma ou mais tags.

   Lembre-se de que as tags devem ser associadas ao canal do YouTube.

1. No canto superior direito da página, clique em **[!UICONTROL Selecionar]**.
1. No canto superior direito da página de propriedades do vídeo, clique em **[!UICONTROL Salvar e fechar]**.
1. Na barra de ferramentas, clique em **[!UICONTROL Quick Publish]**.

   Consulte também [Uso do Gerenciamento de Publicação com o Experience Manager Sites](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/publication-management-feature-video-use.html?lang=pt-BR).

   Como opção, verifique o vídeo publicado no canal do YouTube.

### (Opcional) Verifique o vídeo publicado no YouTube {#optional-verifying-the-published-video-on-youtube}

Como opção, é possível monitorar o progresso da publicação (ou do cancelamento da publicação) do YouTube.

Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

Os tempos de publicação podem variar muito dependendo de vários fatores que incluem o formato do vídeo de origem principal, o tamanho do arquivo e o tráfego de upload. O processo de publicação pode levar de alguns minutos a várias horas. Além disso, os formatos de resolução mais alta são renderizados muito mais lentamente. Por exemplo, 720p e 1080p demoram mais para serem exibidos do que 480p.

Após oito horas se você ainda vir uma mensagem de status que diz **[!UICONTROL Carregado (processando, aguarde)]**, tente remover o vídeo do site de Adobe e carregá-lo novamente.

### Vincular URLs do YouTube ao aplicativo da Web {#linking-youtube-urls-to-your-web-application}

Você pode obter uma cadeia de caracteres de URL do YouTube gerada pelo Dynamic Media após a publicação do vídeo. Ao copiar o URL do YouTube, ele é colocado na Área de transferência para que você possa colá-lo conforme necessário nas páginas do seu site ou aplicativo.

>[!NOTE]
>
>O URL do YouTube não estará disponível para cópia até que você tenha publicado o ativo de vídeo no YouTube.

**Para vincular URLs do YouTube ao seu aplicativo Web:**

1. Navegue até o ativo de vídeo *YouTube publicado* cuja URL você deseja copiar e selecione-o.

   Lembre-se de que as URLs do YouTube só estão disponíveis para cópia *depois* de você ter *publicado* os ativos de vídeo no YouTube.

1. Na barra de ferramentas, clique em **[!UICONTROL Propriedades]**.
1. Clique na guia **[!UICONTROL Avançado]**.
1. No cabeçalho Publicação no YouTube, na Lista de URLs do YouTube, selecione e copie o texto do URL no navegador da Web para visualizar o ativo ou adicionar à página de conteúdo da Web.

### Desfazer a publicação de vídeos para poder removê-los do YouTube {#unpublishing-videos-to-remove-them-from-youtube}

Ao cancelar a publicação de um ativo de vídeo no Experience Manager, o vídeo é removido do YouTube.

>[!CAUTION]
>
>Se você remover um vídeo diretamente do YouTube, o Experience Manager não estará ciente e continuará a se comportar como se o vídeo ainda estivesse publicado no YouTube. Sempre cancele a publicação de um ativo de vídeo do YouTube por meio do Experience Manager.

>[!NOTE]
>
>Para remover o conteúdo do YouTube, o Experience Manager usa o fluxo de trabalho **[!UICONTROL Desfazer publicação do YouTube]**, que permite monitorar o progresso e exibir informações de falha.
>
>Consulte [Monitorar o progresso da codificação de vídeo e da publicação no YouTube](#monitoring-video-encoding-and-youtube-publishing-progress).

**Para desfazer a publicação de vídeos e removê-los do YouTube:**

1. Navegue até os ativos de vídeo que deseja cancelar a publicação do seu canal do YouTube.
1. Em um modo de seleção de ativo, selecione um ou mais ativos de vídeo publicados.
1. Na barra de ferramentas, clique em **[!UICONTROL Gerenciar Publicação]**. Selecione o ícone de três pontos (. . .) na barra de ferramentas para que **[!UICONTROL Gerenciar Publicação]** seja aberto.
1. Na página Gerenciar publicação, selecione **[!UICONTROL Cancelar publicação]**.
1. No canto superior direito da página, selecione **[!UICONTROL Avançar]**.
1. No canto superior direito da página, selecione **[!UICONTROL Cancelar publicação]**.

## Monitorar o progresso da codificação de vídeo e da publicação no YouTube {#monitoring-video-encoding-and-youtube-publishing-progress}

Ao fazer upload de um novo vídeo para uma pasta que tenha a codificação de vídeo aplicada ou publicar seu vídeo no YouTube, é possível monitorar o progresso da codificação de vídeo/publicação no Youtube. O progresso real da publicação no YouTube só está disponível por meio dos logs. No entanto, seu fracasso ou sucesso é listado de maneiras adicionais descritas no procedimento a seguir. Além disso, você recebe notificações por email quando um fluxo de trabalho de publicação ou codificação de vídeo do YouTube é concluído ou interrompido.

### Monitorar progresso {#monitoring-progress}

1. Exibir o progresso da codificação de vídeo na pasta de ativos:

   * Na exibição de cartão, o progresso de codificação do vídeo é exibido no ativo por porcentagem. Se houver um erro, essas informações também serão exibidas no ativo.

   ![chlimage_1-429](assets/chlimage_1-429.png)

   * Na exibição em lista, o progresso de codificação do vídeo é exibido na coluna **[!UICONTROL Status de Processamento]**. Se houver um erro, essa mensagem será exibida nessa mesma coluna.

   ![chlimage_1-430](assets/chlimage_1-430.png)

   Essa coluna não é exibida por padrão. Para habilitar a coluna, selecione **[!UICONTROL Configurações de Exibição]** no menu suspenso de exibições, adicione a coluna **[!UICONTROL Status de Processamento]** e clique em **[!UICONTROL Atualizar]**.

   ![chlimage_1-431](assets/chlimage_1-431.png)

1. Visualize o progresso nos detalhes do ativo. Ao clicar em um ativo, abra o menu suspenso e selecione **[!UICONTROL Linha do tempo]**. Para restringir a atividades de fluxo de trabalho, como codificação ou publicação no YouTube, selecione **[!UICONTROL Fluxos de trabalho]**.

   ![chlimage_1-432](assets/chlimage_1-432.png)

   Todas as informações do fluxo de trabalho, como codificação, são exibidas na linha do tempo. Para publicação no YouTube, a linha do tempo do Fluxo de trabalho também inclui o nome do canal do YouTube e o URL do vídeo do YouTube. Além disso, você verá todas as notificações de falha na linha do tempo do fluxo de trabalho depois que a publicação for concluída.

   >[!NOTE]
   >
   >Pode levar muito tempo para que as mensagens de erro/falha sejam gravadas devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >* Configuração da fila de trabalhos do Apache Sling
   >* Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite
   >* Fila de tempo limite de fluxo de trabalho do Granite
   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** propriedades nessas configurações.

1. Nos fluxos de trabalho em andamento, consulte Instâncias de fluxo de trabalho disponíveis em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Instâncias]**.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-433](assets/chlimage_1-433.png)

   Selecione a instância e selecione **[!UICONTROL Abrir Histórico]**.

   ![chlimage_1-434](assets/chlimage_1-434.png)

   Na área Instâncias de fluxo de trabalho, também é possível suspender, encerrar ou renomear fluxos de trabalho. Consulte [Administrando fluxos de trabalho](/help/sites-administering/workflows-administering.md) para obter mais informações.

1. Em tarefas com falha, consulte Falhas de fluxo de trabalho, disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Falhas]**. A **[!UICONTROL Falha do fluxo de trabalho]** lista todas as atividades do fluxo de trabalho com falha.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-435](assets/chlimage_1-435.png)

   >[!NOTE]
   >
   >Pode levar muito tempo para que a mensagem de erro seja gravada devido a várias configurações de fluxo de trabalho em **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** de [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr), por exemplo:
   >
   >* Configuração da fila de trabalhos do Apache Sling
   >* Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite
   >* Fila de tempo limite de fluxo de trabalho do Granite
   >
   >Você pode ajustar as **[!UICONTROL tentativas]**, **[!UICONTROL atraso de repetição]** e **[!UICONTROL tempo limite]** propriedades nessas configurações.

1. Em fluxos de trabalho concluídos, consulte Arquivo de fluxo de trabalho disponível em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Arquivar]**. O **[!UICONTROL Arquivo de fluxo de trabalho]** lista todas as atividades de fluxo de trabalho concluídas.

   >[!NOTE]
   >
   >Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-436](assets/chlimage_1-436.png)

1. Você recebe notificações por email sobre tarefas de fluxo de trabalho interrompidas ou com falha. Essas notificações por email podem ser configuradas por um administrador. Consulte [Configurar notificações por email](#configuring-e-mail-notifications).

#### Configurar notificações por email {#configuring-e-mail-notifications}

>[!NOTE]
>
>Você precisa de direitos administrativos para acessar o menu **[!UICONTROL Ferramentas]**.

A forma como você configura a notificação depende de se deseja notificações para trabalhos de codificação ou trabalhos de publicação do YouTube:

* Para trabalhos de codificação, você pode acessar a página de configuração para todas as notificações por email do fluxo de trabalho Experience Manager em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]** e procurando pelo **[!UICONTROL Serviço de Notificação por Email do Fluxo de Trabalho CQ do Dia]**. Consulte [Configurar notificação por email no Experience Manager](/help/sites-administering/notification.md). Você pode marcar ou desmarcar as caixas de seleção de **[!UICONTROL Notificar sobre Anular]** ou **[!UICONTROL Notificar sobre Concluído]** apropriadamente.

* Para jobs de publicação do YouTube, faça o seguinte:

1. No Experience Manager, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de Trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho, selecione **[!UICONTROL Publish para YouTube]** e **[!UICONTROL Editar]** na barra de ferramentas.
1. Próximo ao canto superior direito da página de fluxo de trabalho Publish para YouTube, selecione **[!UICONTROL Editar]**.
1. Passe o mouse sobre o componente Upload do YouTube e selecione uma vez para exibir a barra de ferramentas integrada.

   ![6_5_publishtoyoutubeworkflow](assets/6_5_publishtoyoutubeworkflow.png)

1. Na barra de ferramentas em linha, selecione o ícone Configuração (chave inglesa). Clique na guia **[!UICONTROL Argumentos]**.

   ![6_5_publishtoyoutubeworkflow-configurationicon](assets/6_5_publishtoyoutubeworkflow-configurationicon.png)

1. Na caixa de diálogo Processo de Carregamento do YouTube - Propriedades da Etapa, selecione a guia **[!UICONTROL Argumentos]**.

   ![6_5_publishtoyoutubeworkflow-arguments-tab](assets/6_5_publishtoyoutubeworkflow-arguments-tab.png)

1. Você pode marcar ou desmarcar as seguintes caixas de seleção:

   * Início da publicação
   * Falha na publicação
   * Conclusão da Publish - inclui informações sobre canais e URLs

   Desmarcar uma caixa de seleção significa que você não recebe a notificação por email especificada do fluxo de trabalho do YouTube Publish.

   >[!NOTE]
   >
   >Esses emails são específicos do YouTube e estão além das notificações por email do fluxo de trabalho genérico. Como resultado, você pode receber dois conjuntos de notificações por email: a notificação genérica disponível no **[!UICONTROL Serviço de Notificação por Email do Fluxo de Trabalho do CQ de Dias]** e uma específica do YouTube, dependendo de suas configurações.

1. Quando terminar, próximo ao canto superior direito da caixa de diálogo, selecione o ícone **[!UICONTROL Concluído]** (marca de seleção).
1. Na página de fluxo de trabalho Publish para YouTube, próximo ao canto superior direito, selecione **[!UICONTROL Sincronizar]**.

## Anotar ativos de vídeo {#annotate-video-assets}

1. No console do [!DNL Assets], selecione **[!UICONTROL Editar]** no cartão de ativos para exibir a página de detalhes do ativo.
1. Para reproduzir o vídeo, clique em **[!UICONTROL Visualizar]**.
1. Para anotar o vídeo, clique em **[!UICONTROL Anotar]**. Uma anotação é adicionada no horário específico (quadro) do vídeo. Ao anotar, é possível desenhar na tela de desenho e incluir um comentário com o desenho. Os comentários são salvos automaticamente. Para sair do assistente de anotações, clique em **[!UICONTROL Fechar]**.

   ![Draw e anotar em um quadro de vídeo](assets/annotate-video.png)

1. Procure um ponto específico no vídeo, especifique o tempo em segundos no campo de **texto** e clique em **Pular**. Por exemplo, para pular os primeiros 20 segundos de vídeo, digite 20 no campo de texto.

   ![Procure um horário em um vídeo para ignorar os segundos especificados](assets/seek-in-video.png)

1. Para exibi-la na linha do tempo, clique em uma anotação. Para excluir a anotação da linha do tempo, clique em **[!UICONTROL Excluir]**.

   ![Exibir anotações e os detalhes na linha do tempo](assets/timeline-view-annotation.png)

>[!MORELIKETHIS]
>
>* [Gerenciar ativos digitais no Experience Manager Assets](/help/assets/manage-assets.md)
>* [Gerenciar coleções no Experience Manager Assets](/help/assets/manage-collections.md)
>* [documentação de vídeo do Dynamic Media](/help/assets/video.md).
