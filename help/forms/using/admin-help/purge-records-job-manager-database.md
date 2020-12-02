---
title: Expurgar registros do banco de dados do Gerenciador de Jobs
seo-title: Expurgar registros do banco de dados do Gerenciador de Jobs
description: Dados de processos grandes podem resultar em desempenho de formulários de AEM menor. É uma boa prática expurgar os dados do processo quando os registros não forem mais necessários.
seo-description: Dados de processos grandes podem resultar em desempenho de formulários de AEM menor. É uma boa prática expurgar os dados do processo quando os registros não forem mais necessários.
uuid: cf214498-36e9-4dcc-b4d4-e7c46f80dbab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 69a406f2-4fa8-40bb-b671-7b0f5b6a2c4c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---


# Expurgar registros do banco de dados do Gerenciador de Jobs {#purge-records-from-the-job-manager-database}

Os dados do processo que são gerados quando um processo de longa duração é chamado podem se tornar grandes demais, resultando em menor desempenho de formulários AEM e no uso de espaço em disco desnecessário. É uma boa prática expurgar os dados do processo quando os registros não forem mais necessários.

Você pode usar o console de administração para realizar uma expurgação única de registros obsoletos ou para programar expurgações automáticas regulares. Outros métodos para expurgar registros obsoletos são discutidos em [Expurgando dados do processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Acessar a página Scheduler de Expurgação da Tarefa**

1. No Console de administração, clique em Monitor de integridade no canto superior direito da página.
1. Clique na guia Scheduler de Expurgação da Tarefa.

As informações sobre quaisquer expurgações programadas no momento são exibidas na caixa Informações sobre o Scheduler de Expurgação da Ordem de Produção.

>[!NOTE]
>
>Clicar em Parar Scheduler interrompe quaisquer expurgações programadas no futuro, mas não interrompe um trabalho de expurgação já em andamento.

**Agendar uma expurgação única**

1. Selecione Somente uma vez.
1. Na área Expurgar Filtro de Registros Concluídos, especifique o número de dias ou semanas após os quais um registro é considerado obsoleto e pronto para expurgação.

   >[!NOTE]
   >
   >Os registros relacionados a processos que não foram concluídos não são removidos, mesmo se forem mais antigos que a idade especificada.

1. Especifique quando a expurgação ocorrerá. Marque a caixa de seleção Usar data e hora atuais ou desmarque a caixa de seleção e clique nos ícones de calendário e relógio para especificar a data e a hora em que a expurgação será executada.

   >[!NOTE]
   >
   >Se você especificar uma data e hora do start que esteja no passado, a expurgação ocorrerá imediatamente quando você clicar em Scheduler do Start.

1. Clique em Start Scheduler. Quaisquer configurações de scheduler programadas anteriormente serão substituídas pelas novas configurações.

**Configurar uma programação de expurgação automática**

1. Selecione Retornar a cada e especifique o número de dias ou semanas entre purgações.
1. Na área Expurgar Filtro de Registros Concluídos, especifique o número de dias ou semanas após os quais um registro é considerado obsoleto e pronto para expurgação. Não é possível definir o valor como `0`.

   >[!NOTE]
   >
   >Os registros relacionados a processos que não foram concluídos não são removidos, mesmo se forem mais antigos que a idade especificada.

1. Especifique quando as purgações começarão. Marque a caixa de seleção Usar data e hora atuais ou desmarque a caixa de seleção e clique nos ícones de calendário e relógio para especificar a data e a hora em que a expurgação será executada.

   >[!NOTE]
   >
   >Se você especificar uma data e uma hora de start no passado, AEM formulários calculará a data lógica do próximo start com base na data especificada. Por exemplo, se você agendar as expurgações da ordem de produção para ocorrer semanalmente a partir de 7 de abril, e agora for 9 de abril, a primeira expurgação ocorrerá em 14 de abril.

1. Clique em Start Scheduler. Quaisquer configurações de scheduler programadas anteriormente serão substituídas pelas novas configurações.

