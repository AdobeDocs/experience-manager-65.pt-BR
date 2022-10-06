---
title: Minificação dos arquivos JavaScript
seo-title: Minification of the JavaScript files
description: Instruções para gerar código minificado após as personalizações do espaço de trabalho do AEM Forms para otimizar os arquivos JS para a Web.
seo-description: Instructions to generate minified code after AEM Forms workspace customizations to optimize the JS files for the web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
exl-id: d88c6831-8ae9-426d-acb5-2a7e066ad158
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---

# Minificação dos arquivos JavaScript {#minification-of-the-javascript-files}

A minificação remove do código-fonte os caracteres redundantes, como espaço em branco, nova linha e comentários. Isso melhora o desempenho ao reduzir o tamanho do código. Embora a minificação não afete a funcionalidade, ela reduz a legibilidade do código.

Para gerar código minificado para alterações semânticas, siga essas etapas.

1. Copiar `client-html/src/main/webapp/js` do src-package no sistema de arquivos.

   >[!NOTE]
   >
   >Consulte [Introdução à Personalização do espaço de trabalho do AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md) para obter mais detalhes sobre os pacotes.

1. Atualizar caminhos em `main.js` localizado em client-html/src/main/webapp/js, para modelos/visualizações adicionados/atualizados.

   Por exemplo, a adição de um novo modelo do Sharequue, digamos mySharequue, muda:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   Para

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Atualizar `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` em caso de alteração/adição de alias em `main.js`.

   Por exemplo, a adição de um novo modelo do Sharequue, digamos mySharequue, muda:

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

   Ele gera uma pasta arquivos minificados, em client-html/src/main/webapp/js com minificações main.js e registry.js.

>[!NOTE]
>
>A minificação só funcionará na JVM de 64 bits.

>[!NOTE]
>
>Se você diminuir, a atualização será afetada.
