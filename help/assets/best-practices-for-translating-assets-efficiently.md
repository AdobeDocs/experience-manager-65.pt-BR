---
title: Práticas recomendadas para traduzir ativos
description: Práticas recomendadas para o gerenciamento eficiente de ativos para sincronizar várias versões traduzidas e simplificar fluxos de trabalho de tradução.
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 1%

---

# Práticas recomendadas para traduzir ativos {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] O oferece suporte a fluxos de trabalho multilíngues para traduzir binários, metadados e tags de ativos digitais em várias localidades e gerenciar os ativos traduzidos. Para obter detalhes, consulte [Ativos multilíngues](multilingual-assets.md).

Para obter um gerenciamento eficiente de ativos para garantir que diferentes versões traduzidas permaneçam sincronizadas, crie [cópias de idioma](preparing-assets-for-translation.md) de ativos antes de executar fluxos de trabalho de tradução.

Uma cópia de idioma de um ativo ou grupo de ativos é um irmão de idioma (ou uma versão do(s) ativo(s) em um idioma cognato) com uma hierarquia de conteúdo semelhante.

Cada cópia de idioma é um ativo independente. Portanto, a tradução de ativos em várias localidades pode aumentar consideravelmente o tamanho do repositório CRX. Por exemplo, traduzir ativos com um tamanho combinado de 10 GB em dois idiomas pode aumentar o tamanho do repositório em aproximadamente 20 GB (10 GB para cada idioma).

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

1. Ativar o [!UICONTROL Definir última data de modificação] fluxo de trabalho.

   A variável [!UICONTROL Writeback de metadados DAM] O fluxo de trabalho configura a data da última modificação de um ativo. Como você desativa esse fluxo de trabalho na etapa 2, [!DNL Assets] O não pode mais manter a data da última modificação de ativos atualizada. Portanto, habilite o *Definir última data de modificação* fluxo de trabalho para garantir que as datas da última modificação dos ativos estejam atualizadas. Ativos com datas desatualizadas da última modificação podem causar erros.

1. [Configurar a estrutura de integração de tradução](/help/sites-administering/tc-tic.md) para interromper a conversão de binários de ativos. Desmarque a opção **[!UICONTROL Traduzir ativos]** opção no campo [!UICONTROL Assets] para interromper a tradução de binários de Ativos.
1. Traduzir metadados/tags de ativos usando [Fluxos de trabalho de ativos multilíngues](multilingual-assets.md).
