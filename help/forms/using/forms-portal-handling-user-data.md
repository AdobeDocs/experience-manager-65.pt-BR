---
title: Portal da Forms | Tratamento de dados de utilizadores
seo-title: Portal da Forms | Tratamento de dados de utilizadores
description: 'null'
seo-description: 'null'
uuid: 2ac2b2a9-b603-489a-86b8-a78b697f130d
contentOwner: vishgupt
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 48f841b7-0e7f-4216-9ee8-fb6e843acaf0
translation-type: tm+mt
source-git-commit: 4e0709031aca030e50840811a9b3717f3cb20340
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# Portal da Forms | Tratamento de dados de utilizadores {#forms-portal-handling-user-data}

[!DNL AEM Forms] O portal fornece componentes que você pode usar para lista de formulários adaptáveis, formulários HTML5 e outros ativos do Forms na [!DNL AEM Sites] página. Além disso, é possível configurá-lo para exibir rascunhos e formulários adaptativos enviados e formulários HTML5 para um usuário conectado. Para obter mais informações sobre o portal de formulários, consulte [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md).

Quando um usuário conectado salva um formulário adaptável como rascunho ou o envia, ele é exibido nas guias Rascunhos e Envios no portal de formulários. Os dados para rascunhos ou formulários enviados são armazenados no armazenamento de dados configurado para implantação AEM. Os rascunhos e envios de usuários anônimos não são exibidos na página do portal de formulários; no entanto, os dados são armazenados no armazenamento de dados configurado. Para obter mais informações, consulte [Configuração de serviços de armazenamento para rascunhos e envios](/help/forms/using/configuring-draft-submission-storage.md).

## Armazenamento de dados e dados do usuário {#user-data-and-data-stores}

O portal da Forms armazena dados para formulários rascunhos e enviados nos seguintes cenários:

* A ação de envio configurada no formulário adaptável é a Ação **de envio do** Forms Portal.
* Para ações de envio diferentes da Ação **de envio do** Forms Portal, a opção **[!UICONTROL Armazenar dados no portal]** de formulários está ativada nas propriedades de **[!UICONTROL envio]** do container de formulário adaptável.

Para cada rascunho e formulário enviado para usuários conectados e anônimos, o portal de formulários armazena os seguintes dados:

* Metadados de formulário, como nome do formulário, caminho do formulário, ID de rascunho ou envio, caminho de anexos e ID de dados do usuário
* Anexo de formulário como bytes de dados
* Dados do formulário como bytes de dados

Dependendo da persistência do armazenamento de dados configurado, os rascunhos e os dados de formulários enviados são armazenados nos seguintes locais.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistência</strong></p> </td>
   <td><p><strong>Armazenamento de dados</strong></p> </td>
   <td><p><strong>Local</strong></p> </td>
  </tr>
  <tr>
   <td><p>Padrão</p> </td>
   <td><p>AEM repositório de instâncias de autor e publicação</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>AEM repositório de instâncias de autor e AEM remota</p> </td>
   <td><p><code>/content/forms/fp/</code></p> </td>
  </tr>
  <tr>
   <td><p>Banco de dados</p> </td>
   <td><p>AEM repositório de instâncias do autor e tabelas de banco de dados</p> </td>
   <td>Tabelas de banco de dados <code>data</code>, <code>metadata</code>e <code>additionalmetadata</code></td>
  </tr>
 </tbody>
</table>

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar dados de rascunho e formulários enviados para usuários conectados e anônimos nos armazenamentos de dados configurados e, se necessário, excluí-los.

### AEM instâncias {#aem-instances}

Todos os rascunhos e dados de formulários enviados em instâncias AEM (autor, publicação ou remoto) para usuários conectados e anônimos são armazenados no `/content/forms/fp/` nó do repositório AEM aplicável. Toda vez que um usuário conectado ou anônimo salva um rascunho ou envia um formulário, um `draft ID` ou `submission ID`, um `user data ID`e um aleatório `ID` para cada anexo (se aplicável) é gerado, que é associado ao respectivo rascunho ou envio.

#### Acessar dados do usuário {#access-user-data}

Quando um usuário conectado salva um rascunho ou envia um formulário, um nó filho é criado com sua ID de usuário. Por exemplo, rascunhos e envios de dados para Sarah Rose cuja ID de usuário é `srose` armazenada no `/content/forms/fp/srose/` nó AEM repositório. No nó da ID do usuário, os dados são organizados em uma estrutura hierárquica.

A tabela a seguir explica como os dados de todos os rascunhos por `srose` são armazenados AEM repositório.

>[!NOTE]
>
>Uma estrutura exata como `drafts` é replicada para formulários enviados para `srose` `/content/forms/fp/srose/submit/` o nó.
>
>Todos os rascunhos e envios por `anonymous` usuários são armazenados sob o `/content/forms/fp/anonymous/` nó, que organiza rascunhos e envios para todos os usuários anônimos sob os nós `draft` e `submit` .

| Nó | Descrição |
|---|---|
| `/content/forms/fp/srose/drafts` | Dados do nó do container para todos os rascunhos pelo usuário |
| `/content/forms/fp/srose/drafts/attachments/` | Organiza todos os anexos para o usuário com base na ID de rascunho |
| `/content/forms/fp/srose/drafts/attachments/<ID>` | Contém anexo para a ID selecionada no formato binário |
| `/content/forms/fp/srose/drafts/metadata/` | Organiza metadados de formulário para o usuário com base na ID de rascunho |
| `/content/forms/fp/srose/drafts/metadata/<draft ID>` | Contém metadados de formulário para a ID de rascunho selecionada |
| `/content/forms/fp/srose/drafts/data/` | Organiza dados de formulários para o usuário com base na ID de dados do usuário |
| `/content/forms/fp/srose/drafts/data/<user data ID>` | Contém dados de formulário para a ID de dados de usuário selecionada no formato binário |

#### Excluir dados do usuário {#delete-user-data}

Para excluir completamente os dados do usuário dos rascunhos e envios de um usuário conectado AEM sistemas, você deve excluir o `user ID` nó de um usuário específico do nó do autor. Você deve excluir dados manualmente de todas as instâncias AEM aplicáveis.

Os rascunhos e os dados de envio para todos os usuários anônimos são armazenados dentro dos nós comuns `drafts` e `submit` em `/content/forms/fp/anonymous`. Não há método para localizar dados para um usuário anônimo específico, a menos que algumas informações identificáveis sejam conhecidas. Nesse caso, você pode pesquisar as informações que identificam o usuário anônimo AEM repositório e excluir manualmente o nó que o contém de todas as instâncias AEM aplicáveis para remover dados do sistema AEM. No entanto, para excluir dados de todos os usuários anônimos, você pode excluir o `anonymous` nó para remover rascunhos e dados de envios de todos os usuários anônimos.

### Banco de dados {#database}

Quando AEM está configurado para armazenar dados em um banco de dados, os dados de envio e rascunho do portal de formulários são armazenados nas seguintes tabelas de banco de dados para usuários conectados e anônimos:

* data
* metadata
* metadata adicionais

#### Acessar dados do usuário {#access-user-data-1}

Para acessar dados de rascunhos e envios de usuários conectados e anônimos nas tabelas do banco de dados, execute o seguinte comando do banco de dados. No query, substitua `logged-in user` pela ID de usuário cujos dados você deseja acessar ou com `anonymous` os usuários anônimos.

```sql
select * from metadata, data, additionalmetadatatable where metadata.owner = 'logged-in user' and metadata.id = additionalmetadatatable.id and metadata.userdataID = data.id
```

#### Excluir dados do usuário {#delete-user-data-1}

Para excluir os dados de rascunhos e envios de um usuário conectado das tabelas do banco de dados, execute o seguinte comando do banco de dados. No query, substitua `logged-in user` pela ID de usuário cujos dados você deseja excluir ou pelos dados `anonymous` de usuários anônimos. Observe que para excluir dados de um usuário anônimo específico do banco de dados, é necessário encontrá-los usando algumas informações identificáveis e excluí-los das tabelas de banco de dados que contêm as informações.

```sql
DELETE FROM metadata, data, additionalmetadatatable USING metadata INNER JOIN data ON metadata.userdataID = data.id INNER JOIN additionalmetadatatable ON metadata.id = additionalmetadatatable.id WHERE metadata.owner = 'logged-in user'
```

