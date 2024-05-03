---
title: Gerenciamento de correspondência | Manuseio de dados do usuário
description: Saiba mais sobre o Gerenciamento de correspondência e como lidar com dados do usuário em um ambiente do Adobe Experience Manager Forms.
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Admin,User
exl-id: a0c6a02c-47a3-4e70-a14c-953ee016b8e4
solution: Experience Manager, Experience Manager Forms
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# Gerenciamento de correspondência | Manuseio de dados do usuário {#correspondence-management-handling-user-data}

O Gerenciamento de correspondência da AEM Forms permite criar, gerenciar e simplificar correspondências seguras e personalizadas de clientes. Ele fornece uma interface intuitiva para usuários empresariais que permite criar correspondências usando blocos de conteúdo e elementos de mídia pré-aprovados. Para obter mais informações sobre como criar correspondências, consulte [Criar correspondência](/help/forms/using/create-correspondence.md).

Quando um usuário empresarial ou agente salva uma correspondência como rascunho ou a envia, uma ocorrência de carta é salva no repositório AEM. A ocorrência de carta inclui dados de correspondência e metadados.

>[!NOTE]
>
>No AEM 6.5 Forms, o gerenciamento de correspondência não está disponível imediatamente. Se estiver atualizando de uma versão anterior do AEM Forms, instale o pacote de compatibilidade e migre seus ativos de gerenciamento de correspondência para continuar a usá-los no AEM 6.5 Forms. Para obter mais informações, consulte [Pacote de compatibilidade](/help/forms/using/compatibility-package.md).

## Dados do usuário e armazenamentos de dados {#data}

O gerenciamento de correspondência armazena dados de rascunho e cartas enviadas no repositório AEM somente se a instância de publicação estiver configurada para gerenciar instâncias de cartas. Para obter mais informações sobre a configuração, consulte [Propriedades de configuração do Gerenciamento de correspondência](/help/forms/using/cm-configuration-properties.md).

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
   <td><p>Repositório AEM da instância de publicação e instâncias do autor especificadas na configuração de replicação reversa</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code><br /> </p> </td>
  </tr>
  <tr>
   <td><p>Remoto</p> </td>
   <td><p>Repositório AEM da instância do autor de processamento remoto</p> </td>
   <td><p><code>/content/apps/cm/letterInstances/[yyyy]/[mm]/[dd]/[node-id]/[letter-instance-name]/</code></p> </td>
  </tr>
 </tbody>
</table>

No local especificado acima para o repositório AEM:

* `[yyyy]/[mm]/[dd]` é a estrutura do nó com base na data em que a ocorrência de carta foi criada
* `[node-id]` é a ID atribuída à pasta que contém a letra
* `[letter-instance-name]` é o nome especificado ao salvar ou enviar uma carta

No [letter-instance-name] , a seguinte estrutura de nó é criada e os dados de cada ocorrência de carta são armazenados no repositório AEM:

| Nó | Descrição |
|---|---|
| `extendedProperties` | Armazena propriedades de metadados da instância de carta. |
| `dataXML` | Armazena um arquivo dataXML que pode ser baixado, contendo os dados de correspondência em formato binário. |
| `processedXDP` | Inclui os detalhes do modelo XDP usado para criar a carta enviada. Este nó é criado somente para correspondências enviadas. |
| `submittedLetter` | Armazena os dados da carta enviada em formato binário baixável. Este nó é criado somente para correspondências enviadas. |

## Acessar e excluir dados do usuário {#access-and-delete-user-data}

Você pode acessar dados de correspondência de rascunho e enviados nos armazenamentos de dados configurados e, se necessário, excluí-los.

### Acessar dados do usuário {#access-user-data}

O Gerenciamento de correspondência fornece APIs que podem ser usadas para localizar e acessar instâncias de rascunho e de carta enviada. Usando as APIs, você pode localizar e abrir instâncias de cartas usando a ID de instância de cartas ou o usuário que salvou ou enviou a correspondência. Para obter mais informações, consulte [APIs para acessar instâncias de cartas](/help/forms/using/cm-apis-to-access-letter-instances.md).

Como alternativa, você pode navegar até a ocorrência de correspondência no repositório AEM usando CRXDE Lite. Consulte [Dados do usuário e armazenamentos de dados](/help/forms/using/correspondence-management-handling-user-data.md#data) para obter informações sobre os dados armazenados e o local do repositório.

### Excluir dados do usuário {#delete-user-data}

Para localizar uma ocorrência de carta contendo os dados de um usuário específico, é possível:

* Usar APIs do gerenciamento de correspondência se o nome da instância da carta ou o usuário que salvou o rascunho ou enviou a correspondência for conhecido
* Use a pesquisa do repositório AEM usando informações de identificação pessoal, como a ID de email ou o nome, para localizar o nó onde as informações são armazenadas

Para excluir os dados do usuário do rascunho e das correspondências enviadas completamente dos sistemas AEM, você deve excluir manualmente o nó da instância de correspondência de todas as instâncias AEM aplicáveis.
