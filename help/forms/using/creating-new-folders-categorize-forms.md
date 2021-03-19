---
title: Criar novas pastas para categorizar formulários
seo-title: Criar novas pastas para categorizar formulários
description: Use pastas para organizar modelos de formulário, PDFs, recursos e formulários adaptáveis.
seo-description: Use pastas para organizar modelos de formulário, PDFs, recursos e formulários adaptáveis.
uuid: 63fcb807-c9cf-49ae-ad69-6b1187543470
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
discoiquuid: 2a8f4380-8d0f-4354-b2da-4e0c02a545e3
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---


# Criar novas pastas para categorizar formulários {#create-new-folders-to-categorize-forms}

Você pode organizar seus ativos melhor usando pastas. Como o AEM Forms suporta vários tipos de ativos, como modelos de formulário, PDFs, documentos, recursos e formulários adaptáveis, com vários metadados, você pode usar pastas para categorizar seus formulários com base nos critérios desejados.

O AEM Forms permite alterar o título de uma pasta. O título não é o mesmo do nó sob o qual a pasta é armazenada no repositório. Em vez disso, o título é mantido como metadados para a pasta. Se você alterar o título de uma pasta, o caminho de qualquer ativo presente na pasta não será afetado.

## Crie uma pasta {#create-a-folder}

Você pode criar uma pasta no AEM Forms de uma das seguintes maneiras:

* Carregue um arquivo ZIP contendo ativos na estrutura de pastas desejada (Consulte [Obter documentos XDP e PDF no AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Criar uma nova pasta vazia

1. Faça logon na interface do usuário do AEM Forms em `https://<server>:<port>/aem/forms.html`.
1. Navegue até o local em que deseja criar uma pasta.
1. Clique no ícone ![aem6forms_add](assets/aem6forms_add.png) na barra de ferramentas e selecione **[!UICONTROL Criar pasta]**.

1. Insira os seguintes detalhes:

   * **Título:** Exibir nome da pasta
   * **Nome:** *(Obrigatório)* O nome do nó no qual você deseja armazenar a pasta no repositório

   >[!NOTE]
   >
   >Por padrão, o valor do campo de nome é preenchido automaticamente a partir do título. O nome só pode conter caracteres alfanuméricos ou os caracteres especiais de hífen (-) e sublinhado (_). Quaisquer outros caracteres especiais inseridos no título serão substituídos automaticamente por um hífen e você será solicitado a confirmar o novo nome. Você pode optar por continuar com o nome sugerido ou editá-lo ainda mais.

1. Clique em **[!UICONTROL Enviar].**

   Uma nova pasta com o título definido é exibida no local atual na lista de ativos.

   Se existir uma pasta com o nome especificado, o envio falhará com um erro. Você pode exibir a mensagem de erro passando o mouse sobre o ícone de erro ![aem6forms_error_alert](assets/aem6forms_error_alert.png) que aparece ao lado do campo de nome.

### Editar o título da pasta {#edit-the-folder-title-br}

1. Selecione a pasta cujo título você deseja editar.
1. Clique no ícone editar ![aem6forms_edit](assets/aem6forms_edit.png) na barra de ferramentas.
1. Insira o novo título. O campo de texto é pré-preenchido com o valor atual do título da pasta. Você pode alterá-lo para um novo valor.
1. Clique em **[!UICONTROL Enviar].**

