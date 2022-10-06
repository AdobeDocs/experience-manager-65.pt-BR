---
title: Configuração de serviços de armazenamento para rascunhos e envios
seo-title: Configuring storage services for drafts and submissions
description: Saiba como configurar o armazenamento para rascunhos e envios
seo-description: Learn how to configure storage for drafts and submissions
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
exl-id: 51ca2844-91f0-453a-9b39-b876399ebecb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Configuração de serviços de armazenamento para rascunhos e envios {#configuring-storage-services-for-drafts-and-submissions}

## Visão geral {#overview}

Com o AEM Forms, você pode armazenar:

* **Rascunhos**: Um formulário de trabalho em andamento que os usuários finais preenchem e salvam para depois e enviam depois.

* **Submissões**: Formulários enviados contendo dados fornecidos pelo usuário.

Os serviços de metadados e dados do Portal AEM Forms oferecem suporte para rascunhos e envios. Por padrão, os dados são armazenados na instância de publicação, que é replicada reversa para a instância do autor configurada para estar disponível para colaboração com outras instâncias de publicação.

A preocupação com a abordagem predefinida existente é que ela armazena todos os dados na instância de publicação, incluindo os dados que podem ser Informações pessoais identificáveis (PII).

Além da abordagem padrão acima mencionada, uma implementação alternativa também está disponível para enviar os dados do formulário diretamente para o processamento, em vez de salvá-los localmente. Os clientes que têm preocupações com o armazenamento de dados potencialmente confidenciais na instância de publicação podem escolher a implementação alternativa na qual os dados são enviados para um servidor de processamento. Como o processamento acontece na instância do autor, ele normalmente permanece em uma zona segura.

>[!NOTE]
>
>Quando você usa a ação de envio do Portal do Forms ou habilita a opção Armazenar dados no portal de formulários em um formulário adaptável, os dados do formulário são armazenados AEM repositório. Em um ambiente de produção, é recomendável não armazenar dados de rascunho ou de formulário enviado em AEM repositório. Em vez disso, é necessário integrar os rascunhos e o componente de envio a um armazenamento seguro, como o banco de dados corporativo, para armazenar rascunhos e dados de formulários enviados.
>
>Para obter mais informações, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

## Configuração de rascunhos e serviços de envios do Forms Portal {#configuring-forms-portal-drafts-and-submissions-services}

Na Configuração do Console da Web AEM ( `https://[host]:'port'/system/console/configMgr`), clique em para abrir **Configuração de rascunho e envio do portal do Forms** no modo de edição.

Especifique os valores para as propriedades com base em seus requisitos, conforme descrito abaixo:

### Serviços prontos para uso para armazenar dados na instância de publicação {#out-of-the-box-services-to-store-data-on-publish-instance}

Os dados são replicados inversamente para a instância do autor configurada.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Serviço de Dados de Rascunho do Forms Portal (Identificador para serviço de dados de rascunho (<strong>rascunho.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Rascunho do Forms Portal (Identificador para serviço de metadados de rascunho (<strong>rascunho.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de dados de envio do Forms Portal (identificador para enviar serviço de dados (<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Envio do Portal Forms (Identificador para serviço de metadados de envio (<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Serviços prontos para uso para armazenar dados na instância de processamento remoto {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Os dados são enviados diretamente para a instância remota configurada

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Serviço de Dados de Rascunho do Forms Portal (Identificador para serviço de dados de rascunho (<strong>rascunho.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Rascunho do Forms Portal (Identificador para serviço de metadados de rascunho (<strong>rascunho.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de dados de envio do Forms Portal (identificador para enviar serviço de dados (<strong>submit.data.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Envio do Portal Forms (Identificador para serviço de metadados de envio (<strong>submit.metadata.service</strong>)</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Além da configuração especificada acima, forneça informações sobre a instância de processamento remoto configurada.

Na Configuração do Console da Web AEM ( `https://[host]:'port'/system/console/configMgr`), clique em para abrir **Serviço de Definições do AEM DS** no modo de edição. Na caixa de diálogo Serviço de Configurações do AEM DS, forneça informações sobre o URL do servidor de processamento, o nome de usuário do servidor de processamento e a senha.

>[!NOTE]
>
>Uma implementação de amostra também é fornecida para armazenar dados do usuário em um banco de dados. Para entender como configurar os serviços de dados e metadados para armazenar dados do usuário em um banco de dados externo, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).
