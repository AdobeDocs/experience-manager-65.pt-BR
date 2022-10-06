---
title: "Banco de dados DB2: Executar um processo semanalmente"
seo-title: "DB2 database: Running a process weekly"
description: Veja como você pode melhorar o desempenho do banco de dados do AEM forms DB2.
seo-description: See how you can improve the performance of your AEM forms DB2 database.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Banco de dados DB2: Execução de um processo semanal{#db-database-running-a-process-weekly}

Se o banco de dados do AEM forms DB2 começar a ser executado lentamente, executar o seguinte processo semanalmente poderá melhorar o desempenho:

1. Iniciar o Centro de Controle do DB2:

   (Windows) Selecione Iniciar > Programas > IBM DB2 > Ferramentas Administrativas Gerais > Centro de Controle.

   (Linux e UNIX) Em um prompt de comando, digite o `db2jcc` comando.

1. Na árvore de objetos do Centro de Controle de DB2, clique em Todos os Bancos de Dados.
1. Clique no banco de dados criado para AEM formulários e clique na pasta Tabelas .
1. Selecione todas as tabelas do banco de dados no painel de conteúdo, clique com o botão direito do mouse e selecione Executar Estatísticas.
1. Acesse Estatísticas > Estatísticas de índice.
1. Selecione Coletar Estatísticas para Todos os Índices, Colete Estatísticas para Índices com Estatísticas Detalhadas Estendidas e clique em OK.

Uma mensagem é exibida quando o processo é concluído. Feche a mensagem.
