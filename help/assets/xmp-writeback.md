---
title: Write-back de XMP a execuções
description: Saiba como o recurso de write-back de XMP propaga as alterações de metadados de um ativo para todas as representações ou representações específicas do ativo.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 6%

---

# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Este artigo |
| AEM 6.4 | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=en) |

Este recurso de write-back de XMP em [!DNL Adobe Experience Manager Assets] replica as alterações de metadados nas representações do ativo original. Ao alterar os metadados de um ativo de dentro do Assets ou ao fazer upload do ativo, as alterações são armazenadas inicialmente no nó de metadados na hierarquia de ativos.

O recurso de write-back de XMP permite propagar as alterações de metadados para todas as representações ou representações específicas do ativo. O recurso grava somente as propriedades de metadados que usam `jcr` namespace, ou seja, uma propriedade chamada `dc:title` é gravado de volta, mas uma propriedade chamada `mytitle` não é.

Considere um cenário em que você modifica a variável [!UICONTROL Título] propriedade do ativo intitulado `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Nesse caso, a variável [!DNL Experience Manager Assets] salva as alterações no **[!UICONTROL Título]** na `dc:title` para os metadados do ativo armazenados na hierarquia de ativos.

![metadata_stored](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] não propaga automaticamente qualquer alteração de metadados nas representações de um ativo. Consulte [como habilitar XMP write-back](#enable-xmp-writeback).

## Ativar XMP write-back {#enable-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique o **[!UICONTROL Criador de representação do Adobe CQ DAM]** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Criador de representação do Adobe CQ DAM]** configuração.
1. Selecione o **[!UICONTROL Propagar XMP]** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Ativar XMP write-back para representações específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso Writeback de XMP propague alterações de metadados para selecionar representações, especifique essas representações para a etapa XMP do fluxo de trabalho Processo de Writeback de [!UICONTROL WriteBack de metadados de DAM] fluxo de trabalho. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso Writeback de XMP propague metadados para as miniaturas de representação 140.100.png e 319.319.png, execute estas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos , abra o **[!UICONTROL Writeback de metadados DAM]** modelo de fluxo de trabalho.
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. No [!UICONTROL Propriedades da etapa] , clique no botão **[!UICONTROL Processo]** guia .
1. No **Argumentos** caixa, adicionar `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e clique em **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de TIFF da pirâmide para [!DNL Dynamic Media] imagens com os novos atributos, adicione o **[!UICONTROL Ativos de imagem de processo Dynamic Media]** para [!UICONTROL Writeback de metadados DAM] fluxo de trabalho.

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o workflow.

As alterações de metadados são propagadas para a miniatura de representações.140.100.png e thumbnail.319.319.png do ativo, e não para os outros.

>[!NOTE]
>
>Para XMP problemas de write-back no Linux de 64 bits, consulte [Como habilitar XMP write-back no RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para as plataformas compatíveis, consulte [Pré-requisitos de gravação de metadados de XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrar metadados XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] O suporta a filtragem de lista de bloqueios e lista de permissões de propriedades/nós para metadados de XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são assimilados.

Filtrar usando uma lista de bloqueios permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos como arquivos INDD que têm grandes quantidades de metadados de XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes de nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem com uma lista de bloqueios permitir que um grande número de ativos com vários metadados de XMP seja importado, a variável [!DNL Experience Manager] a implantação pode encontrar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados de XMP por meio do lista de permissões resolve esse problema permitindo definir as propriedades de XMP a serem importadas. Dessa forma, quaisquer propriedades de XMP outras ou desconhecidas são ignoradas. Para ter compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista de bloqueios.

>[!NOTE]
>
>A filtragem funciona somente nas propriedades derivadas de fontes de XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada na propriedade chamada `CreateDate` no TIFF EXIF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Adobe CQ DAM XmpFilter]** configuração.
1. Para aplicar a filtragem por meio de uma lista de permissões, selecione **[!UICONTROL Aplicar Lista de permissões às propriedades XMP]** e especifique as propriedades que serão importadas no **[!UICONTROL Nomes XML permitidos para filtragem de XMP]** caixa.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades de XMP bloqueadas após aplicar a filtragem por lista de permissões, especifique as propriedades no **[!UICONTROL Nomes XML bloqueados para filtragem de XMP]** caixa.

   >[!NOTE]
   >
   >O **[!UICONTROL Aplicar Lista de bloqueios às propriedades XMP]** é selecionada por padrão. Em outras palavras, a filtragem usando uma lista de bloqueios é ativada por padrão. Para desativar essa filtragem, cancele a seleção da variável **[!UICONTROL Aplicar Lista de bloqueios às propriedades XMP]** opção.

1. Salve as alterações.
