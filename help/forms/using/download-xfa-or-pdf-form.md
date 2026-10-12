---
title: Baixar um XFA ou um modelo de formulário do PDF
description: É possível exportar formulários do repositório para o sistema local e migrar os formulários baixados para um novo repositório.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: 5b7b9816-38c1-4780-b1fc-8184971f3772
solution: Experience Manager, Experience Manager Forms
feature: Interactive Communication
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: aa28c6c8-3ede-445b-a351-eeb0c9f9aec4
    internal-label: Interactive Communication
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%
---
# Baixar um XFA ou um modelo de formulário do PDF {#download-an-xfa-or-a-pdf-form-template}

A operação de download, como o nome indica, permite exportar formulários do repositório para o sistema local. Em combinação com a operação de upload, essa operação ajuda a migrar seus formulários de um repositório para outro.

No AEM Forms, a operação de download é compatível com os seguintes tipos de ativos:

* Modelos de formulário (XFA Forms)
* PDF forms
* Documentos (arquivos simples do PDF)

O AEM Forms permite o download desses tipos de formulário individualmente ou em uma pasta que contenha um ou mais formulários compatíveis.

Além desses ativos, você pode baixar o tipo de ativo `Resource` se ele estiver presente em uma pasta. Essa funcionalidade é fornecida para permitir que você baixe o recurso referido por um formulário XFA junto com o formulário.

## Baixar um ou mais formulários {#download-one-or-more-forms}

1. Faça logon na interface do usuário do AEM Forms em `https://<server>:<port>/aem/forms.html`.

1. Navegue até o local do ativo que deseja baixar.

1. Selecione o ativo. Clique no ícone **[!UICONTROL Download]** ![aem6forms_download](assets/aem6forms_download.png) na barra de ferramentas.

   >[!NOTE]
   >
   >Você pode selecionar apenas um formulário para download. Para baixar vários formulários, é necessário baixá-los como uma pasta.

1. Na caixa de diálogo exibida, clique em **[!UICONTROL Baixar]**.

   O AEM Forms gera um arquivo ZIP contendo o arquivo selecionado ou a pasta selecionada.

   Se você estiver baixando uma pasta, os ativos compatíveis dentro da pasta serão baixados em sua hierarquia existente.

   O arquivo ZIP foi salvo na pasta `Downloads` do sistema.

## Considerações relacionadas para a operação de upload {#related-considerations-for-the-upload-operation}

* Você pode fazer upload do arquivo ZIP para qualquer outro local no mesmo repositório ou em outro repositório
* A hierarquia dos ativos em uma pasta é retida durante a operação de upload
* Todas as alterações de metadados feitas nos ativos baixados antes do download são refletidas no upload
