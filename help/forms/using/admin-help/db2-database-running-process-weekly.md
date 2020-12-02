---
title: '"Banco de dados DB2: Execução de um processo semanal"'
seo-title: '"Banco de dados DB2: Execução de um processo semanal"'
description: Veja como você pode melhorar o desempenho do banco de dados de formulários AEM DB2.
seo-description: Veja como você pode melhorar o desempenho do banco de dados de formulários AEM DB2.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Banco de dados DB2: Execução de um processo semanal{#db-database-running-a-process-weekly}

Se o banco de dados dos formulários AEM DB2 começar a ser executado lentamente, a execução semanal do seguinte processo pode melhorar seu desempenho:

1. Centro de controle DB2 do start:

   (Windows) Selecione Start > Programas > IBM DB2 > Ferramentas Administrativas Gerais > Centro de Controle.

   (Linux e UNIX) Em um prompt de comando, digite o comando `db2jcc`.

1. Na árvore de objetos do Centro de controle do DB2, clique em Todos os bancos de dados.
1. Clique no banco de dados criado para AEM formulários e clique na pasta Tabelas.
1. Selecione todas as tabelas de banco de dados no painel de conteúdo, clique com o botão direito do mouse nelas e selecione Executar estatísticas.
1. Vá até Estatísticas > Estatísticas de índice.
1. Selecione Coletar estatísticas para todos os índices, selecione Coletar estatísticas para índices com estatísticas detalhadas estendidas e clique em OK.

Uma mensagem é exibida quando o processo é concluído. Feche a mensagem.
