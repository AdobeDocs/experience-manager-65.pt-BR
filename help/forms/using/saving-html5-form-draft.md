---
title: Salvar um formulário HTML5 como rascunho
seo-title: Salvar um formulário HTML5 como rascunho
description: Salve um formulário HTML5 como rascunho e retome o preenchimento do formulário em uma etapa posterior.
seo-description: Salve um formulário HTML5 como rascunho e retome o preenchimento do formulário em uma etapa posterior.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%

---


# Salvar um formulário HTML5 como rascunho {#saving-an-html-form-as-a-draft}

É possível salvar um formulário HTML5 como rascunho e retomar o preenchimento do formulário em uma etapa posterior. O Forms Portal permite que qualquer usuário salve e restaure um formulário HTML5. Para ativar a funcionalidade Salvar como rascunho, adicione as seguintes configurações ao nó do perfil:

## Perfil personalizado para permitir o recurso Salvar como rascunho {#custom-profile-to-allow-save-as-draft-feature}

A AEM Forms fornece um perfil **Salvar como rascunho**. É possível renderizar um formulário com o perfil Salvar como rascunho para ativar a funcionalidade de rascunho para um formulário HTML5. Você pode especificar um perfil de renderização HTML para um formulário em [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar a funcionalidade Salvar como rascunho para o seu [perfil personalizado](/help/forms/using/custom-profile.md) existente, adicione as seguintes propriedades ao nó do perfil personalizado:

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDraft</td>
   <td>Sequência de caracteres</td>
   <td>verdadeiro</td>
   <td><p>Permite salvar como recurso de rascunho</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>Sequência de caracteres</td>
   <td>verdadeiro</td>
   <td><p>Permite o carregamento de anexos</p> <p>com este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Rascunhos de armazenamento e listagem {#drafts-storage-and-listing}

Depois de ativar a funcionalidade Salvar como rascunho para um formulário; quando o formulário é salvo, ele é listado no [componente Rascunhos e Envio](/help/forms/using/draft-submission-component.md). Você pode recuperar e preencher o start do formulário salvo no componente Rascunho e Envio.

Para ativar a listagem de formulários para o componente Rascunho e Envio, adicione a seguinte propriedade ao nó do perfil:

<table>
 <tbody>
  <tr>
   <td><strong>Nome da Propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>Sequência de caracteres</td>
   <td>verdadeiro</td>
   <td>Para permitir que rascunhos e formulários sejam listados no componente Rascunhos e envios do Forms Portal após o envio<br /></td>
  </tr>
 </tbody>
</table>

Por padrão, a AEM Forms armazena os dados do usuário associados ao rascunho e ao envio de um formulário no nó /content/forms/fp na instância Publicar. Você pode adicionar seu provedor de armazenamentos personalizado, para obter detalhes, consulte [armazenamento personalizado para o componente Rascunhos e Envios](/help/forms/using/adding-custom-storage-provider-forms.md).
