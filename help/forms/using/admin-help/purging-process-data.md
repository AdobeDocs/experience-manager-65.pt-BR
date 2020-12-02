---
title: Expurgando dados do processo
seo-title: Expurgando dados do processo
description: Os dados do processo que são gerados quando um processo de longa duração é chamado podem se tornar grandes demais, resultando em menor desempenho de formulários AEM e no uso de espaço em disco desnecessário. Veja como você pode expurgar os dados do processo.
seo-description: Os dados do processo que são gerados quando um processo de longa duração é chamado podem se tornar grandes demais, resultando em menor desempenho de formulários AEM e no uso de espaço em disco desnecessário. Veja como você pode expurgar os dados do processo.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# Expurgando dados do processo {#purging-process-data}

Os dados do processo que são gerados quando um processo de longa duração é chamado podem se tornar grandes demais, resultando em menor desempenho de formulários AEM e no uso de espaço em disco desnecessário. É uma boa prática expurgar os dados do processo quando os registros não forem mais necessários. Os formulários AEM fornecem vários meios de expurgar os dados do processo:

* Você pode usar o console de administração para realizar uma expurgação única de registros obsoletos relacionados a processos de longa duração, ou para programar expurgações automáticas regulares. (Consulte [Limpar registros da base de dados do Gerenciador de Tarefas](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Você pode usar a API Java de formulários AEM e a API de serviço da Web para expurgar programaticamente os dados de processo relacionados a processos duradouros. (Consulte &quot;Expurgando dados do processo&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Use a ferramenta de expurgação do processo para expurgar processos com base no nome do processo e em outros parâmetros. Para obter detalhes, consulte o arquivo readme da ferramenta de expurgação do processo, localizado em *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.

