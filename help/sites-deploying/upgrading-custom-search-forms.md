---
title: Atualização do Forms de pesquisa personalizada
seo-title: Atualização do Forms de pesquisa personalizada
description: Este artigo detalha os ajustes necessários após uma atualização para que os formulários de pesquisa personalizados funcionem.
seo-description: Este artigo detalha os ajustes necessários após uma atualização para que os formulários de pesquisa personalizados funcionem.
uuid: 35b8fbb9-5951-4e1c-bf04-4471a55b9cb0
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
discoiquuid: a08cee9c-e981-4483-8bdc-e6353977f854
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 3%

---


# Atualizando Forms{#upgrading-custom-search-forms} de Pesquisa Personalizada

No AEM 6.2, o local onde o Custom Search Forms está armazenado no repositório foi alterado. Ao atualizar, eles são movidos de sua localização em 6.1 em:

* /apps/cq/gui/content/facets

para um novo local em:

* /conf/global/settings/cq/search/facets

Por isso, os ajustes manuais são necessários após uma atualização para que os formulários continuem a funcionar.

Isso se aplica ao novo Search Forms e ao Forms padrão que foram personalizados.

Para obter mais informações, consulte a documentação em [Aspectos de pesquisa](/help/assets/search-facets.md).

## Alteração da propriedade resourceType {#changing-the-resourcetype-property}

Salvo indicação em contrário, a maioria dos ajustes que precisam ser feitos após a atualização requer a alteração da propriedade `sling:resourceType` para o Forms de pesquisa personalizado configurado. Isso é necessário para que a propriedade aponte para o local correto do script de renderização.

Você pode alterar a propriedade fazendo o seguinte:

1. Abra o CRXDE Lite indo para `https://server:port/crx/de/index.jsp`
1. Navegue até o local do nó que precisa ser ajustado, conforme especificado na Lista [Forms](/help/sites-deploying/upgrading-custom-search-forms.md#list-of-custom-search-forms) de Busca Personalizada abaixo.
1. Clique no nó. No painel de propriedades direito, clique e modifique a propriedade **sling:resourceType**.
1. Finalmente, salve as alterações pressionando o botão **Salvar tudo**.

## Lista do Forms de pesquisa personalizada {#list-of-custom-search-forms}

Abaixo você encontrará uma lista de todos os softwares personalizados do Search Forms e as modificações necessárias após a atualização. Eles se referem aos nomes em `/conf/global/settings/cq/search/facets/sites/items`.

### Predicado de texto completo com nome de nó &quot;texto completo&quot; {#fulltext-predicate-with-node-name-fulltext}

<table>
 <tbody>
  <tr>
   <td>Nó/s no formulário de pesquisa padrão na versão 6.1</td>
   <td>texto completo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td>n/a</td>
  </tr>
 </tbody>
</table>

No AEM 6.1, o predicado de texto completo padrão era parte do formulário de pesquisa. Na seção 6.2, o campo de texto completo foi substituído pelo OmniSearch. Este predicado é ignorado programaticamente e pode ser removido.

**Ação:** remova o nó completamente.

### Outros Predicados de Texto Completo {#other-fulltext-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s na pesquisa padrão De na 6.1</td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/fulltextpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicações do navegador de caminhos {#path-browser-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>path</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicados/pathpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/pathpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de tags {#tags-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>tags</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/common/admin/customsearch/search predicates/tagspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/tagspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Ajuste a propriedade  **** resourceTypeproperty (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do status de página {#page-status-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>pagestatuspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicates/pagestatuspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td>n/d</td>
  </tr>
 </tbody>
</table>

O Status da página foi substituído por dois Predicados de propriedade de opções, um para publicação e outro para status do LiveCopy.

**Ações:**

* Remover o nó `pagestatuspredicate`
* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/publishstatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Copiar nó

   * `/libs/settings/cq/search/facets/sites/jcr:content/items/livecopystatuspredicate`
   * para `/conf/global/settings/cq/search/facets/sites/jcr:content/items`

* Certifique-se de definir a propriedade `listOrder` para o nó `analyticspredicate` como &quot;**8**&quot;. Isto é necessário para evitar conflitos.

### Previsões de intervalo de datas {#date-range-predicates}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.1</td>
   <td>cq/gui/components/common/admin/customsearch/search predicates/daterangepredicate</td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>common/admin/customsearch/search predicates/daterangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Filtro oculto {#hidden-filter}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>tipo</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>granito/ui/componentes/fundação/formulário/oculto</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>granito/ui/componentes/fundação/formulário/oculto</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** Nada para ajustar.

### Predicado do Analytics {#analytics-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>analyticspredicate</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicates/analyticspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/search/predicates/analyticspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo {#range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicados/rangepredicado</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search predicates/rangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

>[!NOTE]
>
>Observação: Em oposição ao 6.1, o Predicado de intervalo não renderiza mais uma tag na barra de pesquisa.

### Predicado da propriedade de opções {#options-property-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicates/optionspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/search/predicates/optionspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do intervalo do controle deslizante {#slider-range-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicates/sliderrangepredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search predicates/sliderrangepredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de componentes {#components-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicates/componentspredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search predicates/componentspredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado do autor {#author-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicados/userpredicate</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search predicates/userpredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicado de modelos {#templates-predicate}

<table>
 <tbody>
  <tr>
   <td>Nó/s no Formulário de pesquisa padrão em 6.1<br /> <br /> </td>
   <td>n/d</td>
  </tr>
  <tr>
   <td><p>Tipo de recurso na versão 6.1</p> </td>
   <td><p>cq/gui/components/siteadmin/admin/search/predicados/templatespredicado</p> </td>
  </tr>
  <tr>
   <td>Tipo de recurso na versão 6.2</td>
   <td><p>cq/gui/components<strong>/coral/</strong>siteadmin/admin/searchpanel/search predicates/templatespredicate</p> </td>
  </tr>
 </tbody>
</table>

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

## Trilho de pesquisa do administrador de ativos {#assets-admin-search-rail}

Os nós abaixo se referem aos nomes em `/conf/global/settings/dam/search/facets/assets/items`

### Predicado de texto completo com nome de nó &quot;texto completo&quot; {#fulltext-predicate-with-node-name-fulltext-1}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | texto completo |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/fulltextpredicate |
| Tipo de recurso na versão 6.2 | n/d |

Na versão 6.1, o predicado de texto completo padrão fazia parte do formulário de pesquisa. Na versão 6.2, o campo de texto completo foi substituído pelo OmniSearch. Este predicado é ignorado programaticamente e pode ser removido.

**Ação:** remova o nó mencionado acima.

### Predicações do navegador de caminhos {#path-browser-predicates-1}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | navegador |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/pathbrowserpredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/pathbrowserpredicate |

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicados de Tipo Mime {#mime-type-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | mimetype |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/optionspredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicados/optionspredicate |

**Ação:** ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima).

### Predicações de tamanho de arquivo {#file-size-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | filesize |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicados/filesizepredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/sliderangepredicate |

**Ação:** ajuste  `resourceType` conforme mostrado no local 6.2 acima.

### Predicados da última modificação do ativo {#asset-last-modified-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | assetlastmodifiedpredicate |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/assetlastmodifiedpredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/assetlastmodifiedpredicate |

Ação: Ajuste a propriedade resourceType (adicione &quot;/coral&quot; como no local 6.2 indicado acima).

### Predicado de publicação {#publish-predicate}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | publicação |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicados/publishpredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicados/publishpredicate |

**Ações:**

* Ajuste a propriedade `resourceType` (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione uma propriedade `optionPaths` (do tipo String) com o valor: `/libs/dam/options/predicates/publish`

* Adicione a propriedade `singleSelect` com valor booliano `true`.

### Predicados de status {#status-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | status |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/optionspredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicados/optionspredicate |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados de Status de Expiração {#expiry-status-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | expirystatus |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/expiredassetpredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/expiredassetpredicate |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados de validação de metadados {#metadata-validity-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | metadatavalidez |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/optionspredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicados/optionspredicate |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicados de Classificação {#rating-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | avaliação |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicados/ratingpredicado |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicates/sliderangepredicate |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicado de orientação {#orientation-predicate}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | orientation |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/tagsfilterpredicate |
| Tipo de recurso na versão 6.2 | cq/gui/components/coral/common/admin/customsearch/search predicates/tagspredicate |

**Ações:**

* Ajuste a propriedade `resourceType` (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione uma propriedade `fieldLabel` com o mesmo valor que a propriedade `text` no mesmo nó.

* Adicione uma propriedade `emptyText` com o mesmo valor que a propriedade `text` no mesmo nó.

* Adicione uma propriedade `rootPath` com o mesmo valor que a propriedade `optionPaths` no mesmo nó.

### Predicado de estilo {#style-predicate}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | estilo |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/tagsfilterpredicate |
| Tipo de recurso na versão 6.2 | cq/gui/components/coral/common/admin/customsearch/search predicates/tagspredicate |

**Ações:**

* Ajuste a propriedade `resourceType` (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

* Adicione uma propriedade `fieldLabel` com o mesmo valor que a propriedade `text` no mesmo nó.

* Adicione uma propriedade `emptyText` com o mesmo valor que a propriedade `text` no mesmo nó.

* Adicione uma propriedade `rootPath` com o mesmo valor que a propriedade `optionPaths` no mesmo nó.

### Predicados do formato de vídeo {#video-format-predicates}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | videoFormat |
|---|---|
| Tipo de recurso na versão 6.1 | dam/gui/components/admin/customsearch/search predicates/optionspredicate |
| Tipo de recurso na versão 6.2 | dam/gui/coral/components/admin/customsearch/search predicados/optionspredicate |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)

### Predicado do Mainasset {#mainasset-predicate}

| Nó/s no formulário de pesquisa padrão na versão 6.1 | ativo principal |
|---|---|
| Tipo de recurso na versão 6.1 | granito/ui/componentes/fundação/formulário/oculto |
| Tipo de recurso na versão 6.2 | granito/ui/componentes/coral/fundação/formulário/oculto |

**Ação:** Ajuste a  `resourceType` propriedade (adicione &quot;**/coral**&quot; como no local 6.2 indicado acima)
