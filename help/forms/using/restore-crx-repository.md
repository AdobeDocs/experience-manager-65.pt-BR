---
title: Não é possível restaurar o repositório CRX corrompido aplicável ao servidor de cluster JEE
description: Etapas para restaurar o repositório CRX corrompido
source-git-commit: a7d125503b0bd3c52cb3a959e2f0dde1a69cbe2b
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# Não é possível restaurar o repositório CRX corrompido {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para o AEM Forms implantado no JEE com persistência de RDB, é necessário que as máquinas de host e máquinas de banco de dados do AEM Forms estejam em sincronização de tempo absoluto. No entanto, se por algum motivo os relógios saírem da sincronização, o repositório CRX será corrompido e seus URLs ficarão inacessíveis. O erro como `AuthenticationsupportService missing` ocorre em arquivos de log.

## Solução {#solution}

Execute as seguintes etapas para resolver o problema:
1. Ir para  [https://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).

1. Localize a variável `oak-core` e verifique se está em execução.

1. Reinicie o `oak-core` pacote se não estiver em execução. Se o botão pausar estiver presente na frente do `oak-core` , então indica que o pacote está em estado de execução.

1. Se o problema ainda não for resolvido, restaure a partir do repositório CRX a partir do backup ou recrie o repositório CRX se o backup não estiver disponível.

   >[!NOTE]
   >
   >Faça o backup do seu repositório CRX antes de executar as etapas acima.

## Aplica-se a {#applies-to}

Esta solução se aplica a:

* AEM Forms no servidor de cluster JEE


