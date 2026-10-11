---
title: Como reiniciar o AEM SDK?
description: Práticas recomendadas para reiniciar o AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms,AEM Forms on JEE,AEM Forms on OSGi
exl-id: f5d69d04-b842-4329-b1b3-57b88266d13d
solution: Experience Manager, Experience Manager Forms
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: 8c4fb903-572c-5473-ad45-8ebb0d5d8134
    internal-label: AEM Forms on OSGi
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 1%
---
# Reiniciar o AEM SDK

Se você reiniciar o AEM SDK interrompendo os processos do Java™, o poderá causar inconsistências no ambiente de desenvolvimento do AEM, e um erro ocorrerá:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Reiniciar-aem-sdk-erro](/help/forms/using/assets/restart-sdk-error.png)

## Solução

Para reiniciar o AEM SDK, vá para a janela de comando ativa e pressione o comando `Ctrl + C` para reiniciar o SDK.

É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java™, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
