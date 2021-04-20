---
title: Ativação de anexos para um formulário HTML5
seo-title: Ativação de anexos para um formulário HTML5
description: Por padrão, o suporte de anexo para formulários HTML5 é desativado.
seo-description: Por padrão, o suporte de anexo para formulários HTML5 é desativado.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---


# Ativação de anexos para um formulário HTML5 {#enabling-attachments-for-an-html-form}

Você pode carregar, visualizar e enviar anexos com formulários HTML5. Por padrão, o suporte ao anexo é desativado. Para ativar o suporte ao anexo:

1. Crie um [perfil personalizado](/help/forms/using/custom-profile.md) com a propriedade de sequência de caracteres de várias seleções `mfAttachmentOptions`.
1. No perfil personalizado, especifique as propriedades `fileSizeLimit`, `multiSelect` e `buttonTex`t para configurar as opções do widget de anexo de arquivo. Conforme necessário, também é possível especificar mais propriedades personalizadas.

1. No perfil personalizado, use as seguintes configurações:

   * **multiSelect** -> true ou false (true por padrão)
   * **fileSizeLimit**  -> value_in_mb (digamos 5) (2 MBs por padrão)
   * **buttonText**  -> Texto do botão para janela pop-up (&quot;Anexar&quot; por padrão)
   * **aceitar** -> tipos de arquivo a serem aceitos (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; por padrão)

   >[!NOTE]
   >
   >No Microsoft Internet Explorer 9, os usuários podem anexar arquivos maiores que o limite especificado. É um problema conhecido.

1. Use o [editor de metadados](/help/forms/using/manage-form-metadata.md) para selecionar o perfil personalizado que você criou acima para formulários HTML 5.
1. Renderize seu modelo de formulário com um perfil personalizado e o ícone de anexos apareceria na barra de ferramentas de formulários.

   >[!NOTE]
   >
   >Pronto para uso, o portal de formulários fornece um perfil personalizado com recursos de rascunhos e anexos ativados. Para obter mais informações sobre o perfil **Salvar como rascunho**, consulte [Salvar formulários HTML5 como rascunho](/help/forms/using/saving-html5-form-draft.md).

1. Clique no ícone de anexo e uma caixa de diálogo de seleção de anexo será exibida. Navegue e selecione o anexo e clique em **Attach**.

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
>Para compatibilidade com versões anteriores, se a opção `mfAllowAttachments` estiver desativada, os formulários HTML5 não enviarão os dados de várias partes. Ele envia dados xml simples no formato **application/xml**.

Se o sinalizador mfAllowAttachments estiver ativado, o [serviço de proxy de serviço de envio](/help/forms/using/service-proxy.md) também publica dados multipart com dataXml e anexos.
