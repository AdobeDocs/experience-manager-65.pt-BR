---
title: Minificação dos arquivos JavaScript
seo-title: Minificação dos arquivos JavaScript
description: Instruções para gerar código minified após personalizações de espaço de trabalho do AEM Forms para otimizar os arquivos JS para a Web.
seo-description: Instruções para gerar código minified após personalizações de espaço de trabalho do AEM Forms para otimizar os arquivos JS para a Web.
uuid: ad91e380-a988-4740-9534-e09657e0322a
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c88a3013-5da2-4b09-9f29-ac1fb00822ec
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Minificação dos arquivos JavaScript {#minification-of-the-javascript-files}

A Minificação remove do código-fonte os caracteres redundantes, como espaço em branco, nova linha e comentários. Isso melhora o desempenho, reduzindo o tamanho do código. Embora a minimização não afete a funcionalidade, ela reduz a legibilidade do código.

Para gerar um código minified para alterações semânticas, siga estas etapas.

1. Copiar `client-html/src/main/webapp/js` de src-package no sistema de arquivos.

   >[!NOTE]
   >
   >Consulte [Introdução à área de trabalho](/help/forms/using/introduction-customizing-html-workspace.md) Personalizar AEM Forms para obter mais detalhes sobre os pacotes.

1. Atualize os caminhos em `main.js` client-html/src/main/webapp/js para modelos/visualizações adicionados/atualizados.

   Por exemplo, adição de um novo modelo do Sharequeue, digamos mySharequeue, alterar:

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/models/sharequeue',
   ```

   Para

   ```javascript
   sharequeuemodel : pathprefix + 'runtime/myModels/mySharequeue',
   ```

1. Atualize `registry-config.xml, located at client-html/src/main/webapp/js/resource_generator,` caso haja alteração/adição de alias em `main.js`.

   Por exemplo, adição de um novo modelo do Sharequeue, digamos mySharequeue, alterar:

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

1. No client-html/src/main/webapp/js/minifier, execute o comando:

   ```shell
   mvn clean install
   ```

   Ele gera uma pasta em minified-files, em client-html/src/main/webapp/js com minified main.js e registry.js.

>[!NOTE]
>
>A Minificação só funcionará com JVM de 64 bits.

>[!NOTE]
>
>Se você minimizar, a atualização será afetada.
