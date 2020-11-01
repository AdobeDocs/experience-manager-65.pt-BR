---
title: Gerenciamento de usuários da Forms | Tratamento de dados de utilizadores
seo-title: Gerenciamento de usuários da Forms | Tratamento de dados de utilizadores
description: Gerenciamento de usuários da Forms | Tratamento de dados de utilizadores
uuid: 2b76b69f-6f3a-4f1a-a2a4-d39f5e529f75
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a88fc933-f1af-4798-b72f-10e7b0d2fd11
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 0%

---


# Gerenciamento de usuários da Forms | Tratamento de dados de utilizadores {#forms-user-management-handling-user-data}

O gerenciamento de usuários é um componente AEM Forms JEE que permite criar, gerenciar e autorizar usuários do AEM Forms a acessar o AEM Forms. O gerenciamento de usuários usa domínios como diretório para obter informações do usuário. Os seguintes tipos de domínio são suportados:

**Domínios** locais: Esse tipo de domínio não está conectado a um sistema de armazenamento de terceiros. Em vez disso, os usuários e grupos são criados localmente e residem no banco de dados Gerenciamento de usuários. As senhas são armazenadas localmente e a autenticação é feita usando um banco de dados local.

**Domínios** híbridos: Esse tipo de domínio não está conectado a um sistema de armazenamento de terceiros. Em vez disso, os usuários e grupos são criados localmente e residem no banco de dados Gerenciamento de usuários. Diferentemente dos domínios locais, os domínios híbridos usam um provedor de autenticação externo, que pode ser LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.

**Domínios** corporativos: Consiste de usuários e grupos que residem em um sistema de armazenamentos de terceiros, como um diretório LDAP. O Gerenciamento de usuários não grava no sistema de armazenamentos de terceiros. Em vez disso, o Gerenciamento de usuários sincroniza as informações do usuário e do grupo com o banco de dados Gerenciamento de usuários. Os domínios corporativos também usam um provedor de autenticação externo, que pode ser LDAP, Kerberos, SAML ou um provedor de autenticação personalizado.

<!-- Fix broken links For more information about how user management works and configured, see AEM Forms JEE administration help. -->

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

O gerenciamento de usuários armazena dados de usuários em um banco de dados, como My Sql, Oracle, MS SQL Server e IBM DB2. Além disso, qualquer usuário que tenha feito logon pelo menos uma vez em aplicativos Forms AEM autor em, `https://'[server]:[port]'lc`o usuário será criado AEM repositório. Portanto, o gerenciamento de usuários é armazenado nos seguintes armazenamentos de dados:

* Banco de dados
* repositório AEM
* Armazenamento de terceiros como diretório LDAP

>[!NOTE]
>
>Os dados armazenados em armazenamentos de terceiros estão fora do escopo desse documento. Entre em contato diretamente com o fornecedor de terceiros para gerenciar os dados do usuário nesses armazenamentos.

### Banco de dados {#database}

O gerenciamento de usuários armazena dados do usuário nas seguintes tabelas de banco de dados:

<table>
 <tbody>
  <tr>
   <td>Tabela de banco de dados</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalEntity</code></td>
   <td><p>Armazena informações sobre entidades principais. Um principal pode ser um usuário, um grupo ou uma função.</p> <p> </p> </td>
  </tr>
  <tr>
   <td><code>EdcPrincipalUserEntity</code></td>
   <td>Armazena informações de identificação pessoal (PII) dos usuários. Ele contém uma entrada para cada usuário de domínios local, corporativo e híbrido.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalLocalAccountEntity</code></p> <p><code class="code">EdcPrincipalLocalAccount
       </code>(Bancos de dados Oracle e MS SQL)</p> </td>
   <td>Armazena dados somente para usuários locais.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalEmailAliasEntity</code></p> <p><code class="code">EdcPrincipalEmailAliasEn
       </code>(Bancos de dados Oracle e MS SQL)</p> </td>
   <td>Contém entradas de todos os usuários de domínios local, corporativo e híbrido. Ele contém IDs de email de usuário.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalGrpCtmntEntity</code></p> <p><code>EdcPrincipalGrpCtmntEnti</code> (Bancos de dados Oracle e MS SQL)</p> </td>
   <td>Armazena o mapeamento entre usuários e grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalRoleEntity</code></td>
   <td>Armazena o mapeamento entre funções e principal para usuários e grupos.</td>
  </tr>
  <tr>
   <td><code>EdcPriResPrmEntity</code></td>
   <td>Armazena o mapeamento entre principal e permissões para usuários e grupos.</td>
  </tr>
  <tr>
   <td><p><code>EdcPrincipalMappingEntity</code></p> <p><code>EdcPrincipalMappingEntit</code> (Bancos de dados Oracle e MS SQL)</p> </td>
   <td>Armazena valores de atributo antigos e novos correspondentes a um principal.<br /> </td>
  </tr>
 </tbody>
</table>

### repositório AEM {#aem-repository}

Os dados de gerenciamento de usuários para usuários que acessaram pelo menos uma vez os aplicativos Forms em `https://'[server]:[port]'lc` são armazenados AEM repositório também.

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar e exportar dados de gerenciamento de usuários para usuários nos bancos de dados de gerenciamento de usuários e AEM repositório e, se necessário, excluí-los permanentemente.

### Banco de dados {#database-1}

Para exportar ou excluir dados do usuário do banco de dados de gerenciamento de usuários, é necessário conectar-se ao banco de dados usando um cliente de banco de dados e descobrir a ID principal com base em alguma PII do usuário. Por exemplo, para recuperar a ID principal de um usuário usando uma ID de logon, execute o seguinte `select` comando no banco de dados.

No `select` comando, substitua o `<user_login_id>` pela ID de login do usuário cuja ID principal você deseja recuperar.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Quando você souber a ID principal, poderá exportar ou excluir os dados do usuário.

#### Exportar dados do usuário {#export-user-data}

Execute os seguintes comandos de banco de dados para exportar dados de gerenciamento de usuários para uma ID principal das tabelas de banco de dados. No `select` comando, substitua `<principal_id>` pela ID principal do usuário cujos dados você deseja exportar.

>[!NOTE]
>
>Os comandos a seguir usam nomes de tabela de banco de dados em bancos de dados My SQL e IBM DB2. Ao executar esses comandos em bancos de dados Oracle e MS SQL, substitua os seguintes nomes de tabela nos comandos:
>
>* Replace `EdcPrincipalLocalAccountEntity` with `EdcPrincipalLocalAccount`
   >
   >
* Replace `EdcPrincipalEmailAliasEntity` with `EdcPrincipalEmailAliasEn`
   >
   >
* Replace `EdcPrincipalMappingEntity` with `EdcPrincipalMappingEntit`
   >
   >
* Replace `EdcPrincipalGrpCtmntEntity` with `EdcPrincipalGrpCtmntEnti`

>



```sql
Select * from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (Select id from EDCPRINCIPALENTITY where id='<principal_id>'));

Select * from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');

Select * from EdcPrincipalEntity where id='<principal_id>';
```

#### Excluir dados do usuário {#delete-user-data}

Faça o seguinte para excluir dados de gerenciamento de usuários de uma ID principal das tabelas do banco de dados.

1. Exclua os dados do usuário AEM repositório, se aplicável, conforme descrito em [Excluir dados](/help/forms/using/user-management-handling-user-data.md#delete-aem)do usuário.
1. Desligue o servidor AEM Forms.
1. Execute os seguintes comandos de banco de dados para excluir dados de gerenciamento de usuários de uma ID principal das tabelas de banco de dados. No `Delete` comando, substitua `<principal_id>` pela ID principal do usuário cujos dados você deseja excluir.

   ```sql
   Delete from EdcPrincipalLocalAccountEntity where refuserprincipalid in (Select id from EdcPrincipalUserEntity where refprincipalid in (select id from EdcPrincipalEntity where id='<principal_id>'));
   
   Delete from EdcPrincipalEmailAliasEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalRoleEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPriResPrmEntity where refprinid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalUserEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalMappingEntity where refprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalGrpCtmntEntity where refchildprincipalid in (Select id from EdcPrincipalEntity where id='<principal_id>');
   
   Delete from EdcPrincipalEntity where id='<principal_id>';
   ```

1. Start o servidor AEM Forms.

### repositório AEM {#aem-repository-1}

Os usuários do Forms JEE têm seus dados AEM repositório se acessaram a instância do autor do AEM Forms pelo menos uma. Você pode acessar e excluir os dados do usuário AEM repositório.

#### Acessar dados do usuário {#access-user-data}

Para visualização do usuário criado no repositório AEM, faça logon `https://'[server]:[port]'/lc/useradmin` com AEM credenciais de administrador. Observe que `server` e `port` no URL estão os da instância do autor AEM. Aqui, você pode procurar usuários com seu nome de usuário. Clique em um duplo para visualização com informações como propriedades, permissões e grupos para o usuário. A `Path` propriedade de um usuário especifica o caminho para o nó do usuário criado AEM repositório.

#### Excluir dados do usuário {#delete-aem}

Para excluir um usuário:

1. Vá para `https://'[server]:[port]'/lc/useradmin` com AEM credenciais de administrador.
1. Procure um usuário e clique no duplo e clique no nome de usuário para abrir as propriedades do usuário. Copie a `Path` propriedade.
1. Vá para AEM CRX DELite em `https://'[server]:[port]'/lc/crx/de/index.jsp` e navegue ou pesquise o caminho do usuário.
1. Exclua o caminho e clique em **[!UICONTROL Salvar tudo]** para excluir permanentemente o usuário AEM repositório.

