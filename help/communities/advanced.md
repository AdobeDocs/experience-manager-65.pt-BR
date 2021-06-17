---
title: Pontuação avançada e emblemas
seo-title: Pontuação avançada e emblemas
description: Configuração de pontuação avançada
seo-description: Configuração de pontuação avançada
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
role: Administrator
exl-id: d3bb6664-6c01-4bcf-840c-072fc491fc99
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---

# Pontuação avançada e emblemas{#advanced-scoring-and-badges}

## Visão geral {#overview}

A pontuação avançada permite a atribuição de selos para identificar membros como especialistas. A pontuação avançada atribui pontos com base na quantidade *e* qualidade do conteúdo criado por um membro, enquanto a pontuação básica atribui pontos simplesmente com base na quantidade de conteúdo criado.

Essa diferença é devido ao mecanismo de pontuação usado para calcular as pontuações. O mecanismo básico de pontuação aplica matemática simples. O mecanismo de pontuação avançado é um algoritmo adaptável que recompensa os membros ativos que contribuem com conteúdo valioso e relevante, deduzido pelo processamento de linguagem natural (NLP) de um tópico.

Além da relevância do conteúdo, os algoritmos de pontuação levam em consideração as atividades dos membros, como votação e porcentagem de respostas. Embora a pontuação básica os inclua quantitativamente, a pontuação avançada os usa algoricamente.

Portanto, o mecanismo de pontuação avançado requer dados suficientes para fazer a análise significativa. O limite de realização para se tornar um especialista é constantemente reavaliado, pois o algoritmo se ajusta continuamente ao volume e à qualidade do conteúdo criado. Também há um conceito de *decay* de publicações mais antigas de um membro. Se um membro especialista deixar de participar do assunto em que ganhou status de especialista, em um ponto predeterminado (consulte [configuração do mecanismo de pontuação](#configurable-scoring-engine)), ele poderá perder seu status de especialista.

Configurar a pontuação avançada é praticamente o mesmo que a pontuação básica:

* As regras básicas e avançadas de pontuação e marcação são [aplicadas ao conteúdo](/help/communities/implementing-scoring.md#apply-rules-to-content) da mesma maneira.

   * Regras básicas e avançadas de pontuação e marcação podem ser aplicadas ao mesmo conteúdo.

* [A ativação de emblemas para ](/help/communities/implementing-scoring.md#enable-badges-for-component) componentes é genérica.

As diferenças na configuração das regras de pontuação e marcação são:

* Mecanismo de pontuação avançado configurável
* Regras avançadas de pontuação:

   * `scoringType` defina como  `advanced`
   * Exige `stopwords`

* Regras avançadas de marcação:

   * `badgingType` defina como  `advanced`
   * `badgingLevels` definir para o  **número de peritos a atribuir**
   * Exige `badgingPaths` matriz de emblemas em vez de limiares de mapeamento de matriz de pontos para emblemas.

>[!NOTE]
>
>Para usar recursos avançados de pontuação e marcação, instale o [pacote de identificação de especialista](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg).

## Mecanismo de pontuação configurável {#configurable-scoring-engine}

O mecanismo de pontuação avançado fornece uma configuração OSGi com parâmetros que afetam o algoritmo de pontuação avançado.

![mecanismo de pontuação avançado](assets/advanced-scoring-engine.png)

* **Pontuação de pesos**

   Para um tópico, especifique o verbo que deve receber a prioridade mais alta ao calcular a pontuação. Um ou mais tópicos podem ser inseridos, mas limitados a **um verbo por tópico**. Consulte [Tópicos e Verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Inserido como `topic,verb` com a vírgula escapada. Por exemplo:
   `/social/forum/hbs/social/forum\,ADD`
O padrão é definido como ADD verb para componentes de QnA e de fórum.

* **Intervalo de pontuação**

   O intervalo para pontuações avançadas é definido por esse valor (pontuação máxima possível) e 0 (pontuação mais baixa possível).

   O valor padrão é 100, de modo que o intervalo de pontuação seja 0-100.

* **Intervalo de tempo de declínio da entidade**

   Esse parâmetro representa o número de horas após as quais todas as pontuações de entidade são descartadas. Isso é necessário para não incluir mais o conteúdo antigo nas pontuações de um site da comunidade.

   O valor padrão é 216000 horas (~24 anos).

* **Taxa de crescimento de pontuação**
Especifica a pontuação entre 0 e o intervalo de pontuação, além do qual o crescimento retarda para limitar o número de especialistas.

   O valor padrão é 50.

## Regras avançadas de pontuação {#advanced-scoring-rules}

Na pontuação básica, é conhecida a quantidade necessária para ganhar um selo.

Na pontuação avançada, a quantidade necessária é ajuste constantemente com base na quantidade de dados de qualidade no sistema. A pontuação é continuamente calculada de forma semelhante a uma curva em forma de sino.

Se um membro ganhou um selo de especialista em um tópico que não está mais ativo, há a possibilidade de ele perder o selo devido a uma queda ao longo do tempo.

### scoringType {#scoringtype}

Uma regra de pontuação é um conjunto de sub-regras de pontuação, cada uma das quais declara o `scoringType`.

Para chamar o mecanismo de pontuação avançado, o `scoringType`deve ser definido como `advanced`.

Consulte [Subregras de pontuação](/help/communities/implementing-scoring.md#scoring-sub-rules).

![tipo de pontuação avançada](assets/advanced-scoring-type.png)

### Palavras-limite {#stopwords}

O pacote de pontuação avançado instala uma pasta de configuração que contém um arquivo de palavras de interrupção:

* `/libs/settings/community/scoring/configuration/stopwords`

O algoritmo de pontuação avançado usa a lista de palavras contidas no arquivo de palavras limites para identificar palavras em inglês comuns que são ignoradas durante o processamento de conteúdo.

Não há expectativa de que esse arquivo seja modificado.

Se o arquivo de palavras de interrupção estiver ausente, o mecanismo de pontuação avançado emitirá um erro.

## Regras avançadas de marcação {#advanced-badging-rules}

As propriedades avançadas da regra de marcação diferem das [propriedades básicas da regra de marcação](/help/communities/implementing-scoring.md#badging-rules).

Em vez de associar pontos a uma imagem de selo, é necessário identificar o número de especialistas permitidos e a imagem do selo a ser premiada.

![regras de marcação avançada](assets/advanced-badging-rules.png)

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Tipo</th>
   <th>Valor Descrição</th>
  </tr>
  <tr>
   <td>badgingPath</td>
   <td>Sequência de caracteres[]</td>
   <td><em>(Obrigatório)</em> Uma sequência de vários valores de imagens de selo até o número de badgingLevels. Os caminhos de imagem do selo devem ser solicitados para que o primeiro seja concedido ao especialista mais alto. Se houver menos emblemas do que o indicado por badgingLevels, o último emblema no array preencherá o restante do array. Exemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Longo</td>
   <td><em>(Opcional)</em> Especifica os níveis de especialização a serem concedidos. Por exemplo, se houver um <code>expert </code>e um <code>almost expert</code> (dois distintivos), o valor deverá ser definido como 2. O badgingLevel deve corresponder ao número de imagens de selo relacionadas a especialistas listadas para a propriedade badgingPath. O padrão é 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sequência de caracteres</td>
   <td><em>(Obrigatório)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Definido como "avançado"; caso contrário, o padrão é "básico".</td>
  </tr>
  <tr>
   <td>regras de pontuação</td>
   <td>Sequência de caracteres[]</td>
   <td><em>(Opcional)</em> Uma string com vários valores para restringir a regra de aprovação a eventos de pontuação identificados pelas regras de pontuação listadas.<br /> Exemplo de entrada: <br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> o padrão não é restrição.</td>
  </tr>
 </tbody>
</table>

## Regras e emblema incluídos {#included-rules-and-badge}

### Símbolo incluído {#included-badge}

Incluído nesta versão beta, há um selo de especialista baseado em recompensa:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![selo de especialista](assets/included-badge.png)

Para que o selo do especialista apareça como uma recompensa pela atividade, verifique se:

* `Badges` são ativadas para o recurso, como um fórum ou componente de QnA.

* As regras avançadas de pontuação e marcação são aplicadas à página (ou ancestral) na qual o componente é colocado

Consulte as informações básicas para:

* [Ativar a marcação para um componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicar regras](/help/communities/implementing-scoring.md#applytopage)

### Regras e subregras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Incluídas na versão beta estão duas regras de pontuação avançadas para a [função de fórum](/help/communities/functions.md#forum-function) (uma para cada componente do fórum e comentários do recurso de fórum):

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

* Ambos os nós `rules` e `sub-rules` são do tipo `cq:Page`.
* `subRules` é um atributo do tipo `[]` String no  `jcr:content` nó da regra.
* `sub-rules` pode ser compartilhado entre várias regras de pontuação.
* `rules` deve estar localizado em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos, independentemente da localização.

### Regras de marcação incluídas {#included-badging-rules}

Incluídas na versão estão duas regras de classificação avançadas que correspondem aos [fóruns avançados e regras de pontuação de comentários](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` nós são do tipo cq:Page.
* `rules` deve estar localizado em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos, independentemente da localização.
