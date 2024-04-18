---
title: Suporte a cláusula de imagem para formulários HTML5
description: Os formulários HTML5 são compatíveis com a cláusula de Imagem XFA para valor de exibição e valor formatado para símbolos de data, texto e numéricos.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
source-git-commit: 9e1c93a0d55d88c08b67392a9f16bfce2ac62445
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Suporte a cláusula de imagem para formulários HTML5 {#picture-clause-support-for-html-forms}

Os formulários HTML5 são compatíveis com a cláusula de Imagem XFA para valor de exibição e valor formatado para símbolos de data, texto e numéricos. As seguintes expressões de cláusula Picture são suportadas:

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>No momento, o Mobile Forms não oferece suporte à cláusula Editar imagem. Além disso, os símbolos de cláusula DateTime e Time Picture não são compatíveis.

## Símbolos de campo de data aceitos {#supported-date-field-symbols}

Expressão suportada para a cláusula Date Picture:

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* data{símbolos da Cláusula de Imagem de data}

>[!NOTE]
>
>O padrão padrão padrão da cláusula picture é o padrão {MMM D, YYYY}. Se nenhum padrão for aplicado, o padrão padrão padrão será usado.

<table>
 <tbody>
  <tr>
   <th><strong>Símbolo</strong></th>
   <th>Interpretação</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Dia do mês com 1 ou 2 dígitos (1-31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Dia do mês com dois dígitos (01-31) preenchidos com zero.<br /> </td>
  </tr>
  <tr>
   <td>S</td>
   <td>Mês do ano com 1 ou 2 dígitos (1-12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mês do ano com dois dígitos (01-12) preenchidos com zeros.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nome abreviado do mês da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nome completo do mês da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nome abreviado do dia da semana da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nome completo do dia da semana da localidade atual<br /> </td>
  </tr>
  <tr>
   <td>AA</td>
   <td>Ano de 2 dígitos, onde 00 = 2000, 29 = 2029, 30 = 1930 e 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>AAAA</td>
   <td>Ano de 4 dígitos<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> De acordo com o design, o campo Data no HTML5 Forms não é compatível com o `MM-YYYY` em formato de edição. No entanto, esse formato é compatível com o formato de exibição.

## Cláusula de Imagem Numérica {#numeric-picture-clause}

Os formulários HTML5 suportam símbolos de figuras numéricas. No entanto, há uma diferença no suporte entre PDF forms e HTML Forms.

Entrada **PDF forms**, um número é formatado independentemente do número de símbolos na cláusula Picture tem

Entrada **HTML Forms**, um número será formatado somente se o número tiver dígitos menores que o número de símbolos na cláusula Picture.

**Exemplo**: Considere uma cláusula Picture: num{zzz,zzz,zz9}.

O número **10000** é formatado como **10.000** tanto no HTML como no PDF forms.

O número 1000000 é formatado como 1.000.000 em PDF forms. No entanto, no HTML Forms, o número permanece sem formatação como 1000000.

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
   <td>Dígito único</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formatação de saída</strong>: um único dígito. Ou para um espaço se os dados de entrada estiverem vazios, um espaço ou o dígito zero na posição correspondente.<br /> </td>
   <td>Dígito ou espaço único</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formatação de saída</strong>: um único dígito. Ou para nada se os dados de entrada estiverem vazios, um espaço ou o dígito zero na posição correspondente.<br /> </td>
   <td>Um dígito ou nada</td>
  </tr>
  <tr>
   <td>Erros</td>
   <td><strong>Formatação de saída</strong>: a parte exponencial de um número de ponto flutuante que consiste no símbolo exponencial (E). Seguido por um sinal opcional de mais ou menos. Seguido pelo valor do expoente.<br /> </td>
   <td>Igual à formatação de saída</td>
  </tr>
  <tr>
   <td>CR ou cr<br /> </td>
   <td>Símbolo de crédito (CR) se o número for negativo. Mais nada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S ou s<br /> </td>
   <td>Formatação de saída: um sinal de menos se o número for negativo. Mais espaço.<br /> </td>
   <td>Sinal de menos se o número for negativo. Sinal de mais se o número for positivo</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Raiz decimal do local predominante. Permitindo que a raiz decimal seja implicada na análise de entrada.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Raiz decimal do local predominante. Permitindo que a raiz decimal seja implicada ao analisar a entrada e formatar a saída.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Raiz decimal do local predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Separador de agrupamento da localidade prevalecente</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Símbolo de moeda do local predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Símbolo de porcentagem da localidade predominante.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>(U+FF08)</td>
   <td>Parêntese esquerdo se o número for negativo. Mais espaço.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Parêntese direito se o número for negativo. Mais espaço.</td>
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

Os formulários HTML5 suportam as seguintes expressões de cláusula Text Picture:

* text{símbolos de cláusula de Imagem de texto}

| **Símbolo** | **Interpretação** |
|---|---|
| A | Caractere alfabético único. |
| X | Caractere único. |
| O | Caractere alfanumérico único. |
| 0 (zero) | Caractere alfanumérico único. |
| 9 | Dígito único. |
