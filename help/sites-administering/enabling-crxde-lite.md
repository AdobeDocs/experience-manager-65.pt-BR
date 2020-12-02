---
title: Ativação do CRXDE Lite no AEM
seo-title: Ativação do CRXDE Lite no AEM
description: Saiba como ativar o CRXDE Lite no AEM.
seo-description: Saiba como ativar o CRXDE Lite no AEM.
uuid: d7a3db67-6384-463b-9aa9-f08ecc6c99c6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 72df3ece-badf-466b-8f9a-0ec985d87741
translation-type: tm+mt
source-git-commit: a833a34bbeb938c72cdb851a46b2ffd97aee9f6d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---


# Habilitar CRXDE Lite no AEM{#enabling-crxde-lite-in-aem}

Para garantir que AEM instalações sejam o mais seguras possível, a lista de verificação de segurança recomenda [desativar WebDAV](/help/sites-administering/security-checklist.md#disable-webdav) em ambientes de produção.

No entanto, o CRXDE Lite depende do pacote `org.apache.sling.jcr.davex` para funcionar corretamente, de modo que a desativação do WebDAV também desativará o CRXDE Lite.

Quando isso acontece, a navegação para `https://serveraddress:4502/crx/de/index.jsp` exibirá um nó raiz vazio e todas as solicitações HTTP para recursos de CRXDE Lite falharão:

```xml
404 Resource at '/crx/server/crx.default/jcr:root/.1.json' not found: No resource found
```

Embora essa recomendação tenha como objetivo reduzir ao máximo as superfícies de ataque, os administradores de sistema às vezes podem precisar de acesso ao CRXDE Lite para navegar pelo conteúdo ou depurar problemas nas instâncias de produção.

Se estiver desativado, você pode ativar o CRXDE Lite seguindo o procedimento abaixo:

1. Vá para o console Componentes OSGi em `http://localhost:4502/system/console/components`
1. Procure pelo seguinte componente:

   * `org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`

1. Clique no ícone da chave de fenda ao lado para ver suas opções de configuração:

   ![chlimage_1-80](assets/chlimage_1-80a.png)

1. Crie a seguinte configuração:

   * **Caminho raiz:** `/crx/server`
   * Marque a caixa em **Usar URIs absolutos**.

1. Ao terminar de usar o CRXDE Lite, certifique-se de desativar o WebDAV novamente.

Você também pode ativar o CRXDE Lite via cURL, executando este comando:

```shell
curl -u admin:admin -F "jcr:primaryType=sling:OsgiConfig" -F "alias=/crx/server" -F "dav.create-absolute-uri=true" -F "dav.create-absolute-uri@TypeHint=Boolean" http://localhost:4502/apps/system/config/org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet
```

## Outros recursos {#other-resources}

Para obter mais informações sobre AEM 6 recursos de segurança, consulte as seguintes páginas:

* [A Lista de Verificação de Segurança da AEM](/help/sites-administering/security-checklist.md)
* [Execução de AEM no modo de produção pronto](/help/sites-administering/production-ready.md)

