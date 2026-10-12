---
title: Modelo de formulário de renderização para formulários HTML5
description: Os perfis de formulários do HTML5 estão associados às renderizações de perfil. Os Renderizadores de perfil são páginas JSP responsáveis por gerar a representação HTML do formulário chamando o serviço OSGi da Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: HTML5 Forms,Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
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
source-wordcount: '543'
ht-degree: 1%
---
# Modelo de formulário de renderização para formulários HTML5 {#rendering-form-template-for-html-forms}

## Renderizar Ponto de Extremidade {#render-endpoint}

Os formulários HTML5 têm a noção de **Perfis** que são expostos como pontos de extremidade REST para habilitar a Renderização Móvel de Modelos de Formulário. Estes perfis associaram o **Renderizador de Perfil**. Elas são páginas JSP responsáveis por gerar a representação do formulário no HTML, chamando o serviço OSGi do Forms. O caminho JCR do nó de Perfil determina o URL do ponto final de renderização. O ponto final de renderização padrão do formulário apontando para o perfil &#39;padrão&#39; é semelhante a:

https://<*host*>:<*porta*>/content/xfaforms/profiles/default.html?contentRoot=<*caminho da pasta que contém o formulário xdp*>&template=<*nome do xdp*>

Por exemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Para um perfil personalizado, o endpoint é alterado de acordo. Por exemplo, o ponto final do perfil personalizado com o nome hrforms é:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se o modelo residir no repositório do AEM em um aplicativo chamado FormSubmission, o URI será:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parâmetros de renderização {#render-parameters}

Os parâmetros de solicitação compatíveis ao renderizar o formulário como HTML são:

<table>
 <tbody>
  <tr>
   <th><strong>Parâmetro </strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>modelo<br /> </td>
   <td>Este parâmetro especifica o nome do arquivo de modelo.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Esse parâmetro especifica o caminho onde o modelo e os recursos associados residem. Este caminho pode ser o caminho do sistema de arquivos do servidor ou um caminho de repositório ou um caminho http ou ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Esse parâmetro especifica a url para a qual o xml de dados de formulário é postado.<br /> </td>
  </tr>
 </tbody>
</table>

### Mesclar dados com o modelo de formulário {#merge-data-with-form-template}

| Parâmetro | Descrição |
|---|---|
| dataRef | Este parâmetro especifica o **caminho absoluto** do arquivo de dados mesclado com o modelo. Esse parâmetro pode ser um URL para um serviço rest que retorna os dados no formato xml. |
| dados | Esse parâmetro especifica os bytes de dados codificados em UTF-8 que são mesclados com o modelo. Se esse parâmetro for especificado, o formulário HTML5 ignorará o parâmetro dataRef. |

### Passagem do parâmetro de renderização {#passing-the-render-parameter}

Os formulários HTML5 suportam três métodos para transmitir os parâmetros de renderização. Você pode enviar parâmetros por meio de URLs, pares de valores chave e nó de perfil. No parâmetro de renderização, o par de valor-chave tem a precedência mais alta seguida pelo nó do perfil. O parâmetro de solicitação de URL tem menos precedência.

* **Parâmetros de solicitação de URL**: você pode especificar os parâmetros de renderização na URL. Nos parâmetros de solicitação de URL, os parâmetros estão visíveis para o usuário final. Por exemplo, a URL de envio a seguir contém um parâmetro de modelo na URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parâmetros de solicitação SetAttribute**: você pode especificar os parâmetros de renderização como um par de valores chave. Nos parâmetros de solicitação SetAttribute, os parâmetros não estão visíveis para o usuário final. Você pode encaminhar uma solicitação de qualquer outro JSP para o JSP do renderizador de perfil de formulário do HTML5 e usar *setAttribute* no objeto de solicitação para passar todos os parâmetros de renderização. Esse método tem a maior precedência.

* **Parâmetros de solicitação de nó de perfil:** Você pode especificar os parâmetros de renderização como propriedades de nó de um nó de perfil. Nos parâmetros de solicitação do nó de perfil, os parâmetros não estão visíveis para o usuário final. O nó de perfil é o nó para onde a solicitação é enviada. Para especificar parâmetros como propriedades de nó, use o CRXDE lite.

### Enviar parâmetros {#submit-parameters}

Os formulários HTML5 enviam dados; executam scripts do lado do servidor e serviços da Web nos servidores da AEM. Para obter informações detalhadas sobre os parâmetros usados para executar scripts do lado do servidor e serviços da Web em servidores AEM, consulte [Proxy do HTML5 Forms Service](/help/forms/using/service-proxy.md).
