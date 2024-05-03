---
title: "Banco de dados DB2&reg;: execução semanal de um processo"
description: Saiba como você pode melhorar o desempenho do seu banco de dados do AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Banco de dados DB2®: execução semanal de um processo{#db-database-running-a-process-weekly}

Se o seu banco de dados AEM Forms DB2® começar a ser executado lentamente, a execução semanal do seguinte processo pode melhorar seu desempenho:

1. Iniciar o DB2® Control Center:

   (Windows) Selecione Iniciar > Programas > IBM® DB2® > Ferramentas administrativas gerais > Centro de controle.

   (Linux® e UNIX®) Em um prompt de comando, digite o `db2jcc` comando.

1. Na árvore de objetos do DB2® Control Center, clique em Todos os Bancos de Dados.
1. Clique no banco de dados criado para o AEM Forms e clique na pasta Tabelas.
1. Selecione todas as tabelas do banco de dados no painel de conteúdo, clique com o botão direito do mouse nelas e selecione Executar estatística.
1. Vá para Estatísticas > Estatísticas de índice.
1. Selecione Coletar Estatísticas para Todos os Índices, selecione Coletar Estatísticas para Índices com Estatísticas Detalhadas Estendidas e clique em OK.

Uma mensagem é exibida quando o processo é concluído. Feche a mensagem.
