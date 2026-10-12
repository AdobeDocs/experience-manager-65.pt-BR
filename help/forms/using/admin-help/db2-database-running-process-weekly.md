---
title: 'Banco de dados DB2&reg;: execução semanal de um processo'
description: Saiba como você pode melhorar o desempenho do seu banco de dados do AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
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
source-wordcount: '149'
ht-degree: 0%
---
# Banco de dados DB2®: execução semanal de um processo{#db-database-running-a-process-weekly}

Se o seu banco de dados AEM Forms DB2® começar a ser executado lentamente, a execução semanal do seguinte processo pode melhorar seu desempenho:

1. Iniciar o DB2® Control Center:

   (Windows) Selecione Iniciar > Programas > IBM® DB2® > Ferramentas administrativas gerais > Centro de controle.

   (Linux® e UNIX®) Em um prompt de comando, digite o comando `db2jcc`.

1. Na árvore de objetos do DB2® Control Center, clique em Todos os Bancos de Dados.
1. Clique no banco de dados criado para o AEM Forms e clique na pasta Tabelas.
1. Selecione todas as tabelas do banco de dados no painel de conteúdo, clique com o botão direito do mouse nelas e selecione Executar estatística.
1. Vá para Estatísticas > Estatísticas de índice.
1. Selecione Coletar Estatísticas para Todos os Índices, selecione Coletar Estatísticas para Índices com Estatísticas Detalhadas Estendidas e clique em OK.

Uma mensagem é exibida quando o processo é concluído. Feche a mensagem.
