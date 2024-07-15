---
title: Referência de predicado do construtor de consultas
description: Complete a referência de predicado para a API do Construtor de consultas.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
exl-id: 54b942f9-5dd9-4826-9a0a-028f2d7b8e41
solution: Experience Manager, Experience Manager Sites
feature: Developing,Search,Query Builder
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '2313'
ht-degree: 2%

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

Corresponde às propriedades BOOLEANAS do JCR. Aceita apenas os valores &quot; `true`&quot; e &quot; `false`&quot;. Se &quot; `false`&quot;, corresponderá se a propriedade tiver o valor &quot; `false`&quot; ou se ela não existir. Isso pode ser útil para verificar se há sinalizadores booleanos definidos apenas quando ativados.

O parâmetro herdado &quot;`operation`&quot; não tem significado.

Oferece suporte à extração de facetas. Fornece compartimentos para cada valor `true` ou `false`, mas somente para propriedades existentes.

#### Propriedades {#properties}

* **boolproperty**
Caminho relativo para a propriedade, por exemplo, `myFeatureEnabled` ou `jcr:content/myFeatureEnabled`.

* **valor**
Valor para verificar a propriedade, &quot; `true`&quot; ou &quot; `false`&quot;.

### contentfragment {#contentfragment}

Restringe o resultado aos fragmentos de conteúdo.

Não oferece suporte à filtragem.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-1}

* **contentfragment**
Ele pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### dateComparison {#datecomparison}

Compara duas propriedades JCR DATE entre si. Você pode testar se eles são iguais, desiguais, maiores ou maiores ou iguais.

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa.

#### Propriedades {#properties-2}

* **propriedade1**

  Caminho para a propriedade da primeira data.

* **propriedade2**

  Caminho para a segunda propriedade de data.

* **operação**

  &quot; `equals`&quot; para correspondência exata, &quot; `!=`&quot; para comparação de desigualdade, &quot; `greater`&quot; para property1 maior que property2, &quot; `>=`&quot; para property1 maior ou igual a property2. O valor padrão é &quot; `equals`&quot;.

### intervalo de datas {#daterange}

Corresponde as propriedades JCR DATE com um intervalo de data/hora. Usa o padrão ISO8601
formato para datas e horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e também permite representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como o número de milissegundos desde 1970 no fuso horário UTC, o formato de hora UNIX®.

Você pode procurar qualquer item entre dois carimbos de data e hora, qualquer item mais recente ou mais antigo que uma determinada data, e também escolher entre intervalos inclusivos e abertos.

Oferece suporte à extração de facetas. Fornece intervalos &quot;hoje&quot;, &quot;esta semana&quot;, &quot;este mês&quot;, &quot;últimos 3 meses&quot;, &quot;este ano&quot;, &quot;último ano&quot; e &quot;anterior ao ano passado&quot;.

Não oferece suporte à filtragem.

#### Propriedades {#properties-3}

* **propriedade**

  Caminho relativo para uma propriedade `DATE`, por exemplo, `jcr:lastModified`.

* **lowerBound**

  Data inferior associada à verificação da propriedade para, por exemplo, `2014-10-01`.

* **lowerOperation**

  &quot; `>`&quot; (mais recente) ou &quot; `>=`&quot; (em ou mais recente), aplica-se a `lowerBound`. O padrão é &quot; `>`&quot;.

* **upperBound**

  Limite superior para verificar a propriedade, por exemplo, `2014-10-01T12:15:00`.

* **upperOperation**

  &quot; `<`&quot; (mais antigo) ou &quot; `<=`&quot; (mais antigo), aplica-se a `upperBound`. O padrão é &quot; `<`&quot;.

* **fuso horário**

  ID do fuso horário a ser usada quando não for fornecida como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepaths {#excludepaths}

Exclui nós do resultado em que o caminho de cada um deles corresponde a uma expressão regular.

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-4}

* **excludepaths**

  A expressão regular corresponde aos caminhos de resultado, excluindo os correspondentes do resultado.

### texto completo {#fulltext}

Pesquisa por termos no índice de texto completo.

Não oferece suporte à filtragem.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-5}

* **texto completo**

  Os termos de pesquisa de texto completo.

* **relPath**

  O caminho relativo para pesquisar na propriedade ou no subnó. Essa propriedade é opcional.

### grupo {#group}

Permite que condições aninhadas sejam criadas. Os grupos podem conter grupos aninhados. Tudo em uma consulta do construtor de consultas está implicitamente em um grupo raiz, que também pode ter `p.or` e `p.not` parâmetros.

Exemplo para corresponder uma das duas propriedades a um valor:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Este é conceitualmente `(1_property` OU `2_property)`.

Exemplo para grupos aninhados:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Pesquisa o termo &quot;**Gerenciamento**&quot; nas páginas em `/content/geometrixx/en` ou nos ativos em `/content/dam/geometrixx`.

Este é conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Essas associações OR precisam de bons índices para o desempenho.

#### Propriedades {#properties-6}

* **p.or**

  Se definido como &quot; `true`&quot;, somente um predicado no grupo deve corresponder. O padrão é &quot; `false`&quot;, o que significa que todos devem corresponder

* **p.não**

  Se definido como &quot; `true`&quot;, nega o grupo (o padrão é &quot; `false`&quot;).

* **&lt;predicado>**

  Adiciona predicados aninhados.

* **N_&lt;predicado>**

  Adiciona vários predicados aninhados ao mesmo tempo, como `1_property, 2_property, ...`.

### hasPermission {#haspermission}

Restringe o resultado aos itens em que a sessão atual tem os [privilégios JCR especificados.](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa. Não há suporte para extração de facetas.

#### Propriedades {#properties-7}

* **hasPermission**

  Privilégios JCR separados por vírgulas que a sessão do usuário atual deve ter TODOS os nós em questão. Por exemplo, `jcr:write`, `jcr:modifyAccessControl`.

### idioma {#language}

Localiza páginas do CQ em um idioma específico. Isso verifica a propriedade de idioma da página e o caminho da página, que geralmente inclui o idioma ou localidade em uma estrutura de site de nível superior.

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa.

Oferece suporte à extração de facetas. Fornece intervalos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **idioma**

  Código de idioma ISO, por exemplo, &quot;`de`&quot;

### principal ativo {#mainasset}

Verifica se um nó é um ativo principal do DAM e não um subativo. Basicamente, isso ocorre em todos os nós que não estão dentro de um nó &quot;subassets&quot;. Isso não verifica o tipo de nó `dam:Asset`. Para usar este predicado, defina &quot; `mainasset=true`&quot; ou &quot; `mainasset=false`&quot;, não há mais propriedades.

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa.

Suporta extração de facetas e fornece dois buckets para ativos principais e secundários.

#### Propriedades {#properties-9}

* **ativo principal**

  Booleano, &quot; `true`&quot; para ativos principais, &quot; `false`&quot; para subativos.

### memberOf {#memberof}

Localiza itens que são membros de uma [coleção de recursos de sling](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/org/apache/sling/resource/collection/ResourceCollection.html) específica.

Este é um predicado somente de filtragem e não pode usar um índice de pesquisa. Não oferece suporte à extração de facetas.

#### Propriedades {#properties-10}

* **memberOf**

  Caminho da coleção de recursos do Sling.

### nodename {#nodename}

Corresponde aos nomes de nó JCR.

Oferece suporte à extração de facetas. Fornece buckets para cada nome de nó exclusivo (nome do arquivo).

#### Propriedades {#properties-11}

* **nodename**

  Padrão de nome de nó que permite curingas: `*` = qualquer caractere ou nenhum caractere, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes.

### não expirado {#notexpired}

Corresponde a itens verificando se uma propriedade JCR DATE é maior ou igual à hora atual do servidor. Isso pode ser usado para verificar uma propriedade de data como &quot; `expiresAt`&quot; e limitar apenas àqueles que ainda não expiraram ( `notexpired=true`) ou que já expiraram ( `notexpired=false`).

Não oferece suporte à filtragem.

Suporta extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-12}

* **nãoexpirou**

  Booleano, &quot; `true`&quot; para ainda não expirado (data futura ou igual), &quot; `false`&quot; para expirado (data no passado) (obrigatório).

* **propriedade**

  Caminho relativo para a propriedade `DATE` a ser verificada (obrigatório).

### orderby {#orderby}

Permite que os resultados sejam classificados. Se a ordenação por várias propriedades for necessária, esse predicado deverá ser adicionado várias vezes usando o prefixo numérico, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **orderby**

  O nome da propriedade JCR indicado por um @ à esquerda, por exemplo, `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado na consulta, por exemplo, `2_property`, no qual classificar.

* **classificar**

  Direção de classificação, &quot; `desc`&quot; para decrescente ou &quot; `asc`&quot; para crescente (padrão).

* **caso**

  Se definido como `ignore`, ele faz com que a classificação não diferencie maiúsculas de minúsculas, o que significa que &quot;a&quot; vem antes de &quot;B&quot;; se estiver vazio ou for deixado de fora, a classificação diferencia maiúsculas de minúsculas, o que significa que &quot;B&quot; vem antes de &quot;a&quot;

### caminho {#path}

Pesquisa em um determinado caminho.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-14}

* **caminho**

  Padrão de caminho. Dependendo do exato, a subárvore inteira é correspondente (como o acréscimo de `//*` em xpath, mas observe que isso não inclui o caminho base) (exato=falso, padrão), ou somente um caminho exato corresponde, que pode incluir curingas ( `*`); se self estiver definido, a subárvore inteira, incluindo o nó base, será pesquisada.

* **exato**

  Se `exact` for verdadeiro/ativado, o caminho exato deve corresponder, mas pode conter curingas simples ( `*`), que correspondem a nomes, mas não &quot; `/`&quot;; se for falso (padrão), todos os descendentes serão incluídos (opcional).

* **simples**

  Pesquisa somente os filhos diretos (como anexar &quot; `/*`&quot; no xpath) (usado somente se &#39; `exact`&#39; não for verdadeiro, opcional).

* **self**

  Pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas).

### propriedade {#property}

Corresponde às propriedades do JCR e seus valores.

Oferece suporte à extração de facetas. Fornece intervalos para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **propriedade**

  Caminho relativo para a propriedade, por exemplo, `jcr:title`.

* **valor**

  Valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string.

* **N_value**

  Use `1_value`, `2_value`, ... para verificar se há vários valores (combinados com `OR` por padrão, com `AND` if e=true) (desde a versão 5.3).

* **e**

  Definido como verdadeiro para combinar vários valores ( `N_value`) com AND (desde 5.3).

* **operação**

  &quot;`equals`&quot; para correspondência exata (padrão), &quot; `unequals`&quot; para comparação de desigualdade, &quot; `like`&quot; para usar a função xpath `jcr:like` (opcional), &quot; `not`&quot; para nenhuma correspondência (por exemplo, &quot;`not(@prop)`&quot; em xpath, o parâmetro de valor é ignorado) ou &quot; `exists`&quot; para verificação de existência (o valor pode ser verdadeiro - a propriedade deve existir, o padrão - ou falso - igual a &quot; `not`&quot;).

* **profundidade**

  Número de níveis curinga sob os quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verifica nó/tamanho, nó/&amp;ast;/tamanho e nó/&amp;ast;/&amp;ast;/tamanho).

### rangeproperty {#rangeproperty}

Corresponde uma propriedade JCR a um intervalo. Isso se aplica às propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE`, consulte o predicado de intervalo de datas que otimizou a entrada de formato de data.

Você pode definir um limite inferior e um limite superior ou apenas um deles. A operação (por exemplo, &quot;menor que&quot; ou &quot;menor ou igual a&quot;) também pode ser especificada para limites inferior e superior, individualmente.

Não oferece suporte à extração de facetas.

#### Propriedades {#properties-16}

* **propriedade**

  Caminho relativo para a propriedade.

* **lowerBound**

  Limite inferior para verificar a propriedade.

* **lowerOperation**

  &quot; `>`&quot; (padrão) ou &quot; `>=`&quot;, aplica-se ao `lowerValue`

* **upperBound**

  Limite superior para verificar a propriedade.

* **upperOperation**

  &quot; `<`&quot; (padrão) ou &quot; `<=`&quot;, aplica-se ao `lowerValue`

* **decimal**

  &quot; `true`&quot; se a propriedade marcada for do tipo Decimal

### relativedaterange {#relativedaterange}

Corresponde as propriedades `JCR DATE` a um intervalo de data/hora usando deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixo com &quot; `-`&quot; para indicar um deslocamento negativo antes da hora atual. Se você especificar apenas `lowerBound` ou `upperBound`, o outro valor padrão será 0, significando a hora atual.

Por exemplo:

* `upperBound=1h` (e nenhum `lowerBound`) selecionaria nada na próxima hora
* `lowerBound=-1d` (e nenhum `upperBound`) selecionaria qualquer item nas últimas 24 horas
* `lowerBound=-6M` e `upperBound=-3M` selecionariam qualquer item com 6 a 3 meses
* `lowerBound=-1500` e `upperBound=5500` selecionariam algo entre 1500 milissegundos no passado e 5500 milissegundos no futuro
* `lowerBound=1d` e `upperBound=2d` selecionariam qualquer item depois de amanhã

Ele não leva anos bissextos em consideração e todos os meses são 30 dias.

Não oferece suporte à filtragem.

Suporta extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-17}

* **upperBound**

  Limite superior de data em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) relativo à hora atual do servidor, use &quot;-&quot; para deslocamento negativo.

* **lowerBound**

  Limite inferior de data em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) relativo à hora atual do servidor, use &quot;-&quot; para deslocamento negativo.

### raiz {#root}

Grupo de predicados raiz. Suporta todos os recursos de um grupo e permite a definição de parâmetros de consulta globais.

O nome &quot;root&quot; nunca é usado em uma query, ele é implícito.

#### Propriedades {#properties-18}

* **p.offset**

  O número que indica o início da página de resultados, ou seja, quantos itens devem ser ignorados.

* **p.limit**

  O número que indica o tamanho da página.

* **p.guessTotal**

  Recomendado: evite calcular o total do resultado completo, que pode ser caro; um número indicando o total máximo a ser contado até (por exemplo, 1000, um número que fornece aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores) ou &quot; `true`&quot; para contar apenas até o mínimo necessário `p.offset` + `p.limit`.

* **p.excerpt**

  Se definido como &quot; `true`&quot;, incluir trecho de texto completo no resultado.

* **p.hits**

  (somente para o servlet JSON) selecione a forma como as ocorrências são gravadas como JSON, com estas padrão (extensíveis por meio do serviço ResultHitWriter):

   * **simples**:

     Mínimo de itens como `path`, `title`, `lastmodified`, `excerpt` (se definido).

   * **cheio**:

     Renderização Sling JSON do nó, com `jcr:path` indicando o caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com `p.nodedepth=N`, com 0 significando a subárvore inteira e infinita; adicione `p.acls=true` para incluir as permissões JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`).

   * **seletivo**:

     Somente as propriedades especificadas em `p.properties`, que é uma lista de caminhos relativos separada por espaços (use &quot;+&quot; em URLs); se o caminho relativo tiver uma profundidade > 1, elas serão representadas como objetos filho; a propriedade jcr:path especial inclui o caminho da ocorrência

### savedquery {#savedquery}

Inclui todos os predicados de uma consulta persistente do construtor de consultas na consulta atual como um predicado de subgrupo.

Isso não executa uma consulta extra, mas estende a consulta atual.

As consultas podem ser persistidas de forma programática usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade de Cadeia de Caracteres de várias linhas ou um nó `nt:file` que contém a consulta como um arquivo de texto no formato de propriedades Java™.

Não oferece suporte à extração de facetas para os predicados da consulta salva.

#### Propriedades {#properties-19}

* **savedquery**

  Caminho para a consulta salva (propriedade de cadeia de caracteres ou nó `nt:file`).

### semelhante {#similar}

Pesquisa de semelhança usando JCR XPath&#39;s `rep:similar()`.

Não oferece suporte à filtragem. Não oferece suporte à extração de facetas.

#### Propriedades {#properties-20}

* **semelhante**
Caminho absoluto para o nó para o qual localizar nós semelhantes.

* **local**
Um caminho relativo para um nó descendente ou `.` para o nó atual (opcional, o padrão é &quot; `.`&quot;).

### tag {#tag}

Pesquisa conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Oferece suporte à extração de facetas. Fornece intervalos para cada tag exclusiva, usando o caminho do título da tag atual.

#### Propriedades {#properties-21}

* **marca**

  O caminho do título da tag a ser procurada, por exemplo, &quot;Propriedades dos ativos : Orientação / Paisagem&quot;.

* **N_value**

  Use `1_value`, `2_value`, ... para verificar se há várias marcas (combinadas com `OR` por padrão, com `AND` if e=true) (desde a versão 5.6).

* **propriedade**

  Propriedade (ou caminho relativo para a propriedade) a ser examinada (padrão &quot; `cq:tags`&quot;)

### tagid {#tagid}

Pesquisa conteúdo marcado com uma ou mais tags, especificando IDs de tag.

Oferece suporte à extração de facetas. Fornece compartimentos para cada tag exclusiva, usando a ID de tag atual.

#### Propriedades {#properties-22}

* **tagid**

  ID da tag para que você possa procurar, por exemplo, &quot; `properties:orientation/landscape`&quot;.

* **N_value**

  Use `1_value`, `2_value`, ... para verificar se há várias tagids (combinadas com `OR` por padrão, com `AND` if e=true) (desde a versão 5.6).

* **propriedade**

  Propriedade (ou caminho relativo para a propriedade) a ser examinada (padrão &quot; `cq:tags`&quot;).

### tagsearch {#tagsearch}

Pesquisa conteúdo marcado com uma ou mais tags, especificando palavras-chave. Primeiro, busca tags que contenham essas palavras-chave em seus títulos, depois restringe o resultado a apenas itens marcados com eles.

Não oferece suporte à extração de facetas.

#### Propriedades {#Properties-1}

* **tagsearch**

  Palavra-chave a ser pesquisada em títulos de tags.

* **propriedade**

  Propriedade (ou caminho relativo para a propriedade) a ser examinada (padrão `cq:tags`).

* **lang**

  Para pesquisar apenas um determinado título de tag localizado (por exemplo, `de`).

* **todos**

  (bool) Pesquisa o texto completo da tag, ou seja, todos os títulos, descrições e assim por diante. Tem prioridade sobre &quot;l `ang`&quot;.

### tipo {#type}

Restringe os resultados a um tipo de nó JCR específico, seja do tipo de nó primário ou do tipo de mixin. Isso também encontra subtipos desse tipo de nó. Os índices de pesquisa do repositório devem abranger os tipos de nó para uma execução eficiente.

Oferece suporte à extração de facetas. Fornece intervalos para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **tipo**

  Tipo de nó ou nome de mixin para procurar, por exemplo, `cq:Page`.
