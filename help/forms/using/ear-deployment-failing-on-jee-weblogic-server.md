---
title: Falha na implantação do EAR no JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Etapas para resolver falha de Implantação EAR no JEE WebLogic Server
source-git-commit: 05712cfcef1d9c37b7cd015133abaf6df0e351d2
workflow-type: tm+mt
source-wordcount: '97'
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
