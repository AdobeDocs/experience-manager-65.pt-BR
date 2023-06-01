---
title: Falha na implantação do EAR no JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Etapas para resolver falha de Implantação EAR no JEE WebLogic Server
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 6%

---


# Falha na implantação do EAR no JEE WebLogic Server {#ear-deployment-failing-on-jee-weblogic-server}

## Problema {#issue}

Quando um usuário tenta implantar o `adobe-livecycle-weblogic.ear`, o `Null Pointer` exceção encontrada.

## Aplica-se a {#applies-to}

Esta solução aplica-se a:

* AEM Forms no servidor WebLogic JEE versão 12.2.1.x.

## Solução {#solution}

Para resolver o problema, siga estas etapas:

1. Vá para a `<domain_home>\bin` diretório do servidor WebLogic JEE instalado.

1. Edite o `setDomainEnv.cmd` ou `setDomainEnv.sh` arquivo, como `applicable`.

1. Pesquisar a última ocorrência de `JAVA_OPTS` e adicionar `-DANTLR_USE_DIRECT_CLASS_LOADING=true` a ele. Por exemplo, a string atualizada é exibida como:

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Salve as alterações.


