---
title: Limpando dados do processo
description: Os dados de processo gerados quando um processo de longa duração é chamado podem se tornar muito grandes, resultando em menor desempenho dos formulários AEM e no uso de espaço em disco desnecessário. Veja como você pode limpar dados de processo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Limpando dados do processo {#purging-process-data}

Os dados de processo gerados quando um processo de longa duração é chamado podem se tornar muito grandes, resultando em menor desempenho dos formulários AEM e no uso de espaço em disco desnecessário. É uma boa prática limpar os dados do processo quando os registros não são mais necessários. Os formulários AEM fornecem vários meios de limpar dados de processo:

* Você pode usar o console de administração para executar uma expurgação única de registros obsoletos relacionados a processos de longa duração ou para programar expurgações automáticas regulares. (Consulte [Expurgar registros do banco de dados do Gerenciador de Jobs](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Você pode usar a API Java dos formulários AEM e a API do serviço da Web para limpar programaticamente os dados do processo relacionados aos processos de longa duração. (Consulte &quot;Expurgação de dados do processo&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Use a ferramenta de limpeza de processos para remover processos com base no nome do processo e em outros parâmetros. Para obter detalhes, consulte o arquivo readme da ferramenta de limpeza de processos, em *[raiz de aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
