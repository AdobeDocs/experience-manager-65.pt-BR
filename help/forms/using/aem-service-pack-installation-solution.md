---
title: Erros de indisponibilidade de serviço do CRX/pacote e da página inicial após a instalação do service pack mais recente do 6.5.15.0
description: Erros de indisponibilidade de serviço do CRX/pacote e da página inicial após a instalação do service pack mais recente do 6.5.15.0
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 2%

---

# Erro de serviço indisponível após a instalação do pacote de serviços do AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Depois de instalar o [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), o erro ocorre:
* ERRO [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Não é possível resolver org.apache.sling.scripting.console

Após instalar o pacote de serviços AEM 6.5.15.0, o CRX/pacote e a página inicial mostram erros de serviço indisponíveis.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:
* AEM Forms em todos os servidores JEE, exceto aqueles executados no JBoss EAP 7.4.0

## Solução {#solution}

>[!NOTE]
>
>As etapas de solução de problemas são aplicáveis a todos os servidores de aplicativos, exceto o JBoss EAP 7.4.

Depois de instalar o [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se o CRX/pacote e a página inicial mostrarem erros de serviço indisponível, execute as seguintes etapas:

1. Interrompa o servidor de aplicativos.
1. Vá até `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Localize o arquivo `bundle.info`.
1. Abra o arquivo `bundle.info` no editor de texto ant e procure o nome do pacote como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Caso o `bundle.info` em `bundle52` não contenha o pacote `org.apache.felix.http.bridge`, verifique o número do pacote em colchetes ao lado de `org.apache.felix.http.bridge`. Em seguida, navegue até [raiz do aem-forms]\crx-repository\launchpad\felix\bundle[x] e execute as próximas etapas neste local.

1. Navegue até a URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Pesquise por `bundle.jar` e renomeie o `bundle.jar` como `bundle.jar.bak`.
1. Copie o `Bundle for AEM 6.5 Forms on JEE Service Pack 15` neste local da [Distribuição de Software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie o servidor de aplicativos, aguarde os logs estabilizarem e verifique o estado do pacote.
1. Quando todos os pacotes estiverem no estado ativo, instale o [Fragment for AEM 6.5 Forms no JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) a partir do `system/console/bundles` e aguarde a estabilização do servidor de aplicativos.
1. Interrompa o servidor de aplicativos.
1. Navegue até `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` e exclua o `bundle.jar`.
1. Renomeie o `bundle.jar.bak` para `bundle.jar`.
1. Inicie o servidor de aplicativos.
