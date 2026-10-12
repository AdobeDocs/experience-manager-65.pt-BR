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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '156'
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

Para executar uma verificação de consistência, navegue até a página de administração do Mbean JMX **com.adobe.granite (Repositório)**. Na tela principal do AEM, acesse:

**Ferramentas > Console da Web > Principal (na barra de menus) > JMX > com.adobe.granite (Repositório)**

Em uma instalação padrão, ela é encontrada aqui: **[|Mostre-me|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Na seção **Operações** da página, você encontrará dois métodos: **`traversalCheck`** e **`consistencyCheck`**. Para executar uma verificação, clique na operação e insira os parâmetros desejados.

![chlimage_1-117](assets/chlimage_1-117.png)
