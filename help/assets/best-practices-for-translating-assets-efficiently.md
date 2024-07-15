---
title: Práticas recomendadas para traduzir ativos
description: Práticas recomendadas para o gerenciamento eficiente de ativos para sincronizar várias versões traduzidas e simplificar fluxos de trabalho de tradução.
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Práticas recomendadas para traduzir ativos {#best-practices-for-translating-assets-efficiently}

O [!DNL Adobe Experience Manager Assets] oferece suporte a fluxos de trabalho multilíngues para traduzir binários, metadados e marcas de ativos digitais em várias localidades e gerenciar os ativos traduzidos. Para obter detalhes, consulte [Assets multilíngue](multilingual-assets.md).

Para obter um gerenciamento eficiente de ativos e garantir que diferentes versões traduzidas permaneçam sincronizadas, crie [cópias de idioma](preparing-assets-for-translation.md) dos ativos antes de executar fluxos de trabalho de tradução.

Uma cópia de idioma de um ativo ou grupo de ativos é um irmão de idioma (ou uma versão dos ativos em um idioma cognato) com uma hierarquia de conteúdo semelhante.

Cada cópia de idioma é um ativo independente. Portanto, a tradução de ativos em várias localidades pode aumentar consideravelmente o tamanho do repositório do CRX. Por exemplo, traduzir ativos com um tamanho combinado de 10 GB em dois idiomas pode aumentar o tamanho do repositório em aproximadamente 20 GB (10 GB para cada idioma).

Os binários de ativos ocupam um espaço de armazenamento muito maior em comparação aos metadados e às tags. Portanto, se a tradução de metadados e tags servir apenas à sua finalidade, omita a tradução dos binários. Você pode reter a cópia original dos binários no repositório para associação com metadados e tags traduzidos em diferentes localidades. Manter uma única cópia de binários, em vez de várias versões traduzidas, minimiza o impacto no tamanho do repositório.

O File Data Store e o Amazon S3 Data Store fornecem uma infraestrutura de armazenamento que é mais adequada para esses cenários. Esses repositórios de armazenamento armazenam uma única cópia de binários de ativos (incluindo representações) que podem ser compartilhados por metadados e tags em vários locais. Portanto, a criação de cópias de idioma do ativo e a tradução de metadados e tags não afetam o tamanho do repositório.

Você também pode fazer algumas alterações de configuração em alguns fluxos de trabalho e na estrutura de integração de tradução para simplificar ainda mais o processo.

1. Siga uma das seguintes opções:

   * [Configurar o armazenamento de dados do arquivo](/help/sites-deploying/data-store-config.md)
   * [Configurar o armazenamento de dados do Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Habilite o fluxo de trabalho [!UICONTROL Definir data da última modificação].

   O fluxo de trabalho [!UICONTROL Writeback de metadados DAM] configura a data da última modificação de um ativo. Como você desabilita esse fluxo de trabalho na etapa 2, [!DNL Assets] não pode mais manter atualizada a data da última modificação de ativos. Portanto, habilite o fluxo de trabalho *Definir data da última modificação* para garantir que as datas da última modificação dos ativos estejam atualizadas. O Assets com datas desatualizadas da última modificação pode causar erros.

1. [Configure a estrutura de integração de tradução](/help/sites-administering/tc-tic.md) para interromper a tradução de binários de ativos. Desmarque a opção **[!UICONTROL Traduzir Assets]** na guia [!UICONTROL Assets] para interromper a tradução de binários de Ativos.
1. Traduza metadados/marcas de ativos usando [Fluxos de trabalho de ativos multilíngues](multilingual-assets.md).
