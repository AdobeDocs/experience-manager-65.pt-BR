---
title: Erros de indisponibilidade de serviço do CRX/pacote e da página inicial após a instalação do service pack mais recente do 6.5.15.0
description: Erros de indisponibilidade de serviço do CRX/pacote e da página inicial após a instalação do service pack mais recente do 6.5.15.0
SEO Description: Trouble shooting steps to resolve the errors after installing latest 6.5.15.0 service pack
exl-id: dfe015a3-3a24-41c5-aede-8e086851d62b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%
---
# Erro de serviço indisponível após a instalação do service pack do AEM (6.5.15.0) {#steps-to-resolve-error-after-installing-service-pack}

## Problema {#issue}

Após a instalação do [AEM 6.5.15.0 service pack](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), o erro ocorre como:
* ERRO [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: Não é possível resolver org.apache.sling.scripting.console

Após instalar o pacote de serviços do AEM 6.5.15.0, o CRX/pacote e a página inicial mostram erros de serviço indisponíveis.

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
