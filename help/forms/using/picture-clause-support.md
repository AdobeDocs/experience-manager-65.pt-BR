---
title: Suporte a cláusula de imagem para formulários HTML5
description: O HTML5 Forms oferece suporte à cláusula de Imagem XFA para valor de exibição e valor formatado para símbolos de data, texto e numéricos.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
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
source-wordcount: '652'
ht-degree: 1%
---
# Suporte a cláusula de imagem para formulários HTML5 {#picture-clause-support-for-html-forms}

O HTML5 Forms oferece suporte à cláusula de Imagem XFA para valor de exibição e valor formatado para símbolos de data, texto e numéricos. As seguintes expressões de cláusula Picture são suportadas:

* categoria(localidade){picture-clause} | categoria(localidade){picture-clause} | categoria(localidade){picture-clause}
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
* data{date Picture Clause symbols}

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
   <td>Dia do mês com dois dígitos (01-31) preenchidos com zeros.<br /> </td>
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
   <td>Nome de mês abreviado da localidade atual<br /> </td>
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
> De acordo com o design, o campo Data no HTML5 Forms não oferece suporte ao padrão `MM-YYYY` no formato de edição. No entanto, o padrão é compatível com o formato de exibição.

## Cláusula de Imagem Numérica {#numeric-picture-clause}

Os formulários HTML5 suportam símbolos de Imagem Numérica. No entanto, há uma diferença no suporte entre o PDF forms e o HTML Forms.

Em **PDF forms**, um número é formatado independentemente do número de símbolos na cláusula Picture

No **HTML Forms**, um número será formatado somente se o número tiver dígitos menores que o número de símbolos na cláusula Picture.

**Exemplo**: Considere uma cláusula Picture: num{zzz,zzz,zz9}.

O número **10000** está formatado como **10.000** no HTML e no PDF forms.

O número 1000000 é formatado como 1.000.000 no PDF forms. No entanto, no HTML Forms, o número permanece sem formatação como 1000000.

As expressões suportadas para a cláusula de Imagem Numérica em **HTML Forms** são:

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

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

Os formulários HTML5 são compatíveis com as seguintes expressões de cláusula Text Picture:

* text{text Picture clause symbols}

| **Símbolo** | **Interpretação** |
|---|---|
| A | Caractere alfabético único. |
| X | Caractere único. |
| O | Caractere alfanumérico único. |
| 0 (zero) | Caractere alfanumérico único. |
| 9 | Dígito único. |
