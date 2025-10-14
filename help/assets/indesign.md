---
title: Integrar [!DNL Assets] com [!DNL InDesign Server]
description: Saiba como integrar [!DNL Adobe Experience Manager Assets] com [!DNL Adobe InDesign Server].
contentOwner: AG
role: Admin
feature: Publishing
exl-id: 5ba020a3-c36c-402b-a11b-d6b0426b03bf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 75c15b0f0e4de2ea7fff339ae46b88ce8f6af83f
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 1%

---

# Integrar [!DNL Adobe Experience Manager Assets] a [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] usa:

* Um proxy para distribuir a carga de determinadas tarefas de processamento. Um proxy é uma instância [!DNL Experience Manager] que se comunica com um trabalhador proxy para realizar uma tarefa específica e outras instâncias [!DNL Experience Manager] para fornecer os resultados.
* Um trabalhador proxy para definir e gerenciar uma tarefa específica.
Elas podem abranger uma grande variedade de tarefas; por exemplo, usar um [!DNL InDesign Server] para processar arquivos.

Para carregar arquivos totalmente para [!DNL Experience Manager Assets] que você criou com [!DNL Adobe InDesign], um proxy é usado. Isso usa um trabalho de proxy para se comunicar com [!DNL Adobe InDesign Server], onde scripts são executados para extrair metadados e gerar várias representações para [!DNL Experience Manager Assets]. O trabalhador proxy habilita a comunicação bidirecional entre as instâncias [!DNL InDesign Server] e [!DNL Experience Manager] em uma configuração de nuvem.

>[!NOTE]
>
>[!DNL Adobe InDesign] é oferecido como duas ofertas separadas. Aplicativo de desktop [Adobe InDesign](https://www.adobe.com/products/indesign.html) usado para criar layouts de página para distribuição digital e impressa. O [Adobe InDesign Server](https://www.adobe.com/products/indesignserver.html) permite criar documentos automatizados de forma programática com base no que você criou com o [!DNL InDesign]. Ela opera como um serviço que oferece uma interface para o mecanismo ExtendScript. Os scripts são gravados em [!DNL ExtendScript], que é semelhante a [!DNL JavaScript].

## Como a extração funciona {#how-the-extraction-works}

O [!DNL Adobe InDesign Server] pode ser integrado ao [!DNL Experience Manager Assets] para que os arquivos INDD criados com o [!DNL InDesign] possam ser carregados, as representações geradas, todas as mídias extraídas (por exemplo, vídeo) e armazenadas como ativos:

>[!NOTE]
>
>As versões anteriores do [!DNL Experience Manager] puderam extrair o XMP e a miniatura. Agora todas as mídias podem ser extraídas.

1. Carregue seu arquivo INDD para [!DNL Experience Manager Assets].
1. Uma estrutura envia scripts de comando para o [!DNL InDesign Server] por meio do SOAP (Simple Object Access Protocol).
Este script de comando irá:

   * Recupere o arquivo INDD.
   * Executar comandos [!DNL InDesign Server]:

      * A estrutura, o texto e quaisquer arquivos de mídia são extraídos.
      * As representações do PDF e do JPG são geradas.
      * As representações HTML e IDML são geradas.

   * Postar os arquivos resultantes de volta para [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML é um formato baseado em XML que renderiza todo o conteúdo do arquivo [!DNL InDesign]. Ele é armazenado como um pacote compactado usando a compactação [ZIP](https://techterms.com/definition/zip). Para obter mais informações, consulte [InDesign Interchange Formats INX e IDML](https://www.peachpit.com/promotions/adobe-creative-cloud-2024-release-books-ebooks-and-142536).

   >[!CAUTION]
   >
   >Se o [!DNL InDesign Server] não estiver instalado ou configurado, você ainda poderá carregar um arquivo INDD para [!DNL Experience Manager]. No entanto, as representações geradas são limitadas a PNG e JPEG. Você não poderá gerar o HTML, `.idml` ou as representações de página.

1. Após a geração da extração e da representação:

   * A estrutura é replicada para um `cq:Page` (tipo de representação).
   * O texto e os arquivos extraídos estão armazenados em [!DNL Experience Manager Assets].
   * Todas as representações são armazenadas em [!DNL Experience Manager Assets], no próprio ativo.

## Integrar o [!DNL InDesign Server] ao Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar o [!DNL InDesign Server] para uso com [!DNL Experience Manager Assets] e após configurar seu proxy, você precisa:

1. [Instalar o InDesign Server](#installing-the-indesign-server).
1. Se necessário, [configure o fluxo de trabalho do Experience Manager Assets](#configuring-the-aem-assets-workflow).
Isso só será necessário se os valores padrão não forem apropriados para a sua instância.
1. Configure um [trabalhador proxy para o InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instalar o [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e iniciar o [!DNL InDesign Server] para uso com [!DNL Experience Manager]:

1. Baixe e instale o [!DNL InDesign Server].

1. Se necessário, você pode personalizar a configuração da sua instância do [!DNL InDesign Server].

1. Na linha de comando, inicie o servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Isso inicia o servidor com o plug-in do SOAP escutando na porta 8080. Todas as mensagens de registro e saída são gravadas diretamente na janela de comando.

   >[!NOTE]
   >
   >Se você quiser salvar as mensagens de saída em um arquivo, use o redirecionamento; por exemplo, no Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurar o fluxo de trabalho [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tem um fluxo de trabalho pré-configurado **[!UICONTROL Ativo de atualização do DAM]**, que tem várias etapas de processo especificamente para [!DNL InDesign]:

* [Extração de mídia &#x200B;](#media-extraction)
* [Extração de página](#page-extraction)

Este fluxo de trabalho é configurado com valores padrão que podem ser adaptados para sua configuração nas várias instâncias do autor (este é um fluxo de trabalho padrão, portanto, mais informações estão disponíveis em [Editando um Fluxo de Trabalho](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se estiver usando os valores padrão (incluindo a porta SOAP), nenhuma configuração será necessária.

Após a configuração, o carregamento de arquivos [!DNL InDesign] no [!DNL Experience Manager Assets] (por qualquer um dos métodos usuais) aciona o fluxo de trabalho para processar o ativo e preparar as várias representações. Teste sua configuração carregando um arquivo INDD no [!DNL Experience Manager Assets] para confirmar que você vê as diferentes representações criadas por IDS no `<*your_asset*>.indd/Renditions`

#### Extração de mídia {#media-extraction}

Esta etapa controla a extração de mídia do arquivo INDD.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de Mídia]**.

![Argumentos de extração de mídia e caminhos de script](assets/media_extraction_arguments_scripts.png)

Argumentos de extração de mídia e caminhos de script

* **Biblioteca ExtendScript**: é uma biblioteca de métodos http get/post simples, exigida pelos outros scripts.

* **Scripts Estendidos**: você pode especificar diferentes combinações de scripts aqui. Se quiser que seus próprios scripts sejam executados em [!DNL InDesign Server], salve os scripts em `/apps/settings/dam/indesign/scripts`.

<!-- TBD: Hiding this link since ADC is not available anymore. 
For information about [!DNL Adobe InDesign] scripts, see [InDesign developer documentation](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).
-->

>[!CAUTION]
>
>Não altere a biblioteca ExtendScript. Essa biblioteca fornece a funcionalidade HTTP necessária para se comunicar com o Sling. Esta configuração especifica a biblioteca a ser enviada para o [!DNL InDesign Server] para ser usada lá.

O script `ThumbnailExport.jsx` executado pela etapa de fluxo de trabalho Extração de mídia gera uma representação de miniatura no formato JPG. Esta representação é usada pela etapa do fluxo de trabalho Processar Miniaturas para gerar as representações estáticas necessárias para [!DNL Experience Manager].

Você pode configurar a etapa do fluxo de trabalho Processar miniaturas para gerar representações estáticas em tamanhos diferentes. Não remova os padrões, pois eles são exigidos pela interface [!DNL Experience Manager Assets]. Por fim, a etapa do fluxo de trabalho Excluir representação da visualização da imagem remove a representação em miniatura do JPG, pois ela não é mais necessária.

#### Extração de página {#page-extraction}

Isso cria uma página [!DNL Experience Manager] a partir dos elementos extraídos. Um manipulador de extração é usado para extrair dados de uma representação (atualmente HTML ou IDML). Esses dados são usados para criar uma página usando o Page Builder.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de página]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Manipulador de extração de página**: na lista pop-up, selecione o manipulador que deseja usar. Um manipulador de extração opera em uma representação específica, escolhida por um `RenditionPicker` relacionado (consulte a API `ExtractionHandler`). Em uma instalação padrão do [!DNL Experience Manager], o seguinte está disponível:
   * Identificador de extração de exportação IDML: opera na representação `IDML` gerada na etapa MediaExtract.

* **Nome da Página**: especifique o nome que você deseja atribuir à página resultante. Se deixado em branco, o nome é &quot;página&quot; (ou um derivado se &quot;página&quot; já existir).

* **Título da Página**: especifique o título que deseja atribuir à página resultante.

* **Caminho raiz da página**: o caminho para o local raiz da página resultante. Se deixado em branco, o nó que contém as representações do ativo será usado.

* **Modelo de página**: o modelo a ser usado ao gerar a página resultante.

* **Design da Página**: o design da página a ser usado ao gerar a página resultante.

### Configurar o trabalho de proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>O trabalhador reside na instância do proxy.

1. No console Ferramentas, expanda **[!UICONTROL Configurações de Cloud Services]** no painel esquerdo. Em seguida, expanda **[!UICONTROL Configuração de proxy de nuvem]**.

1. Clique duas vezes no **[!UICONTROL trabalhador IDS]** para abrir a configuração.

1. Clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo de configuração e definir as configurações necessárias:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool de IDS**
Os pontos de extremidade do SOAP usados para comunicação com o [!DNL InDesign Server]. É possível adicionar, remover e solicitar itens.

1. Clique em OK para salvar.

### Configurar o Day CQ Link Externalizer {#configuring-day-cq-link-externalizer}

Se o [!DNL InDesign Server] e o [!DNL Experience Manager] estiverem em hosts diferentes ou se um ou ambos os aplicativos não estiverem funcionando em portas padrão, configure o [!UICONTROL Day CQ Link Externalizer] para definir o nome do host, a porta e o caminho do conteúdo para o [!DNL InDesign Server].

1. Acesse o Console da Web em `https://[aem_server]:[port]/system/console/configMgr`.
1. Localize o **[!UICONTROL Day CQ Link Externalizer]**. Clique em **[!UICONTROL Editar]** para abrir.
1. As configurações do Externalizador de Link ajudam a criar URLs absolutas para a implantação do [!DNL Experience Manager] e para o [!DNL InDesign Server]. Use o campo **[!UICONTROL Domínios]** para especificar o nome de host para o [!DNL Adobe InDesign Server]. Clique em **Salvar**.

   Em URLs absolutos, use `localhost` como nome de host para sua instância local (autor) e nome de host ou endereço IP para a instância de publicação, como mostrado na ilustração a seguir.

   ![Configuração do externalizador de link](assets/link-externalizer-config.png)

### Habilitar processamento de trabalho paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Agora você pode ativar o processamento paralelo de tarefas para IDS. Determine o número máximo de trabalhos paralelos (`x`) que um [!DNL InDesign Server] pode processar:

* Em uma única máquina com multiprocessador, o número máximo de trabalhos paralelos (`x`) que um [!DNL InDesign Server] pode processar é um a menos do que o número de processadores que executam IDS.
* Quando estiver executando o IDS em vários computadores, você precisará contar o número total de processadores disponíveis (ou seja, em todos os computadores) e depois subtrair o número total de computadores.

Para configurar o número de jobs de IDS paralelos:

1. Abra a guia **[!UICONTROL Configurações]** do Felix Console; por exemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selecione a fila de processamento de IDS em `Apache Sling Job Queue Configuration`.

1. Defina:

   * **Tipo** - `Parallel`
   * **Máximo de Trabalhos Paralelos** - `<*x*>` (conforme calculado acima)

1. Salve essas alterações.
1. Para habilitar o suporte a várias sessões para o Adobe CS6 e posterior, marque a caixa de seleção `enable.multisession.name`, na configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Crie um [pool de `x` trabalhadores de IDS adicionando pontos de extremidade do SOAP à configuração de Trabalho de IDS](#configuring-the-proxy-worker-for-indesign-server).

   Se houver vários computadores executando o [!DNL InDesign Server], adicione pontos de extremidade SOAP (número de processadores por computador -1) para cada computador.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Ao trabalhar com um pool de trabalhadores, é possível ativar uma lista de bloqueios de trabalhadores de IDS.
>
>Para fazer isso, habilite a caixa de seleção **[!UICONTROL enable.retry.name]**, na configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, que permite novas tentativas de trabalho de IDS.
>
>Além disso, na configuração `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, defina um valor positivo para o parâmetro `max.errors.to.blacklist`, que determina o número de tentativas de trabalho antes de barrar uma ID da lista de manipuladores de trabalho.
>
>Por padrão, após o tempo configurável (`retry.interval.to.whitelist.name`) em minutos, o trabalhador de IDS é revalidado. Se o trabalhador for encontrado online, ele será removido da lista de bloqueios.

## Habilitar suporte para [!DNL InDesign Server] 10.0 ou posterior {#enabling-support-for-indesign-server-or-later}

Para o [!DNL InDesign Server] 10.0 ou superior, execute as etapas a seguir para habilitar o suporte a várias sessões.

1. Abra o Configuration Manager da sua instância [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selecione a opção **[!UICONTROL ids.cc.enable]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Para a integração do [!DNL InDesign Server] com o [!DNL Experience Manager Assets], use um processador de vários núcleos porque o recurso de suporte a sessões necessário para a integração não tem suporte em sistemas de núcleo único.

## Configurar credenciais do [!DNL Experience Manager] {#configure-aem-credentials}

Você pode alterar as credenciais de administrador padrão (nome de usuário e senha) para acessar o [!DNL InDesign Server] da sua implantação do [!DNL Experience Manager] sem interromper a integração com o [!DNL InDesign Server].

1. Acesse `/etc/cloudservices/proxy.html`.
1. Na caixa de diálogo, especifique o novo nome de usuário e a senha.
1. Salve as credenciais.

>[!MORELIKETHIS]
>
>* [Sobre o Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)
