---
title: Salvamento de um formulário HTML5 como rascunho
description: Salve um formulário do HTML5 como rascunho e retome o preenchimento do formulário em um estágio posterior.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 445e24af-cd1a-414d-bd01-9feb6631bbef
feature: HTML5 Forms,Mobile Forms
exl-id: a9879445-d626-4279-8a95-a9009294b483
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 5%
---
# Salvamento de um formulário HTML5 como rascunho {#saving-an-html-form-as-a-draft}

Você pode salvar um formulário HTML5 como rascunho e retomar o preenchimento do formulário em um estágio posterior. O Forms Portal permite que qualquer usuário salve e restaure um formulário do HTML5. Para ativar a funcionalidade Salvar como rascunho, adicione as seguintes configurações ao nó do perfil:

## Perfil personalizado para permitir o recurso Salvar como rascunho {#custom-profile-to-allow-save-as-draft-feature}

Por padrão, a AEM Forms fornece um perfil **Salvar como rascunho**. Você pode renderizar um formulário com o perfil Salvar como rascunho para ativar a funcionalidade de rascunho para um formulário do HTML5. Você pode especificar o perfil de renderização do HTML para um formulário no [Forms Manager](/help/forms/using/introduction-managing-forms.md).

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

Por padrão, o AEM Forms armazena os dados do usuário associados ao rascunho e ao envio de um formulário no nó /content/forms/fp na instância de Publicação. Você pode adicionar seu provedor de armazenamento personalizado. Para obter detalhes, consulte [Armazenamento personalizado para componentes de Rascunhos e Envios](/help/forms/using/adding-custom-storage-provider-forms.md).
