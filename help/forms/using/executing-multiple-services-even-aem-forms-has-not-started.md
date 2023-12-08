---
title: A execução de vários serviços apesar do AEM Forms não foi iniciada.
description: Mesmo que a AEM Forms não tenha iniciado totalmente, ela processa vários serviços.
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# A execução de vários serviços apesar do AEM Forms não foi iniciada completamente{#steps-to-resolve-error-after-installing-service-pack}


## Problema {#issue}

Quando o usuário reinicia o AEM Forms, os processos de chamada atuais ainda continuam, como a renderização de documentos PDF e muito mais. Isso faz com que a reinicialização do servidor do AEM Forms não seja feita corretamente.

## Aplica-se a {#applies-to}

A solução se aplica ao AEM Forms no servidor JEE e ao AEM Forms no servidor OSGi.

## Solução {#solution}

Para resolver o problema, os usuários adicionam um argumento `Dcom.adobe.livecycle.dsc.deferServiceStart=true` para [arquivo de lote](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) durante a inicialização do servidor.





