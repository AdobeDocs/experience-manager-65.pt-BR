---
title: Integração da criação da interface de usuário de correspondência com o portal personalizado
seo-title: Integração da criação da interface de usuário de correspondência com o portal personalizado
description: Saiba como integrar criar interface de usuário de correspondência com seu portal personalizado
seo-description: Saiba como integrar criar interface de usuário de correspondência com seu portal personalizado
uuid: 68ef5bf2-b271-4c44-8840-6c495069164d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 0d3bb98e-7139-4d8e-b110-6ebd11debda1
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Integração da criação da interface de usuário de correspondência com o portal personalizado{#integrating-create-correspondence-ui-with-your-custom-portal}

## Visão geral {#overview}

Este artigo detalha como você pode integrar a solução Criar correspondência com seu ambiente.

## Invocação baseada em URL {#url-based-invocation}

Uma maneira de chamar o aplicativo Criar correspondência a partir de um portal personalizado é preparar o URL com os seguintes parâmetros de solicitação:

* o identificador do modelo de letra (usando o parâmetro cmLetterId).

* o URL para os dados XML obtidos da fonte de dados desejada (usando o parâmetro cmDataUrl).

Por exemplo, o portal personalizado prepararia o URL como\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, que pode ser o href de um link no portal.

>[!NOTE]
>
>Chamar dessa forma não é seguro, pois os parâmetros necessários são passados como uma solicitação GET, expondo o mesmo (claramente visível) no URL.

>[!NOTE]
>
>Antes de chamar o aplicativo Criar correspondência, salve e carregue os dados para chamar a interface de usuário Criar correspondência no dataURL fornecido. Isso pode ser feito pelo próprio portal personalizado ou por outro processo back-end.

## Invocação em linha baseada em dados {#inline-data-based-invocation}

Outra maneira (e mais segura) de chamar o aplicativo Criar correspondência pode ser simplesmente acessar o URL em https://&#39;[server]:[port]&#39;/[contextPath]/aem/forms/createcorrespondence.html, enviando os parâmetros e dados para chamar o aplicativo Criar correspondência como uma solicitação POST (ocultando-os do usuário final). Isso também significa que agora você pode passar os dados XML para o aplicativo Criar correspondência em linha (como parte da mesma solicitação, usando o parâmetro cmData), que não era possível/ideal na abordagem anterior.

### Parâmetros para especificar a carta {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrição** |
|---|---|---|
| cmLetterInstanceId | Sequência de caracteres | O identificador da instância da carta. |
| cmLetterId | Sequência de caracteres | O nome do modelo Carta. |

A ordem dos parâmetros na tabela especifica a preferência dos parâmetros usados para carregar a carta.

### Parâmetros para especificar a fonte de dados XML {#parameters-for-specifying-the-xml-data-source}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrição</strong></td> 
  </tr>
  <tr>
   <td>cmDataUrl<br /> </td> 
   <td>URL</td> 
   <td>Dados XML de um arquivo de origem usando protocolos básicos como cq, ftp, http ou arquivo.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>Sequência de caracteres</td> 
   <td>Usando dados xml disponíveis em Instância de carta.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Para reutilizar os dados de teste anexados no dicionário de dados.</td> 
  </tr>
 </tbody>
</table>

A ordem dos parâmetros na tabela especifica a preferência dos parâmetros usados para carregar os dados XML.

### Outros parâmetros {#other-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td> 
   <td><strong>Tipo</strong></td> 
   <td><strong>Descrição</strong></td> 
  </tr>
  <tr>
   <td>cmPreview<br /> </td> 
   <td>Booleano</td> 
   <td>Verdadeiro para abrir a letra no modo de pré-visualização<br /> </td> 
  </tr>
  <tr>
   <td>Aleatório</td> 
   <td>Carimbo de data e hora</td> 
   <td>Para resolver problemas de cache do navegador.</td> 
  </tr>
 </tbody>
</table>

Se você estiver usando o protocolo http ou cq para cmDataURL, o URL de http/cq deve estar acessível anonimamente.
