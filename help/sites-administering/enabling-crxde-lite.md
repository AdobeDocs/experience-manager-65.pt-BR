---
title: Habilitar o CRXDE Lite no AEM
description: Saiba como habilitar o CRXDE Lite no Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 0%
---
# Habilitar o CRXDE Lite no AEM{#enabling-crxde-lite-in-aem}

Para garantir que as instalações do AEM sejam o mais seguras possível, a lista de verificação de segurança recomenda [desabilitar o WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) em ambientes de produção.

No entanto, o CRXDE Lite depende do pacote `org.apache.sling.jcr.davex` para funcionar corretamente, portanto, desabilitar o WebDAV também desabilitará efetivamente o CRXDE Lite.

Quando isso acontecer, navegar até `https://serveraddress:4502/crx/de/index.jsp` exibirá um nó raiz vazio e todas as solicitações HTTP para os recursos do CRXDE Lite falharão:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Embora essa recomendação tenha como objetivo reduzir ao máximo as superfícies de ataque, os administradores do sistema podem, às vezes, precisar acessar o CRXDE Lite para navegar pelo conteúdo ou depurar problemas em instâncias de produção.

Você pode habilitar o CRXDE Lite com [configurações OSGi](#enabling-crxde-lite-osgi) ou com um [cURL command](#enabling-crxde-lite-curl).

>[!WARNING]
>
>Devido a pequenas diferenças na forma como esses métodos operam, você deve usar ***ou*** OSGI ***ou*** cURL.
>
>Os dois métodos são ***não*** intercambiáveis.

## Habilitar o CRXDE Lite com OSGI {#enabling-crxde-lite-osgi}

Se estiver desativado, você poderá ativar o CRXDE Lite seguindo o procedimento abaixo:

1. Ir para o console de Componentes OSGi em `http://localhost:4502/system/console/components`
1. Procure o seguinte componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Clique no ícone de chave inglesa ao lado dele para ver suas opções de configuração:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Crie a seguinte configuração:

   * **Caminho raiz:** `/crx/server`
   * Marque a caixa em **Usar URIs absolutos**.

1. Quando terminar de usar o CRXDE Lite, desative o WebDAV novamente.

## Habilitar o CRXDE Lite com cURL {#enabling-crxde-lite-curl}

Você também pode ativar o CRXDE Lite via cURL executando (ambos) estes dois comandos:

* Habilitar `create-absolute-uri`:

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&dav.create-absolute-uri=true&propertylist=dav.create-absolute-uri'
  ```

* Definir `alias`:

  ```shell
  curl -u admin:admin 'http://localhost:4502/system/console/configMgr/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet' --data-raw 'apply=true&action=ajaxConfigManager&%24location=&alias=/crx/server&propertylist=alias'
  ```

## Outros recursos {#other-resources}

Para obter mais informações sobre os recursos de segurança do AEM 6, consulte as seguintes páginas:

* [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md)
* [Execução do AEM no modo de produção pronta](/help/sites-administering/production-ready.md)
