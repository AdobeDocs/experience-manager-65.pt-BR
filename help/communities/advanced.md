---
title: Pontuação avançada e símbolos
seo-title: Pontuação avançada e símbolos
description: Configuração de pontuação avançada
seo-description: Configuração de pontuação avançada
uuid: 48caca57-43d3-4f2f-adf3-257428ba54d5
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: eb3d5c37-8097-46de-8c4f-804ea723f1c5
docset: aem65
translation-type: tm+mt
source-git-commit: 9ea2efb7409ae38c8771815336ae0d9388d923fa
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 1%

---


# Pontuação avançada e símbolos{#advanced-scoring-and-badges}

## Visão geral {#overview}

A pontuação avançada permite a atribuição de emblemas para identificar membros como especialistas. A pontuação avançada atribui pontos com base na quantidade ** e na qualidade do conteúdo criado por um membro, enquanto a pontuação básica atribui pontos simplesmente com base na quantidade de conteúdo criado.

Essa diferença se deve ao mecanismo de pontuação usado para calcular as pontuações. O mecanismo básico de pontuação aplica matemática simples. O mecanismo avançado de pontuação é um algoritmo adaptável que recompensa os membros ativos que contribuem com conteúdo valioso e relevante, deduzido pelo processamento de linguagem natural (NLP) de um tópico.

Além da relevância do conteúdo, os algoritmos de pontuação levam em conta atividades de membros, como votação e porcentagem de respostas. Embora a pontuação básica os inclua quantitativamente, a pontuação avançada os usa algoricamente.

Portanto, o mecanismo de pontuação avançado requer dados suficientes para tornar a análise significativa. O limite de conquista para se tornar um especialista é constantemente reavaliado à medida que o algoritmo se ajusta continuamente ao volume e à qualidade do conteúdo criado. Há também um conceito de *decaimento* das postagens mais antigas de um membro. Se um membro especialista deixar de participar no assunto em que adquiriu o estatuto de perito, em determinado ponto (ver configuração [do mecanismo de](#configurable-scoring-engine)pontuação) poderá perder o seu estatuto de perito.

Configurar a pontuação avançada é praticamente o mesmo que a pontuação básica:

* As regras básicas e avançadas de pontuação e marcação são [aplicadas ao conteúdo](/help/communities/implementing-scoring.md#apply-rules-to-content) da mesma maneira.

   * Regras básicas e avançadas de pontuação e marcação podem ser aplicadas ao mesmo conteúdo.

* [Habilitar emblemas para componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) é genérico.

As diferenças na configuração das regras de pontuação e marcação são:

* Mecanismo de pontuação avançada configurável
* Regras avançadas de pontuação:

   * `scoringType` definir para `advanced`
   * Exige `stopwords`

* Regras avançadas de identificação:

   * `badgingType` definir para `advanced`
   * `badgingLevels` definido para **número de especialistas a serem atribuídos**
   * Requer `badgingPaths` uma matriz de emblemas em vez de limitar os pontos de mapeamento da matriz para emblemas.

>[!NOTE]
>
>Para usar recursos avançados de pontuação e marcação, instale o pacote [de identificação de](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/social/cq-social-expert-identification-pkg)especialistas.


## Mecanismo de Pontuação Configurável {#configurable-scoring-engine}

O mecanismo de pontuação avançado fornece uma configuração OSGi com parâmetros que afetam o algoritmo de pontuação avançado.

![chlimage_1-260](assets/chlimage_1-260.png)

* **pesos de pontuação**

   Para um tópico, especifique o verbo que deve receber a prioridade mais alta ao calcular a pontuação. Um ou mais tópicos podem ser inseridos, mas limitados a **um verbo por tópico**. Consulte [Tópicos e Verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Digitado como `topic,verb` com a vírgula que escapou. Por exemplo:
   `/social/forum/hbs/social/forum\,ADD`
O padrão é definido para o verbo ADD para QnA e componentes do fórum.

* **Intervalo de pontuação**

   O intervalo para pontuações avançadas é definido por esse valor (pontuação máxima possível) e 0 (pontuação mais baixa possível).

   O valor padrão é 100 para que o intervalo de pontuação seja de 0 a 100.

* **Intervalo de tempo de decadência de entidade**

   Este parâmetro representa o número de horas após as quais todas as pontuações de entidade são diminuídas. Isso é necessário para não incluir mais conteúdo antigo em pontuações para um site da comunidade.

   O valor padrão é 216000 horas (~24 anos).

* **Pontuação da taxa de crescimento** Especifica a pontuação entre 0 e o intervalo de pontuação, além da qual o crescimento retarda para limitar o número de especialistas.

   O valor padrão é 50.

## Regras avançadas de pontuação {#advanced-scoring-rules}

Na pontuação básica, é conhecida a quantidade necessária para ganhar um crachá.

Na pontuação avançada, a quantidade necessária é constantemente ajustada com base na quantidade de dados de qualidade no sistema. A pontuação é continuamente calculada de forma semelhante à curva em forma de sino.

Se um membro ganhou um crachá de especialista em um tópico que não está mais ativo, há a possibilidade de que ele perca seu crachá devido a uma degradação ao longo do tempo.

### scoringType {#scoringtype}

Uma regra de pontuação é um conjunto de sub-regras de pontuação, cada uma das quais declara o `scoringType`.

Para chamar o mecanismo de pontuação avançado, o `scoringType`deve ser definido como `advanced`.

Consulte Sub-regras [de](/help/communities/implementing-scoring.md#scoring-sub-rules)Pontuação.

![chlimage_1-261](assets/chlimage_1-261.png)

### Palavras de interrupção {#stopwords}

O pacote de pontuação avançado instala uma pasta de configuração que contém um arquivo de palavras de interrupção:

* `/libs/settings/community/scoring/configuration/stopwords`

O algoritmo avançado de pontuação usa a lista de palavras contida no arquivo de palavras de interrupção para identificar palavras comuns em inglês que são ignoradas durante o processamento do conteúdo.

Não há expectativa de que esse arquivo seja modificado.

Se o arquivo de palavras de interrupção estiver ausente, o mecanismo de pontuação avançado emitirá um erro.

## Regras avançadas de identificação {#advanced-badging-rules}

As propriedades avançadas da regra de identificação diferem das propriedades [](/help/communities/implementing-scoring.md#badging-rules)básicas da regra de identificação.

Em vez de associar pontos a uma imagem emblema, basta identificar o número de especialistas permitidos e a imagem do crachá a ser premiada.

![chlimage_1-262](assets/chlimage_1-262.png)

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
   <td><em>(Obrigatório)</em> Uma string de vários valores de imagens de emblema até o número de badgingLevels. Os caminhos de imagem do crachá devem ser ordenados para que o primeiro seja concedido ao especialista mais alto. Se houver menos emblemas do que o indicado por badgingLevels, o último emblema no storage preencherá o restante do storage. Exemplo de entrada:<br /> <code>/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png</code></td>
  </tr>
  <tr>
   <td>badgingLevels</td>
   <td>Longo</td>
   <td><em>(Opcional)</em> Especifica os níveis de especialização a atribuir. Por exemplo, se houver um <code>expert </code>e <code>almost expert</code> (dois símbolos), o valor deverá ser definido como 2. O badgingLevel deve corresponder ao número de imagens de crachá relacionadas a especialistas listadas para a propriedade badgingPath. O padrão é 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>Sequência de caracteres</td>
   <td><em>(Obrigatório)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Definido como "avançado"; caso contrário, o padrão é "básico".</td>
  </tr>
  <tr>
   <td>regras de pontuação</td>
   <td>Sequência de caracteres[]</td>
   <td><em>(Opcional)</em> Uma string de vários valores para restringir a regra de identificação aos eventos de pontuação identificados pelas regras de pontuação listadas.<br /> Exemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> O padrão não é restrição.</td>
  </tr>
 </tbody>
</table>

## Regras e selo incluídos {#included-rules-and-badge}

### Crachá incluído {#included-badge}

Incluído nesta versão beta, há um selo de especialista baseado em recompensa:

* `expert`

   `/libs/settings/community/badging/images/expert-badge/jcr:content/expert.png`

![chlimage_1-263](assets/chlimage_1-263.png)

Para que o selo do especialista apareça como recompensa pela atividades, verifique se:

* `Badges` são ativados para o recurso, como um fórum ou componente QnA.

* As regras avançadas de pontuação e marcação são aplicadas à página (ou ancestral) na qual o componente é colocado

Consulte as informações básicas para:

* [Ativar a identificação para um componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicação de regras](/help/communities/implementing-scoring.md#applytopage)

### Regras e sub-regras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Na versão beta estão incluídas duas regras de pontuação avançadas para a função [do](/help/communities/functions.md#forum-function) fórum (uma para cada componente do fórum e comentários do recurso do fórum):

1. `/libs/settings/community/scoring/rules/adv-comments-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule`

1. `/libs/settings/community/scoring/rules/adv-forums-scoring`

   * `subRules[] =
/libs/settings/community/scoring/rules/sub-rules/adv-forums-rule
/libs/settings/community/scoring/rules/sub-rules/adv-comments-rule
/libs/settings/community/scoring/rules/sub-rules/adv-voting-rule-owner`

**Notas:**

* Ambos `rules` e `sub-rules` nós são do tipo `cq:Page`.

* `subRules` é um atributo do tipo String[] no nó da regra `jcr:content` .

* `sub-rules` pode ser compartilhado entre várias regras de pontuação.

* `rules` deve estar localizado em um local de repositório com permissão de leitura para todos.

* Os nomes de regras devem ser exclusivos, independentemente da localização.

### Regras de marcação incluídas {#included-badging-rules}

Estão incluídas na versão duas regras avançadas de identificação que correspondem aos fóruns [avançados e às regras](#included-scoring-rules-and-sub-rules)de pontuação de comentários.

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` nós são do tipo cq:Page.
* `rules` deve estar localizado em um local de repositório com permissão de leitura para todos.
* Os nomes de regras devem ser exclusivos, independentemente da localização.

