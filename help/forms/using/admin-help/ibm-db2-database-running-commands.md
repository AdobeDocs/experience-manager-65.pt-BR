---
title: "Banco de dados IBM DB2: execução de comandos para manutenção regular"
description: Este documento lista os comandos do IBM DB2 recomendados para a manutenção regular do banco de dados de formulários AEM.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7a4281e7-1544-473a-a471-e9a4c2819a58
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Banco de dados IBM DB2: execução de comandos para manutenção regular {#ibm-db-database-running-commands-for-regular-maintenance}

Os seguintes comandos do IBM DB2 são recomendados para a manutenção regular do banco de dados de formulários AEM. Para obter informações detalhadas sobre manutenção e ajuste de desempenho para o banco de dados DB2, consulte o *Guia de Administração do IBM DB2*.

* **runstats:** este comando atualiza estatísticas que descrevem as características físicas de uma tabela de banco de dados, juntamente com seus índices associados. As instruções SQL dinâmicas geradas por formulários AEM usam automaticamente essas estatísticas atualizadas, mas as instruções SQL estáticas criadas dentro de um banco de dados também exigem que o comando `db2rbind` seja executado.
* **db2rbind:** este comando reassocia todos os pacotes do banco de dados. Use este comando após executar o utilitário `runstats` para revalidar todos os pacotes no banco de dados.
* **reorganizar tabela ou índice:** Este comando verifica se é necessária uma reorganização de algumas tabelas e índices.

  À medida que seus bancos de dados crescem e mudam, o recálculo das estatísticas da tabela é essencial para melhorar o desempenho do banco de dados e deve ser feito regularmente. Esses comandos podem ser executados manualmente usando scripts ou usando um trabalho cron.

>[!NOTE]
>
>Antes de executar o comando `runstats`, o banco de dados deve conter dados e pelo menos uma sincronização de diretório deve ter sido executada.

Para um banco de dados pequeno, como para 10.000 usuários ou 2.500 grupos, é suficiente invocar o comando `runstats` para reduzir os tempos de sincronização.

Para bancos de dados maiores, como para 100.000 usuários ou 10.000 grupos, execute o comando `reorg` antes de executar o comando `runstats`.

## Use o comando runstats no banco de dados de formulários AEM {#use-the-runstats-command-on-your-aem-forms-database}

Execute o comando `runstats` nas tabelas e índices do banco de dados de formulários AEM a seguir.

>[!NOTE]
>
>O comando `runstats` precisa ser executado somente durante a primeira sincronização de banco de dados. No entanto, ele deve ser executado duas vezes durante esse processo: uma vez durante a sincronização de Usuários e Grupos e, em seguida, durante a sincronização de Membros do Grupo. Certifique-se de que o script seja executado completamente sempre que você executá-lo.

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

Execute o comando `reorg` nas tabelas e índices do banco de dados de formulários AEM a seguir. Para obter a sintaxe e o uso corretos, consulte a documentação do fabricante do banco de dados.

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
