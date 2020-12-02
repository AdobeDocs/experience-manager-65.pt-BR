---
title: Externalização de URLs
seo-title: Externalização de URLs
description: O Externalizer é um serviço OSGI que permite transformar programaticamente um caminho de recurso em um URL externo e absoluto
seo-description: O Externalizer é um serviço OSGI que permite transformar programaticamente um caminho de recurso em um URL externo e absoluto
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# Externalização de URLs{#externalizing-urls}

No AEM, o **Externalizer** é um serviço OSGI que permite transformar programaticamente um caminho de recurso (por exemplo, `/path/to/my/page`) em um URL externo e absoluto (por exemplo, `https://www.mycompany.com/path/to/my/page`) ao prefixar o caminho com um DNS pré-configurado.

Como uma instância não pode saber seu URL visível externamente se estiver sendo executado atrás de uma camada da Web e como às vezes um link precisa ser criado fora do escopo da solicitação, esse serviço fornece um local central para configurar esses URLs externos e criá-los.

Esta página explica como configurar o serviço **Externalizer** e como usá-lo. Para obter mais detalhes, consulte [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configuração do serviço Externalizer {#configuring-the-externalizer-service}

O serviço **Externalizer** permite definir centralmente vários domínios que podem ser usados para prefixar programaticamente caminhos de recursos. Cada domínio é identificado por um nome exclusivo que é usado para fazer referência programaticamente ao domínio.

Para definir um mapeamento de domínio para o serviço **Externalizer**:

1. Navegue até o gerenciador de configuração por **Ferramentas**, em seguida **Console Web**, ou insira:

   `https://<host>:<port>/system/console/configMgr`

1. Clique em **Externalizador de links do Day CQ** para abrir a caixa de diálogo de configuração.

   >[!NOTE]
   >
   >O link direto para a configuração é `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Defina um mapeamento **Domínios**: um mapeamento consiste em um nome exclusivo que pode ser usado no código para referenciar o domínio, um espaço e o domínio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Em que:

   * **Geralmente,** os esquemas são http ou https, mas também podem ser ftp etc.

      * use https para aplicar links https se desejar
      * será usado se o código do cliente não substituir o esquema ao solicitar a externalização de um URL.
   * **O** servidor é o nome do host (pode ser um nome de domínio ou endereço IP).
   * **port**  (opcional) é o número da porta.
   * **o contexto**  (opcional) só é definido se AEM é instalado como um aplicativo da Web em um caminho de contexto diferente.

   Por exemplo: `production https://my.production.instance`

   Os seguintes nomes de mapeamento são predefinidos e devem ser sempre definidos como AEM depende deles:

   * `local` - a instância local
   * `author` - o DNS do sistema de criação
   * `publish` - DNS, o sítio Web público

   >[!NOTE]
   >
   >Uma configuração personalizada permite adicionar uma nova categoria, como `production`, `staging` ou até mesmo sistemas externos não AEM, como `my-internal-webservice`. É útil evitar a codificação desses URLs em diferentes locais na base de códigos de um projeto.

1. Clique em **Salvar** para salvar as alterações.

>[!NOTE]
>
>O Adobe recomenda que você [adicione a configuração ao repositório](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Usando o serviço Externalizer {#using-the-externalizer-service}

Esta seção mostra alguns exemplos de como o serviço **Externalizer** pode ser usado:

1. **Para obter o serviço Externalizer em um JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Para externalizar um caminho com o domínio &#39;publicar&#39;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Assumindo o mapeamento de domínio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina com o valor:

   * `https://www.website.com/contextpath/my/page.html`


1. **Para externalizar um caminho com o domínio &#39;autor&#39;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Assumindo o mapeamento de domínio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina com o valor:

   * `https://author.website.com/contextpath/my/page.html`


1. **Para externalizar um caminho com o domínio &#39;local&#39;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Assumindo o mapeamento de domínio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina com o valor:

   * `https://publish-3.internal/contextpath/my/page.html`


1. Você pode encontrar mais exemplos em [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
