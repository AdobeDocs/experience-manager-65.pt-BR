---
title: Resolução de Problemas
seo-title: Resolução de Problemas
description: Comunidade de solução de problemas incluindo problemas conhecidos
seo-description: Comunidade de solução de problemas incluindo problemas conhecidos
uuid: 99225430-fa2a-4393-ae5a-18b19541c358
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: cdb2d80a-2fbf-4ee6-b89b-b5d74e6d3bfc
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Resolução de Problemas{#troubleshooting}

Esta seção contém preocupações comuns e problemas conhecidos.

## Problemas conhecidos {#known-issues}

### Falha na Refetoração do Dispatcher {#dispatcher-refetch-fails}

Ao usar o Dispatcher 4.1.5 com uma versão mais recente do JavaScript, uma busca pode resultar em &quot;Não é possível receber resposta do servidor remoto&quot; após aguardar o tempo limite da solicitação.

O uso do Dispatcher 4.1.6 ou posterior resolverá esse problema.

### Não é possível acessar a publicação do fórum após atualizar do CQ 5.4 {#cannot-access-forum-post-after-upgrading-from-cq}

Se um fórum tiver sido criado no CQ 5.4 e os tópicos tiverem sido publicados e o site tiver sido atualizado para o AEM 5.6.1 ou posterior, tentar visualização das publicações existentes poderá resultar em um erro na página:

O caractere de padrão ilegal &#39;a&#39;Não é possível enviar solicitação para `/content/demoforums/forum-test.html` este servidor e os registros contêm o seguinte:

```xml
20.03.2014 22:49:35.805 ERROR [10.177.45.32 [1395380975744] GET /content/demoforums/forum-test.html HTTP/1.1] com.day.cq.wcm.tags.IncludeTag Error while executing script content.jsp
org.apache.sling.api.scripting.ScriptEvaluationException:
at org.apache.sling.scripting.core.impl.DefaultSlingScript.call(DefaultSlingScript.java:388)
at org.apache.sling.scripting.core.impl.DefaultSlingScript.eval(DefaultSlingScript.java:171)
```

O problema é que a string de formato para com.day.cq.commons.date.RelativeTimeFormat foi alterada entre 5.4 e 5.5 de modo que &quot;a&quot; para &quot;ago&quot; não é mais aceito.

Assim, qualquer código que use a API RelativeTimeFormat() precisará ser alterado:

* De: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r a", resourceBundle);`
* Para: `final RelativeTimeFormat fmt = new RelativeTimeFormat("r", resourceBundle);`

A falha é diferente no autor e na publicação. Em seu autor, ele falha silenciosamente e simplesmente não exibe os tópicos do fórum. Ao publicar, o erro é exibido na página.

Consulte a API [com.day.cq.commons.date.RelativeTimeFormat](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/date/RelativeTimeFormat.html) para obter mais informações.

## Preocupações comuns {#common-concerns}

### Aviso em registros: Handlebars Obsoleto {#warning-in-logs-handlebars-deprecated}

Durante a inicialização (não o 1º, mas todos depois disso), o seguinte aviso pode ser visto nos registros:

* `11.04.2014 08:38:07.223 WARN [FelixStartLevel]com.github.jknack.handlebars.Handlebars Helper 'i18n'` foi substituído por `com.adobe.cq.social.handlebars.I18nHelper@15bac645`

Este aviso pode ser ignorado com segurança, pois `jknack.handlebars.Handlebars`, usado pelo [SCF](scf.md#handlebarsjavascripttemplatinglanguage), vem com seu próprio utilitário auxiliar i18n. Ao start para cima, ele é substituído por um auxiliar AEM específico [i18n](handlebars-helpers.md#i-n). Esse aviso é gerado pela biblioteca de terceiros para confirmar a substituição de um auxiliar existente.

### Aviso em registros: OakResourceListener processOsgiEventQueue {#warning-in-logs-oakresourcelistener-processosgieventqueue}

A publicação de vários tópicos do fórum das Comunidades sociais pode resultar em quantidades enormes de registros de avisos e informações do processo OakResourceListenerOsgiEventQueue.

Esses avisos podem ser ignorados com segurança.

```xml
23.04.2014 14:21:18.900 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.frq/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.908 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/search-collections/ugc-sc/_m.prx/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.909 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/67/67699ab5-9d57-4c79-a755-2727ba9e6452/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
23.04.2014 14:21:18.990 *WARN* [pool-5-thread-3] org.apache.sling.jcr.resource.internal.OakResourceListener processOsgiEventQueue: Resource at /var/replication/data/1f799fb4-0aeb-4660-aadb-705657f16048/b9/b91f1690-87e8-41d8-a78e-cd2259f837c8/jcr:content not found, which is not expected for an added or modified node
```

### Erro nos registros: NoClassDefFoundError para IndexElementFactory {#error-in-logs-noclassdeffounderror-for-indexelementfactory}

Atualizar o AEM 5.6.1 GA para o cq-socialCommunities-pkg-1.4.x mais recente ou para o AEM 6.0 resulta em erros no arquivo de log durante a inicialização para uma condição que resolverá a si mesmo, como evidenciado pelo erro, que não é visto na reinicialização.

```xml
14.11.2013 20:52:39.453 ERROR [Apache Sling JCR Resource Event Queue Processor for path '/'] com.adobe.cq.social.storage.index.impl.IndexService Error occurred while processing event java.util.ConcurrentModificationException
14.11.2013 20:52:40.716 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Error during instantiation of the implementation object (java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory) java.lang.NoClassDefFoundError: com/adobe/cq/social/storage/index/IndexElementFactory
14.11.2013 20:52:40.717 ERROR [OsgiInstallerImpl] com.adobe.cq.social.cq-social-commons [CommentListProvider] Failed creating the component instance; see log for reason
```
