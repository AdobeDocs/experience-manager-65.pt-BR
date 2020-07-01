---
title: Essenciais de pontuação e emblemas
seo-title: Essenciais de pontuação e emblemas
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
source-git-commit: 56c2e6b55964ea5f3e180b17bd2a244882aa62ea
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---


# Essenciais de pontuação e emblemas {#scoring-and-badges-essentials}

O recurso de pontuação de AEM Communities e emblemas fornece a capacidade de identificar e recompensar membros da comunidade.

Os detalhes da configuração do recurso estão descritos em

* [Pontuação das comunidades e emblemas](/help/communities/implementing-scoring.md)

Esta página contém detalhes técnicos adicionais :

* Como [exibir um crachá](#displaying-badges) como imagem ou texto
* Como ativar o registro de [depuração extenso](#debug-log-for-scoring-and-badging)
* Como [acessar o UGC](#ugc-for-scoring-and-badging) relacionado à pontuação e à identificação

>[!CAUTION]
>
>A estrutura de implementação visível no CRXDE Lite está sujeita a alterações.

## Exibição de emblemas {#displaying-badges}

Se um crachá é exibido como texto ou imagem é controlado no lado do cliente no modelo HBS.

Por exemplo, pesquise `this.isAssigned` em `/libs/social/forum/components/hbs/topic/list-item.hbs`:

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

Quaisquer alterações nesse comportamento devem ser feitas em um script personalizado (sobreposição ou sobreposição). Consulte Personalização do lado [do cliente](/help/communities/client-customize.md).

## Registro de depuração para pontuação e marcação {#debug-log-for-scoring-and-badging}

Para ajudar a depurar a pontuação e a identificação, é possível configurar um arquivo de log personalizado. O conteúdo desse arquivo de log pode ser fornecido ao suporte ao cliente se forem encontrados problemas com o recurso.

Para obter instruções detalhadas, visite [Criar um arquivo](/help/sites-deploying/monitoring-and-maintaining.md#create-a-custom-log-file)de log personalizado.

Para configurar rapidamente um arquivo de registro de slides:

1. Acesse o suporte **de log do console da Web do** Adobe Experience Manager, por exemplo

   * https://localhost:4502/system/console/slinglog

1. Selecione **Adicionar novo agente de log**

   1. Selecionar `DEBUG` para o Nível **de Log**

   1. Digite um nome para Arquivo **de** log, por exemplo

      * logs/scoring-debug.log
   1. Digite duas entradas **do Logger** (classe) (usando o `+` ícone)

      * `com.adobe.cq.social.scoring`
      * `com.adobe.cq.social.badging`
   1. Selecione **Salvar**



![chlimage_1-248](assets/chlimage_1-248.png)

Para ver as entradas de log:

* Do Console da Web

   * No menu **Status**
   * Selecionar arquivos **de registro**
   * Procure o nome do arquivo de log, como `scoring-debug`

* No disco local do servidor

   * O arquivo de log está em &lt;*server-install-dir*>/crx-quickstart/logs/&lt;*log-file-name*>.log

   * Por exemplo, `.../crx-quickstart/logs/scoring-debug.log`

![chlimage_1-249](assets/chlimage_1-249.png)

## UGC para Pontuação e Crachá {#ugc-for-scoring-and-badging}

É possível visualização do UGC relacionado à pontuação e à identificação quando o SRP escolhido for JSRP ou MSRP, mas não ASRP. (Se não estiver familiarizado com esses termos, consulte Armazenamento [de conteúdo da](/help/communities/working-with-srp.md) comunidade e Visão geral [do provedor de recursos do](/help/communities/srp.md)Armazenamento.)

As descrições para acessar dados de pontuação e marcação usam o JSRP, já que o UGC é facilmente acessível usando o [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

**JSRP no autor**: experimentar no ambiente do autor resulta em UGC que só é visível do ambiente do autor.

**JSRP ao publicar**: da mesma forma, se estiver testando o ambiente publish, será necessário acessar o CRXDE Lite com privilégios administrativos em uma instância de publicação. Se a instância de publicação estiver sendo executada no modo [de](/help/sites-administering/production-ready.md) produção (nosamplecontent runmode), será necessário [ativar o CRXDE Lite](/help/sites-administering/enabling-crxde-lite.md).

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

   * Usar o site Tutorial de introdução (engajamento) criado durante o tutorial de [introdução](/help/communities/getting-started.md)
   * Localize o nó da página do fórum

      `/content/sites/engage/en/forum/jcr:content`

   * Adicionar propriedades de pontuação e marcação

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

   * Adicionar propriedade para exibir emblemas

      `allowBadges = true`

   * Um usuário entra, cria um tópico do fórum e recebe um crachá de bronze


1. Um site do AEM *sem* uma id exclusiva:

   * Uso do guia Componentes [da comunidade](/help/communities/components-guide.md)
   * Localize o nó da página do fórum

      `/content/community-components/en/forum/jcr:content`

   * Adicionar propriedades de pontuação e marcação

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

   * Adicionar propriedade para exibir emblemas

      `allowBadges = true`

   * Um usuário entra, cria um tópico do fórum e recebe um crachá de bronze


1. Um usuário recebe um crachá de moderador usando cURL:

   ```shell
   curl -i -X POST -H "Accept:application/json" -u admin:admin -F ":operation=social:assignBadge" -F "badgeContentPath=/libs/settings/community/badging/images/moderator/jcr:content/moderator.png" https://localhost:4503/home/users/community/w271OOup2Z4DjnOQrviv/profile.social.json
   ```

   Como um usuário ganhou dois crachás de bronze e recebeu um crachá de moderador, é assim que o usuário aparece com sua entrada no fórum.

![chlimage_1-250](assets/chlimage_1-250.png)

>[!NOTE]
>
>Este exemplo não segue essas práticas recomendadas:
>
>* Os nomes das regras de pontuação devem ser globalmente exclusivos; não devem terminar com o mesmo nome.
   >  Um exemplo do que *não* fazer:
   >  /libs/settings/community/scoring/rules/site1/forums-scoring
   >  /libs/settings/community/scoring/rules/site2/forums-scoring
   >
   >
* Criar imagens de crachá exclusivas para sites do AEM diferentes

>



### Acesse a Pontuação UGC {#access-scoring-ugc}

O uso das [APIs](#scoring-and-badging-apis) é preferido.

Para fins de investigação, usando o JSRP como exemplo, a pasta base que contém pontuações é

* `/content/usergenerated/asi/jcr/scoring`

O nó filho de `scoring` é o nome da regra de pontuação. Assim, uma prática recomendada é que os nomes das regras de pontuação em um servidor sejam globalmente exclusivos.

Para o site de Envolvimento Geometrixx, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, a ID do site da comunidade ( `engage-ba81p`), uma ID exclusiva e a ID do usuário:

* `.../scoring/forums-scoring/engage-ba81p/6d179715c0e93cb2b20886aa0434ca9b5a540401/riley`

Para o site de guia Componentes da comunidade, o usuário e sua pontuação estão em um caminho construído com o nome da regra de pontuação, uma ID padrão ( `default-site`), uma ID exclusiva e a ID do usuário:

* `.../scoring/forums-scoring/default-site/b27a17cb4910a9b69fe81fb1b492ba672d2c086e/riley`

A pontuação é armazenada na propriedade `scoreValue_tl` que pode conter apenas um valor ou indiretamente se referir a um atomicCounter.

![chlimage_1-251](assets/chlimage_1-251.png)

### UGC da marca de acesso {#access-badging-ugc}

O uso das [APIs](#scoring-and-badging-apis) é preferido.

Para fins de investigação, usando o JSRP como exemplo, a pasta base que contém informações sobre crachás atribuídos ou atribuídos é

* `/content/usergenerated/asi/jcr`

Seguido pelo caminho para o perfil do usuário, terminando em uma pasta de crachás, como:

* `/home/users/community/w271OOup2Z4DjnOQrviv/profile/badges`

#### Crachá concedido {#awarded-badge}

![chlimage_1-252](assets/chlimage_1-252.png)

#### Crachá atribuído {#assigned-badge}

![chlimage_1-253](assets/chlimage_1-253.png)

## Informações adicionais {#additional-information}

Para exibir uma lista classificada de membros com base em pontos:

* [Função](/help/communities/functions.md#leaderboard-function) de quadro de líderes para inclusão em um site da comunidade ou modelo de grupo.
* [Componente](/help/communities/enabling-leaderboard.md)de quadro de líderes, o componente em destaque da função de quadro de líderes, para criação de página.

