---
title: Minificação dos arquivos JavaScript
description: Instruções para gerar código minificado após as personalizações do espaço de trabalho do AEM Forms para otimizar os arquivos JS para a Web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# Minificação dos arquivos JavaScript {#minification-of-the-javascript-files}

A minificação remove do código-fonte os caracteres redundantes, como espaço em branco, novas linhas e comentários. Isso melhora o desempenho ao reduzir o tamanho do código. Embora a minificação não afete a funcionalidade, ela reduz a legibilidade do código.

Para gerar um código minificado para alterações semânticas, siga estas etapas.

1. Copie `client-html/src/main/webapp/js` de src-package no sistema de arquivos.

   >[!NOTE]
   >
   >Consulte [Introdução à personalização do espaço de trabalho do AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) para obter mais detalhes sobre os pacotes.

1. Atualizar caminhos em `main.js`, localizado em client-html/src/main/webapp/js, para modelos/exibições adicionados/atualizados.

   Por exemplo, a adição de um novo modelo Sharequeue, digamos mySharequeue, altera:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   Para

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Atualizar `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` caso haja alteração/adição de alias em `main.js`.

   Por exemplo, a adição de um novo modelo Sharequeue, digamos mySharequeue, altera:

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/models/sharequeue.js"
               service="service"/>
   ```

   Para

   ```xml
   <sharequeue
               name="sharequeue"
               path="runtime/myModels/mySharequeue.js"
               service="service"/>
   ```

1. Em client-html/src/main/webapp/js/minifier, execute o comando:

   ```shell
   mvn clean install
   ```

   Ele gera uma pasta de arquivos minificados, em client-html/src/main/webapp/js com main.js e registry.js minificados.

>[!NOTE]
>
>A minificação só funciona em uma JVM de 64 bits.

>[!NOTE]
>
>Se você minificar, sua atualização será afetada.
