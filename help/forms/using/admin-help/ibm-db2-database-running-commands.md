---
title: "Banco de dados IBM DB2: execução de comandos para manutenção regular"
seo-title: "IBM DB2 database: Running commands for regular maintenance"
description: Este documento lista os comandos do IBM DB2 recomendados para a manutenção regular do banco de dados de formulários AEM.
seo-description: This document lists IBM DB2 commands that are recommended for regular maintenance of your AEM forms database.
uuid: 235d59df-b9b9-4770-8b7d-00713701c3c2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a62b68b4-7735-49b1-8938-f0d9e4c4a051
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---

# Banco de dados IBM DB2: execução de comandos para manutenção regular {#ibm-db-database-running-commands-for-regular-maintenance}

Os seguintes comandos do IBM DB2 são recomendados para a manutenção regular do banco de dados de formulários AEM. Para obter informações detalhadas sobre manutenção e ajuste de desempenho para seu banco de dados DB2, consulte *Guia de administração do IBM DB2*.

* **runstats:** Esse comando atualiza estatísticas que descrevem as características físicas de uma tabela de banco de dados, juntamente com seus índices associados. As instruções SQL dinâmicas geradas por formulários AEM usam automaticamente essas estatísticas atualizadas, mas as instruções SQL estáticas criadas em um banco de dados exigem que o `db2rbind` comando também pode ser executado.
* **db2rbind:** Este comando vincula novamente todos os pacotes no banco de dados. Use este comando após executar o `runstats` para revalidar todos os pacotes no banco de dados.
* **reorganizar tabela ou índice:** Este comando verifica se é necessária uma reorganização de algumas tabelas e índices.

   À medida que seus bancos de dados crescem e mudam, o recálculo das estatísticas da tabela é essencial para melhorar o desempenho do banco de dados e deve ser feito regularmente. Esses comandos podem ser executados manualmente usando scripts ou usando um trabalho cron.

>[!NOTE]
>
>Antes de executar o `runstats` , o banco de dados deverá conter dados e pelo menos uma sincronização de diretório deverá ter sido executada.

Para um banco de dados pequeno, como para 10.000 usuários ou 2.500 grupos, basta chamar a variável `runstats` comando para reduzir os tempos de sincronização.

Para bancos de dados maiores, como para 100.000 usuários ou 10.000 grupos, execute o `reorg` antes de executar o `runstats` comando.

## Use o comando runstats no banco de dados de formulários AEM {#use-the-runstats-command-on-your-aem-forms-database}

Execute o `runstats` comando nos seguintes índices e tabelas de banco de dados de formulários AEM.

>[!NOTE]
>
>A variável `runstats` precisa ser executado somente durante a primeira sincronização do banco de dados. No entanto, ele deve ser executado duas vezes durante esse processo: uma vez durante a sincronização de Usuários e Grupos e, em seguida, durante a sincronização de Membros do Grupo. Certifique-se de que o script seja executado completamente sempre que você executá-lo.

Para obter a sintaxe e o uso corretos, consulte a documentação do fabricante do banco de dados. Abaixo, `<schema>` é usado para denotar o esquema associado ao seu nome de usuário DB2. Se você tiver uma instalação padrão simples do DB2, este é o nome do esquema do banco de dados.

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

## Execute o comando reorg no banco de dados de formulários AEM {#run-the-reorg-command-on-your-aem-forms-database}

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
