---
title: Referência de previsão do Construtor de query
seo-title: Referência de previsão do Construtor de query
description: Referência de previsão completa para a API do Construtor de Query.
seo-description: Referência de previsão completa para a API do Construtor de Query.
uuid: af0e269e-7d52-4032-b22e-801c7b5dccfa
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 94a05894-743a-4ace-a292-bfee90ba9068
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 3%

---


# Referência de previsão do Query Builder{#query-builder-predicate-reference}

## Geral {#general}

* [root](#root)
* [grupo](#group)
* [orderby](#orderby)

## Predicados {#predicates}

* [propriedade](/help/sites-developing/querybuilder-predicate-reference.md#boolproperty)
* [contentfragment](/help/sites-developing/querybuilder-predicate-reference.md#contentfragment)
* [dateComparison](/help/sites-developing/querybuilder-predicate-reference.md#datecomparison)
* [daterange](/help/sites-developing/querybuilder-predicate-reference.md#daterange)
* [excludedoors](/help/sites-developing/querybuilder-predicate-reference.md#excludepaths)
* [texto completo](/help/sites-developing/querybuilder-predicate-reference.md#fulltext)
* [hasPermission](/help/sites-developing/querybuilder-predicate-reference.md#haspermission)
* [language](/help/sites-developing/querybuilder-predicate-reference.md#language)
* [ativo principal](/help/sites-developing/querybuilder-predicate-reference.md#mainasset)
* [membroOf](/help/sites-developing/querybuilder-predicate-reference.md#memberof)
* [nodenome](/help/sites-developing/querybuilder-predicate-reference.md#nodename)
* [notexpired](/help/sites-developing/querybuilder-predicate-reference.md#notexpired)
* [path](/help/sites-developing/querybuilder-predicate-reference.md#path)
* [propriedade](/help/sites-developing/querybuilder-predicate-reference.md#property)
* [rangeproperty](/help/sites-developing/querybuilder-predicate-reference.md#rangeproperty)
* [paredaterange](/help/sites-developing/querybuilder-predicate-reference.md#relativedaterange)
* [savedquery](/help/sites-developing/querybuilder-predicate-reference.md#savedquery)
* [similar](/help/sites-developing/querybuilder-predicate-reference.md#similar)
* [tag](/help/sites-developing/querybuilder-predicate-reference.md#tag)
* [tagid](/help/sites-developing/querybuilder-predicate-reference.md#tagid)
* [tagsearch](/help/sites-developing/querybuilder-predicate-reference.md#tagsearch)
* [tipo](/help/sites-developing/querybuilder-predicate-reference.md#type)

### boolproperty {#boolproperty}

Corresponde às propriedades BOOLEAN do JCR. Aceita somente os valores &quot; `true`&quot; e &quot; `false`&quot;. No caso de &quot; `false`&quot;, corresponderá se a propriedade tiver o valor &quot; `false`&quot; ou se não existir. Isso pode ser útil para verificar sinalizadores booleanos que só são definidos quando ativados.

O parâmetro &quot; `operation`&quot; herdado não tem significado.

Suporta extração de facetas. Fornecerá compartimentos para cada valor `true` ou `false`, mas somente para propriedades existentes.

#### Propriedades {#properties}

* **caminho**
boolpropertyrelative para propriedade, por exemplo 
`myFeatureEnabled` ou `jcr:content/myFeatureEnabled`

* **valor**
para verificar a propriedade, &quot; 
`true`&quot; ou &quot; `false`&quot;

### contentfragment {#contentfragment}

Restringe o resultado a fragmentos de conteúdo.

Não suporta filtragem.

Não suporta extração de facetas.

#### Propriedades {#properties-1}

* ****
contentfragmentPode ser usado com qualquer valor para verificar fragmentos de conteúdo.

### dateComparison {#datecomparison}

Compara duas propriedades JCR DATE entre si. Pode testar se são iguais, desiguais, maiores ou maiores que ou iguais.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

#### Propriedades {#properties-2}

* **property1**

   propriedade path to first date

* **property2**

   propriedade path to second date

* **operation**

   &quot; `=`&quot; para correspondência exata, &quot; `!=`&quot; para comparação de desigualdade, &quot; `>`&quot; para property1 maior que property2, &quot; `>=`&quot; para property1 maior que ou igual a property2. O valor padrão é &quot; `=`&quot;.

### daterange {#daterange}

Corresponde às propriedades JCR DATE em relação a um intervalo de data/hora. Isso usa o ISO8601
formato para datas e horas ( `YYYY-MM-DDTHH:mm:ss.SSSZ`) e permite também representações parciais, como `YYYY-MM-DD`. Como alternativa, o carimbo de data e hora pode ser fornecido como o número de milissegundos desde 1970 no fuso horário UTC, o formato de hora único.

Você pode procurar qualquer coisa entre dois carimbos de data e hora, qualquer coisa mais recente ou mais antiga que uma data específica, e também escolher entre intervalos inclusivos e abertos.

Suporta extração de facetas. Fornecerá baldes &quot;hoje&quot;, &quot;esta semana&quot;, &quot;este mês&quot;, &quot;últimos 3 meses&quot;, &quot;este ano&quot;, &quot;último ano&quot; e &quot;anterior ao ano passado&quot;.

Não suporta filtragem.

#### Propriedades {#properties-3}

* **propriedade**

   caminho relativo para uma propriedade `DATE`, por exemplo `jcr:lastModified`

* **lowerBound**

   data inferior vinculada à propriedade check para, por exemplo, `2014-10-01`

* **lowerOperation**

   &quot; `>`&quot; (mais recente) ou &quot; `>=`&quot; (em ou mais recente), aplica-se a `lowerBound`. O padrão é &quot; `>`&quot;.

* **upperBound**

   limite superior para verificar a propriedade, por exemplo `2014-10-01T12:15:00`

* **upperOperation**

   &quot; `<`&quot; (mais antigo) ou &quot; `<=`&quot; (mais antigo ou mais antigo), aplica-se a `upperBound`. O padrão é &quot; `<`&quot;.

* **timeZone**

   ID do fuso horário a ser usado quando não for fornecido como uma string de data ISO-8601. O padrão é o fuso horário padrão do sistema.

### excludepath{#excludepaths}

Exclui nós do resultado, onde seu caminho corresponde a uma expressão regular.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Não suporta extração de facetas.

#### Propriedades {#properties-4}

* **excludedoors**

   a expressão regular correspondeu aos caminhos de resultado, exceto os correspondentes do resultado.

### fulltext {#fulltext}

Pesquisa termos no índice de texto completo.

Não suporta filtragem.

Não suporta extração de facetas.

#### Propriedades {#properties-5}

* **texto completo**

   os termos de pesquisa de texto completo

* **relPath**

   o caminho relativo a ser pesquisado na propriedade ou no subnó. Essa propriedade é opcional.

### grupo {#group}

Permite criar condições aninhadas. Os grupos podem conter grupos aninhados. Tudo o que está em um query do querybuilder está implicitamente em um grupo raiz, que também pode ter parâmetros `p.or` e `p.not`.

Exemplo para corresponder uma de duas propriedades em relação a um valor:

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

Isso pesquisa o termo &quot;**Management**&quot; nas páginas em `/content/geometrixx/en` ou nos ativos em `/content/dam/geometrixx`.

Isto é conceitualmente `fulltext AND ( (path AND type) OR (path AND type) )`. Esteja ciente de que tais junções OU precisam de bons índices para o desempenho.

#### Propriedades {#properties-6}

* **p.or**

   se definido como &quot; `true`&quot;, apenas um predicado no grupo deve corresponder. O padrão é &quot; `false`&quot;, o que significa que todos devem corresponder

* **p.not**

   se estiver definido como &quot; `true`&quot;, nega o grupo (o padrão é &quot; `false`&quot;)

* **&lt;predicate>**

   adiciona predicados aninhados

* **N_&lt;predicate>**

   adiciona vários predicados aninhados do mesmo tempo, como `1_property, 2_property, ...`

### hasPermission {#haspermission}

Restringe o resultado aos itens em que a sessão atual tem os privilégios [JCR especificados.](https://docs.adobe.com/content/docs/en/spec/jcr/2.0/16_Access_Control_Management.html#16.2.3%20Standard%20Privileges)

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa. Ele não suporta extração de facetas.

#### Propriedades {#properties-7}

* **hasPermission**

   privilégios JCR separados por vírgulas que a sessão do usuário atual deve ter TODOS para o nó em questão; por exemplo `jcr:write`, `jcr:modifyAccessControl`

### language {#language}

Encontra páginas CQ em um idioma específico. Isso analisa a propriedade de idioma da página e o caminho da página que geralmente inclui o idioma ou a localidade em uma estrutura de site de nível superior.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Suporta extração de facetas. Fornecerá compartimentos para cada código de idioma exclusivo.

#### Propriedades {#properties-8}

* **linguagem**

   código de idioma ISO, por exemplo &quot; `de`&quot;

### mainasset {#mainasset}

Verifica se um nó é um ativo principal do DAM e não um subativo. Isto é basicamente cada nó não dentro de um nó &quot;subassets&quot;. Observe que isso não verifica o tipo de nó `dam:Asset`. Para usar esse predicado, basta definir &quot; `mainasset=true`&quot; ou &quot; `mainasset=false`&quot;, não há outras propriedades.

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa.

Suporta extração de facetas. Fornecerá dois compartimentos para principais e subativos.

#### Propriedades {#properties-9}

* **ativo principal**

   booleano, &quot; `true`&quot; para ativos principais, &quot; `false`&quot; para subativos

### MemberOf {#memberof}

Encontra itens que são membros de uma coleção de recursos específica [sling](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/sling/resource/collection/ResourceCollection.html).

Este é um predicado somente para filtragem e não pode aproveitar um índice de pesquisa. Não suporta extração de facetas.

#### Propriedades {#properties-10}

* **membroOf**

   caminho da coleção de recursos Sling

### nodename {#nodename}

Corresponde aos nomes dos nós do JCR.

Suporta extração de facetas. Fornecerá compartimentos para cada nome de nó exclusivo (nome de arquivo).

#### Propriedades {#properties-11}

* **nodenome**

   padrão de nome do nó que permite curingas: `*` = qualquer caractere ou nenhum, `?` = qualquer caractere, `[abc]` = somente caracteres entre colchetes

### notexpired {#notexpired}

Corresponde itens verificando se uma propriedade JCR DATE é maior ou igual à hora atual do servidor. Isso pode ser usado para verificar uma propriedade de data semelhante &quot; `expiresAt`&quot; e limitar somente àqueles que ainda não expiraram ( `notexpired=true`) ou que já expiraram ( `notexpired=false`).

Não suporta filtragem.

Suporta a extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-12}

* **notexpired**

   booleano, &quot; `true`&quot; para ainda não expirado (data no futuro ou igual), &quot; `false`&quot; para expirado (data no passado) (obrigatório)

* **propriedade**

   caminho relativo para a propriedade `DATE` a ser verificada (obrigatório)

### orderby {#orderby}

Permite classificar o resultado. Se a ordem por várias propriedades for necessária, esse predicado precisa ser adicionado várias vezes usando o prefixo number, como `1_orderby=first`, `2_oderby=second`.

#### Propriedades {#properties-13}

* **orderby**

   o nome da propriedade JCR indicado por um @ à esquerda, por exemplo `@jcr:lastModified` ou `@jcr:content/jcr:title`, ou outro predicado no query, por exemplo `2_property`, no qual classificar

* **classificar**

   direção de classificação, &quot; `desc`&quot; para decrescente ou &quot; `asc`&quot; para ascendente (padrão)

* **caso**

   se definido como &quot; `ignore`&quot; fará com que a classificação não diferencie maiúsculas de minúsculas, significando que &quot;a&quot; vem antes de &quot;B&quot;; se vazio ou deixado de fora, a classificação diferencia maiúsculas de minúsculas, o que significa &quot;B&quot; vem antes de &quot;a&quot;

### path {#path}

Pesquisa em um determinado caminho.

Não suporta extração de facetas.

#### Propriedades {#properties-14}

* **caminho**

   padrão do caminho; dependendo do exato, a subárvore inteira corresponderá (como anexar `//*` no xpath, mas observe que isso não inclui o caminho base) (exato=falso, padrão) ou somente uma correspondência exata de caminho, que pode incluir curingas ( `*`); se auto estiver definido, a subárvore inteira, incluindo o nó base, será pesquisada

* **exato**

   se `exact` for true/on, o caminho exato deverá corresponder, mas pode conter curingas simples ( `*`), que correspondam aos nomes, mas não &quot; `/`&quot;; se for falso (padrão), todos os descendentes serão incluídos (opcional)

* **apartamento**

   pesquisa somente os filhos diretos (como anexar &quot; `/*`&quot; no xpath) (somente usado se &#39; `exact`&#39; não for verdadeiro, opcional)

* **self**

   pesquisa a subárvore, mas inclui o nó base fornecido como caminho (sem curingas)

### propriedade {#property}

Corresponde às propriedades do JCR e seus valores.

Suporta extração de facetas. Fornecerá compartimentos para cada valor de propriedade exclusivo nos resultados.

#### Propriedades {#properties-15}

* **propriedade**

   caminho relativo para a propriedade, por exemplo `jcr:title`

* **valor**

   valor para verificar a propriedade; segue o tipo de propriedade JCR para conversões de string

* **N_value**

   use `1_value`, `2_value`, ... para verificar vários valores (combinados com `OR` por padrão, com `AND` if e=true) (desde 5.3)

* **e**

   definido como true para combinar vários valores ( `N_value`) com AND (desde 5.3)

* **operação**

   &quot; `equals`&quot; para correspondência exata (padrão), &quot; `unequals`&quot; para comparação de desigualdade, &quot; `like`&quot; para usar a função `jcr:like` xpath (opcional), &quot; `not`&quot; para nenhuma correspondência (por exemplo, &quot; `not(@prop)`&quot; no xpath, o parâmetro value será ignorado) ou &quot; `exists`&quot; para verificação de existência (o valor pode ser true - a propriedade deve existir, o padrão - ou false - o mesmo que &quot; `not`&quot;)

* **profundidade**

   número de níveis curingas abaixo dos quais a propriedade/caminho relativo pode existir (por exemplo, `property=size depth=2` verificará o nó/tamanho, nó/&amp;ast;/size e nó/&amp;ast;/&amp;ast;/size)

### rangeproperty {#rangeproperty}

Corresponde uma propriedade JCR a um intervalo. Isso se aplica a propriedades com tipos lineares como `LONG`, `DOUBLE` e `DECIMAL`. Para `DATE`, consulte o predicado de intervalo de datas que otimizou a entrada de formato de data.

É possível definir um limite inferior e um limite superior ou apenas um deles. A operação (por exemplo, &quot;menor que&quot; ou &quot;menor ou igual a&quot;) também pode ser especificado para limite inferior e superior individualmente.

Não suporta extração de facetas.

#### Propriedades {#properties-16}

* **propriedade**

   caminho relativo para a propriedade

* **lowerBound**

   limite inferior para verificar a propriedade para

* **lowerOperation**

   &quot; `>`&quot; (padrão) ou &quot; `>=`&quot;, aplica-se a `lowerValue`

* **upperBound**

   limite superior para verificar a propriedade

* **upperOperation**

   &quot; `<`&quot; (padrão) ou &quot; `<=`&quot;, aplica-se a `lowerValue`

* **decimal**

   &quot; `true`&quot; se a propriedade selecionada for do tipo Decimal

### relativedaterange {#relativedaterange}

Corresponde as propriedades `JCR DATE` em relação a um intervalo de data/hora usando os deslocamentos de tempo relativos à hora atual do servidor. Você pode especificar `lowerBound` e `upperBound` usando um valor de milissegundo ou a sintaxe bugzilla `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos). Prefixo com &quot; `-`&quot; para indicar um deslocamento negativo antes da hora atual. Se você especificar apenas `lowerBound` ou `upperBound`, o outro assumirá 0 como padrão, o que significa a hora atual.

Por exemplo:

* `upperBound=1h` (e não  `lowerBound`) selecionaria qualquer item na próxima hora
* `lowerBound=-1d` (e não  `upperBound`) selecionaria qualquer item nas últimas 24 horas
* `lowerBound=-6M` e  `upperBound=-3M` selecionaria qualquer coisa entre 6 meses e 3 meses
* `lowerBound=-1500` e  `upperBound=5500` selecionaria algo entre 1500 milissegundos no passado e 5500 milissegundos no futuro
* `lowerBound=1d` e  `upperBound=2d` selecionaria qualquer coisa depois de amanhã

Observe que não leva anos bissextos em consideração e todos os meses são 30 dias.

Não suporta filtragem.

Suporta a extração de facetas da mesma forma que o predicado daterange.

#### Propriedades {#properties-17}

* **upperBound**

   limite de data superior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use &quot;-&quot; para deslocamento negativo

* **lowerBound**

   limite de data inferior em milissegundos ou `1s 2m 3h 4d 5w 6M 7y` (um segundo, dois minutos, três horas, quatro dias, cinco semanas, seis meses, sete anos) em relação ao tempo atual do servidor, use &quot;-&quot; para deslocamento negativo

### raiz {#root}

Grupo de predicados raiz. Suporta todos os recursos de um grupo e permite definir parâmetros de query globais.

O nome &quot;raiz&quot; nunca é usado em um query, é implícito.

#### Propriedades {#properties-18}

* **p.offset**

   número que indica o start da página de resultados, ou seja, quantos itens ignorar

* **p.limit**

   número que indica o tamanho da página

* **p.aginárioTotal**

   recomendado: Evitar calcular o total dos resultados que possam ser dispendiosos; um número que indica o total máximo para contar até (por exemplo, 1000, um número que dá aos usuários feedback suficiente sobre o tamanho bruto e números exatos para resultados menores) ou &quot; `true`&quot; para contar apenas até o mínimo necessário `p.offset` + `p.limit`

* **p.excerto**

   se definido como &quot; `true`&quot;, inclua o trecho de texto completo no resultado

* **p.hits**

   (somente para o servlet JSON) selecione a maneira como as ocorrências são gravadas como JSON, com essas ocorrências padrão (extensíveis pelo serviço ResultHitWriter):

   * **simples**:

      itens mínimos como `path`, `title`, `lastmodified`, `excerpt` (se definido)

   * **completo**:

      renderização JSON Sling do nó, com `jcr:path` indicando o caminho da ocorrência: por padrão, apenas lista as propriedades diretas do nó, inclui uma árvore mais profunda com `p.nodedepth=N`, o que significa 0 como a subárvore inteira e infinita; adicione `p.acls=true` para incluir as permissões do JCR da sessão atual no item de resultado fornecido (mapeamentos: `create` = `add_node`, `modify` = `set_property`, `delete` = `remove`)

   * **seletivo**:

      somente as propriedades especificadas em `p.properties`, que é uma lista separada por espaços (use &quot;+&quot; em URLs) de caminhos relativos; se o caminho relativo tiver uma profundidade > 1, eles serão representados como objetos filhos; a propriedade jcr:path especial inclui o caminho da ocorrência

### savedquery {#savedquery}

Inclui todos os predicados de um query querybuilder persistente no query atual como um predicado de subgrupo.

Observe que isso não executará um query extra, mas estenderá o query atual.

Os query podem ser persistentes programaticamente usando `QueryBuilder#storeQuery()`. O formato pode ser uma propriedade String de várias linhas ou um nó `nt:file` que contenha o query como um arquivo de texto no formato de propriedades Java.

Não suporta extração de facetas para os predicados do query salvo.

#### Propriedades {#properties-19}

* **savedquery**

   caminho para o query salvo (propriedade String ou nó `nt:file`)

### similar {#similar}

Pesquisa de semelhança usando `rep:similar()` do JCR XPath.

Não suporta filtragem. Não suporta extração de facetas.

#### Propriedades {#properties-20}

* **caminho absoluto**
semelhante ao nó para o qual encontrar nós semelhantes

* **caminho relativo**
locala para um nó descendente ou 
`.` para o nó atual (opcional, o padrão é &quot;  `.`&quot;)

### tag {#tag}

Pesquisa conteúdo marcado com uma ou mais tags, especificando caminhos de título de tag.

Suporta extração de facetas. Fornecerá compartimentos para cada tag exclusiva, usando seu caminho de título de tag atual.

#### Propriedades {#properties-21}

* **tag**

   caminho do título da tag a ser procurado, por exemplo, &quot;Propriedades do ativo : Orientação / Paisagem&quot;

* **N_value**

   use `1_value`, `2_value`, ... para verificar se há várias tags (combinadas com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para propriedade) a ser vista (padrão &quot; `cq:tags`&quot;)

### tagid {#tagid}

Pesquisa conteúdo marcado com uma ou mais tags, especificando IDs de tags.

Suporta extração de facetas. Fornecerá compartimentos para cada tag exclusiva, usando sua ID de tag atual.

#### Propriedades {#properties-22}

* **tagid**

   ID da tag a ser procurada, por exemplo &quot; `properties:orientation/landscape`&quot;

* **N_value**

   use `1_value`, `2_value`, ... para verificar se há várias tags (combinadas com `OR` por padrão, com `AND` if e=true) (desde 5.6)

* **propriedade**

   propriedade (ou caminho relativo para propriedade) a ser vista (padrão &quot; `cq:tags`&quot;)

### tagsearch {#tagsearch}

Pesquisa conteúdo marcado com uma ou mais tags, especificando palavras-chave. Primeiro, isso pesquisará por tags que contenham essas palavras-chave em seus títulos e, em seguida, restringirá o resultado somente aos itens marcados com elas.

Não suporta extração de facetas.

#### Propriedades {#Properties-1}

* **tagsearch**

   palavra-chave a ser pesquisada em títulos de tag

* **propriedade**

   propriedade (ou caminho relativo para propriedade) a ser vista (padrão &quot; `cq:tags`&quot;)

* **lang**

   para pesquisar somente um título de tag localizado (por exemplo, &quot; `de`&quot;)

* **all**

   (bool) pesquisar todo o texto da tag, ou seja, todos os títulos, descrição etc. (tem prioridade sobre &quot;l `ang`&quot;)

### tipo {#type}

Restringe os resultados a um tipo de nó JCR específico, tanto do tipo de nó primário quanto do tipo de mixin. Isso também localizará subtipos desse tipo de nó. Observe que os índices de pesquisa do repositório precisam abranger os tipos de nó para uma execução eficiente.

Suporta extração de facetas. Fornecerá compartimentos para cada tipo exclusivo nos resultados.

#### Propriedades {#Properties-2}

* **tipo**

   tipo de nó ou nome de mistura a ser procurado, por exemplo `cq:Page`