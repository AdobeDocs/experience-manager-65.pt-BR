---
title: Erros de indisponibilidade de serviço de pacote CRX/página inicial após a instalação do service pack mais recente do 6.5.15.0
description: Erros de indisponibilidade de serviço de pacote CRX/página inicial após a instalação do service pack mais recente do 6.5.15.0
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

Após instalar o [Pacote de serviços para AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), o erro ocorre como:
* ERRO [FelixDispatchQueue] org.apache.sling.scripting.console FrameworkEvent ERROR (org.osgi.framework.BundleException: não é possível resolver org.apache.sling.scripting.console

Após instalar o pacote de serviço AEM 6.5.15.0, o CRX/bundle e a página inicial mostram erros de serviço indisponíveis.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:
* AEM Forms em todos os servidores JEE, exceto aqueles executados no JBoss EAP 7.4.0

## Solução {#solution}

>[!NOTE]
>
>As etapas de solução de problemas são aplicáveis a todos os servidores de aplicativos, exceto o JBoss EAP 7.4.

Após a instalação [Pacote de serviços para AEM 6.5.15.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.15.0.zip), se o CRX/pacote e a página inicial mostrarem erros de serviço indisponível, execute as seguintes etapas:

1. Interrompa o servidor de aplicativos.
1. Vá até `[aem-forms root]\crx-repository\launchpad\felix\bundle52`.
1. Localize o `bundle.info` arquivo.
1. Abra o `bundle.info` arquivo no editor de texto ant e procure pelo nome do pacote como `org.apache.felix.http.bridge`.

   >[!NOTE]
   >
   >Caso a variável `bundle.info` em `bundle52` não contém o `org.apache.felix.http.bridge` pacote, verifique o número do pacote em colchetes ao lado da tag `org.apache.felix.http.bridge`. Em seguida, acesse [raiz de aem-forms]\crx-repository\launchpad\felix\bundle[x] e execute as próximas etapas neste local.

1. Navegue até o URL: `[aem-forms root]\crx-repository\launchpad\felix\bundle[x]\version0.1`.
1. Pesquisar por `bundle.jar` e renomeie o `bundle.jar` para `bundle.jar.bak`.
1. Copie o `Bundle for AEM 6.5 Forms on JEE Service Pack 15` neste local do [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/bundle.jar).
1. Inicie o servidor de aplicativos, aguarde os logs estabilizarem e verifique o estado do pacote.
1. Quando todos os pacotes estiverem no estado ativo, instale o [Fragmento para AEM 6.5 Forms no JEE Service Pack 15](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/org.apache.felix.http.servlet-api-1.2.0_fragment_full.jar) do `system/console/bundles` e aguarde a estabilização do servidor de aplicativos.
1. Interrompa o servidor de aplicativos.
1. Navegue até `[aem-forms root]\crx-repository\launchpad\felix\bundle52\version0.1` e exclua a variável `bundle.jar`.
1. Renomeie o `bundle.jar.bak` para o `bundle.jar`.
1. Inicie o servidor de aplicativos.
