---
title: Expurgar registros do banco de dados do Gerenciador de Jobs
description: Dados de processos grandes podem resultar em um desempenho de formulários AEM mais baixo. É uma boa prática limpar os dados do processo quando os registros não são mais necessários.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5279f6c3-5954-472c-9ea0-18e8a7ec860e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---

# Expurgar registros do banco de dados do Gerenciador de Jobs {#purge-records-from-the-job-manager-database}

Os dados de processo gerados quando um processo de longa duração é chamado podem se tornar muito grandes, resultando em menor desempenho dos formulários AEM e no uso de espaço em disco desnecessário. É uma boa prática limpar os dados do processo quando os registros não são mais necessários.

Você pode usar a console de administração para executar uma expurgação única de registros obsoletos ou para programar expurgações automáticas regulares. Outros métodos para expurgar registros obsoletos são discutidos em [Limpando dados do processo](/help/forms/using/admin-help/purging-process-data.md#purging-process-data).

**Acessar a página Programador de Expurgação do Job**

1. No Console de administração, clique em Monitor de integridade no canto superior direito da página.
1. Clique na guia Agendador de Expurgação de Job.

As informações sobre expurgações programadas no momento são exibidas na caixa Informações do Agendador de Expurgação de Job.

>[!NOTE]
>
>Clicar em Interromper Scheduler interrompe todas as expurgações programadas no futuro, mas não interrompe um job de expurgação que já esteja em andamento.

**Programar uma limpeza única**

1. Selecione Somente Uma Vez.
1. Na área Filtro de Registros de Expurgação Concluída, especifique o número de dias ou semanas após os quais um registro será considerado obsoleto e pronto para expurgação.

   >[!NOTE]
   >
   >Os registros relacionados a processos que não foram concluídos não serão removidos, mesmo se forem mais antigos que a idade especificada.

1. Especifique quando a limpeza ocorrerá. Marque a caixa de seleção Usar data e hora atuais ou desmarque a caixa de seleção e clique nos ícones de calendário e relógio para especificar a data e a hora em que a limpeza será realizada.

   >[!NOTE]
   >
   >Se você especificar uma data e hora iniciais que estejam no passado, a expurgação ocorrerá imediatamente quando você clicar em Iniciar Scheduler.

1. Clique em Iniciar Scheduler. Todas as configurações do scheduler previamente agendadas são substituídas pelas novas configurações.

**Configurar um agendamento de limpeza automática**

1. Selecione Repetir a Cada e especifique o número de dias ou semanas entre expurgações.
1. Na área Filtro de Registros de Expurgação Concluída, especifique o número de dias ou semanas após os quais um registro será considerado obsoleto e pronto para expurgação. Não é possível definir o valor como `0`.

   >[!NOTE]
   >
   >Os registros relacionados a processos que não foram concluídos não serão removidos, mesmo se forem mais antigos que a idade especificada.

1. Especifique quando as limpezas começarão. Marque a caixa de seleção Usar data e hora atuais ou desmarque a caixa de seleção e clique nos ícones de calendário e relógio para especificar a data e a hora em que a limpeza será realizada.

   >[!NOTE]
   >
   >Se você especificar uma data e hora de início que esteja no passado, os formulários AEM calcularão a próxima data de início lógica com base na data especificada. Por exemplo, se você programar que as expurgações de job ocorram semanalmente a partir de 7 de abril e agora for 9 de abril, a primeira expurgação ocorrerá em 14 de abril.

1. Clique em Iniciar Scheduler. Todas as configurações do scheduler previamente agendadas são substituídas pelas novas configurações.
