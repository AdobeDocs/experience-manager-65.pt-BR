---
title: Segurança do Documento| Tratamento de dados de utilizadores
seo-title: Segurança do Documento| Tratamento de dados de utilizadores
description: 'null'
seo-description: 'null'
uuid: 1624a465-8b0c-4347-a53f-1118bfa6e18f
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 898268cb-4426-421f-8f63-d75bd85cb57f
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Segurança do Documento| Tratamento de dados de utilizadores {#document-security-handling-user-data}

A segurança do documento do AEM Forms permite que você crie, armazene e aplique configurações de segurança predefinidas a seus documentos. Ela garante que somente usuários autorizados possam usar os documentos. É possível proteger documentos usando políticas. Uma política é uma coleção de informações que inclui configurações de segurança e uma lista de usuários autorizados. Você pode aplicar uma política a um ou mais documentos e autorizar usuários adicionados ao gerenciamento de usuários JEE do AEM Forms.

<!-- Fix broken link For more information about how document security works, see AEM Forms JEE administration help. -->

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

A segurança do Documento armazena políticas e dados relacionados a documentos protegidos, incluindo dados do usuário em um banco de dados, como My Sql, Oracle, MS SQL Server e IBM DB2. Além disso, os dados para usuários autorizados em uma política armazenada no gerenciamento de usuários. Para obter informações sobre dados armazenados no gerenciamento de usuários, consulte Gerenciamento de usuários do [Forms: Manuseio de dados](/help/forms/using/user-management-handling-user-data.md)do usuário.

A tabela a seguir mapeia como a segurança do documento organiza os dados nas tabelas do banco de dados.

<table>
 <tbody>
  <tr>
   <td>Tabela de banco de dados</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><code>EdcPrincipalKeyEntity</code></td>
   <td>Armazena informações sobre chaves principais para os usuários. As chaves são usadas em workflows de segurança de documento offline.</td>
  </tr>
  <tr>
   <td><code>EdcAuditEntity</code></td>
   <td>Armazena informações sobre auditoria de eventos como eventos de usuários, eventos de documentos e eventos de políticas.</td>
  </tr>
  <tr>
   <td><p><code>EdcLicenseEntity</code></p> </td>
   <td>Armazena o registro de um documento protegido. Ele armazena detalhes de licença para cada documento protegido.</td>
  </tr>
  <tr>
   <td><p><code>EdcDocumentEntity</code></p> </td>
   <td>Armazena o nome do documento para cada licença criada no sistema.</td>
  </tr>
  <tr>
   <td><p><code>EdcRevokationEntity</code></p> </td>
   <td>Armazena informações sobre a revogação e a reinstalação de documentos protegidos.</td>
  </tr>
  <tr>
   <td><code>EdcMyPolicyListEntity</code></td>
   <td>Armazena informações sobre usuários que podem criar políticas pessoais exibidas na guia Minhas políticas da página Políticas. </td>
  </tr>
  <tr>
   <td><code>EdcPolicyEntity</code></td>
   <td>Armazena informações sobre políticas. Cada política corresponde a uma linha nesta tabela.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyXmlEntity</code></td>
   <td>Armazena arquivos XML para políticas ativas. Um XML<sup> de política </sup>contém referências a IDs principais de usuários associados à política. O XML de política é armazenado como um objeto Blob.</td>
  </tr>
  <tr>
   <td><code>EdcPolicyArchiveEntity</code></td>
   <td>Armazena informações sobre políticas arquivadas. Uma política arquivada contém a política XML armazenada como um objeto Blob.</td>
  </tr>
  <tr>
   <td><p><code>EdcPolicySetPrincipalEntity</code></p> <p><code>EdcPolicySetPrincipalEnt</code> (Bancos de dados Oracle e MS SQL)</p> </td>
   <td>Armazena o mapeamento entre o conjunto de políticas e os usuários.</td>
  </tr>
  <tr>
   <td><code>EdcInvitedUserEntity</code></td>
   <td>Armazena informações sobre o usuário convidado.</td>
  </tr>
 </tbody>
</table>

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar e exportar dados de segurança do documento para usuários nos bancos de dados e, se necessário, excluí-los permanentemente.

Para exportar ou excluir dados do usuário de um banco de dados, é necessário conectar-se ao banco de dados usando um cliente de banco de dados e descobrir a ID principal com base em algumas informações pessoalmente identificáveis do usuário. Por exemplo, para recuperar a ID principal de um usuário usando uma ID de logon, execute o seguinte `select` comando no banco de dados.

No `select` comando, substitua o `<user_login_id>` pela ID de logon do usuário cuja ID principal você deseja recuperar da tabela do `EdcPrincipalUserEntity` banco de dados.

```sql
select refprincipalid from EdcPrincipalUserEntity where uidstring = <user_login_id>
```

Quando você souber a ID principal, poderá exportar ou excluir os dados do usuário.

### Exportar dados do usuário {#export-user-data}

Execute os seguintes comandos de banco de dados para exportar dados do usuário para uma ID principal das tabelas de banco de dados. No `select` comando, substitua `<principal_id>` pela ID principal do usuário cujos dados você deseja exportar.

>[!NOTE]
>
>Os comandos a seguir usam nomes de tabela de banco de dados em bancos de dados My SQL e IBM DB2. Ao executar esses comandos em bancos de dados Oracle e MS SQL, substitua `EdcPolicySetPrincipalEntity` por `EdcPolicySetPrincipalEnt` nos comandos.

```sql
Select * from EdcPrincipalKeyEntity where principalid = '<principal_id>';

Select * from EdcLicenseEntity where publisherId = '<principal_id>';

Select * from EdcDocumentEntity where id in (Select documentid from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcRevokationEntity where licenseid in (Select id from EdcLicenseEntity where publisherId = '<principal_id>');

Select * from EdcMyPolicyListEntity where principalId = '<principal_id>';

Select * from edcpolicyentity where policyownerId = '<principal_id>';

Select * from edcpolicyxmlentity where policyidref in (Select id from edcpolicyentity where policyownerId = '<principal_id>');

Select * from edcpolicyarchiveentity where policyownerId = '<principal_id>';

Select * from edcpolicysetprincipalentity where principalId = '<principal_id>';

Select * from edcinviteduserentity where principalId = '<principal_id>';
```

>[!NOTE]
>
>Para exportar dados da `EdcAuditEntity` tabela, use a API [EventManager.exportEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que utiliza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parâmetro para exportar dados de auditoria com base em `principalId`, `policyId`ou `licenseId`.

Para obter dados completos sobre um usuário no sistema, você deve acessar e exportar dados do banco de dados de gerenciamento de usuários. Para obter mais informações, consulte Gerenciamento de usuários do [Forms: Manuseio de dados](/help/forms/using/user-management-handling-user-data.md)do usuário.

### Excluir dados do usuário {#delete-user-data}

Faça o seguinte para excluir dados de segurança do documento de uma ID principal das tabelas do banco de dados.

1. Desligue o servidor de formulários AEM.
1. Execute os seguintes comandos de banco de dados para excluir dados da ID principal das tabelas de banco de dados para segurança do documento. No `Delete` comando, substitua `<principal_id>` pela ID principal do usuário cujos dados você deseja excluir.

   ```sql
   Delete from EdcPrincipalKeyEntity where principalid = '<principal_id>';
   
   Delete from EdcMyPolicyListEntity where principalId = '<principal_id>';
   
   Delete from edcpolicyarchiveentity where policyownerId = '<principal_id>';
   
   Delete from edcpolicysetprincipalentity where principalId = '<principal_id>';
   
   Delete from edcinviteduserentity where principalId = '<principal_id>';
   ```

   >[!NOTE]
   >
   >Para excluir dados da `EdcAuditEntity` tabela, use a API [EventManager.deleteEvents](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/index.html?com/adobe/livecycle/rightsmanagement/client/EventManager.html) que utiliza [EventSearchFilter](https://helpx.adobe.com/experience-manager/6-5/forms/programlc/javadoc/com/adobe/livecycle/rightsmanagement/client/infomodel/EventSearchFilter.html) como parâmetro para excluir dados de auditoria com base em `principalId`, `policyId`ou `licenseId`.

1. Os arquivos XML de política ativos e arquivados são armazenados nas tabelas do banco de dados `EdcPolicyXmlEntity` e do banco de `EdcPolicyArchiveEntity` dados, respectivamente. Para excluir dados de um usuário dessas tabelas, faça o seguinte:

   1. Abra o blob XML de cada linha na tabela `EdcPolicyXMLEntity` ou `EdcPolicyArchiveEntity` e extraia o arquivo XML. O arquivo XML é semelhante ao mostrado abaixo.
   1. Edite o arquivo XML para remover o blob da ID principal.
   1. Repita as etapas 1 e 2 para o outro arquivo.
   >[!NOTE]
   >
   >Você deve remover o blob completo dentro da `Principal` tag para uma ID principal ou o XML da política pode ficar corrompido ou inutilizável.

   ```xml
   <ns2:Principal PrincipalNameType="USER">
       <ns2:PrincipalDomain>OID</ns2:PrincipalDomain>
       <ns2:PrincipalName>56F33FEB-098A-1036-A651-00000A2A2656</ns2:PrincipalName>
   </ns2:Principal>
   </ns2:PolicyEntry>
       <ns2:Property PropertyName="isCertified">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">false</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="encryptionAlgorithm">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string">AES128</ns2:PropertyValue>
       </ns2:Property>
       <ns2:Property PropertyName="AccessDeniedErrorMessage">
           <ns2:PropertyValue xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xmlns:xs="https://www.w3.org/2001/XMLSchema" xsi:type="xs:string"></ns2:PropertyValue>
       </ns2:Property>
   <ns2:PolicyEntry>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.onlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.copy" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.offlineOpen" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.accessible" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.editNotes" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.edit" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.fillAndSign" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printHigh" Access="ALLOW"/>
   <ns2:Permission PermissionName="ns3:com.adobe.aps.pdf.printLow" Access="ALLOW"/>
   ```

   Além de excluir dados diretamente da `EdcPolicyXmlEntity` tabela, há mais duas maneiras de conseguir isso:

   **Uso do console de administração**

   1. Como administrador, faça logon no console de administração do Forms JEE em https://[*server*]:[*port*]/adminui.
   1. Navegue até **[!UICONTROL Serviços > Segurança do Documento > Conjuntos]** de políticas.
   1. Abra um conjunto de políticas e exclua o usuário da política.
   **Usando a página da Web de segurança do documento**

   Os usuários de segurança do Documento que têm permissões para criar políticas pessoais podem excluir dados do usuário de suas políticas. Para isso:

   1. Os usuários que têm políticas pessoais fazem logon em sua página da Web de segurança do documento em https://[*server*]:[*port*]/edc.
   1. Navegue até **[!UICONTROL Serviços > Segurança do Documento > Minhas políticas]**.
   1. Abra uma política e exclua o usuário da política.
   >[!NOTE]
   >
   >Os administradores podem pesquisar, acessar e excluir dados do usuário de políticas pessoais de outros usuários em **[!UICONTROL Serviços > Segurança do Documento > Minhas políticas]** usando o console de administração.

1. Exclua os dados da ID principal do banco de dados de gerenciamento de usuários. Para obter etapas detalhadas, consulte Gerenciamento de usuários de [formulários| Tratamento de dados](/help/forms/using/user-management-handling-user-data.md)do utilizador.
1. Start do servidor do AEM Forms.

