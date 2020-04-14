---
title: Use o Connected Assets para compartilhar ativos do DAM no fluxo de trabalho de criação do Adobe Experience Manager Sites
description: Use os ativos disponíveis em uma implantação remota do Adobe Experience Manager Assets ao criar suas páginas da Web em outra implantação do Experience Manager Site.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 04fef21d6027dcfcb6a67a1121e0d1570926db41

---


# Use o Connected Assets para compartilhar ativos do DAM no AEM Sites {#use-connected-assets-to-share-dam-assets-in-aem-sites}

Em grandes empresa, a infraestrutura necessária para criar sites pode ser distribuída. Às vezes, os recursos de criação de sites e os ativos digitais usados para criar esses sites podem residir em diferentes implantações. Algumas razões podem ser distribuídas geograficamente por implantações existentes que são necessárias para trabalhar em paralelo ou em aquisições que levam a uma infraestrutura heterogênea que a empresa pai deseja usar em conjunto.

O AEM Sites oferece recursos para criar páginas da Web e o AEM Assets é o sistema de gerenciamento de ativos digitais (DAM) que fornece os ativos necessários para sites. O AEM agora dá suporte ao caso de uso acima integrando o AEM Sites e o AEM Assets.

## Visão geral do Connected Assets {#overview-of-connected-assets}

Ao editar páginas no Editor de páginas, os autores podem pesquisar, procurar e incorporar facilmente ativos de uma implantação diferente do AEM Assets. Para fazer um administrador do AEM, faça uma integração única de uma implantação local do AEM Sites com uma implantação diferente (remota) do AEM Assets.

Para os autores do Sites, os ativos remotos estão disponíveis como ativos locais somente leitura. A funcionalidade suporta pesquisa e uso ininterruptos de alguns ativos remotos de cada vez. Para disponibilizar muitos ativos remotos em uma única implantação local, considere migrar os ativos em massa. Consulte [guia de migração de Ativos](/help/assets/assets-migration-guide.md).

### Pré-requisitos e implantações compatíveis {#prerequisites}

Antes de usar ou configurar esse recurso, verifique o seguinte:

* Os usuários fazem parte dos grupos de usuários apropriados em cada implantação.
* Para os tipos de implantação do Adobe Experience Manager, um dos critérios compatíveis é atendido. Os ativos AEM 6.5 funcionam com o AEM como um serviço em nuvem. Para obter mais informações, consulte Funcionalidade de ativos [conectados no AEM como um serviço](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/assets/admin/use-assets-across-connected-assets-instances.html)em nuvem.

   |  | AEM Sites as a Cloud Service | AEM 6.5 Sites no AMS | AEM 6.5 Sites no local |
   |---|---|---|---|
   | **AEM Assets as a Cloud Service** | Compatível | Compatível | Compatível |
   | **AEM 6.5 Assets no AMS** | Compatível | Compatível | Compatível |
   | **AEM 6.5 Assets no local** | Incompatível | Incompatível | Incompatível |

### Formatos de arquivo não suportados {#mimetypes}

Os autores podem pesquisar imagens e os seguintes tipos de documentos no Localizador de conteúdo e usar os ativos pesquisados no Editor de páginas. Os documentos podem ser adicionados ao componente `Download` e as imagens podem ser adicionadas ao componente `Image`. Os autores também podem adicionar os ativos remotos em qualquer componente personalizado do AEM, que estende os componentes padrão `Download` ou `Image`. A lista de formatos suportados são:

* **Formatos** de imagem: Os formatos de imagem suportados pelo componente [](https://docs.adobe.com/content/help/pt/experience-manager-core-components/using/components/image.html) Imagem são suportados pelos Ativos conectados. As imagens da mídia dinâmica não são compatíveis.
* **Formatos de documento**: consulte [Formatos de documento compatíveis com os Connected Assets](assets-formats.md#supported-document-formats).

### Usuários e grupos envolvidos {#users-and-groups-involved}

As várias funções envolvidas para configurar e usar o recurso e seus grupos de usuários correspondentes são descritas abaixo. O escopo local é usado para o caso de uso em que uma página da Web é criada por um autor. O escopo remoto é usado para a implantação do DAM que hospeda os ativos necessários. O autor do Sites busca esses ativos remotos.

| Função | Escopo | Grupo de usuários | Nome do usuário na apresentação | Requisito |
|---|---|---|---|---|
| Administrador do AEM Sites | Local | Administrador do AEM | `admin` | Configure o AEM, configure a integração com a implantação remota do Assets. |
| Usuário do DAM | Local | Autor | `ksaner` | Usado para exibir e duplicar os ativos pesquisados em `/content/DAM/connectedassets/`. |
| Autor do AEM Sites | Local | Autor (com acesso de leitura no DAM remoto e acesso de autor no Sites local) | `ksaner` | Os usuários finais são autores do Sites que usam essa integração para melhorar sua velocidade de conteúdo. Os autores pesquisam e procuram ativos no DAM remoto usando o Localizador de conteúdo e usando as imagens necessárias nas páginas da Web locais. As credenciais do usuário do DAM `ksaner` são usadas. |
| Administrador do AEM Assets | Remoto | Administrador do AEM | `admin` no AEM remoto | Configure o CORS (Cross-Origin Resource Sharing). |
| Usuário do DAM | Remoto | Autor | `ksaner` no AEM remoto | Função de autor na implantação remota do AEM. Pesquise e procure ativos no Connected Assets usando o Localizador de conteúdo. |
| Distribuidor do DAM (usuário técnico) | Remoto | construtores de pacotes e autores de sites | `ksaner` no AEM remoto | Este usuário presente na implantação remota é usado pelo servidor local do AEM (não pela função de autor do Site) para buscar os ativos remotos, em nome do autor do Sites. Essa função não é igual às duas funções `ksaner` acima e pertence a um grupo de usuários diferente. |

## Configure uma conexão entre implantações do Sites e do Assets {#configure-a-connection-between-sites-and-assets-deployments}

Um administrador do AEM pode criar essa integração. Depois de criadas, as permissões necessárias para usá-la são estabelecidas por meio dos grupos de usuários definidos na implantação do Sites e na implantação do DAM.

Para configurar a conectividade do Connected Assets e dos Sites local, siga estas etapas.

1. Acesse uma implantação existente do AEM Sites ou crie uma implantação usando o seguinte comando:

   1. Na pasta do arquivo JAR, execute o seguinte comando em um terminal para criar cada servidor do AEM.
      `java -XX:MaxPermSize=768m -Xmx4096m -jar <quickstart jar filepath> -r samplecontent -p 4502 -nofork -gui -nointeractive &`

   1. Após alguns minutos, o servidor do AEM será iniciado com êxito. Considere essa implantação do AEM Sites como a máquina local da criação de página da Web, digamos no `https://[local_sites]:4502`.

1. Verifique se os usuários e as funções com escopo local existem na implantação do AEM Sites e na implantação do AEM Assets no AMS. Crie um usuário técnico na implantação do Assets e adicione ao grupo de usuários mencionado nos [usuários e grupos envolvidos](/help/assets/use-assets-across-connected-assets-instances.md#users-and-groups-involved).

1. Acesse a implantação local do AEM Sites em `https://[local_sites]:4502`. Clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Configuração do Connected Assets]** e forneça os seguintes valores:

   1. O local do AEM Assets é `https://[assets_servername_ams]:[port]`.
   1. Credenciais de um distribuidor do DAM (usuário técnico).
   1. No campo **[!UICONTROL Ponto de montagem]**, insira o caminho do AEM local onde o AEM busca os ativos. Por exemplo, pasta `remoteassets`.
   1. Ajuste os valores do **[!UICONTROL Limite de otimização da transferência do binário original]**, dependendo da sua rede. Uma representação de ativos maior que esse limite é transferida de forma assíncrona.
   1. Selecione **[!UICONTROL Datastore compartilhado com o Connected Assets]**, se você usar um datastore para armazenar seus ativos e se o Datastore for o armazenamento comum entre as duas implantações do AEM. Nesse caso, o limite não importa, pois os binários de ativos reais residem no datastore e não são transferidos.
      ![Uma configuração normal do Connected Assets](assets/connected-assets-typical-config.png)
   *Figura: uma configuração normal do Connected Assets*

1. Como os ativos já são processados e as representações são buscadas, desative os inicializadores do fluxo de trabalho. Ajuste as configurações do iniciador na implantação local (AEM Sites) para excluir a pasta `connectedassets`, em que os ativos remotos são buscados.

   1. Na implantação do AEM Sites, clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Iniciadores]**.

   1. Procure Iniciadores com fluxos de trabalho como **[!UICONTROL Ativo de atualização do DAM]** e **[!UICONTROL Writeback de metadados do DAM]**.

   1. Selecione o iniciador do fluxo de trabalho e clique em **[!UICONTROL Propriedades]** na barra de ações.

   1. No assistente Propriedades, altere os campos **[!UICONTROL Caminho]** como os seguintes mapeamentos para atualizar as expressões regulares para excluir os **[!UICONTROL ativos conectados]** do ponto de montagem.
   | Antes | Depois |
   |---|---|
   | /content/dam(/((?!/subassets).)*/)renditions/original | /content/dam(/((?!/subassets)(?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*/)renditions/original | /content/dam(/((?!connectedassets).)*/)renditions/original |
   | /content/dam(/.*)/jcr:content/metadata | /content/dam(/((?!connectedassets).)*/)jcr:content/metadata |

   >[!NOTE]
   >
   >Todas as representações disponíveis na implantação remota do AEM são buscadas, quando os autores buscam um ativo. Se você quiser criar mais representações de um ativo buscado, pule esta etapa de configuração. The [!UICONTROL DAM Update Asset] workflow gets triggered and creates more renditions. These renditions are available only on the local [!DNL Sites] deployment and not on the remote DAM deployment.

1. Adicione a instância do AEM Sites como uma das **[!UICONTROL Origens permitidas]** na configuração remota do CORS do AEM Assets.

   1. Faça logon usando as credenciais de administrador. Procure Entre origens. Acesse **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.

   1. Para criar uma configuração do CORS para a instância do AEM Sites, clique no ícone ![aem_assets_add_icon](assets/aem_assets_add_icon.png) ao lado da **[!UICONTROL Política de compartilhamento de recursos entre origens do Adobe Granite]**.

   1. No campo **[!UICONTROL Origens permitidas]**, insira o URL do Sites local, ou seja, `https://[local_sites]:[port]`. Salve a configuração.

## Use ativos remotos {#use-remote-assets}

Os autores do site usam o Localizador de conteúdo para se conectar à instância do DAM. Os autores podem procurar, buscar e arrastar os ativos remotos em um componente. Para autenticar no DAM remoto, mantenha acessíveis as credenciais do usuário do DAM fornecidas pelo administrador.

Os autores podem usar os ativos disponíveis nas instâncias do DAM local e do DAM remoto, em uma única página da Web. Use o Localizador de conteúdo para alternar entre a pesquisa no DAM local ou a pesquisa no DAM remoto.

Somente as tags de ativos remotos que têm uma tag correspondente exata junto com a mesma hierarquia de taxonomia, estão disponíveis na instância de Sites local. Quaisquer outras tags são descartadas. Os autores podem pesquisar ativos remotos usando todas as tags presentes na implantação remota do AEM, já que o AEM oferece uma pesquisa em texto completo.

### Apresentação do uso {#walk-through-of-usage}

Use a configuração acima para ter uma experiência de criação a fim de entender a funcionalidade. Use documentos ou imagens de sua escolha na implantação remota do DAM.

1. Navegue até a interface do usuário do Assets na implantação remota, acessando **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]** na área de trabalho do AEM. Como alternativa, acesse `https://[assets_servername_ams]:[port]/assets.html/content/dam` em um navegador. Carregue os ativos de sua escolha.
1. Na instância do Sites, no ativador de perfil no canto superior direito, clique em **[!UICONTROL Representar como]**. Forneça `ksaner` como nome de usuário, selecione a opção fornecida e clique em **[!UICONTROL OK]**.
1. Abra uma página do site We.Retail em **[!UICONTROL Sites]** > **[!UICONTROL We.Retail]** > **[!UICONTROL br]** > **[!UICONTROL pt]**. Edite a página. Como alternativa, acesse `https://[aem_server]:[port]/editor.html/content/we-retail/us/en/men.html` em um navegador para editar uma página.

   Clique em **[!UICONTROL Alternar painel lateral]** no canto superior esquerdo da página.

1. Abra a guia Ativos e clique em **[!UICONTROL Fazer logon no Connected Assets]**.
1. Forneça as credenciais - `ksaner` como nome de usuário e `password` como senha. Esse usuário tem permissões de criação em ambas as implantações do AEM.
1. Procure o ativo que você adicionou ao DAM. Os ativos remotos são exibidos no painel esquerdo. Filtre por imagens ou documentos e filtre também por tipos de documentos compatíveis. Arraste as imagens em um componente `Image` e os documentos em um componente `Download`.

   Os ativos buscados são somente leitura na implantação local do AEM Sites. Você ainda pode usar as opções fornecidas pelos componentes do AEM Sites para editar o ativo buscado. A edição por componentes não é destrutiva.

   ![Opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto](assets/filetypes_filter_connected_assets.png)

   *Figura: opções para filtrar tipos de documentos e imagens ao pesquisar ativos no DAM remoto*

1. Um autor do site será notificado se ocorrer uma busca assíncrona de ativo e uma falha na tarefa de busca. Durante a criação ou até mesmo após a criação, os autores podem ver informações detalhadas sobre as tarefas de busca e erros na interface do usuário de [trabalhos assíncronos](/help/assets/asynchronous-jobs.md).

   ![Notificação sobre a busca assíncrona de ativos que ocorre em segundo plano.](assets/assets_async_transfer_fails.png)

   *Figura: notificação sobre a busca assíncrona de ativos que ocorre em segundo plano*

1. Ao publicar uma página, o AEM exibe uma lista completa dos ativos usados na página. Verifique se os ativos remotos foram buscados com êxito no momento da publicação. Para verificar o status de cada ativo buscado, consulte a interface do usuário de [trabalhos assíncronos](/help/assets/asynchronous-jobs.md).

   >[!NOTE]
   >
   >Mesmo se um ou mais ativos remotos não forem buscados, a página será publicada. O componente que usa o ativo remoto é publicado vazio. A área de notificação do AEM exibe notificações de erros que são mostrados na página de trabalhos assíncronos.

>[!CAUTION]
>
>Uma vez usados em uma página da Web, os ativos remotos buscados podem ser pesquisados e usados por qualquer pessoa com permissões para acessar a pasta local em que os ativos buscados são armazenados (`connectedassets` na apresentação acima). Os ativos também podem ser pesquisados e visualizados no repositório local por meio do [!UICONTROL Localizador de conteúdo].

Os ativos buscados podem ser usados como qualquer outro ativo local, exceto se os metadados associados não puderem ser editados.

## Limitações       {#limitations}

**Permissões e gerenciamento de ativos**

* Os ativos locais não são sincronizados com os ativos originais na implantação remota. As edições, exclusões ou revogação de permissões na implantação do DAM não são propagadas para a jusante.
* Os ativos locais são cópias somente leitura. Os componentes do AEM fazem edições não destrutivas nos ativos. Nenhuma outra edição é permitida.
* Os ativos buscados localmente estão disponíveis apenas para fins de criação. Os fluxos de trabalho de atualização de ativos não podem ser aplicados e os metadados não podem ser editados.
* Somente as imagens e os formatos de documento listados são compatíveis. Os ativos de mídia dinâmica, Fragmentos de conteúdo e Fragmentos de experiência não são compatíveis.
* Os esquemas de metadados não são buscados.
* Todos os Autores do Sites têm permissões de leitura nas cópias buscadas, mesmo que não tenham acesso à implantação remota do DAM.
* Não há suporte de API para personalizar a integração.
* A funcionalidade suporta pesquisa e uso ininterruptos de ativos remotos. Para disponibilizar muitos ativos remotos em uma única implantação local, considere migrar os ativos. Consulte [guia de migração de Ativos](assets-migration-guide.md).
* Não é possível usar um ativo remoto como uma miniatura de página na interface do usuário Propriedades [!UICONTROL da] página. Você pode definir uma miniatura de uma página da Web na interface do usuário Propriedades [!UICONTROL da] página na [!UICONTROL miniatura] clicando em [!UICONTROL Selecionar imagem].

**Configuração e licenciamento**

* A implantação do AEM Assets no AMS é compatível.
* O AEM Sites pode se conectar a um único repositório do AEM Assets de cada vez.
* Uma licença do AEM Assets que funciona como repositório remoto.
* Uma ou mais licenças do AEM Sites que funcionam como implantação de criação local.

**Uso**

* A única funcionalidade compatível é pesquisar ativos remotos e arrastar os ativos remotos na página local para criar conteúdo.
* A operação de busca expira após 5 segundos. Os autores podem ter problemas ao buscar ativos, digamos se houver problemas de rede. Os autores podem tentar novamente, arrastando o ativo remoto do [!UICONTROL Localizador de conteúdo] para o [!UICONTROL Editor de páginas].
* Edições simples que não são destrutivas e a edição compatível por meio do componente `Image` do AEM podem ser realizadas nos ativos buscados. Os ativos são somente leitura.

## Solução de problemas {#troubleshoot}

Siga estas etapas para solucionar problemas de cenários de erro comuns:

* Se não for possível pesquisar ativos remotos no Localizador de conteúdo, verifique novamente se as funções e permissões necessárias estão em vigor.
* Um ativo buscado em um DAM remoto pode não ser publicado em uma página da Web pelos motivos a seguir: ele não existe no local remoto, falta de permissões adequadas para buscá-lo e falha de rede. Verifique se o ativo não foi removido do DAM remoto ou se as permissões não foram alteradas. Verifique se os requisitos necessários foram atendidos. Tente adicionar o ativo novamente à página e publique-o de novo. Verifique a [lista de trabalhos assíncronos](/help/assets/asynchronous-jobs.md) quanto a erros na busca de ativos.
