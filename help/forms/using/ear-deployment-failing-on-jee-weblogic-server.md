---
title: Falha na implantação do EAR no JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Etapas para resolver falha de Implantação EAR no JEE WebLogic Server
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 7%
---
# Falha na implantação do EAR no JEE WebLogic Server {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

Quando um usuário tenta implantar o `adobe-livecycle-weblogic.ear`, a exceção `Null Pointer` é encontrada.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:

* AEM Forms no servidor WebLogic JEE versão 12.2.1.x.

## Solução {#solution}

Para resolver o problema, siga estas etapas:

1. Vá para o diretório `<domain_home>\bin` do servidor WebLogic JEE instalado.

1. Edite o arquivo `setDomainEnv.cmd` ou `setDomainEnv.sh` como `applicable`.

1. Pesquise a última ocorrência de `JAVA_OPTS` e adicione `-DANTLR_USE_DIRECT_CLASS_LOADING=true` a ela. Por exemplo, a string atualizada é exibida como:

       definir `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Salve as alterações.
