---
title: Envio de uma confirmação de envio de formulário por email
description: O AEM Forms permite configurar a ação de envio de email que envia uma confirmação para um usuário sobre o envio do formulário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: bca4044a-18a9-4b97-92de-eff1e9a840f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Envio de uma confirmação de envio de formulário por email {#sending-a-form-submission-acknowledgement-via-email}

## Envio de dados do formulário adaptável {#adaptive-form-data-submission}

Os formulários adaptáveis fornecem vários fluxos de trabalho de [ações de envio](../../forms/using/configuring-submit-actions.md) prontos para uso para enviar os dados do formulário para diferentes pontos de extremidade.

Por exemplo, a ação de envio **[!UICONTROL Enviar email]** envia um email após o envio bem-sucedido de um formulário adaptável. Ele também pode ser configurado para enviar os dados do formulário e o PDF no email.

Este artigo detalha as etapas para ativar a ação de Email em um formulário adaptável e as diferentes configurações que ele fornece.

>[!NOTE]
>
>Você também pode usar a opção **[!UICONTROL Enviar PDF por email]** para enviar o formulário preenchido por email como um anexo de PDF. As opções de configuração disponíveis para esta ação são iguais às opções disponíveis para a ação **[!UICONTROL Enviar email]**. A ação PDF de email está disponível somente para formulários adaptáveis baseados em XFA

## Enviar ação de email {#email-action}

A ação Enviar email permite que um autor envie emails automaticamente para um ou mais recipients no envio bem-sucedido de um formulário adaptável.

>[!NOTE]
>
>Para usar a ação Enviar email, você precisa configurar o serviço de email AEM conforme descrito em [Configurando o serviço de email](/help/sites-administering/notification.md#configuring-the-mail-service).

### Ativação da ação Enviar email em um formulário adaptável {#enabling-email-action-on-an-adaptive-form}

1. Abra um formulário adaptável no modo **[!UICONTROL editar]**.

1. Na guia **[!UICONTROL Conteúdo]**, selecione **[!UICONTROL Contêiner de Formulário]** e selecione ![configurar](assets/configure-icon.svg) para exibir as propriedades do formulário adaptável.

1. Na seção **[!UICONTROL Envio]**, selecione **[!UICONTROL Enviar email]** na lista suspensa **[!UICONTROL Ação de envio]**.

   ![Enviar ações](assets/submission-actions.png)

1. Especifique IDs de email válidas nos campos **[!UICONTROL Para]**, **[!UICONTROL CC]** e **[!UICONTROL Cco]**.

   Especifique o assunto e o corpo do email nos campos **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de email]**, respectivamente.

   Também é possível especificar espaços reservados para variáveis nos campos, nesse caso, os valores dos campos são processados quando o formulário é enviado com êxito por um usuário final. Para obter mais informações, consulte [Usar nomes de campos de formulário adaptáveis para criar conteúdo de email dinamicamente](../../forms/using/form-submission-receipt-via-email.md#p-using-adaptive-form-field-names-to-dynamically-create-email-content-p).

   Selecione **[!UICONTROL Incluir anexos]** se o formulário incluir anexos de arquivo e você quiser anexar esses arquivos no email.

   >[!NOTE]
   >
   >Se você escolher a opção **[!UICONTROL Enviar PDF por email]**, deverá selecionar a opção Incluir anexos.

1. Clique em ![salvar](assets/save_icon.svg) para salvar as alterações.

### Utilização de nomes de campos de formulário adaptáveis para criar dinamicamente conteúdo de email {#using-adaptive-form-field-names-to-dynamically-create-email-content}

Os nomes de campo em um formulário adaptável são chamados de espaços reservados que são substituídos pelo valor desse campo depois que um usuário envia o formulário.

Na ação **[!UICONTROL Enviar email]**, você pode usar espaços reservados que são processados quando a ação é executada. Isso implica que os cabeçalhos do email (como **[!UICONTROL To]**, **[!UICONTROL CC]**, **[!UICONTROL BCC]**, **[!UICONTROL Subject]**) são gerados quando o usuário envia o formulário.

Para definir um espaço reservado, especifique `${<field name>}` em um campo depois de selecionar **[!UICONTROL Enviar email]** como a Ação de Envio.

Por exemplo, se o formulário contiver o campo **[!UICONTROL Endereço de email]**, denominado `email_addr`, para capturar a ID de email de um usuário, você poderá especificar o seguinte nos campos **[!UICONTROL Para]**, **[!UICONTROL CC]** ou **[!UICONTROL BCC]**.

`${email_addr}`

Quando um usuário envia o formulário, um email é enviado para a ID de email inserida no campo `email_addr` do formulário.

>[!NOTE]
>
>Você pode encontrar o nome de um campo na caixa de diálogo **[!UICONTROL Editar]** para o campo.

Os espaços reservados para variáveis também podem ser usados nos campos **[!UICONTROL Assunto]** e **[!UICONTROL Modelo de email]**.

Por exemplo:

`Hi ${first_name} ${last_name},`

`Your form has been received by our department. It usually takes ten business days to process the request.`

`Regards`

`Administrator`

>[!NOTE]
>
>Os campos em painéis repetíveis não podem ser usados como espaços reservados para variáveis.
