---
title: '"Banco de dados IBM DB2: Executar comandos para manutenção regular"'
seo-title: '"Banco de dados IBM DB2: Executar comandos para manutenção regular"'
description: Este documento lista comandos IBM DB2 recomendados para manutenção regular do banco de dados de formulários do AEM.
seo-description: Este documento lista comandos IBM DB2 recomendados para manutenção regular do banco de dados de formulários do AEM.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---


# Banco de dados IBM DB2: Execução de comandos para manutenção regular {#ibm-db-database-running-commands-for-regular-maintenance}

Os seguintes comandos do IBM DB2 são recomendados para a manutenção regular do banco de dados de formulários do AEM. Para obter informações detalhadas sobre manutenção e ajuste de desempenho para seu banco de dados DB2, consulte *IBM DB2 Administration Guide*.

* **runstats:** Esse comando atualiza estatísticas que descrevem as características físicas de uma tabela de banco de dados, juntamente com seus índices associados. Instruções SQL dinâmicas geradas por formulários AEM usam automaticamente essas estatísticas atualizadas, mas instruções SQL estáticas criadas dentro de um banco de dados exigem que o `db2rbind` comando também seja executado.
* **db2rbind:** Esse comando reassocia todos os pacotes no banco de dados. Use esse comando depois de executar o `runstats` utilitário para revalidar todos os pacotes no banco de dados.
* **tabela de reorganização ou índice:** Este comando verifica se é necessária uma reorganização de algumas tabelas e índices.

   À medida que seus bancos de dados crescem e mudam, recalcular as estatísticas da tabela é essencial para melhorar o desempenho do banco de dados e deve ser feito regularmente. Esses comandos podem ser executados manualmente usando scripts ou usando um trabalho cron.

>[!NOTE]
>
>Antes de executar o `runstats` comando, o banco de dados deve conter dados e pelo menos uma sincronização de diretório deve ter sido executada.

Para um banco de dados pequeno, como 10.000 usuários ou 2.500 grupos, basta chamar o `runstats` comando para reduzir os tempos de sincronização.

Para bancos de dados maiores, como 100.000 usuários ou 10.000 grupos, execute o `reorg` comando antes de executar o `runstats` comando.

## Usar o comando runstats no banco de dados de formulários do AEM {#use-the-runstats-command-on-your-aem-forms-database}

Execute o `runstats` comando nos seguintes índices e tabelas de banco de dados de formulários AEM.

>[!NOTE]
>
>O `runstats` comando precisa ser executado somente durante a primeira sincronização do banco de dados. No entanto, ele deve ser executado duas vezes durante esse processo: uma vez durante a sincronização de Usuários e Grupos e, em seguida, durante a sincronização de Membros do Grupo. Certifique-se de que o script seja executado completamente sempre que você o executar.

Para obter a sintaxe e o uso corretos, consulte a documentação do fabricante do banco de dados. Abaixo, `<schema>` é usado para indicar o schema associado ao nome de usuário do DB2. Se você tiver uma instalação padrão simples do DB2, este é o nome do schema do banco de dados.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGROUPENTITY FOR INDEXES ALL
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY FOR INDEXES ALL
```

## Execute o comando reorg no banco de dados de formulários do AEM {#run-the-reorg-command-on-your-aem-forms-database}

Execute o `reorg` comando nos seguintes índices e tabelas de banco de dados de formulários AEM. Para obter a sintaxe e o uso corretos, consulte a documentação do fabricante do banco de dados.

```sql
     TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
 
     TABLE <schema>.EDCPRINCIPALENTITY
 
     TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALEMAILALIASENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALUSERENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGROUPENTITY
 
     INDEXES ALL FOR TABLE <schema>.EDCPRINCIPALGRPCTMNTENTITY
```

