---
title: OPÇÃO A - Configurar Dynamic Media - Modo Scene7
description: Saiba como configurar o Dynamic Media - Modo Scene7.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
mini-toc-levels: 3
hide: true
hidefromtoc: true
feature: Configuration,Scene7 Mode
exl-id: null
source-git-commit: bfa41deb156ffd0adb8138c11548912bc954f084
workflow-type: tm+mt
source-wordcount: '11558'
ht-degree: 3%

---

# OPÇÃO A - Configurar Dynamic Media - Modo Scene7{#configuring-dynamic-media-scene-mode}

>[!NOTE]
>
>OPÇÃO A - OS DOIS NOVOS TÓPICOS QUE ESCREVI SÃO EXCLUÍDOS. MAS ANTES DE EXCLUIR OS TÓPICOS, TODO O CONTEÚDO FOI MOVIDO PARA ESTE TÓPICO, PARA AS RESPECTIVAS ÁREAS ONDE JÁ FALEI SOBRE CONFIGURAÇÕES GERAIS E CONFIGURAÇÃO DE PUBLICAÇÃO.

Se você usar o Adobe Experience Manager configurado para ambientes diferentes, como desenvolvimento, armazenamento temporário e produção, configure os Dynamic Media Cloud Services para cada um desses ambientes.

## Diagrama de arquitetura do Dynamic Media - Modo Scene7 {#architecture-diagram-of-dynamic-media-scene-mode}

**RICK: MANTER COMO ESTÁ**

O diagrama de arquitetura a seguir descreve como o modo Dynamic Media - Scene7 funciona.

Com a nova arquitetura, o Experience Manager é responsável pelos ativos e sincronizações de origem primária com o Dynamic Media para processamento e publicação de ativos:

1. Quando o ativo de origem principal é carregado no Experience Manager, ele é replicado no Dynamic Media. Nesse momento, o Dynamic Media lida com todo o processamento de ativos e a geração de representação, como a codificação de vídeo e as variantes dinâmicas de uma imagem.
(No modo Dynamic Media - Scene7, o tamanho padrão do arquivo de upload é de 2 GB ou menos. Para ativar o upload de tamanhos de arquivo de 2 GB até 15 GB, consulte [(Opcional) Configurar o Dynamic Media - Modo Scene7 para upload de ativos com mais de 2 GB](#optional-config-dms7-assets-larger-than-2gb).)
1. Depois que as renderizações são geradas, o Experience Manager pode acessar com segurança e visualizar as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta para a instância do Experience Manager).
1. Depois que o conteúdo estiver pronto para ser publicado e aprovado, ele aciona o serviço da Dynamic Media para enviar o conteúdo para os servidores de entrega e armazenar em cache o conteúdo na CDN (Content Delivery Network).

![chlimage_1-550](assets/chlimage_1-550.png)

>[!IMPORTANT]
>
>A lista de recursos a seguir requer o uso do CDN pronto para uso fornecido com o Adobe Experience Manager - Dynamic Media. Nenhum outro CDN personalizado é compatível com esses recursos.
>
>* [Imagem inteligente](/help/assets/imaging-faq.md)
>* [Invalidação de cache](/help/assets/invalidate-cdn-cache-dynamic-media.md)
>* [Proteção de hotlink](/help/assets/hotlink-protection.md)
>* [Entrega de conteúdo HTTP/2](/help/assets/http2.md)
>* Redirecionamento de URL no nível CDN
>* Akamai ChinaCDN (para entrega ideal na China)


## Ativar o Dynamic Media no modo Scene7 {#enabling-dynamic-media-in-scene-mode}

**RICK: MANTER COMO ESTÁ**

[As mídias dinâmicas são desativadas por padrão. ](https://business.adobe.com/products/experience-manager/assets/dynamic-media.html) Para aproveitar os recursos do Dynamic Media, você deve habilitá-lo.

>[!WARNING]
>
>Dynamic Media - O modo Scene7 é para o *Somente instância Experience Manager Author*. Dessa forma, você deve configurar `runmode=dynamicmedia_scene7` na instância Experience Manager Author, *not* a instância Experience Manager Publish .

Para ativar o Dynamic Media, você deve iniciar o Experience Manager usando o `dynamicmedia_scene7` execute o modo a partir da linha de comando inserindo o seguinte em uma janela de terminal (por exemplo, a porta usada é 4502):

```shell
java -Xms4096m -Xmx4096m -Doak.queryLimitInMemory=500000 -Doak.queryLimitReads=500000 -jar cq-quickstart-6.5.0.jar -gui -r author,dynamicmedia_scene7 -p 4502
```

## (Opcional) Migrar predefinições e configurações do Dynamic Media de 6.3 para 6.5 Zero Down time {#optional-migrating-dynamic-media-presets-and-configurations-from-to-zero-downtime}

**RICK: MANTER COMO ESTÁ**

A atualização do Experience Manager Dynamic Media de 6.3 para 6.4 ou 6.5 agora inclui a capacidade de zero implantações de tempo de inatividade. Para migrar todas as suas predefinições e configurações do `/etc` para `/conf` no CRXDE Lite, execute o seguinte comando curl.

>[!NOTE]
>
>Se você executar a instância do Experience Manager no modo de compatibilidade, ou seja, você tem o pacote de compatibilidade instalado, não é necessário executar esses comandos.

Para todas as atualizações, com ou sem o pacote de compatibilidade, você pode copiar as predefinições padrão e prontas para uso do visualizador que vieram originalmente com o Dynamic Media executando o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets/viewer.pushviewerpresets.json`

Para migrar qualquer predefinição e configuração do visualizador personalizado do `/etc` para `/conf`, execute o seguinte comando curl do Linux®:

`curl -u admin:admin -X POST https://<server_address>:<server_port>/libs/settings/dam/dm/presets.migratedmcontent.json`

## Instale o feature pack 18912 para migração de ativos em massa {#installing-feature-pack-for-bulk-asset-migration}

**RICK: MANTER COMO ESTÁ**

A instalação do feature pack 18912 é *opcional*.

O Feature pack 18912 permite assimilar ativos em massa por meio de FTP ou migrar ativos do Dynamic Media - Modo híbrido ou Dynamic Media Classic para o Dynamic Media - modo Scene7 no Experience Manager. Está disponível em [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html).

Consulte [Instale o feature pack 18912 para migração de ativos em massa](/help/assets/bulk-ingest-migrate.md) para obter mais informações.

## Criar uma configuração do Dynamic Media no Cloud Services {#configuring-dynamic-media-cloud-services}

**RICK: MANTER COMO ESTÁ**

**Antes de configurar o Dynamic Media** - Depois de receber seu email de provisionamento com credenciais do Dynamic Media, você deve abrir a [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta para alterar a senha. A senha fornecida no email de provisionamento é gerada pelo sistema e deve ser apenas uma senha temporária. É importante atualizar a senha para que o Dynamic Media Cloud Service seja configurado com as credenciais corretas.

![dynamicmediaconfiguration2atualizado](assets/dynamicmediaconfiguration2updated.png)

**Para criar uma configuração do Dynamic Media no Cloud Services:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e selecione o ícone Ferramentas , em seguida, vá para **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuração do Dynamic Media]**.
1. Na página Navegador de configuração do Dynamic Media, no painel esquerdo, selecione **[!UICONTROL global]** (não selecione o ícone de pasta à esquerda de **[!UICONTROL global]**) e, em seguida, selecione **[!UICONTROL Criar]**.
1. No **[!UICONTROL Criar configuração do Dynamic Media]** , insira um título, o endereço de email da conta do Dynamic Media, a senha e selecione sua região. Essas informações são fornecidas pelo Adobe no email de provisionamento. Entre em contato com o Suporte ao cliente do Adobe se não tiver recebido o email.

   Selecionar **[!UICONTROL Conectar-se ao Dynamic Media]**.

   >[!NOTE]
   **RICK: MANTER COMO ESTÁ??** Depois de receber seu email de provisionamento com credenciais do Dynamic Media, abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta para alterar a senha. A senha fornecida no email de provisionamento é gerada pelo sistema e deve ser apenas uma senha temporária. É importante atualizar a senha para que o Dynamic Media Cloud Service seja configurado com as credenciais corretas.

1. Quando a conexão for bem-sucedida, defina o seguinte. São necessários títulos com um asterisco (*):

   * **[!UICONTROL Empresa]** - o nome da conta do Dynamic Media. Você tem várias contas Dynamic Media. Por exemplo, você pode ter diferentes submarcas, divisões, preparo ou ambientes de produção.

   * **[!UICONTROL Caminho da pasta raiz da empresa]**

   * **[!UICONTROL Publicar ativos]** - Você pode escolher entre as três opções a seguir:
      * **[!UICONTROL Imediatamente]** significa que, quando os ativos são carregados, o sistema assimila os ativos e fornece o URL/Incorporado instantaneamente. Não há necessidade de intervenção do usuário para publicar ativos.
      * **[!UICONTROL Após ativação]** significa que você deve publicar explicitamente o ativo primeiro antes de um link URL/Incorporar ser fornecido.<br><!-- CQDOC-17478, Added March 9, 2021-->A partir do Experience Manager 6.5.8, a instância de publicação do Experience Manager reflete valores precisos de metadados de Dynamic Media, como `dam:scene7Domain` e `dam:scene7FileStatus` em **[!UICONTROL Após ativação]** apenas o modo de publicação. Para ativar essa funcionalidade, instale o Service Pack 8 e, em seguida, reinicie o Experience Manager. Vá para o Sling Config Manager. Encontre a configuração para `Scene7ActivationJobConsumer Component` ou criar um novo). Marque a caixa de seleção **[!UICONTROL Replicar metadados após a publicação do Dynamic Media]**, em seguida selecione **[!UICONTROL Salvar]**.

         ![Caixa de seleção Replicar metadados após a publicação do Dynamic Media](assets-dm/replicate-metadata-setting.png)

      * **[!UICONTROL Publicação seletiva]** Essa opção permite controlar quais pastas são publicadas no Dynamic Media. Ele permite usar recursos como Recorte inteligente ou representações dinâmicas, ou determinar quais pastas são publicadas exclusivamente no Experience Manager para visualização. Esses mesmos ativos são *not* publicado no Dynamic Media para entrega no domínio público.<br>Você pode definir essa opção aqui na **[!UICONTROL Configuração da Dynamic Media Cloud]** ou, se preferir, você pode optar por definir essa opção no nível da pasta, em um **[!UICONTROL Propriedades]**.<br>Consulte [Trabalhar com publicação seletiva no Dynamic Media](/help/assets/selective-publishing.md).<br>Se posteriormente alterar essa configuração ou alterá-la no nível da pasta, essas alterações afetarão somente os novos ativos que você carregar a partir desse ponto. O estado de publicação dos ativos existentes na pasta permanece como está até que você os altere manualmente de **[!UICONTROL Publicação rápida]** ou **[!UICONTROL Gerenciar publicação]** caixa de diálogo.
   * **[!UICONTROL Servidor de visualização segura]** - permite especificar o caminho do URL para o servidor de visualização de representações seguras. Ou seja, depois que as renderizações são geradas, o Experience Manager pode acessar com segurança e visualizar as renderizações remotas do Dynamic Media (nenhum binário é enviado de volta à instância do Experience Manager).
A menos que você tenha um acordo especial para usar o servidor da sua empresa ou um servidor especial, o Adobe recomenda deixar essa configuração como especificado.

   * **[!UICONTROL Sincronizar todo o conteúdo]** - <!-- NEW OPTION, CQDOC-15371, Added March 4, 2020-->Selecionado por padrão. Desmarque essa opção se desejar incluir ou excluir seletivamente ativos da sincronização com o Dynamic Media. Desmarcar essa opção permite escolher entre os dois modos de sincronização Dynamic Media a seguir:

   * **[!UICONTROL Modo de sincronização do Dynamic Media]**
      * **[!UICONTROL Ativado por padrão]** - A configuração é aplicada a todas as pastas por padrão, a menos que você marque uma pasta especificamente para exclusão. <!-- you can then deselect the folders that you do not want the configuration applied to.-->
      * **[!UICONTROL Desabilitado por padrão]** - A configuração não é aplicada a nenhuma pasta até que você marque explicitamente uma pasta selecionada para sincronização com o Dynamic Media.
Para marcar uma pasta selecionada para sincronização com o Dynamic Media, selecione uma pasta de ativos e, na barra de ferramentas, selecione **[!UICONTROL Propriedades]**. No **[!UICONTROL Detalhes]** na guia , no **[!UICONTROL Modo de sincronização Dynamic Media]** selecione uma das três opções a seguir. Quando terminar, selecione **[!UICONTROL Salvar]**. *Lembre-se: essas três opções não estarão disponíveis se você tiver selecionado **[!UICONTROL Sincronizar todo o conteúdo]**anteriormente.* Consulte também [Trabalhar com a Publicação seletiva no nível da pasta no Dynamic Media](/help/assets/selective-publishing.md).
         * **[!UICONTROL Herdado]** - Nenhum valor de sincronização explícito na pasta; em vez disso, a pasta herda o valor de sincronização de uma de suas pastas ancestrais ou o modo padrão na configuração da nuvem. O status detalhado de herdado é exibido por meio de uma dica de ferramenta.
         * **[!UICONTROL Ativar para subpastas]** - Inclua tudo nesta subárvore para sincronização com o Dynamic Media. As configurações específicas da pasta substituem o modo padrão na configuração da nuvem.
         * **[!UICONTROL Desabilitado para subpastas]** - Excluir de sincronização tudo nesta subárvore para o Dynamic Media.

   >[!NOTE]
   Não há suporte para o controle de versão no DMS7. Além disso, a ativação atrasada se aplica somente se **[!UICONTROL Publicar ativos]** na página Editar configuração do Dynamic Media estiver definida como **[!UICONTROL Na ativação]** e, em seguida, somente até a primeira vez que o ativo for ativado.
   Depois que um ativo é ativado, todas as atualizações são publicadas imediatamente no S7 Delivery.

1. Selecione **[!UICONTROL Salvar]**.
1. Para visualizar com segurança o conteúdo do Dynamic Media antes de ele ser publicado, é necessário &quot;lista de permissões&quot; a instância do autor do Experience Manager para se conectar ao Dynamic Media:

   * **RICK: LINK PARA NOVO TÓPICO DE CONFIGURAÇÃO DE PUBLICAÇÃO** Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta. Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente do Adobe.

   * Na barra de navegação próxima à parte superior direita da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configuração de publicação]** > **[!UICONTROL Servidor de imagem]**.

   * Na página Publicação do servidor de imagens, na lista suspensa Publicar contexto , selecione **[!UICONTROL Testar o fornecimento de imagem]**.
   * Para o Filtro de endereço do cliente, selecione **[!UICONTROL Adicionar]**.
   * Para ativar (ativar) o endereço, marque a caixa de seleção . Insira o endereço IP da instância Experience Manager Author (não o IP do Dispatcher).
   * Selecione **[!UICONTROL Salvar]**.

Agora você terminou com a configuração básica; você está pronto para usar o modo Dynamic Media - Scene7.

Se você quiser personalizar ainda mais sua configuração, poderá, opcionalmente, concluir qualquer uma das tarefas em [(Opcional) Definir configurações avançadas no modo Dynamic Media - Scene7](#optional-configuring-advanced-settings-in-dynamic-media-scene-mode).

## (Opcional) Definir configurações avançadas no modo Dynamic Media - Scene7 {#optional-configuring-advanced-settings-in-dynamic-media-scene-mode}

**RICK: MANTER COMO ESTÁ**

Se você quiser personalizar ainda mais a configuração e configuração do Dynamic Media - modo Scene7 ou otimizar seu desempenho, é possível concluir um ou mais dos seguintes procedimentos *opcional* tarefas:

* [(Opcional) Configurar o Dynamic Media - Modo Scene7 para upload de ativos com mais de 2 GB](#optional-config-dms7-assets-larger-than-2gb)

* [(Opcional) Configuração e configuração do Dynamic Media - Configurações do modo Scene7](#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings)

* [(Opcional) Ajustar o desempenho do Dynamic Media - Modo Scene7](#optional-tuning-the-performance-of-dynamic-media-scene-mode)

* [(Opcional) Filtrar ativos para replicação](#optional-filtering-assets-for-replication)

### (Opcional) Configurar o Dynamic Media - Modo Scene7 para upload de ativos com mais de 2 GB {#optional-config-dms7-assets-larger-than-2gb}

**RICK: MANTER COMO ESTÁ**

No modo Dynamic Media - Scene7, o tamanho padrão do arquivo de upload de ativos é de 2 GB ou menos. No entanto, opcionalmente, é possível configurar o upload de ativos com mais de 2 GB e até 15 GB.

Se você pretende usar esse recurso, esteja ciente dos seguintes pré-requisitos e pontos:

* Você deve estar executando o Experience Manager 6.5 com Service Pack 6.5.4.0 ou posterior no modo Dynamic Media - Scene7.
* Esse recurso de upload grande é compatível somente com [*Managed Services*](https://business.adobe.com/products/experience-manager/managed-services.html) clientes.
* Certifique-se de que a instância do Experience Manager esteja configurada com o armazenamento Amazon S3 ou Microsoft® Azure Blob.

   >[!NOTE]
   Configure o armazenamento do Azure Blob com uma chave de acesso e uma chave secreta porque esse recurso de upload grande não é compatível com o AzureSas na configuração de armazenamento do Blob.

* Oak&#39;s [Download do Acesso binário direto](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html) está ativado (Oak&#39;s *Upload de acesso binário direto* não é obrigatório).

   Para habilitar o download do Acesso binário direto, defina a propriedade `presignedHttpDownloadURIExpirySeconds > 0` na configuração do armazenamento de dados. O valor deve ser longo o suficiente para baixar binários maiores e possivelmente tentar novamente.

* Os ativos com mais de 15 GB não são carregados. (O limite de tamanho é definido na etapa 8 abaixo.)
* Quando a variável **[!UICONTROL Dynamic Media Reprocess]** O fluxo de trabalho de ativos é acionado em uma pasta, ele reprocessa todos os ativos grandes que já estão sincronizados com a empresa da Dynamic Media. No entanto, se algum ativo grande ainda não estiver sincronizado na pasta, ele não fará upload do ativo. Portanto, para sincronizar ativos grandes existentes no Dynamic Media, você pode executar **[!UICONTROL Dynamic Media Reprocess]** fluxo de trabalho de ativos em ativos individuais.

**Para configurar o Dynamic Media - Modo Scene7 para upload de ativos com mais de 2 GB:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

1. Na janela CRXDE Lite, execute um dos seguintes procedimentos:

   * No painel à esquerda, navegue até o seguinte caminho:

      `/libs/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie e cole o caminho acima no campo CRXDE Lite path abaixo da barra de ferramentas e pressione `Enter`.

1. No painel à esquerda, clique com o botão direito do mouse em `fileupload`e, no menu pop-up, selecione **[!UICONTROL Nó de sobreposição]**.

   ![Opção Sobrepor nó](/help/assets/assets-dm/uploadassets15gb_a.png)

1. Na caixa de diálogo Sobrepor nó , selecione o **[!UICONTROL Corresponder tipos de nó]** caixa de seleção para ativar (ativar) a opção e, em seguida, selecionar **[!UICONTROL OK]**.

   ![Caixa de diálogo Sobrepor nó](/help/assets/assets-dm/uploadassets15gb_b.png)

1. Na janela CRXDE Lite, execute um dos seguintes procedimentos:

   * No painel à esquerda, navegue até o seguinte caminho do nó de sobreposição:

      `/apps/dam/gui/content/assets/jcr:content/actions/secondary/create/items/fileupload`

   * Copie e cole o caminho acima no campo CRXDE Lite path abaixo da barra de ferramentas e pressione `Enter`.

1. No **[!UICONTROL Propriedades]** na guia , em **[!UICONTROL Nome]** coluna, localizar `sizeLimit`.
1. À direita do `sizeLimit` nome, sob o **[!UICONTROL Valor]** , clique duas vezes no campo de valor.
1. Insira o valor apropriado em bytes, para que você possa aumentar o limite de tamanho para o tamanho máximo de upload desejado. Por exemplo, para aumentar o limite de tamanho do ativo de upload para 10 GB, insira `10737418240` no campo de valor.
Você pode inserir um valor de até 15 GB (`2013265920` bytes). Nesse caso, os ativos carregados com mais de 15 GB não são carregados.


   ![Valor limite de tamanho](/help/assets/assets-dm/uploadassets15gb_c.png)

1. Próximo ao canto superior esquerdo da janela CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

   *Agora defina o tempo limite para o Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite fazendo o seguinte:*

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global.
1. Siga um destes procedimentos:

   * Navegue até o seguinte caminho de URL:

      `localhost:4502/system/console/configMgr/com.adobe.granite.workflow.core.job.ExternalProcessJobHandler`

   * Copie e cole o caminho acima no campo URL do seu navegador. Certifique-se de substituir `localhost:4502` com sua própria instância do Experience Manager.

1. No **[!UICONTROL Manipulador de Trabalho do Processo Externo do Fluxo de Trabalho do Adobe Granite]** na caixa de diálogo , na **[!UICONTROL Tempo limite máximo]** , defina o valor como `18000` minutos (cinco horas). O padrão é 10800 minutos (três horas).

   ![Valor máximo do tempo limite](/help/assets/assets-dm/uploadassets15gb_d.png)

1. No canto inferior direito da caixa de diálogo, selecione **[!UICONTROL Salvar]**.

   *Agora defina o tempo limite para a etapa do processo de Upload binário direto do Scene7, fazendo o seguinte:*

1. No Experience Manager, selecione o logotipo Experience Manager para acessar o console de navegação global.
1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos de fluxo de trabalho , selecione **[!UICONTROL Codificar vídeo no Dynamic Media]**.
1. Na barra de ferramentas, selecione **[!UICONTROL Editar]**.
1. Na página do fluxo de trabalho , clique duas vezes no botão **[!UICONTROL Upload binário direto do Scene7]** etapa do processo.
1. No **[!UICONTROL Propriedades da etapa]** na caixa de diálogo , em **[!UICONTROL Frequentes]** na guia , em **[!UICONTROL Configurações avançadas]** no cabeçalho **[!UICONTROL Tempo limite]** , insira um valor de `18000` minutos (cinco horas). O padrão é `3600` minutos (uma hora).
1. Selecionar **[!UICONTROL OK]**.
1. Selecionar **[!UICONTROL Sincronizar]**.
1. Repita as etapas 14 a 21 para a **[!UICONTROL Ativo de atualização DAM]** modelo de fluxo de trabalho e **[!UICONTROL Dynamic Media Reprocess]** modelo de fluxo de trabalho.

### (Opcional) Configurar a configuração de publicação do Dynamic Media {#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings}

**RICK: TODO O CONTEÚDO DO NOVO TÓPICO DE CONFIGURAÇÃO DE PUBLICAÇÃO ADICIONADO AQUI**

>[!IMPORTANT]
A Configuração de publicação do Dynamic Media só estará disponível se:
* Você está executando o Dynamic Media no modo Scene7.
* Você tem um *existente* **[!UICONTROL Configuração do Dynamic Media]** (em **[!UICONTROL Cloud Services]**) no Adobe Experience Manager 6.5 ou no Experience Manager as a Cloud Service.
* Você é um administrador de sistema do Experience Manager com privilégios de administrador.


As configurações da página Configuração de publicação do Dynamic Media determinam como os ativos são entregues por padrão dos servidores do Adobe Dynamic Media para sites ou aplicativos da Web. Se nenhuma configuração for especificada, o servidor Adobe Dynamic Media fornece um ativo de acordo com uma configuração padrão em uma página Publicar configuração . Por exemplo, uma solicitação para fornecer uma imagem que não inclua um atributo de resolução gera uma imagem com a configuração de Resolução de objeto padrão na página Servidor de imagem.

Os administradores podem alterar as configurações padrão nas páginas Servidor de imagem, Renderizador de imagem e Vinheta para estabelecer configurações padrão para o fornecimento de ativos dos servidores.

>[!NOTE]
A Configuração de publicação do Dynamic Media deve ser usada por desenvolvedores e programadores de sites experientes. O Adobe recomenda que os usuários que alteram qualquer uma dessas configurações de publicação padrão estejam familiarizados com o Adobe Dynamic Media, padrões e convenções de protocolo HTTP e tecnologia básica de geração de imagens.

**Para configurar a Configuração de publicação do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, selecione o ícone Ferramentas e vá para **[!UICONTROL Ativos]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagens, defina o Servidor de imagens - contexto de publicação e use as cinco guias para definir as configurações de publicação padrão.

   * [Servidor de imagem](#image-server)
   * [Segurança](#security-tab) guia
   * [Gerenciamento de catálogo](#catalog-management-tab) guia
   * [Atributos da solicitação](#request-attributes-tab) guia
   * [Atributos de miniatura comuns](#common-thumbnail-attributes-tab) guia
   * [Atributos do gerenciamento de cores](#color-management-attributes-tab) guia

   ![Página Configuração de publicação do Dynamic Media](/help/assets/assets-dm/dm-publish-setup.png)
   *página Configuração de publicação do Dynamic Media, com o **[!UICONTROL Atributos da solicitação]**selecionada.*<br><br>

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

#### Servidor de imagem {#image-server}

A página Servidor de imagens estabelece as configurações padrão para o fornecimento de imagens de servidores de imagens. As configurações estão disponíveis em cinco categorias

| Contexto de publicação | Descrição |
| --- | --- |
| Serviço de imagem | Especifica o contexto das configurações de publicação. |
| Servidor de imagens de teste | Especifica o contexto para testar as configurações de publicação.<br>Consulte [Testar ativos antes de torná-los públicos](#test-assets-before-making-public). |

#### Guia Segurança {#security-tab}

**[!UICONTROL Endereço do cliente]** - Permite especificar um ou mais endereços IP ou intervalos de endereço IP. Quando especificado, as solicitações para este catálogo de imagem que se origina de um cliente em um endereço IP não listado são rejeitadas. Essa regra se aplica à entrega de imagens e imagens renderizadas.

#### Guia Gerenciamento de catálogo {#catalog-management-tab}

**[!UICONTROL Caminho do arquivo de definição do conjunto de regras]** - Especifica o arquivo que contém as definições do conjunto de regras para o catálogo de imagens.

Consulte também [RuleSetFile](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-rulesetfile.html) no Guia de referência de visualizadores do Dynamic Media.

#### Guia Atributos da solicitação {#request-attributes-tab}

Essas configurações pertencem à aparência padrão das imagens.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Limite de tamanho da imagem de resposta]** | Obrigatório.<br>Especifica a largura e a altura máximas da imagem de resposta que são retornadas ao cliente. O servidor retornará um erro se uma solicitação causar uma imagem de resposta cuja largura, altura ou ambos forem maiores que essa configuração.<br>Consulte também [MaxPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-maxpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de solicitação de ofuscação]** | Ative se desejar que a codificação base64 seja aplicada a solicitações válidas.<br>Consulte também [RequestObfuscation](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestobfuscation.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de bloqueio de solicitação]** | Ative se desejar que um simples bloqueio de hash seja incluído em solicitações.<br>Consulte também [RequestLock](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-requestlock.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de solicitação padrão]** |  |
| **[!UICONTROL Sufixo do arquivo de imagem padrão]** | Obrigatório.<br>Extensão padrão do arquivo de dados que é anexada aos valores dos campos Caminho e Máscara do catálogo se o caminho não incluir um sufixo de arquivo.<br>Consulte também [DefaultExt](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultext.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Nome da face da fonte padrão]** | Especifica qual fonte é usada se nenhuma fonte for fornecida por uma solicitação de camada de texto. Se especificado, deve ser um valor de nome de fonte válido no mapa de fonte deste catálogo de imagem ou no mapa de fontes do catálogo padrão.<br>Consulte também [DefaultFont](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultfont.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Imagem padrão]** | Fornece uma imagem padrão a ser retornada em resposta a uma solicitação na qual a imagem solicitada não é encontrada.<br>Consulte também [DefaultImage](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-defaultimage.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Modo de imagem padrão]** | Quando a caixa de controle deslizante estiver ativada (controle deslizante à direita), a variável **[!UICONTROL Imagem padrão]** substitui cada camada ausente na imagem de origem pela imagem padrão e retorna o composto como de costume. Quando a caixa de controle deslizante está desativada (controle deslizante à esquerda), a imagem padrão substitui toda a imagem composta, mesmo que a imagem ausente seja apenas uma das várias camadas.<br>Consulte também [DefaultImageMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultimagemode.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tamanho de exibição padrão]** | Obrigatório.<br>O servidor restringe as imagens de resposta a não serem maiores que essa largura e altura, se a solicitação não especificar o tamanho de exibição explicitamente usando `wid=`, `hei=`ou `scl=`.<br>Consulte também [DefaultPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tamanho padrão da miniatura]** | Obrigatório.<br>Usado em vez do atributo **[!UICONTROL Tamanho de exibição padrão]** para solicitações de miniatura (`req=tmb`). O servidor restringe as imagens de resposta para não serem maiores que essa largura e altura, se houver uma solicitação em miniatura (`req=tmb`) não especifica o tamanho explicitamente usando `wid=`, `hei=`ou `scl=`.<br>Consulte também [DefaultThumbPix](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-defaultthumbpix.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Cor de fundo padrão]** | Especifica o valor RGB usado para preencher qualquer área de uma imagem de resposta que não contenha dados de imagem reais.<br>Consulte também [BkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-bkgcolor.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Atributos de codificação de JPEG]** |  |
| **[!UICONTROL Qualidade]** | Especifica os atributos padrão para imagens JPEG reply. O **[!UICONTROL Qualidade]** é definido no intervalo de 1 - 100.<br>Consulte também [JpegQuality](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-jpegquality.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Diminuição da resolução cromática]** | Ative ou desative a redução cromaticamente da amostragem que é empregada por codificadores JPEG. |
| **[!UICONTROL Modo de reamostragem padrão]** | Especifica a reamostragem e os atributos de interpolação padrão a serem usados para dimensionar dados de imagem. Use quando `resMode` não é especificado em uma solicitação.<br>Consulte também [ResMode](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-is-cat-resmode.html) no Guia de referência de visualizadores do Dynamic Media. |

#### Guia Atributos de miniatura comuns {#common-thumbnail-attributes-tab}

Essas configurações pertencem à aparência padrão e ao alinhamento de imagens em miniatura.

| Configuração | Descrição |
| --- | --- |
| **[!UICONTROL Cor de fundo padrão para miniatura]** | Especifica o valor de RGB usado para preencher a área de uma imagem em miniatura de saída que não contém dados de imagem reais. Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]** ou **[!UICONTROL Textura]**.<br>Consulte também [ThumbBkgColor](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbbkgcolor.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento horizontal]** | Especifica o alinhamento horizontal da imagem em miniatura no retângulo de imagem de resposta especificado por `wid=` e `hei=` valores.<br>Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos horizontais para escolher: **[!UICONTROL Alinhamento central]**, **[!UICONTROL Alinhamento à esquerda]** e **[!UICONTROL Alinhamento à direita]**.<br>Consulte também [MiniaturaAlinhar](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbhorizalign.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Alinhamento vertical]** | Especifica o alinhamento vertical da imagem em miniatura no retângulo de imagem de resposta especificado por `wid=` e `hei=` valores. Usado somente para solicitações de miniatura (`req=tmb`) e quando **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Ajustar]**.<br>Há três alinhamentos verticais a serem escolhidos: **[!UICONTROL Alinhamento superior]**, **[!UICONTROL Alinhamento central]** e **[!UICONTROL Alinhamento inferior]**.<br>Consulte também [ThumbVertAlign](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbvertalign.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tempo de funcionamento padrão do cache]** | Fornece um intervalo de expiração padrão em horas, caso um registro de catálogo específico não contenha um valor de Expiração de catálogo válido. Defina como `-1` para marcar como nunca expirar. <br>Consulte também [Expiração](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-expiration.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Tipo de miniatura padrão]** | Fornece um padrão para o tipo de miniatura caso um registro de catálogo específico não contenha um valor ThumbType de catálogo válido. Usado somente para solicitações de miniatura (`req=tmb`).<br>Há três tipos de miniaturas para escolher: **[!UICONTROL Cortar]**, **[!UICONTROL Ajustar]** e **[!UICONTROL Textura]**.<br>Consulte também [ThumbType](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbtype.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Resolução padrão de miniatura]** | Fornece um padrão para a resolução de objeto de miniatura caso um registro de catálogo específico não contenha um valor de ThumbRes de catálogo válido. Usado somente para solicitações de miniatura (`req=tmb`) e quando a variável **[!UICONTROL Tipo de miniatura padrão]** está definida como **[!UICONTROL Textura]**.<br>Consulte também [ThumbRes](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-thumbres.html) no Guia de referência de visualizadores do Dynamic Media. |

#### Guia Atributos de gerenciamento de cores {#color-management-attributes-tab}

Essas configurações determinam quais perfis de cores ICC são usados para imagens.

**Propósito de renderização da conversão de cores**
Um propósito de renderização de conversão de cores permite a substituição da intenção de renderização padrão dos perfis de trabalho para determinar como as cores de origem são ajustadas. Usado quando:

1. Um dos perfis ICC padrão é o espaço de cores de destino de uma conversão de cores.
1. Um dispositivo de saída (impressora ou monitor) é caracterizado por esse perfil.
1. E o propósito de renderização especificado é válido para este perfil.

Diferentes intenções de renderização usam regras diferentes para determinar como as cores de origem são ajustadas.

Como exemplo, você pode definir a variável **[!UICONTROL RGB espaço de cores padrão]** para **[!UICONTROL sRGB]** e **[!UICONTROL Espaço de cores padrão CMYK]** para **[!UICONTROL WebCoated]**.

Isso faria o seguinte:

* Habilita a correção de cores para imagens RGB e CMYK.
* Pressupõe-se que as imagens RGB que não têm um perfil de cor estejam na *sRGB* espaço de cores.
* Pressupõe-se que as imagens CMYK que não têm um perfil de cor estejam em *WebCoated* espaço de cores.
* As renderizações dinâmicas que retornam a saída do RGB, retornam-na no *sRGB* espaço de cores.
* As renderizações dinâmicas que retornam a saída CMYK, retornam-na no *WebCoated* espaço de cores.

Consulte também [IccRenderIntent](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccrenderintent.html) no Guia de referência de visualizadores do Dynamic Media.

>[!NOTE]
Em geral, é melhor usar o propósito de renderização padrão para a configuração de cor selecionada, que foi testada pelo Adobe para atender aos padrões do setor. Por exemplo, se você escolher uma configuração de cor para América do Norte ou Europa, o objetivo padrão de renderização da conversão de cores será **[!UICONTROL Colormétrica relativa]**. Se você escolher uma configuração de cor para o Japão, o objetivo padrão de renderização da conversão de cores será **[!UICONTROL Perceptivo]**.

| Configuração | Características |
| --- | --- |
| **[!UICONTROL Espaço de cores padrão CMYK]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados CMYK. If **[!UICONTROL Nenhum especificado]** for escolhida, o gerenciamento de cores será desativado para esse catálogo de imagens quando as imagens de origem CMYK estiverem envolvidas. Todos os espaços de trabalho CMYK dependem do dispositivo, o que significa que eles são baseados em combinações reais de tinta e papel. Os Adobe dos espaços de trabalho CMYK são fornecidos com base em condições de impressão comercial padrão.<br> Consulte também [IccProfileCMYK](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilecmyk.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Espaço de cores padrão de escala de cinza]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados em escala de cinza. If **[!UICONTROL Nenhum especificado]** for escolhido, o gerenciamento de cores será desativado para esse catálogo de imagens quando imagens de origem em escala cinza forem envolvidas.<br>Consulte também [IccProfileGray](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilegray.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL RGB espaço de cores padrão]** | Especifica o nome do perfil de cores ICC a ser usado como um perfil de trabalho para dados de RGB. If **[!UICONTROL Nenhum especificado]** for escolhido, o gerenciamento de cores será desativado para esse catálogo de imagens quando as imagens de RGB forem envolvidas. Em geral, é melhor escolher **[!UICONTROL Adobe RGB]** ou **[!UICONTROL sRGB]**, em vez do perfil de um dispositivo específico (como um perfil de monitor). **[!UICONTROL sRGB]** O é recomendado ao preparar imagens para a Web ou dispositivos móveis, pois define o espaço de cores do monitor padrão usado para exibir imagens na Web. **[!UICONTROL sRGB]** O também é uma boa escolha para trabalhar com imagens de câmeras digitais de nível de consumidor, pois a maioria dessas câmeras usa o sRGB como espaço de cores padrão.<br>Consulte também [IccProfileRBG](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/attributes/r-iccprofilergb.html) no Guia de referência de visualizadores do Dynamic Media. |
| **[!UICONTROL Objetivo de renderização da conversão de cores]** | **[!UICONTROL Perceptivo]** - Tem como objetivo preservar a relação visual entre as cores para que seja percebida como natural para o olho humano, mesmo que os próprios valores de cor possam mudar. Essa intenção é adequada para imagens fotográficas com muitas cores fora do gamut. Essa configuração é o propósito de renderização padrão para o setor de impressão japonês. |
|  | **[!UICONTROL Colorimétrica relativa]** - Compara o realce extremo do espaço de cores de origem com o do espaço de cores de destino e alterna todas as cores de acordo. As cores fora do gamut são transferidas para a cor reprodutível mais próxima no espaço de cores de destino. Colorimétrica relativa preserva mais das cores originais em uma imagem do que Perceptual. Essa configuração é o propósito de renderização padrão para impressão na América do Norte e na Europa. |
|  | **[!UICONTROL Saturação]** - Tenta produzir cores vivas em uma imagem, em detrimento da precisão das cores. Esse propósito de renderização é adequado para gráficos comerciais, como gráficos ou gráficos, em que cores saturadas brilhantes são mais importantes do que a relação exata entre cores. |
|  | **[!UICONTROL Colorimétrica absoluta]** - Deixa inalteradas as cores que estão dentro da gama de destino. As cores fora do gamut são cortadas. Não é executado o dimensionamento de cores para o ponto branco de destino. Essa intenção tem como objetivo manter a precisão da cor em detrimento da preservação das relações entre cores e é adequada para a prova para simular a saída de um determinado dispositivo. Essa intenção é útil para visualizar como a cor do papel afeta as cores impressas. |

### Testar ativos antes de torná-los públicos {#test-assets-before-making-public}

O Teste Seguro ajuda você a definir um ambiente de teste seguro e criar uma solução empresarial para negócios robusta, com base em um conjunto configurável de endereços IP e intervalos. Essa funcionalidade permite que você corresponda suas implantações do Adobe Dynamic Media à arquitetura do seu sistema de negócios e de gerenciamento de conteúdo.

Com o Teste Seguro, você pode visualizar a versão de preparo do site com conteúdo não publicado.

Se desejar, crie um ambiente de preparo em vez de tornar os ativos disponíveis publicamente pelos seguintes motivos:

* Visualizar sites antes do lançamento público (site de preparo).
* Adicione ativos que exigem acesso restrito, como eCatalogs que mostrem preços em uma aplicação Web B2B.
* Use os ativos por trás de um firewall como parte do sistema de gerenciamento de informações do produto, do aplicativo de atendimento ao cliente, do site de treinamento e assim por diante.

>[!NOTE]
O Teste Seguro não afeta o acesso ao Adobe Dynamic Media Classic. A segurança do Adobe Dynamic Media Classic permanece consistente e requer as credenciais usuais para acesso ao Adobe Dynamic Media Classic e serviços da Web relacionados.

#### Como o teste seguro funciona {#how-test-assets-works}

A maioria das corporações mantém a Internet por trás de um firewall. O acesso à Internet é possível através de determinadas rotas e geralmente através de uma gama limitada de endereços IP públicos.

Na sua rede corporativa, você pode descobrir seu endereço IP público usando sites como [https://www.whatismyip.com](https://www.whatismyip.com/) ou solicite essas informações à sua organização de TI corporativa.

Com o Teste Seguro, o Adobe Dynamic Media estabelece um Servidor de Imagem dedicado para ambientes de preparo ou aplicativos internos. Qualquer solicitação para este servidor verifica o endereço IP de origem. Se a solicitação recebida não estiver na lista aprovada de endereços IP, uma resposta de falha será retornada. O Administrador da empresa do Adobe Dynamic Media configura a lista aprovada de endereços IP para o ambiente de Teste Seguro da empresa.

Como a localização da solicitação original deve ser confirmada, o tráfego do serviço de Teste Seguro não é roteado por meio de uma rede de distribuição de conteúdo como o tráfego público do Dynamic Media Image Server. As solicitações para o serviço de teste seguro têm uma latência ligeiramente maior em comparação com os servidores públicos de imagem da Dynamic Media.

Os ativos não publicados ficam imediatamente disponíveis nos serviços de Teste Seguro, sem a necessidade de publicar. Dessa forma, é possível executar uma visualização antes que os ativos sejam publicados em seu servidor de imagens aberto ao público.

>[!NOTE]
Os serviços de Teste Seguro usam o Servidor de Catálogo configurado com um contexto de publicação interno. Portanto, se sua empresa estiver configurada para publicar no Teste seguro, todos os ativos carregados no Adobe Dynamic Media imediatamente se tornarão disponíveis nos serviços de Teste seguro. Essa funcionalidade é verdadeira independentemente de os ativos serem marcados para publicação no upload.

Os serviços de Teste Seguro atualmente oferecem suporte aos seguintes tipos de ativos e funcionalidades:

* Imagens.
* Vinhetas (Solicitações do Servidor de Renderização).
* Solicitações do Servidor de Renderização (suportadas, mas devem ser solicitadas explicitamente pelo cliente).
* Conjuntos, incluindo conjuntos de imagens, eCatalog, conjuntos de renderização e conjuntos de mídia.
* Visualizadores de mídia avançada do Adobe Standard Dynamic Media.
* Adobe Dynamic Media OnDemand JSP pages.
* Conteúdo estático, como arquivos PDF e vídeos fornecidos progressivamente.
* streaming de vídeo HTTP.
* Transmissão contínua de vídeo.

Os seguintes tipos de ativos e funcionalidades não são suportados no momento:

* Pesquisa de informações ou eCatalog do Adobe Dynamic Media Classic
* Transmissão de vídeo RTMP
* Web-to-print
* Serviços UGC (Conteúdo gerado pelo usuário)

>[!IMPORTANT]
O suporte para ativos de imagem vetorial UGC novos ou existentes no Adobe Dynamic Media terminou em 30 de setembro de 2021.

#### Testar o serviço de teste seguro {#test-secure-testing-service}

Para garantir que o serviço de Teste Seguro funcione conforme o esperado, faça o seguinte:

##### Prepare sua conta

1. Entre em contato com o Atendimento ao cliente do Adobe e solicite que ele ative o Teste seguro em sua conta.
1. No Adobe Experience Manager, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração de publicação do Dynamic Media]**.
1. Na página Servidor de imagem , no **[!UICONTROL Publicar contexto]** , selecione **[!UICONTROL Testar o fornecimento de imagem]**.
1. Selecione o **[!UICONTROL Segurança]** guia .
1. Para o **[!UICONTROL Endereço do cliente]** filtro, selecione **[!UICONTROL Adicionar]**.
1. No **[!UICONTROL Endereço IP]** digite um endereço IP.
1. No **[!UICONTROL Máscara]** digite uma máscara de rede.

   >[!NOTE]
   Se você adicionar mais de um endereço IP e uma máscara de rede, ela permitirá *all* Endereços IP para fazer chamadas de ativos e todos aparecem.

1. Faça uma das seguintes opções:

   * Para adicionar mais endereços IP, repita as três etapas anteriores.
   * Prossiga para a próxima etapa.

1. No canto superior direito da página Servidor de imagem, selecione **[!UICONTROL Salvar]**.
1. Faça upload das imagens desejadas para sua conta do Adobe Dynamic Media.

<!--    See [Upload files](uploading-files.md#uploading_files). -->

1. Certifique-se de que algumas imagens estejam marcadas para publicação e outras não estejam marcadas e envie o trabalho de publicação.

<!--    See [Publish files](publishing-files.md#publishing_files). -->

1. Determine o nome do seu serviço de Teste Seguro acessando **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração geral do Dynamic Media]**.
1. No **[!UICONTROL Servidor]** , localize o nome do servidor à direita de **[!UICONTROL Nome do servidor publicado]**.

Entre em contato com o Adobe Care se o nome do servidor estiver ausente ou se o URL para o servidor não funcionar.

##### Preparar variações do site

Você precisa de duas variações de um site que vincula os ativos publicados e não publicados:

* Versão pública - Vincule ativos usando a sintaxe de URL tradicional do Adobe Dynamic Media.
* Versão de armazenamento temporário - Vincule ativos usando a mesma sintaxe, mas com o nome do site Teste seguro .

##### Executar os testes

Execute os seguintes testes:

1. Verifique se os ativos estão visíveis na rede corporativa.

   Na rede corporativa identificada pelo intervalo de endereços IP definido anteriormente, a versão de preparo do site exibe todas as imagens, independentemente de serem ou não marcadas para publicação. Dessa forma, é possível testar sem disponibilizar acidentalmente as imagens antes de visualizar a aprovação ou o lançamento do produto.

   Confirme se a versão pública do seu site mostra os ativos publicados como anteriormente tinham experiência com o Adobe Dynamic Media.

1. De fora da rede corporativa, verifique se os ativos não publicados (ou seja, não marcados para publicação) estão protegidos do acesso de terceiros.

   Acesse sua rede de fora (como de seu computador doméstico ou por uma conexão 4G/5G) e verifique se a versão pública do site mostra todos os ativos publicados, mas nenhum do conteúdo não publicado.

   Confirme se a versão de armazenamento temporário não mostra nenhum ativo porque você está acessando o serviço de Teste Seguro a partir de um endereço IP não aprovado.

### Definir as configurações gerais do Dynamic Media {#configuring-application-general-settings}

>[!IMPORTANT]
A Configuração geral do Dynamic Media só estará disponível se:
* Você está executando o Dynamic Media no modo Scene7.
* Você tem um *existente* **[!UICONTROL Configuração do Dynamic Media]** (em **[!UICONTROL Cloud Services]**) no Adobe Experience Manager 6.5 ou no Experience Manager as a Cloud Service.
* Você é um administrador de sistema do Experience Manager com privilégios de administrador.


Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos para sua empresa. Esses servidores são usados para criar strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas da sua conta do .

Consulte também [Testar o serviço de teste seguro](/help/assets/dm-publish-settings.md#test-assets-before-making-public).

**Para configurar a Configuração geral do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, selecione o ícone Ferramentas e vá para **[!UICONTROL Ativos]** > **[!UICONTROL Configuração geral do Dynamic Media]**.
1. Na página Servidor , defina seu **[!UICONTROL Nome do servidor publicado]** e **[!UICONTROL Nome do servidor de origem]** e, em seguida, use as cinco guias para definir as configurações de publicação padrão.

   * [Servidor](#server-general-setting)
   * [Carregar no aplicativo](#upload-to-application)
   * [Edição de imagem](#image-editing-tab) guia
   * [PostScript](#postscript-tab) guia
   * [Photoshop](#photoshop-tab) guia
   * [PDF](#pdf-tab) guia
   * [Illustrator](#illustrator-tab) guia

   ![Página Configurações gerais do Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *página Configurações gerais do Dynamic Media , com o **[!UICONTROL Edição de imagem]**selecionada.*<br><br>

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

#### Servidor {#server-general-setting}

Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos para sua empresa. Esses servidores são usados para criar strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas da sua conta do .

| Opção | Descrição |
| --- | --- |
| **[!UICONTROL Nome do servidor publicado]** | Obrigatório.<br>Este servidor é o servidor CDN (Content Deliver Network) ao vivo usado em todas as chamadas de URL geradas pelo sistema que são específicas da sua conta. Não altere o nome deste servidor a menos que seja instruído a fazê-lo pelo Suporte Técnico Adobe. O nome deve usar `https://` no caminho. |
| **[!UICONTROL Nome do servidor de origem]** | Obrigatório.<br>Este servidor é usado somente para testes de controle de qualidade. Não altere o nome deste servidor a menos que seja instruído a fazê-lo pelo Suporte Técnico Adobe. |

#### Carregar no aplicativo {#upload-to-application}

* **[!UICONTROL Substituir imagens]**

   O Adobe Dynamic Media não permite que dois arquivos tenham o mesmo nome. A Adobe Dynamic Media ID de cada item (o nome da imagem menos a extensão do nome do arquivo) deve ser exclusiva. Por causa dessa regra, **[!UICONTROL Fazer upload para o aplicativo]** tem uma substituição. O efeito exato dessa opção depende da opção de Substituição de imagens especificada que você escolheu. Essas opções especificam como as imagens de substituição são carregadas: se eles substituem as imagens originais ou se tornam imagens duplicadas. Imagens duplicadas são renomeadas com um `-1`. Por exemplo, `chair.tif` é renomeado `chair-1.tif`. Essas opções afetam as imagens carregadas em uma pasta diferente da original ou as imagens com uma extensão de nome de arquivo diferente da original, como JPG, TIF ou PNG.

   | Opção Substituir imagens | Descrição |
   | --- | --- |
   | **[!UICONTROL Substituir na pasta atual, mesmo nome base/extensão]** | Padrão.<br>Essa opção é a regra mais rígida para substituição. Ela requer que você carregue a imagem de substituição na mesma pasta do original e que a imagem de substituição tenha a mesma extensão de nome de arquivo do original. Se esses requisitos não forem atendidos, uma duplicata será criada. |
   | **[!UICONTROL Substituir na pasta atual, mesmo nome base independentemente da extensão]** | Requer que você carregue a imagem de substituição na mesma pasta do original, no entanto, a extensão do nome do arquivo pode ser diferente do original. Por exemplo, chair.tif substitui chair.jpg. |
   | **[!UICONTROL Substituir em qualquer pasta, mesmo nome/extensão do ativo base]** | Requer que a imagem de substituição tenha a mesma extensão de nome de arquivo que a imagem original (por exemplo, chair.jpg deve substituir chair.jpg, não chair.tif). No entanto, é possível fazer upload da imagem de substituição para uma pasta diferente da original. A imagem atualizada reside na nova pasta; o arquivo não pode mais ser encontrado em seu local original. |
   | **[!UICONTROL Substituir em qualquer pasta, mesmo nome de ativo base independentemente da extensão]** | Essa é a regra de substituição mais inclusiva. Você pode fazer upload de uma imagem de substituição para uma pasta diferente do original, fazer upload de um arquivo com uma extensão de nome de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição residirá na nova pasta para a qual foi carregada. |

* **[!UICONTROL Preservar corte]**

   Controla a preservação de qualquer definição manual de cultura existente.

   Consulte também `preserveCrop` em [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) e [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambos no Guia de referência de visualizadores do Dynamic Media.

#### Opções padrão de upload {#default-upload-options}

##### Guia Edição de imagem {#image-editing-tab}

Esse filtro permite ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Ajuda a controlar a intensidade do efeito, o raio do efeito (conforme medido em pixels) e um limite de contraste que é ignorado.

O efeito Tirar nitidez da máscara usa as mesmas opções do filtro Tirar nitidez da máscara da Photoshop. Ao contrário do que o nome sugere, Tirar nitidez da máscara é um filtro de nitidez.

| Tirar nitidez das opções de Máscara | Descrição |
| --- | --- |
| **[!UICONTROL Quantidade]** | Obrigatório.<br>Controla a quantidade de contraste que é aplicada aos pixels da borda.<br>Pense nisso como a intensidade do efeito. A principal diferença entre os valores de quantidade de Tirar nitidez da máscara no Adobe Dynamic Media e os valores de quantidade no Adobe Photoshop é que o Photoshop tem um intervalo de quantidade de 1% a 500%. Enquanto no Adobe Dynamic Media, o intervalo de valores é `0.0` para `5.0`. Um valor de 5,0 no Adobe Dynamic Media é o equivalente aproximado de 500% no Photoshop; um valor de 0,9 é o equivalente a 90%, e assim por diante. |
| **[!UICONTROL Raio]** | Obrigatório.<br>Controla o raio do efeito.<br>O intervalo de valores é `0` para `250`. O efeito é executado em todos os pixels em uma imagem e irradia de todos os pixels em todas as direções. O raio é medido em pixels. Por exemplo, para obter um efeito de nitidez semelhante para uma imagem de 2000 x 2000 pixels e imagem de 500 x 500 pixels, você define um raio de dois pixels na imagem de 2000 x 2000 pixels. Em seguida, defina um valor de raio de um pixel na imagem de 500 x 500 pixels. Um valor maior é usado para uma imagem que tem mais pixels. |
| **[!UICONTROL Limite]** | Obrigatório.<br>O limite é um intervalo de contraste que é ignorado quando o filtro Tirar nitidez da máscara é aplicado. Esse efeito é importante para que nenhum &quot;ruído&quot; seja introduzido em uma imagem quando esse filtro for usado. O intervalo de valores é `0` - `255`, que é o número de etapas de brilho em uma imagem em tons de cinza. `0`=black, `128`=50% cinza e `255`=branco.<br>Um valor limite de `12` O ignora pequenas variações é o brilho do tom da pele para evitar a adição de ruído, mas ainda adiciona o contraste da borda a áreas contrastantes, como onde as pálpebras tocam a pele.<br>Se você tiver uma foto do rosto de alguém, a máscara de nitidez afeta as partes contrastantes da imagem. Por exemplo, onde as pálpebras e a pele se encontram para criar uma área de contraste óbvia e a própria pele lisa. Mesmo a pele mais suave apresenta alterações sutis nos valores de brilho. Se você não usar um valor de limite, o filtro acentuará essas sutis alterações em pixels da pele. Por sua vez, um efeito ruidoso e indesejável é criado enquanto o contraste nas pálpebras aumenta, aumentando a nitidez.<br>Para evitar esse problema, é introduzido um valor limite que informa ao filtro para ignorar pixels que não alteram o contraste drasticamente, como pele lisa.<br>No gráfico zipper mostrado anteriormente, observe a textura ao lado dos zippers. O ruído da imagem é exibido porque os valores de limite eram muito baixos para suprimir o ruído. |
| **[!UICONTROL Monocromático]** | Selecione para ativar o brilho (intensidade) da imagem da máscara de nitidez.<br>Desmarque para desfazer a nitidez de cada componente de cor separadamente. |

Consulte também [Nitidez de imagens no Adobe Dynamic Media e no servidor de imagens](/help/assets/assets/sharpening_images.pdf).

##### Guia PostScript {#postscript-tab}

Você pode rasterizar arquivos Adobe PostScript®, manter planos de fundo transparentes, escolher uma resolução e escolher um espaço de cores.

Você pode usar arquivos Adobe PostScript® (EPS) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao carregar arquivos de imagem PostScript (EPS), você pode formatá-los de várias maneiras. Você pode rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores.

| Opção PostScript | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter plano de fundo transparente em imagens renderizadas]** | Preserva a transparência em segundo plano do arquivo. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |

##### Guia Photoshop {#photoshop-tab}

Você pode criar modelos a partir de arquivos Adobe® Photoshop®, manter camadas, especificar como as camadas são nomeadas, extrair texto e especificar como as imagens são ancoradas em modelos.

| Opção Photoshop | Descrição |
| --- | --- |
| **[!UICONTROL Manter camadas]** | Arrasta as camadas na PSD, se houver, para ativos individuais. As camadas de ativo permanecem associadas ao PSD. É possível visualizá-los abrindo o arquivo PSD na Exibição de detalhes e selecionando o painel de camada. Consulte Exibição e edição de camadas em um arquivo PSD. |
| **[!UICONTROL Criar modelo]** | Cria um modelo a partir das camadas no arquivo PSD. |
| **[!UICONTROL Extrair texto]** | Extrai o texto para que os usuários possam pesquisar por texto em um Visualizador. |
| **[!UICONTROL Estender camadas ao tamanho do plano de fundo]** | Estende o tamanho das camadas de imagem cortadas até o tamanho da camada de plano de fundo. |
| **[!UICONTROL Nomeação de camada]** | Estende o tamanho das camadas de imagem cortadas até o tamanho da camada de plano de fundo.<br>・ ・ **[!UICONTROL Nome da camada]** - Nomeia as imagens depois dos nomes das camadas no arquivo PSD. Por exemplo, uma camada chamada Tag de preço no arquivo PSD original se torna uma imagem chamada Tag de preço. No entanto, se os nomes de camada no arquivo PSD forem nomes de camada padrão do Photoshop (Plano de fundo, Camada 1, Camada 2 e assim por diante), as imagens serão nomeadas após seus números de camada no arquivo PSD. <br>・ ・ **[!UICONTROL Photoshop e número da camada]** - Nomes das imagens depois de seus números de camada no arquivo PSD, ignorando nomes de camada originais. As imagens são nomeadas com o nome do arquivo Photoshop e um número de camada anexado. Por exemplo, a segunda camada de um arquivo chamado `Spring Ad.psd` é nomeado `Spring Ad_2` mesmo que tivesse um nome não padrão no Photoshop.<br>・ ・ **[!UICONTROL Photoshop e nome da camada]** - Nomeia as imagens após o PSD, seguido do nome da camada ou do número da camada. O número da camada é usado se os nomes da camada no arquivo PSD forem nomes padrão da camada do Photoshop. Por exemplo, uma camada chamada `Price Tag` em um arquivo PSD `SpringAd` é nomeado `Spring Ad_Price Tag`. Uma camada com o nome padrão Camada 2 é chamada `Spring Ad_2`. |
| **[!UICONTROL Âncora]** | Especifique como as imagens são ancoradas em modelos que são gerados a partir da composição em camadas produzida a partir do arquivo PSD. Por padrão, a âncora é o centro. Uma âncora central permite que imagens de substituição preencham melhor o mesmo espaço, independentemente da proporção da imagem de substituição. Imagens com um aspecto diferente que substituem essa imagem, ao referenciar o modelo e usar substituição de parâmetro, ocupam efetivamente o mesmo espaço. Altere para uma configuração diferente se o aplicativo exigir as imagens de substituição para preencher o espaço alocado no modelo. |

##### Guia PDF {#pdf-tab}

Você pode optar por rasterizar os arquivos, extrair palavras de pesquisa e links, definir a resolução e escolher um espaço de cores.

| opção PDF | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | ・ ・ **[!UICONTROL Nenhum]** - Não é efetuado qualquer processamento do PDF.<br>・ ・ **[!UICONTROL Miniatura]** - Remove cada página do arquivo PDF e a converte em uma imagem em miniatura.<br> ・ ・ **[!UICONTROL Rasterizar]** - Remove as páginas do arquivo PDF e converte gráficos vetoriais em imagens de bitmap. Para criar um eCatalog, escolha essa opção. |
| **[!UICONTROL Extrair]** | ・ ・ **[!UICONTROL Nenhum]** - Nenhuma palavra de pesquisa ou link é extraído do PDF.<br>・ ・ **[!UICONTROL Pesquisar palavras]** - Extrai palavras de pesquisa do arquivo PDF para que o arquivo possa ser pesquisado por palavra-chave em um visualizador de eCatalog.<br>・ ・ **[!UICONTROL Links]** - Extrai links dos arquivos do PDF e os converte em mapas de imagem usados em um visualizador de eCatalog.<br>・ ・ **[!UICONTROL Pesquisar palavras e links]** - Extrai palavras de pesquisa e links para uso em um visualizador de eCatalog. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Esta configuração determina quantos pixels são exibidos por polegada no arquivo PDF. O padrão é 150. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo PDF.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |

##### Guia Illustrator {#illustrator-tab}

Você pode rasterizar arquivos Adobe Illustrator®, manter planos de fundo transparentes, escolher uma resolução e escolher um espaço de cores.

Você pode usar arquivos Adobe® Illustrator® (AI) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao carregar arquivos de imagem do Illustrator (AI), você pode formatá-los de várias maneiras. Você pode rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores. As opções para formatar arquivos PostScript e Illustrator estão disponíveis na tela Upload em Opções de PostScript e Opções do Illustrator na caixa Opções de trabalho de upload .


| Opção Illustrator | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter plano de fundo transparente em imagens renderizadas]** | Preserva a transparência em segundo plano do arquivo. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |


**[!UICONTROL Perfis de cores padrão]** - Consulte [Configurar gerenciamento de cores](#configuring-color-management) para obter mais informações.

>[!NOTE]
Por padrão, o sistema mostra 15 execuções ao selecionar **[!UICONTROL Representações]** e 15 predefinições do visualizador ao selecionar **[!UICONTROL Visualizadores]** na exibição detalhada do ativo. Você pode aumentar esse limite. Consulte [Aumente o número de predefinições de imagens exibidas](/help/assets/managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display) ou [Aumentar o número de predefinições do visualizador exibidas](/help/assets/managing-viewer-presets.md#increasing-the-number-of-viewer-presets-that-display).

### (Opcional) Tarefas adicionais de configuração

As tarefas opcionais de configuração e configuração incluem o seguinte:

* [Editar tipos MIME para formatos compatíveis](#editing-mime-types-for-supported-formats) **RICK: CONTINUAR?**
* [Adicionar tipos MIME para formatos não suportados](#adding-mime-types-for-unsupported-formats) **RICK: CONTINUAR?**
* [Criar predefinições de conjunto de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação](#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets) **RICK: CONTINUAR?**

* **[!UICONTROL Atributos de compatibilidade]** - **RICK: AINDA É NECESSÁRIO? ESTAVA NO CLASSIC** Essa configuração permite que os parágrafos anteriores e posteriores em camadas de texto sejam tratados como na versão 3.6 para compatibilidade com versões anteriores.
* **[!UICONTROL Suporte à localização]** - **RICK: AINDA É NECESSÁRIO? ESTAVA NO CLASSIC** Essas configurações permitem gerenciar vários atributos de localidade. Ela também permite especificar uma sequência de mapa de localidade para que você possa definir quais idiomas deseja suportar para as várias dicas de ferramentas em Visualizadores. Para obter mais informações sobre como configurar **[Suporte à localização]**, consulte [Considerações ao configurar a localização de ativos](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/publish-setup.html#considerations-when-setting-up-localization-of-assets).

#### Editar tipos MIME para formatos compatíveis {#editing-mime-types-for-supported-formats}

**RICK: MANTER COMO ESTÁ??**

Você pode definir quais tipos de ativos são processados pelo Dynamic Media e personalizar parâmetros avançados de processamento de ativos. Por exemplo, você pode especificar parâmetros de processamento de ativos para fazer o seguinte:

* Converter um Adobe PDF em um ativo de eCatalog.
* Converta um documento do Adobe Photoshop (.PSD) em um ativo de modelo de banner para personalização.
* Rasterize um arquivo Adobe Illustrator (.AI) ou um arquivo Adobe Photoshop Encapsulated PostScript® (.EPS).
* [Perfis de vídeo](/help/assets/video-profiles.md) e [Perfis de imagens](/help/assets/image-profiles.md) pode ser usada para definir o processamento de vídeos e imagens, respectivamente.

Consulte [Upload de ativos](/help/assets/manage-assets.md#uploading-assets).

**Para editar tipos MIME para formatos compatíveis:**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e, em seguida, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. No painel à esquerda, navegue até o seguinte:

   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

   ![Tipos MIME](assets/mimetypes.png)

1. Na pasta mimeTypes , selecione um tipo MIME.
1. No lado direito da página CRXDE Lite, na parte inferior:

   * Clique duas vezes no botão **[!UICONTROL ativado]** campo. Por padrão, todos os tipos de ativos mime estão ativados (definido como **[!UICONTROL true]**), o que significa que os ativos são sincronizados com a Dynamic Media para processamento. Se desejar excluir esse tipo de ativo MIME do processamento, altere essa configuração para **[!UICONTROL false]**.

   * Toque duplo **[!UICONTROL jobParam]** para abrir o campo de texto associado. Consulte [Tipos Mime Suportados](/help/assets/assets-formats.md#supported-mime-types) para obter uma lista de valores de parâmetros de processamento permitidos, você pode usar para um determinado tipo MIME.

1. Faça uma das seguintes opções:

   * Repita as etapas 3 a 4 para editar mais tipos MIME.
   * Na barra de menu da página do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

1. No canto superior esquerdo da página, selecione **[!UICONTROL CRXDE Lite]** para voltar ao Experience Manager.

#### Adição de tipos MIME para formatos não suportados {#adding-mime-types-for-unsupported-formats}

**RICK: MANTER COMO ESTÁ??**

Você pode adicionar tipos MIME personalizados para formatos não compatíveis no Experience Manager Assets. Certifique-se de que qualquer novo nó adicionado no CRXDE Lite não seja excluído pelo Experience Manager movendo o tipo MIME antes de `image_`. Além disso, verifique se o valor ativado está definido como **[!UICONTROL false]**.

**Para adicionar tipos MIME para formatos não suportados:**

1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   ![2019-08-02_16-13-14](assets/2019-08-02_16-13-14.png)

1. Uma nova guia do navegador é aberta para o **[!UICONTROL Configuração do Console da Web do Adobe Experience Manager]** página.

   ![2019-08-02_16-17-29](assets/2019-08-02_16-17-29.png)

1. Na página, role para baixo até o nome *Adobe CQ Scene7 Asset MIME type Service*, como visto na seguinte captura de tela. À direita do nome, selecione a opção **[!UICONTROL Editar os valores de configuração]** (ícone de lápis).

   ![2019-08-02_16-44-56](assets/2019-08-02_16-44-56.png)

1. No **Serviço do tipo MIME do Adobe CQ Scene7 Asset** selecione qualquer ícone de sinal de mais &lt;+>. O local na tabela onde você seleciona o sinal de mais para adicionar o novo tipo MIME é trivial.

   ![2019-08-02_16-27-27](assets/2019-08-02_16-27-27.png)

1. Tipo `DWG=image/vnd.dwg` no campo de texto vazio que você acabou de adicionar.

   O exemplo `DWG=image/vnd.dwg` é somente para fins de demonstração. O tipo MIME adicionado aqui pode ser qualquer outro formato não suportado.

   ![2019-08-02_16-36-36](assets/2019-08-02_16-36-36.png)

1. No canto inferior direito da página, selecione **[!UICONTROL Salvar]**.

   Nesse ponto, você pode fechar a guia do navegador que tem a página de Configuração do Console da Web do Adobe Experience Manager aberta.

1. Retorne à guia do navegador que tem seu console de Experience Manager aberto.
1. No Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.

   ![2019-08-02_16-55-41](assets/2019-08-02_16-55-41.png)

1. No painel à esquerda, navegue até o seguinte:

   `conf/global/settings/cloudconfigs/dmscene7/jcr:content/mimeTypes`

1. Arraste o tipo mime `image_vnd.dwg` e solte-o diretamente acima `image_` na árvore, como visto na captura de tela a seguir.

   ![crxdelite_cqdoc-14627](assets/crxdelite_cqdoc-14627.png)

1. Com o tipo mime `image_vnd.dwg` ainda selecionado, no **[!UICONTROL Propriedades]** na guia , no **[!UICONTROL ativado]** , abaixo da **[!UICONTROL Valor]** no cabeçalho da coluna, toque duas vezes no valor para abrir a **[!UICONTROL Valor]** lista suspensa.
1. Tipo `false` no campo (ou selecione **[!UICONTROL false]** na lista suspensa).

   ![2019-08-02_16-60-30](assets/2019-08-02_16-60-30.png)

1. Próximo ao canto superior esquerdo da página do CRXDE Lite, selecione **[!UICONTROL Salvar tudo]**.

#### Criar predefinições de conjunto de lotes para gerar automaticamente Conjuntos de imagens e Conjuntos de rotação {#creating-batch-set-presets-to-auto-generate-image-sets-and-spin-sets}

**RICK: MANTER COMO ESTÁ??**

Use predefinições de conjuntos em lotes para automatizar a criação de conjuntos de imagens ou conjuntos de rotação enquanto os ativos são carregados no Dynamic Media.

Primeiro, defina a convenção de nomenclatura de como os ativos são agrupados em um conjunto. Em seguida, crie uma predefinição de conjunto de lotes que seja um conjunto de instruções autocontido e com nome exclusivo. Ele deve definir como construir o conjunto usando imagens que correspondam às convenções de nomenclatura definidas na receita predefinida.

Ao carregar arquivos, o Dynamic Media cria automaticamente um conjunto com todos os arquivos que correspondem à convenção de nomenclatura definida nas predefinições ativas.

##### Configurar nomenclatura padrão

Crie uma convenção de nomenclatura padrão que seja usada em qualquer fórmula predefinida de conjunto de lotes. A convenção de nomenclatura padrão selecionada na definição predefinida do conjunto de lotes provavelmente é tudo o que é necessário para a empresa gerar conjuntos em lote. Uma predefinição de conjunto de lotes é criada para usar a convenção de nomenclatura padrão que você define. Você pode criar quantas predefinições do Conjunto de Lotes tiverem as convenções de nomenclatura alternativas e personalizadas necessárias para um conjunto específico de conteúdo, em casos em que há uma exceção na nomenclatura padrão definida pela empresa.

Embora a configuração de uma convenção de nomenclatura padrão não seja necessária para usar a funcionalidade predefinida do conjunto de lotes, a prática recomendada é usar a convenção de nomenclatura padrão. Ele permite definir quantos elementos de sua convenção de nomenclatura você deseja agrupar em um conjunto, para que seja possível simplificar a criação do conjunto de lotes.

Como alternativa, você pode usar **[!UICONTROL Exibir código]** sem campos de formulário disponíveis. Nesta visualização, você cria suas definições de convenção de nomenclatura totalmente usando expressões regulares.

Dois elementos estão disponíveis para definição, Correspondência e Nome de base. Esses campos permitem definir todos os elementos de uma convenção de nomenclatura e identificar a parte da convenção usada para nomear o conjunto no qual eles estão contidos. A convenção de nomenclatura individual de uma empresa geralmente usa uma ou mais linhas de definição para cada um desses elementos. Você pode usar quantas linhas para sua definição exclusiva e agrupá-las em elementos distintos, como para Imagem principal, Elemento de cor, Elemento de exibição alternativo e Elemento de amostra.

**Para configurar a nomenclatura padrão:**

**RICK: MANTER COMO ESTÁ??**

1. Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente do Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Nomenclatura padrão]**.
1. Selecione **[!UICONTROL Exibir formulário]** ou **[!UICONTROL Exibir código]** para especificar como deseja exibir e inserir informações sobre cada elemento.

   Você pode selecionar a variável **[!UICONTROL Exibir código]** para exibir a criação do valor da expressão regular ao lado das seleções de formulário. É possível inserir ou alterar esses valores para ajudar a definir os elementos da convenção de nomenclatura, se a exibição do formulário limitar você por qualquer motivo. Se os valores não puderem ser analisados na visualização do formulário, os campos do formulário ficarão inativos.

   >[!NOTE]
   Campos de formulário desativados não executam nenhuma validação para confirmar se as expressões regulares estão corretas. Você verá os resultados da expressão regular que está criando para cada elemento após a linha Resultado. A expressão regular completa é visível na parte inferior da página.

1. Expanda cada elemento conforme necessário e insira as convenções de nomenclatura que deseja usar.
1. Conforme necessário, execute um dos seguintes procedimentos:

   * Selecionar **[!UICONTROL Adicionar]** para adicionar outra convenção de nomenclatura para um elemento.
   * Selecionar **[!UICONTROL Remover]** para excluir uma convenção de nomenclatura para um elemento.

1. Faça uma das seguintes opções:

   * Selecionar **[!UICONTROL Salvar como]** e digite um nome para a predefinição.
   * Selecionar **[!UICONTROL Salvar]** se você estiver editando uma predefinição existente.

##### Criar uma predefinição de conjunto de lotes

O Dynamic Media usa predefinições de conjuntos em lotes para organizar ativos em conjuntos de imagens (imagens alternativas, opções de cores, rotação 360) para exibição em visualizadores. As predefinições do conjunto de lotes são executadas automaticamente com os processos de upload de ativos no Dynamic Media.

Você pode criar, editar e gerenciar as predefinições do conjunto de lotes. Existem duas formas de definições predefinidas de conjunto de lotes: um para uma convenção de nomenclatura padrão que você pode configurar e um para convenções de nomenclatura personalizadas que você cria em tempo real.

Você pode usar o método de campo de formulário para definir uma predefinição de conjunto de lotes ou o método de código, que permite usar expressões regulares. Como em Nomenclatura padrão, você pode escolher Exibir código ao mesmo tempo em que está definindo na Exibição do formulário e usar expressões regulares para criar suas definições. Como alternativa, você pode desmarcar qualquer exibição para usar uma ou a outra exclusivamente.

**Para criar uma predefinição de conjunto de lotes:**

**RICK: MANTER COMO ESTÁ??**

1. Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente do Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Predefinição do conjunto de lotes]**.

   **[!UICONTROL Exibir formulário]**, conforme definido no canto superior direito da página Detalhes, é a exibição padrão.

1. No painel Lista de predefinições , selecione **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição , digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lote, selecione um tipo predefinido.
1. Faça uma das seguintes opções:

   * Se estiver usando uma convenção de nomenclatura padrão que você configurou anteriormente em **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Nomenclatura padrão]**, expandir **[!UICONTROL Convenções de nomenclatura de ativos]** e, na lista suspensa Nomenclatura de arquivo , selecione **[!UICONTROL Padrão]**.

   * Para definir uma nova convenção de nomenclatura conforme configura a predefinição, expanda **[!UICONTROL Convenções de nomenclatura de ativos]** e, na lista suspensa Nomenclatura de arquivo , selecione **[!UICONTROL Personalizado]**.

1. Para Ordem de sequência, defina a ordem na qual as imagens são exibidas após o conjunto ser agrupado em Dynamic Media.

   Por padrão, os ativos são classificados alfanumérico. No entanto, é possível usar uma lista separada por vírgulas de expressões regulares para definir a ordem.

1. Para Definir a Convenção de Nomenclatura e Criação, especifique o sufixo ou prefixo do nome básico definido na Convenção de Nomenclatura de Ativos. Além disso, defina onde o conjunto é criado na estrutura de pastas do Dynamic Media.

   Se você definir grandes números de conjuntos, mantenha os conjuntos separados das pastas que contêm os próprios ativos. Por exemplo, crie uma pasta Conjuntos de imagens e coloque os conjuntos gerados aqui.

1. No painel Detalhes, selecione **[!UICONTROL Salvar]**.
1. Selecionar **[!UICONTROL Ativo]** ao lado do novo nome predefinido.

   Ativar a predefinição garante que, ao fazer upload de ativos no Dynamic Media, a predefinição do conjunto de lotes seja aplicada para gerar o conjunto.

##### Criar uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D

Você pode usar o Tipo de Conjunto de Lotes **[!UICONTROL Conjunto de rotação de vários eixos]** para criar uma receita que automatize a geração de Conjuntos de rotação 2D. O agrupamento de imagens usa expressões regulares de Linha e Coluna para que os ativos de imagem sejam alinhados corretamente no local correspondente na matriz multidimensional. Não há um número mínimo ou máximo de linhas ou colunas que você deve ter em um conjunto de rotação de vários eixos.

Por exemplo, suponha que você queira criar um conjunto de rotação de vários eixos chamado `spin-2dspin`. Você tem um conjunto de imagens de conjunto de rotação que contém três linhas, com 12 imagens por linha. As imagens são nomeadas da seguinte maneira:

```
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

O agrupamento para a parte do nome do ativo compartilhado do conjunto de rotação é adicionado ao **[!UICONTROL Corresponder]** (como destacado). A parte variável do nome do ativo que contém a linha e a coluna é adicionada aos campos **[!UICONTROL Linha]** e **[!UICONTROL Coluna]**, respectivamente.

Quando o Conjunto de rotação é carregado e publicado, você ativaria o nome da fórmula do Conjunto de rotação 2D que está listada em **[!UICONTROL Predefinições de conjunto de lote]** na caixa de diálogo **[!UICONTROL Opções de trabalho de upload]**.

**Para criar uma predefinição de conjunto de lotes para a geração automática de um conjunto de rotação 2D:**

**RICK: MANTER COMO ESTÁ??**

1. Abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta.

   Suas credenciais e detalhes de logon foram fornecidos pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte ao cliente do Adobe.

1. Na barra de navegação próxima à parte superior da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Predefinições do conjunto de lotes]** > **[!UICONTROL Predefinição do conjunto de lotes]**.

   **[!UICONTROL Exibir formulário]**, conforme definido no canto superior direito da página Detalhes, é a exibição padrão.

1. No painel Lista de predefinições , selecione **[!UICONTROL Adicionar]** para ativar os campos de definição no painel Detalhes no lado direito da tela.
1. No painel Detalhes, no campo Nome da predefinição , digite um nome para a predefinição.
1. No menu suspenso Tipo de conjunto de lote, selecione **[!UICONTROL Conjunto de ativos]**.
1. Na lista suspensa Subtipo , selecione **[!UICONTROL Conjunto de rotação de vários eixos]**.
1. Expandir **[!UICONTROL Convenções de nomenclatura de ativos]** e, na lista suspensa Nomenclatura de arquivo , selecione **[!UICONTROL Personalizado]**.
1. Use os atributos **[!UICONTROL Correspondência]** e, opcionalmente, **[!UICONTROL Nome de base]** para definir uma expressão regular para nomear ativos de imagem que compõem o agrupamento.

   Por exemplo, a expressão regular Correspondência literal pode ter a seguinte aparência:

   `(w+)-w+-w+`

1. Expandir **[!UICONTROL Posição da Coluna da Linha]** e, em seguida, defina o formato do nome para a posição do ativo de imagem dentro da matriz de Conjunto de rotação 2D.

   Use os parênteses para abraçar a posição da linha ou da coluna no nome do arquivo.

   Por exemplo, para a expressão regular da linha, ela pode ter a seguinte aparência:

   `\w+-R([0-9]+)-\w+`

   ou

   `\w+-(\d+)-\w+`

   Para a expressão regular da coluna, ela pode ter a seguinte aparência:

   `\w+-\w+-C([0-9]+)`

   ou

   `\w+-\w+-C(\d+)`

   As amostras acima são apenas para fins de demonstração. Você pode criar sua expressão regular da maneira que quiser, de acordo com suas necessidades.

   >[!NOTE]
   Se a combinação de expressões regulares de linha e coluna não puder determinar a posição do ativo dentro da matriz de conjunto de rotação multidimensional, o ativo não será adicionado ao conjunto. Um erro também é registrado.

1. Para Definir a Convenção de Nomenclatura e Criação, especifique o sufixo ou prefixo do nome básico definido na Convenção de Nomenclatura de Ativos.

   Além disso, defina onde o conjunto de rotação é criado na estrutura de pastas do Dynamic Media Classic.

   Se você definir grandes números de conjuntos, mantenha os conjuntos separados das pastas que contêm os próprios ativos. Por exemplo, crie uma pasta Conjuntos de rotação para colocar conjuntos gerados aqui.

1. No painel Detalhes, selecione **[!UICONTROL Salvar]**.
1. Selecionar **[!UICONTROL Ativo]** ao lado do novo nome predefinido.

   Ativar a predefinição garante que, ao fazer upload de ativos no Dynamic Media, a predefinição do conjunto de lotes seja aplicada para gerar o conjunto.

### (Opcional) Ajustar o desempenho do Dynamic Media - Modo Scene7 {#optional-tuning-the-performance-of-dynamic-media-scene-mode}

**RICK: MANTER COMO ESTÁ??**

Para manter o Dynamic Media - modo Scene7 em execução sem problemas, o Adobe recomenda as seguintes dicas de ajuste de desempenho/escalabilidade de sincronização:

* Atualização dos parâmetros de Trabalho predefinidos para processamento de diferentes formatos de arquivo.
* Atualizar os encadeamentos de trabalho de fila predefinidos do fluxo de trabalho Granite (ativos de vídeo).
* Atualização dos threads de trabalho de fila predefinidos do fluxo de trabalho transitório do Granite (imagens e ativos que não são de vídeo).
* Atualização das conexões máximas de upload para o servidor do Dynamic Media Classic.

#### Atualizar os parâmetros de Trabalho predefinidos para o processamento de diferentes formatos de arquivo

**RICK: MANTER COMO ESTÁ??**

Você pode ajustar parâmetros de trabalho para processamento mais rápido ao carregar arquivos. Por exemplo, se você carregar arquivos PSD, mas não quiser processá-los como modelos, poderá definir a extração de camada como false (off). Nesse caso, o parâmetro de trabalho ajustado aparece da seguinte maneira: `process=None&createTemplate=false`.

Caso deseje ativar a criação do modelo, use os seguintes parâmetros: `process=MaintainLayers&layerNaming=AppendName&createTemplate=true`.

<!-- THIS PARAGRAPH WAS REPLACED WITH THE TWO PARAGRAPHS DIRECTLY ABOVE BASED ON CQDOC-17657 You can tune job parameters for faster processing when you upload files. For example, if you are uploading PSD files, but do not want to process them as templates, you can set layer extraction to false (off). In such case, the tuned job parameter would appear as `process=None&createTemplate=false`. -->

O Adobe recomenda usar os seguintes parâmetros de trabalho &quot;ajustados&quot; para arquivos PDF, PostScript® e PSD:

<!-- OLD PDF JOB PARAMETERS `pdfprocess=Rasterize&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` -->

<!-- OLD POSTSCRIPT JOB PARAMETERS `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Rasterize&airesolution=150&aicolorspace=Auto&aialpha=false` -->

| Tipo de arquivo | Parâmetros de tarefa recomendados |
| ---| ---|
| PDF | `pdfprocess=Thumbnail&resolution=150&colorspace=Auto&pdfbrochure=false&keywords=false&links=false` |
| PostScript® | `psprocess=Rasterize&psresolution=150&pscolorspace=Auto&psalpha=false&psextractsearchwords=false&aiprocess=Thumbnail&airesolution=150&aicolorspace=Auto&aialpha=false` |
| PSD | `process=None&layerNaming=AppendName&anchor=Center&createTemplate=false&extractText=false&extendLayers=false` |

<!-- CQDOC-17657 for PSD entry in table above -->

Para atualizar qualquer um desses parâmetros, siga as etapas em [Ativar o suporte ao parâmetro de trabalho de upload do Dynamic Media Classic/Ativos baseados em tipo MIME](/help/sites-administering/scene7.md#enabling-mime-type-based-assets-scene-upload-job-parameter-support).

#### Atualizar a fila de fluxo de trabalho transitório do Granite {#updating-the-granite-transient-workflow-queue}

**RICK: MANTER COMO ESTÁ??**

A fila Fluxo de trabalho de trânsito do Granite é usada para **[!UICONTROL Ativo de atualização DAM]** fluxo de trabalho. No Dynamic Media, é usado para assimilação e processamento de imagens.

**Para atualizar a fila de fluxo de trabalho transitório do Granite:**

1. Navegar para [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr) e procurar **Fila: Fila de Fluxo de Trabalho Transitório do Granite**.

   >[!NOTE]
   Uma pesquisa de texto é necessária em vez de um URL direto porque o PID do OSGi é gerado dinamicamente.

1. No **[!UICONTROL Máximo de trabalhos paralelos]** altere o número para o valor desejado.

   Você pode aumentar **[!UICONTROL Máximo de trabalhos paralelos]** para suportar adequadamente o upload pesado de arquivos para o Dynamic Media. O valor exato depende da capacidade do hardware. Em determinados cenários - ou seja, uma migração inicial ou um upload em massa único - é possível usar um valor grande. Esteja ciente, no entanto, de que o uso de um valor grande (como duas vezes o número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, teste e ajuste o valor com base no seu caso de uso específico.

<!--    By default, the maximum number of parallel jobs depends on the number of available CPU cores. For example, on a 4-core server, it assigns 2 worker threads. (A value between 0.0 and 1.0 is ratio based, or any numbers greater than 1 will assign the number of worker threads.)

   Adobe recommends that 32 **[!UICONTROL Maximum Parallel Jobs]** be configured to adequately support heavy upload of files to Dynamic Media Classic (Scene7). -->

![chlimage_1](assets/chlimage_1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a fila do fluxo de trabalho do Granite {#updating-the-granite-workflow-queue}

**RICK: MANTER COMO ESTÁ??**

A fila Fluxo de trabalho do Granite é usada para fluxos de trabalho não transitórios. No Dynamic Media, ele processava vídeo com a variável **[!UICONTROL Codificar vídeo no Dynamic Media]** fluxo de trabalho.

**Para atualizar a fila do fluxo de trabalho do Granite:**

1. Navegar para `https://<server>/system/console/configMgr` e procurar **Fila: Fila de Fluxo de Trabalho do Granite**.

   >[!NOTE]
   Uma pesquisa de texto é necessária em vez de um URL direto porque o PID do OSGi é gerado dinamicamente.

1. No **[!UICONTROL Máximo de trabalhos paralelos]** altere o número para o valor desejado.

   Você pode aumentar o número máximo de trabalhos paralelos para suportar adequadamente o upload pesado de arquivos para o Dynamic Media. O valor exato depende da capacidade do hardware. Em determinados cenários - ou seja, uma migração inicial ou um upload em massa único - é possível usar um valor grande. Esteja ciente, no entanto, de que o uso de um valor grande (como duas vezes o número de núcleos) pode ter efeitos negativos em outras atividades simultâneas. Dessa forma, teste e ajuste o valor com base no seu caso de uso específico.

   ![chlimage_1-1](assets/chlimage_1-1.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

#### Atualizar a conexão de upload do Dynamic Media Classic {#updating-the-scene-upload-connection}

**RICK: MANTER COMO ESTÁ??**

A configuração Scene7 Upload Connection sincroniza ativos do Experience Manager para servidores da Dynamic Media Classic.

**Para atualizar a conexão de upload do Dynamic Media Classic:**

1. Vá até `https://<server>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl`
1. No **[!UICONTROL Número de conexões]** e/ou o **[!UICONTROL Tempo limite do trabalho ativo]** altere o número conforme desejado.

   O **[!UICONTROL Número de conexões]** A configuração controla o número máximo de conexões HTTP permitidas para upload do Experience Manager para o Dynamic Media; normalmente, o valor predefinido de dez conexões é suficiente.

   O **[!UICONTROL Tempo limite do trabalho ativo]** determina o tempo de espera para que os ativos carregados do Dynamic Media sejam publicados no servidor de entrega. Esse valor é de 2100 segundos ou 35 minutos por padrão.

   Para a maioria dos casos de uso, a configuração de 2100 é suficiente.

   ![chlimage_1-2](assets/chlimage_1-2.jpeg)

1. Selecione **[!UICONTROL Salvar]**.

### (Opcional) Filtrar ativos para replicação {#optional-filtering-assets-for-replication}

**RICK: MANTER COMO ESTÁ**

Em implantações que não são da Dynamic Media, você replica *all* ativos (imagens e vídeo) do ambiente de criação do Experience Manager para o nó de publicação do Experience Manager. Esse workflow é necessário porque os servidores de Publicação do Experience Manager também entregam os ativos.

No entanto, em implantações do Dynamic Media, como os ativos são fornecidos por meio do Cloud Service, não há necessidade de replicar esses mesmos ativos para nós de publicação do Experience Manager. Esse workflow de &quot;publicação híbrida&quot; evita custos de armazenamento extras e tempos de processamento mais longos para replicar ativos. Outros conteúdos, como páginas do Site, continuam a ser veiculados a partir dos nós de publicação do Experience Manager.

Os filtros fornecem uma maneira de *exclude* ativos de serem replicados para o nó de publicação do Experience Manager.

#### Usar filtros de ativos padrão para replicação {#using-default-asset-filters-for-replication}

**RICK: MANTER COMO ESTÁ**

Se você usa o Dynamic Media para geração de imagens, ou vídeo, ou ambos, você pode usar os filtros padrão que o Adobe fornece como estão. Os seguintes filtros estão ativos por padrão:

|  | Filtro | Tipo Mime | Representações |
| --- | --- | --- | --- |
| Entrega de imagem do Dynamic Media | filter-image<br>conjuntos de filtros | Começa com **image/**<br> Contém **aplicativos/** e terminar com **set**. | As &quot;imagens-filtro&quot; prontas para uso (aplica-se a ativos de imagens individuais, incluindo imagens interativas) e &quot;conjuntos de filtros&quot; (aplica-se a Conjuntos de rotação, Conjuntos de imagens, Conjuntos de mídia mista e Conjuntos de carrossel):<br>・ Excluir da replicação a imagem original e as representações de imagem estática. |
| Entrega de vídeo do Dynamic Media | filter-video | Começa com **video/** | O &quot;vídeo de filtro&quot; pronto para uso:<br>・ Excluir da replicação o vídeo original e as representações de miniatura estáticas. |

>[!NOTE]
Os filtros se aplicam aos tipos MIME e não podem ser específicos de caminho.

#### Personalizar filtros de ativos para replicação {#customizing-asset-filters-for-replication}

**RICK: MANTER COMO ESTÁ**

1. No Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global e navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL CRXDE Lite]**.
1. Na árvore da pasta esquerda, navegue até `/etc/replication/agents.author/publish/jcr:content/damRenditionFilters` para analisar os filtros.

   ![chlimage_1-17](assets/chlimage_1-2.png)

1. Para definir o Tipo MIME para o filtro, você pode localizar o Tipo MIME da seguinte maneira:

   No painel esquerdo, expanda `content > dam > <locate_your_asset> > jcr:content > metadata`e, em seguida, na tabela, localize `dc:format`.

   O gráfico a seguir é um exemplo do caminho de um ativo para `dc:format`.

   ![chlimage_1-18](assets/chlimage_1-3.png)

   Observe que a variável `dc:format` para o ativo `Fiji Red.jpg` é `image/jpeg`.

   Para que esse filtro se aplique a todas as imagens, independentemente do formato, defina o valor como `image/*` em que `*` é uma expressão regular aplicada a todas as imagens de qualquer formato.

   Para que o filtro seja aplicado somente às imagens do JPEG de tipo , insira um valor de `image/jpeg`.

1. Defina quais representações deseja incluir ou excluir da replicação.

   Os caracteres que você pode usar para filtrar para replicação incluem:

   | Caractere a ser usado | Como ele filtra ativos para replicação |
   | --- | --- |
   | * | Caracteres curingas |
   | + | Inclui ativos para replicação |
   | - | Exclui ativos da replicação |

   Vá até `content/dam/<locate your asset>/jcr:content/renditions`.

   O gráfico a seguir é um exemplo das representações de um ativo.

   ![chlimage_1-4](assets/chlimage_1-4.png)

   Se você quiser apenas replicar o original, insira `+original`.
