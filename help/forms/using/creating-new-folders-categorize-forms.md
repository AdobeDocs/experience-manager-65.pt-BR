---
title: Criar novas pastas para categorizar formulários
description: Use pastas para organizar modelos de formulário, PDF, recursos e formulários adaptáveis.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
role: Admin,User
exl-id: f8af1ac3-6a95-4f91-8979-6b41a7e02ca4
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Criar novas pastas para categorizar formulários {#create-new-folders-to-categorize-forms}

Você pode organizar melhor seus ativos usando pastas. Como o AEM Forms é compatível com vários tipos de ativos — modelos de formulário, PDF, documentos, recursos e formulários adaptáveis, com vários metadados — você pode usar pastas para categorizar seus formulários com base nos critérios desejados.

O AEM Forms permite alterar o título de uma pasta. O título não é o mesmo que o nome do nó em que a pasta está armazenada no repositório. Em vez disso, o título é mantido como metadados para a pasta. Se você alterar o título de uma pasta, o caminho de qualquer ativo presente na pasta não será afetado.

## Criar uma pasta {#create-a-folder}

Você pode criar uma pasta no AEM Forms de uma das seguintes maneiras:

* Faça upload de um arquivo ZIP contendo ativos na estrutura de pastas desejada (Consulte [Obtenção de documentos XDP e PDF no AEM Forms](/help/forms/using/get-xdp-pdf-documents-aem.md))

* Criar uma pasta vazia

1. Faça logon na interface do usuário do AEM Forms em `https://<server>:<port>/aem/forms.html`.
1. Navegue até o local em que deseja criar uma pasta.
1. Clique em ![aem6forms_add](assets/aem6forms_add.png) na barra de ferramentas e selecione **[!UICONTROL Criar pasta]**.

1. Insira os seguintes detalhes:

   * **Título:** Nome de exibição da pasta
   * **Nome:** *(Obrigatório)* O nome do nó sob o qual você deseja armazenar a pasta no repositório

   >[!NOTE]
   >
   >Por padrão, o valor do campo de nome é preenchido automaticamente a partir do título. O nome só pode conter caracteres alfanuméricos ou os caracteres especiais de hífen (-) e sublinhado (_). Quaisquer outros caracteres especiais inseridos no título são substituídos automaticamente por um hífen e você será solicitado a confirmar o novo nome. Você pode optar por continuar com o nome sugerido ou fazer mais edições.

1. Clique em **[!UICONTROL Enviar].**

   Uma nova pasta com o título definido é exibida no local atual na lista de ativos.

   Se existir uma pasta com o nome especificado, o envio falha com um erro. Você pode exibir a mensagem de erro passando o cursor do mouse sobre ele ![aem6forms_error_alert](assets/aem6forms_error_alert.png) ícone que aparece ao lado do campo de nome.

### Editar o título da pasta {#edit-the-folder-title-br}

1. Selecione a pasta cujo título deseja editar.
1. Clique no botão de edição ![aem6forms_edit](assets/aem6forms_edit.png) na barra de ferramentas.
1. Insira o novo título. O campo de texto é pré-preenchido com o valor atual do título da pasta. Você pode alterá-lo para um novo valor.
1. Clique em **[!UICONTROL Enviar].**
