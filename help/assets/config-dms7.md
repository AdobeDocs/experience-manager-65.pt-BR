---
title: Configurar o modo Dynamic Media - Scene7
description: Saiba como configurar o modo Dynamic Media - Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 4
exl-id: badd0f5c-2eb7-430d-ad77-fa79c4ff025a
feature: Configuration,Scene7 Mode
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '6508'
ht-degree: 3%

---

# Configurar o modo Dynamic Media - Scene7{#configuring-dynamic-media-scene-mode}

Se você usar o Adobe Experience Manager definido para ambientes diferentes, como desenvolvimento, preparo e produção, configure o Dynamic Media Cloud Service para cada um desses ambientes.

## Diagrama de arquitetura do modo Dynamic Media - Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

O diagrama de arquitetura a seguir descreve como o modo Dynamic Media - Scene7 funciona.

Com a nova arquitetura, o Experience Manager é responsável pelos ativos de origem principal e sincroniza com o Dynamic Media para o processamento e a publicação de ativos:

1. Quando o ativo de origem principal é carregado no Experience Manager, ele é replicado para o Dynamic Media. Nesse ponto, o Dynamic Media lida com todo o processamento de ativos e a geração de representações, como a codificação de vídeo e as variantes dinâmicas de uma imagem.
(No modo Dynamic Media - Scene7, o tamanho padrão do arquivo de upload é de 2 GB ou menos. Para habilitar o tamanho dos arquivos de upload de 2 GB até 15 GB, consulte [(Opcional) Configurar Dynamic Media - Modo Scene7 para o upload de ativos maiores que 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. Depois que as representações são geradas, o Experience Manager pode acessar e pré-visualizar com segurança as representações remotas do Dynamic Media (nenhum binário é enviado de volta para a instância do Experience Manager).
1. Depois que o conteúdo está pronto para ser publicado e aprovado, ele aciona o serviço do Dynamic Media para enviar o conteúdo para os servidores de entrega e armazená-lo em cache na CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>A lista de recursos a seguir requer o uso da CDN integrada que acompanha o Adobe Experience Manager - Dynamic Media. Nenhum outro CDN personalizado é compatível com esses recursos.
>
>* [Imagem inteligente](/help/assets/imaging-faq.md)
>* [Invalidação de cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Proteção de hotlink](/help/assets/hotlink-protection.md)
>* [Entrega de conteúdo HTTP/2](/help/assets/http2.md)
>* Redirecionamento de URL no nível da CDN
>* Akamai ChinaCDN (para entrega ideal na China)

## Ativar o Dynamic Media no modo Scene7 {#enabling-dynamic-media-in-scene-mode}

O [Dynamic Media](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) está desabilitado por padrão. Para aproveitar os recursos do Dynamic Media, é necessário ativá-lo.

>[!WARNING]
>
>Dynamic Media - O modo Scene7 é somente para a *instância do Experience Manager Author*. Dessa forma, você deve configurar `runmode=dynamicmedia_scene7` na instância do Autor do Experience Manager, *não* na instância do Publish do Experience Manager.

Para habilitar o Dynamic Media, inicialize o Experience Manager usando o modo de execução `dynamicmedia_scene7` na linha de comando digitando o seguinte em uma janela de terminal (a porta de exemplo usada é 4502):

```shell {.line-numbers}
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Opcional) Migração de predefinições e configurações do Dynamic Media de 6.3 para 6.5, sem tempo de inatividade {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

A atualização do Experience Manager Dynamic Media de 6.3 para 6.4 ou 6.5 agora inclui a capacidade de implantações sem tempo de inatividade. Para migrar todas as suas predefinições e configurações do `/etc` para o `/conf` em CRXDE Lite, execute o seguinte comando curl.

>[!NOTE]
>
>Se você executar a instância do Experience Manager no modo de compatibilidade, ou seja, se o pacote de compatibilidade estiver instalado, não será necessário executar esses comandos.

Para todas as atualizações, com ou sem o pacote de compatibilidade, você pode copiar as predefinições do visualizador padrão prontas para uso que vieram originalmente com o Dynamic Media executando o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar qualquer predefinição e configuração personalizada do visualizador criada de `/etc` para `/conf`, execute o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Instalar o pacote de recursos 18912 para migração de ativos em massa {#installing-feature-pack-for-bulk-asset-migration}

A instalação do pacote de recursos 18912 é *opcional*.

O Feature Pack 18912 permite assimilar ativos em massa por meio do FTP ou migrar ativos do Dynamic Media - modo híbrido ou do Dynamic Media Classic para o Dynamic Media - modo Scene7 no Experience Manager. Ele está disponível em [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Consulte [Instalar o pacote de recursos 18912 para migração de ativos em massa](/help/assets/bulk-ingest-migrate.md) para obter mais informações.

## Criar uma configuração do Dynamic Media no Cloud Service {#configuring-dynamic-media-cloud-services}

<!-- **Before you configure Dynamic Media** - After you receive your provisioning email with Dynamic Media credentials, you must open the [Dynamic Media Classic desktop application](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), then sign in to your account to change your password. The password provided in the provisioning email is system-generated and intended to be a temporary password only. It is important that you update the password so that Dynamic Media Cloud Service is set up with the correct credentials.

   ![dynamicmediaconfiguration2updated](assets/dynamicmediaconfiguration2updated.png)

**To create a Dynamic Media Configuration in Cloud Services:** -->

1. No modo Experience Manager Author, selecione o logotipo do Experience Manager para acessar o console de navegação global, selecione o ícone Tools e acesse **[!UICONTROL Cloud Service]** > **[!UICONTROL Dynamic Media Configuration]**.
1. Na página Navegador de Configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**) e **[!UICONTROL Criar]**.
1. Na página **[!UICONTROL Criar configuração do Dynamic Media]**, digite um título, o endereço de email da conta do Dynamic Media, a senha e selecione sua região. Essas informações são fornecidas pelo Adobe no e-mail de provisionamento. Entre em contato com o Suporte ao cliente do Adobe se não receber o email.

   Selecione **[!UICONTROL Conectar ao Dynamic Media]**.

1. Na caixa de diálogo **[!UICONTROL Alterar Senha]**, no campo **[!UICONTROL Nova Senha]**, digite uma nova senha que contenha de 8 a 25 caracteres. A senha deve conter pelo menos um dos seguintes itens:

   * Letra maiúscula
   * Letra minúscula
   * Número
   * Caractere especial: `# $ & . - _ : { }`

   O campo **[!UICONTROL Senha Atual]** foi intencionalmente preenchido previamente e está oculto na interação.

   Se necessário, você pode verificar a ortografia de uma senha digitada ou digitada novamente selecionando o ícone de olho da senha para revelar a senha. Selecione o ícone novamente para ocultar a senha.

1. No campo **[!UICONTROL Repetir Senha]**, digite novamente a nova senha e selecione **[!UICONTROL Concluído]**.

   A nova senha é salva ao selecionar **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Criar configuração do Dynamic Media]**.

   Se você selecionou **[!UICONTROL Cancelar]** na caixa de diálogo **[!UICONTROL Alterar senha]**, ainda deverá digitar uma nova senha ao salvar a configuração do Dynamic Media recém-criada.

   Consulte também [Alterar a senha para Dynamic Media](#change-dm-password).

1. Quando a conexão for bem-sucedida, defina o seguinte. Cabeçalhos com um asterisco (*) são obrigatórios:

   * **[!UICONTROL Empresa]** - o nome da conta do Dynamic Media.

     >[!IMPORTANT]
     >
     >Somente uma configuração Dynamic Media no Cloud Service é suportada em uma instância de Experience Manager; não adicione mais de uma configuração. Várias Configurações do Dynamic Media em uma instância Experience Manager _não_ suportadas ou recomendadas pelo Adobe.

     <!-- CQDOC-19579 and CQDOC-19612 -->

     Consulte também [Configurar conta alias da empresa Dynamic Media](/help/assets/dm-alias-account.md).

   * **[!UICONTROL Caminho da Pasta Raiz da Empresa]**

   * **[!UICONTROL Publicando Assets]** - Você pode escolher entre as três opções a seguir:
      * **[!UICONTROL Imediatamente]** significa que quando os ativos são carregados, o sistema assimila os ativos e fornece a URL/Incorporar instantaneamente. Não há necessidade de intervenção do usuário para publicar ativos.
      * **[!UICONTROL Na ativação]** significa que você deve publicar explicitamente o ativo primeiro, antes que um link de URL/Incorporação seja fornecido.<br><!-- CQDOC-17478, Added March 9, 2021-->A partir do Experience Manager 6.5.8, a instância do Publish do Experience Manager reflete valores precisos de metadados do Dynamic Media, como `dam:scene7Domain` e `dam:scene7FileStatus` somente no modo de publicação **[!UICONTROL Na Ativação]**. Para ativar essa funcionalidade, instale o Service Pack 8 e reinicie o Experience Manager. Acesse o Sling Config Manager. Localize a configuração de `Scene7ActivationJobConsumer Component` ou crie uma nova). Marque a caixa de seleção **[!UICONTROL Replicar metadados após a publicação do Dynamic Media]** e selecione **[!UICONTROL Salvar]**.

        ![Replicar metadados após a caixa de seleção de publicação do Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Publish seletiva]** Essa opção permite controlar quais pastas são publicadas no Dynamic Media. Ele permite usar recursos como Recorte inteligente ou representações dinâmicas, ou determinar quais pastas são publicadas exclusivamente no Experience Manager para visualização. Esses mesmos ativos *não* foram publicados no Dynamic Media para entrega no domínio público.<br>Você pode definir esta opção aqui na **[!UICONTROL Configuração da Dynamic Media Cloud]** ou, se preferir, pode optar por definir esta opção no nível da pasta, nas **[!UICONTROL Propriedades]** de uma pasta.<br>Consulte [Trabalhar com Publish Seletiva no Dynamic Media](/help/assets/selective-publishing.md).<br>Se você alterar esta configuração posteriormente ou alterá-la no nível da pasta, essas alterações afetarão somente os novos ativos carregados a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente da caixa de diálogo **[!UICONTROL Publish Rápido]** ou **[!UICONTROL Gerenciar Publicação]**.

   * **[!UICONTROL Servidor de Visualização Seguro]** - permite que você especifique o caminho da URL para seu servidor de visualização de representações seguras. Ou seja, depois que as representações são geradas, o Experience Manager pode acessar e pré-visualizar com segurança as representações remotas do Dynamic Media (nenhum binário é enviado de volta para a instância do Experience Manager).
A menos que você tenha uma organização especial para usar o servidor de sua própria empresa ou um servidor especial, a Adobe recomenda que você deixe essa configuração conforme especificado.

   * **[!UICONTROL Sincronizar todo o conteúdo]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Selecionado por padrão. Desmarque essa opção se desejar incluir ou excluir seletivamente ativos da sincronização com o Dynamic Media. Desmarcar essa opção permite escolher entre os dois modos de sincronização do Dynamic Media a seguir:

   * **[!UICONTROL Modo de sincronização do Dynamic Media]**
      * **[!UICONTROL Habilitado por padrão]** - A configuração é aplicada a todas as pastas por padrão, a menos que você marque uma pasta especificamente para exclusão. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Desabilitado por padrão]** - A configuração não é aplicada a nenhuma pasta até que você marque explicitamente uma pasta selecionada para sincronização com o Dynamic Media.
Para marcar uma pasta selecionada para sincronização com o Dynamic Media, selecione uma pasta de ativos e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**. Na guia **[!UICONTROL Detalhes]**, na lista suspensa **[!UICONTROL Modo de sincronização do Dynamic Media]**, escolha uma das três opções a seguir. Quando terminar, selecione **[!UICONTROL Salvar]**. *Lembre-se: estas três opções não estarão disponíveis se você tiver selecionado **[!UICONTROL Sincronizar todo o conteúdo]**&#x200B;anteriormente.* Consulte também [Trabalhar com Publish seletiva no nível da pasta no Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Herdado]** - Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão na configuração de nuvem. O status detalhado de herdado é exibido por meio de uma dica de ferramenta.
         * **[!UICONTROL Habilitar para subpastas]** - Incluir tudo nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem o modo padrão na configuração da nuvem.
         * **[!UICONTROL Desabilitado para subpastas]** - Exclua tudo nesta subárvore da sincronização com o Dynamic Media.

   >[!NOTE]
   >
   >Não há suporte para o controle de versão no modo Dynamic Media - Scene7. Além disso, a ativação atrasada se aplica somente se **[!UICONTROL Publicar ativos]** na página Editar configuração do Dynamic Media estiver definida como **[!UICONTROL Na ativação]** e, em seguida, somente até a primeira vez que o ativo for ativado.
   >
   >Depois que um ativo é ativado, todas as atualizações são publicadas imediatamente no Delivery S7.

1. Selecione **[!UICONTROL Salvar]**.
1. Para visualizar com segurança o conteúdo do Dynamic Media antes de ele ser publicado, o Autor do Experience Manager usa a validação baseada em token e, portanto, o Autor do Experience Manager visualiza o conteúdo do Dynamic Media por padrão. No entanto, você pode &quot;incluir na lista de permissões&quot; mais IPs para fornecer aos usuários acesso à visualização segura do conteúdo. Para configurar essa ação no Experience Manager, consulte [Configurar a configuração do Dynamic Media Publish para o servidor de imagens - guia Segurança](/help/assets/dm-publish-settings.md#security-tab).

Se quiser personalizar ainda mais sua configuração, como habilitar permissões de ACL (Access Control List, Lista de Controle de Acesso), você poderá, opcionalmente, concluir qualquer uma das tarefas em [(Opcional) Definir Configurações Avançadas no modo Dynamic Media - Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

<!-- 1. To securely preview Dynamic Media content before it gets published, Experience Manager uses token-based validation and hence Experience Manager Author previews Dynamic Media content by default. However, you can *allowlist* more IPs to provide users access to securely preview content. To set up this action in Experience Manager, see [Configure Dynamic Media Publish Setup for Image Server - Security tab](/help/assets/dm-publish-settings.md#security-tab).     * In Experience Manager Author mode, select the Experience Manager logo to access the global navigation console.
    * In the left rail, select the **[!UICONTROL Tools]** icon, then go to **[!UICONTROL Assets]** > **[!UICONTROL Dynamic Media Publish Setup]**.
    * On the Dynamic Media Image Server page, in the **[!UICONTROL Publish Context]** drop-down list, select **[!UICONTROL Test Image Serving]**.
    * Select the **[!UICONTROL Security]** tab.
    * For the **[!UICONTROL Client address]**, select **[!UICONTROL Add]**.
    * Enter the IP address of the Experience Manager Author instance (not Dispatcher IP).
    * In the upper-right corner of the page, select **[!UICONTROL Save]**. -->

Agora você concluiu a configuração básica; você está pronto para usar o modo Dynamic Media - Scene7.

### Altere a senha para Dynamic Media {#change-dm-password}

A expiração da senha no Dynamic Media está definida como 100 anos a partir da data atual do sistema.

A senha deve conter pelo menos um dos seguintes itens:

* Letra maiúscula
* Letra minúscula
* Número
* Caractere especial: `# $ & . - _ : { }`

Se necessário, você pode verificar a ortografia de uma senha digitada ou digitada novamente selecionando o ícone de olho da senha para revelar a senha. Selecione o ícone novamente para ocultar a senha.

A senha alterada é salva quando você seleciona **[!UICONTROL Salvar]** no canto superior direito da página **[!UICONTROL Editar Configuração do Dynamic Media]**.

**Para alterar a senha para o Dynamic Media:**

1. No modo Experience Manager Author, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. À esquerda do console, selecione o ícone Ferramentas e vá para **[!UICONTROL Cloud Service] > [!UICONTROL Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]**. Não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**. Em seguida, selecione **[!UICONTROL Editar]**.
1. Na página **[!UICONTROL Editar Configuração do Dynamic Media]**, logo abaixo do campo **[!UICONTROL Senha]**, selecione **[!UICONTROL Alterar Senha]**.
1. Na caixa de diálogo **[!UICONTROL Alterar Senha]**, faça o seguinte:

   * No campo **[!UICONTROL Nova Senha]**, digite uma nova senha.

     O campo **[!UICONTROL Senha Atual]** foi intencionalmente preenchido previamente e está oculto na interação.

   * No campo **[!UICONTROL Repetir Senha]**, digite novamente a nova senha e selecione **[!UICONTROL Concluído]**.

1. No canto superior direito da página **[!UICONTROL Editar Configuração do Dynamic Media]**, selecione **[!UICONTROL Salvar]** e **[!UICONTROL OK]**.

## (Opcional) Definir configurações avançadas no modo Dynamic Media - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

Se quiser personalizar ainda mais a configuração do Dynamic Media - modo Scene7 ou otimizar seu desempenho, conclua uma ou mais das seguintes tarefas *opcionais*:

* [(Opcional) Ativar permissões de ACL no modo Dynamic Media - Scene7](#optional-enable-acl)

* [(Opcional) Configure o modo Dynamic Media - Scene7 para carregar ativos maiores que 2 GB](#optional-config-dms7-assets-larger-than-2gb)

* [(Opcional) Instalação e configuração do Dynamic Media - configurações do modo Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Opcional) Ajuste o desempenho do modo Dynamic Media - Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Opcional) Filtrar ativos para replicação](#optional-filtering-assets-for-replication)

### (Opcional) Ativar permissões da Lista de controle de acesso no modo Dynamic Media - Scene7 {#optional-enable-acl}

Quando você executa o Dynamic Media - Scene7 mode no AEM, ele encaminha atualmente `/is/image` solicitações para o Servidor de imagens de visualização segura sem verificar as permissões de ACL (Access Control List, Lista de controle de acesso) no PlatformServerServlet. No entanto, você pode *habilitar* permissões de ACL. Isso encaminha as solicitações `/is/image` autorizadas. Se um usuário não estiver autorizado a acessar o ativo, um erro &quot;403 - Proibido&quot; será exibido.

**Para habilitar permissões de ACL no Dynamic Media - modo Scene7:**

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   ![13-16-08-2019](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta na página **[!UICONTROL Configuração do Adobe Experience Manager Web Console]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role até o nome *Adobe CQ Scene7 PlatformServer*.

1. À direita do nome, selecione o ícone de lápis (**[!UICONTROL Editar os valores de configuração]**).

1. Na página **com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.name**, marque a caixa de seleção das duas configurações a seguir:

   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.cache.enable.name` - Quando habilitada, essa configuração armazena em cache os resultados da permissão por 120 segundos (dois minutos) (padrão) para salvar.
   * `com.adobe.cq.dam.s7imaging.impl.ps.PlatformServerServlet.validate.userAccess.name` - Quando habilitada, essa configuração valida o acesso de um usuário enquanto ele visualiza ativos por meio do Dynamic Media Image Server.

   ![Habilitar configurações da Lista de Controle de Acesso no Dynamic Media - modo Scene7](/help/assets/assets-dm/acl.png)

1. Próximo ao canto inferior direito da página, selecione **[!UICONTROL Salvar]**.

### (Opcional) Configure o modo Dynamic Media - Scene7 para carregar ativos maiores que 2 GB {#optional-config-dms7-assets-larger-than-2gb}

No modo Dynamic Media - Scene7, o tamanho padrão do arquivo de upload de ativos é de 2 GB ou menos. No entanto, é possível configurar opcionalmente o upload de ativos maiores que 2 GB e até 15 GB.

Se você pretende usar esse recurso, esteja ciente dos seguintes pré-requisitos e pontos:

* Você deve executar o Experience Manager 6.5 com o Service Pack 6.5.4.0 ou posterior no modo Dynamic Media - Scene7.
* Este grande recurso de carregamento só tem suporte para clientes do [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html).
* Verifique se a instância do Experience Manager está configurada com o armazenamento Amazon S3 ou Microsoft® Azure Blob.

  >[!NOTE]
  >
  >Configure o armazenamento do Azure Blob com uma chave de acesso e uma chave secreta porque esse grande recurso de upload não é compatível com o AzureSas na configuração de armazenamento do Blob.

* O [download de Acesso Binário Direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) da Oak está habilitado (o *upload de Acesso Binário Direto* da Oak não é necessário).

  Para habilitar o download do Acesso Binário Direto, defina a propriedade `presignedHttpDownloadURIExpirySeconds > 0` na configuração do armazenamento de dados. O valor deve ser longo o suficiente para baixar binários maiores e possivelmente tentar novamente.

* Assets maiores que 15 GB não são carregados. (O limite de tamanho é definido na etapa 8 abaixo.)
* Quando o fluxo de trabalho **[!UICONTROL Reprocessamento de ativos do Dynamic Media]** é acionado em uma pasta, ele reprocessa todos os ativos grandes que já estão em sincronia com a empresa do Dynamic Media. No entanto, se algum ativo grande ainda não estiver sincronizado na pasta, ele não fará upload do ativo. Portanto, para sincronizar ativos grandes existentes no Dynamic Media, você pode executar o fluxo de trabalho **[!UICONTROL Reprocessamento de ativos do Dynamic Media]** em ativos individuais.

**Para configurar o Dynamic Media - modo Scene7 para carregar ativos com mais de 2 GB:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

1. Na janela do CRXDE Lite, execute um dos procedimentos a seguir:

   * No painel à esquerda, navegue até o seguinte caminho:

     `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie e cole o caminho acima no campo do caminho de CRXDE Lite abaixo da barra de ferramentas e pressione `Enter`.

1. No painel à esquerda, clique com o botão direito do mouse em `fileupload` e, no menu pop-up, selecione **[!UICONTROL Sobrepor Nó]**.

   ![Opção Sobrepor Nó](/help/assets/assets-dm/uploadassets15gb_a.png)

1. Na caixa de diálogo Sobrepor Nó, marque a caixa de seleção **[!UICONTROL Corresponder Tipos de Nó]** para habilitar (ativar) a opção e, em seguida, selecione **[!UICONTROL OK]**.

   ![Caixa de diálogo Sobrepor Nó](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Na janela CRXDE Lite, execute um dos procedimentos a seguir:

   * No painel à esquerda, navegue até o seguinte caminho de nó de sobreposição:

     `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie e cole o caminho acima no campo do caminho de CRXDE Lite abaixo da barra de ferramentas e pressione `Enter`.

1. Na guia **[!UICONTROL Propriedades]**, na coluna **[!UICONTROL Nome]**, localize `sizeLimit`.
1. À direita do nome `sizeLimit`, na coluna **[!UICONTROL Value]**, clique duas vezes no campo de valor.
1. Insira o valor apropriado em bytes para que você possa aumentar o limite de tamanho para o tamanho máximo desejado para o upload. Por exemplo, para aumentar o limite de tamanho do ativo de carregamento para 10 GB, insira `10737418240` no campo de valor.
Você pode inserir um valor de até 15 GB (`2013265920` bytes). Nesse caso, ativos carregados com mais de 15 GB não são carregados.

   ![Valor de limite de tamanho](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Próximo ao canto superior esquerdo da janela do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

   *Agora defina o tempo limite para o Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite fazendo o seguinte:*

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global.
1. Siga um destes procedimentos:

   * Navegue até o seguinte caminho de URL:

     `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copie e cole o caminho acima no campo URL do seu navegador. Certifique-se de substituir `localhost:4502` pela sua própria instância do Experience Manager.

1. Na caixa de diálogo **[!UICONTROL Manipulador de trabalho do processo externo do fluxo de trabalho do Adobe Granite]**, no campo **[!UICONTROL Tempo limite máximo]**, defina o valor como `18000` segundos (cinco horas). O padrão é 10.800 segundos (três horas).

   ![Valor de tempo limite máximo](/help/assets/assets-dm/uploadassets15gb_d.png)

1. No canto inferior direito da caixa de diálogo, selecione **[!UICONTROL Salvar]**.

   *Agora defina o tempo limite para a etapa do processo de Carregamento Binário Direto do Scene7 fazendo o seguinte:*

1. Em Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global.
1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho, selecione **[!UICONTROL Codificação de vídeo Dynamic Media]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**.
1. Na página de fluxo de trabalho, clique duas vezes na etapa de processo **[!UICONTROL Upload binário direto do Scene7]**.
1. Na caixa de diálogo **[!UICONTROL Propriedades da Etapa]**, na guia **[!UICONTROL Comum]**, no cabeçalho **[!UICONTROL Configurações Avançadas]**, no campo **[!UICONTROL Tempo Limite]**, insira um valor de `18000` segundos (cinco horas). O padrão é `3600` segundos (uma hora).
1. Selecione **[!UICONTROL OK]**.
1. Selecione **[!UICONTROL Sincronizar]**.
1. Repita as etapas 14 a 21 para o modelo de fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]** e o modelo de fluxo de trabalho **[!UICONTROL Reprocessamento do Dynamic Media]**.

### (Opcional) Instalação e configuração do Dynamic Media - configurações do modo Scene7 {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

<!-- When you are in run mode `dynamicmedia_scene7`, use the Dynamic Media Classic user interface to change your Dynamic Media settings. -->

* [Configurar a configuração do Dynamic Media Publish para o servidor de imagens](/help/assets/dm-publish-settings.md)
* [Definir configurações gerais do Dynamic Media](/help/assets/dm-general-settings.md)
* [Configurar gerenciamento de cores](#configuring-color-management)
* [Editar tipos MIME para formatos compatíveis](#editing-mime-types-for-supported-formats)
* [Adicionar tipos MIME para formatos não suportados](#adding-mime-types-for-unsupported-formats)
* [Criar predefinições de conjunto de lotes para gerar automaticamente Conjuntos de Imagens e Conjuntos de Rotação](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) (concluído na interface do usuário do Dynamic Media Classic)

#### Configurar a configuração do Dynamic Media Publish para o servidor de imagens {#publishing-setup-for-image-server}

A página Configuração do Dynamic Media Publish estabelece configurações padrão que determinam como os ativos são entregues de servidores Adobe Dynamic Media para sites ou aplicativos.

Consulte [Configurar a Instalação do Dynamic Media Publish para o Servidor de Imagens](/help/assets/dm-publish-settings.md).

#### Definir configurações gerais do Dynamic Media {#configuring-application-general-settings}

Configure a URL do Dynamic Media **[!UICONTROL Nome do Servidor do Publish]** e a URL do **[!UICONTROL Nome do Servidor de Origem]**. Você também pode especificar as configurações de **[!UICONTROL Carregar no Aplicativo]** e **[!UICONTROL Opções de Carregamento Padrão]**, todas com base no seu caso de uso específico.

Consulte [Definir Configurações Gerais do Dynamic Media](/help/assets/dm-general-settings.md).

#### Configurar gerenciamento de cores {#configuring-color-management}

O gerenciamento de cores do Dynamic Media permite corrigir as cores dos ativos. Com a correção de cores, os ativos assimilados mantêm o espaço de cores (RGB, CMYK, Cinza) e o perfil de cores incorporado. Quando você solicita uma representação dinâmica, a cor da imagem é corrigida no espaço de cores de destino usando a saída CMYK, RGB ou Cinza.

Consulte [Configurar predefinições de imagem](/help/assets/managing-image-presets.md).

>[!NOTE]
>
>Por padrão, o sistema mostra 15 execuções ao selecionar **[!UICONTROL Representações]** e 15 predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição de Detalhes do ativo. Você pode aumentar esse limite. Consulte [Aumentar o número de predefinições de imagens exibidas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar o número de predefinições do visualizador exibidas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

#### Editar tipos MIME para formatos compatíveis {#editing-mime-types-for-supported-formats}

Você pode definir quais tipos de ativos são processados pelo Dynamic Media e personalizar os parâmetros avançados de processamento de ativos. Por exemplo, você pode especificar parâmetros de processamento de ativos para fazer o seguinte:

* Converter um Adobe PDF em um ativo de eCatalog.
* Converta um documento do Adobe Photoshop (.PSD) em um ativo de modelo de banner para personalização.
* Rasterize um arquivo Adobe Illustrator (.AI) ou um arquivo PostScript® encapsulado Adobe Photoshop (.EPS).
* [Perfis de vídeo](/help/assets/video-profiles.md) e [Perfis de imagem](/help/assets/image-profiles.md) podem ser usados para definir o processamento de vídeos e imagens, respectivamente.

Consulte [Carregando Assets](/help/assets/manage-assets.md#uploading-assets).

**Para editar tipos MIME para formatos com suporte:**

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No painel à esquerda, navegue até o seguinte:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. Na pasta mimeTypes, selecione um tipo mime.
1. No lado direito da página de CRXDE Lite, na parte inferior:

   * Clique duas vezes no campo **[!UICONTROL habilitado]**. Por padrão, todos os tipos MIME de ativos estão habilitados (definidos como **[!UICONTROL true]**), o que significa que os ativos estão sincronizados com o Dynamic Media para processamento. Se você deseja excluir este tipo de ativo mime de ser processado, altere esta configuração para **[!UICONTROL false]**.

   * Selecione duas vezes **[!UICONTROL jobParam]** para abrir seu campo de texto associado. Consulte [Tipos MIME suportados](/help/assets/assets-formats.md#supported-mime-types) para obter uma lista de valores de parâmetro de processamento permitidos que você pode usar para um determinado tipo MIME.

1. Siga uma das seguintes opções:

   * Repita as etapas 3 a 4 para editar mais tipos MIME.
   * Na barra de menus da página de CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página, selecione **[!UICONTROL CRXDE Lite]** para retornar ao Experience Manager.

#### Adição de tipos MIME para formatos não compatíveis {#adding-mime-types-for-unsupported-formats}

Você pode adicionar tipos MIME personalizados para formatos não compatíveis com o Experience Manager Assets. Certifique-se de que qualquer novo nó adicionado no CRXDE Lite não seja excluído pelo Experience Manager movendo o tipo MIME antes de `image_`. Além disso, verifique se o valor habilitado está definido como **[!UICONTROL false]**.

**Para adicionar tipos MIME para formatos sem suporte:**

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   ![13-16-08-2019](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta na página **[!UICONTROL Configuração do Adobe Experience Manager Web Console]**.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role para baixo até o nome *Adobe CQ Scene7 Asset MIME type Service*, como visto na seguinte captura de tela. À direita do nome, selecione **[!UICONTROL Editar os valores de configuração]** (ícone de lápis).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. Na página **Adobe CQ Scene7 Asset MIME type Service**, selecione qualquer ícone de sinal de adição &lt;+>. O local na tabela onde você seleciona o sinal de adição para adicionar o novo tipo MIME é trivial.

   ![27-08-2019-02_16-27](assets/2019-08-02_16-27-27.png)

1. Digite `DWG=image/vnd.dwg` no campo de texto vazio que você acabou de adicionar.

   O exemplo `DWG=image/vnd.dwg` é somente para fins de demonstração. O tipo MIME adicionado aqui pode ser qualquer outro formato não suportado.

   ![08-2019-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. No canto inferior direito da página, selecione **[!UICONTROL Salvar]**.

   Nesse ponto, é possível fechar a guia do navegador que tem a página aberta Configuração do console da Web do Adobe Experience Manager.

1. Retorne à guia do navegador que tem o console de Experience Manager aberto.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. No painel à esquerda, navegue até o seguinte:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arraste o tipo MIME `image_vnd.dwg` e solte-o diretamente acima de `image_` na árvore, como visto na seguinte captura de tela.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Com o tipo mime `image_vnd.dwg` ainda selecionado, na guia **[!UICONTROL Propriedades]**, na linha **[!UICONTROL habilitada]**, no cabeçalho da coluna **[!UICONTROL Valor]**, selecione duas vezes o valor para abrir a lista suspensa **[!UICONTROL Valor]**.
1. Digite `false` no campo (ou selecione **[!UICONTROL false]** na lista suspensa).

   ![08-2019-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Próximo ao canto superior esquerdo da página de CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

#### Criar predefinições de conjunto de lotes para gerar automaticamente conjuntos de imagens e conjuntos de rotação {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

Use predefinições de conjunto de lotes para automatizar a criação de conjuntos de imagens ou conjuntos de rotação enquanto os ativos são carregados no Dynamic Media.

Primeiro, defina a convenção de nomenclatura para como os ativos são agrupados em um conjunto. Em seguida, crie uma predefinição de conjunto de lotes que seja um conjunto de instruções com nome exclusivo e independente. Ele deve definir como construir o conjunto usando imagens que correspondam às convenções de nomenclatura definidas na fórmula predefinida.

Ao fazer upload de arquivos, o Dynamic Media cria automaticamente um conjunto com todos os arquivos que correspondem à convenção de nomenclatura definida nas predefinições ativas.

##### Configurar nomenclatura padrão

Crie uma convenção de nomenclatura padrão que seja usada em qualquer fórmula predefinida de conjunto de lotes. A convenção de nomenclatura padrão selecionada na definição de predefinição de conjunto de lotes é provavelmente tudo o que é necessário para a empresa gerar conjuntos em lote. Uma predefinição de conjunto de lotes é criada para usar a convenção de nomenclatura padrão que você define. É possível criar quantas predefinições de Conjunto de Lotes precisarem com convenções de nomenclatura alternativas e personalizadas para um conjunto específico de conteúdo nos casos em que houver uma exceção à nomenclatura padrão definida pela empresa.

Embora a configuração de uma convenção de nomenclatura padrão não seja necessária para usar a funcionalidade de predefinição de conjunto de lotes, a prática recomendada é usar a convenção de nomenclatura padrão. Ela permite definir quantos elementos de sua convenção de nomenclatura você quiser agrupar em um conjunto, de modo que possa simplificar a criação do conjunto de lotes.

Como alternativa, você pode usar **[!UICONTROL Exibir Código]** sem campos de formulário disponíveis. Nesta visualização, você cria suas definições de convenção de nomenclatura inteiramente usando expressões regulares.

Dois elementos estão disponíveis para definição: Correspondência e Nome de base. Esses campos permitem definir todos os elementos de uma convenção de nomenclatura e identificar a parte da convenção usada para nomear o conjunto no qual eles estão contidos. A convenção de nomenclatura individual de uma empresa geralmente usa uma ou mais linhas de definição para cada um desses elementos. É possível usar quantas linhas forem necessárias para a definição exclusiva e agrupá-las em elementos distintos, como Imagem principal, Elemento de cor, Elemento de exibição alternativa e Elemento de amostra.

**Para configurar a nomeação padrão:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente da Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Predefinições do Conjunto de Lotes]** > **[!UICONTROL Nomeação Padrão]**.
1. Selecione **[!UICONTROL Exibir formulário]** ou **[!UICONTROL Exibir código]** para especificar como deseja exibir e inserir informações sobre cada elemento.

   Você pode marcar a caixa de seleção **[!UICONTROL Exibir código]** para exibir a compilação do valor de expressão regular ao lado das seleções de formulário. Você pode inserir ou alterar esses valores para ajudar a definir os elementos da convenção de nomenclatura, se a exibição do formulário limitar você por qualquer motivo. Se os valores não puderem ser analisados no modo de exibição de formulário, os campos de formulário ficarão inativos.

   >[!NOTE]
   >
   >Os campos de formulário desativados não executam nenhuma validação de que suas expressões regulares estão corretas. Você vê os resultados da expressão regular que está criando para cada elemento após a linha Resultado. A expressão regular completa é visível na parte inferior da página.

1. Expanda cada elemento conforme necessário e insira as convenções de nomenclatura que deseja usar.
1. Conforme necessário, execute um dos procedimentos a seguir:

   * Selecione **[!UICONTROL Adicionar]** para adicionar outra convenção de nomenclatura para um elemento.
   * Selecione **[!UICONTROL Remover]** para excluir uma convenção de nomenclatura de um elemento.

1. Siga uma das seguintes opções:

   * Selecione **[!UICONTROL Salvar como]** e digite um nome para a predefinição.
   * Selecione **[!UICONTROL Salvar]** se estiver editando uma predefinição existente.

##### Criar uma predefinição de conjunto de lotes

O Dynamic Media usa predefinições de conjunto de lotes para organizar ativos em conjuntos de imagens (imagens alternativas, opções de cor, rotação de 360) para exibição em visualizadores. As predefinições de conjunto de lotes são executadas automaticamente junto com os processos de upload de ativos no Dynamic Media.

É possível criar, editar e gerenciar predefinições de conjunto de lotes. Há duas formas de definições de predefinições de conjunto de lotes: uma para uma convenção de nomenclatura padrão que você pode configurar e outra para convenções de nomenclatura personalizadas que você cria dinamicamente.

Você pode usar o método de campo de formulário para definir uma predefinição de conjunto de lotes ou o método de código, que permite usar expressões regulares. Como na Nomeação padrão, você pode escolher Exibir código ao mesmo tempo em que está definindo na Exibição de formulário e usar expressões regulares para criar suas definições. Como alternativa, você pode desmarcar qualquer exibição para usar uma ou a outra exclusivamente.

**Para criar uma Predefinição de conjunto de lotes:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente da Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Predefinição do conjunto de lotes]**.

   O **[!UICONTROL Exibir Formulário]**, conforme definido no canto superior direito da página Detalhes, é o modo de exibição padrão.

1. No painel Lista de predefinições, selecione **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição, digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lote, selecione um tipo de predefinição.
1. Siga uma das seguintes opções:

   * Se você estiver usando uma convenção de nomenclatura padrão configurada anteriormente em **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Predefinições do Conjunto de Lotes]** > **[!UICONTROL Nomeação Padrão]**, expanda **[!UICONTROL Convenções de Nomeação de Ativos]** e, na lista suspensa Nomeação de Arquivos, selecione **[!UICONTROL Padrão]**.

   * Para definir uma nova convenção de nomenclatura conforme configura a predefinição, expanda **[!UICONTROL Convenções de nomenclatura de ativos]** e, na lista suspensa Nomenclatura de arquivos, selecione **[!UICONTROL Personalizado]**.

1. Para Ordem de sequência, defina a ordem em que as imagens são exibidas depois que o conjunto é agrupado no Dynamic Media.

   Por padrão, seus ativos são ordenados alfanumericamente. No entanto, você pode usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

1. Em Definir convenção de nomeação e criação, especifique o sufixo ou prefixo para o nome base definido na Convenção de nomeação de ativos. Além disso, defina onde o conjunto é criado na estrutura de pastas do Dynamic Media.

   Se você definir um grande número de conjuntos, mantenha os conjuntos separados das pastas que contêm os próprios ativos. Por exemplo, crie uma pasta de Conjuntos de imagens e coloque os conjuntos gerados aqui.

1. No painel Detalhes, selecione **[!UICONTROL Salvar]**.
1. Selecione **[!UICONTROL Ativo]** ao lado do novo nome de predefinição.

   A ativação da predefinição garante que, ao fazer upload de ativos para o Dynamic Media, a predefinição de conjunto de lotes seja aplicada para gerar o conjunto.

##### Criar uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D

Você pode usar o Tipo de conjunto de lotes **[!UICONTROL Conjunto de rotação com vários eixos]** para criar uma fórmula que automatize a geração de conjuntos de rotação 2D. O agrupamento de imagens usa expressões regulares de Linha e Coluna para que os ativos de imagem sejam alinhados corretamente no local correspondente na matriz multidimensional. Não há número mínimo ou máximo de linhas ou colunas que você deve ter em um conjunto de rotação multieixo.

Por exemplo, suponha que você queira criar um conjunto de rotação multieixo chamado `spin-2dspin`. Você tem um conjunto de imagens do conjunto de rotação que contém três linhas, com 12 imagens por linha. As imagens são nomeadas da seguinte maneira:

```xml {.line-numbers}
spin-01-01
 spin-01-02
 …
 spin-01-12
 spin-02-01
 …
 spin-03-12
```

Com essas informações, a fórmula Tipo de conjunto de lotes pode ser criada da seguinte maneira:

![chlimage_1-560](assets/chlimage_1-560.png)

O agrupamento para a parte do nome do ativo compartilhado do conjunto de rotação é adicionado ao campo **[!UICONTROL Correspondência]** (como destacado). A parte variável do nome do ativo que contém a linha e a coluna é adicionada aos campos **[!UICONTROL Linha]** e **[!UICONTROL Coluna]**, respectivamente.

Quando o Conjunto de rotação é carregado e publicado, você ativaria o nome da fórmula do Conjunto de rotação 2D que está listada em **[!UICONTROL Predefinições de conjunto de lote]** na caixa de diálogo **[!UICONTROL Opções de trabalho de upload]**.

**Para criar uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e entre na sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente da Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Predefinição do conjunto de lotes]**.

   O **[!UICONTROL Exibir Formulário]**, conforme definido no canto superior direito da página Detalhes, é o modo de exibição padrão.

1. No painel Lista de predefinições, selecione **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição, digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lote, selecione **[!UICONTROL Conjunto de ativos]**.
1. Na lista suspensa Subtipo, selecione **[!UICONTROL Conjunto de rotação de vários eixos]**.
1. Expanda **[!UICONTROL Convenções de nomenclatura de ativos]** e, na lista suspensa Nomenclatura de arquivos, selecione **[!UICONTROL Personalizado]**.
1. Use os atributos **[!UICONTROL Correspondência]** e, opcionalmente, **[!UICONTROL Nome de base]** para definir uma expressão regular para nomear ativos de imagem que compõem o agrupamento.

   Por exemplo, sua expressão regular de Correspondência literal pode ser semelhante ao seguinte:

   `(w+)-w+-w+`

1. Expanda **[!UICONTROL Posição da coluna de linha]** e defina o formato do nome para a posição do ativo de imagem na matriz do conjunto de rotação 2D.

   Use os parênteses para incorporar a posição da linha ou da coluna no nome do arquivo.

   Por exemplo, para sua expressão regular de linha, ela pode ser semelhante ao seguinte:

   `\w+-R([0-9]+)-\w+`

   ou

   `\w+-(\d+)-\w+`

   Para sua expressão regular de coluna, ela pode ser semelhante ao seguinte:

   `\w+-\w+-C([0-9]+)`

   ou

   `\w+-\w+-C(\d+)`

   As amostras acima são apenas para fins de demonstração. Você pode criar sua expressão regular da maneira que quiser que atenda às suas necessidades.

   >[!NOTE]
   >
   >Se a combinação de expressões regulares de linha e coluna não puder determinar a posição do ativo na matriz do conjunto de rotação multidimensional, o ativo não será adicionado ao conjunto. Um erro também é registrado.

1. Em Definir convenção de nomeação e criação, especifique o sufixo ou prefixo para o nome base definido na Convenção de nomeação de ativos.

   Além disso, defina onde o conjunto de rotação é criado na estrutura de pastas do Dynamic Media Classic.

   Se você definir um grande número de conjuntos, mantenha os conjuntos separados das pastas que contêm os próprios ativos. Por exemplo, crie uma pasta de Conjuntos de rotação para colocar conjuntos gerados aqui.

1. No painel Detalhes, selecione **[!UICONTROL Salvar]**.
1. Selecione **[!UICONTROL Ativo]** ao lado do novo nome de predefinição.

   A ativação da predefinição garante que, ao fazer upload de ativos para o Dynamic Media, a predefinição de conjunto de lotes seja aplicada para gerar o conjunto.

### (Opcional) Ajuste o desempenho do modo Dynamic Media - Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

Para manter o modo Dynamic Media - Scene7 funcionando sem problemas, o Adobe recomenda as seguintes dicas de ajuste de desempenho/escalabilidade de sincronização:

* Atualização dos parâmetros de Job predefinidos para processamento de diferentes formatos de arquivo.
* Atualizar as threads de trabalho da fila de fluxo de trabalho predefinidas do Granite (ativos de vídeo).
* Atualizar os threads de trabalho de fila de fluxo de trabalho transitório predefinido do Granite (imagens e ativos que não são de vídeo).
* Atualizar o máximo de conexões de upload para o servidor do Dynamic Media Classic.

#### Atualizar os parâmetros de Trabalho predefinidos para processamento de diferentes formatos de arquivo

Você pode ajustar parâmetros de job para um processamento mais rápido ao fazer upload de arquivos. Por exemplo, se você fizer upload de arquivos PSD, mas não quiser processá-los como modelos, poderá definir a extração de camada como false (desativado). Nesse caso, o parâmetro do trabalho ajustado aparece da seguinte maneira: `process=None&createTemplate=false`.

Caso deseje ativar a criação de modelo, use os seguintes parâmetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

O Adobe recomenda o uso dos seguintes parâmetros de job &quot;ajustados&quot; para arquivos PDF, PostScript® e PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo de arquivo | Parâmetros de processo recomendados |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para atualizar qualquer um desses parâmetros, siga as etapas em [Habilitando o suporte ao parâmetro de trabalho de carregamento do Assets/Dynamic Media Classic baseado em tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Atualizar a fila de fluxo de trabalho transitório do Granite {#updating-the-granite-transient-workflow-queue}

A fila de Fluxo de trabalho de Trânsito do Granite é usada para o fluxo de trabalho **[!UICONTROL Ativo de atualização do DAM]**. No Dynamic Media, é usado para assimilação e processamento de imagem.

**Para atualizar a fila de fluxos de trabalho transitórios do Granite:**

1. Navegue até [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e procure por **Fila: Fila de Fluxo de Trabalho Transitório do Granite**.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos paralelos]**, altere o número para o valor desejado.

   Você pode aumentar o **[!UICONTROL Máximo de Trabalhos Paralelos]** para oferecer suporte adequado ao carregamento pesado de arquivos para o Dynamic Media. O valor exato depende da capacidade do hardware. Em determinados cenários, ou seja, uma migração inicial ou um upload em massa único, você pode usar um valor alto. No entanto, esteja ciente de que usar um valor alto (como o dobro do número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, teste e ajuste o valor com base em seu caso de uso específico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0&ndash;1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a fila de fluxo de trabalho do Granite {#updating-the-granite-workflow-queue}

A fila de Fluxo de trabalho do Granite é usada para fluxos de trabalho não transitórios. No Dynamic Media, ele é usado para processar vídeos com o fluxo de trabalho **[!UICONTROL Codificação de vídeo do Dynamic Media]**.

**Para atualizar a fila de fluxo de trabalho do Granite:**

1. Navegue até `https://<server>/system/console/configMgr` e procure por **Fila: Fila de fluxos de trabalho do Granite**.

   >[!NOTE]
   >
   >Uma pesquisa de texto é necessária em vez de um URL direto, pois o PID OSGi é gerado dinamicamente.

1. No campo **[!UICONTROL Máximo de trabalhos paralelos]**, altere o número para o valor desejado.

   Você pode aumentar o Máximo de trabalhos paralelos para oferecer suporte adequado ao upload pesado de arquivos para o Dynamic Media. O valor exato depende da capacidade do hardware. Em determinados cenários, ou seja, uma migração inicial ou um upload em massa único, você pode usar um valor alto. No entanto, esteja ciente de que usar um valor alto (como o dobro do número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, teste e ajuste o valor com base em seu caso de uso específico.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a conexão de upload do Dynamic Media Classic {#updating-the-scene-upload-connection}

A configuração Conexão de upload do Scene7 sincroniza ativos do Experience Manager com os servidores da Dynamic Media Classic.

**Para atualizar a conexão de carregamento do Dynamic Media Classic:**

1. Navegue até `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. No campo **[!UICONTROL Número de conexões]** e/ou no campo **[!UICONTROL Tempo limite do trabalho ativo]**, altere o número conforme desejado.

   A configuração **[!UICONTROL Número de conexões]** controla o número máximo de conexões HTTP permitidas para o carregamento do Experience Manager para o Dynamic Media; normalmente, o valor predefinido de dez conexões é suficiente.

   A configuração **[!UICONTROL Tempo limite do trabalho ativo]** determina o tempo de espera para que os ativos carregados do Dynamic Media sejam publicados no servidor de entrega. Esse valor é de 2100 segundos (35 minutos) por padrão.

   Para a maioria dos casos de uso, a configuração de 2100 é suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

### (Opcional) Filtrar ativos para replicação {#optional-filtering-assets-for-replication}

Em implantações que não sejam da Dynamic Media, você replica *todos* ativos (tanto imagens quanto vídeos) do ambiente de criação do Experience Manager para o nó Experience Manager Publish. Esse fluxo de trabalho é necessário porque os servidores Experience Manager Publish também fornecem os ativos.

No entanto, nas implantações do Dynamic Media, como os ativos são entregues por meio do Cloud Service, não há necessidade de replicar esses mesmos ativos para os nós de publicação do Experience Manager. Esse fluxo de trabalho de &quot;publicação híbrida&quot; evita custos adicionais de armazenamento e tempos de processamento mais longos para replicar ativos. Outros conteúdos, como páginas do site, continuam a ser oferecidos pelos nós de publicação do Experience Manager.

Os filtros fornecem uma maneira de *excluir* ativos de serem replicados para o nó de publicação do Experience Manager.

#### Usar filtros de ativos padrão para replicação {#using-default-asset-filters-for-replication}

Se você usa o Dynamic Media para criação de imagens, vídeo ou ambos, é possível usar os filtros padrão que o Adobe fornece como está. Os seguintes filtros estão ativos por padrão:

|   | Filtro | Tipo MIME | Representações |
| --- | --- | --- | --- |
| Entrega de imagem do Dynamic Media | filter-image<br>filter-sets | Começa com **image/**<br> Contém **applications/** e termina com **set**. | As &quot;imagens de filtro&quot; prontas para uso (aplica-se a ativos de imagens únicas, incluindo imagens interativas) e os &quot;conjuntos de filtros&quot; (aplica-se a Conjuntos de rotação, Conjuntos de imagem, Conjuntos de mídia mista e Conjuntos de carrossel) irão:<br>· Excluir da replicação a imagem original e as representações de imagem estática. |
| Entrega de vídeo do Dynamic Media | filter-video | Começa com **vídeo/** | O &quot;vídeo de filtro&quot; pronto para uso irá:<br>· Excluir da replicação o vídeo original e as representações de miniatura estáticas. |

>[!NOTE]
>
>Os filtros se aplicam aos tipos MIME e não podem ser específicos de caminho.

#### Personalizar filtros de ativos para replicação {#customizing-asset-filters-for-replication}

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore de pastas à esquerda, navegue até `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` para examinar os filtros.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Para definir o Tipo MIME para o filtro, você pode localizar o Tipo MIME da seguinte maneira:

   No painel à esquerda, expanda `content > dam > <locate_your_asset> > jcr:content > metadata` e, na tabela, localize `dc:format`.

   O gráfico a seguir é um exemplo do caminho de um ativo para `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observe que `dc:format` para o ativo `Fiji Red.jpg` é `image/jpeg`.

   Para que esse filtro seja aplicado a todas as imagens, independentemente do formato, defina o valor como `image/*`, onde `*` é uma expressão regular aplicada a todas as imagens de qualquer formato.

   Para que o filtro se aplique somente a imagens do tipo JPEG, digite um valor de `image/jpeg`.

1. Defina quais representações você deseja incluir ou excluir da replicação.

   Os caracteres que podem ser usados para filtrar para replicação incluem:

   | Caractere a ser usado | Como ele filtra ativos para replicação |
   | --- | --- |
   | * | Caracteres curingas |
   | + | Inclui ativos para replicação |
   | - | Exclui ativos da replicação |

   Vá até `content/dam/<locate your asset>/jcr:content/renditions`.

   O gráfico a seguir é um exemplo das representações de um ativo.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Se você quiser replicar apenas o original, digite `+original`.
