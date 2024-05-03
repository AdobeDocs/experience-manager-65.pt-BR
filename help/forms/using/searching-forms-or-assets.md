---
title: Pesquisar formulários e ativos
description: Você pode pesquisar formulários e ativos na instância do AEM usando a pesquisa AEM. A pesquisa básica e avançada permite localizar rapidamente os ativos.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager
docset: aem65
role: Admin,User
exl-id: 1f4f49b7-5f32-47dd-9dc7-a6974faf2bdf
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '689'
ht-degree: 3%

---

# Pesquisar formulários e ativos{#searching-for-forms-and-assets}

Você pode pesquisar seus formulários ou ativos de formulário, usando uma sequência de texto ou de texto com curingas. Você também pode restringir sua pesquisa usando os critérios disponíveis em várias categorias no painel Pesquisar.

Ao selecionar um ou mais critérios e também especificar uma cadeia de caracteres de texto, a interseção do texto e dos critérios é retornada como resultado de pesquisa. Os resultados da pesquisa são tão bons quanto os metadados de formulário e ativo fornecidos.

Clique em ![aem6forms_search](assets/aem6forms_search.png), para mostrar ou ocultar o painel de pesquisa.

## Pesquisa básica {#basic-search}

Uma pesquisa básica é a pesquisa padrão, executada sem especificar filtros. Uma pesquisa de texto completo sobre propriedades de metadados é conduzida pelo AEM Forms.

Para executar uma pesquisa básica, insira a consulta de pesquisa no campo de texto e pressione Return. Também é possível inserir o caractere curinga (&#42;) para corresponder a qualquer número de caracteres.

O Adobe Experience Manager pesquisa o texto inserido nas propriedades de metadados e retorna os resultados correspondentes. Se você digitar mais de uma palavra, a operação de pesquisa corresponderá ao texto completo da pesquisa.

Observe os seguintes pontos sobre a pesquisa básica:

* A pesquisa é conduzida usando as propriedades de metadados de formulário e ativo.
* Se você digitar mais de uma palavra, a operação de pesquisa corresponderá ao texto completo da pesquisa.
* A pesquisa não diferencia maiúsculas de minúsculas. Por exemplo, ao digitar `geometrixx`, ativos com títulos `Geometrixx`, `GEOMETRIXX`, e `GeoMetRixx` são exibidos nos resultados da pesquisa.

* Correspondências parciais de uma palavra não são suportadas. Para pesquisar usando strings parciais, use &#42; curinga. No entanto, se a consulta de pesquisa corresponder a uma palavra completa, o formulário ou ativo correspondente será exibido.
* Os espaços extras são respeitados e não são aparados durante a pesquisa. Por exemplo, `My form` não é a mesma consulta de pesquisa que `My form`.

* Se os valores de exibição e de dados dos campos nas propriedades de metadados forem diferentes, você não poderá usar valores de exibição como parâmetros de pesquisa. Por exemplo, não é possível pesquisar com base em um status, como Modificado ou Publicado, já que essas propriedades são armazenadas em um formato diferente.

## Pesquisa avançada {#advanced-search}

Nos critérios de pesquisa, além da consulta, você pode especificar alguns parâmetros de pesquisa para tornar a pesquisa básica mais eficiente e focada.

![Campo de pesquisa e parâmetros ou filtros para pesquisa de formulário e ativo no AEM](assets/search_forms_assets.png)

Campo de pesquisa e parâmetros ou filtros para pesquisa de formulário e ativo no AEM

### Caminho do ativo {#asset-path}

Ao usar o filtro de caminho de ativo, é possível limitar os resultados da pesquisa ao diretório atual. Se a opção Pesquisar no diretório atual não estiver selecionada, os resultados da pesquisa conterão ativos do diretório base. Se a página atual não for um diretório e a opção ‘pesquisar no diretório atual’ estiver selecionada, a pesquisa retornará os ativos presentes no diretório pai.

### Modificação de ativos {#asset-modification}

Selecione uma das seguintes opções para pesquisar todos os ativos modificados em um período específico.

| **Opção** | **Descrição** |
|---|---|
| Há duas horas | Pesquisar em todos os ativos que foram modificados nas últimas duas horas. |
| Uma semana atrás | Pesquisar em todos os ativos que foram modificados na última semana. |
| Há um mês | Pesquisar em todos os ativos que foram modificados nos últimos um mês. |
| Há um ano | Pesquisar em todos os ativos modificados no último ano. |

### Status do ativo {#asset-status}

Você pode pesquisar ativos usando um dos seguintes status:

* **Publicado**: pesquise todos os ativos publicados e não modificados após a publicação.

* **Não publicado**: pesquise todos os ativos que nunca são publicados.

* **Modificado**: pesquise todos os ativos modificados ou cuja publicação foi cancelada.

### Tipo de ativo {#asset-type}

Você pode selecionar qualquer número de tipos de ativos. A pesquisa retorna a união de todos os tipos de ativos selecionados.

<table>
 <tbody>
  <tr>
   <th>Opção</th> 
   <th>Descrição</th> 
  </tr>
  <tr>
   <td>Modelo de formulário<br /> </td> 
   <td>Pesquise em todos os modelos de formulário.<br /> </td> 
  </tr>
  <tr>
   <td>Formulário PDF</td> 
   <td>Pesquise em todos os documentos do PDF.</td> 
  </tr>
  <tr>
   <td>Documento</td> 
   <td>Pesquisar em todos os documentos.</td> 
  </tr>
  <tr>
   <td>Formulário adaptável<br /> </td> 
   <td>Pesquise em todos os formulários adaptáveis.</td> 
  </tr>
  <tr>
   <td>Recurso</td> 
   <td>Pesquise em todos os recursos.<br /> </td> 
  </tr>
 </tbody>
</table>

### Tags {#tags}

Tags são etiquetas anexadas a ativos para identificação. Ao pesquisar, selecione qualquer número de tags no menu suspenso ou adicione tags personalizadas, se necessário. Um resultado de pesquisa contém a interseção das tags selecionadas.
