---
title: Suporte a cláusula de imagem para formulários HTML5
seo-title: Picture clause support for HTML5 forms
description: Os formulários HTML5 oferecem suporte à cláusula de imagem XFA para valores de exibição e valores formatados para data, texto e símbolos numéricos.
seo-description: HTML5 forms supports XFA Picture clause for display value and formatted value for date, text, and numeric symbols.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 5%

---

# Suporte a cláusula de imagem para formulários HTML5 {#picture-clause-support-for-html-forms}

Os formulários HTML5 oferecem suporte à cláusula de imagem XFA para valores de exibição e valores formatados para data, texto e símbolos numéricos. As seguintes Expressões de cláusula de imagem são suportadas:

* category(locale){picture-cláusula} | category(locale){picture-cláusula} | category(locale){picture-cláusula}
* category.subcategory{}

>[!NOTE]
>
>Atualmente, o Mobile Forms não oferece suporte à cláusula Editar imagem. Além disso, os símbolos de cláusula DateTime e Time Picture não são compatíveis.

## Símbolos de campo de data suportados {#supported-date-field-symbols}

Expressão suportada para a cláusula de imagem de data:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Símbolos da Cláusula de Imagem}

>[!NOTE]
>
>O padrão padrão da cláusula de imagem é o padrão {MMM D, YYYY}. Se nenhum padrão for aplicado, o padrão será usado.

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th>Interpretação</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Dia do mês com 1 ou 2 dígitos (de 1 a 31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Dia do mês com 2 dígitos e 0 incluído (de 01 a 31).<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>Mês do ano com 1 ou 2 dígitos (de 1 a 12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mês do ano com 2 dígitos e 0 incluído (de 01 a 12).<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nome do mês abreviado da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nome completo do mês da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nome do dia da semana abreviado da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nome completo do dia da semana da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>Ano com 2 dígitos, em que 00 = 2000, 29 = 2029, 30 = 1930 e 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>Ano com 4 dígitos<br /> </td>
  </tr>
 </tbody>
</table>

## Cláusula de Imagem Numérica {#numeric-picture-clause}

Os formulários HTML5 são compatíveis com símbolos de Imagem numérica. No entanto, há uma diferença no suporte entre o PDF forms e o HTML Forms.

Em **PDF forms**, um número é formatado independentemente do número de símbolos na cláusula Picture

Em **HTML Forms**, um número é formatado somente se o número tiver dígitos inferiores ao número de símbolos na cláusula Picture.

**Exemplo**: Considere uma cláusula de imagem: num{zzz,zzz,zz9}.

O número **10000** é formatado como **10.000** em HTML e PDF forms.

O número 100000 é formatado como 1.000.000 em PDF forms. No entanto, no HTML Forms, o número permanece não formatado como 1000000.

Expressões suportadas para a cláusula de Imagem Numérica em **HTML Forms** são:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Símbolos de Cláusula de Imagem Numérica}

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th><strong>Interpretação</strong></th>
   <th>Análise de entrada</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formatação de saída</strong>: um único dígito. Ou para o dígito zero se os dados de entrada estiverem vazios ou um espaço na posição correspondente.<br /> </td>
   <td>Um único dígito</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formatação de saída</strong>: um único dígito. Ou para um espaço se os dados de entrada estiverem vazios, um espaço ou o dígito zero na posição correspondente.<br /> </td>
   <td>Um único dígito ou espaço</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formatação de saída</strong>: um único dígito. Ou para nada se os dados de entrada estiverem vazios, um espaço ou o dígito zero na posição correspondente.<br /> </td>
   <td>Um único dígito ou nada</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Formatação de saída</strong>: A parte exponente de um número de ponto flutuante que consiste no símbolo exponencial (E). Seguido por um sinal opcional de mais ou menos. Seguido pelo valor do expoente.<br /> </td>
   <td>Igual à formatação de saída</td>
  </tr>
  <tr>
   <td>CR ou cr<br /> </td>
   <td>Símbolo de crédito (CR) se o número for negativo. Mais nada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S ou s<br /> </td>
   <td>Formatação de saída: um sinal de menos se o número for negativo. Outro espaço.<br /> </td>
   <td>Um sinal de menos se o número for negativo. Sinal de mais se o número for positivo</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Radix decimal do local prevalecente. Permitir que o radix decimal seja implícito ao analisar a entrada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Radix decimal do local prevalecente. Permitir que o radix decimal seja implícito ao analisar a entrada e formatar a saída.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Radix decimal do local prevalecente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Separador de agrupamento da localidade prevalecente</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Símbolo monetário da localidade prevalecente.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Símbolo de porcentagem da localidade predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>Parênteses esquerdo se o número for negativo. Outro espaço.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Parênteses direito se o número for negativo. Outro espaço.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Caractere de tabulação</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Cláusula de Imagem de Texto {#text-picture-clause}

Os formulários HTML5 oferecem suporte para as seguintes expressões de cláusula de figura de texto:

* text{text Símbolos de cláusula de imagem}

| **Símbolo** | **Interpretação** |
|---|---|
| A | Um caractere alfabético único. |
| X | Um caractere único. |
| O | Um caractere alfanumérico único. |
| 0 (zero) | Um caractere alfanumérico único. |
| 9 | Um único dígito. |
