---
title: O AEM Forms Server inicia o processamento dos documentos mesmo antes de todos os serviços estarem em execução.
description: O AEM Forms Server inicia o processamento dos documentos mesmo antes de todos os serviços estarem em execução no JEE Server e no OSGi Server.
source-git-commit: 6f2b16a51d4ad0f5c199ff41e8abe150c27ecc01
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# O AEM Forms Server inicia o processamento dos documentos antes mesmo que todos os serviços estejam em execução{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problema {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Antes que o servidor do AEM Forms esteja totalmente ativo e todos os aplicativos estejam em execução, o servidor do AEM Forms inicia o processamento dos documentos.


## Aplica-se a {#applies-to}

A solução se aplica ao AEM Forms no servidor JEE e ao AEM Forms no servidor OSGi.

## Solução {#solution}

Para resolver o problema, adicione um argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` para o [arquivo de lote](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante a inicialização do servidor.
