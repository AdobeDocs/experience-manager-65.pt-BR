---
title: Como reiniciar o SDK do AEM?
description: Práticas recomendadas para reiniciar o SDK do AEM
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '92'
ht-degree: 1%

---

# Reiniciar o SDK do AEM

Se você reiniciar o SDK do AEM interrompendo os processos do Java™, o poderá causar inconsistências no ambiente de desenvolvimento do AEM. Um erro ocorrerá:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Reiniciar-aem-sdk-erro](/help/forms/using/assets/restart-sdk-error.png)

## Solução

Para reiniciar o SDK do AEM, vá para a janela de comando ativa e pressione o comando `Ctrl + C` para reiniciar o SDK.

É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos do Java™, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
