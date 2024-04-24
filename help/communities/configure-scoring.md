---
title: Fundamentos de pontuação e medalhas
description: Saiba mais sobre como o recurso de pontuação e medalhas das comunidades Adobe Experience Manager identifica e recompensa os membros da comunidade.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 470a382a-2aa7-449e-bf48-b5a804c5b114
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Fundamentos de pontuação e medalhas {#scoring-and-badges-essentials}

O recurso de pontuação e medalhas do AEM Communities identifica e recompensa os membros da comunidade.

Os detalhes da configuração do recurso estão descritos em

* [Pontuação e medalhas das comunidades](/help/communities/implementing-scoring.md)

Esta página contém detalhes técnicos adicionais:

* Como [exibir um selo](#displaying-badges) como imagem ou texto
* Como ativar extensivo [log de depuração](#debug-log-for-scoring-and-badging)
* Como [acessar UGC](#ugc-for-scoring-and-badging) relacionado à pontuação e à medalha

>[!CAUTION]
>
>A estrutura de implementação visível no CRXDE Lite está sujeita a alterações.

## Exibição de selos {#displaying-badges}

Se um selo é exibido como texto ou imagem é controlado no lado do cliente no modelo HBS.

Por exemplo, pesquisar por `this.isAssigned` in `/libs/social/forum/components/hbs/topic/list-item.hbs`:

```
{{#each author.badges}}

  {{#if this.isAssigned}}

    <div class="scf-badge-text">

      {{this.title}}

    </div>

  {{/if}}

{{/each}}

{{#each author.badges}}

  {{#unless this.isAssigned}}

    <img class="scf-badge-image" alt="{{this.title}}" title="{{this.title}}" src="{{this.imageUrl}}" />

  {{/unless}}

{{/each}}
```

Se verdadeiro, `isAssigned` indica que o selo foi atribuído a uma função e deve ser exibido como texto.

Se falso, `isAssigned` indica que a medalha foi concedida por uma pontuação obtida e a medalha deve ser exibida como uma imagem.

Qualquer alteração nesse comportamento deve ser feita em um script personalizado (substituição ou sobreposição). Consulte [Personalização do lado do cliente](/help/communities/client-customize.md).

## Log de depuração para pontuação e medalha {#debug-log-for-scoring-and-badging}

Para ajudar a depurar a pontuação e o símbolo, é possível configurar um arquivo de log personalizado. O conteúdo desse arquivo de log poderá ser fornecido ao suporte ao cliente se forem encontrados problemas com o recurso.

Para obter instruções detalhadas, visite [Criar um arquivo de log personalizado](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file).

Para configurar rapidamente um arquivo de log do Sling:

1. Acesse o **Suporte ao log do console da Web do Adobe Experience Manager**, por exemplo

   * https://localhost:4502/system/console/slinglog

1. Selecionar **Adicionar novo agente de log**

   1. Selecionar `DEBUG` para **Nível de registro**

   1. Digite um nome para **Arquivo de log**, por exemplo

      * logs/scoring-debug.log

   1. Insira dois **Logger** entradas (classe) (usando `+` ícone)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`

   1. Selecionar **Salvar**

![debug-scoring-log](assets/debug-scoring-log.png)

Para ver entradas de log:

* No console da Web

   * No **Status** menu
   * Selecionar **Arquivos de log**
   * Procure pelo seu nome de Arquivo de Log, como `scoring-debug`

* No disco local do servidor

   * O arquivo de log está em &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Por exemplo, `.../crx-quickstart/logs/scoring-debug.log`

![log de pontuação](assets/scoring-log.png)

## UGC para pontuação e medalha {#ugc-for-scoring-and-badging}

É possível exibir o UGC relacionado à pontuação e ao badging quando o SRP escolhido for JSRP ou MSRP, mas não ASRP. (Se não estiver familiarizado com esses termos, consulte [Armazenamento de conteúdo da comunidade](/help/communities/working-with-srp.md) e [Visão geral do provedor de recursos de armazenamento](/help/communities/srp.md).)

As descrições para acessar dados de pontuação e badging usam JSRP, pois o UGC é facilmente acessível usando [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP no autor**: experimentar no ambiente do autor resulta em uma UGC que só é visível do ambiente do autor.

**JSRP em publicação**: da mesma forma, se estiver testando no ambiente de publicação, será necessário acessar o CRXDE Lite com privilégios administrativos em uma instância de publicação. Se a instância de publicação estiver em execução no [modo de produção](/help/sites-administering/production-ready.md) (modo de execução nosamplecontent), é necessário [ativar o CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

A localização básica do UGC no JSRP é `/content/usergenerated/asi/jcr/`.

### APIs de pontuação e medalha {#scoring-and-badging-apis}

As seguintes APIs estão disponíveis para uso:

* [com.adobe.cq.social.scoring.api no 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR)
* [com.adobe.cq.social.badging.api no 6.3](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=pt-BR)

Os Javadocs mais recentes para o pacote de recursos instalado estão disponíveis para desenvolvedores no repositório do Adobe. Consulte [Uso do Maven para comunidades : Javadocs](/help/communities/maven.md#javadocs).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso**.

### Exemplo de configuração {#example-setup}

As capturas de tela dos dados do repositório vêm da configuração de pontuação e badging para um fórum em dois sites AEM diferentes:

1. Um site de AEM *com* um identificador exclusivo (site da comunidade criado usando o assistente):

   * Uso do site Tutorial de introdução (engajamento) criado durante o [tutorial de introdução](/help/communities/getting-started.md)
   * Localize o nó da página do fórum

     `/content/sites/engage/en/forum/jcr:content`

   * Adicionar propriedades de pontuação e medalha

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-scoring,
   /libs/settings/community/badging/rules/forums-scoring]
   ```

   * Localize o nó do componente do fórum

     `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Para exibir selos, adicione a propriedade

     `allowBadges = true`

   * Um usuário se conecta, cria um tópico do fórum e recebe um selo bronze

1. Um site de AEM *sem* uma id exclusiva:

   * Usar o [Guia de componentes da comunidade](/help/communities/components-guide.md)
   * Localize o nó da página do fórum

     `/content/community-components/en/forum/jcr:content`

   * Adicionar propriedades de pontuação e medalha

   ```
   scoringRules = [/libs/settings/community/scoring/rules/comments-scoring,
   /libs/settings/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/libs/settings/community/badging/rules/comments-badging,
   /libs/settings/community/badging/rules/forums-badging]
   ```

   * Localize o nó do componente do fórum

     `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

   * Para exibir selos, adicione a propriedade

     `allowBadges = true`

   * Um usuário se conecta, cria um tópico do fórum e recebe um selo bronze

1. Um usuário recebe um selo de moderador usando cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Como um usuário ganhou dois selos de bronze e recebeu um selo de moderador, o usuário aparece com sua entrada no fórum da seguinte maneira:

   ![moderador](assets/moderator.png)

>[!NOTE]
>
>Este exemplo não segue estas práticas recomendadas:
>
>* Os nomes das regras de pontuação devem ser globalmente exclusivos; eles não devem terminar com o mesmo nome.
>
>  Um exemplo do que *não* fazer:
>
>  /libs/settings/community/scoring/rules/site1/forums-scoring
>  /libs/settings/community/scoring/rules/site2/forums-scoring
>
>* Criação de imagens exclusivas de crachás para diferentes sites de AEM

### UGC de pontuação de acesso {#access-scoring-ugc}

Utilização do [APIs](#scoring-and-badging-apis) é preferível.

Para fins investigativos, usando JSRP para o exemplo, a pasta base que contém pontuações é

* `/content/usergenerated/asi/jcr/scoring`

O nó filho de `scoring` é o nome da regra de pontuação. Assim, uma prática recomendada é que os nomes de regras de pontuação em um servidor sejam globalmente exclusivos.

Para o site Geometrixx Engage, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, a ID do site da comunidade ( `engage-ba81p`), um identificador exclusivo e o identificador do usuário:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Para o site de guia dos Componentes da comunidade, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, uma ID padrão ( `default-site`), um identificador exclusivo e o identificador do usuário:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

A pontuação é armazenada na propriedade `scoreValue_tl` que só pode conter um valor ou se referir indiretamente a um atomicCounter.

![access-scoring-ugc](assets/access-scoring-ugc.png)

### UGC de acesso a emblemas {#access-badging-ugc}

Utilização do [APIs](#scoring-and-badging-apis) é preferível.

Para fins de investigação, usando JSRP como exemplo, a pasta base que contém informações sobre selos atribuídos ou concedidos é

* `/content/usergenerated/asi/jcr`

Seguido pelo caminho para o perfil do usuário, terminando em uma pasta de selos, como:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Selo concedido {#awarded-badge}

![award-badging-ugc](assets/access-badging-ugc.png)

#### Selo atribuído {#assigned-badge}

![selo atribuído](assets/assigned-badge.png)

## Informações adicionais {#additional-information}

Para exibir uma lista classificada de membros com base em pontos:

* [Função de placar de líderes](/help/communities/functions.md#leaderboard-function) para inclusão em um site da comunidade ou modelo de grupo.
* [Componente do quadro de classificação](/help/communities/enabling-leaderboard.md), o componente em destaque da função Placar de líderes, para criação de páginas.
