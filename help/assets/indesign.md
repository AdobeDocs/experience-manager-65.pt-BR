---
title: Integrar [!DNL Assets] com [!DNL InDesign Server]
description: Saiba como integrar [!DNL Adobe Experience Manager Assets] com [!DNL Adobe InDesign Server].
contentOwner: AG
translation-type: tm+mt
source-git-commit: a31fa2712e541dfdc7a5b08ee9b33782f190f00b
workflow-type: tm+mt
source-wordcount: '1578'
ht-degree: 4%

---


# Integrar [!DNL Adobe Experience Manager Assets] com [!DNL Adobe InDesign Server] {#integrating-aem-assets-with-indesign-server}

[!DNL Adobe Experience Manager Assets] Usa o:

* Um proxy para distribuir a carga de determinadas tarefas de processamento. Um proxy é uma instância [!DNL Experience Manager] que se comunica com um funcionário proxy para atender a uma tarefa específica e outras instâncias [!DNL Experience Manager] para fornecer os resultados.
* Um funcionário proxy para definir e gerenciar uma tarefa específica.
Podem abranger uma grande variedade de tarefas; por exemplo, usar um [!DNL InDesign Server] para processar arquivos.

Para fazer upload completo de arquivos para [!DNL Experience Manager Assets] criados com [!DNL Adobe InDesign], um proxy é usado. Isso usa um funcionário proxy para se comunicar com [!DNL Adobe InDesign Server], onde [scripts](https://www.adobe.com/devnet/indesign/documentation.html#idscripting) são executados para extrair metadados e gerar várias execuções para [!DNL Experience Manager Assets]. O trabalho proxy permite a comunicação bidirecional entre as instâncias [!DNL InDesign Server] e [!DNL Experience Manager] em uma configuração em nuvem.

>[!NOTE]
>
>[!DNL Adobe InDesign] é oferecido como duas ofertas separadas. [Adobe ](https://www.adobe.com/products/indesign.html) InDesign desktop app usado para criar layouts de página para distribuição impressa e digital. [O Adobe InDesign ](https://www.adobe.com/products/indesignserver.html) Server permite que você crie documentos automatizados de forma programática com base no que você criou com  [!DNL InDesign]. Ele opera como um serviço que oferece uma interface para seu mecanismo [ExtendScript](https://www.adobe.com/devnet/scripting.html).Os scripts são escritos em [!DNL ExtendScript], que é semelhante a [!DNL JavaScript]. Para obter informações sobre [!DNL InDesign] scripts, consulte [https://www.adobe.com/devnet/indesign/documentation.html#idscripting](https://www.adobe.com/devnet/indesign/documentation.html#idscripting).

## Como a extração funciona {#how-the-extraction-works}

[!DNL Adobe InDesign Server] pode ser integrado com [!DNL Experience Manager Assets] para que os arquivos INDD criados com [!DNL InDesign] possam ser carregados, as representações geradas, todas as mídias extraídas (por exemplo, vídeo) e armazenados como ativos:

>[!NOTE]
>
>As versões anteriores do [!DNL Experience Manager] podiam extrair XMP e a miniatura, agora todas as mídias podem ser extraídas.

1. Carregue o arquivo INDD para [!DNL Experience Manager Assets].
1. Uma estrutura envia scripts de comando para [!DNL InDesign Server] via SOAP (Simple Object Access Protocol).
Esse script de comando:

   * Recupere o arquivo INDD.
   * Executar comandos [!DNL InDesign Server]:

      * A estrutura, o texto e quaisquer arquivos de mídia são extraídos.
      * Execuções de PDF e JPG são geradas.
      * Execuções HTML e IDML são geradas.
   * Poste os arquivos resultantes de volta para [!DNL Experience Manager Assets].

   >[!NOTE]
   >
   >IDML é um formato baseado em XML que renderiza todo o conteúdo do arquivo [!DNL InDesign]. É armazenado como um pacote compactado usando a compactação [ZIP](https://www.techterms.com/definition/zip). Para obter mais informações, consulte [Formatos de intercâmbio de InDesigns INX e IDML](https://www.peachpit.com/articles/article.aspx?p=1381880&amp;seqNum=8).

   >[!CAUTION]
   >
   >Se [!DNL InDesign Server] não estiver instalado ou configurado, você ainda poderá fazer upload de um arquivo INDD para [!DNL Experience Manager]. No entanto, as renderizações geradas serão limitadas a PNG e JPEG. Não será possível gerar HTML, .idml ou as execuções da página.

1. Após a geração de extração e execução:

   * A estrutura é replicada para `cq:Page` (tipo de representação).
   * O texto e os arquivos extraídos são armazenados em [!DNL Experience Manager Assets].
   * Todas as representações são armazenadas em [!DNL Experience Manager Assets], no próprio ativo.

## Integre o [!DNL InDesign Server] ao Experience Manager {#integrating-the-indesign-server-with-aem}

Para integrar o [!DNL InDesign Server] para uso com [!DNL Experience Manager Assets] e depois de configurar seu proxy, é necessário:

1. [Instale o InDesign Server](#installing-the-indesign-server).
1. Se necessário, [configure o Fluxo de trabalho do Experience Manager Assets](#configuring-the-aem-assets-workflow).
Isso só é necessário se os valores padrão não forem apropriados para sua instância.
1. Configure um [trabalhador proxy para o InDesign Server](#configuring-the-proxy-worker-for-indesign-server).

### Instale o [!DNL InDesign Server] {#installing-the-indesign-server}

Para instalar e start o [!DNL InDesign Server] para uso com [!DNL Experience Manager]:

1. Baixe e instale o [!DNL InDesign Server].

1. Se necessário, você pode personalizar a configuração da sua instância [!DNL InDesign Server].

1. Na linha de comando, start o servidor:

   `<*ids-installation-dir*>/InDesignServer.com -port 8080`

   Isso start o servidor com o plug-in SOAP escutando na porta 8080. Todas as mensagens de registro e saída são gravadas diretamente na janela de comando.

   >[!NOTE]
   >
   >Se desejar salvar as mensagens de saída em um arquivo, use redirecionamento; por exemplo, em Windows:
   >`<ids-installation-dir>/InDesignServer.com -port 8080 > ~/temp/INDD-logfile.txt 2>&1`

### Configurar o fluxo de trabalho [!DNL Experience Manager Assets] {#configuring-the-aem-assets-workflow}

[!DNL Experience Manager Assets] tem um Ativo **[!UICONTROL de atualização]** DAM de fluxo de trabalho pré-configurado, que tem várias etapas de processo especificamente para  [!DNL InDesign]:

* [Extração de mídia](#media-extraction)
* [Extração de página](#page-extraction)

Este fluxo de trabalho é configurado com valores padrão que podem ser adaptados para sua configuração nas várias instâncias do autor (este é um fluxo de trabalho padrão, portanto, mais informações estão disponíveis em [Editando um fluxo de trabalho](/help/sites-developing/workflows-models.md#configuring-a-workflow-step)). Se você estiver usando os valores padrão (incluindo a porta SOAP), nenhuma configuração será necessária.

Após a configuração, carregar arquivos [!DNL InDesign] em [!DNL Experience Manager Assets] (por qualquer um dos métodos habituais) ativa o fluxo de trabalho para processar o ativo e preparar as várias representações. Teste sua configuração carregando um arquivo INDD em [!DNL Experience Manager Assets] para confirmar que você vê as diferentes representações criadas pelo IDS em `<*your_asset*>.indd/Renditions`

#### Extração de mídia {#media-extraction}

Esta etapa controla a extração da mídia a partir do arquivo INDD.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de mídia]**.

![Argumentos de extração de mídia e caminhos de script](assets/media_extraction_arguments_scripts.png)

Argumentos de extração de mídia e caminhos de script

* **Biblioteca** ExtendScript: Esta é uma biblioteca de métodos http get/post simples, exigida pelos outros scripts.

* **Estender scripts**: É possível especificar diferentes combinações de scripts aqui. Se você quiser que seus próprios scripts sejam executados em [!DNL InDesign Server], salve os scripts em `/apps/settings/dam/indesign/scripts`.

Para obter informações sobre [!DNL Adobe InDesign] scripts, consulte [documentação do desenvolvedor do InDesign](https://www.adobe.com/devnet/indesign/documentation.html#idscripting)

>[!CAUTION]
>
>Não altere a biblioteca ExtendScript. Esta biblioteca fornece a funcionalidade HTTP necessária para se comunicar com o Sling. Esta configuração especifica a biblioteca a ser enviada para [!DNL InDesign Server] para uso lá.

O script `ThumbnailExport.jsx` executado pela etapa de fluxo de trabalho da Extração de mídia gera uma execução em miniatura no formato JPG. Essa execução é usada pela etapa de fluxo de trabalho Processar miniaturas para gerar as representações estáticas exigidas por [!DNL Experience Manager].

Você pode configurar a etapa de fluxo de trabalho Processar miniaturas para gerar representações estáticas em tamanhos diferentes. Certifique-se de não remover os padrões, pois eles são exigidos pela interface [!DNL Experience Manager Assets]. Por fim, a etapa do fluxo de trabalho Excluir representação de Pré-visualização de imagem remove a execução de miniatura JPG, pois ela não é mais necessária.

#### Extração da página {#page-extraction}

Isso cria uma página [!DNL Experience Manager] a partir dos elementos extraídos. Um manipulador de extração é usado para extrair dados de uma execução (atualmente HTML ou IDML). Esses dados são usados para criar uma página usando o PageBuilder.

Para personalizar, edite a guia **[!UICONTROL Argumentos]** da etapa **[!UICONTROL Extração de página]**.

![chlimage_1-96](assets/chlimage_1-289.png)

* **Manipulador** de Extração da página: Na lista pop-up, selecione o manipulador que deseja usar. Um manipulador de extração opera em uma representação específica, escolhida por um `RenditionPicker` relacionado (consulte a `ExtractionHandler` API). Em uma instalação padrão [!DNL Experience Manager], o seguinte está disponível:
   * Identificador de Extração de exportação IDML: Opera na execução `IDML` gerada na etapa MediaExtract.

* **Nome** da página: Especifique o nome que deseja atribuir à página resultante. Se deixado em branco, o nome será &quot;page&quot; (ou um derivado se &quot;page&quot; já existir).

* **Título** da página: Especifique o título que deseja atribuir à página resultante.

* **Caminho** raiz da página: O caminho para o local raiz da página resultante. Se deixado em branco, o nó que retém as representações do ativo será usado.

* **Modelo** de página: O modelo a ser usado ao gerar a página resultante.

* **Design** da página: O design da página a ser usado ao gerar a página resultante.

### Configure o trabalho proxy para [!DNL InDesign Server] {#configuring-the-proxy-worker-for-indesign-server}

>[!NOTE]
>
>O trabalhador reside na instância do proxy.

1. No console Ferramentas, expanda **[!UICONTROL Configurações de Cloud Services]** no painel esquerdo. Em seguida, expanda **[!UICONTROL Configuração de Proxy da Nuvem]**.

1. Clique duas vezes no **[!UICONTROL trabalhador IDS]** para abrir a configuração.

1. Clique em **[!UICONTROL Editar]** para abrir a caixa de diálogo de configuração e definir as configurações necessárias:

   ![proxy_idsworkerconfig](assets/proxy_idsworkerconfig.png)

   * **Pool**
de IDSos pontos de extremidade SOAP a serem usados para comunicação com o  [!DNL InDesign Server]. Você pode adicionar, remover e ordenar itens necessários.

1. Clique em OK para salvar.

### Configurar o Externalizador de links do Day CQ {#configuring-day-cq-link-externalizer}

Se [!DNL InDesign Server] e [!DNL Experience Manager] estiverem em hosts diferentes ou um ou ambos os aplicativos não estiverem funcionando em portas padrão, configure [!UICONTROL Externalizador de links do Day CQ] para definir o nome do host, a porta e o caminho do conteúdo para [!DNL InDesign Server].

1. Acesse o console da Web em `https://[aem_server]:[port]/system/console/configMgr`.
1. Localize a configuração **[!UICONTROL Externalizador de links Day CQ]**. Clique em **[!UICONTROL Editar]** para abrir.
1. As configurações do Externalizador de links ajudam a criar URLs absolutos para a implantação [!DNL Experience Manager] e para [!DNL InDesign Server]. Use o campo **[!UICONTROL Domínios]** para especificar o nome do host e o caminho do contexto para [!DNL Adobe InDesign Server]. Clique em **Salvar**.

   ![Configuração do externalizador de links](assets/link-externalizer-config.png)

### Habilitar processamento de trabalho paralelo para [!DNL InDesign Server] {#enabling-parallel-job-processing-for-indesign-server}

Agora você pode ativar o processamento paralelo de tarefas para IDS. Determine o número máximo de trabalhos paralelos (`x`) que um [!DNL InDesign Server] pode processar:

* Em uma única máquina de multiprocessador, o número máximo de trabalhos paralelos (`x`) que um [!DNL InDesign Server] pode processar é um menor que o número de processadores que executam o IDS.
* Ao executar IDS em várias máquinas, é necessário contar o número total de processadores disponíveis (ou seja, em todas as máquinas) e subtrair o número total de máquinas.

Para configurar o número de trabalhos de IDS paralelos:

1. Abra a guia **[!UICONTROL Configurações]** do Console Felix; por exemplo: `https://[aem_server]:[port]/system/console/configMgr`.

1. Selecione a fila de processamento IDS em `Apache Sling Job Queue Configuration`.

1. Ajustar:

   * **Tipo** - `Parallel`
   * **Máximo de trabalhos**  paralelos -  `<*x*>` (conforme calculado acima)

1. Salve essas alterações.
1. Para habilitar o suporte a várias sessões para a Adobe CS6 e posterior, marque a caixa de seleção `enable.multisession.name`, em `com.day.cq.dam.ids.impl.IDSJobProcessor.name` configuração.
1. Crie um pool [de `x` trabalhadores IDS adicionando pontos de extremidade SOAP à configuração do IDS Worker](#configuring-the-proxy-worker-for-indesign-server).

   Se houver várias máquinas executando [!DNL InDesign Server], adicione pontos de extremidade SOAP (número de processadores por máquina -1) para cada máquina.

<!-- 
TBD: Make updates to configurations for allow and block list after product updates are done.
-->

>[!NOTE]
>
>Ao trabalhar com um pool de trabalhadores, você pode habilitar a lista de bloqueios de trabalhadores IDS.
>
>Para fazer isso, ative a caixa de seleção **[!UICONTROL enable.retry.name]**, na configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`, que ativa as tentativas de trabalho do IDS.
>
>Além disso, na configuração `com.day.cq.dam.ids.impl.IDSPoolImpl.name`, defina um valor positivo para o parâmetro `max.errors.to.blacklist`, que determina o número de tentativas de tarefa antes de impedir uma IDS da lista de manipuladores de tarefas.
>
>Por padrão, após o tempo configurável (`retry.interval.to.whitelist.name`) em minutos, o trabalho IDS é revalidado. Se o trabalhador for encontrado on-line, ele será removido da lista de bloqueios.

## Ative o suporte para [!DNL InDesign Server] 10.0 ou posterior {#enabling-support-for-indesign-server-or-later}

Para [!DNL InDesign Server] 10.0 ou superior, execute as seguintes etapas para habilitar o suporte a várias sessões.

1. Abra o Configuration Manager a partir da sua instância [!DNL Experience Manager Assets] `https://[aem_server]:[port]/system/console/configMgr`.
1. Edite a configuração `com.day.cq.dam.ids.impl.IDSJobProcessor.name`.
1. Selecione a opção **[!UICONTROL ids.cc.enable]** e clique em **[!UICONTROL Salvar]**.

>[!NOTE]
>
>Para a integração [!DNL InDesign Server] com [!DNL Experience Manager Assets], use um processador multi-core porque o recurso de suporte de sessão necessário para a integração não é suportado em sistemas de núcleo único.

## Configurar [!DNL Experience Manager] credenciais {#configure-aem-credentials}

Você pode alterar as credenciais padrão do administrador (nome de usuário e senha) para acessar [!DNL InDesign Server] da implantação [!DNL Experience Manager] sem interromper a integração com o [!DNL InDesign Server].

1. Ir para `/etc/cloudservices/proxy.html`.
1. Na caixa de diálogo, especifique o novo nome de usuário e senha.
1. Salve as credenciais.

>[!MORELIKETHIS]
>
>* [Sobre o Adobe InDesign Server](https://www.adobe.com/products/indesignserver/faq.html)

