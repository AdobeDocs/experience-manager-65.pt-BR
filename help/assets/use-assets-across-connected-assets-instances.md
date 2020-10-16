---
title: Use o Connected Assets para compartilhar ativos do DAM no [!DNL Sites]
description: Use ativos disponíveis em uma implantação [!DNL Adobe Experience Manager Assets] deployment when creating your web pages on another [!DNL Adobe Experience Manager Sites] remota.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 2c3836cb7e2275c30e88e8a750eafce24a05837a
workflow-type: tm+mt
source-wordcount: '2247'
ht-degree: 41%

---


# Use o Connected Assets para compartilhar ativos do DAM no [!DNL Experience Manager Sites] {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais usados para criar esses sites podem residir em diferentes implantações. Um motivo pode ser a distribuição geográfica de implantações existentes necessárias para trabalhar em conjunto. Outra razão pode ser as aquisições que levam a uma infraestrutura heterogênea que a empresa pai quer usar em conjunto.

Os usuários podem criar páginas da Web em [!DNL Experience Manager Sites]. [!DNL Experience Manager Assets] é o sistema de Gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites. [!DNL Experience Manager] agora suporta o caso de uso acima, integrando [!DNL Sites] e [!DNL Assets].

## Visão geral do Connected Assets {#overview-of-connected-assets}

When editing pages in [!UICONTROL Page Editor], the authors can seamlessly search, browse, and embed assets from a different [!DNL Assets] deployment. Os administradores criam uma integração única de uma implantação do [!DNL Sites] com uma implantação diferente (remota) do [!DNL Assets].

For the [!DNL Sites] authors, the remote assets are available as read-only local assets. A funcionalidade suporta pesquisa e uso ininterruptos de alguns ativos remotos de cada vez. To make many remote assets available on a [!DNL Sites] deployment in one-go, consider migrating the assets in bulk. Consulte Guia [de migração dos ativos](/help/assets/assets-migration-guide.md)Experience Manager.

### Pré-requisitos e implantações compatíveis {#prerequisites}

Antes de usar ou configurar esse recurso, verifique o seguinte:

* Os usuários fazem parte dos grupos de usuários apropriados em cada implantação.
* For [!DNL Adobe Experience Manager] deployment types, one of the supported criteria is met. [!DNL Experience Manager] 6.5 [!DNL Assets] funciona como um Cloud Service [!DNL Experience Manager] . Para obter mais informações, consulte Funcionalidade de ativos [conectados no Experience Manager como Cloud Service](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html).

   |  | [!DNL Sites] como um Cloud Service | [!DNL Experience Manager] 6.5 [!DNL Sites] no AMS | [!DNL Experience Manager] 6.5 [!DNL Sites] local |
   |---|---|---|---|
   | **[!DNL Experience Manager Assets]como um Cloud Service** | Compatível | Compatível | Compatível |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] no AMS** | Compatível | Compatível | Compatível |
   | **[!DNL Experience Manager]6.5 [!DNL Assets] local** | Incompatível | Incompatível | Incompatível |

### Formatos de arquivo não suportados {#mimetypes}

Os autores pesquisam por imagens e pelos seguintes tipos de documentos no Localizador de conteúdo e usam os ativos pesquisados no Editor de páginas. Documentos são adicionados ao `Download` componente e às imagens ao `Image` componente. Authors also add the remote assets in any custom [!DNL Experience Manager] component that extends the default `Download` or `Image` components. Os formatos suportados são:

* **Formatos** de imagem: Os formatos suportados pelo componente [](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/components/image.html) de Imagem. [!DNL Dynamic Media] as imagens não são compatíveis.
* **Formatos** de documento: Consulte os formatos [de documento](assets-formats.md#supported-document-formats)suportados.

### Usuários e grupos envolvidos {#users-and-groups-involved}

As várias funções envolvidas para configurar e usar o recurso e seus grupos de usuários correspondentes são descritas abaixo. O escopo local é usado para o caso de uso em que um autor cria uma página da Web. O escopo remoto é usado para a implantação do DAM que hospeda os ativos necessários. The [!DNL Sites] author fetches these remote assets.

| Função | Escopo | Grupo de usuários | Nome do usuário na apresentação | Requisito |
|---|---|---|---|---|
| [!DNL Sites] administrador | Local | [!DNL Experience Manager] `administrators` | `admin` | Set up [!DNL Experience Manager] and configure integration with the remote [!DNL Assets] deployment. |
| Usuário do DAM | Local | `Authors` | `ksaner` | Usado para exibir e duplicar os ativos pesquisados em `/content/DAM/connectedassets/`. |
| [!DNL Sites] author | Local | `Authors` (com acesso de leitura no DAM remoto e acesso de autor no local [!DNL Sites]) | `ksaner` | End user are [!DNL Sites] authors who use this integration to improve their content velocity. The authors search and browse assets in remote DAM using [!UICONTROL Content Finder] and using the required images in local web pages. As credenciais do usuário do DAM `ksaner` são usadas. |
| [!DNL Assets] administrador | Remoto | [!DNL Experience Manager] `administrators` | `admin` em remoto [!DNL Experience Manager] | Configure o CORS (Cross-Origin Resource Sharing). |
| Usuário do DAM | Remoto | `Authors` | `ksaner` em remoto [!DNL Experience Manager] | Author role on the remote [!DNL Experience Manager] deployment. Search and browse assets in Connected Assets using the [!UICONTROL Content Finder]. |
| Distribuidor do DAM (usuário técnico) | Remoto | [!DNL Sites] `Authors` | `ksaner` em remoto [!DNL Experience Manager] | This user present on the remote deployment is used by [!DNL Experience Manager] local server (not the [!DNL Sites] author role) to fetch the remote assets, on behalf of [!DNL Sites] author. Essa função não é igual às duas funções `ksaner` acima e pertence a um grupo de usuários diferente. |

## Configure a connection between [!DNL Sites] and [!DNL Assets] deployments {#configure-a-connection-between-sites-and-assets-deployments}

An [!DNL Experience Manager] administrator can create this integration. Depois de criadas, as permissões necessárias para usá-las são estabelecidas por meio de grupos de usuários. Os grupos de usuários são definidos na [!DNL Sites] implantação e na implantação do DAM.

To configure Connected Assets and local [!DNL Sites] connectivity, follow these steps:

1. Access an existing [!DNL Sites] deployment or create a deployment using the following command:

   1. In the folder of the JAR file, execute the following command on a terminal to create each [!DNL Experience Manager] server.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. After a few minutes, the [!DNL Experience Manager] server starts successfully. Consider this [!DNL Sites] deployment as the local machine for web page authoring, say at `https://[local_sites]:4502`.

1. Ensure that the users and roles with local scope exist on the [!DNL Sites] deployment and on the [!DNL Assets] deployment on AMS. Create a technical user on [!DNL Assets] deployment and add to the user group mentioned in [users and groups involved](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Access the local [!DNL Sites] deployment at `https://[local_sites]:4502`. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração do Connected Assets]** e forneça os seguintes valores:

   1. [!DNL Assets] o local é `https://[assets_servername_ams]:[port]`.
   1. Credenciais de um distribuidor do DAM (usuário técnico).
   1. In the **[!UICONTROL Mount Point]** field, enter the local [!DNL Experience Manager] path where [!DNL Experience Manager] fetches the assets. Por exemplo, pasta `remoteassets`.
   1. Ajuste os valores do **[!UICONTROL Limite de otimização da transferência do binário original]**, dependendo da sua rede. Uma representação de ativos maior que esse limite é transferida de forma assíncrona.
   1. Selecione **[!UICONTROL Datastore compartilhado com o Connected Assets]**, se você usar um datastore para armazenar seus ativos e se o Datastore for o armazenamento comum entre as duas implantações do Nesse caso, o limite não importa, pois os binários de ativos reais residem no datastore e não são transferidos.

   ![Uma configuração normal do Connected Assets](assets/connected-assets-typical-config.png)

   *Figura: uma configuração normal do Connected Assets.*

1. Como os ativos já são processados e as representações são buscadas, desative os inicializadores do fluxo de trabalho. Adjust the launcher configurations on the local ([!DNL Sites]) deployment to exclude the `connectedassets` folder, in which the remote assets are fetched.

   1. On [!DNL Sites] deployment, click **[!UICONTROL Tools]** > **[!UICONTROL Workflow]** > **[!UICONTROL Launchers]**.

   1. Procure Iniciadores com fluxos de trabalho como **[!UICONTROL Ativo de atualização do DAM]** e **[!UICONTROL Writeback de metadados do DAM]**.

   1. Selecione o iniciador do fluxo de trabalho e clique em **[!UICONTROL Propriedades]** na barra de ações.

   1. In the [!UICONTROL Properties] wizard, change the **[!UICONTROL Path]** fields as the following mappings to update their regular expressions to exclude the mount point **[!UICONTROL connectedassets]**.

   | Antes | Depois |
   |---|---|
   | `/content/dam(/((?!/subassets).)*/)renditions/original` | `/content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*/)renditions/original` | `/content/dam(/((?!connectedassets).)*/)renditions/original` |
   | `/content/dam(/.*)/jcr:content/metadata` | `/content/dam(/((?!connectedassets).)*/)jcr:content/metadata` |

   >[!NOTE]
   >
   >Todas as representações disponíveis na implantação remota do são buscadas, quando os autores buscam um ativo. Se você quiser criar mais representações de um ativo buscado, pule esta etapa de configuração. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Add the [!DNL Sites] deployment as one of the **[!UICONTROL Allowed Origins]** on the remote [!DNL Assets'] CORS configuration.

   1. Faça logon usando as credenciais de administrador. Pesquisar `Cross-Origin`. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   1. To create a CORS configuration for [!DNL Sites] deployment, click add option ![Assets add icon](assets/do-not-localize/assets_add_icon.png) next to **[!UICONTROL Adobe Granite Cross-Origin Resource Sharing Policy]**.

   1. In the field **[!UICONTROL Allowed Origins]**, input the URL of the local [!DNL Sites], that is, `https://[local_sites]:[port]`. Salve a configuração.

## Use ativos remotos {#use-remote-assets}

Os autores do site usam o Localizador de conteúdo para se conectar à implantação do DAM. Os autores podem procurar, buscar e arrastar os ativos remotos em um componente. Para autenticar no DAM remoto, mantenha acessíveis as credenciais do usuário do DAM fornecidas pelo administrador.

Os autores podem usar os ativos disponíveis no DAM local e a implantação remota do DAM, em uma única página da Web. Use o Localizador de conteúdo para alternar entre a pesquisa no DAM local ou a pesquisa no DAM remoto.

Somente as tags de ativos remotos que têm uma tag correspondente exata junto com a mesma hierarquia de taxonomia, estão disponíveis na [!DNL Sites] implantação local. Quaisquer outras tags são descartadas. Authors can search for remote assets using all the tags present on the remote [!DNL Experience Manager] deployment, as it offers a full-text search.

### Apresentação do uso {#walk-through-of-usage}

Use a configuração acima para ter uma experiência de criação a fim de entender a funcionalidade. Use documentos ou imagens de sua escolha na implantação remota do DAM.

1. Navigate to the [!DNL Assets] interface on the remote deployment by accessing **[!UICONTROL Assets]** > **[!UICONTROL Files]** from [!DNL Experience Manager] workspace. Como alternativa, acesse `https://[assets_servername_ams]:[port]/assets.html/content/dam` em um navegador. Carregue os ativos de sua escolha.
1. On the [!DNL Sites] deployment, in the profile activator in the upper-right corner, click **[!UICONTROL Impersonate as]**. Forneça `ksaner` como nome de usuário, selecione a opção fornecida e clique em **[!UICONTROL OK]**.
1. Abra uma página do site We.Retail em **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL br]** > **[!UICONTROL pt]**. Edite a página. Como alternativa, acesse `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` em um navegador para editar uma página.

   Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo da página.

1. Open the [!UICONTROL Assets] tab and click **[!UICONTROL Log in to Connected Assets]**.
1. Forneça as credenciais - `ksaner` como nome de usuário e `password` como senha. This user has authoring permissions on both the [!DNL Experience Manager] deployments.
1. Procure o ativo que você adicionou ao DAM. Os ativos remotos são exibidos no painel esquerdo. Filtre por imagens ou documentos e filtre também por tipos de documentos compatíveis. Arraste as imagens em um componente `Image` e os documentos em um componente `Download`.

   The fetched assets are read-only on the local [!DNL Sites] deployment. You can still use the options provided by your [!DNL Sites] components to edit the fetched asset. A edição por componentes não é destrutiva.

   ![Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto.*

1. Um autor do site será notificado se ocorrer uma busca assíncrona de ativo e uma falha na tarefa de busca. Durante a criação ou até mesmo após a criação, os autores podem ver informações detalhadas sobre as tarefas de busca e erros na interface do usuário de [trabalhos assíncronos](/help/sites-administering/asynchronous-jobs.md).

   ![Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.*

1. When publishing a page, [!DNL Experience Manager] displays a complete list of assets that are used on the page. Verifique se os ativos remotos foram buscados com êxito no momento da publicação. Para verificar o status de cada ativo buscado, consulte a interface do usuário de [trabalhos assíncronos](/help/sites-administering/asynchronous-jobs.md).

   >[!NOTE]
   >
   >Mesmo se um ou mais ativos remotos não forem buscados, a página será publicada. O componente que usa o ativo remoto é publicado vazio. The [!DNL Experience Manager] notification area displays a notification for errors that show in async jobs page.

>[!CAUTION]
>
>Depois de usados em uma página da Web, os ativos remotos obtidos são pesquisáveis e utilizáveis por qualquer pessoa que tenha permissões para acessar a pasta local. Os ativos buscados são armazenados na pasta local (`connectedassets` na apresentação acima). Os ativos também podem ser pesquisados e visualizados no repositório local por meio do [!UICONTROL Localizador de conteúdo].

Os ativos buscados podem ser usados como qualquer outro ativo local, exceto se os metadados associados não puderem ser editados.

## Limitações         and best practices {#tips-and-limitations}

* Para obter insights sobre o uso de ativos, configure a funcionalidade [Asset Insight](/help/assets/touch-ui-asset-insights.md) na [!DNL Sites] instância.

### Permissões e gerenciamento de ativos {#permissions-and-managing-assets}

* Os ativos locais não são sincronizados com os ativos originais na implantação remota. As edições, exclusões ou revogação de permissões na implantação do DAM não são propagadas para a jusante.
* Os ativos locais são cópias somente leitura. [!DNL Experience Manager]Os componentes do fazem edições não destrutivas nos ativos. Nenhuma outra edição é permitida.
* Os ativos buscados localmente estão disponíveis apenas para fins de criação. Os fluxos de trabalho de atualização de ativos não podem ser aplicados e os metadados não podem ser editados.
* Somente as imagens e os formatos de documento listados são compatíveis. [!DNL Dynamic Media] ativos, Fragmentos de conteúdo e Fragmentos de experiência não são suportados.
* [!DNL Experience Manager] não busca os schemas de metadados. Isso significa que nem todos os metadados obtidos podem ser exibidos. Se o schema for atualizado separadamente, todas as propriedades serão exibidas.
* Todos os [!DNL Sites] autores têm permissões de leitura nas cópias buscadas, mesmo se os autores não puderem acessar a implantação remota do DAM.
* Não há suporte de API para personalizar a integração.
* A funcionalidade suporta pesquisa e uso ininterruptos de ativos remotos. Para disponibilizar muitos ativos remotos em uma única implantação local, considere migrar os ativos. Consulte [guia de migração de Ativos](assets-migration-guide.md).
* Não é possível usar um ativo remoto como uma miniatura de página na interface do usuário Propriedades [!UICONTROL da] página. Você pode definir uma miniatura de uma página da Web na interface do usuário Propriedades [!UICONTROL da] página na [!UICONTROL miniatura] clicando em [!UICONTROL Selecionar imagem].

### Configuração e licenciamento {#setup-licensing}

* [!DNL Assets] a implantação em [!DNL Adobe Managed Services] é suportada.
* [!DNL Sites] pode se conectar a um único [!DNL Assets] repositório de cada vez.
* A license of [!DNL Assets] working as remote repository.
* One or more licenses of [!DNL Sites] working as local authoring deployment.

### Uso {#usage}

* Os usuários podem pesquisar ativos remotos e arrastá-los na página local durante a criação. Nenhuma outra funcionalidade é suportada.
* A operação de busca expira após 5 segundos. Os autores podem ter problemas ao buscar ativos, digamos se houver problemas de rede. Authors can reattempt by dragging the remote asset from [!UICONTROL Content Finder] to [!UICONTROL Page Editor].
* Edições simples que não são destrutivas e a edição compatível por meio do componente `Image` do podem ser realizadas nos ativos buscados. Os ativos são somente leitura.
* O único método para recuperar o ativo é arrastá-lo para uma página. Não há suporte a API ou outros métodos para recuperar um ativo para atualizá-lo.
* Se os ativos forem descontinuados do DAM, eles continuarão a ser usados nas [!DNL Sites] páginas.

## Solução de problemas {#troubleshoot}

Para solucionar problemas do cenário de erro comum, siga estas etapas:

* If you cannot search for remote assets from the [!UICONTROL Content Finder], then ensure that the required roles and permissions are in place.
* Um ativo obtido da barragem remota pode não ser publicado em uma página da Web por um ou mais motivos. Ele não existe no servidor remoto, falta de permissões apropriadas para buscá-lo ou falha na rede pode ser o motivo. Verifique se o ativo não foi removido do DAM remoto. Verifique se as permissões apropriadas estão em vigor e se os pré-requisitos foram atendidos. Tente adicionar o ativo novamente à página e publique-o novamente. Verifique a [lista de trabalhos assíncronos](/help/sites-administering/asynchronous-jobs.md) quanto a erros na busca de ativos.
* Se você não conseguir acessar a implantação remota do DAM a partir da [!DNL Sites] implantação local, verifique se os cookies entre sites são permitidos. Se os cookies entre sites estiverem bloqueados, as duas implantações do podem não [!DNL Experience Manager] ser autenticadas. Por exemplo, [!DNL Google Chrome] no modo Incognito pode bloquear cookies de terceiros. Para permitir cookies no [!DNL Chrome] navegador, clique no ícone &#39;olho&#39; na barra de endereços, navegue até Site Not Working > Blocked, selecione o URL do DAM remoto e permita o cookie do token de login. Como alternativa, consulte a ajuda sobre [como ativar cookies](https://support.google.com/chrome/answer/95647)de terceiros.

   ![Erro de cookie no Chrome no modo cognito](assets/chrome-cookies-incognito-dialog.png)
