---
title: Ativação de anexos para um formulário HTML5
seo-title: Enabling attachments for an HTML5 form
description: Por padrão, o suporte de anexo para formulários HTML5 está desativado.
seo-description: By default, the attachment support for HTML5 forms is disabled.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
exl-id: 68912260-179a-4d1b-b944-0a1777c021ac
source-git-commit: 6e2a0f053a1f6989524e9ae2b1dcb001b0397ac6
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# Ativação de anexos para um formulário HTML5 {#enabling-attachments-for-an-html-form}

Você pode carregar, visualizar e enviar anexos com formulários HTML5. Por padrão, o suporte ao anexo é desativado. Para ativar o suporte ao anexo:

1. Crie um [perfil personalizado](/help/forms/using/custom-profile.md) com um `mfAttachmentOptions` propriedade de string de seleção múltipla. Cada string na variável `mfAttachmentOptions` deve ter uma `property=value` formato para configurar as opções do widget anexo de arquivo. O `property` e `value` pode ter qualquer um dos seguintes valores:

   | Propriedade | Valor |
   |--- |---|
   | multiSelect | true ou false (true por padrão) |
   | fileSizeLimit | Número em MBs (2 MBs por padrão). Por exemplo, 5. |
   | buttonText | Texto do botão para a janela pop-up (&quot;Anexar&quot; por padrão) |
   | Aceitar | lista de tipos de arquivos separados por vírgulas a serem aceitos (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; por padrão) |

   Por exemplo:

   ![configurar opções](assets/mfAttachmentOptions.png)

   Conforme necessário, também é possível especificar mais opções personalizadas para a variável `mfAttachmentOptions` propriedade.

   >[!NOTE]
   >
   >No Microsoft Internet Explorer 9, os usuários podem anexar arquivos maiores que o limite especificado. É um problema conhecido.

1. Use o [editor de metadados](/help/forms/using/manage-form-metadata.md) para selecionar o perfil personalizado criado acima para formulários HTML 5.
1. Renderize seu modelo de formulário com um perfil personalizado e o ícone de anexos apareceria na barra de ferramentas de formulários.

   >[!NOTE]
   >
   >Pronto para uso, o portal de formulários fornece um perfil personalizado com recursos de rascunhos e anexos ativados. Para obter mais informações sobre o **Salvar como rascunho** perfil, consulte [Salvar formulários HTML5 como rascunho](/help/forms/using/saving-html5-form-draft.md).

1. Clique no ícone de anexo e uma caixa de diálogo de seleção de anexo será exibida. Navegue e selecione o anexo e clique em **Anexar**.

   >[!NOTE]
   >
   >Para visualizar um anexo, clique no nome do anexo.

   >[!NOTE]
   >
   >A opção de visualização de arquivo não está disponível para usuários anônimos.

## Formato de envio do anexo {#attachment-submission-format}

Quando os anexos são ativados, o formulário HTML5 envia dados de várias partes. Os dados de envio de várias partes têm duas partes **dataXml** e **anexos**.

>[!NOTE]
>
>Para compatibilidade com versões anteriores, se `mfAllowAttachments` estiver desativada, os formulários HTML5 não enviarão os dados de várias partes. Ele envia dados xml simples em **application/xml** formato.

Se o sinalizador mfAllowAttachments estiver ativado, a variável [enviar serviço proxy de serviço](/help/forms/using/service-proxy.md) também publica dados de várias partes com dataXml e anexos.
