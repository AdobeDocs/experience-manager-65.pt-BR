---
title: Referência de predicado do construtor de consultas
seo-title: Query Builder Predicate Reference
description: Complete a referência de predicado para a API do Construtor de consultas.
seo-description: Complete predicate reference for the Query Builder API.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
source-git-commit: f97eb2e028263016131b0c86be5a0508ae4def9b
workflow-type: tm+mt
source-wordcount: '2371'
ht-degree: 3%

---

# Referência de predicado do construtor de consultas{#query-builder-predicate-reference}

>[!CAUTION]
>
>As informações nesta página não são exaustivas.
>
>Para obter informações completas, consulte a lista em **Predicados disponíveis** no console do Query Builder Debugger; por exemplo, em:
>* [http://localhost:4502/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)
>
>Por exemplo, consulte:
>
>* [http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29](http://localhost:4502/system/console/services?filter=%28component.factory%3Dcom.day.cq.search.eval.PredicateEvaluator%2F*%29)


## Geral {#general}

* [raiz](#root)
* [grupo](#group)
* [orderby](#orderby)

## Predicados {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [intervalo de datas](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [texto completo](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [idioma](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [principal ativo](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [não expirado](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [caminho](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [propriedade](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [relativedaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [semelhante](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Corresponde às propriedades BOOLEANAS do JCR. Aceita apenas os valores &quot; `true`&quot; e &quot; `false`&quot;. No caso de &quot; `false`&quot;, isso corresponderá se a propriedade tiver o valor &quot; `false`&quot; ou se não existir. Isso pode ser útil para verificar se há sinalizadores booleanos definidos apenas quando ativados.

O &quot; `operation`O parâmetro &quot; não tem significado.

Oferece suporte à extração de facetas. Fornecerá intervalos para cada `true` ou `false` mas somente para propriedades existentes.

#### Propriedades {#properties}

* **boolproperty**
caminho relativo para a propriedade, por exemplo 
`myFeatureEnabled` ou `jcr:content/myFeatureEnabled`

* **value**
valor para verificar a propriedade, &quot; 
`true`&quot; ou &quot; `false`&quot;

### contentfragment {#contentfragment}

Restringe o resultado aos fragmentos de conteúdo.

Não oferece suporte à filtragem.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-1}

* **contentfragment**
Ele pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### dateComparison {#datecomparison}

Compara duas propriedades JCR DATE entre si. É possível testar se eles são iguais, desiguais, maiores ou maiores ou iguais.

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa.

#### Propriedades {#properties-2}

* **property1**

   caminho para a propriedade da primeira data

* **property2**

   caminho para a segunda propriedade de data

* **operação**

   &quot; `equals`&quot; para correspondência exata, &quot; `!=`&quot; para comparação de desigualdade, &quot; `greater`&quot; para property1 maior que property2, &quot; `>=`&quot; para property1 maior ou igual a property2. O valor padrão é &quot; `equals`&quot;.

### intervalo de datas {#daterange}

Corresponde as propriedades JCR DATE com um intervalo de data/hora. Usa o formato ISO8601 para datas e horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e permite também representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como o número de milissegundos desde 1970 no fuso horário UTC, o formato de hora unix.

Você pode procurar qualquer item entre dois carimbos de data e hora, qualquer item mais recente ou mais antigo que uma determinada data, e também escolher entre intervalos inclusivos e abertos.

Oferece suporte à extração de facetas. Fornecerá intervalos &quot;hoje&quot;, &quot;esta semana&quot;, &quot;este mês&quot;, &quot;últimos 3 meses&quot;, &quot;este ano&quot;, &quot;último ano&quot; e &quot;anterior ao ano passado&quot;.

Não oferece suporte à filtragem.

#### Propriedades {#properties-3}

* **propriedade**

   caminho relativo para um `DATE` propriedade, por exemplo `jcr:lastModified`

* **lowerBound**

   data inferior vinculada para verificar a propriedade, por exemplo `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (mais recente) ou &quot; `>=`&quot; (em ou mais recente), aplica-se à `lowerBound`. O padrão é &quot; `>`&quot;.

* **upperBound**

   limite superior para verificar a propriedade, por exemplo `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (mais antigo) ou &quot; `<=`&quot; (em ou mais antigo), aplica-se à `upperBound`. O padrão é &quot; `<`&quot;.

* **timeZone**

   ID do fuso horário a ser usada quando não for fornecida como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepaths {#excludepaths}

Exclui nós do resultado em que o caminho de cada um deles corresponde a uma expressão regular.

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-4}

* **excludepaths**

   a expressão regular corresponde aos caminhos de resultado, excluindo os correspondentes do resultado.

### texto completo {#fulltext}

Pesquisa por termos no índice de texto completo.

Não oferece suporte à filtragem.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-5}

* **texto completo**

   o(s) termo(s) de pesquisa de texto completo

* **relPath**

   o caminho relativo para pesquisar na propriedade ou no subnó. Essa propriedade é opcional.

### grupo {#group}

Permite criar condições aninhadas. Os grupos podem conter grupos aninhados. Tudo em uma consulta do querybuilder está implicitamente em um grupo raiz, que pode ter `p.or` e `p.not` também.

Exemplo para corresponder uma das duas propriedades a um valor:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Isto é conceitualmente `(1_property` OU `2_property)`.

Exemplo para grupos aninhados:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Isso pesquisa o termo &quot;**Gerenciamento**&quot; nas páginas em `/content/geometrixx/en` ou em ativos no `/content/dam/geometrixx`.

Isto é conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Esteja ciente de que essas junções OR precisam de bons índices para o desempenho.

#### Propriedades {#properties-6}

* **p.ou**

   se definido como &quot; `true`&quot;, somente um predicado no grupo deve corresponder. O padrão é &quot; `false`&quot;, o que significa que todos devem corresponder

* **p.não**

   se definido como &quot; `true`&quot;, nega o grupo (o padrão é &quot; `false`&quot;)

* **&lt;predicate>**

   adiciona predicados aninhados

* **N_&lt;predicate>**

   adiciona vários predicados aninhados ao mesmo tempo, como `1_property, 2_property, ...`

### hasPermission {#haspermission}

Restringe o resultado a itens em que a sessão atual tem o valor especificado [Privilégios JCR.](https://www.adobe.io/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa. Não há suporte para extração de facetas.

#### Propriedades {#properties-7}

* **hasPermission**

   privilégios JCR separados por vírgulas que a sessão do usuário atual DEVE TER TODOS para o nó em questão; por exemplo `jcr:write`, `jcr:modifyAccessControl`

### idioma {#language}

Localiza páginas do CQ em um idioma específico. Isso verifica a propriedade de idioma da página e o caminho da página, que geralmente inclui o idioma ou localidade em uma estrutura de site de nível superior.

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa.

Oferece suporte à extração de facetas. Fornecerá intervalos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **idioma**

   Código de idioma ISO, por exemplo &quot; `de`&quot;

### principal ativo {#mainasset}

Verifica se um nó é um ativo principal do DAM e não um subativo. Basicamente, isso ocorre em todos os nós que não estão dentro de um nó &quot;subassets&quot;. Observe que isso não verifica a `dam:Asset` tipo de nó. Para usar esse predicado, basta definir &quot; `mainasset=true`&quot; ou &quot; `mainasset=false`&quot;, não há mais propriedades.

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa.

Oferece suporte à extração de facetas. Fornecerá 2 compartimentos para ativos principais e secundários.

#### Propriedades {#properties-9}

* **principal ativo**

   booleano, &quot; `true`&quot; para os ativos principais, &quot; `false`&quot;para subativos

### memberOf {#memberof}

Localiza itens que são membros de um [coleção de recursos do sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Este é um predicado somente de filtragem e não pode utilizar um índice de pesquisa. Não oferece suporte à extração de facetas.

#### Propriedades {#properties-10}

* **memberOf**

   caminho da coleção de recursos do Sling

### nodename {#nodename}

Corresponde aos nomes de nó JCR.

Oferece suporte à extração de facetas. Fornecerá buckets para cada nome de nó exclusivo (nome de arquivo).

#### Propriedades {#properties-11}

* **nodename**

   padrão de nome de nó que permite curingas: `*` = qualquer ou nenhum caractere, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes

### não expirado {#notexpired}

Corresponde a itens verificando se uma propriedade JCR DATE é maior ou igual à hora atual do servidor. Isso pode ser usado para verificar um &quot; `expiresAt`&quot;curtir a propriedade de data e limitar apenas àqueles que ainda não expiraram ( `notexpired=true`) ou que já expiraram ( `notexpired=false`).

Não oferece suporte à filtragem.

Suporta extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-12}

* **não expirado**

   booleano, &quot; `true`&quot; para ainda não expirado (data futura ou igual), &quot; `false`&quot; para expirado (data no passado) (obrigatório)

* **propriedade**

   caminho relativo para o `DATE` propriedade a ser verificada (obrigatório)

### orderby {#orderby}

Permite classificar o resultado. Se a ordenação por várias propriedades for necessária, esse predicado precisará ser adicionado várias vezes usando o prefixo do número, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **orderby**

   o nome da propriedade do JCR é indicado por um @ à esquerda, por exemplo `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado na consulta, por exemplo `2_property`, no qual classificar

* **classificar**

   direção da classificação, &quot; `desc`&quot; para decrescente ou &quot; `asc`&quot; para crescente (padrão)

* **caso**

   se definido como &quot; `ignore`&quot; fará com que a classificação não diferencie maiúsculas de minúsculas, o que significa que &quot;a&quot; vem antes de &quot;B&quot;; se estiver vazia ou for deixada de fora, a classificação diferencia maiúsculas de minúsculas, o que significa que &quot;B&quot; vem antes de &quot;a&quot;

### caminho {#path}

Pesquisa em um determinado caminho.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-14}

* **caminho**

   padrão de caminho; dependendo do exato, a subárvore inteira corresponderá (como anexar `//*` no xpath, mas observe que isso não inclui o caminho base) (exato=falso, padrão) ou apenas um caminho exato corresponde, que pode incluir curingas ( `*`); se self estiver definido, a subárvore inteira, incluindo o nó base, será pesquisada

* **exato**

   se `exact` for true/on, o caminho exato deve corresponder, mas pode conter curingas simples ( `*`), que correspondem a nomes, mas não &quot; `/`&quot;; se for falso (padrão) todos os descendentes serão incluídos (opcional)

* **plano**

   pesquisa somente os filhos diretos (como anexar &quot; `/*`&quot; no xpath) (usado somente se &#39; `exact`&#39; não é verdadeiro, opcional)

* **self**

   pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas)

### propriedade {#property}

Corresponde às propriedades do JCR e seus valores.

Oferece suporte à extração de facetas. Fornecerá intervalos para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **propriedade**

   caminho relativo para a propriedade, por exemplo `jcr:title`

* **valor**

   valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string

* **Valor_N**

   use `1_value`, `2_value`, ... para verificar se há vários valores (combinados com `OR` por padrão, com `AND` if e=true) (desde 5.3)

* **e**

   definido como verdadeiro para a combinação de vários valores ( `N_value`) com E (desde 5.3)

* **operação**

   &quot;`equals`&quot; para correspondência exata (padrão), &quot; `unequals`&quot; para comparação de desigualdade, &quot; `like`&quot; para usar o `jcr:like` função xpath (opcional), &quot; `not`&quot; para nenhuma correspondência (por exemplo, &quot;`not(@prop)`&quot; no xpath, o parâmetro do valor será ignorado) ou &quot; `exists`&quot;para verificação de existência (o valor pode ser verdadeiro - a propriedade deve existir, o padrão - ou falso - o mesmo que&quot; `not`&quot;)

* **profundidade**

   número de níveis curingas abaixo dos quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verificará o nó/tamanho, nó/&amp;ast;/tamanho e nó/&amp;ast;/&amp;ast;/tamanho)

### rangeproperty {#rangeproperty}

Corresponde uma propriedade JCR a um intervalo. Isso se aplica a propriedades com tipos lineares, como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE` consulte o predicado daterange que otimizou a entrada de formato de data.

Você pode definir um limite inferior e um limite superior ou apenas um deles. A operação (por exemplo, &quot;menor que&quot; ou &quot;menor ou igual&quot;) também podem ser especificados para limites inferior e superior individualmente.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-16}

* **propriedade**

   caminho relativo para a propriedade

* **lowerBound**

   limite inferior para verificar a propriedade

* **lowerOperation**

   &quot; `>`&quot; (padrão) ou &quot; `>=`&quot;, aplica-se ao `lowerValue`

* **upperBound**

   limite superior para verificar a propriedade

* **upperOperation**

   &quot; `<`&quot; (padrão) ou &quot; `<=`&quot;, aplica-se ao `lowerValue`

* **decimal**

   &quot; `true`&quot; se a propriedade marcada for do tipo Decimal

### relativedaterange {#relativedaterange}

Corresponde `JCR DATE` propriedades em um intervalo de data/hora usando deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixar com &quot; `-`&quot; para indicar um deslocamento negativo antes da hora atual. Se você especificar apenas `lowerBound` ou `upperBound`, o outro assumirá 0 como padrão, o que significa a hora atual.

Por exemplo:

* `upperBound=1h` (e não `lowerBound`) selecionaria qualquer item na próxima hora
* `lowerBound=-1d` (e não `upperBound`) selecionaria qualquer coisa nas últimas 24 horas
* `lowerBound=-6M` e `upperBound=-3M` selecionaria qualquer idade entre 6 e 3 meses
* `lowerBound=-1500` e `upperBound=5500` selecionaria algo entre 1500 milissegundos no passado e 5500 milissegundos no futuro
* `lowerBound=1d` e `upperBound=2d` selecionaria qualquer coisa no dia depois de amanhã

Observe que não são considerados anos bissextos e todos os meses são 30 dias.

Não oferece suporte à filtragem.

Suporta extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-17}

* **upperBound**

   limite superior de data em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação à hora atual do servidor, use &quot;-&quot; para deslocamento negativo

* **lowerBound**

   limite inferior de data em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação à hora atual do servidor, use &quot;-&quot; para deslocamento negativo

### raiz {#root}

Grupo de predicados raiz. Suporta todos os recursos de um grupo e permite definir parâmetros de consulta globais.

O nome &quot;raiz&quot; nunca é usado em uma consulta, ele está implícito.

#### Propriedades {#properties-18}

* **p.offset**

   número que indica o início da página de resultados, ou seja, quantos itens devem ser ignorados

* **p.limit**

   número que indica o tamanho da página

* **p.guessTotal**

   recomendado: evite calcular o total do resultado completo, que pode ser caro; um número que indique o total máximo a ser contado até (por exemplo, 1000, um número que fornece aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores) ou &quot; `true`&quot; para contar somente até o mínimo necessário `p.offset` + `p.limit`

* **p.excerpt**

   se definido como &quot; `true`&quot;, incluir trecho de texto completo no resultado

* **p.hits**

   (somente para o servlet JSON) selecione a forma como as ocorrências são gravadas como JSON, com estas padrão (extensíveis por meio do serviço ResultHitWriter):

   * **simples**:

      mínimo de itens como `path`, `title`, `lastmodified`, `excerpt` (se definido)

   * **completo**:

      renderização Sling JSON do nó, com `jcr:path` indicando o caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com `p.nodedepth=N`, com 0 significando a subárvore inteira e infinita; adicione `p.acls=true` para incluir as permissões JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **seletivo**:

      somente propriedades especificadas em `p.properties`, que é uma lista de caminhos relativos separada por espaços (use &quot;+&quot; em URLs); se o caminho relativo tiver uma profundidade > 1, eles serão representados como objetos filho; a propriedade especial jcr:path inclui o caminho da ocorrência

### savedquery {#savedquery}

Inclui todos os predicados de uma consulta persistente do querybuilder na consulta atual como um predicado de subgrupo.

Observe que isso não executará uma consulta extra, mas estenderá a consulta atual.

As consultas podem ser persistentes de forma programática usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade de string multilinha ou uma `nt:file` nó que contém a consulta como um arquivo de texto no formato de propriedades Java.

Não oferece suporte à extração de facetas para os predicados da consulta salva.

#### Propriedades {#properties-19}

* **savedquery**

   caminho para a consulta salva (propriedade de string ou `nt:file` node)

### semelhante {#similar}

Pesquisa de semelhança usando JCR XPath&#39;s `rep:similar()`.

Não oferece suporte à filtragem. Não oferece suporte à extração de facetas.

#### Propriedades {#properties-20}

* **semelhante**
caminho absoluto para o nó para o qual localizar nós semelhantes

* **local**
um caminho relativo para um nó descendente ou 
`.` para o nó atual (opcional, o padrão é &quot; `.`&quot;)

### tag {#tag}

Pesquisa conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Oferece suporte à extração de facetas. Fornecerá intervalos para cada tag exclusiva, usando o caminho do título da tag atual.

#### Propriedades {#properties-21}

* **tag**

   caminho do título da tag a ser procurado, por exemplo &quot;Propriedades de ativos : Orientação / Paisagem&quot;

* **Valor_N**

   use `1_value`, `2_value`, ... para verificar se há várias tags (combinadas com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

### tagid {#tagid}

Pesquisa conteúdo marcado com uma ou mais tags, especificando IDs de tag.

Oferece suporte à extração de facetas. Fornecerá compartimentos para cada tag exclusiva, usando a ID de tag atual.

#### Propriedades {#properties-22}

* **tagid**

   id da tag a ser procurada, por exemplo &quot; `properties:orientation/landscape`&quot;

* **Valor_N**

   use `1_value`, `2_value`, ... para verificar se há vários tagids (combinados com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Pesquisa conteúdo marcado com uma ou mais tags, especificando palavras-chave. Isso primeiro pesquisará tags que contenham essas palavras-chave em seus títulos e, em seguida, restringirá o resultado a apenas itens marcados com eles.

Não oferece suporte à extração de facetas.

#### Propriedades {#Properties-1}

* **tagsearch**

   palavra-chave a ser pesquisada em títulos de tags

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

* **lang**

   para pesquisar somente em um determinado título de tag localizado (por exemplo, &quot; `de`&quot;)

* **todas**

   (bool) pesquisa o texto completo da tag inteira, ou seja, todos os títulos, descrição etc. (tem precedência sobre &quot;l `ang`&quot;)

### tipo {#type}

Restringe os resultados a um tipo de nó JCR específico, seja do tipo de nó primário ou do tipo de mixin. Isso também encontrará subtipos desse tipo de nó. Observe que os índices de pesquisa do repositório precisam abranger os tipos de nó para uma execução eficiente.

Oferece suporte à extração de facetas. Fornecerá intervalos para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **tipo**

   tipo de nó ou nome de mixin a ser pesquisado, por exemplo `cq:Page`
