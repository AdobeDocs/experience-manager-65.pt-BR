---
title: Verificações de consistência e passagem
description: Saiba como executar verificações de consistência e percurso.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
feature: Configuring
exl-id: 10dde29b-5dc7-4d4e-80ae-3d4fd0397f7e
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Verificações de consistência e passagem{#consistency-and-traversal-checks}

Durante a atualização, pode haver problemas devido a inconsistências no espaço de trabalho. Você pode executar uma atualização de teste para ver se isso é um problema ou executar as verificações de consistência como uma ação preventiva.

Se você executar uma atualização de teste que falha devido a inconsistências no espaço de trabalho, verá entradas semelhantes às seguintes em crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Executar uma verificação de consistência {#perform-a-consistency-check}

Para executar uma verificação de consistência, navegue até a página de administração do bean JMX **com.adobe.granite (Repositório)**. Na tela principal do AEM, acesse:

**Ferramentas > Console da Web > Principal (na barra de menus) > JMX > com.adobe.granite (Repositório)**

Em uma instalação padrão, ela é encontrada aqui:  **[|Mostre-me|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

No **Operações** da página, você encontrará dois métodos: **`traversalCheck`** e **`consistencyCheck`**. Para executar uma verificação, clique na operação e insira os parâmetros desejados.

![chlimage_1-117](assets/chlimage_1-117.png)
