---
title: Renderizar modelo de formulário para formulários HTML5
seo-title: Renderizar modelo de formulário para formulários HTML5
description: perfis de formulários HTML5 estão associados a renderizações de perfis. Renderizações de Perfil são páginas JSP responsáveis por gerar representação HTML do formulário chamando o serviço Forms OSGi.
seo-description: perfis de formulários HTML5 estão associados a renderizações de perfis. Renderizações de Perfil são páginas JSP responsáveis por gerar representação HTML do formulário chamando o serviço Forms OSGi.
uuid: 34daed78-0611-4355-9698-0d7f758e6b61
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: cb75b826-d044-44be-b364-790c046513e0
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 1%

---


# Renderizar modelo de formulário para formulários HTML5 {#rendering-form-template-for-html-forms}

## Renderizar ponto final {#render-endpoint}

Formulários HTML5 têm a noção de **Perfis** que são expostos como pontos finais REST para permitir a renderização móvel de modelos de formulário. Esses Perfis associaram o **Perfil Renderer**. Elas são páginas JSP responsáveis por gerar a representação HTML do formulário chamando o serviço Forms OSGi. O caminho JCR do nó do Perfil determina o URL do ponto final de renderização. O ponto final de renderização padrão do formulário que aponta para o perfil &#39;padrão&#39; é semelhante a:

https://&lt;*host*>:&lt;*porta*>/content/xfaforms/profiles/default.html?contentRoot=&lt;*caminho da pasta que contém o formulário xdp*>&amp;template=&lt;*nome do xdp*>

Por exemplo, `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Para um perfil personalizado, o ponto de extremidade é alterado de acordo. Por exemplo, o ponto final do perfil personalizado com o nome formas é:

`http://localhost:4502/content/xfaforms/profiles/hrforms.html?contentRoot=c:/xdps&template=sampleForm.xdp`

Se seu modelo residir no repositório do AEM em um aplicativo chamado FormSubmission, o URI será:

```http
http://localhost:4502/content/xfaforms/profiles/default.html?
 contentRoot=crx:///content/dam/formsanddocuments/FormSubmission/1.0
 &template=sampleForm.xdp
```

## Parâmetros de renderização {#render-parameters}

Os parâmetros de solicitação suportados ao renderizar o formulário como HTML são:

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
   <td>Esse parâmetro especifica o caminho onde o modelo e os recursos associados residem. Esse caminho pode ser o caminho do sistema de arquivos do servidor ou um caminho do repositório ou http ou um caminho ftp.<br /> </td>
  </tr>
  <tr>
   <td>submitUrl<br /> </td>
   <td>Esse parâmetro especifica o url para o qual o xml de dados de formulário é postado.<br /> </td>
  </tr>
 </tbody>
</table>

### Mesclar dados com modelo de formulário {#merge-data-with-form-template}

| Parâmetro | Descrição |
|---|---|
| dataRef | Esse parâmetro especifica o caminho **** absoluto do arquivo de dados que é unido ao modelo. Esse parâmetro pode ser um URL para um serviço de repouso que retorna os dados no formato xml. |
| data | Esse parâmetro especifica os bytes de dados codificados UTF-8 que são unidos ao modelo. Se esse parâmetro for especificado, o formulário HTML5 ignorará o parâmetro dataRef. |

### Transmissão do parâmetro de renderização {#passing-the-render-parameter}

Os formulários HTML5 suportam três métodos para transmitir os parâmetros de renderização. Você pode passar parâmetros por URLs, pares de valores chave e nó de perfil. No parâmetro de renderização, o par key-value tem a maior precedência seguida pelo nó do perfil. O parâmetro de Solicitação de URL tem menos precedência.

* **Parâmetros** de solicitação de URL: Você pode especificar os parâmetros de renderização no URL. Nos parâmetros de solicitação de URL, os parâmetros ficam visíveis para o usuário final. Por exemplo, o URL de envio a seguir contém um parâmetro de modelo no URL: `http://localhost:4502/content/xfaforms/profiles/default.html?contentRoot=/Applications/FormSubmission/1.0&template=sampleForm.xdp`

* **Parâmetros** de solicitação SetAttribute: Você pode especificar os parâmetros de renderização como um par de valores chave. Nos parâmetros de solicitação SetAttribute, os parâmetros não são visíveis para o usuário final. Você pode encaminhar uma solicitação de qualquer outro JSP para o renderizador de perfil de formulário HTML5 JSP e usar *setAttribute* no objeto de solicitação para passar todos os parâmetros de renderização. Este método tem a maior precedência.

* **Parâmetros de solicitação de nó de Perfil:** Você pode especificar os parâmetros de renderização como propriedades de nó de um nó de perfil. Nos parâmetros de solicitação do nó de perfil, os parâmetros não são visíveis para o usuário final. O nó Perfil é o nó para o qual a solicitação é enviada. Para especificar parâmetros como propriedades de nó, use a lista CRXDE.

### Enviar parâmetros {#submit-parameters}

Dados de envio de formulários HTML5; execute scripts do lado do servidor e serviços da Web em servidores AEM. Para obter informações detalhadas sobre parâmetros usados para executar scripts do lado do servidor e serviços da Web em servidores AEM, consulte Proxy [de Serviço para formulários](/help/forms/using/service-proxy.md)HTML5.
