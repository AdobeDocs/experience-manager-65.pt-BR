---
title: Salvamento de um formulário HTML 5 como rascunho
description: Salve um formulário HTML5 como rascunho e retome o preenchimento do formulário em um estágio posterior.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 5%

---

# Salvamento de um formulário HTML 5 como rascunho {#saving-an-html-form-as-a-draft}

Você pode salvar um formulário HTML5 como rascunho e retomar o preenchimento do formulário em um estágio posterior. O Forms Portal permite que qualquer usuário salve e restaure um formulário HTML5. Para ativar a funcionalidade Salvar como rascunho, adicione as seguintes configurações ao nó do perfil:

## Perfil personalizado para permitir o recurso Salvar como rascunho {#custom-profile-to-allow-save-as-draft-feature}

Por padrão, a AEM Forms fornece um perfil **Salvar como rascunho**. Você pode renderizar um formulário com o perfil Salvar como rascunho para ativar a funcionalidade de rascunho para um formulário HTML5. Você pode especificar o perfil de renderização de HTML para um formulário no [Forms Manager](/help/forms/using/introduction-managing-forms.md).

Para habilitar a funcionalidade Salvar como Rascunho para o seu [perfil personalizado](/help/forms/using/custom-profile.md) existente, adicione as seguintes propriedades ao nó de perfil personalizado:

<table>
 <tbody>
  <tr>
   <td><strong>Nome de propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>mfAllowFPDdraft</td>
   <td>String</td>
   <td>verdadeiro</td>
   <td><p>Habilita o recurso salvar como rascunho</p> <p>para este perfil.</p> </td>
  </tr>
  <tr>
   <td>mfAllowAttachments</td>
   <td>String</td>
   <td>verdadeiro</td>
   <td><p>Permite o upload de anexos</p> <p>com este perfil.</p> </td>
  </tr>
 </tbody>
</table>

## Armazenamento de rascunhos e listagem {#drafts-storage-and-listing}

Depois de habilitar a funcionalidade Salvar como Rascunho para um formulário; quando o formulário é salvo, ele é listado no [componente Rascunhos e Envio](/help/forms/using/draft-submission-component.md). Você pode recuperar e começar a preencher o formulário salvo no componente de Rascunho e Envio.

Para ativar a listagem de formulários para o componente Rascunho e Envio, adicione a seguinte propriedade ao nó do perfil:

<table>
 <tbody>
  <tr>
   <td><strong>Nome de propriedade</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>fp.enablePortalSubmit</td>
   <td>String</td>
   <td>verdadeiro</td>
   <td>Para permitir que rascunhos e formulários sejam listados no <br /> Componente Rascunhos e Envios do Forms Portal após o envio</td>
  </tr>
 </tbody>
</table>

Por padrão, o AEM Forms armazena os dados do usuário associados ao rascunho e ao envio de um formulário no nó /content/forms/fp na instância do Publish. Você pode adicionar seu provedor de armazenamento personalizado. Para obter detalhes, consulte [Armazenamento personalizado para componentes de Rascunhos e Envios](/help/forms/using/adding-custom-storage-provider-forms.md).
