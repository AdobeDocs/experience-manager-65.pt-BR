---
title: Gerenciamento de correspondência | Tratamento de dados de utilizadores
seo-title: Gerenciamento de correspondência | Tratamento de dados de utilizadores
description: Gerenciamento de correspondência | Tratamento de dados de utilizadores
uuid: d5bb190b-d668-4da3-95da-b7705ad302d9
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 764d8e0d-604d-4c7b-89cd-7686ce5f03ff
role: Admin
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Gerenciamento de correspondência | Tratamento de dados de utilizadores {#correspondence-management-handling-user-data}

O AEM Forms Correspondence Management permite criar, gerenciar e simplificar correspondências seguras e personalizadas do cliente. Ela oferece uma interface de usuário intuitiva para usuários empresariais criarem correspondências usando blocos de conteúdo e elementos de mídia pré-aprovados. Para obter mais informações sobre como criar correspondências, consulte [Criar correspondência](/help/forms/using/create-correspondence.md).

Quando um usuário empresarial ou um agente salva uma correspondência como rascunho ou a envia, uma instância da carta é salva no repositório de AEM. A instância da carta inclui dados e metadados da correspondência.

>[!NOTE]
>
>No AEM 6.5 Forms, o gerenciamento de correspondência não está disponível imediatamente. Se estiver atualizando de uma versão anterior do AEM Forms, instale o pacote de compatibilidade e migre seus ativos de gerenciamento de correspondência para continuar a usá-los no AEM 6.5 Forms. Para obter mais informações, consulte [Pacote de compatibilidade](/help/forms/using/compatibility-package.md).

## Armazenamento de dados e dados do usuário {#data}

O gerenciamento de correspondência armazena dados para rascunho e cartas enviadas em AEM repositório somente se a instância de publicação estiver configurada para gerenciar instâncias de carta. Para obter mais informações sobre a configuração, consulte [Propriedades de configuração do Correspondence Management](/help/forms/using/cm-configuration-properties.md).

Dependendo da persistência do armazenamento de dados configurada para a implantação do AEM, os rascunhos e os dados de correspondência enviados são armazenados nos seguintes locais.

<table>
 <tbody>
  <tr>
   <td><p><strong>Tipo de persistência</strong></p> </td>
   <td><p><strong>Armazenamento de dados</strong></p> </td>
   <td><p><strong>Local</strong></p> </td>
  </tr>
  <tr>
   <td><p>Padrão</p> </td>
   <td><p>AEM repositório de instâncias de publicação e de autor especificadas na configuração de replicação inversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Repositório AEM da instância do autor de processamento remoto</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

No local do repositório AEM acima especificado:

* `[yyyy]/[mm]/[dd]` é a estrutura do nó com base na data em que a instância da carta foi criada
* `[node-id]` é o ID atribuído à pasta que contém a carta
* `[letter-instance-name]` é o nome especificado ao salvar ou enviar uma carta

No nó [letter-instance-name], a seguinte estrutura de nó é criada e os dados para cada instância de carta são armazenados no repositório AEM:

| Nó | Descrição |
|---|---|
| `extendedProperties` | Armazena as propriedades de metadados da instância de carta. |
| `dataXML` | Armazena um arquivo dataXML baixável que contém os dados de correspondência em formato binário. |
| `processedXDP` | Inclui os detalhes do template XDP usado para criar a carta enviada. Esse nó é criado somente para correspondências enviadas. |
| `submittedLetter` | Armazena os dados da carta enviados em formato binário que pode ser baixado. Esse nó é criado somente para correspondências enviadas. |

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar dados de rascunho e enviar a correspondência nos armazenamentos de dados configurados e, se necessário, excluí-los.

### Acessar dados do usuário {#access-user-data}

O gerenciamento de correspondência fornece APIs que podem ser usadas para localizar e acessar instâncias de rascunho e de carta enviada. Usando as APIs, é possível encontrar e abrir instâncias de carta usando a ID da instância de carta ou o usuário que salvou ou enviou a correspondência. Para obter mais informações, consulte [APIs para acessar instâncias de carta](/help/forms/using/cm-apis-to-access-letter-instances.md).

Como alternativa, você pode navegar até a instância da carta AEM repositório usando o CRX DELite. Consulte [Dados do usuário e armazenamentos de dados](/help/forms/using/correspondence-management-handling-user-data.md#data) para obter informações sobre os dados armazenados e o local do repositório.

### Excluir dados do usuário {#delete-user-data}

Para localizar uma instância de carta contendo os dados de um usuário específico, é possível:

* Use as APIs de gerenciamento de correspondência se o nome da instância da carta ou o usuário que salvou o rascunho ou enviou a correspondência for conhecido
* Use AEM pesquisa do repositório usando informações pessoalmente identificáveis, como a ID do email ou o nome para encontrar o nó onde as informações são armazenadas

Para excluir os dados do usuário do rascunho e as correspondências enviadas completamente dos sistemas de AEM, é necessário excluir manualmente o nó da instância de carta de todas as instâncias AEM aplicáveis.
