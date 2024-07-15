---
title: Pontuação avançada e medalhas
description: Saiba como configurar a pontuação avançada para permitir a atribuição de medalhas para identificar membros como especialistas.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 1%

---

# Pontuação avançada e medalhas{#advanced-scoring-and-badges}

## Visão geral {#overview}

A pontuação avançada permite a atribuição de medalhas para identificar membros como especialistas. A pontuação avançada atribui pontos com base na quantidade *e* de qualidade do conteúdo criado por um membro, enquanto a pontuação básica atribui pontos com base na quantidade de conteúdo criado.

Essa diferença se deve ao mecanismo de pontuação usado para calcular as pontuações. O mecanismo de pontuação básico aplica matemática simples. O mecanismo de pontuação avançado é um algoritmo adaptável que recompensa os membros ativos que contribuem com conteúdo valioso e relevante, deduzido por meio do processamento de linguagem natural (NLP) de um tópico.

Além da relevância do conteúdo, os algoritmos de pontuação contabilizam as atividades dos membros, como votação e porcentagem de respostas. Embora a pontuação básica os inclua quantitativamente, a pontuação avançada os usa de forma algorítmica.

Portanto, o mecanismo de pontuação avançado requer dados suficientes para tornar a análise significativa. O limite de conquista para se tornar um especialista é constantemente reavaliado à medida que o algoritmo se ajusta continuamente ao volume e à qualidade do conteúdo criado. Também há um conceito de *decaimento* das postagens mais antigas de um membro. Se um membro especialista parar de participar do assunto em que obteve o status de especialista, em algum momento predeterminado (consulte [configuração do mecanismo de pontuação](#configurable-scoring-engine)) ele poderá perder seu status de especialista.

Configurar a pontuação avançada é praticamente o mesmo que a pontuação básica:

* As regras de pontuação e medalha básicas e avançadas são [aplicadas ao conteúdo](/help/communities/implementing-scoring.md#apply-rules-to-content) da mesma maneira.

   * Regras básicas e avançadas de pontuação e medalha podem ser aplicadas ao mesmo conteúdo.

* [Habilitar selos para os componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) é genérico.

As diferenças na configuração das regras de pontuação e medalha são:

* Mecanismo de pontuação avançado configurável
* Regras de pontuação avançadas:

   * `scoringType` definido como `advanced`
   * Requer `stopwords`

* Regras avançadas de medalha:

   * `badgingType` definido como `advanced`
   * `badgingLevels` definido como **número de níveis de especialistas a serem premiados**
   * Requer a matriz `badgingPaths` de medalhas em vez de pontos de mapeamento de matriz de limites para medalhas.

>[!NOTE]
>
>Para usar recursos avançados de pontuação e medalha, instale o [Pacote de Identificação de Especialista](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## Mecanismo de pontuação configurável {#configurable-scoring-engine}

O mecanismo de pontuação avançado fornece uma configuração OSGi com parâmetros que afetam o algoritmo de pontuação avançado.

![mecanismo de pontuação avançado](assets/advanced-scoring-engine.png)

* **Pesos de pontuação**

  Para um tópico, especifique o verbo que deve ter a maior prioridade ao calcular a pontuação. Um ou mais tópicos podem ser inseridos, mas limitados a **um verbo por tópico**. Consulte [Tópicos e Verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Inserido como `topic,verb` com escape de vírgula. Por exemplo:
  `/social/forum/hbs/social/forum\,ADD`
O padrão é definido como ADICIONAR verbo para componentes de QnA e fórum.

* **Intervalo de pontuação**

  O intervalo das pontuações avançadas é definido por esse valor (pontuação máxima) e 0 (pontuação mais baixa possível).

  O valor padrão é 100, de modo que o intervalo de pontuação seja de 0 a 100.

* **Intervalo de tempo de declínio da entidade**

  Esse parâmetro representa o número de horas após o qual todas as pontuações da entidade são decaídas. Isso é necessário para não incluir mais conteúdo antigo nas pontuações de um site da comunidade.

  O valor padrão é de 216.000 horas (~24 anos).

* **Taxa de crescimento da pontuação**
Isso especifica a pontuação entre o intervalo de pontuação 0, além do qual o crescimento diminui para limitar o número de especialistas.

  O valor padrão é 50.

## Regras de pontuação avançadas {#advanced-scoring-rules}

Na pontuação básica, a quantidade necessária para ganhar um selo é conhecida.

Na pontuação avançada, a quantidade necessária está sendo ajustada constantemente com base na quantidade de dados de qualidade no sistema. A pontuação é continuamente calculada de maneira semelhante a uma curva em forma de sino.

Se um membro ganhou uma medalha de especialista em um tópico que não está mais ativo, há a possibilidade de que ele perderá sua medalha devido à decadência ao longo do tempo.

### scoringType {#scoringtype}

Uma regra de pontuação é um conjunto de subregras de pontuação, cada uma declarando o `scoringType`.

Para invocar o mecanismo de pontuação avançado, o `scoringType` deve ser definido como `advanced`.

Consulte [Subregras de Pontuação](/help/communities/implementing-scoring.md#scoring-sub-rules).

![tipo-de-pontuação-avançada](assets/advanced-scoring-type.png)

### Palavras de interrupção {#stopwords}

O pacote de pontuação avançado instala uma pasta de configuração que contém um arquivo de palavras irrelevantes:

* `/libs/settings/community/scoring/configuration/stopwords`

O algoritmo de pontuação avançado usa a lista de palavras contidas no arquivo de palavras irrelevantes para identificar palavras comuns em inglês que são ignoradas durante o processamento de conteúdo.

Não há expectativa de que esse arquivo seja modificado.

Se o arquivo de palavras irrelevantes estiver ausente, o mecanismo de pontuação avançado emitirá um erro.

## Regras avançadas de insígnia {#advanced-badging-rules}

As propriedades avançadas da regra de criação de selo são diferentes das [propriedades básicas da regra de criação de selo](/help/communities/implementing-scoring.md#badging-rules).

Em vez de associar pontos a uma imagem de selo, é necessário apenas identificar o número de especialistas permitidos e a imagem de selo a ser premiada.

![regras-avançadas-de-medalha](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Tipo</th>
   <th>Valor Descrição</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>String[]</td>
   <td><em>(Obrigatório)</em> Uma cadeia de caracteres de vários valores de imagens de selo até o número de badgingLevels. Os caminhos da imagem do selo devem ser solicitados para que o primeiro seja concedido ao especialista mais alto. Se houver menos selos do que o indicado por badgingLevels, o último selo na matriz preencherá o restante da matriz. Exemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Longo</td>
   <td><em>(Opcional)</em> Especifica os níveis de experiência a serem atribuídos. Por exemplo, se deve haver um <code>expert </code> e um <code>almost expert</code> (dois emblemas), o valor deve ser definido como 2. O badgingLevel deve corresponder ao número de imagens de selo relacionadas a especialistas listadas para a propriedade badgingPath. O padrão é 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>String</td>
   <td><em>(Obrigatório)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Defina como "avançado", caso contrário, o padrão será "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>(Opcional)</em> Uma cadeia de caracteres de vários valores para restringir a regra de notificação a eventos de pontuação identificados por uma ou mais regras de pontuação listadas.<br /> Exemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> O padrão é sem restrição.</td>
  </tr>
 </tbody>
</table>

## Regras incluídas e selo {#included-rules-and-badge}

### Medalha incluída {#included-badge}

Incluído nesta versão beta está um selo de especialista baseado em recompensas:

* `expert`

  `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![selo de especialista](assets/included-badge.png)

Para que o selo de especialista apareça como uma recompensa pela atividade, verifique se:

* `Badges` estão habilitados para o recurso, como um fórum ou componente QnA.

* As regras avançadas de pontuação e medalha são aplicadas à página (ou antecessora) em que o componente é colocado.

Consulte as informações básicas para:

* [Ativação de símbolo para um componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicar regras](/help/communities/implementing-scoring.md#applytopage)

### Regras e sub-regras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Estão incluídas na versão beta duas regras de pontuação avançadas para a [função de fórum](/help/communities/functions.md#forum-function) (uma para cada componente de fórum e comentários do recurso de fórum):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule
   ```

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   ```
   subRules[] =
   /libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
   /libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
   ```

**Notas:**

* Os nós `rules` e `sub-rules` são do tipo `cq:Page`.
* `subRules` é um atributo do tipo Cadeia de Caracteres `[]` no nó `jcr:content` da regra.
* `sub-rules` pode ser compartilhado entre várias regras de pontuação.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos independentemente da localização.

### Regras de insígnia incluídas {#included-badging-rules}

Estão incluídas na versão duas regras avançadas de atribuição de etiquetas que correspondem aos [fóruns avançados e regras de pontuação de comentários](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` nós são do tipo cq:Page.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos independentemente da localização.
