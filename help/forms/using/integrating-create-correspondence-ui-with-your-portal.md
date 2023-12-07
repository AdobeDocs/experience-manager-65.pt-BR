---
title: Integrando Criar interface do usuário de correspondência ao portal personalizado
description: Saiba como integrar criar interface do usuário de correspondência ao portal personalizado
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: c3b6ee31-ccbb-4446-86c8-f618226fefc4
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# Integrando Criar interface do usuário de correspondência ao portal personalizado{#integrating-create-correspondence-ui-with-your-custom-portal}

## Visão geral {#overview}

Este artigo detalha como é possível integrar a opção Criar solução de correspondência ao seu ambiente.

## Chamada baseada em URL {#url-based-invocation}

Uma maneira de chamar o aplicativo Criar correspondência de um portal personalizado é preparar o URL com os seguintes parâmetros de solicitação:

* o identificador do modelo de correspondência (usando o parâmetro cmLetterId).

* o URL para os dados XML obtidos da fonte de dados desejada (usando o parâmetro cmDataUrl ).

Por exemplo, o portal personalizado prepararia o URL como\
`https://'[server]:[port]'/[contextPath]/aem/forms/createcorrespondence.html?random=[timestamp]&cmLetterId=[letter identifier]&cmDataUrl=[data URL]`, que pode ser o href de um link no portal.

>[!NOTE]
>
>Chamar dessa maneira não é seguro, pois os parâmetros necessários são transmitidos como uma solicitação do GET, expondo o mesmo (claramente visível) no URL.

>[!NOTE]
>
>Antes de chamar o aplicativo Criar correspondência, salve e faça upload dos dados para chamar a interface Criar correspondência no URL de dados fornecido. Isso pode ser feito no próprio portal personalizado ou por meio de outro processo de back-end.

## Chamada embutida baseada em dados {#inline-data-based-invocation}

Outra (e uma maneira mais segura) de chamar o aplicativo Criar correspondência pode ser simplesmente clicar no URL em https://&#39;[server]:[porta]&#39;/[contextPath]/aem/forms/createcorrespondence.html, ao enviar os parâmetros e dados para chamar o aplicativo Criar correspondência como uma solicitação POST (ocultando-os do usuário final). Isso também significa que agora é possível transmitir os dados XML para o aplicativo Criar correspondência em linha (como parte da mesma solicitação, usando o parâmetro cmData ), o que não era possível/ideal na abordagem anterior.

### Parâmetros para especificação de carta {#parameters-for-specifying-letter}

| **Nome** | **Tipo** | **Descrição** |
|---|---|---|
| cmLetterInstanceId | String | O identificador para a ocorrência de carta. |
| cmLetterId | String | O nome do modelo de Carta. |

A ordem dos parâmetros na tabela especifica a preferência dos parâmetros usados para carregar a correspondência.

### Parâmetros para especificação da fonte de dados XML {#parameters-for-specifying-the-xml-data-source}

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
   <td>Dados XML de um arquivo de origem usando protocolos básicos como cq, ftp, http ou file.<br /> </td> 
  </tr>
  <tr>
   <td>cmLetterInstanceId</td> 
   <td>String</td> 
   <td>Uso de dados xml disponíveis na Instância de Carta.</td> 
  </tr>
  <tr>
   <td>cmUseTestData</td> 
   <td>Booleano</td> 
   <td>Para reutilizar os dados de teste anexados ao dicionário de dados.</td> 
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
   <td>Verdadeiro para abrir a carta no modo de visualização<br /> </td> 
  </tr>
  <tr>
   <td>Aleatório</td> 
   <td>Carimbo de data e hora</td> 
   <td>Para resolver problemas de cache do navegador.</td> 
  </tr>
 </tbody>
</table>

Se você estiver usando o protocolo http ou cq para cmDataURL, o URL de http/cq deverá estar acessível anonimamente.
