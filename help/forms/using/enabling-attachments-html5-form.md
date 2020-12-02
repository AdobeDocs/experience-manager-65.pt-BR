---
title: Ativação de anexos para um formulário HTML5
seo-title: Ativação de anexos para um formulário HTML5
description: Por padrão, o suporte ao anexo para formulários HTML5 está desativado.
seo-description: Por padrão, o suporte ao anexo para formulários HTML5 está desativado.
uuid: 2c62ac3e-4b27-46c7-a61d-a805fb5d26fb
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 8eebfcd6-0597-44ed-b718-bf9a1baa6c12
translation-type: tm+mt
source-git-commit: 00e14be8a0775149b3ee7ce8cd781dd7f1e49e4f
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Habilitar anexos para um formulário HTML5 {#enabling-attachments-for-an-html-form}

Você pode carregar, pré-visualização e enviar anexos com formulários HTML5. Por padrão, o suporte ao anexo é desativado. Para ativar o suporte ao anexo:

1. Crie um [perfil personalizado](/help/forms/using/custom-profile.md) com a propriedade de sequência de caracteres multiselect `mfAttachmentOptions`.
1. No perfil personalizado, especifique as propriedades `fileSizeLimit`, `multiSelect` e `buttonTex`t para configurar as opções do widget de anexo de arquivo. Conforme necessário, também é possível especificar mais propriedades personalizadas.

1. No perfil personalizado, use as seguintes configurações:

   * **multiSelect** -> true ou false (true por padrão)
   * **fileSizeLimit** -> value_in_mb (digamos 5) (2 MBs por padrão)
   * **buttonText** -> Texto do botão para janela pop-up (&quot;Anexar&quot; por padrão)
   * **aceitar** -> tipos de arquivo para aceitar (&quot;audio/&amp;ast;, video/&amp;ast;, image/&amp;ast;, text/&amp;ast;, .pdf&quot; por padrão)

   >[!NOTE]
   >
   >No Microsoft Internet Explorer 9, os usuários podem anexar arquivos maiores que o limite especificado. É um problema conhecido.

1. Use o [editor de metadados](/help/forms/using/manage-form-metadata.md) para selecionar o perfil personalizado criado acima para formulários HTML 5.
1. Renderize seu modelo de formulário com perfil personalizado e o ícone de anexos aparecerá na barra de ferramentas de formulários.

   >[!NOTE]
   >
   >O portal de formulários fornece um perfil personalizado com recursos de rascunhos e anexos ativados. Para obter mais informações sobre o perfil **Salvar como rascunho**, consulte [Salvar formulários HTML5 como rascunho](/help/forms/using/saving-html5-form-draft.md).

1. Clique no ícone de anexo e uma caixa de diálogo de seleção de anexo será exibida. Procure e selecione o anexo e clique em **Anexar**.

   >[!NOTE]
   >
   >Para pré-visualização um anexo, clique no nome do anexo.

   >[!NOTE]
   >
   >A opção pré-visualização de arquivo não está disponível para usuários anônimos.

## Formato de envio do anexo {#attachment-submission-format}

Quando os anexos estão ativados, o formulário HTML5 envia dados de várias partes. Os dados de envio de várias partes têm duas partes **dataXml** e **anexos**.

>[!NOTE]
>
>Para compatibilidade com versões anteriores, se a opção `mfAllowAttachments` estiver desativada, os formulários HTML5 não enviarão os dados de várias partes. Ele envia um xml de dados simples no formato **application/xml**.

Se o sinalizador mfAllowAttachments estiver ativado, o [serviço de proxy de serviço de envio](/help/forms/using/service-proxy.md) também postará dados de várias partes com dataXml e anexos.
