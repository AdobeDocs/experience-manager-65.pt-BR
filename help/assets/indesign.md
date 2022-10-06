---
title: Integrar [!DNL Assets] com [!DNL InDesign Server]
description: Saiba como integrar [!DNL Adobe Experience Manager Assets] com [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
source-git-commit: 67e145e250bbe386168ab2c0f8967f91aa9d8a36
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 4%

---

# Integrar [!DNL Adobe Experience Manager Assets] com [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] Usa o:

* Um proxy para distribuir a carga de determinadas tarefas de processamento. Um proxy é um [!DNL Experience Manager] instância que se comunica com um trabalhador proxy para realizar uma tarefa específica, e outras [!DNL Experience Manager] para entregar os resultados.
* Um trabalhador proxy para definir e gerenciar uma tarefa específica.
Estas podem abranger uma grande variedade de tarefas; por exemplo, usando um [!DNL InDesign Server] para processar arquivos.

Para fazer o upload completo dos arquivos para o [!DNL Experience Manager Assets] que você criou com [!DNL Adobe InDesign] um proxy é usado. Isso usa um trabalhador proxy para se comunicar com o [!DNL Adobe InDesign Server], onde [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) são executados para extrair metadados e gerar várias renderizações para [!DNL Experience Manager Assets]. O trabalhador proxy permite a comunicação bidirecional entre os [!DNL InDesign Server] e [!DNL Experience Manager] em uma configuração de nuvem.

>[!NOTE]
>
>[!DNL Adobe InDesign] O é oferecido como duas ofertas separadas. [Adobe InDesign](https://www.adobe.com/products/indesign.html) aplicativo de desktop usado para criar layouts de página para distribuição digital e impressa. [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) permite criar documentos automatizados de forma programática com base no que você criou com [!DNL InDesign]. Funciona como um serviço que oferece uma interface para o seu [ExtendScript](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) engine.Os scripts são gravados em [!DNL ExtendScript], que é semelhante a [!DNL JavaScript]. Para obter informações sobre [!DNL InDesign] scripts consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Como a extração funciona {#how-the-extraction-works}

O [!DNL Adobe InDesign Server] pode ser integrado ao [!DNL Experience Manager Assets] para que os arquivos INDD sejam criados com [!DNL InDesign] podem ser carregadas, representações geradas, todas as mídias extraídas (por exemplo, vídeo) e armazenadas como ativos:

>[!NOTE]
>
>Versões anteriores de [!DNL Experience Manager] Conseguimos extrair XMP e a miniatura, agora todas as mídias podem ser extraídas.

1. Faça upload do arquivo INDD para [!DNL Experience Manager Assets].
1. Uma estrutura envia scripts de comando para a [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
Este script de comando irá:

   * Recupere o arquivo INDD.
   * Executar [!DNL InDesign Server] comandos:

      * A estrutura, o texto e os arquivos de mídia são extraídos.
      * As representações de PDF e JPG são geradas.
      * As representações de HTML e IDML são geradas.
   * Poste os arquivos resultantes de volta para [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML é um formato baseado em XML que renderiza todo o conteúdo da variável [!DNL InDesign] arquivo. Ele é armazenado como um pacote compactado usando [ZIP](https://www.techterms.com/definition/zip) compactação. Para obter mais informações, consulte [Formatos de intercâmbio de InDesigns INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se a variável [!DNL InDesign Server] não estiver instalado ou não estiver configurado, você ainda poderá fazer upload de um arquivo INDD no [!DNL Experience Manager]. No entanto, as representações geradas serão limitadas a PNG e JPEG. Você não poderá gerar HTML, .idml ou as representações de página.

1. Após a geração da extração e da representação:

   * A estrutura é replicada para um `cq:Page` (tipo de representação).
   * O texto e os arquivos extraídos são armazenados em [!DNL Experience Manager Assets].
   * Todas as representações são armazenadas em [!DNL Experience Manager Assets], no próprio ativo.

## Integre o [!DNL InDesign Server] com Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar o [!DNL InDesign Server] para uso com [!DNL Experience Manager Assets] e após configurar seu proxy, é necessário:

1. [Instalar o InDesign Server](#installing-the-indesign-server).
1. Se necessário, [configurar o fluxo de trabalho do Experience Manager Assets](#configuring-the-aem-assets-workflow).
Isso só será necessário se os valores padrão não forem apropriados para sua instância.
1. Configure um [trabalhador proxy para o InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instale o [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar o [!DNL InDesign Server] para uso com [!DNL Experience Manager]:

1. Baixe e instale o [!DNL InDesign Server].

1. Se necessário, você pode personalizar a configuração de seu [!DNL InDesign Server] instância.

1. Na linha de comando, inicie o servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Isso iniciará o servidor com o plug-in SOAP escutando na porta 8080. Todas as mensagens de log e a saída são gravadas diretamente na janela de comando.

   >[!NOTE]
   >
   >Se desejar salvar as mensagens de saída em um arquivo, use redirecionamento; por exemplo, em Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configure o [!DNL Experience Manager Assets] workflow {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tem um fluxo de trabalho pré-configurado **[!UICONTROL Ativo de atualização DAM]**, que possui várias etapas do processo especificamente para [!DNL InDesign]:

* [Extração de mídia](#media-extraction)
* [Extração de página](#page-extraction)

Esse workflow é configurado com valores padrão que podem ser adaptados para sua configuração nas várias instâncias do autor (esse é um workflow padrão, portanto, mais informações estão disponíveis em [Editar um fluxo de trabalho](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se você estiver usando os valores padrão (incluindo a porta SOAP), nenhuma configuração será necessária.

Após a configuração, faça o upload [!DNL InDesign] arquivos em [!DNL Experience Manager Assets] (de acordo com qualquer um dos métodos habituais) aciona o fluxo de trabalho para processar o ativo e preparar as várias representações. Teste sua configuração carregando um arquivo INDD no [!DNL Experience Manager Assets] para confirmar que você vê as diferentes representações criadas pelo IDS em `<*your_asset*>.indd/Renditions`

#### Extração de mídia {#media-extraction}

Esta etapa controla a extração de mídia do arquivo INDD.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de mídia]**.

![Argumentos de extração de mídia e caminhos de script](assets/media_extraction_arguments_scripts.png)

Argumentos de extração de mídia e caminhos de script

* **Biblioteca da ExtendScript**: Esta é uma biblioteca de método http get/post simples, exigida pelos outros scripts.

* **Estender scripts**: Você pode especificar combinações de script diferentes aqui. Se você quiser que seus próprios scripts sejam executados na variável [!DNL InDesign Server], salve os scripts em `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Não altere a biblioteca ExtendScript. Esta biblioteca fornece a funcionalidade HTTP necessária para se comunicar com o Sling. Essa configuração especifica a biblioteca a ser enviada para o [!DNL InDesign Server] para uso lá.

O `ThumbnailExport.jsx` O script executado pela etapa do fluxo de trabalho Extração de mídia gera uma renderização de miniatura no formato JPG. Essa representação é usada pela etapa do fluxo de trabalho Processar miniaturas para gerar as representações estáticas necessárias para [!DNL Experience Manager].

Você pode configurar a etapa do fluxo de trabalho Processar miniaturas para gerar representações estáticas em tamanhos diferentes. Certifique-se de não remover os padrões, pois eles são exigidos pela variável [!DNL Experience Manager Assets] interface. Finalmente, a etapa de fluxo de trabalho Excluir representação da visualização de imagem remove a representação de miniatura do JPG, pois não é mais necessária.

#### Extração de página {#page-extraction}

Isso cria um [!DNL Experience Manager] dos elementos extraídos. Um manipulador de extração é usado para extrair dados de uma representação (atualmente HTML ou IDML). Esses dados são usados para criar uma página usando o PageBuilder.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de página]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Manipulador de extração de página**: Na lista pop-up, selecione o manipulador que deseja usar. Um manipulador de extração opera em uma representação específica, escolhida por um `RenditionPicker` relacionado (consulte a `ExtractionHandler` API). Em um [!DNL Experience Manager] instalação, o seguinte está disponível:
   * Identificador de Extração de Exportação IDML: Opera no `IDML` representação gerada na etapa MediaExtract .

* **Nome da página**: Especifique o nome que deseja atribuir à página resultante. Se deixado em branco, o nome será &quot;página&quot; (ou um derivado se &quot;página&quot; já existir).

* **Título da página**: Especifique o título que deseja atribuir à página resultante.

* **Caminho raiz da página**: O caminho para o local raiz da página resultante. Se deixado em branco, o nó que mantém as representações do ativo será usado.

* **Modelo de página**: O modelo a ser usado ao gerar a página resultante.

* **Design da página**: O design da página a ser usado ao gerar a página resultante.

### Configure o trabalhador proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>O trabalhador reside na instância do proxy.

1. No console Ferramentas , expanda **[!UICONTROL Configurações do Cloud Services]** no painel esquerdo. Em seguida, expanda **[!UICONTROL Configuração do Cloud Proxy]**.

1. Clique duas vezes no **[!UICONTROL trabalhador IDS]** para abrir a configuração.

1. Clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo de configuração e definir as configurações necessárias:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool IDS**
Os endpoints SOAP a serem usados para comunicação com a [!DNL InDesign Server]. Você pode adicionar, remover e ordenar itens necessários.

1. Clique em OK para salvar.

### Configurar o Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se a variável [!DNL InDesign Server] e [!DNL Experience Manager] estão em hosts diferentes ou um ou ambos os aplicativos não estão funcionando em portas padrão, em seguida, configuram [!UICONTROL Externalizador de links CQ do dia] para definir o nome do host, a porta e o caminho do conteúdo para o [!DNL InDesign Server].

1. Acesse o Console da Web em `https://[aem_server]:[port]/system/console/configMgr`.
1. Localize a configuração **[!UICONTROL Externalizador de links CQ do dia]**. Clique em **[!UICONTROL Editar]** para abrir.
1. As configurações do Link Externalizer ajudam a criar URLs absolutos para o [!DNL Experience Manager] e para a [!DNL InDesign Server]. Use **[!UICONTROL Domínios]** para especificar o nome do host para a variável [!DNL Adobe InDesign Server]. Clique em **Salvar**.

   Em URLs absolutos, use `localhost` como o nome do host para sua instância local (autor) e o nome do host ou endereço IP para a instância de publicação, conforme mostrado na ilustração a seguir.

   ![Configuração do externalizador de links](assets/link-externalizer-config.png)

### Habilitar processamento de trabalho paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Agora é possível habilitar o processamento paralelo de tarefas para IDS. Determine o número máximo de trabalhos paralelos (`x`) [!DNL InDesign Server] pode processar:

* Em uma única máquina multiprocessador, o número máximo de trabalhos paralelos (`x`) que [!DNL InDesign Server] O processo pode ser um menor que o número de processadores executando IDS.
* Ao executar IDS em várias máquinas, é necessário contar o número total de processadores disponíveis (ou seja, em todas as máquinas) e subtrair o número total de máquinas.

Para configurar o número de trabalhos paralelos do IDS:

1. Abra o **[!UICONTROL Configurações]** guia do Felix Console; por exemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selecione a fila de processamento do IDS em `Apache Sling Job Queue Configuration`.

1. Ajustar:

   * **Tipo** - `Parallel`
   * **Máximo de trabalhos paralelos** - `<*x*>` (conforme calculado acima)

1. Salve essas alterações.
1. Para ativar o suporte a várias sessões para o Adobe CS6 e posterior, marque `enable.multisession.name` caixa de seleção, em `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuração.
1. Crie um [conjunto de `x` Trabalhadores IDS adicionando pontos de extremidade SOAP à configuração do trabalhador IDS](#configuring-the-proxy-worker-for-indesign-server).

   Se houver várias máquinas em execução [!DNL InDesign Server], adicione pontos de extremidade SOAP (número de processadores por máquina -1) para cada máquina.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Ao trabalhar com um pool de trabalhadores, você pode habilitar a lista de bloqueios de trabalhadores IDS.
>
>Para fazer isso, ative a **[!UICONTROL enable.retry.name]** caixa de seleção, em `com.day.cq.dam.ids.impl.IDSJobProcessor.name` , que permite novas tentativas de trabalho do IDS.
>
>Além disso, em `com.day.cq.dam.ids.impl.IDSPoolImpl.name` , defina um valor positivo para `max.errors.to.blacklist` que determina o número de novas tentativas de trabalho antes de barrar uma IDS da lista de manipuladores de trabalho.
>
>Por padrão, depois do valor configurável (`retry.interval.to.whitelist.name`) em minutos, o trabalhador IDS é revalidado. Se o trabalhador for encontrado online, ele será removido da lista de bloqueios.

## Ativar suporte para [!DNL InDesign Server] 10.0 ou posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 ou superior, execute as etapas a seguir para ativar o suporte a várias sessões.

1. Abra o Gerenciador de configuração do [!DNL Experience Manager Assets] instância `https://[aem_server]:[port]/system/console/configMgr`.
1. Editar a configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selecione o **[!UICONTROL ids.cc.enable]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Para [!DNL InDesign Server] integração com [!DNL Experience Manager Assets], use um processador multi-núcleo porque o recurso de suporte de sessão necessário para a integração não é suportado em sistemas de núcleo único.

## Configurar [!DNL Experience Manager] credenciais {#configure-aem-credentials}

Você pode alterar as credenciais de administrador padrão (nome de usuário e senha) para acessar o [!DNL InDesign Server] do [!DNL Experience Manager] implantação sem interromper a integração com o [!DNL InDesign Server].

1. Ir para `/etc/cloudservices/proxy.html`.
1. Na caixa de diálogo, especifique o novo nome de usuário e senha.
1. Salve as credenciais.

>[!MORELIKETHIS]
>
>* [Sobre o Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

