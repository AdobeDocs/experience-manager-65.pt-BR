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
source-git-commit: 0a4aca939c564720f63f055e9522e56942eaa128
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 1%

---

# Pontuação avançada e medalhas{#advanced-scoring-and-badges}

## Visão geral {#overview}

A pontuação avançada permite a atribuição de medalhas para identificar membros como especialistas. A pontuação avançada atribui pontos com base na quantidade *e* qualidade do conteúdo criado por um membro, enquanto a pontuação básica atribui pontos com base na quantidade de conteúdo criado.

Essa diferença se deve ao mecanismo de pontuação usado para calcular as pontuações. O mecanismo de pontuação básico aplica matemática simples. O mecanismo de pontuação avançado é um algoritmo adaptável que recompensa os membros ativos que contribuem com conteúdo valioso e relevante, deduzido por meio do processamento de linguagem natural (NLP) de um tópico.

Além da relevância do conteúdo, os algoritmos de pontuação contabilizam as atividades dos membros, como votação e porcentagem de respostas. Embora a pontuação básica os inclua quantitativamente, a pontuação avançada os usa de forma algorítmica.

Portanto, o mecanismo de pontuação avançado requer dados suficientes para tornar a análise significativa. O limite de conquista para se tornar um especialista é constantemente reavaliado à medida que o algoritmo se ajusta continuamente ao volume e à qualidade do conteúdo criado. Existe também um conceito de *decaimento* de postagens mais antigas de um membro. Se um perito deixar de participar na matéria em que obteve o estatuto de perito, num determinado momento [configuração do mecanismo de pontuação](#configurable-scoring-engine)) podem perder o estatuto de perito.

Configurar a pontuação avançada é praticamente o mesmo que a pontuação básica:

* As regras básicas e avançadas de pontuação e medalha são [aplicado ao conteúdo](/help/communities/implementing-scoring.md#apply-rules-to-content) do mesmo modo.

   * Regras básicas e avançadas de pontuação e medalha podem ser aplicadas ao mesmo conteúdo.

* [Ativação de selos para componentes](/help/communities/implementing-scoring.md#enable-badges-for-component) é genérico.

As diferenças na configuração das regras de pontuação e medalha são:

* Mecanismo de pontuação avançado configurável
* Regras de pontuação avançadas:

   * `scoringType` definir como `advanced`
   * Exige `stopwords`

* Regras avançadas de medalha:

   * `badgingType` definir como `advanced`
   * `badgingLevels` definir como **número de níveis de especialistas a serem concedidos**
   * Exige `badgingPaths` matriz de selos em vez de limites, o mapeamento de matriz aponta para selos.

>[!NOTE]
>
>Para usar recursos avançados de pontuação e medalha, instale o [Pacote de identificação do especialista](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=%2Fcontent%2Fsoftware-distribution%2Fen%2Fdetails.html%2Fcontent%2Fdam%2Faem%2Fpublic%2Fadobe%2Fpackages%2Fcq610%2Fsocial%2Ffeaturepack%2Fcq-social-expert-identification-pkg).

## Mecanismo de pontuação configurável {#configurable-scoring-engine}

O mecanismo de pontuação avançado fornece uma configuração OSGi com parâmetros que afetam o algoritmo de pontuação avançado.

![mecanismo de pontuação avançado](assets/advanced-scoring-engine.png)

* **Pontuações e pesos**

  Para um tópico, especifique o verbo que deve ter a maior prioridade ao calcular a pontuação. Um ou mais tópicos podem ser inseridos, mas limitados a **um verbo por tópico**. Consulte [Tópicos e verbos](/help/communities/implementing-scoring.md#topics-and-verbs).
Inserido como `topic,verb` com a vírgula escapada. Por exemplo:
  `/social/forum/hbs/social/forum\,ADD`
O padrão é definido como ADICIONAR verbo para componentes de QnA e fórum.

* **Intervalo de pontuação**

  O intervalo das pontuações avançadas é definido por esse valor (pontuação máxima) e 0 (pontuação mais baixa possível).

  O valor padrão é 100, de modo que o intervalo de pontuação seja de 0 a 100.

* **Intervalo de tempo de decaimento da entidade**

  Esse parâmetro representa o número de horas após o qual todas as pontuações da entidade são decaídas. Isso é necessário para não incluir mais conteúdo antigo nas pontuações de um site da comunidade.

  O valor padrão é de 216.000 horas (~24 anos).

* **Pontuação da taxa de crescimento**
Isso especifica a pontuação entre 0 e o intervalo de pontuação, além do qual o crescimento diminui para limitar o número de especialistas.

  O valor padrão é 50.

## Regras de pontuação avançadas {#advanced-scoring-rules}

Na pontuação básica, a quantidade necessária para ganhar um selo é conhecida.

Na pontuação avançada, a quantidade necessária está sendo ajustada constantemente com base na quantidade de dados de qualidade no sistema. A pontuação é continuamente calculada de maneira semelhante a uma curva em forma de sino.

Se um membro ganhou uma medalha de especialista em um tópico que não está mais ativo, há a possibilidade de que ele perderá sua medalha devido à decadência ao longo do tempo.

### scoringType {#scoringtype}

Uma regra de pontuação é um conjunto de subregras de pontuação, cada uma das quais declara o `scoringType`.

Para chamar o mecanismo de pontuação avançado, a variável `scoringType`deve ser definido como `advanced`.

Consulte [Sub-regras de pontuação](/help/communities/implementing-scoring.md#scoring-sub-rules).

![tipo de pontuação avançada](assets/advanced-scoring-type.png)

### Palavras de interrupção {#stopwords}

O pacote de pontuação avançado instala uma pasta de configuração que contém um arquivo de palavras irrelevantes:

* `/libs/settings/community/scoring/configuration/stopwords`

O algoritmo de pontuação avançado usa a lista de palavras contidas no arquivo de palavras irrelevantes para identificar palavras comuns em inglês que são ignoradas durante o processamento de conteúdo.

Não há expectativa de que esse arquivo seja modificado.

Se o arquivo de palavras irrelevantes estiver ausente, o mecanismo de pontuação avançado emitirá um erro.

## Regras avançadas de insígnia {#advanced-badging-rules}

As propriedades avançadas da regra de atribuição de tags são diferentes das [propriedades básicas da regra de medalha](/help/communities/implementing-scoring.md#badging-rules).

Em vez de associar pontos a uma imagem de selo, é necessário apenas identificar o número de especialistas permitidos e a imagem de selo a ser premiada.

![advanced-badging-rules](assets/advanced-badging-rules.png)

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
   <td><em>(Opcional)</em> Especifica os níveis de experiência a serem atribuídos. Por exemplo, se houver uma variável <code>expert </code>e uma <code>almost expert</code> (duas medalhas), então o valor deve ser definido como 2. O badgingLevel deve corresponder ao número de imagens de selo relacionadas a especialistas listadas para a propriedade badgingPath. O padrão é 1.</td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>String</td>
   <td><em>(Obrigatório)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Defina como "avançado", caso contrário, o padrão será "básico".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String[]</td>
   <td><em>(Opcional)</em> Uma string de vários valores para restringir a regra de selo aos eventos de pontuação identificados por uma ou mais regras de pontuação listadas.<br /> Exemplo de entrada:<br /> <code>/libs/settings/community/scoring/rules/adv-comments-scoring</code><br /> O padrão é sem restrição.</td>
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

* `Badges` são ativados para o recurso, como um fórum ou componente QnA.

* As regras avançadas de pontuação e medalha são aplicadas à página (ou antecessora) em que o componente é colocado.

Consulte as informações básicas para:

* [Ativação de símbolo para um componente](/help/communities/implementing-scoring.md#enableforcomponent)
* [Aplicar regras](/help/communities/implementing-scoring.md#applytopage)

### Regras e sub-regras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Estão incluídas na versão beta duas regras de pontuação avançadas para o [função de fórum](/help/communities/functions.md#forum-function) (um para os componentes fórum e comentários do recurso fórum):

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

* Ambos `rules` e `sub-rules` os nós são do tipo `cq:Page`.
* `subRules` é um atributo do tipo String`[]` no campo de `jcr:content` nó.
* `sub-rules` podem ser compartilhados entre várias regras de pontuação.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos independentemente da localização.

### Regras de insígnia incluídas {#included-badging-rules}

Estão incluídas na versão duas regras avançadas de criação de tags que correspondem à [regras de pontuação de fóruns e comentários avançados](#included-scoring-rules-and-sub-rules).

* `/libs/settings/community/badging/rules/adv-comments-badging`
* `/libs/settings/community/badging/rules/adv-forums-badging`

**Notas:**

* `rules` Os nós são do tipo cq:Page.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.
* Os nomes das regras devem ser exclusivos independentemente da localização.
