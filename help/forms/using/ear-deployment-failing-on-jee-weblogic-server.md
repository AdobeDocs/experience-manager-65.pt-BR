---
title: Falha na implantação do EAR no JEE WebLogic Server
description: Etapas para resolver falha de Implantação EAR no JEE WebLogic Server
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
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
