---
title: Essenciais de pontuação e símbolos
seo-title: Essenciais de pontuação e símbolos
description: Visão geral do recurso Pontuação e emblemas
seo-description: Visão geral do recurso Pontuação e emblemas
uuid: 6e3af071-04e8-4dc1-977a-0da711b72961
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 628b6dcd-8b1c-4166-8fc2-843baa86ac1c
docset: aem65
translation-type: tm+mt
source-git-commit: d522c5ec6c72a9fd391d021f2fac37f88c686bd9

---


# Essenciais de pontuação e símbolos{#scoring-and-badges-essentials}

O recurso de pontuação e selo do AEM Communities permite identificar e recompensar membros da comunidade.

Os detalhes da configuração do recurso estão descritos em

* [Pontuação e símbolos das comunidades](/help/communities/implementing-scoring.md)

Esta página contém detalhes técnicos adicionais :

* como [exibir um crachá](#displaying-badges) como imagem ou texto
* como ativar o registro de [depuração extenso](#debug-log-for-scoring-and-badging)
* como [acessar o UGC](#ugc-for-scoring-and-badging) relacionado à pontuação e à marcação

>[!CAUTION]
>
>A estrutura de implementação visível no CRXDE Lite está sujeita a alterações.

## Exibição de emblemas {#displaying-badges}

Se um selo é exibido como texto ou imagem é controlado no lado do cliente no modelo HBS.

Por exemplo, pesquise `this.isAssigned` em `/libs/social/forum/components/hbs/topic/list-item.hbs`, :

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

Se verdadeiro, isAssigned indica que o crachá foi atribuído a uma função e que o crachá deve ser exibido como texto.

Se falso, é Atribuído indica que o crachá foi concedido para uma pontuação ganha e o crachá deve ser exibido como uma imagem.

Quaisquer alterações nesse comportamento devem ser feitas em um script personalizado (sobreposição ou sobreposição). Consulte Personalização do [cliente](/help/communities/client-customize.md).

## Registro de depuração para pontuação e marcação {#debug-log-for-scoring-and-badging}

Para ajudar a depurar a pontuação e a identificação, é possível configurar um arquivo de log personalizado. O conteúdo desse arquivo de log pode ser fornecido ao suporte ao cliente se forem encontrados problemas com o recurso.

Para obter instruções detalhadas, visite [Criar um arquivo](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)de log personalizado.

Para configurar rapidamente um arquivo de registro de slides:

1. acesse o suporte **de log do console da Web do** Adobe Experience Manager, por exemplo

   * https://localhost:4502/system/console/slinglog

1. selecione **Adicionar novo agente de log**

   1. selecionar `DEBUG`para Nível **de Log**

   1. digite um nome para Arquivo **de** log, por exemplo

      * logs/scoring-debug.log
   1. digite duas entradas **Logger **(class) (usando o `+` ícone)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. select **Save**



![chlimage_1-193](assets/chlimage_1-193.png)

Para ver entradas de log

* do Web Console

   * no menu **Status **Menu
   * selecionar arquivos **de registro**
   * procure o nome do arquivo de log, como `scoring-debug`

* no disco local do servidor

   * o arquivo de log está em &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * for example, `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-194](assets/chlimage_1-194.png)

## UGC para Pontuação e Crachá {#ugc-for-scoring-and-badging}

É possível visualizar o UGC relacionado à pontuação e à identificação quando o SRP escolhido é JSRP ou MSRP, mas não ASRP. (Se não estiver familiarizado com esses termos, consulte [Community Content Storage](/help/communities/working-with-srp.md) and [Storage Resource Provider Overview](/help/communities/srp.md).)

As descrições para acessar dados de pontuação e marcação usam o JSRP, já que o UGC é facilmente acessível usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP sobre o autor** : experimentar no ambiente do autor resulta em UGC que é visível apenas do ambiente do autor.

**JSRP ao publicar** : da mesma forma, se estiver testando no ambiente de publicação, será necessário acessar o CRXDE Lite com privilégios administrativos em uma instância de publicação. Se a instância de publicação estiver sendo executada no modo [de](/help/sites-administering/production-ready.md) produção (nosamplecontent runmode), será necessário [ativar o CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

A localização básica do UGC no JSRP é `/content/usergenerated/asi/jcr/`.

### APIs de pontuação e marcação {#scoring-and-badging-apis}

As seguintes APIs estão disponíveis para uso:

* [com.adobe.cq.social.scoring.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/scoring/api/package-summary.html)
* [com.adobe.cq.social.badging.api](https://docs.adobe.com/content/docs/en/aem/6-3/develop/ref/javadoc/com/adobe/cq/social/badging/api/package-summary.html)

Os mais recentes Javadocs para o pacote de recursos instalados estão disponíveis para desenvolvedores do repositório da Adobe. Consulte [Uso do Maven para comunidades : Javadocs](/help/communities/maven.md#javadocs).

**A localização e o formato do UGC no repositório estão sujeitos a alterações sem aviso prévio**.

### Exemplo de configuração {#example-setup}

As capturas de tela dos dados do repositório vêm da configuração da pontuação e da identificação de um fórum em dois sites diferentes do AEM:

1. Um site do AEM *com* uma ID exclusiva (site da comunidade criado usando o assistente):

* usando o site Tutorial de introdução (engajamento) criado durante o tutorial de [introdução](/help/communities/getting-started.md)
* localizar o nó da página do fórum

   * `/content/sites/engage/en/forum/jcr:content`

* adicionar propriedades de pontuação e marcação

   ```
   scoringRules = [/etc/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/etc/community/badging/rules/comments-scoring,
   /etc/community/badging/rules/forums-scoring]
   ```

* localizar o nó do componente do fórum

   * `/content/sites/engage/en/forum/jcr:content/content/primary/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* adicionar propriedade para exibir emblemas

   * `allowBadges = true`

* um usuário entra, cria um tópico do fórum e recebe um selo de bronze

1. Um site do AEM *sem* uma id exclusiva:

* usando o guia Componentes [da comunidade](/help/communities/components-guide.md)
* localizar o nó da página do fórum

   * `/content/community-components/en/forum/jcr:content`

* adicionar propriedades de pontuação e marcação

   ```
   scoringRules = [/etc/community/scoring/rules/comments-scoring,
   /etc/community/scoring/rules/forums-scoring]
   ```

   ```
   badgingRules =[/etc/community/badging/rules/comments-scoring,
   /etc/community/badging/rules/forums-scoring]
   ```

* localizar o nó do componente do fórum

   * `/content/community-components/en/forum/jcr:content/content/forum`
( `sling:resourceType = social/forum/components/hbs/forum`)

* adicionar propriedade para exibir emblemas

   * `allowBadges = true`

* um usuário entra, cria um tópico do fórum e recebe um selo de bronze

1. um usuário recebe um crachá de moderador usando cURL:

```shell
curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/etc/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
```

Como um usuário ganhou dois símbolos de bronze e recebeu um crachá de moderador, é assim que o usuário aparece com sua entrada no fórum :

![chlimage_1-195](assets/chlimage_1-195.png)

>[!NOTE]
>
>Este exemplo não segue essas práticas recomendadas:
>
>* nomes de regras de pontuação devem ser globalmente exclusivos; não devem terminar com o mesmo nome.
   >  Um exemplo do que *não *fazer :
   >  /etc/community/scoring/rules/site1/forums-scoring
   >  /etc/community/scoring/rules/site2/forums-scoring
   >
   >
* criação de imagens de crachá exclusivas para sites do AEM diferentes
>



### Acesse a Pontuação UGC {#access-scoring-ugc}

É preferível usar as [APIs](#scoring-and-badging-apis) .

Para fins de investigação, usando o JSRP como exemplo, a pasta base que contém pontuações é

* `/content/usergenerated/asi/jcr/scoring`

O nó filho de `scoring`é o nome da regra de pontuação. Assim, uma prática recomendada é que os nomes das regras de pontuação em um servidor sejam globalmente exclusivos.

Para o site de Envolvimento Geometrixx, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, a ID do site da comunidade ( `engage-ba81p`), uma ID exclusiva e a ID do usuário:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Para o site de guia Componentes da comunidade, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, uma ID padrão ( `default-site`), uma ID exclusiva e a ID do usuário:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

A pontuação é armazenada na propriedade `scoreValue_tl` que pode conter apenas um valor ou indiretamente se referir a um atomicCounter.

![chlimage_1-196](assets/chlimage_1-196.png)

### UGC da marca de acesso {#access-badging-ugc}

É preferível usar as [APIs](#scoring-and-badging-apis) .

Para fins de investigação, usando o JSRP como exemplo, a pasta base que contém informações sobre crachás atribuídos ou atribuídos é

* /content/usergenerate/asi/jcr

Seguido pelo caminho para o perfil do usuário, terminando em uma pasta de crachás, como

* /home/users/community/w271Oup2Z4DjnOQrviv/profile/badges

#### crachá concedido {#awarded-badge}

![chlimage_1-197](assets/chlimage_1-197.png)

#### crachá atribuído {#assigned-badge}

![chlimage_1-198](assets/chlimage_1-198.png)

## Informações adicionais {#additional-information}

Para exibir uma lista classificada de membros com base em pontos:

* [Função](/help/communities/functions.md#leaderboard-function) de quadro de líderes para inclusão em um site da comunidade ou modelo de grupo.
* [Componente](/help/communities/enabling-leaderboard.md)de quadro de líderes, o componente em destaque da função de quadro de líderes, para criação de página.

