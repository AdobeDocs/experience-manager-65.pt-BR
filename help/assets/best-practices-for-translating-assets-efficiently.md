---
title: Práticas recomendadas para traduzir ativos
description: Práticas recomendadas para o gerenciamento eficiente de ativos para sincronizar várias versões traduzidas e simplificar os workflows de tradução.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---


# Práticas recomendadas para traduzir ativos {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] suporta workflows multilíngues para traduzir binários, metadados e tags para ativos digitais em várias localidades e gerenciar os ativos traduzidos. Para obter detalhes, consulte Ativos [multilíngues](multilingual-assets.md).

Para o gerenciamento eficiente de ativos, a fim de garantir que diferentes versões traduzidas permaneçam sincronizadas, crie cópias [de](preparing-assets-for-translation.md) idioma de ativos antes de executar workflows de tradução.

Uma cópia de idioma de um ativo ou de um grupo de ativos é um idioma irmão (ou uma versão do(s) ativo(s) em uma linguagem cognitiva) com uma hierarquia de conteúdo semelhante.

Cada cópia de idioma é um ativo independente. Portanto, a conversão de ativos em várias localidades pode aumentar drasticamente o tamanho do repositório CRX. Por exemplo, a tradução de ativos com um tamanho combinado de 10 GB em dois idiomas pode aumentar o tamanho do repositório em aproximadamente 20 GB (10 GB para cada idioma).

Os binários de ativos ocupam um espaço de armazenamento muito maior em comparação aos metadados e tags. Portanto, se a tradução de metadados e tags serve apenas à sua finalidade, omita traduzir os binários. Você pode reter a cópia original dos binários no repositório para associação com metadados e tags traduzidos para localidades diferentes. A manutenção de uma única cópia de binários, em vez de várias versões traduzidas, minimiza o impacto no tamanho do repositório.

O File Data Store e o Amazon S3 Data Store fornecem uma infraestrutura de armazenamento mais adequada para esses cenários. Esses repositórios de armazenamentos armazenam uma única cópia dos binários de ativos (incluindo execuções) que podem ser compartilhados por metadados e tags em várias localidades. Portanto, a criação de cópias de idioma do ativo e a tradução de metadados e tags não afeta o tamanho do repositório.

Você também pode fazer algumas alterações de configuração em alguns workflows e na estrutura de integração de tradução para agilizar ainda mais o processo.

1. Faça uma das seguintes opções:

   * [Configurar Arquivo Data Store](/help/sites-deploying/data-store-config.md)
   * [Configurar o Amazon S3 Data Store](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Ative o fluxo de trabalho [!UICONTROL Definir última data] modificada.

   O fluxo de trabalho [!UICONTROL DAM MetaData Writeback] configura a última data modificada para um ativo. Como você desativa esse fluxo de trabalho na etapa 2, não [!DNL Assets] é mais capaz de manter a última data modificada dos ativos atualizados. Portanto, ative o fluxo de trabalho *Definir última data* modificada para garantir que as últimas datas modificadas dos ativos estejam atualizadas. Os ativos com datas de última modificação desatualizadas podem causar erros.

1. [Configure a estrutura](/help/sites-administering/tc-tic.md) de integração de tradução para parar a tradução de binários de ativos. Desmarque a opção **[!UICONTROL Traduzir ativos]** na guia [!UICONTROL Ativos] para interromper a tradução de binários de ativos.
1. Traduza metadados/tags de ativos usando workflows [](multilingual-assets.md)de ativos multilíngues.
