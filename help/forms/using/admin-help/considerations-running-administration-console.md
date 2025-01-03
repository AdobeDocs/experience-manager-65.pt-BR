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
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
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
