---
title: Relatórios sobre uso e compartilhamento de ativos
description: Relatórios sobre seus ativos em [!DNL Adobe Experience Manager Assets] que ajudam você a entender o uso, a atividade e o compartilhamento de seus ativos digitais.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 6016cefa9456d8f142347ff197b61b1614d55ab9
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 9%

---


# Relatórios de ativos {#asset-reports}

O relatórios de ativos permite que você avalie a utilidade de sua implantação [!DNL Adobe Experience Manager Assets]. Com [!DNL Assets], você pode gerar vários relatórios para seus ativos digitais. Os relatórios fornecem informações úteis sobre o uso do sistema, como os usuários interagem com ativos e quais ativos são baixados e compartilhados.

Use as informações nos relatórios para derivar as principais métricas de sucesso para medir a adoção de [!DNL Assets] na sua empresa e pelos clientes.

A estrutura de relatórios [!DNL Assets] usa [!DNL Sling] trabalhos para processar de forma assíncrona solicitações de relatório de maneira ordenada. É escalável para repositórios grandes. O processamento assíncrono de relatórios aumenta a eficiência e a velocidade com que os relatórios são gerados.

A interface de gerenciamento de relatórios é intuitiva e inclui opções e controles refinados para acessar relatórios arquivados e status de execução de relatórios de visualização (sucesso, falha e enfileirados).

Quando um relatório é gerado, você é notificado por meio de um email (opcional) e de uma notificação de caixa de entrada. Você pode visualização, baixar ou excluir um relatório da página de listagem do relatório, onde todos os relatórios gerados anteriormente são exibidos.

## Pré-requisitos {#prerequisite-for-reporting}

Para gerar relatórios, faça o seguinte:

* Ative o serviço [!UICONTROL Gravador de Evento do Day CQ DAM] de **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
* Selecione as atividades ou eventos em que deseja relatórios. Por exemplo, para gerar um relatório sobre ativos baixados, selecione [!UICONTROL Ativo baixado (DOWNLOADED)].

![Ativar relatórios de ativos no Console da Web](assets/reports-config-day-cq-dam-event-recorder.png)

## Gerar relatórios {#generate-reports}

[!DNL Experience Manager Assets] gera os seguintes relatórios padrão para você:

* Imagem
* Download
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] Publicar
* Uso do disco
* Arquivos
* Compartilhamento de link

[!DNL Adobe Experience Manager] os administradores podem facilmente gerar e personalizar esses relatórios para sua implementação. Um administrador pode seguir estas etapas para gerar um relatório:

1. Na interface [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.

   ![Página Ferramentas para navegar no relatório de ativos](assets/AssetsReportNavigation.png)

1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Criar relatório]**, escolha o relatório que deseja criar e clique em **[!UICONTROL Próximo]**.

   ![Selecionar tipo de relatório](assets/choose_report.png)

   >[!NOTE]
   >
   >Por padrão, os Fragmentos de conteúdo e compartilhamentos de link estão incluídos no relatório de Ativo [!UICONTROL Download]. Selecione a opção apropriada para criar um relatório de compartilhamentos de link ou para excluir Fragmentos de conteúdo do relatório de download.

   >[!NOTE]
   >
   >O relatório [!UICONTROL Download] exibe detalhes somente dos ativos que são baixados após a seleção individual ou baixados por meio da Ação rápida. No entanto, não inclui os detalhes dos ativos que estão dentro de uma pasta baixada.

1. Configure detalhes do relatório, como título, descrição, miniatura e caminho da pasta no repositório CRX onde o relatório é armazenado. Por padrão, o caminho da pasta é `/content/dam`. Você pode especificar um caminho diferente.

   ![Página para adicionar detalhes do relatório](assets/report_configuration.png)

   Escolha o intervalo de datas para seu relatório.

   Você pode optar por gerar o relatório agora ou em uma data e hora futuras.

   >[!NOTE]
   >
   >Se você optar por agendar o relatório posteriormente, especifique a data e a hora nos campos Data e Hora. Se você não especificar nenhum valor, o mecanismo de relatório o tratará como um relatório que deve ser gerado instantaneamente.

   Os campos de configuração podem diferir com base no tipo de relatório que você cria. Por exemplo, o relatório **[!UICONTROL Uso do disco]** fornece opções para incluir representações de ativos ao calcular o espaço em disco usado pelos ativos. Você pode optar por incluir ou excluir ativos em subpastas para o cálculo de uso do disco.

   >[!NOTE]
   >
   >O relatório **[!UICONTROL Uso de disco]** não inclui campos de intervalo de datas porque indica apenas o uso atual do espaço em disco.

   ![Página Detalhes do relatório Uso de Disco](assets/disk_usage_configuration.png)

   Ao criar o relatório **[!UICONTROL Arquivos]**, você pode incluir/excluir subpastas. No entanto, não é possível incluir representações de ativos para este relatório.

   ![Página de detalhes do relatório Arquivos](assets/files_report.png)

   O relatório **[!UICONTROL Compartilhamento de links]** exibe URLs de ativos que são compartilhados com usuários externos a partir do [!DNL Assets]. Inclui IDs de email do usuário que compartilhou os ativos, IDs de email de usuários com os quais os ativos são compartilhados, data de compartilhamento e data de expiração do link. As colunas não são personalizáveis.

   O relatório **[!UICONTROL Compartilhamento de links]** não inclui opções para subpastas e execuções porque apenas publica os URLs compartilhados que aparecem em `/var/dam/share`.

   ![Página de detalhes do relatório Compartilhamento de links](assets/link_share.png)

1. Clique em **[!UICONTROL Próximo]** na barra de ferramentas.

1. Na página **[!UICONTROL Configurar colunas]**, algumas colunas são selecionadas para aparecerem no relatório por padrão. É possível selecionar mais colunas. Desmarque uma coluna selecionada para excluí-la no relatório.

   ![Selecionar ou desmarcar colunas de relatório](assets/configure_columns.png)

   Para exibir um nome de coluna ou caminho de propriedade personalizado, configure as propriedades para o binário de ativo no nó `jcr:content` no CRX. Como alternativa, adicione-o através do seletor de caminho de propriedade.

   ![Selecionar ou desmarcar colunas de relatório](assets/custom_columns.png)

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatórios foi iniciada.
1. Na página [!UICONTROL Relatórios de ativos], o status de geração de relatórios baseia-se no estado atual do trabalho de relatório, por exemplo [!UICONTROL Êxito], [!UICONTROL Falha], [!UICONTROL Enfileirado] ou [!UICONTROL Agendado]. O mesmo status aparece na caixa de entrada de notificações.Para visualização na página de relatório, clique no link do relatório. Como alternativa, selecione o relatório e clique em **[!UICONTROL Visualização]** na barra de ferramentas.

   ![Um relatório gerado](assets/report_page.png)

   Clique em **[!UICONTROL Baixar]** na barra de ferramentas para baixar o relatório no formato CSV.

## Adicionar colunas personalizadas {#add-custom-columns}

Você pode adicionar colunas personalizadas aos seguintes relatórios para exibir mais dados para seus requisitos personalizados:

* Imagem
* Download
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] Publicar
* Arquivos

Para adicionar colunas personalizadas a esses relatórios, siga estas etapas:

1. Em [!DNL Manager interface], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Relatórios]**.
1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.

1. Na página **[!UICONTROL Criar relatório]**, escolha o relatório que deseja criar e clique em **[!UICONTROL Próximo]**.
1. Configure detalhes do relatório, como título, descrição, miniatura, caminho da pasta e intervalo de datas, conforme aplicável.

1. Para exibir uma coluna personalizada, especifique o nome da coluna em **[!UICONTROL Colunas personalizadas]**.

   ![Especificar o nome da coluna personalizada do relatório](assets/custom_columns-1.png)

1. Adicione o caminho de propriedade sob o nó `jcr:content` no CRXDE usando o seletor de caminho de propriedade. Como alternativa, digite o caminho no campo de caminho da propriedade.

   ![Mapear o caminho de propriedade de caminhos em jcr:content](assets/property_picker.png)

   Para adicionar mais colunas personalizadas, clique em **[!UICONTROL Adicionar]** e repita as etapas 5 e 6.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatórios foi iniciada.

## Configurar o serviço de remoção {#configure-purging-service}

Para remover relatórios que não são mais necessários, configure o serviço de Expurgação de relatórios do DAM do console da Web para expurgar os relatórios existentes com base na quantidade e idade.

1. Acesse o console da Web (gerenciador de configuração) de `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL DAM Report Purge Service]**.
1. Especifique a frequência (intervalo de tempo) do serviço de expurgação no campo `scheduler.expression.name`. Você também pode configurar a idade e o limite de quantidade para os relatórios.
1. Salve as alterações.

## Solução de problemas de informações, dicas e limitações {#best-practices-and-limitations}

* Se alguns relatórios ou números nos relatórios não estiverem disponíveis ou conforme esperado, certifique-se de que o serviço [!UICONTROL Gravador de Evento Day CQ DAM] esteja ativado.

* Remova os relatórios que não são mais necessários. Use as opções de configuração no serviço de Expurgação de relatório do DAM para configurar os critérios para expurgar relatórios.

* Se o Relatório de uso de disco não for gerado e você estiver usando [!DNL Dynamic Media], verifique se todos os ativos foram processados corretamente. Para resolver, reprocesse os ativos e gere o relatório novamente.
