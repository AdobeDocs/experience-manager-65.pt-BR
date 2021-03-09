---
title: Referência de predicado do construtor de consultas
seo-title: Referência de predicado do construtor de consultas
description: Referência completa do predicado para a API do Construtor de consultas.
seo-description: Referência completa do predicado para a API do Construtor de consultas.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 054b49fb8aacb9e267ed23552d788f72123ed3b3
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 3%

---


# Referência de predicado do construtor de consultas{#query-builder-predicate-reference}

## Geral {#general}

* [root](#root)
* [grupo](#group)
* [orderby](#orderby)

## Predicados {#predicates}

* [boolproperty](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludepaths](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [texto completo](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [ativo principal](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [memberOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodename](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [não textuoso](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
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

Corresponde às propriedades BOOLEAN do JCR. Aceita apenas os valores &quot; `true`&quot; e &quot; `false`&quot;. No caso de &quot; `false`&quot;, ela corresponderá se a propriedade tiver o valor &quot; `false`&quot; ou se não existir. Isso pode ser útil para verificar sinalizadores booleanos que são definidos somente quando ativados.

O parâmetro &quot; `operation`&quot; herdado não tem significado.

Oferece suporte à extração de facetas. Fornecerá buckets para cada valor `true` ou `false`, mas somente para as propriedades existentes.

#### Propriedades {#properties}

* ****
boolpropertyrelative path to property, por exemplo 
`myFeatureEnabled` ou `jcr:content/myFeatureEnabled`

* ****
valor do valor para verificar a propriedade, &quot; 
`true`&quot; ou &quot; `false`&quot;

### contentfragment {#contentfragment}

Restringe o resultado a fragmentos de conteúdo.

Não suporta filtragem.

Não suporta extração de facetas.

#### Propriedades {#properties-1}

* ****
contentfragmentEle pode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### dateComparison {#datecomparison}

Compara duas propriedades JCR DATE entre si. Pode testar se são iguais, desiguais, maiores ou maiores que ou iguais.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

#### Propriedades {#properties-2}

* **property1**

   propriedade path to first date

* **property2**

   propriedade path to Second date

* **operation**

   &quot; `equals`&quot; para correspondência exata, &quot; `!=`&quot; para comparação de desigualdade, &quot; `greater`&quot; para propriedade1 maior que propriedade2, &quot; `>=`&quot; para propriedade1 maior ou igual a propriedade2. O valor padrão é &quot; `equals`&quot;.

### intervalo de datas {#daterange}

Corresponde às propriedades JCR DATE em relação a um intervalo de data/hora. Isso usa a ISO8601
formato para datas e horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e também permite representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como o número de milissegundos desde 1970 no fuso horário UTC, o formato de hora unix.

Você pode procurar qualquer valor entre dois carimbos de data e hora, qualquer valor mais recente ou mais antigo que uma determinada data e também escolher entre intervalos inclusivos e abertos.

Oferece suporte à extração de facetas. Fornecerá baldes &quot;hoje&quot;, &quot;esta semana&quot;, &quot;este mês&quot;, &quot;últimos 3 meses&quot;, &quot;este ano&quot;, &quot;último ano&quot; e &quot;anterior ao ano passado&quot;.

Não suporta filtragem.

#### Propriedades {#properties-3}

* **propriedade**

   caminho relativo para uma propriedade `DATE` , por exemplo `jcr:lastModified`

* **lowerBound**

   data inferior vinculada para verificar a propriedade, por exemplo `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (mais recente) ou &quot; `>=`&quot; (em ou mais recente), se aplica ao `lowerBound`. O padrão é &quot; `>`&quot;.

* **upperBound**

   limite superior para verificar a propriedade, por exemplo `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (mais antigo) ou &quot; `<=`&quot; (em ou mais), se aplica ao `upperBound`. O padrão é &quot; `<`&quot;.

* **timeZone**

   ID do fuso horário a ser usado quando não for fornecido como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepaths {#excludepaths}

Exclui nós do resultado, onde seu caminho corresponde a uma expressão regular.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Não suporta extração de facetas.

#### Propriedades {#properties-4}

* **excludepaths**

   a expressão regular corresponde aos caminhos de resultado, excluindo os correspondentes do resultado.

### texto completo {#fulltext}

Pesquisa termos no índice de texto completo.

Não suporta filtragem.

Não suporta extração de facetas.

#### Propriedades {#properties-5}

* **texto completo**

   os termos de pesquisa de texto completo

* **relPath**

   o caminho relativo a ser pesquisado na propriedade ou no subnó . Essa propriedade é opcional.

### grupo {#group}

Permite criar condições aninhadas. Os grupos podem conter grupos aninhados. Tudo que está em uma consulta do querybuilder está implicitamente em um grupo raiz, que também pode ter parâmetros `p.or` e `p.not`.

Exemplo para corresponder uma de duas propriedades a um valor:

```
group.p.or=true
group.1_property=jcr:title
group.1_property.value=My Page
group.2_property=navTitle
group.2_property.value=My Page
```

Isso é conceitualmente `(1_property` OU `2_property)`.

Exemplo para grupos aninhados:

```
fulltext=Management
group.p.or=true
group.1_group.path=/content/geometrixx/en
group.1_group.type=cq:Page
group.2_group.path=/content/dam/geometrixx
group.2_group.type=dam:Asset
```

Isso pesquisa o termo &quot;**Management**&quot; nas páginas em `/content/geometrixx/en` ou em ativos em `/content/dam/geometrixx`.

Isso é conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Esteja ciente de que essas associações OR precisam de bons índices para o desempenho.

#### Propriedades {#properties-6}

* **p.or**

   se definido como &quot; `true`&quot;, somente um predicado no grupo deve corresponder. O padrão é &quot; `false`&quot;, o que significa que todas devem corresponder

* **p.not**

   se definido como &quot; `true`&quot;, nega o grupo (o padrão é &quot; `false`&quot;)

* **&lt;predicate>**

   adiciona predicados aninhados

* **N_&lt;predicate>**

   adiciona vários predicados aninhados do mesmo tempo, como `1_property, 2_property, ...`

### hasPermission {#haspermission}

Restringe o resultado a itens em que a sessão atual tem os privilégios [JCR especificados.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa. Ele não oferece suporte à extração de facetas.

#### Propriedades {#properties-7}

* **hasPermission**

   privilégios JCR separados por vírgulas que a sessão do usuário atual TODOS devem ter para o nó em questão; por exemplo `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Encontra páginas CQ em um idioma específico. Isso observa a propriedade de idioma da página e o caminho da página que geralmente inclui o idioma ou o local em uma estrutura de site de nível superior.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Oferece suporte à extração de facetas. Fornecerá compartimentos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **idioma**

   Código de idioma ISO, por exemplo &quot; `de`&quot;

### principal {#mainasset}

Verifica se um nó é um ativo principal do DAM e não um subativo. Basicamente, cada nó não está dentro de um nó &quot;subassets&quot;. Observe que isso não verifica o tipo de nó `dam:Asset`. Para usar esse predicado, basta definir &quot; `mainasset=true`&quot; ou &quot; `mainasset=false`&quot;, não há mais propriedades.

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa.

Oferece suporte à extração de facetas. Fornecerá dois buckets para os ativos principais e secundários.

#### Propriedades {#properties-9}

* **ativo principal**

   booleano, &quot; `true`&quot; para ativos principais, &quot; `false`&quot; para subativos

### memberOf {#memberof}

Encontra itens que são membros de uma [coleção de recursos sling específica](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Este é um predicado somente filtragem e não pode utilizar um índice de pesquisa. Não suporta extração de facetas.

#### Propriedades {#properties-10}

* **memberOf**

   caminho da coleção de recursos do Sling

### nodename {#nodename}

Corresponde aos nomes do nó JCR.

Oferece suporte à extração de facetas. Fornecerá buckets para cada nome de nó exclusivo (nome do arquivo).

#### Propriedades {#properties-11}

* **nodename**

   padrão de nome de nó que permite curingas: `*` = qualquer ou nenhum caractere, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes

### {#notexpired} não texturizado

Corresponde itens verificando se uma propriedade JCR DATE é maior ou igual ao tempo atual do servidor. Isso pode ser usado para verificar uma propriedade de data similar &quot; `expiresAt`&quot; e limitar somente àqueles que ainda não expiraram ( `notexpired=true`) ou que já expiraram ( `notexpired=false`).

Não suporta filtragem.

Oferece suporte à extração de facetas da mesma forma que o predicado de intervalo de datas.

#### Propriedades {#properties-12}

* **não textuoso**

   booleano, &quot; `true`&quot; para ainda não expirado (data no futuro ou igual), &quot; `false`&quot; para expirado (data no passado) (obrigatório)

* **propriedade**

   caminho relativo para a propriedade `DATE` a ser verificada (obrigatório)

### orderby {#orderby}

Permite classificar o resultado. Se for necessário solicitar por várias propriedades, esse predicado precisará ser adicionado várias vezes usando o prefixo do número, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **orderby**

   o nome da propriedade JCR indicado por um @ à esquerda, por exemplo `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado na consulta, por exemplo `2_property`, no qual classificar

* **classificar**

   direção de classificação, &quot; `desc`&quot; para decrescente ou &quot; `asc`&quot; para crescente (padrão)

* **caso**

   se definido como &quot; `ignore`&quot; fará com que a classificação não diferencie maiúsculas de minúsculas, o que significa &quot;a&quot; vem antes de &quot;B&quot;; se estiver vazio ou não, a classificação diferencia maiúsculas de minúsculas, o que significa &quot;B&quot; vem antes de &quot;a&quot;

### path {#path}

Pesquisa em um determinado caminho.

Não suporta extração de facetas.

#### Propriedades {#properties-14}

* **caminho**

   padrão do caminho; dependendo do exato, a subárvore inteira corresponderá (como anexar `//*` no xpath, mas observe que isso não inclui o caminho base) (exato=falso, padrão) ou somente uma correspondência de caminho exata, que pode incluir curingas ( `*`); se auto for definido, a subárvore inteira, incluindo o nó base, será pesquisada

* **exato**

   se `exact` for true/on, o caminho exato deverá corresponder, mas poderá conter curingas simples ( `*`), que correspondam a nomes, mas não &quot; `/`&quot;; se for falso (padrão) todos os descendentes serão incluídos (opcional)

* **plano**

   pesquisa apenas os filhos diretos (como anexar &quot; `/*`&quot; em xpath) (usado somente se &#39; `exact`&#39; não for verdadeiro, opcional)

* **self**

   pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas)

### propriedade {#property}

Corresponde às propriedades do JCR e seus valores.

Oferece suporte à extração de facetas. Fornecerá buckets para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **propriedade**

   caminho relativo para a propriedade, por exemplo `jcr:title`

* **valor**

   valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string

* **N_value**

   use `1_value`, `2_value`, ... para verificar vários valores (combinados com `OR` por padrão, com `AND` if e=true) (desde 5.3)

* **e**

   definido como verdadeiro para a combinação de vários valores ( `N_value`) com AND (desde 5.3)

* **operation**

   &quot;`equals`&quot; para correspondência exata (padrão), &quot; `unequals`&quot; para comparação de desigualdade, &quot; `like`&quot; para usar a função `jcr:like` xpath (opcional), &quot; `not`&quot; para nenhuma correspondência (por exemplo, &quot;`not(@prop)`&quot; no xpath, o parâmetro do valor será ignorado) ou &quot; `exists`&quot; para verificação de existência (o valor pode ser verdadeiro - a propriedade deve existir, o padrão - ou falso - o mesmo que &quot; `not`&quot;)

* **profundidade**

   número de níveis de curinga sob os quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verificará o nó/tamanho, nó/&amp;ast;/size e node/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Corresponde uma propriedade JCR a um intervalo. Isso se aplica a propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE`, consulte o predicado de intervalo de datas que otimizou a entrada de formato de data.

Você pode definir um limite inferior e um limite superior ou apenas um deles. A operação (por exemplo, &quot;menor que&quot; ou &quot;menor ou igual&quot;) também pode ser especificado para limite inferior e superior individualmente.

Não suporta extração de facetas.

#### Propriedades {#properties-16}

* **propriedade**

   caminho relativo para a propriedade

* **lowerBound**

   limite inferior para verificar a propriedade para

* **lowerOperation**

   &quot; `>`&quot; (padrão) ou &quot; `>=`&quot;, se aplica a `lowerValue`

* **upperBound**

   limite superior para verificar a propriedade para

* **upperOperation**

   &quot; `<`&quot; (padrão) ou &quot; `<=`&quot;, se aplica a `lowerValue`

* **decimal**

   &quot; `true`&quot; se a propriedade verificada for do tipo Decimal

### relativedaterange {#relativedaterange}

Corresponde a `JCR DATE` propriedades em relação a um intervalo de data/hora usando deslocamentos de tempo relativos ao tempo atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe de bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixo com &quot; `-`&quot; para indicar um deslocamento negativo antes do tempo atual. Se você especificar apenas `lowerBound` ou `upperBound`, o outro assumirá 0 como padrão, o que significa o horário atual.

Por exemplo:

* `upperBound=1h` (e não  `lowerBound`) selecionaria qualquer item na próxima hora
* `lowerBound=-1d` (e não  `upperBound`) selecionaria qualquer coisa nas últimas 24 horas
* `lowerBound=-6M` e  `upperBound=-3M` selecionaria qualquer item entre 6 meses e 3 meses
* `lowerBound=-1500` e  `upperBound=5500` selecionaria algo entre 1500 milissegundos no passado e 5500 milissegundos no futuro
* `lowerBound=1d` e  `upperBound=2d` selecionaria qualquer coisa no dia depois de amanhã

Observe que não leva anos bissextos em consideração e todos os meses são 30 dias.

Não suporta filtragem.

Oferece suporte à extração de facetas da mesma forma que o predicado de intervalo de datas.

#### Propriedades {#properties-17}

* **upperBound**

   limite de data superior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use &quot;-&quot; para deslocamento negativo

* **lowerBound**

   limite de data inferior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use &quot;-&quot; para deslocamento negativo

### raiz {#root}

Grupo de predicado raiz. Suporta todos os recursos de um grupo e permite definir parâmetros de consulta global.

O nome &quot;raiz&quot; nunca é usado em um query, está implícito.

#### Propriedades {#properties-18}

* **p.offset**

   número que indica o início da página de resultados, ou seja, quantos itens ignorar

* **p.limit**

   número que indica o tamanho da página

* **p.guessTotal**

   recomendado: evitar calcular o total dos resultados que podem ser onerosos; um número que indica o total máximo para contar até (por exemplo, 1000, um número que fornece aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores) ou &quot; `true`&quot; para contar somente até o mínimo necessário `p.offset` + `p.limit`

* **p.excerto**

   se definido como &quot; `true`&quot;, inclua o trecho de texto completo no resultado

* **p.hits**

   (somente para o servlet JSON) selecione a maneira como as ocorrências são gravadas como JSON, com essas ocorrências padrão (extensíveis por meio do serviço ResultHitWriter):

   * **simples**:

      itens mínimos como `path`, `title`, `lastmodified`, `excerpt` (se definido)

   * **completo**:

      sling JSON rendering do nó, com `jcr:path` indicando o caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com `p.nodedepth=N`, o que significa 0 como a subárvore inteira e infinita; adicione `p.acls=true` para incluir as permissões JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **seletivo**:

      somente as propriedades especificadas em `p.properties`, que é uma lista de caminhos relativos separada por espaços (use &quot;+&quot; em URLs); se o caminho relativo tiver uma profundidade > 1, eles serão representados como objetos filhos; a propriedade especial jcr:path inclui o caminho da ocorrência

### savedquery {#savedquery}

Inclui todos os predicados de uma consulta persistente do querybuilder na consulta atual como um predicado de subgrupo.

Observe que isso não executará uma query extra, mas estenderá a query atual.

As consultas podem ser mantidas programaticamente usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade de sequência de caracteres de várias linhas ou um nó `nt:file` que contém a consulta como um arquivo de texto no formato de propriedades Java.

Não suporta extração de facetas para os predicados da consulta salva.

#### Propriedades {#properties-19}

* **savedquery**

   caminho para a consulta salva (propriedade String ou nó `nt:file`)

### semelhante {#similar}

Pesquisa de semelhança usando o `rep:similar()` do JCR XPath.

Não suporta filtragem. Não suporta extração de facetas.

#### Propriedades {#properties-20}

* ****
caminho absoluto semelhante para o nó para o qual encontrar nós semelhantes

* ****
caminho relativo de locala para um nó descendente ou 
`.` para o nó atual (opcional, o padrão é &quot;  `.`&quot;)

### tag {#tag}

Pesquisa por conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Oferece suporte à extração de facetas. Fornecerá buckets para cada tag única, usando seu caminho de título de tag atual.

#### Propriedades {#properties-21}

* **tag**

   caminho do título da tag a ser procurado, por exemplo &quot;Propriedades do ativo : Orientação / Paisagem&quot;

* **N_value**

   use `1_value`, `2_value`, ... para verificar várias tags (combinadas com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

### tagid {#tagid}

Pesquisa por conteúdo marcado com uma ou mais tags, especificando IDs de tags.

Oferece suporte à extração de facetas. Fornecerá buckets para cada tag exclusiva, usando sua ID de tag atual.

#### Propriedades {#properties-22}

* **tagid**

   id da tag a ser procurada, por exemplo &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... para verificar se há várias tags (combinadas com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Pesquisa por conteúdo marcado com uma ou mais tags, especificando palavras-chave. Isso primeiro pesquisará tags que contenham essas palavras-chave em seus títulos e, em seguida, restringirá o resultado somente a itens marcados com elas.

Não suporta extração de facetas.

#### Propriedades {#Properties-1}

* **tagsearch**

   palavra-chave a ser pesquisada em títulos de tag

* **propriedade**

   propriedade (ou caminho relativo para a propriedade) a ser observada (padrão &quot; `cq:tags`&quot;)

* **lang**

   para pesquisar somente um determinado título de tag localizado (por exemplo, &quot; `de`&quot;)

* **all**

   (bool) pesquisar todo o texto completo da tag, ou seja, todos os títulos, descrição etc. (tem precedência sobre &quot;l `ang`&quot;)

### tipo {#type}

Restringe os resultados a um tipo de nó JCR específico, tanto o tipo de nó primário como o tipo mixin. Isso também encontrará subtipos desse tipo de nó. Observe que os índices de pesquisa do repositório precisam abranger os tipos de nó para uma execução eficiente.

Oferece suporte à extração de facetas. Fornecerá compartimentos para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **tipo**

   tipo de nó ou nome mixin a ser procurado, por exemplo `cq:Page`