---
title: Práticas recomendadas para traduzir ativos
description: Práticas recomendadas para o gerenciamento eficiente de ativos para sincronizar várias versões traduzidas e simplificar os fluxos de trabalho de tradução.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Práticas recomendadas para traduzir ativos {#best-practices-for-translating-assets-efficiently}

Os ativos Adobe Experience Manager (AEM) oferecem suporte a fluxos de trabalho multilíngues para traduzir binários, metadados e tags de ativos digitais em várias localidades e gerenciar os ativos convertidos. Para obter detalhes, consulte Ativos [multilíngues](multilingual-assets.md).

Para o gerenciamento eficiente de ativos para garantir que diferentes versões traduzidas permaneçam sincronizadas, crie cópias [de](preparing-assets-for-translation.md) idioma de ativos antes de executar fluxos de trabalho de tradução.

Uma cópia de idioma de um ativo ou de um grupo de ativos é um idioma irmão (ou uma versão do(s) ativo(s) em uma linguagem cognitiva) com uma hierarquia de conteúdo semelhante.

Cada cópia de idioma é um ativo independente. Portanto, a conversão de ativos em várias localidades pode aumentar drasticamente o tamanho do repositório CRX. Por exemplo, a tradução de ativos com um tamanho combinado de 10 GB em dois idiomas pode aumentar o tamanho do repositório em aproximadamente 20 GB (10 GB para cada idioma).

Os binários de ativos ocupam um espaço de armazenamento muito maior em comparação aos metadados e tags. Portanto, se a tradução de metadados e tags serve apenas à sua finalidade, omita traduzir os binários. Você pode reter a cópia original dos binários no repositório para associação com metadados e tags traduzidos para localidades diferentes. A manutenção de uma única cópia de binários, em vez de várias versões traduzidas, minimiza o impacto no tamanho do repositório.

O File Data Store e o Amazon S3 Data Store fornecem uma infraestrutura de armazenamento mais adequada a esses cenários. Esses repositórios de armazenamento armazenam uma única cópia de binários de ativos (incluindo execuções) que podem ser compartilhados por metadados e tags em várias localidades. Portanto, a criação de cópias de idioma do ativo e a tradução de metadados e tags não afeta o tamanho do repositório.

Você também pode fazer algumas alterações de configuração em alguns fluxos de trabalho e na estrutura de integração de tradução para simplificar ainda mais o processo.

1. Faça uma das seguintes opções:

   * [Configurar Arquivo Data Store](/help/sites-deploying/data-store-config.md)
   * [Configurar o Amazon S3 Data Store](/help/sites-deploying/data-store-config.md)

1. Desative o fluxo de trabalho de Write-back [de Metadados do](/help/sites-administering/workflow-offloader.md#disable-offloading) DAM.

   Como o nome sugere, o fluxo de trabalho de Writeback [!UICONTROL de Metadados] DAM regrava os metadados no arquivo binário. Como os metadados mudam após a tradução, gravá-los de volta no arquivo binário gera um binário diferente para uma cópia de idioma.

   >[!NOTE]
   >
   >A desativação do fluxo de trabalho de Writeback [!UICONTROL de Metadados] DAM desativa a gravação de metadados XMP nos binários de ativos. Consequentemente, alterações futuras nos metadados não serão mais salvas nos ativos. Avalie as consequências antes de desativar esse fluxo de trabalho.

1. Ative o fluxo de trabalho [!UICONTROL Definir última data] modificada.

   O fluxo de trabalho [!UICONTROL DAM MetaData Writeback] configura a última data modificada para um ativo. Como você desativa esse fluxo de trabalho na etapa 2, os ativos AEM não podem mais manter a última data modificada dos ativos atualizados. Portanto, ative o fluxo de trabalho *Definir última data* modificada para garantir que as últimas datas modificadas dos ativos estejam atualizadas. Os ativos com datas de última modificação desatualizadas podem causar erros.

1. [Configure a estrutura](/help/sites-administering/tc-tic.md) de integração de tradução para parar a tradução de binários de ativos. Desmarque a opção **[!UICONTROL Traduzir ativos]** na guia Ativos para interromper a conversão de binários de ativos.
1. Traduza metadados/tags de ativos usando fluxos de trabalho de ativos [multilíngues](multilingual-assets.md).
