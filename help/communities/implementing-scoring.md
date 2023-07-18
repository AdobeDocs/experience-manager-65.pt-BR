---
title: Pontuação e medalhas das comunidades
description: A pontuação e as medalhas do AEM Communities permitem identificar e recompensar os membros da comunidade
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
tagskeywords: scoring, badging, badges, gamification
role: Admin
exl-id: 4aa857f7-d111-4548-8f03-f6d6c27acf51
source-git-commit: d3c40d1452217983b01245ec1c81111a3c4e7295
workflow-type: tm+mt
source-wordcount: '2853'
ht-degree: 2%

---

# Pontuação e medalhas das comunidades {#communities-scoring-and-badges}

## Visão geral {#overview}

O recurso de pontuação e medalhas do AEM Communities oferece a capacidade de identificar e premiar membros da comunidade.

Os principais aspectos de pontuação e medalhas são:

* [Atribuir medalhas](#assign-and-revoke-badges) para identificar a função de um membro na comunidade.

* [Atribuição básica de medalhas](#enable-scoring) aos membros para incentivar a sua participação (quantidade de conteúdo criado).

* [Atribuição avançada de medalhas](/help/communities/advanced.md) para identificar membros como especialistas (qualidade do conteúdo criado).

**Nota** que a atribuição de medalhas é [não ativado por padrão](/help/communities/implementing-scoring.md#main-pars-text-237875536).

>[!CAUTION]
>
>A estrutura de implementação visível no CRXDE Lite está sujeita a alterações assim que a interface do usuário estiver disponível.

## Selos {#badges}

As medalhas são colocadas sob o nome de um membro para indicar seu papel ou sua posição na comunidade. Os emblemas podem ser exibidos como uma imagem ou como um nome. Quando exibido como uma imagem, o nome é incluído como texto alternativo para acessibilidade.

Por padrão, os selos estão no repositório no seguinte local:

* `/libs/settings/community/badging/images`

Se armazenadas em um local diferente, elas devem ser lidas e acessíveis a todos.

As medalhas são diferenciadas em UGC, sejam elas atribuídas ou ganhas de acordo com as regras. Atualmente, as medalhas atribuídas são exibidas como texto e as medalhas obtidas são exibidas como uma imagem.

### Interface do usuário de gerenciamento de selos {#badge-management-ui}

As Comunidades [Console de selos](/help/communities/badges.md) permite adicionar medalhas personalizadas que podem ser exibidas para um membro quando ganho (premiado) ou quando ele assume uma função específica na comunidade (atribuído).

### Medalhas atribuídas {#assigned-badges}

As medalhas baseadas em função são atribuídas por um administrador aos membros da comunidade com base em sua função na comunidade.

Os emblemas atribuídos (e concedidos) são armazenados no [SRP](/help/communities/srp.md) e não estão diretamente acessíveis. Até que uma GUI esteja disponível, o único meio de atribuir emblemas baseados em função é fazê-lo com código ou cURL. Para obter instruções sobre cURL, consulte a seção intitulada [Atribuir e revogar selos](#assign-and-revoke-badges).

Estão incluídos na versão três selos com base em funções:

* **moderador**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gerente de grupo**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiado**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![selos atribuídos](assets/assigned-badges.png)

### Medalhas premiadas {#awarded-badges}

Os emblemas baseados em recompensas são concedidos pelo serviço de pontuação aos membros da comunidade com base nas regras aplicadas à atividade na comunidade.

Para que os selos apareçam como uma recompensa por atividade, há duas coisas que devem acontecer:

* A insígnia deve ser [habilitado](#enableforcomponent) para o componente de recurso.
* As regras de pontuação e medalha devem ser [aplicado](#applytopage) à página (ou antecessora) em que o componente é colocado.

Estão incluídos na versão três medalhas com base em recompensa:

* **ouro**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **prata**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronze**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![medalhas concedidas](assets/awarded-badges.png)

>[!NOTE]
>
>As regras de pontuação podem ser configuradas para atribuir pontos negativos para postagens sinalizadas como inadequadas e, portanto, afetar o valor da pontuação. No entanto, uma vez que um selo é ganho, ele não será removido automaticamente devido à redução do ponto de pontuação ou a alterações nas regras de pontuação.
>
>As medalhas concedidas podem ser revogadas da mesma maneira que as medalhas atribuídas. Consulte a [Atribuir e revogar selos](#assign-and-revoke-badges) seção. Os aprimoramentos futuros incluirão uma interface para gerenciar os emblemas dos membros.

### Medalhas personalizadas {#custom-badges}

Os emblemas personalizados podem ser instalados usando o [Console de selos](/help/communities/badges.md) e atribuído ou especificado nas regras de medalha.

Quando instalados no console Selos, os selos personalizados são replicados automaticamente para o ambiente de publicação.

## Ativar pontuação {#enable-scoring}

A pontuação não está ativada por padrão. As etapas básicas para configurar e ativar a pontuação e a atribuição de medalhas são:

* Identificar regras para pontos de ganhos ([regras de pontuação](#scoring-rules)).
* Para pontos acumulados por regras de pontuação, atribua [medalhas](#badges) ([regras de medalha](#badging-rules)).

* [Aplicar as regras de pontuação e medalha a um site da comunidade](#apply-rules-to-content).
* [Ativar medalha para recursos da comunidade](#enable-badges-for-component).

Consulte a [Teste rápido](#quick-test) para ativar a pontuação para um site da comunidade usando as regras padrão de pontuação e selo para fóruns e comentários.

### Aplicar regras ao conteúdo {#apply-rules-to-content}

Para ativar a pontuação e os selos, adicione as propriedades `scoringRules` e `badgingRules` para qualquer nó na árvore de conteúdo do site.

Se o site já estiver publicado, depois de aplicar todas as regras e ativar os componentes, publique novamente o site.

As regras que se aplicam a um componente habilitado para marcação são aquelas do nó atual ou de seu antecessor.

Se o nó for do tipo `cq:Page` (recomendado), em seguida, usando o CRXDE|Lite, adicione as propriedades à `jcr:content` nó.

| **Propriedade** | **Tipo** | **Descrição** |
|---|---|---|
| badgingRules | String | uma lista de matriz de [regras de medalha](#badging-rules) |
| scoringRules | String | uma lista de matriz de [regras de pontuação](#scoring-rules) |

>[!NOTE]
>
>Se uma regra de pontuação parecer não ter efeito na atribuição de medalhas, verifique se a regra de pontuação não foi bloqueada pela propriedade scoringRules da regra de medalha. Consulte a seção intitulada [Regras de insígnia](#badging-rules).

### Ativar selos para componente {#enable-badges-for-component}

As regras de pontuação e faixas estão em vigor somente para instâncias de componentes que ativaram a marcação editando a configuração do componente no [modo de criação](/help/communities/author-communities.md).

Uma propriedade booleana, `allowBadges`, ativa/desativa a exibição de selos para uma instância de componente. É configurável na variável [caixa de diálogo editar componente](/help/communities/author-communities.md) para componentes de fórum, QnA e comentário por meio de uma caixa de seleção rotulada **Exibir selos**.

#### Exemplo: allowBadges para a instância do componente do Fórum {#example-allowbadges-for-forum-component-instance}

![enable-badges-component](assets/enable-badges-component.png)

>[!NOTE]
>
>Qualquer componente pode ser sobreposto para exibir emblemas usando o código HBS encontrado em fóruns, QnA e comentários como exemplo.

## Regras de pontuação {#scoring-rules}

As regras de pontuação são a base da pontuação para a atribuição de medalhas.

Cada regra de pontuação é uma lista de uma ou mais subregras. As regras de pontuação são aplicadas ao conteúdo do site da comunidade para identificar as regras a serem aplicadas quando os selos estiverem ativados.

As regras de pontuação são herdadas, mas não aditivas. Por exemplo:

* Se a página2 contiver a regra de pontuação 2 e sua página1 antecessora contiver a regra de pontuação 1.
* Uma ação em um componente página2 chama a regra 1 e a regra 2.
* Se ambas as regras contiverem subregras aplicáveis para a mesma `topic/verb`:

   * Somente a subregra da regra 2 afeta a pontuação.
   * As pontuações de ambas as subregras não são adicionadas.

Quando houver mais de uma regra de pontuação, as pontuações serão mantidas separadamente para cada regra.

As regras de pontuação são nós do tipo `cq:Page` com propriedades em seu `jcr:content` nó que especifica a lista de subregras que a definem.

As pontuações são armazenadas no SRP.

>[!NOTE]
>
>Prática recomendada: nomear cada regra de pontuação de maneira exclusiva.
>
>Os nomes das regras de pontuação devem ser globalmente exclusivos; eles não devem terminar com o mesmo nome.
>
>Um exemplo do que *não* fazer:
>
>/libs/settings/community/scoring/rules/site1/forums-scoring
>/libs/settings/community/scoring/rules/site2/forums-scoring

### Sub-regras de pontuação {#scoring-sub-rules}

As subregras de pontuação contêm as propriedades que detalham os valores para participar da comunidade.

Cada subregra de pontuação identifica:

* Quais atividades estão sendo rastreadas?
* Que função comunitária específica está envolvida?
* Quantos pontos são concedidos?

Por padrão, os pontos são atribuídos ao membro que está executando a ação, a menos que a subregra especifique o proprietário do conteúdo como destinatário dos pontos ( `forOwner`).

Cada subregra pode ser incluída em uma ou mais regras de pontuação.

O nome da subregra normalmente segue o padrão de uso de um *assunto*, *objeto*, e *verbo*. Por exemplo:

* member-comment-create
* membro-recebe-voto

As sub-regras são nós do tipo `cq:Page` com propriedades em seu `jcr:content`nó que especifica a [verbos e tópicos](#topics-and-verbs) .

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Tipo</th>
   <th> Valor Descrição</th>
  </tr>
  <tr>
   <td><i><code>VERB</code></i></td>
   <td>Longo</td>
   <td>
    <ul>
     <li>obrigatório; o verbo corresponde a uma ação de evento</li>
     <li>deve haver pelo menos uma propriedade de verbo</li>
     <li>o verbo deve ser inserido totalmente em MAIÚSCULAS</li>
     <li>pode haver várias propriedades de verbo, mas nenhuma duplicata</li>
     <li>o valor é a pontuação a ser aplicada para esse evento</li>
     <li>o valor pode ser positivo ou negativo</li>
     <li>uma lista de verbos suportados na versão está na variável <a href="#topics-and-verbs">Tópicos e verbos</a> seção</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>String</td>
   <td>
    <ul>
     <li>opcional; restringe a subregra aos componentes da comunidade identificados por tópicos do evento</li>
     <li>se especificado : o valor é uma cadeia de caracteres de vários valores de tópicos de evento</li>
     <li>uma lista de tópicos da versão está na <a href="#topics-and-verbs">Tópicos e verbos</a> seção</li>
     <li>o padrão é aplicar a todos os tópicos associados aos verbos</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>forOwner</code></td>
   <td>Booleano</td>
   <td>
    <ul>
     <li>opcional; não relevante quando o membro está agindo em seu conteúdo</li>
     <li>se verdadeiro, aplicar pontuação ao proprietário do conteúdo sobre o qual está sendo atuado</li>
     <li>se for falso, aplicar pontuação ao membro que está executando a ação</li>
     <li>o padrão é falso</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>scoringType</code></td>
   <td>String</td>
   <td>
    <ul>
     <li>opcional; identifica o mecanismo de pontuação</li>
     <li>se "básico", especifica o mecanismo de pontuação com base na quantidade
      <ul>
       <li>incluído na versão</li>
      </ul> </li>
     <li>se "avançado", especifica o mecanismo de pontuação com base na qualidade e na quantidade
      <ul>
       <li>exige um <a href="/help/communities/advanced.md">pacote extra</a></li>
      </ul> </li>
     <li>o padrão é "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Regras e sub-regras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Estão incluídas na versão duas regras de pontuação para o [Função do fórum](/help/communities/functions.md#forum-function) (um para os componentes Fórum e Comentários do recurso Fórum):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-comment-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] = /libs/settings/community/scoring/rules/sub-rules/member-forum-create /libs/settings/community/scoring/rules/sub-rules/member-receive-vote /libs/settings/community/scoring/rules/sub-rules/member-give-vote /libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Notas:**

* Ambos `rules` e `sub-rules` Os nós são do tipo cq:Page.

* `subRules` é um atributo do tipo String[] no campo de `jcr:content` nó.

* `sub-rules` podem ser compartilhados entre várias regras de pontuação.
* `rules` O deve estar localizado em um local de repositório com permissão de leitura para todos.

   * Os nomes das regras devem ser exclusivos independentemente da localização.

### Ativação de regras de pontuação personalizadas {#activating-custom-scoring-rules}

Quaisquer alterações ou adições feitas às regras de pontuação ou subregras feitas no ambiente de criação devem ser instaladas na publicação.

## Regras de insígnia {#badging-rules}

As regras de atribuição de emblemas vinculam regras de pontuação aos emblemas especificando:

* Regra de pontuação
* Pontuação necessária para receber um selo específico

As regras de insígnia são nós do tipo `cq:Page` com propriedades em seu `jcr:content` nó que correlaciona regras de pontuação a pontuações e selos.

As regras para a aposição de `thresholds` propriedade que é uma lista ordenada de pontuações mapeadas aos selos. As pontuações devem ser ordenadas em valor crescente. Por exemplo:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Uma medalha de bronze é concedida por ganhar um ponto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Um emblema de prata é concedido quando 60 pontos foram acumulados.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Um selo de ouro é concedido quando 80 pontos foram acumulados.

As regras de insígnia são combinadas às regras de pontuação, que determinam como os pontos se acumulam. Consulte a seção intitulada [Aplicar regras ao conteúdo](#apply-rules-to-content).

A variável `scoringRules` em uma regra de notificação, o simplesmente restringe quais regras de pontuação podem ser emparelhadas com essa regra de notificação específica.

>[!NOTE]
>
>Prática recomendada : criar imagens de selo exclusivas para cada site de AEM.

![badging-rule-configuration](assets/badging-rule-configuration.png)

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Tipo</th>
   <th>Valor Descrição</th>
  </tr>
  <tr>
   <td>limites</td>
   <td>String</td>
   <td><em>(obrigatório)</em> Uma cadeia de caracteres de vários valores no formato 'número|caminho'
    <ul>
     <li>número = pontuação</li>
     <li>| = sinal de linha vertical (U+007C)</li>
     <li>caminho = caminho completo para o recurso de imagem do selo</li>
    </ul> As cadeias de caracteres devem ser ordenadas de modo que os números aumentem em valor e nenhum espaço em branco deva aparecer entre o número e o caminho.<br /> Exemplo de entrada:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>String</td>
   <td><em>(opcional)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Se o mecanismo de pontuação avançado for desejado, consulte <a href="/help/communities/advanced.md">Pontuação avançada e medalhas</a>. O padrão é "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String</td>
   <td>(<em>opcional</em>) Uma string de vários valores para restringir a regra de classificação a eventos de pontuação identificados pelas regras de classificação</td>
  </tr>
 </tbody>
</table>

### Regras de insígnia incluídas {#included-badging-rules}

Estão incluídas na versão duas regras de insígnia que correspondem à [Regras de pontuação de fóruns e comentários](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Notas:**

* `rules` Os nós são do tipo cq:Page.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.

   * Os nomes das regras devem ser exclusivos independentemente da localização.

### Ativação das regras personalizadas de marcação {#activating-custom-badging-rules}

Quaisquer alterações ou adições feitas às regras de marcação ou imagens feitas no ambiente de criação devem ser instaladas na publicação.

## Atribuir e revogar selos {#assign-and-revoke-badges}

Os emblemas podem ser atribuídos aos membros usando o [console de membros](/help/communities/members.md#badges-tab) ou programaticamente usando comandos cURL.

Os seguintes comandos cURL mostram o que é necessário para uma solicitação HTTP para atribuir e revogar selos. O formato básico é:

cURL -i -X POST -H *cabeçalho* -u *fazer logon* -F *operação* -F *selo* *member-profile-url*

*cabeçalho* = cabeçalho personalizado &quot;Accept:application/json&quot; para passar para o servidor (obrigatório)

*fazer logon* = administrator-id:password por exemplo : admin:admin

*operação* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*selo* = &quot;badgeContentPath=*badge-image-file*&quot;

*badge-image-file* = o local do arquivo de imagem do selo no repositório, por exemplo : /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = o endpoint do perfil do membro em publicar, por exemplo: https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>A variável *member-profile-url*:
>
>* Pode se referir a uma instância de autor se a variável [Serviço de túnel](/help/communities/users.md#tunnel-service) está ativado.
>* Pode ser um nome obscuro e aleatório - consulte [Lista de verificação de segurança](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) em relação à ID autorizável.

### Exemplos: {#examples}

#### Atribuir um selo de moderador {#assign-a-moderator-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

#### Revogar um selo prateado atribuído {#revoke-an-assigned-silver-badge}

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:deleteBadge" -F "badgeContentPath=/libs/settings/community/badging/images/silver/jcr:content/silver.png" /home/users/community/updcs9DndLEI74DB9zsB/profile.social.json
```

>[!NOTE]
>
>O uso de cURL para atribuir e revogar selos funciona para qualquer imagem de selo, mas quando atribuído em vez de ganho, eles são marcados como selos atribuídos e manipulados adequadamente.

## Pontuação e selos para componentes personalizados {#scoring-and-badges-for-custom-components}

As regras de pontuação e medalha podem ser criadas para componentes personalizados associando os tópicos do evento criados para o componente com verbos.

## Tópicos e verbos {#topics-and-verbs}

Quando os membros interagem com os recursos de comunidades, são enviados eventos que podem acionar ouvintes assíncronos, como notificações e pontuação.

A instância SocialEvent de um componente registra os eventos como `actions` que ocorrem por um `topic`. O SocialEvent inclui um método para retornar um `verb` associada à ação. Existe uma *n-1* relação entre `actions` e `verbs`.

Para os componentes de comunidades entregues, as tabelas a seguir descrevem a `verbs` definido para cada `topic` disponível para uso no [subregras de pontuação](#scoring-sub-rules).

>[!NOTE]
>
>Uma nova propriedade booleana, `allowBadges`, ativa/desativa a exibição de selos para uma instância de componente. Pode ser configurado na versão atualizada [caixas de diálogo de edição de componente](/help/communities/author-communities.md) por meio de uma caixa de seleção rotulada **Exibir selos**.

**[Componente de calendário](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria um evento de calendário |
| ADICIONAR | comentários de membros em um evento de calendário |
| ATUALIZAR | comentário ou evento de calendário do membro editado |
| EXCLUIR | o evento de calendário ou comentário do membro foi excluído |

**[Componente de comentários](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria um comentário |
| ADICIONAR | membro responde ao comentário |
| ATUALIZAR | comentário do membro editado |
| EXCLUIR | comentário do membro excluído |

**[Componente da biblioteca de arquivos](/help/communities/file-library.md)**
SocialEvent `topic`= com/adobe/cq/social/fileLibrary

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria uma pasta |
| ANEXE | membro carrega um arquivo |
| ATUALIZAR | membro atualiza uma pasta ou arquivo |
| EXCLUIR | membro exclui uma pasta ou arquivo |

**[Componente do fórum](/help/communities/forum.md)**
SocialEvent `topic`= com/adobe/cq/social/forum

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria tópico de fórum |
| ADICIONAR | respostas dos membros ao tópico do fórum |
| ATUALIZAR | o tópico ou a resposta do fórum do membro for editado |
| EXCLUIR | o tópico ou a resposta do fórum do membro for excluído |

**[Componente do diário](/help/communities/blog-feature.md)**
SocialEvent `topic`= com/adobe/cq/social/journal

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria um artigo de blog |
| ADICIONAR | comentários de membros em um artigo de blog |
| ATUALIZAR | artigo ou comentário do blog do membro editado |
| EXCLUIR | artigo ou comentário do blog do membro excluído |

**[Componente de QnA](/help/communities/working-with-qna.md)**
SocialEvent `topic` = com/adobe/cq/social/qna

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria uma pergunta QnA |
| ADICIONAR | membro cria uma resposta QnA |
| ATUALIZAR | a pergunta ou resposta QnA do membro é editada |
| SELECIONE | a resposta do membro está selecionada |
| DESMARCAR | a resposta do membro foi desmarcada |
| EXCLUIR | A pergunta ou resposta QnA do membro é excluída |

**[Componente de análises](/help/communities/reviews.md)**
SocialEvent `topic`= com/adobe/cq/social/review

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria revisão |
| ATUALIZAR | revisão do membro editada |
| EXCLUIR | revisão do membro excluída |

**[Componente de classificação](/help/communities/rating.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/rating

| **Verbo** | **Descrição** |
|---|---|
| ADICIONAR CLASSIFICAÇÃO | o conteúdo do membro foi avaliado em alta |
| REMOVER CLASSIFICAÇÃO | o conteúdo do membro foi classificado como inativo |

**[Componente de votação](/help/communities/voting.md)**
SocialEvent `topic`= com/adobe/cq/social/tally/voting

| **Verbo** | **Descrição** |
|---|---|
| ADICIONAR VOTAÇÃO | o conteúdo do membro foi aprovado |
| REMOVER VOTAÇÃO | o conteúdo do membro foi rejeitado |

**Componentes habilitados para moderação**
SocialEvent `topic`= com/adobe/cq/social/moderation

| **Verbo** | **Descrição** |
|---|---|
| NEGAR | conteúdo do membro negado |
| SINALIZAR COMO INADEQUADO | o conteúdo do membro está sinalizado |
| NÃO SINALIZAR COMO INAPROPRIADO | o conteúdo do membro não está sinalizado |
| ACCEPT | o conteúdo do membro é aprovado pelo moderador |
| FECHAR | membro fecha comentário para edições e respostas |
| ABRIR | membro reabre comentário |

### Eventos de componente personalizados {#custom-component-events}

Para um componente personalizado, um SocialEvent é instanciado para registrar os eventos do componente como `actions` que ocorrem por um `topic`.

Para suportar pontuação, o SocialEvent precisa substituir o método `getVerb()` de modo a que um `verb` é retornado para cada `action`. A variável `verb` retornados para uma ação podem ser aqueles normalmente usados (como `POST`) ou uma especializada para o componente (como `ADD RATING`). Existe uma *n-1* relação entre `actions` e `verbs`.

## Resolução de problemas {#troubleshooting}

### As medalhas não aparecem {#badges-are-not-appearing}

Se as regras de pontuação e medalha tiverem sido aplicadas ao conteúdo do site, mas as medalhas não estiverem sendo concedidas para nenhuma atividade, verifique se as medalhas foram ativadas para a instância desse componente.

Consulte [Ativar selos para componente](#enable-badges-for-component).

### A regra de pontuação não tem efeito {#scoring-rule-has-no-effect}

Se as regras de pontuação e medalha tiverem sido aplicadas ao conteúdo do site, e as medalhas estiverem sendo concedidas para algumas ações, mas não outras, verifique se a regra de medalha não restringiu as regras de pontuação às quais se aplica.

Consulte a `scoringRules` propriedade de [Regras de insígnia](#badging-rules).

### Erro de digitação que diferencia maiúsculas de minúsculas {#case-sensitive-typo}

A maioria das propriedades e valores, especialmente os verbos, fazem distinção entre maiúsculas e minúsculas. Todos os verbos devem estar em MAIÚSCULAS quando usados em uma subregra de pontuação.

Se o recurso não estiver funcionando como esperado, verifique se os dados foram inseridos corretamente.

## Teste rápido {#quick-test}

É possível tentar rapidamente a pontuação e o badging usando o [Tutorial de introdução](/help/communities/getting-started.md) (engajar) local:

* Acessar CRXDE Lite no autor.
* Navegue até a página base:

   * /content/sites/engage/en/jcr:content

* Adicione a propriedade badgingRules:

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Selecionar **Multi**
   * Selecionar **Adicionar**
   * Insira `/libs/settings/community/badging/rules/forums-badging`
   * Selecionar **+**
   * Insira `/libs/settings/community/badging/rules/comments-badging`
   * Selecionar **OK**

* Adicione a propriedade scoringRules:

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Selecionar **Multi**
   * Selecionar **Adicionar**
   * Insira `/libs/settings/community/scoring/rules/forums-scoring`
   * Selecionar **+**
   * Insira `/libs/settings/community/scoring/rules/comments-scoring`
   * Selecionar **OK**

* Selecionar **Salvar tudo**.

![test-scoring-badging](assets/test-scoring-badging.png)

Em seguida, verifique se os componentes do fórum e dos comentários permitem que os emblemas sejam exibidos:

* Novamente usando o CRXDE Lite.
* Navegue até o componente do fórum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Adicione a propriedade booleana allowBadges, se necessário, e verifique se ela é verdadeira.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

![test-forum-component](assets/test-forum-component.png)

Em seguida, [republicar](/help/communities/sites-console.md#publishing-the-site) site da comunidade.

Finalmente,

* Navegue até o componente na instância de publicação.
* Faça logon como um membro da comunidade (por exemplo: weston.mccall@dodgit.com / senha).
* Publique um novo tópico do fórum.
* A página deve ser atualizada para que o selo seja exibido.

   * Faça logoff e logon como um membro da comunidade diferente (por exemplo: aaron.mcdonald@mailinator.com/password).

* Selecione o Fórum.

Isso deve dar ao membro da comunidade um selo de bronze visível com sua publicação no fórum, devido ao primeiro limite da regra de classificação em fóruns ser uma pontuação de 1.

![bronzebadge](assets/bronzebadge.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos de pontuação e medalhas](/help/communities/configure-scoring.md) página para desenvolvedores.

Para obter informações sobre o mecanismo de pontuação avançado, consulte [Pontuação avançada e medalhas](/help/communities/advanced.md).

O quadro de classificação configurável [componente](/help/communities/enabling-leaderboard.md) e [função](/help/communities/functions.md#leaderboard-function) simplifica a exibição de membros e suas pontuações em um site da comunidade.
