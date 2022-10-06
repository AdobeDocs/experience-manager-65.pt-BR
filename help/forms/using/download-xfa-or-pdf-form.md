---
title: Baixar um modelo de formulário XFA ou PDF
seo-title: Download an XFA or a PDF form template
description: Você pode exportar formulários do repositório para o sistema local e migrar os formulários baixados para o novo repositório.
seo-description: You can export forms from the repository to the local system and migrate the downloaded forms to new repository.
uuid: 5f7fbd14-cb9d-4749-8708-7efe49df89d7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 6699e0e7-fd42-41ae-86a2-3b940d905111
role: Admin
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Baixar um modelo de formulário XFA ou PDF {#download-an-xfa-or-a-pdf-form-template}

A operação de download, como o nome indica, permite exportar formulários do repositório para o sistema local. Em combinação com a operação de upload, essa operação ajuda a migrar os formulários de um repositório para outro.

No AEM Forms, a operação de download é compatível com os seguintes tipos de ativos:

* Modelos de formulário (Forms XFA)
* PDF forms
* Documentos (arquivos PDF simples)

O AEM Forms suporta o download desses tipos de formulário individualmente ou em uma pasta que contenha um ou mais formulários compatíveis.

Além desses ativos, você pode baixar a variável `Resource` tipo de ativo se ele estiver presente em uma pasta. Essa funcionalidade é fornecida para permitir o download do recurso mencionado por um formulário XFA junto com o formulário.

## Baixar um ou mais formulários {#download-one-or-more-forms}

1. Faça logon na interface do usuário do AEM Forms em `https://<server>:<port>/aem/forms.html`.

1. Navegue até o local do ativo que deseja baixar.

1. Selecione o ativo. Clique no botão **[!UICONTROL Baixar]** ![aem6forms_download](assets/aem6forms_download.png) na barra de ferramentas.

   >[!NOTE]
   >
   >Você pode selecionar apenas um formulário para download. Para baixar vários formulários, é necessário baixá-los como uma pasta.

1. Na caixa de diálogo exibida, clique em **[!UICONTROL Baixar]**.

   O AEM Forms gera um arquivo ZIP contendo o arquivo selecionado ou a pasta selecionada.

   Se você estiver baixando uma pasta, os ativos suportados dentro da pasta serão baixados na hierarquia existente.

   O arquivo ZIP é salvo no `Downloads` no seu sistema.

## Considerações relacionadas para a operação de upload {#related-considerations-for-the-upload-operation}

* Você pode fazer upload do arquivo ZIP para qualquer outro local no mesmo repositório ou em outro
* A hierarquia dos ativos em uma pasta é retida durante a operação de upload
* Quaisquer alterações de metadados feitas nos ativos baixados antes do download são refletidas no upload
