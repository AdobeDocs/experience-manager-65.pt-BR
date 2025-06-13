---
title: Writeback XMP para representações
description: Saiba como o recurso de writeback do XMP propaga as alterações de metadados de um ativo para todas as representações ou representações específicas do ativo.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 6%

---

# Writeback XMP para representações {#xmp-writeback-to-renditions}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/pt-br/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata) |
| AEM 6.5 | Este artigo |

Esse recurso de write-back do XMP em [!DNL Adobe Experience Manager Assets] replica as alterações de metadados nas representações do ativo original. Ao alterar os metadados de um ativo no Assets ou ao fazer upload do ativo, as alterações são inicialmente armazenadas no nó de metadados na hierarquia do ativo.

O recurso de write-back do XMP permite propagar as alterações de metadados para todas as representações ou representações específicas do ativo. O recurso grava somente as propriedades de metadados que usam namespaces registrados, ou seja, uma propriedade chamada `dc:title` é gravada, mas uma propriedade chamada `mytitle` não.

Considere um cenário em que você modifica a propriedade [!UICONTROL Title] do ativo intitulado `Classic Leather` para `Nylon`.

![metadados](assets/metadata.png)

Nesse caso, o [!DNL Experience Manager Assets] salva as alterações na propriedade **[!UICONTROL Title]** no parâmetro `dc:title` para os metadados de ativos armazenados na hierarquia de ativos.

![metadados_armazenados](assets/metadata_stored.png)

No entanto, o [!DNL Experience Manager Assets] não propaga automaticamente quaisquer alterações de metadados nas representações de um ativo. Consulte [como habilitar o write-back do XMP](#enable-xmp-writeback).

## Habilitar write-back do XMP {#enable-xmp-writeback}

Para habilitar a propagação das alterações de metadados nas representações do ativo ao carregá-lo, modifique a configuração do **[!UICONTROL Criador de representação do Adobe CQ DAM]** no Gerenciador de configurações.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a **[!UICONTROL configuração do Criador de representação do Adobe CQ DAM]**.
1. Selecione a opção **[!UICONTROL Propagar XMP]** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Ativação do Writeback XMP para representações específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso Writeback XMP propague alterações de metadados para selecionar representações, especifique essas representações para a etapa do fluxo de trabalho Processo de Writeback XMP do fluxo de trabalho [!UICONTROL WriteBack de Metadados DAM]. Por padrão, essa etapa é configurada com a representação original.

Para que o recurso Writeback do XMP propague metadados para as miniaturas de representação 140.100.png e 319.319.png, execute essas etapas.

1. Na interface do Experience Manager, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Fluxo de trabalho]** > **[!UICONTROL Modelos]**.
1. Na página Modelos, abra o modelo de fluxo de trabalho **[!UICONTROL Writeback de metadados DAM]**.
1. Na página de propriedades **[!UICONTROL DAM Metadata Writeback]**, abra a etapa **[!UICONTROL Processo de Writeback XMP]**.
1. Na caixa de diálogo [!UICONTROL Propriedades da Etapa], clique na guia **[!UICONTROL Processo]**.
1. Na caixa **Argumentos**, adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png` e clique em **[!UICONTROL OK]**.

   ![propriedades_da_etapa](assets/step_properties.png)

1. Salve as alterações.
1. Para regenerar as representações de pirâmide do TIFF para imagens [!DNL Dynamic Media] com os novos atributos, adicione a etapa **[!UICONTROL Assets de Imagem do Processo do Dynamic Media]** ao fluxo de trabalho [!UICONTROL Writeback de Metadados do DAM].

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o workflow.

As alterações de metadados são propagadas para as representações thumbnail.140.100.png e thumbnail.319.319.png do ativo, e não para as outras.

>[!NOTE]
>
>Para as plataformas compatíveis, consulte [pré-requisitos de gravação de metadados do XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtragem de metadados do XMP {#filtering-xmp-metadata}

O [!DNL Experience Manager Assets] oferece suporte à filtragem de lista de bloqueios e lista de permissões de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados em JCR quando os ativos são assimilados.

A filtragem usando uma lista de bloqueios permite importar todas as propriedades de metadados do XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos como arquivos INDD que têm quantidades enormes de metadados do XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem usando uma lista de bloqueios permitir que um grande número de ativos com vários metadados XMP seja importado, a implantação do [!DNL Experience Manager] pode encontrar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem de metadados do XMP por meio do lista de permissões resolve esse problema, permitindo que você defina as propriedades do XMP que serão importadas. Dessa forma, qualquer outra propriedade ou propriedade desconhecida do XMP é ignorada. Para compatibilidade com versões anteriores, você pode adicionar algumas dessas propriedades ao filtro que usa uma lista de bloqueios.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes do XMP em binários de ativos. Para as propriedades derivadas de fontes diferentes do XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada na propriedade chamada `CreateDate` no EXIF TIFF. O Experience Manager armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a origem é uma origem que não é do XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **[!UICONTROL Adobe CQ DAM XmpFilter]**.
1. Para aplicar a filtragem por meio de uma lista de permissões, selecione **[!UICONTROL Aplicar Inclui na lista de permissões às Propriedades da XMP]** e especifique as propriedades a serem importadas na caixa **[!UICONTROL Nomes XML permitidos para filtragem da XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades bloqueadas do XMP depois de aplicar a filtragem por meio da lista de permissões, especifique aquelas na caixa **[!UICONTROL Nomes XML bloqueados para filtragem do XMP]**.

   >[!NOTE]
   >
   >A opção **[!UICONTROL Aplicar Inclui na lista de bloqueios às propriedades do XMP]** é selecionada por padrão. Em outras palavras, a filtragem usando uma lista de bloqueios é ativada por padrão. Para desabilitar essa filtragem, cancele a seleção da opção **[!UICONTROL Aplicar XMP às Propriedades da Incluir na lista de bloqueios]**.

1. Salve as alterações.
