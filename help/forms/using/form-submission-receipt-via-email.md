---
title: Envio de uma confirmação de envio de formulário por email
seo-title: Sending a form submission acknowledgement via email
description: O AEM Forms permite configurar a ação de envio de email que envia uma confirmação para um usuário sobre o envio do formulário.
seo-description: AEM Forms lets you configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Envio de uma confirmação de envio de formulário por email {#sending-a-form-submission-acknowledgement-via-email}

## Envio de dados do formulário adaptável {#adaptive-form-data-submission}

Formulários adaptáveis fornecem vários formulários prontos para uso [enviar ações](../../forms/using/configuring-submit-actions.md) fluxos de trabalho para enviar os dados de formulário para diferentes endpoints.

Por exemplo, a variável **[!UICONTROL Enviar e-mail]** ação de envio envia um email ao enviar com êxito um formulário adaptável. Ele também pode ser configurado para enviar os dados do formulário e o PDF no email.

Este artigo detalha as etapas para ativar a ação de Email em um formulário adaptável e as diferentes configurações que ele fornece.

>[!NOTE]
>
>Você também pode usar a variável **[!UICONTROL Enviar PDF por e-mail]** opção para enviar o formulário preenchido por email como um anexo PDF. As opções de configuração disponíveis para esta ação são as mesmas que as opções disponíveis para a **[!UICONTROL Enviar e-mail]** ação. A ação PDF de email está disponível somente para formulários adaptáveis baseados em XFA

## Enviar ação de email {#email-action}

A ação Enviar email permite que um autor envie emails automaticamente para um ou mais recipients no envio bem-sucedido de um formulário adaptável.

>[!NOTE]
>
>Para usar a ação Enviar email, é necessário configurar o serviço de email AEM conforme descrito em [Configurando o serviço de e-mail](/help/sites-administering/notification.md#configuring-the-mail-service).

### Ativação da ação Enviar email em um formulário adaptável {#enabling-email-action-on-an-adaptive-form}

1. Abra um formulário adaptável no **[!UICONTROL editar]** modo.

1. No **[!UICONTROL Conteúdo]** selecione **[!UICONTROL Contêiner de formulário]** e selecione ![configurar](assets/configure-icon.svg) para exibir as propriedades do formulário adaptável.

1. No **[!UICONTROL Envio]** , selecione **[!UICONTROL Enviar e-mail]** do **[!UICONTROL Ação de envio]** lista suspensa.

   ![Enviar ações](assets/submission-actions.png)

1. Especifique IDs de email válidas no **[!UICONTROL Para]**, **[!UICONTROL CC]**, e **[!UICONTROL CCO]** campos.

   Especifique o assunto e o corpo do email no **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de e-mail]** campos, respectivamente.

   Também é possível especificar espaços reservados para variáveis nos campos, nesse caso, os valores dos campos são processados quando o formulário é enviado com êxito por um usuário final. Para obter mais informações, consulte [Utilização de nomes de campos de formulário adaptáveis para criar dinamicamente conteúdo de email](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Selecionar **[!UICONTROL Incluir anexos]** se o formulário incluir anexos de arquivo e você quiser anexar esses arquivos no email.

   >[!NOTE]
   >
   >Se você escolher a variável **[!UICONTROL Enviar PDF por e-mail]** você deve selecionar a opção Include attachments.

1. Clique em ![save](assets/save_icon.svg) para salvar as alterações.

### Utilização de nomes de campos de formulário adaptáveis para criar dinamicamente conteúdo de email {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Os nomes de campo em um formulário adaptável são chamados de espaços reservados que são substituídos pelo valor desse campo depois que um usuário envia o formulário.

No **[!UICONTROL Enviar e-mail]** , é possível usar espaços reservados que são processados quando a ação é executada. Isso implica que os cabeçalhos do email (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]**, **[!UICONTROL Assunto]**) são gerados quando o usuário envia o formulário.

Para definir um espaço reservado, especifique `${<field name>}` em um campo depois de selecionar **[!UICONTROL Enviar e-mail]** como a Ação enviar.

Por exemplo, se o formulário contiver a variável **[!UICONTROL Endereço de email]** campo, nomeado `email_addr`, para capturar a ID de email de um usuário, você pode especificar o seguinte na **[!UICONTROL Para]**, **[!UICONTROL CC]** ou **[!UICONTROL CCO]** campos.

`${email_addr}`

Quando um usuário envia o formulário, um email é enviado para a ID de email inserida na `email_addr` do formulário.

>[!NOTE]
>
>É possível encontrar o nome de um campo no **[!UICONTROL Editar]** para o campo.

Espaços reservados para variáveis também podem ser usados no **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de e-mail]** campos.

Por exemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Os campos em painéis repetíveis não podem ser usados como espaços reservados para variáveis.
