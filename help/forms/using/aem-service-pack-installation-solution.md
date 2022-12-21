---
title: CRX/bundle e Start page service unavailable errors depois que o service pack 6.5.15.0 mais recente for instalado
description: CRX/bundle e Start page service unavailable errors depois que o service pack 6.5.15.0 mais recente for instalado
source-git-commit: 974796a6b9e921f8c2f40d72a4764eb9f4d8b92b
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---


# Erro de serviço indisponível após a instalação do AEM (6.5.15.0) service pack {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Depois de instalar o [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), o erro ocorre como:
* ERRO [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERRO (org.osgi.framework.BundleException: Não é possível resolver org.apache.sling.scripting.console

Depois de instalar o AEM 6.5.15.0 service pack, o CRX/bundle e a página de início mostram erros de serviço indisponíveis.

## Aplica-se a {#applies-to}

Esta solução se aplica a:
* AEM Forms em todos os servidores JEE, exceto aqueles executados no JBoss EAP 7.4.0

## Solução {#solution}

>[!NOTE]
>
>As etapas de solução de problemas são aplicáveis a todos os servidores de aplicativos, exceto JBoss EAP 7.4.

Depois de instalar [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se o pacote CRX/e a página inicial mostrarem erros de serviço indisponíveis, execute as seguintes etapas:

1. Pare o servidor de aplicativos.
1. Vá até `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Localize a variável `bundle.info` arquivo.
1. Abra o `bundle.info` no editor de texto de ant e procure pelo nome do pacote como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Caso a variável `bundle.info` under `bundle52` não contém o `org.apache.felix.http.bridge` pacote, verifique o número do pacote entre colchetes ao lado do `org.apache.felix.http.bridge`. Em seguida, navegue até [raiz do aem-forms]\crx-repository\launchpad\felix\bundle[x] e execute as próximas etapas neste local.

1. Vá até o URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Procurar por `bundle.jar` e renomeie o `bundle.jar` para `bundle.jar.bak`.
1. Copie o `Bundle for AEM 6.5 Forms on JEE Service Pack 15` neste local da [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie o servidor de aplicativos, aguarde os logs para estabilizar e verificar o estado do pacote.
1. Depois que todos os pacotes estiverem no estado ativo, instale o [Fragmento para AEM 6.5 Forms no JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) do `system/console/bundles` e aguarde a estabilização do servidor de aplicativos.
1. Pare o servidor de aplicativos.
1. Navegar para `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` e exclua o `bundle.jar`.
1. Renomeie o `bundle.jar.bak` para `bundle.jar`.
1. Inicie o servidor de aplicativos.