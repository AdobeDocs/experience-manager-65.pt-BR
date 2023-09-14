---
title: Considerações ao executar o Console de administração
description: Este documento lista alguns pontos a serem considerados ao executar o Administration Console.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: e33816b3b8d190e185d2b23dad3a05aca272f01c
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Considerações ao executar o Console de administração {#considerations-when-running-administrationconsole}

Estes são alguns aspectos a serem considerados ao executar o Administration Console:

* Se você acessar o console de administração usando o URL `https://[hostname]:'port'/adminui`, o nome de host especificado não pode conter caracteres sublinhados. Caso contrário, os links para algumas áreas do console de administração podem não funcionar corretamente.
* Se você executar um console de administração no Windows Explorer em um sistema operacional japonês, poderá encontrar os seguintes problemas:

   * Clicar em um link o retorna à página de logon em vez do link esperado.
   * Clicar em um link exibe um erro de permissão.

  A prática recomendada é executar o console de administração a partir de outro navegador, como o Mozilla Firefox, para garantir que nenhum link falhe.

* Não use caracteres de barra invertida () ao realizar pesquisas no console de administração.
