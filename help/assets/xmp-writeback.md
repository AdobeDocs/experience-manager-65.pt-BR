---
title: Writeback XMP para representações
description: Saiba como o recurso de writeback XMP propaga as alterações de metadados de um ativo para todas as representações ou representações específicas do ativo.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 5%

---

# Writeback XMP para representações {#xmp-writeback-to-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Este artigo |

Esse recurso de writeback XMP no [!DNL Adobe Experience Manager Assets] O replica as alterações nos metadados nas representações do ativo original. Ao alterar os metadados de um ativo no Assets ou ao fazer upload do ativo, as alterações são inicialmente armazenadas no nó de metadados na hierarquia do ativo.

O recurso de writeback XMP permite propagar as alterações de metadados em todas as representações ou representações específicas do ativo. O recurso grava somente as propriedades de metadados que usam `jcr` namespace, ou seja, uma propriedade chamada `dc:title` é gravado de volta, mas uma propriedade chamada `mytitle` não é.

Considere um cenário em que você modifica a variável [!UICONTROL Título] propriedade do ativo intitulada `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Neste caso, o [!DNL Experience Manager Assets] salva as alterações no **[!UICONTROL Título]** propriedade na `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadata_stored](assets/metadata_stored.png)

No entanto, [!DNL Experience Manager Assets] O não propaga automaticamente quaisquer alterações de metadados para as representações de um ativo. Consulte [como ativar o writeback XMP](#enable-xmp-writeback).

## Ativar writeback XMP {#enable-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a variável **[!UICONTROL Criador de representação do Adobe CQ DAM]** configuração no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL Criador de representação do Adobe CQ DAM]** configuração.
1. Selecione o **[!UICONTROL Propagar XMP]** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Ativação do writeback XMP para representações específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso Writeback XMP propague alterações de metadados para representações selecionadas, especifique essas representações para a etapa do fluxo de trabalho Processo de Writeback XMP de [!UICONTROL WriteBack de metadados DAM] fluxo de trabalho. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso Writeback XMP propague metadados para as miniaturas de representação 140.100.png e 319.319.png, execute essas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos, abra o **[!UICONTROL Writeback de metadados DAM]** modelo de fluxo de trabalho.
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. No [!UICONTROL Propriedades da etapa] caixa de diálogo, clique no botão **[!UICONTROL Processo]** guia.
1. No **Argumentos** caixa, adicionar `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e clique em **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de TIFF da pirâmide para [!DNL Dynamic Media] com os novos atributos, adicione a variável **[!UICONTROL Ativos de imagem do processo Dynamic Media]** etapa para o [!UICONTROL Writeback de metadados DAM] fluxo de trabalho.

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o workflow.

As alterações nos metadados são propagadas para as representações representações miniatura.140.100.png e miniatura.319.319.png do ativo, e não para as outras.

>[!NOTE]
>
>Para problemas de writeback XMP no Linux de 64 bits, consulte [Como habilitar a gravação do XMP no RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Para as plataformas compatíveis, consulte [Pré-requisitos de gravação de metadados XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtragem de metadados XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] O é compatível com a filtragem de propriedades/nós do lista de bloqueios e do lista de permissões para metadados do XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são assimilados.

A filtragem usando uma lista de bloqueios permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos como arquivos INDD que têm quantidades enormes de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem usando uma lista de bloqueios permitir a importação de um grande número de ativos com vários metadados XMP, a variável [!DNL Experience Manager] a implantação do pode encontrar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados de XMP por meio do lista de permissões resolve esse problema, permitindo que você defina as propriedades do XMP que serão importadas. Dessa forma, qualquer outra propriedade ou propriedade desconhecida do XMP é ignorada. Para compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista de bloqueios.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não-XMP, como os formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada na propriedade chamada `CreateDate` no TIFF EXIF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a origem é uma origem não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra o **[!UICONTROL XmpFilter para Adobe CQ DAM]** configuração.
1. Para aplicar a filtragem por meio de uma lista de permissões, selecione **[!UICONTROL Aplicar Inclui na lista de permissões às propriedades XMP]** e especifique as propriedades que serão importadas na variável **[!UICONTROL Nomes XML permitidos para filtragem por XMP]** caixa.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades de XMP bloqueadas após aplicar a filtragem por meio da lista de permissões, especifique aquelas na variável **[!UICONTROL Nomes XML bloqueados para filtragem por XMP]** caixa.

   >[!NOTE]
   >
   >A variável **[!UICONTROL Aplicar Inclui na lista de bloqueios às propriedades XMP]** for selecionada por padrão. Em outras palavras, a filtragem usando uma lista de bloqueios é ativada por padrão. Para desativar essa filtragem, cancele a seleção da variável **[!UICONTROL Aplicar Inclui na lista de bloqueios às propriedades XMP]** opção.

1. Salve as alterações.
