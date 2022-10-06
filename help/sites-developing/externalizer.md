---
title: Exteriorização de URLs
seo-title: Externalizing URLs
description: O Externalizador é um serviço OSGI que permite transformar programaticamente um caminho de recurso em um URL externo e absoluto
seo-description: The Externalizer is an OSGI service that allows you to programmatically transform a resource path into an external and absolute URL
uuid: 65bcc352-fc8c-4aa0-82fb-1321a035602d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 938469ad-f466-42f4-8b6f-bfc060ae2785
docset: aem65
exl-id: 971d6c25-1fbe-4c07-944e-be6b97a59922
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# Exteriorização de URLs{#externalizing-urls}

Em AEM, a variável **Externalizador** é um serviço OSGI que permite transformar programaticamente um caminho de recurso (por exemplo, `/path/to/my/page`) em um URL externo e absoluto (por exemplo, `https://www.mycompany.com/path/to/my/page`) ao prefixar o caminho com um DNS pré-configurado.

Como uma instância não pode saber seu URL externamente visível se estiver em execução atrás de uma camada da Web e porque, às vezes, um link precisa ser criado fora do escopo da solicitação, esse serviço fornece um local central para configurar esses URLs externos e criá-los.

Esta página explica como configurar a variável **Externalizador** e como usá-lo. Para obter mais detalhes, consulte o [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).

## Configurar o serviço Externalizador {#configuring-the-externalizer-service}

O **Externalizador** permite definir centralmente vários domínios que podem ser usados para prefixar programaticamente caminhos de recursos. Cada domínio é identificado por um nome exclusivo usado para fazer referência programaticamente ao domínio.

Para definir um mapeamento de domínio para a variável **Externalizador** serviço:

1. Navegue até o gerenciador de configuração por meio de **Ferramentas**, em seguida **Console da Web** ou digite:

   `https://<host>:<port>/system/console/configMgr`

1. Clique em **Externalizador de links CQ do dia** para abrir a caixa de diálogo de configuração.

   >[!NOTE]
   >
   >O link direto para a configuração é `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

   ![aem-externalizer-01](assets/aem-externalizer-01.png)

1. Defina um **Domínios** mapeamento: um mapeamento consiste em um nome exclusivo que pode ser usado no código para fazer referência ao domínio, a um espaço e ao domínio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Em que:

   * **esquema** geralmente é http ou https, mas também pode ser ftp, etc.

      * usar https para aplicar links https, se desejado
      * ele será usado se o código do cliente não substituir o esquema ao solicitar a externalização de um URL.
   * **server** é o nome do host (pode ser um nome de domínio ou endereço ip).
   * **porta** (opcional) é o número da porta.
   * **contextpath** (opcional) só será definido se AEM for instalado como um aplicativo web em um caminho de contexto diferente.

   Por exemplo: `production https://my.production.instance`

   Os seguintes nomes de mapeamento são predefinidos e devem sempre ser definidos conforme AEM dependem deles:

   * `local` - a instância local
   * `author` - DNS do sistema de criação
   * `publish` - DNS, o sítio web público

   >[!NOTE]
   >
   >Uma configuração personalizada permite adicionar uma nova categoria, como `production`, `staging` ou mesmo sistemas externos não AEM como `my-internal-webservice`. É útil evitar a codificação rígida desses URLs em diferentes locais na base de código de um projeto.

1. Clique em **Salvar** para salvar as alterações.

>[!NOTE]
>
>O Adobe recomenda que você [adicionar a configuração ao repositório](/help/sites-deploying/configuring.md#addinganewconfigurationtotherepository).

### Uso do serviço Externalizador {#using-the-externalizer-service}

Esta seção mostra alguns exemplos de como a variável **Externalizador** pode ser usado:

1. **Para obter o serviço Externalizador em um JSP:**

   ```java
   Externalizer externalizer = resourceResolver.adaptTo(Externalizer.class);
   ```

1. **Para exteriorizar um caminho com o domínio &quot;publicar&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `publish https://www.website.com`

   `myExternalizedUrl` termina com o valor :

   * `https://www.website.com/contextpath/my/page.html`


1. **Para exteriorizar um caminho com o domínio &quot;autor&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `author https://author.website.com`

   `myExternalizedUrl` termina com o valor :

   * `https://author.website.com/contextpath/my/page.html`


1. **Para exteriorizar um caminho com o domínio &quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Considerando o mapeamento de domínio:

   * `local https://publish-3.internal`

   `myExternalizedUrl` termina com o valor :

   * `https://publish-3.internal/contextpath/my/page.html`


1. Você pode encontrar mais exemplos na [Javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/Externalizer.html).
