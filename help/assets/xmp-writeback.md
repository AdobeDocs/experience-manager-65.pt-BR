---
title: Write-back de XMP a execuções
description: Saiba como o recurso de gravação XMP propaga as alterações de metadados de um ativo para todas as execuções ou representações específicas do ativo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 33ab9845f7800c80a6beb5db06f3fadf582122d0

---


# Write-back de XMP a execuções {#xmp-writeback-to-renditions}

Esse recurso de Writeback XMP nos ativos Adobe Experience Manager (AEM) replica as alterações nos metadados do ativo nas representações do ativo.

Quando você altera os metadados de um ativo dos ativos AEM ou durante o upload do ativo, as alterações são armazenadas inicialmente no nó do ativo no Crx-De.

O recurso de Writeback XMP propaga as alterações de metadados para todas as execuções ou representações específicas do ativo.

Considere um cenário em que você modifica a propriedade Título do ativo com título `Classic Leather` para `Nylon`.

![metadata](assets/metadata.png)

Nesse caso, os ativos AEM salvam as alterações na propriedade **Title** no `dc:title` parâmetro para os metadados do ativo armazenados na hierarquia do ativo.

![metadata_storage](assets/metadata_stored.png)

No entanto, os ativos AEM não propagam automaticamente quaisquer alterações de metadados nas representações de um ativo.

O recurso de Writeback XMP permite que você propague as alterações de metadados para todas as representações ou representações específicas do ativo. No entanto, as alterações não são armazenadas no nó de metadados na hierarquia do ativo. Em vez disso, esse recurso incorpora as alterações nos arquivos binários das execuções.

## Habilitando o write-back XMP {#enabling-xmp-writeback}

Para permitir que as alterações de metadados sejam propagadas para as representações do ativo ao carregá-lo, modifique a configuração do **Adobe CQ DAM Rendition Maker** no Configuration Manager.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração do **Adobe CQ DAM Rendition Maker** .
1. Selecione a opção **Propagar XMP** e salve as alterações.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Habilitar o write-back XMP para execuções específicas {#enabling-xmp-writeback-for-specific-renditions}

Para permitir que o recurso de Gravação XMP propague alterações de metadados para selecionar execuções, especifique essas execuções para a etapa de fluxo de trabalho do Processo de Gravação XMP do fluxo de trabalho WriteBack de Metadados DAM. Por padrão, essa etapa é configurada com a representação original.

Para o recurso de Writeback XMP propagar metadados para as miniaturas de execução 140.100.png e 319.319.png, execute estas etapas.

1. Toque/clique no logotipo do AEM e navegue até **Ferramentas** > **Fluxo de trabalho** > **Modelos**.
1. Na página Modelos, abra o modelo de fluxo de trabalho Writeback **de metadados** DAM.
1. Na página de propriedades **DAM Metadata Writeback**, abra a etapa **Processo de Writeback XMP**.
1. Na caixa de diálogo Propriedades da etapa, toque/clique na guia **Processo**.
1. Na caixa **Argumentos** , adicione `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`e toque/clique em **OK**.

   ![step_properties](assets/step_properties.png)

1. Salve as alterações.
1. To regenerate the pyramid TIF renditions for Dynamic Media images with the new attributes, add the **Dynamic Media Process Image Assets** step to the DAM Metadata Writeback workflow.

   As representações PTIFF são criadas e armazenadas apenas localmente em uma implementação híbrida do Dynamic Media.

1. Salve o fluxo de trabalho.

As alterações de metadados são propagadas para as representações representações thumbnail.140.100.png e thumbnail.319.319.png do ativo, e não para as outras.

>[!NOTE]
>
>Para problemas de gravação em XMP no Linux de 64 bits, consulte [Como ativar a gravação em XMP no RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)de 64 bits.
>
>Para obter mais informações sobre plataformas compatíveis, consulte Pré-requisitos [de gravação de metadados](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back)XMP.

## Filtrar metadados XMP {#filtering-xmp-metadata}

Os ativos AEM oferecem suporte à filtragem de listas negras e de listas brancas de propriedades/nós para metadados XMP que são lidos de binários de ativos e armazenados no JCR quando os ativos são ingeridos.

A filtragem da lista negra permite importar todas as propriedades de metadados XMP, exceto as propriedades especificadas para exclusão. No entanto, para tipos de ativos, como arquivos INDD que têm quantidades enormes de metadados XMP (por exemplo, 1000 nós com 10.000 propriedades), os nomes dos nós a serem filtrados nem sempre são conhecidos antecipadamente. Se a filtragem da lista negra permitir a importação de um grande número de ativos com diversos metadados XMP, a instância/cluster do AEM poderá enfrentar problemas de estabilidade, por exemplo, filas de observação obstruídas.

A filtragem da lista de permissões dos metadados XMP resolve esse problema ao permitir que você defina as propriedades XMP a serem importadas. Dessa forma, outras propriedades XMP/desconhecidas são ignoradas. Você pode adicionar algumas dessas propriedades ao filtro da lista negra para compatibilidade com versões anteriores.

>[!NOTE]
>
>A filtragem funciona somente para as propriedades derivadas de fontes XMP em binários de ativos. Para as propriedades derivadas de fontes não XMP, como formatos EXIF e IPTC, a filtragem não funciona. Por exemplo, a data de criação do ativo é armazenada em uma propriedade chamada `CreateDate` em EXIF TIFF. O AEM armazena esse valor em um campo de metadados chamado `exif:DateTimeOriginal`. Como a fonte é uma fonte não XMP, a filtragem não funciona nessa propriedade.

1. Para abrir o Configuration Manager, acesse `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra a configuração **Adobe CQ DAM XmpFilter** .
1. Para aplicar a filtragem de lista de permissões, selecione **Aplicar lista de permissões às propriedades XMP** e especifique as propriedades que serão importadas na caixa **Nomes XML na lista de permissões para filtragem XMP**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Para filtrar as propriedades XMP proibidas após aplicar a filtragem de lista de permissões, especifique-as na caixa **Nomes XML não permitidos para filtragem XMP**.

   >[!NOTE]
   >
   >A opção **Aplicar lista negra a propriedades** XMP está selecionada por padrão. Em outras palavras, a filtragem da lista negra é ativada por padrão. Para desativar a filtragem da lista negra, desmarque a opção **Aplicar lista negra às propriedades** XMP.

1. Salve as alterações.
