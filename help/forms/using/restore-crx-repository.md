---
title: Não foi possível restaurar o repositório CRX corrompido aplicável ao servidor de cluster JEE
description: Etapas para restaurar o repositório CRX corrompido.
exl-id: 212f61f1-360f-4abe-b874-055ec65454c7
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 2%

---

# Não foi possível restaurar o repositório CRX corrompido {#unable-to-restore-corrupt-crx-repository}

## Problema {#issue}

Para o AEM Forms no JEE que usa um banco de dados relacional, o tempo na máquina que hospeda o AEM Forms e o banco de dados relacional devem estar sempre em sincronia absoluta. Se o tempo nessas máquinas ficar fora de sincronia, o repositório CRX do AEM Forms no servidor JEE poderá se tornar inacessível. Ele pode parecer corrompido e se tornar inacessível por meio do URL. A variável `AuthenticationsupportService missing` erro registrado.

## Pré-requisitos {#prerequisites}

Faça o backup do seu repositório CRX antes de executar as etapas mencionadas abaixo.

## Solução {#solution}

Execute as seguintes etapas para resolver o problema:
1. Acesse  `https://[AEM Forms Server]:[port]/system/console/bundles`.

1. Localize o `oak-core` pacote e verifique se ele está em execução.

1. Reinicie o `oak-core` pacote se não estiver em execução. Se  ![Botão Pausar](/help/forms/using/assets/stop.png) O ícone está presente na frente do `oak-core` pacote, então indica que o pacote está em estado de execução.

1. Se o problema ainda não for resolvido, restaure do repositório CRX a partir do backup ou recrie o repositório CRX se o backup não estiver disponível.


## Aplica-se a {#applies-to}

Esta solução aplica-se a:

* AEM Forms no cluster JEE