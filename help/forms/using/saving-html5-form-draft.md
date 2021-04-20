---
title: Salvar um formulário HTML5 como rascunho
seo-title: Salvar um formulário HTML5 como rascunho
description: Salve um formulário HTML5 como rascunho e retome o preenchimento do formulário em um estágio posterior.
seo-description: Salve um formulário HTML5 como rascunho e retome o preenchimento do formulário em um estágio posterior.
uuid: 70cd5f6f-f125-470c-8cee-ee14d2127713
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 5%

---


# Salvar um formulário HTML5 como rascunho {#saving-an-html-form-as-a-draft}

Você pode salvar um formulário HTML5 como rascunho e retomar o preenchimento do formulário posteriormente. O Forms Portal permite que qualquer usuário salve e restaure um formulário HTML5. Para ativar a funcionalidade Salvar como rascunho , adicione as seguintes configurações ao nó do perfil:

## Perfil personalizado para permitir o recurso Salvar como rascunho {#custom-profile-to-allow-save-as-draft-feature}

Imediatamente, o AEM Forms fornece um perfil **Salvar como rascunho**. É possível renderizar um formulário com o perfil Salvar como rascunho para ativar a funcionalidade de rascunho para um formulário HTML5. Você pode especificar o perfil de renderização HTML para um formulário no [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para ativar a funcionalidade Salvar como rascunho para seu [perfil personalizado](/help/forms/using/custom-profile.md) existente, adicione as seguintes propriedades ao nó de perfil personalizado:

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
   <td><p>Permite o upload de anexos</p> <p>com este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Rascunhos de armazenamento e listagem {#drafts-storage-and-listing}

Depois de ativar a funcionalidade Salvar como rascunho para um formulário; quando o formulário é salvo, ele é listado no [componente Rascunhos e Envio](/help/forms/using/draft-submission-component.md). Você pode recuperar e começar a preencher o formulário salvo no componente Rascunho e Envio .

Para ativar a listagem de formulários para o componente Rascunho e Envio , adicione a seguinte propriedade ao nó do perfil:

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
   <td>Para permitir que rascunhos e formulários sejam listados no componente <br /> Rascunhos e envios do Portal do Forms após o envio</td>
  </tr>
 </tbody>
</table>

Por padrão, o AEM Forms armazena os dados do usuário associados ao rascunho e ao envio de um formulário no nó /content/forms/fp na instância de publicação. Você pode adicionar seu provedor de armazenamento personalizado, para obter detalhes, consulte [Armazenamento personalizado para o componente Rascunhos e Envios](/help/forms/using/adding-custom-storage-provider-forms.md).
