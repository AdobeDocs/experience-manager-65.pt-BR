---
title: Atualização do Forms de pesquisa personalizada
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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1681'
ht-degree: 3%

---

# Atualização do Forms de pesquisa personalizada{#upgrading-custom-search-forms}

No AEM 6.2, o local onde as Forms de pesquisa personalizada são armazenadas no repositório foi alterado. Ao atualizar, eles são movidos de seu local no 6.1 em:

* /apps/cq/gui/content/facets

para um novo local em:

* /conf/global/settings/cq/search/facets

Por causa disso, são necessários ajustes manuais após uma atualização para que os formulários continuem funcionando.

Isso se aplica ao novo Search Forms e Forms padrão que foram personalizados.

Para obter mais informações, consulte a documentação em [Pesquisar aspectos](/help/assets/search-facets.md).

## Alteração da propriedade resourceType {#changing-the-resourcetype-property}

Salvo indicação em contrário, a maioria dos ajustes que precisam ser feitos após a atualização requer a alteração do `sling:resourceType` para a Forms de pesquisa personalizada configurada. Isso é necessário para que a propriedade aponte para o local correto do script de renderização.

Você pode alterar a propriedade fazendo o seguinte:

1. Abra o CRXDE Lite acessando `https://server:port/crx/de/index.jsp`
1. Navegue até o local do nó que precisa ser ajustado, conforme especificado na Lista de [Forms de pesquisa personalizada](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) abaixo.
1. Clique no nó. No painel de propriedades direito, clique em e modifique a variável **sling:resourceType** propriedade.
1. Por fim, salve as alterações pressionando o botão **Salvar tudo** botão.

## Lista de Forms de pesquisa personalizada {#list-of-custom-search-forms}

Abaixo você encontrará uma lista de todas as Forms de pesquisa personalizadas e as modificações necessárias após a atualização. Elas se referem aos nomes em `/conf/global/settings/cq/search/facets/sites/items`.

### Predicado de texto completo com nome de nó &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1</td>
   <td>texto completo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

No AEM 6.1, o predicado padrão de texto completo fazia parte do formulário de pesquisa. Na versão 6.2, o campo de texto completo foi substituído pelo OmniSearch. Este predicado é ignorado programaticamente e pode ser removido.

**Ação:** Remova o nó totalmente.

### Outros predicados de texto completo {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó(s) na pesquisa padrão de no 6.1</td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados do navegador de caminhos {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>caminho</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tags {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>tags</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável **resourceType** propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do status de página {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

O Status da página foi substituído por dois Predicados de propriedade de opções, um para publicação e um para o status da Live Copy.

**Ações:**

* Remova o `pagestatuspredicate` nó
* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Verifique se você definiu `listOrder` propriedade para o `analyticspredicate` nó para &quot;**8**&quot;. Isso é necessário para evitar conflitos.

### Predicados do intervalo de datas {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/searchpredicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/searchpredicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Filtro oculto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>granite/ui/components/foundation/form/hidden</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Nada para ajustar.

### Predicado do Analytics {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/range predicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/range predicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

>[!NOTE]
>
>Observação: em oposição ao 6.1, o Predicado do intervalo não renderiza mais uma tag na barra de pesquisa.

### Predicado da propriedade de opções {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo do controle deslizante {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/sderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/sderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de componentes {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do autor {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de modelos {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nós no formulário de pesquisa padrão no 6.1<br /> <br /> </td>
   <td>n/a</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso no 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/searchpanel/searchpredicates/templates predicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso no 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/searchpredicates/templates predicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

## Trilho de pesquisa do administrador de ativos {#assets-admin-search-rail}

Os nós abaixo se referem aos nomes em `/conf/global/settings/dam/search/facets/assets/items`

### Predicado de texto completo com nome de nó &quot;fulltext&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nós no formulário de pesquisa padrão no 6.1 | texto completo |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/fulltextpredicate |
| Tipo de recurso no 6.2 | n/a |

No 6.1, o predicado de texto completo padrão fazia parte do formulário de pesquisa. Na versão 6.2, o campo de texto completo foi substituído por OmniSearch. Este predicado é ignorado programaticamente e pode ser removido.

**Ação:** Remova o nó mencionado acima.

### Predicados do navegador de caminhos {#path-browser-predicates-1}

| Nós no formulário de pesquisa padrão no 6.1 | pathbrowser |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/pathbrowserpredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/pathbrowserpredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tipo MIME {#mime-type-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | mimetype |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tamanho de arquivo {#file-size-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | tamanho do arquivo |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/filesizepredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sderangepredicate |

**Ação:** Ajustar `resourceType` conforme mostrado na localização 6.2 acima.

### Predicados da última modificação do ativo {#asset-last-modified-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/assetlastmodifiedpredicate |

Ação: ajuste a propriedade resourceType (adicione &quot;/coral&quot; como no local 6.2 indicado acima).

### Publicar predicado {#publish-predicate}

| Nós no formulário de pesquisa padrão no 6.1 | publicação |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/publishpredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/publishpredicate |

**Ações:**

* Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

* Adicionar um `optionPaths` (do tipo String) com o valor: `/libs/dam/options/predicates/publish`

* Adicionar `singleSelect` propriedade com valor booleano `true`.

### Predicados de status {#status-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | status |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

### Predicados do status de expiração {#expiry-status-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | expirystatus |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/expiredassetpredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/expiredassetpredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

### Predicados da validade de metadados {#metadata-validity-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | metadatavalidity |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

### Predicados de classificação {#rating-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | avaliação |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/ratingpredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/sderangepredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

### Predicado de orientação {#orientation-predicate}

| Nós no formulário de pesquisa padrão no 6.1 | Orientação |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso no 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Ações:**

* Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

* Adicionar um `fieldLabel` propriedade com o mesmo valor da variável `text` no mesmo nó.

* Adicionar um `emptyText` propriedade com o mesmo valor da variável `text` no mesmo nó.

* Adicionar um `rootPath` propriedade com o mesmo valor que a variável `optionPaths` no mesmo nó.

### Predicado do estilo {#style-predicate}

| Nós no formulário de pesquisa padrão no 6.1 | estilo |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/tagsfilterpredicate |
| Tipo de recurso no 6.2 | cq/gui/components/coral/common/admin/customsearch/searchpredicates/tagspredicate |

**Ações:**

* Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

* Adicionar um `fieldLabel` propriedade com o mesmo valor da variável `text` no mesmo nó.

* Adicionar um `emptyText` propriedade com o mesmo valor da variável `text` no mesmo nó.

* Adicionar um `rootPath` propriedade com o mesmo valor que a variável `optionPaths` no mesmo nó.

### Predicados de formato de vídeo {#video-format-predicates}

| Nós no formulário de pesquisa padrão no 6.1 | videoFormat |
|---|---|
| Tipo de recurso no 6.1 | dam/gui/components/admin/customsearch/searchpredicates/optionspredicate |
| Tipo de recurso no 6.2 | dam/gui/coral/components/admin/customsearch/searchpredicates/optionspredicate |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)

### Predicado do Mainasset {#mainasset-predicate}

| Nós no formulário de pesquisa padrão no 6.1 | principal ativo |
|---|---|
| Tipo de recurso no 6.1 | granite/ui/components/foundation/form/hidden |
| Tipo de recurso no 6.2 | granite/ui/components/coral/foundation/form/hidden |

**Ação:** Ajuste a variável `resourceType` propriedade (adicionar &quot;**/coral**&quot; como na localização do 6.2 indicada acima)
