---
title: Envio de uma confirmação de envio de formulário por email
seo-title: Sending a form submission acknowledgement via email
description: O AEM Forms permite configurar a ação de envio de email que envia uma confirmação a um usuário ao enviar o formulário.
seo-description: AEM Forms allows you to configure the email submit action that sends an acknowledgement to a user on submitting the form.
uuid: c80b1ef4-8fe3-48e0-8fc6-3032dc022a38
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 574de3d5-69ba-4e2f-a8ab-c59f357e4386
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Envio de uma confirmação de envio de formulário por email {#sending-a-form-submission-acknowledgement-via-email}

## Envio de dados do formulário adaptável {#adaptive-form-data-submission}

Formulários adaptáveis oferecem vários recursos prontos para uso [enviar ações](../../forms/using/configuring-submit-actions.md) fluxos de trabalho para enviar os dados do formulário para diferentes pontos de extremidade.

Por exemplo, a variável **[!UICONTROL Enviar email]** enviar ação envia um email após o envio bem-sucedido de um formulário adaptável. Ele também pode ser configurado para enviar os dados do formulário e o PDF no email.

Este artigo detalha as etapas para habilitar a ação Email em um formulário adaptável e diferentes configurações fornecidas.

>[!NOTE]
>
>Também é possível usar a variável **[!UICONTROL Enviar PDF por email]** para enviar o formulário preenchido por email como anexo de PDF. As opções de configuração disponíveis para essa ação são as mesmas opções disponíveis para a variável **[!UICONTROL Enviar email]** ação. A ação PDF de email está disponível somente para formulários adaptáveis baseados em XFA

## Enviar ação por email {#email-action}

A ação Send email permite que um autor envie emails automaticamente para um ou mais recipients no envio bem-sucedido de um formulário adaptável.

>[!NOTE]
>
>Para usar a ação Enviar email, você precisa configurar o serviço de email AEM conforme descrito em [Configuração do serviço de email](/help/sites-administering/notification.md#configuring-the-mail-service).

### Ativar a ação Enviar email em um formulário adaptável {#enabling-email-action-on-an-adaptive-form}

1. Abra um formulário adaptável em **[!UICONTROL editar]** modo.

1. No **[!UICONTROL Conteúdo]** guia , toque em **[!UICONTROL Contêiner de formulário]** e tocar ![configure](assets/configure-icon.svg) para exibir as propriedades do formulário adaptável.

1. No **[!UICONTROL Submissão]** seção , selecione **[!UICONTROL Enviar email]** do **[!UICONTROL Enviar ação]** lista suspensa.

   ![Enviar ações](assets/submission-actions.png)

1. Especifique IDs de email válidas no **[!UICONTROL Para]**, **[!UICONTROL CC]** e **[!UICONTROL CCO]** campos.

   Especifique o assunto e o corpo do email no **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de email]** , respectivamente.

   Também é possível especificar espaços reservados variáveis nos campos, nesse caso, os valores dos campos são processados quando o formulário é enviado com êxito por um usuário final. Para obter mais informações, consulte [Uso de nomes de campos de formulário adaptáveis para criar conteúdo de email dinamicamente](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Selecionar **[!UICONTROL Incluir anexos]** se o formulário incluir anexos de arquivo e você desejar anexar esses arquivos no email.

   >[!NOTE]
   >
   >Se você escolher a variável **[!UICONTROL Enviar PDF via Email]** é necessário selecionar a opção Include attachment .

1. Clique em ![salvar](assets/save_icon.svg) para salvar as alterações.

### Uso de nomes de campos de formulário adaptáveis para criar conteúdo de email dinamicamente {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Os nomes de campo em um formulário adaptável são chamados de espaços reservados que são substituídos pelo valor desse campo depois que um usuário envia o formulário.

No **[!UICONTROL Enviar email]** , é possível usar espaços reservados que são processados quando a ação é executada. Isso implica que os cabeçalhos do email (como **[!UICONTROL Para]**, **[!UICONTROL CC]**, **[!UICONTROL CCO]**, **[!UICONTROL Assunto]**) são geradas quando o usuário envia o formulário.

Para definir um espaço reservado, especifique `${<field name>}` em um campo depois de selecionar **[!UICONTROL Enviar email]** como Ação de envio.

Por exemplo, se o formulário contiver a variável **[!UICONTROL Endereço de email]** campo, nome `email_addr`, para capturar a ID do email de um usuário, é possível especificar o seguinte na variável **[!UICONTROL Para]**, **[!UICONTROL CC]** ou **[!UICONTROL CCO]** campos.

`${email_addr}`

Quando um usuário envia o formulário, um email é enviado para a ID de email inserida na variável `email_addr` do formulário.

>[!NOTE]
>
>Você pode encontrar o nome de um campo na variável **[!UICONTROL Editar]** para o campo.

Os marcadores de posição de variável também podem ser usados na variável **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de email]** campos.

Por exemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Os campos em painéis repetíveis não podem ser usados como espaços reservados variáveis.
