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
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2856'
ht-degree: 1%

---

# Pontuação e medalhas das comunidades {#communities-scoring-and-badges}

## Visão geral {#overview}

O recurso de pontuação e medalhas do AEM Communities oferece a capacidade de identificar e premiar membros da comunidade.

Os principais aspectos de pontuação e medalhas são:

* [Atribuir medalhas](#assign-and-revoke-badges) para identificar a função de um membro na comunidade.

* [Atribuição básica de medalhas](#enable-scoring) aos membros para incentivar sua participação (quantidade de conteúdo criado).

* [Atribuição avançada de medalhas](/help/communities/advanced.md) para identificar membros como especialistas (qualidade do conteúdo criado).

**Observe** que a atribuição de medalhas é [não habilitada por padrão](/help/communities/implementing-scoring.md#main-pars-text-237875536).

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

O [console de Medalhas](/help/communities/badges.md) das Comunidades permite adicionar medalhas personalizadas que podem ser exibidas para um membro quando ganho (premiado) ou quando ele assume uma função específica na comunidade (atribuído).

### Medalhas atribuídas {#assigned-badges}

As medalhas baseadas em função são atribuídas por um administrador aos membros da comunidade com base em sua função na comunidade.

Os emblemas atribuídos são armazenados no [SRP](/help/communities/srp.md) selecionado e não são diretamente acessíveis. Até que uma GUI esteja disponível, o único meio de atribuir emblemas baseados em função é fazê-lo com código ou cURL. Para obter instruções sobre cURL, consulte a seção denominada [Atribuir e revogar selos](#assign-and-revoke-badges).

Estão incluídos na versão três selos com base em funções:

* **moderador**
  `/libs/settings/community/badging/images/moderator/jcr:content/moderator.png`

* **gerente do grupo**
  `/libs/settings/community/badging/images/group-manager/jcr:content/group-manager.png`

* **membro privilegiado**
  `/libs/settings/community/badging/images/privileged-member/jcr:content/privileged-member.png`

  ![selos atribuídos](assets/assigned-badges.png)

### Medalhas premiadas {#awarded-badges}

Os emblemas baseados em recompensas são concedidos pelo serviço de pontuação aos membros da comunidade com base nas regras aplicadas à atividade na comunidade.

Para que os selos apareçam como uma recompensa por atividade, há duas coisas que devem acontecer:

* A medalha deve ser [habilitada](#enableforcomponent) para o componente de recurso.
* As regras de pontuação e medalha devem ser [aplicadas](#applytopage) à página (ou antecessora) em que o componente é colocado.

Estão incluídos na versão três medalhas com base em recompensa:

* **ouro**
  `/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

* **prata**
  `/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

* **bronze**
  `/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

  ![medalhas-premiadas](assets/awarded-badges.png)

>[!NOTE]
>
>As regras de pontuação podem ser configuradas para atribuir pontos negativos para postagens sinalizadas como inadequadas e, portanto, afetar o valor da pontuação. No entanto, uma vez que um selo é ganho, ele não será removido automaticamente devido à redução do ponto de pontuação ou a alterações nas regras de pontuação.
>
>As medalhas concedidas podem ser revogadas da mesma maneira que as medalhas atribuídas. Consulte a seção [Atribuir e revogar medalhas](#assign-and-revoke-badges). Os aprimoramentos futuros incluirão uma interface para gerenciar os emblemas dos membros.

### Medalhas personalizadas {#custom-badges}

É possível instalar selos personalizados usando o [console de selos](/help/communities/badges.md) e atribuídos ou especificados nas regras de selos.

Quando instalados no console Selos, os selos personalizados são replicados automaticamente para o ambiente de publicação.

## Ativar pontuação {#enable-scoring}

A pontuação não está ativada por padrão. As etapas básicas para configurar e ativar a pontuação e a atribuição de medalhas são:

* Identificar regras para pontos de ganhos ([regras de pontuação](#scoring-rules)).
* Para pontos acumulados por regras de pontuação, atribua [medalhas](#badges) ([regras de medalha](#badging-rules)).

* [Aplique as regras de pontuação e medalha a um site da comunidade](#apply-rules-to-content).
* [Habilitar a marca para os recursos da comunidade](#enable-badges-for-component).

Consulte a seção [Teste rápido](#quick-test) para habilitar a pontuação para um site da comunidade usando as regras padrão de pontuação e medalha para fóruns e comentários.

### Aplicar regras ao conteúdo {#apply-rules-to-content}

Para habilitar a pontuação e os selos, adicione as propriedades `scoringRules` e `badgingRules` a qualquer nó na árvore de conteúdo do site.

Se o site já estiver publicado, depois de aplicar todas as regras e ativar os componentes, publique novamente o site.

As regras que se aplicam a um componente habilitado para marcação são aquelas do nó atual ou de seu antecessor.

Se o nó for do tipo `cq:Page` (recomendado), usando CRXDE|Lite, adicione as propriedades ao nó `jcr:content`.

| **Propriedade** | **Tipo** | **Descrição** |
|---|---|---|
| badgingRules | String | uma lista de matriz de [regras de medalha](#badging-rules) |
| scoringRules | String | uma lista de matriz de [regras de pontuação](#scoring-rules) |

>[!NOTE]
>
>Se uma regra de pontuação parecer não ter efeito na atribuição de medalhas, verifique se a regra de pontuação não foi bloqueada pela propriedade scoringRules da regra de medalha. Consulte a seção intitulada [Regras para atribuição de insígnias](#badging-rules).

### Ativar selos para componente {#enable-badges-for-component}

As regras de pontuação e faixas estão em vigor somente para instâncias de componentes que habilitaram a medalha editando a configuração do componente no [modo de criação](/help/communities/author-communities.md).

Uma propriedade booleana, `allowBadges`, habilita/desabilita a exibição de emblemas para uma instância de componente. Ele pode ser configurado na [caixa de diálogo de edição do componente](/help/communities/author-communities.md) para os componentes de fórum, QnA e comentário por meio de uma caixa de seleção rotulada **Exibir Selos**.

#### Exemplo: allowBadges para a instância do componente do Fórum {#example-allowbadges-for-forum-component-instance}

![ativar-medalhas-componente](assets/enable-badges-component.png)

>[!NOTE]
>
>Qualquer componente pode ser sobreposto para exibir emblemas usando o código HBS encontrado em fóruns, QnA e comentários como exemplo.

## Regras de pontuação {#scoring-rules}

As regras de pontuação são a base da pontuação para a atribuição de medalhas.

Cada regra de pontuação é uma lista de uma ou mais subregras. As regras de pontuação são aplicadas ao conteúdo do site da comunidade para identificar as regras a serem aplicadas quando os selos estiverem ativados.

As regras de pontuação são herdadas, mas não aditivas. Por exemplo:

* Se a página2 contiver a regra de pontuação 2 e sua página1 antecessora contiver a regra de pontuação 1.
* Uma ação em um componente página2 chama a regra 1 e a regra 2.
* Se ambas as regras contiverem subregras aplicáveis para o mesmo `topic/verb`:

   * Somente a subregra da regra 2 afeta a pontuação.
   * As pontuações de ambas as subregras não são adicionadas.

Quando houver mais de uma regra de pontuação, as pontuações serão mantidas separadamente para cada regra.

As regras de pontuação são nós do tipo `cq:Page` com propriedades em seu nó `jcr:content` que especificam a lista de subregras que a definem.

As pontuações são armazenadas no SRP.

>[!NOTE]
>
>Prática recomendada: nomear cada regra de pontuação de maneira exclusiva.
>
>Os nomes das regras de pontuação devem ser globalmente exclusivos; eles não devem terminar com o mesmo nome.
>
>Um exemplo do que *não* deve fazer:
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

O nome da subregra geralmente segue o padrão de uso de um *assunto*, *objeto* e *verbo*. Por exemplo:

* member-comment-create
* membro-recebe-voto

Subregras são nós do tipo `cq:Page` com propriedades em seu nó `jcr:content` que especificam os [verbos e tópicos](#topics-and-verbs).

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
     <li>uma lista de verbos com suporte nesta versão está na seção <a href="#topics-and-verbs">Tópicos e Verbos</a></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>topics</code></td>
   <td>String</td>
   <td>
    <ul>
     <li>opcional; restringe a subregra aos componentes da comunidade identificados por tópicos do evento</li>
     <li>se especificado : o valor é uma cadeia de caracteres de vários valores de tópicos de evento</li>
     <li>uma lista de tópicos da versão está na seção <a href="#topics-and-verbs">Tópicos e Verbos</a></li>
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
       <li>requer um <a href="/help/communities/advanced.md">pacote extra</a></li>
      </ul> </li>
     <li>o padrão é "basic"</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### Regras e sub-regras de pontuação incluídas {#included-scoring-rules-and-sub-rules}

Estão incluídas na versão duas regras de pontuação para a [Função do fórum](/help/communities/functions.md#forum-function) (uma para os componentes Fórum e Comentários do recurso Fórum):

1. /libs/settings/community/scoring/rules/comments-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-comment-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-give-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

1. /libs/settings/community/scoring/rules/forums-scoring

   * subRules[] =
/libs/settings/community/scoring/rules/sub-rules/member-forum-create
/libs/settings/community/scoring/rules/sub-rules/member-receive-vote
/libs/settings/community/scoring/rules/sub-rules/member-give-vote
/libs/settings/community/scoring/rules/sub-rules/member-is-moderated

**Notas:**

* Os nós `rules` e `sub-rules` são do tipo cq:Page.

* `subRules` é um atributo do tipo Cadeia de Caracteres [] no nó `jcr:content` da regra.

* `sub-rules` pode ser compartilhado entre várias regras de pontuação.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.

   * Os nomes das regras devem ser exclusivos independentemente da localização.

### Ativação de regras de pontuação personalizadas {#activating-custom-scoring-rules}

Quaisquer alterações ou adições feitas às regras de pontuação ou subregras feitas no ambiente de criação devem ser instaladas na publicação.

## Regras de insígnia {#badging-rules}

As regras de atribuição de emblemas vinculam regras de pontuação aos emblemas especificando:

* Regra de pontuação
* Pontuação necessária para receber um selo específico

As regras de atribuição de emblemas são nós do tipo `cq:Page` com propriedades em seu nó `jcr:content` que correlacionam regras de pontuação a pontuações e emblemas.

As regras para medalha consistem em uma propriedade obrigatória `thresholds`, que é uma lista ordenada de pontuações mapeadas para medalhas. As pontuações devem ser ordenadas em valor crescente. Por exemplo:

* `1|/libs/settings/community/badging/images/bronze-badge/jcr:content/bronze.png`

   * Uma medalha de bronze é concedida por ganhar um ponto.

* `60|/libs/settings/community/badging/images/silver-badge/jcr:content/silver.png`

   * Um emblema de prata é concedido quando 60 pontos foram acumulados.

* `80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png`

   * Um selo de ouro é concedido quando 80 pontos foram acumulados.

As regras de insígnia são combinadas às regras de pontuação, que determinam como os pontos se acumulam. Consulte a seção denominada [Aplicar regras ao conteúdo](#apply-rules-to-content).

A propriedade `scoringRules` em uma regra de marca simplesmente restringe quais regras de pontuação podem ser emparelhadas com essa regra de marca específica.

>[!NOTE]
>
>Prática recomendada : criar imagens de selo exclusivas para cada site de AEM.

![configuração-regra-medalha](assets/badging-rule-configuration.png)

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
   <td><em>(obrigatório)</em> Uma cadeia de caracteres de vários valores no formato 'number|path'
    <ul>
     <li>número = pontuação</li>
     <li>| = caractere de linha vertical (U+007C)</li>
     <li>caminho = caminho completo para o recurso de imagem do selo</li>
    </ul> As cadeias de caracteres devem ser ordenadas de modo que os números aumentem em valor e nenhum espaço em branco deva aparecer entre o número e o caminho.<br /> Exemplo de entrada:<br /> <code>80|/libs/settings/community/badging/images/gold-badge/jcr:content/gold.png</code></td>
  </tr>
  <tr>
   <td>badgingType</td>
   <td>String</td>
   <td><em>(opcional)</em> Identifica o mecanismo de pontuação como "básico" ou "avançado". Se desejar usar o mecanismo de pontuação avançado, consulte <a href="/help/communities/advanced.md">Pontuação avançada e medalhas</a>. O padrão é "basic".</td>
  </tr>
  <tr>
   <td>scoringRules</td>
   <td>String</td>
   <td>(<em>opcional</em>) uma cadeia de caracteres de vários valores para restringir a regra de medalha aos eventos de pontuação identificados pelas regras de pontuação</td>
  </tr>
 </tbody>
</table>

### Regras de insígnia incluídas {#included-badging-rules}

Estão incluídas na versão duas regras de atribuição de emblemas que correspondem às [Regras de pontuação de fóruns e comentários](#includedscoringrules).

* `/libs/settings/community/badging/rules/comments-badging`

* `/libs/settings/community/badging/rules/forums-badging`

**Notas:**

* `rules` nós são do tipo cq:Page.
* `rules` deve estar em um local de repositório com permissão de leitura para todos.

   * Os nomes das regras devem ser exclusivos independentemente da localização.

### Ativação das regras personalizadas de marcação {#activating-custom-badging-rules}

Quaisquer alterações ou adições feitas às regras de marcação ou imagens feitas no ambiente de criação devem ser instaladas na publicação.

## Atribuir e revogar selos {#assign-and-revoke-badges}

Os emblemas podem ser atribuídos a membros usando o [console de membros](/help/communities/members.md#badges-tab) ou de forma programática usando comandos cURL.

Os seguintes comandos cURL mostram o que é necessário para uma solicitação HTTP para atribuir e revogar selos. O formato básico é:

cURL -i -X POST -H *cabeçalho* -u *entrada* -F *operação* -F *selo* *membro-perfil-url*

*cabeçalho* = &quot;Accept:application/json&quot;
cabeçalho personalizado a ser transmitido ao servidor (obrigatório)

*entrada* = administrator-id:password
por exemplo, admin:admin

*operação* = &quot;:operation=social:assignBadge&quot; OR &quot;:operation=social:deleteBadge&quot;

*selo* = &quot;seloContentPath=*arquivo-imagem-selo*&quot;

*arquivo-imagem-selo* = o local do arquivo de imagem de selo no repositório
por exemplo, /libs/settings/community/badging/images/moderator/jcr:content/moderator.png

*member-profile-url* = o ponto de extremidade do perfil do membro na publicação
por exemplo, https://&lt;server>:&lt;port>/home/users/community/riley/profile.social.json

>[!NOTE]
>
>O *member-profile-url*:
>
>* Pode se referir a uma instância de autor se o [Serviço de Túnel](/help/communities/users.md#tunnel-service) estiver habilitado.
>* Pode ser um nome aleatório e obscuro - consulte a [Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path) em relação à ID autorizável.

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

A instância SocialEvent de um componente registra os eventos como `actions` que ocorrem para `topic`. O SocialEvent inclui um método para retornar um `verb` associado à ação. Há uma relação *n-1* entre `actions` e `verbs`.

Para os componentes de comunidades entregues, as tabelas a seguir descrevem a `verbs` definida para cada `topic` disponível para uso em [subregras de pontuação](#scoring-sub-rules).

>[!NOTE]
>
>Uma nova propriedade booleana, `allowBadges`, habilita/desabilita a exibição de emblemas para uma instância de componente. Ele pode ser configurado nas [caixas de diálogo de edição do componente](/help/communities/author-communities.md) atualizadas por meio de uma caixa de seleção denominada **Exibir selos**.

**[Componente de calendário](/help/communities/calendar.md)**
SocialEvent `topic`= com/adobe/cq/social/calendar

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria um evento de calendário |
| ADICIONAR | comentários de membros em um evento de calendário |
| ATUALIZAR | o comentário ou evento de calendário do membro foi editado |
| EXCLUIR | o evento de calendário ou comentário do membro foi excluído |

**[Componente de comentários](/help/communities/comments.md)**
SocialEvent `topic`= com/adobe/cq/social/comment

| **Verbo** | **Descrição** |
|---|---|
| POST | membro cria um comentário |
| ADICIONAR | membro responde ao comentário |
| ATUALIZAR | comentário do membro editado |
| EXCLUIR | comentário do membro excluído |

**[Componente de Biblioteca de Arquivos](/help/communities/file-library.md)**
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

**[Componente QnA](/help/communities/working-with-qna.md)**
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

Para um componente personalizado, um SocialEvent é instanciado para registrar os eventos do componente como `actions` que ocorrem para um `topic`.

Para dar suporte à pontuação, o SocialEvent precisa substituir o método `getVerb()` para que um `verb` apropriado seja retornado para cada `action`. O `verb` retornado para uma ação pode ser um usado com frequência (como `POST`) ou um especializado para o componente (como `ADD RATING`). Há uma relação *n-1* entre `actions` e `verbs`.

## Resolução de problemas {#troubleshooting}

### As medalhas não aparecem {#badges-are-not-appearing}

Se as regras de pontuação e medalha tiverem sido aplicadas ao conteúdo do site, mas as medalhas não estiverem sendo concedidas para nenhuma atividade, verifique se as medalhas foram ativadas para a instância desse componente.

Consulte [Habilitar medalhas para o componente](#enable-badges-for-component).

### A regra de pontuação não tem efeito {#scoring-rule-has-no-effect}

Se as regras de pontuação e medalha tiverem sido aplicadas ao conteúdo do site, e as medalhas estiverem sendo concedidas para algumas ações, mas não outras, verifique se a regra de medalha não restringiu as regras de pontuação às quais se aplica.

Consulte a propriedade `scoringRules` de [Regras para Marcação](#badging-rules).

### Erro de digitação que diferencia maiúsculas de minúsculas {#case-sensitive-typo}

A maioria das propriedades e valores, especialmente os verbos, fazem distinção entre maiúsculas e minúsculas. Todos os verbos devem estar em MAIÚSCULAS quando usados em uma subregra de pontuação.

Se o recurso não estiver funcionando como esperado, verifique se os dados foram inseridos corretamente.

## Teste rápido {#quick-test}

É possível tentar rapidamente pontuar e criar medalhas usando o [site Tutorial de introdução](/help/communities/getting-started.md) (engajamento):

* Acessar CRXDE Lite no autor.
* Navegue até a página base:

   * /content/sites/engage/en/jcr:content

* Adicione a propriedade badgingRules:

   * **Nome**: `badgingRules`
   * **Tipo**: `String`
   * Selecionar **Multi**
   * Selecionar **Adicionar**
   * Inserir `/libs/settings/community/badging/rules/forums-badging`
   * Selecionar **+**
   * Inserir `/libs/settings/community/badging/rules/comments-badging`
   * Selecione **OK**

* Adicione a propriedade scoringRules:

   * **Nome**: `scoringRules`
   * **Tipo**: `String`
   * Selecionar **Multi**
   * Selecionar **Adicionar**
   * Inserir `/libs/settings/community/scoring/rules/forums-scoring`
   * Selecionar **+**
   * Inserir `/libs/settings/community/scoring/rules/comments-scoring`
   * Selecione **OK**

* Selecione **Salvar tudo**.

![testar-pontuação-medalha](assets/test-scoring-badging.png)

Em seguida, verifique se os componentes do fórum e dos comentários permitem que os emblemas sejam exibidos:

* Novamente usando o CRXDE Lite.
* Navegue até o componente do fórum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`

* Adicione a propriedade booleana allowBadges, se necessário, e verifique se ela é verdadeira.

   * **Nome**: `allowBadges`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

![componente-fórum-teste](assets/test-forum-component.png)

Em seguida, [republique](/help/communities/sites-console.md#publishing-the-site) o site da comunidade.

Por último,

* Navegue até o componente na instância de publicação.
* Faça logon como um membro da comunidade (por exemplo, weston.mccall@dodgit.com / senha).
* Post: um novo tópico de fórum.
* A página deve ser atualizada para que o selo seja exibido.

   * Faça logoff e logon como um membro da comunidade diferente (por exemplo: aaron.mcdonald@mailinator.com/password).

* Selecione o Fórum.

Isso deve dar ao membro da comunidade um selo de bronze visível com sua publicação no fórum, devido ao primeiro limite da regra de classificação em fóruns ser uma pontuação de 1.

![bronzebadge](assets/bronzebadge.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Scoring and Badges Essentials](/help/communities/configure-scoring.md) para desenvolvedores.

Para obter informações sobre o mecanismo de pontuação avançado, consulte [Pontuação avançada e medalhas](/help/communities/advanced.md).

O [componente](/help/communities/enabling-leaderboard.md) e a [função](/help/communities/functions.md#leaderboard-function) do quadro de classificação configuráveis simplificam a exibição de membros e suas pontuações em um site da comunidade.
