---
title: Atualizar o Forms de pesquisa personalizada
seo-title: Upgrading Custom Search Forms
description: Este artigo detalha os ajustes necessários após uma atualização para que os formulários de pesquisa personalizados funcionem.
seo-description: This article details the adjustments that are required after an upgrade in order for the custom search forms to function.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
feature: Upgrading
exl-id: 797bbdf9-917a-4537-a5f9-bf2682db968b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1685'
ht-degree: 3%

---

# Atualizar o Forms de pesquisa personalizada{#upgrading-custom-search-forms}

No AEM 6.2, o local onde o Custom Search Forms está armazenado no repositório foi alterado. Após a atualização, eles são movidos da localização em 6.1 em:

* /apps/cq/gui/content/facets

para um novo local em:

* /conf/global/settings/cq/search/facets

Por causa disso, são necessários ajustes manuais após uma atualização para que os formulários continuem a funcionar.

Isso se aplica ao novo Search Forms e ao Forms padrão que foram personalizados.

Para obter mais informações, consulte a documentação em [Aspectos de pesquisa](/help/assets/search-facets.md).

## Alteração da propriedade resourceType {#changing-the-resourcetype-property}

Salvo indicação em contrário, a maioria dos ajustes que precisam ser feitos após a atualização requer a alteração da variável `sling:resourceType` para o Forms de pesquisa personalizado configurado. Isso é necessário para que a propriedade aponte para o local correto do script de renderização.

Você pode alterar a propriedade fazendo o seguinte:

1. Abra o CRXDE Lite indo para `https://server:port/crx/de/index.jsp`
1. Navegue até o local do nó que precisa ser ajustado, conforme especificado na Lista de [Forms de pesquisa personalizada](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) abaixo.
1. Clique no nó . No painel de propriedades direito, clique em e modifique o **sling:resourceType** propriedade.
1. Por fim, salve as alterações pressionando a tecla **Salvar tudo** botão.

## Lista de Forms de pesquisa personalizada {#list-of-custom-search-forms}

Abaixo você encontrará uma lista de todas as modificações personalizadas do Search Forms e as modificações necessárias após a atualização. Elas se referem aos nomes em `/conf/global/settings/cq/search/facets/sites/items`.

### Predicado de texto completo com o nome de nó &quot;texto completo&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1</td>
   <td>texto completo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

No AEM 6.1, o predicado de texto completo padrão era parte do formulário de pesquisa. Na versão 6.2, o campo de texto completo foi substituído pelo OmniSearch. Esse predicado é ignorado programaticamente e pode ser removido.

**Ação:** Remova o nó totalmente.

### Outros predicados de texto completo {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s na pesquisa padrão de em 6.1</td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados do navegador de caminhos {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tags {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>tags</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o **resourceType** propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do status de página {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

O Status da página foi substituído por dois Predicados de propriedade de opções, um para publicação e outro para o status da Live Copy.

**Ações:**

* Remova o `pagestatuspredicate` nó
* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Certifique-se de configurar `listOrder` para a `analyticspredicate` nó para &quot;**8**&quot;. Tal é necessário para evitar conflitos.

### Predicados de intervalo de datas {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Filtro oculto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Nada para ajustar.

### Predicado do Analytics {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

>[!NOTE]
>
>Observação: Em oposição à versão 6.1, o Predicado de intervalo não renderiza mais uma tag na barra de pesquisa.

### Predicado da propriedade de opções {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo do controle deslizante {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de componentes {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do autor {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de modelos {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

## Trilho de pesquisa do administrador de ativos {#assets-admin-search-rail}

Os nós abaixo se referem aos nomes em `/conf/global/settings/dam/search/facets/assets/items`

### Predicado de texto completo com o nome de nó &quot;texto completo&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nó/s no Formulário de pesquisa padrão no 6.1 | texto completo |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo de recurso na 6.2 | n/d |

No 6.1, o predicado de texto completo padrão fazia parte do formulário de pesquisa. No 6.2, o campo de texto completo foi substituído por OmniSearch. Esse predicado é ignorado programaticamente e pode ser removido.

**Ação:** Remova o nó mencionado acima.

### Predicados do navegador de caminhos {#path-browser-predicates-1}

| Nó/s no Formulário de pesquisa padrão no 6.1 | navegador de caminho |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados do Tipo Mime {#mime-type-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | mimetype |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tamanho de arquivo {#file-size-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | filesize |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Ação:** Ajustar `resourceType` como mostrado no local 6.2 acima.

### Predicados da Última Modificação do Ativo {#asset-last-modified-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Ação: Ajuste a propriedade resourceType (adicione &quot;/coral&quot; como no local 6.2 indicado acima).

### Predicado de publicação {#publish-predicate}

| Nó/s no Formulário de pesquisa padrão no 6.1 | publicação |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**Ações:**

* Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione um `optionPaths` propriedade (do tipo String) com o valor: `/libs/dam/options/predicates/publish`

* Adicionar `singleSelect` propriedade com valor booleano `true`.

### Predicados de status {#status-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | status |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados de Status de Expiração {#expiry-status-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | expirystatus |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/exiredassetpredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados da validade de metadados {#metadata-validity-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | metadatavalidez |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados de classificação {#rating-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | avaliação |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sliderangepredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicado de orientação {#orientation-predicate}

| Nó/s no Formulário de pesquisa padrão no 6.1 | orientation |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso na 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Ações:**

* Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione um `fieldLabel` com o mesmo valor da variável `text` no mesmo nó.

* Adicione um `emptyText` com o valor igual ao `text` no mesmo nó.

* Adicione um `rootPath` propriedade com o mesmo valor que `optionPaths` no mesmo nó.

### Predicado de estilo {#style-predicate}

| Nó/s no Formulário de pesquisa padrão no 6.1 | estilo |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso na 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Ações:**

* Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione um `fieldLabel` com o mesmo valor da variável `text` no mesmo nó.

* Adicione um `emptyText` com o valor igual ao `text` no mesmo nó.

* Adicione um `rootPath` propriedade com o mesmo valor que `optionPaths` no mesmo nó.

### Predicados de formato de vídeo {#video-format-predicates}

| Nó/s no Formulário de pesquisa padrão no 6.1 | videoFormat |
|---|---|
| Tipo de recurso na 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso na 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicado de ativos principais {#mainasset-predicate}

| Nó/s no Formulário de pesquisa padrão no 6.1 | ativo principal |
|---|---|
| Tipo de recurso na 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo de recurso na 6.2 | granite/ui/components/coral/foundation/form/hidden |

**Ação:** Ajuste o `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)
