---
title: Mensagens de erro sobre APIs obsoletas em logs de erros
description: Mensagens de erro sobre APIs obsoletas em logs de erros
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# Mensagens de erro sobre APIs obsoletas em logs de erros {#error-messages-about-deprecated-apis-in-error-logs}

O problema se aplica às seguintes versões:

* Experience Manager 6.5 Forms

## Problema {#issue}

* As seguintes mensagens de erro são exibidas no arquivo error.log:
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## Resolução {#workaround}

1. Instalar [Experience Manager Forms Service Pack 13 ou posterior (6.5.13.0 ou posterior)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=pt-BR)
1. Use o link a seguir para baixar o pacote (arquivo .jar com resolução) da Distribuição de software:

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Abra o Experience Manager Configuration Manager e instale o arquivo baixado com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar.

O problema foi resolvido.