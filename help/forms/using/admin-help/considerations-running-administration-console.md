---
title: Considerações ao executar o Console de administração
description: Este documento lista alguns pontos a serem considerados ao executar o Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%
---
# Considerações ao executar o Console de administração {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Estes são alguns aspectos a serem considerados ao executar o Administration Console:

* Se você acessar o console de administração usando a URL `https://[hostname]:'port'/adminui`, o nome de host especificado não poderá conter caracteres sublinhados. Caso contrário, os links para algumas áreas do console de administração podem não funcionar corretamente.
* Se você executar um console de administração no Windows Explorer em um sistema operacional japonês, poderá encontrar os seguintes problemas:

  * Clicar em um link o retorna à página de logon em vez do link esperado.
  * Clicar em um link exibe um erro de permissão.

  A prática recomendada é executar o console de administração a partir de outro navegador, como o Mozilla Firefox, para garantir que nenhum link falhe.

* Não use caracteres de barra invertida () ao realizar pesquisas no console de administração.
