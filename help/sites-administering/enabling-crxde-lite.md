---
title: CRXDE Lite no AEM
seo-title: Enabling CRXDE Lite in AEM
description: Saiba como ativar o CRXDE Lite no Adobe Experience Manager.
seo-description: Learn how to enable CRXDE Lite in AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
exl-id: bf51def2-1dd4-4bd3-b989-685058f0ead8
source-git-commit: e54c1d422f2bf676e8a7b0f50a101e495c869c96
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# CRXDE Lite no AEM{#enabling-crxde-lite-in-aem}

Para garantir que as instalações do AEM sejam o mais seguras possível, a lista de verificação de segurança recomenda [desabilitar WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) em ambientes de produção.

No entanto, o CRXDE Lite depende da `org.apache.sling.jcr.davex` para funcionar corretamente, de modo que desabilitar WebDAV também desabilitará efetivamente o CRXDE Lite.

Quando isso acontecer, navegue até `https://serveraddress:4502/crx/de/index.jsp` exibirá um nó raiz vazio e todas as solicitações HTTP para os recursos CRXDE Lite falharão:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Embora essa recomendação tenha como objetivo reduzir ao máximo as superfícies de ataque, os administradores do sistema podem, às vezes, precisar acessar o CRXDE Lite para navegar pelo conteúdo ou depurar problemas em instâncias de produção.

Você pode habilitar o CRXDE Lite com [Configurações de OSGi](#enabling-crxde-lite-osgi) ou com um [comando cURL](#enabling-crxde-lite-curl).

>[!WARNING]
>
>Devido a pequenas diferenças em como esses métodos operam, você deve usar ***ou*** OSGI ***ou*** cURL.
>
>Os dois métodos ***não*** intercambiável.

## Habilitar o CRXDE Lite com OSGI {#enabling-crxde-lite-osgi}

Se desativado, você pode ativar o CRXDE Lite seguindo o procedimento abaixo:

1. Acesse o console de Componentes OSGi em `http://localhost:4502/system/console/components`
1. Procure o seguinte componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Clique no ícone de chave inglesa ao lado dele para ver suas opções de configuração:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Crie a seguinte configuração:

   * **Caminho raiz:** `/crx/server`
   * Marque a caixa em **Usar URIs absolutos**.

1. Quando terminar de usar o CRXDE Lite, certifique-se de desativar o WebDAV novamente.

## Habilitar CRXDE Lite com cURL {#enabling-crxde-lite-curl}

Você também pode ativar o CRXDE Lite via cURL executando este comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Outros recursos {#other-resources}

Para obter mais informações sobre os recursos de segurança do AEM 6, consulte as seguintes páginas:

* [Lista de verificação de segurança do AEM](/help/sites-administering/security-checklist.md)
* [Execução do AEM no modo de produção pronta](/help/sites-administering/production-ready.md)
