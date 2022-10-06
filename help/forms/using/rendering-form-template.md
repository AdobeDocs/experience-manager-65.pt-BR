---
title: Modelo de formulário de renderização para formulários HTML5
seo-title: Rendering form template for HTML5 forms
description: Os perfis de formulários HTML5 estão associados aos renderizadores de perfil. As Renderizações de perfil são páginas JSP responsáveis pela geração de representação de HTML do formulário, chamando o serviço OSGi da Forms.
seo-description: HTML5 forms profiles are associated with profile renders. Profile Renders are JSP pages responsible for generating HTML representation of the form by calling the Forms OSGi service.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
feature: Mobile Forms
exl-id: 022b9953-2d64-473f-87b7-aac1602f6a7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Modelo de formulário de renderização para formulários HTML5 {#rendering-form-template-for-html-forms}

## Endpoint de renderização {#render-endpoint}

As formas HTML5 têm a noção de **Perfis** que são expostos como Pontos de extremidade REST para permitir a renderização móvel de modelos de formulário. Esses perfis foram associados **Renderizador de perfil**. São páginas JSP responsáveis pela geração de representação HTML do formulário, chamando o serviço OSGi da Forms. O caminho JCR do nó Perfil determina o URL do ponto final de renderização. O ponto final de renderização padrão do formulário apontando para o perfil &quot;padrão&quot; tem a seguinte aparência:

https://&lt;*host*>:&lt;*porta*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*caminho da pasta que contém o formulário xdp*>&amp;template=&lt;*nome do xdp*>

Por exemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Para um perfil personalizado, o ponto de extremidade é alterado adequadamente. Por exemplo, o ponto final do perfil personalizado com o nome formas é:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se seu modelo reside no repositório AEM em um aplicativo chamado FormSubmission, o URI é:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parâmetros de renderização {#render-parameters}

Os parâmetros de solicitação compatíveis durante a renderização do formulário como HTML são:

<table>
 <tbody>
  <tr>
   <th><strong>Parâmetro </strong></th>
   <th><strong>Descrição</strong></th>
  </tr>
  <tr>
   <td>template<br /> </td>
   <td>Esse parâmetro especifica o nome do arquivo de modelo.<br /> </td>
  </tr>
  <tr>
   <td>contentRoot<br /> </td>
   <td>Esse parâmetro especifica o caminho onde o modelo e os recursos associados residem. Esse caminho pode ser o caminho do sistema de arquivos do servidor ou um caminho de repositório ou http ou um caminho ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Esse parâmetro especifica o url para o qual o xml de dados de formulário é publicado.<br /> </td>
  </tr>
 </tbody>
</table>

### Mesclar dados com modelo de formulário {#merge-data-with-form-template}

| Parâmetro | Descrição |
|---|---|
| dataRef | Esse parâmetro especifica **caminho absoluto** do arquivo de dados que é unido ao modelo. Esse parâmetro pode ser um URL para um serviço restante que retorna os dados no formato xml. |
| data | Esse parâmetro especifica os bytes de dados codificados UTF-8 que são mesclados com o modelo. Se esse parâmetro for especificado, o formulário HTML5 ignorará o parâmetro dataRef. |

### Transmissão do parâmetro de renderização {#passing-the-render-parameter}

Os formulários HTML5 suportam três métodos para transmitir os parâmetros de renderização. Você pode passar parâmetros por URLs, pares de valores chave e nó do perfil. No parâmetro de renderização, o par de valor chave tem a maior precedência seguida pelo nó do perfil. O parâmetro de Solicitação de URL tem menos precedência.

* **Parâmetros de solicitação de URL**: Você pode especificar os parâmetros de renderização no URL. Nos parâmetros de solicitação de URL, os parâmetros são visíveis para o usuário final. Por exemplo, o seguinte URL de envio contém o parâmetro de modelo no URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parâmetros da solicitação SetAttribute**: Você pode especificar os parâmetros de renderização como um par de valores chave. Nos parâmetros de solicitação SetAttribute , os parâmetros não estão visíveis para o usuário final. Você pode encaminhar uma solicitação de qualquer outro JSP para o JSP do renderizador de perfil de formulário HTML5 e usar *setAttribute* objeto de solicitação para transmitir todos os parâmetros de renderização. Este método tem a maior precedência.

* **Parâmetros de solicitação do nó de perfil:** Você pode especificar os parâmetros de renderização como propriedades do nó de um nó de perfil. Nos parâmetros de solicitação do nó de perfil, os parâmetros não estão visíveis para o usuário final. O nó do perfil é o nó para o qual a solicitação é enviada. Para especificar parâmetros como propriedades do nó, use o CRXDE lite.

### Enviar parâmetros {#submit-parameters}

Os formulários HTML5 apresentam dados; executar scripts do lado do servidor e serviços da Web em servidores AEM. Para obter informações detalhadas sobre os parâmetros usados para executar scripts do lado do servidor e serviços da Web em servidores AEM, consulte [Proxy de Serviço de Formulários HTML5](/help/forms/using/service-proxy.md).
