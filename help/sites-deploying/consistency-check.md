---
title: Verificações de consistência e passagem
seo-title: Verificações de consistência e passagem
description: Saiba como executar verificações de consistência e travessia.
seo-description: Saiba como executar verificações de consistência e travessia.
uuid: 0304e378-7c60-4bf5-9052-d01149d2a6df
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: af9a3e9d-194a-42e5-be28-b238e0c1e55e
feature: Configuração
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---


# Verificações de consistência e passagem{#consistency-and-traversal-checks}

Ao atualizar, pode haver problemas devido a inconsistências no espaço de trabalho. Você pode executar uma atualização de teste para ver se isso será um problema ou executar as verificações de consistência como ação preventiva.

Se você executar uma atualização de teste que falhar devido a inconsistências do espaço de trabalho, verá entradas semelhantes às seguintes em crx-quickstart/logs/crx/error.log:

```xml
*ERROR* TarPersistenceManager: No bundle found for uuid 'deadbeef-cafe-babe-cafe-babecafebabe'
 ...
*ERROR* RepositoryImpl: Failed to initialize workspace 'crx.default'
javax.jcr.RepositoryException: Error indexing workspace: Error indexing workspace: Error indexing workspace
...
```

## Executar uma verificação de consistência {#perform-a-consistency-check}

Para executar uma verificação de consistência, navegue até a página de administração do JMX Mbean** com.adobe.granite (Repositório)**. Na tela principal do AEM, acesse:

**Ferramentas > Console da Web > Principal (na barra de menu) > JMX > com.adobe.granite (Repositório)**

Em uma instalação padrão, ela é encontrada aqui:  **[|Mostrar-me|](http://localhost:4502/system/console/jmx/com.adobe.granite%3Atype%3DRepository)**

Na seção **Operations** da página, você encontrará dois métodos: **`traversalCheck`** e **`consistencyCheck`**. Para executar uma verificação, clique na operação e insira os parâmetros desejados.

![chlimage_1-117](assets/chlimage_1-117.png)

