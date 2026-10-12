---
title: Não foi possível restaurar o repositório CRX corrompido aplicável ao servidor de cluster JEE
description: Saiba mais sobre como restaurar um repositório do CRX corrompido.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
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
source-wordcount: '184'
ht-degree: 1%
---
# Não foi possível restaurar o repositório CRX corrompido {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para o AEM Forms no JEE que usa um banco de dados relacional, o tempo na máquina que hospeda o AEM Forms e o banco de dados relacional devem estar sempre em sincronia absoluta. Se o tempo nessas máquinas sair de sincronia, o repositório do CRX do AEM Forms no servidor JEE poderá ficar inacessível. Ele pode parecer corrompido e se tornar inacessível por meio do URL. O erro `AuthenticationsupportService missing` foi registrado em log.

## Pré-requisitos {#prerequisites}

Faça o backup do seu repositório CRX antes de executar as etapas mencionadas abaixo.

## Solução {#solution}

1. Ir para `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Localize o pacote `oak-core` e verifique se ele está em execução.

1. Reinicie o pacote `oak-core` se ele não estiver em execução. Se o ícone do ![Botão Pausar](/help/forms/using/assets/stop.png) estiver presente na frente do pacote `oak-core`, isso indicará que o pacote está em estado de execução.

1. Se o problema ainda não for resolvido, restaure a partir do repositório da CRX a partir do backup ou recrie o repositório da CRX se o backup não estiver disponível.


## Aplica-se a {#applies-to}

Essa solução se aplica ao AEM Forms no cluster JEE.
