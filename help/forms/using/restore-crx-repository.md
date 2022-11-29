---
title: Não é possível restaurar o repositório CRX corrompido aplicável ao servidor de cluster JEE
description: Etapas para restaurar o repositório CRX corrompido
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: c4f776b08cb8cc8c6eea78a3757735e063bec20c
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Não é possível restaurar o repositório CRX corrompido {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para o AEM Forms no JEE que usa um banco de dados relacional, o tempo no computador que hospeda o AEM Forms e o banco de dados relacional sempre devem estar em sincronização absoluta. Se o tempo nessas máquinas ficar fora de sincronia, o repositório CRX do AEM Forms no servidor JEE pode se tornar inacessível. Ele pode parecer corrompido e se tornar inacessível via URL. O `AuthenticationsupportService missing` está registrado.

## Pré-requisitos {#prerequisites}

Faça o backup do seu repositório CRX antes de executar as etapas abaixo mencionadas.

## Solução {#solution}

Execute as seguintes etapas para resolver o problema:
1. Ir para  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Localize a variável `oak-core` e verifique se está em execução.

1. Reinicie o `oak-core` pacote se não estiver em execução. If  ![Botão Pausar](/help/forms/using/assets/stop.png) está presente na frente do `oak-core` , então indica que o pacote está em estado de execução.

1. Se o problema ainda não for resolvido, restaure a partir do repositório CRX a partir do backup ou recrie o repositório CRX se o backup não estiver disponível.


## Aplica-se a {#applies-to}

Esta solução se aplica a:

* AEM Forms no cluster JEE