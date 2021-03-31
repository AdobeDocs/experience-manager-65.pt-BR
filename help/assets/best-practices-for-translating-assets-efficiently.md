---
title: Práticas recomendadas para traduzir ativos
description: Práticas recomendadas para o gerenciamento eficiente de ativos para sincronizar várias versões traduzidas e simplificar os fluxos de trabalho de tradução.
contentOwner: AG
role: Administrador
feature: Gerenciamento de ativos
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 1%

---


# Práticas recomendadas para traduzir ativos {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] O suporta fluxos de trabalho multilíngues para traduzir binários, metadados e tags de ativos digitais em várias localidades e gerenciar os ativos traduzidos. Para obter detalhes, consulte [Ativos multilíngues](multilingual-assets.md).

Para o gerenciamento eficiente de ativos para garantir que diferentes versões traduzidas permaneçam sincronizadas, crie [cópias de idioma](preparing-assets-for-translation.md) de ativos antes de executar fluxos de trabalho de tradução.

Uma cópia de idioma de um ativo ou de um grupo de ativos é um idioma irmão (ou uma versão do(s) ativo(s) em uma linguagem cognitiva) com uma hierarquia de conteúdo semelhante.

Cada cópia de idioma é um ativo independente. Portanto, traduzir ativos em várias localidades pode aumentar drasticamente o tamanho do repositório CRX. Por exemplo, traduzir ativos com um tamanho combinado de 10 GB em dois idiomas pode aumentar o tamanho do repositório em aproximadamente 20 GB (10 GB para cada idioma).

Os binários de ativos ocupam um espaço de armazenamento muito maior em comparação aos metadados e tags. Portanto, se a tradução de metadados e tags servir apenas à sua finalidade, omita para traduzir os binários. Você pode reter a cópia original dos binários no repositório para associação com metadados e tags traduzidos para diferentes locais. Manter uma única cópia de binários, em vez de várias versões traduzidas, minimiza o impacto no tamanho do repositório.

O File Data Store e o Amazon S3 Data Store fornecem uma infraestrutura de armazenamento mais adequada para esses cenários. Esses repositórios de armazenamento armazenam uma única cópia de binários de ativos (incluindo representações) que podem ser compartilhados por metadados e tags em várias localidades. Portanto, criar cópias de idioma de ativo e traduzir metadados e tags não afeta o tamanho do repositório.

Você também pode fazer algumas alterações na configuração de alguns fluxos de trabalho e na estrutura de integração de tradução para simplificar ainda mais o processo.

1. Faça uma das seguintes opções:

   * [Configurar Arquivo Data Store](/help/sites-deploying/data-store-config.md)
   * [Configurar o Data Store do Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Habilite o workflow [!UICONTROL Definir data da última modificação].

   O workflow [!UICONTROL DAM MetaData Writeback] configura a data da última modificação para um ativo. Como você desativa esse fluxo de trabalho na etapa 2, [!DNL Assets] não é mais capaz de manter a data da última modificação dos ativos atualizada. Portanto, ative o workflow *Definir data da última modificação* para garantir que as datas da última modificação dos ativos estejam atualizadas. Os ativos com datas da última modificação desatualizadas podem causar erros.

1. [Configure a ](/help/sites-administering/tc-tic.md) estrutura de integração de tradução para parar a tradução de binários de ativos. Desmarque a opção **[!UICONTROL Traduzir ativos]** na guia [!UICONTROL Ativos] para interromper a tradução de binários de Ativos.
1. Traduza metadados/tags de ativos usando [Fluxos de trabalho de ativos multilíngues](multilingual-assets.md).
