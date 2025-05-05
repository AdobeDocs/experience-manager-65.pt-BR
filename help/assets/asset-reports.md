---
title: Relatórios sobre o uso e o compartilhamento de ativos
description: Relatórios sobre seus ativos no [!DNL Adobe Experience Manager Assets]  que ajudam você a entender o uso, a atividade e o compartilhamento de seus ativos digitais.
contentOwner: AG
role: User, Admin
feature: Asset Reports,Asset Management
exl-id: b4963a03-3496-4c6c-9d30-8812304d0e9f
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 8%

---

# Relatórios de ativos {#asset-reports}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/asset-reports.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |

Os relatórios de ativos permitem avaliar a utilidade da implantação do [!DNL Adobe Experience Manager Assets]. Com o [!DNL Assets], você pode gerar vários relatórios para seus ativos digitais. Os relatórios fornecem informações úteis sobre o uso do sistema, como os usuários interagem com ativos e quais ativos são baixados e compartilhados.

Use as informações nos relatórios para obter as principais métricas de sucesso e medir a adoção do [!DNL Assets] na sua empresa e por clientes.

A estrutura de relatório [!DNL Assets] usa [!DNL Sling] trabalhos para processar de forma assíncrona solicitações de relatório de maneira ordenada. Ele é escalável para repositórios grandes. O processamento assíncrono de relatórios aumenta a eficiência e a velocidade com que os relatórios são gerados.

A interface de gerenciamento de relatórios é intuitiva e inclui opções e controles refinados para acessar relatórios arquivados e exibir status de execução de relatórios (bem-sucedido, com falha e em fila).

Quando um relatório é gerado, você é notificado por email (opcional) e uma notificação na caixa de entrada. É possível visualizar, baixar ou excluir um relatório da página de listagem de relatórios, na qual todos os relatórios gerados anteriormente são exibidos.

## Pré-requisitos {#prerequisite-for-reporting}

Para gerar relatórios, faça o seguinte:

* Habilitar o serviço [!UICONTROL Day CQ DAM Event Recorder] em **[!UICONTROL Ferramentas]** > **[!UICONTROL Operações]** > **[!UICONTROL Console da Web]**.
* Selecione as atividades ou eventos sobre os quais deseja criar relatórios. Por exemplo, para gerar um relatório sobre ativos baixados, selecione [!UICONTROL Ativo baixado (BAIXADO)].

![Habilitar relatórios de ativos no Console da Web](assets/reports-config-day-cq-dam-event-recorder.png)

## Gerar relatórios {#generate-reports}

[!DNL Experience Manager Assets] gera os seguintes relatórios padrão para você:

* Upload
* Download
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] publicação
* Uso do disco
* Arquivos
* Compartilhamento de link

Os administradores do [!DNL Adobe Experience Manager] podem facilmente gerar e personalizar esses relatórios para sua implementação. Um administrador pode seguir estas etapas para gerar um relatório:

1. Na interface do [!DNL Experience Manager], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.

   ![Página de ferramentas para navegar pelo relatório de ativos](assets/AssetsReportNavigation.png)

1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.
1. Na página **[!UICONTROL Criar Relatório]**, escolha o relatório que deseja criar e clique em **[!UICONTROL Avançar]**.

   ![Selecionar tipo de relatório](assets/choose_report.png)

   >[!NOTE]
   >
   >Por padrão, os Fragmentos de conteúdo e os compartilhamentos de link são incluídos no relatório de Ativo [!UICONTROL Download]. Selecione a opção apropriada para criar um relatório de compartilhamentos de links ou excluir Fragmentos de conteúdo do relatório de download.

   >[!NOTE]
   >
   >O relatório [!UICONTROL Download] exibe detalhes apenas dos ativos que são baixados após a seleção individual ou que são baixados por meio da Ação Rápida. No entanto, não inclui os detalhes dos ativos que estão dentro de uma pasta baixada.

1. Configure os detalhes do relatório, como título, descrição, miniatura e caminho da pasta no repositório do CRX onde o relatório está armazenado. Por padrão, o caminho da pasta é `/content/dam`. Você pode especificar um caminho diferente.

   ![Página para adicionar detalhes do relatório](assets/report_configuration.png)

   Escolha o intervalo de datas do relatório.

   Você pode optar por gerar o relatório agora ou em uma data e hora futuras.

   >[!NOTE]
   >
   >Se optar por agendar o relatório posteriormente, certifique-se de especificar a data e a hora nos campos Data e Hora. Se você não especificar nenhum valor, o mecanismo de relatório o tratará como um relatório a ser gerado instantaneamente.

   Os campos de configuração podem diferir de acordo com o tipo de relatório que você cria. Por exemplo, o relatório **[!UICONTROL Uso de disco]** fornece opções para incluir representações de ativos ao calcular o espaço em disco usado por ativos. Você pode optar por incluir ou excluir ativos em subpastas para cálculo de uso do disco.

   >[!NOTE]
   >
   >O relatório **[!UICONTROL Uso de disco]** não inclui campos de intervalo de datas porque indica apenas o uso atual do espaço em disco.

   ![Página de detalhes do relatório de Uso de Disco](assets/disk_usage_configuration.png)

   Ao criar o relatório **[!UICONTROL Arquivos]**, você pode incluir/excluir subpastas. No entanto, não é possível incluir representações de ativos neste relatório.

   ![Página de detalhes do relatório de arquivos](assets/files_report.png)

   O relatório **[!UICONTROL Compartilhamento de links]** exibe URLs de ativos que são compartilhados com usuários externos a partir do [!DNL Assets]. Inclui IDs de email do usuário que compartilhou os ativos, IDs de email de usuários com os quais os ativos são compartilhados, data de compartilhamento e data de expiração do link. As colunas não são personalizáveis.

   O relatório **[!UICONTROL Compartilhamento de links]** não inclui opções para subpastas e representações porque apenas publica as URLs compartilhadas que aparecem em `/var/dam/share`.

   ![Página de detalhes do relatório de Compartilhamento de links](assets/link_share.png)

1. Clique em **[!UICONTROL Avançar]** na barra de ferramentas.

1. Na página **[!UICONTROL Configurar Colunas]**, algumas colunas são selecionadas para serem exibidas no relatório por padrão. Você pode selecionar mais colunas. Cancele a seleção de uma coluna para excluí-la no relatório.

   ![Selecione ou cancele a seleção das colunas do relatório](assets/configure_columns.png)

   Para exibir um nome de coluna ou caminho de propriedade personalizado, configure as propriedades para o binário de ativos no nó `jcr:content` no CRX. Como alternativa, adicione-o por meio do seletor de caminho de propriedade.

   ![Selecione ou cancele a seleção das colunas do relatório](assets/custom_columns.png)

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatório foi iniciada.
1. Na página [!UICONTROL Relatórios de ativos], o status de geração de relatório é baseado no estado atual do trabalho de relatório, por exemplo, [!UICONTROL Sucesso], [!UICONTROL Falha], [!UICONTROL Em fila] ou [!UICONTROL Agendado]. O mesmo status aparece na caixa de entrada de notificações.Para exibir a página do relatório, clique no link do relatório. Como alternativa, selecione o relatório e clique em **[!UICONTROL Exibir]** na barra de ferramentas.

   <!--![A generated report](assets/report_page.png)-->
   [Status do relatório](assets/report-status.JPG)

   Clique em **[!UICONTROL Baixar]** na barra de ferramentas para baixar o relatório no formato CSV.

## Adicionar colunas personalizadas {#add-custom-columns}

Você pode adicionar colunas personalizadas aos seguintes relatórios para exibir mais dados de acordo com seus requisitos personalizados:

* Upload
* Download
* Expiração
* Modificação
* Publicação
* [!DNL Brand Portal] publicação
* Arquivos

Para adicionar colunas personalizadas a esses relatórios, siga estas etapas:

1. No [!DNL Manager interface], clique em **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Relatórios]**.
1. Na página [!UICONTROL Relatórios de ativos], clique em **[!UICONTROL Criar]** na barra de ferramentas.

1. Na página **[!UICONTROL Criar Relatório]**, escolha o relatório que deseja criar e clique em **[!UICONTROL Avançar]**.
1. Configure os detalhes do relatório, como título, descrição, miniatura, caminho da pasta e intervalo de datas, conforme aplicável.

1. Para exibir uma coluna personalizada, especifique o nome da coluna em **[!UICONTROL Colunas personalizadas]**.

   ![Especificar nome para a coluna personalizada do relatório](assets/custom_columns-1.png)

1. Adicione o caminho da propriedade no nó `jcr:content` no CRXDE usando o seletor de caminho de propriedade. Como alternativa, digite o caminho no campo caminho da propriedade.

   ![Mapear o caminho de propriedade a partir de caminhos em jcr:content](assets/property_picker.png)

   Para adicionar mais colunas personalizadas, clique em **[!UICONTROL Adicionar]** e repita as etapas 5 e 6.

1. Clique em **[!UICONTROL Criar]** na barra de ferramentas. Uma mensagem notifica que a geração de relatório foi iniciada.

## Configurar serviço de limpeza {#configure-purging-service}

Para remover relatórios desnecessários, configure o serviço de Limpeza de relatórios do DAM no console da Web para limpar os relatórios existentes com base na quantidade e idade.

1. Acesse o console da Web (gerenciador de configurações) de `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **[!UICONTROL Serviço de limpeza de relatórios do DAM]**.
1. Especifique a frequência (intervalo de tempo) do serviço de limpeza no campo `scheduler.expression.name`. Você também pode configurar a idade e o limite de quantidade dos relatórios.
1. Salve as alterações.

## Informações sobre solução de problemas, dicas e limitações {#best-practices-and-limitations}

* Se alguns relatórios ou números nos relatórios não estiverem disponíveis ou como esperado, verifique se o serviço [!UICONTROL Gravador de eventos DAM do DAM do Day] está habilitado.

* Remova os relatórios que não são mais necessários. Use as opções de configuração no serviço de Limpeza de relatório do DAM para configurar os critérios para limpar relatórios.

* Se o Relatório de Uso de Disco não for gerado e você estiver usando o [!DNL Dynamic Media], verifique se todos os ativos estão funcionando corretamente. Para resolver, reprocesse os ativos e gere o relatório novamente.
