---
title: Configurar serviços de armazenamento para rascunhos e envios
seo-title: Configurar serviços de armazenamento para rascunhos e envios
description: Saiba como configurar o armazenamento para rascunhos e envios
seo-description: Saiba como configurar o armazenamento para rascunhos e envios
uuid: 2f4efc07-312c-4908-8c91-84f4e6c5ad25
topic-tags: publish
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6ebb6420-68b6-4abc-b298-c252db038416
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configurar serviços de armazenamento para rascunhos e envios {#configuring-storage-services-for-drafts-and-submissions}

## Visão geral {#overview}

Com o AEM Forms, é possível armazenar:

* **Rascunhos**: Um formulário de trabalho em andamento que os usuários finais preenchem e salvam para mais tarde e enviam depois.

* **Envios**: Formulários enviados contendo dados fornecidos pelo usuário.

Os serviços de metadados e dados do portal de formulários AEM fornecem suporte para rascunhos e envios. Por padrão, os dados são armazenados na instância de publicação, que é revertida e replicada para a instância do autor configurada para que esteja disponível para implementação em outras instâncias de publicação.

A preocupação com a abordagem predefinida atual é que ela armazene todos os dados na instância de publicação, incluindo os dados que podem ser Informações pessoais identificáveis (PII).

Além da abordagem padrão mencionada acima, uma implementação alternativa também está disponível para encaminhar os dados do formulário diretamente para o processamento, em vez de salvá-los localmente. Os clientes que têm preocupações com o armazenamento de dados potencialmente confidenciais na instância de publicação podem escolher a implementação alternativa na qual os dados são enviados para um servidor de processamento. Como o processamento ocorre na instância do autor, ele geralmente permanece em uma zona segura.

>[!NOTE]
>
>Quando você usa a ação de envio do Portal do Forms ou habilita a opção Armazenar dados no portal de formulários em forma adaptável, os dados do formulário são armazenados no repositório do AEM. Em um ambiente de produção, é recomendável não armazenar dados de formulário rascunho ou enviados no repositório do AEM. Em vez disso, é necessário integrar os rascunhos e o componente de envio a um armazenamento seguro como o banco de dados corporativo para armazenar rascunhos e dados de formulários enviados.
>
>Para obter mais informações, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

## Configurar serviços de envio e rascunhos do Portal do Forms {#configuring-forms-portal-drafts-and-submissions-services}

Em Configuração do console da Web do AEM ( `https://[host]:'port'/system/console/configMgr`), clique para abrir Configuração **de rascunho e envio do portal de** formulários no modo de edição.

Especifique os valores para as propriedades com base em seus requisitos, conforme descrito abaixo:

### Serviços prontos para armazenar dados na instância de publicação {#out-of-the-box-services-to-store-data-on-publish-instance}

Os dados são replicados reversivamente para a instância do autor configurada.

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Serviço de Dados de Rascunho do Portal de Formulários(Identificador para serviço de dados de rascunho (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Rascunho do Portal do Forms (Identificador para serviço de metadados de rascunho (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de dados de envio do Portal do Forms (Identificador para serviço de dados de envio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Envio do Portal do Forms (Identificador para serviço de metadados de envio (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceImpl<br /> </td>
  </tr>
 </tbody>
</table>

### Serviços prontos para armazenar dados na instância de processamento remoto {#out-of-the-box-services-to-store-data-on-remote-processing-instance}

Os dados são enviados diretamente para a instância remota configurada

<table>
 <tbody>
  <tr>
   <th>Propriedade</th>
   <th>Valor</th>
  </tr>
  <tr>
   <td>Serviço de Dados de Rascunho do Portal de Formulários(Identificador para serviço de dados de rascunho (<strong>draft.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Rascunho do Portal do Forms (Identificador para serviço de metadados de rascunho (<strong>draft.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.DraftMetadataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de dados de envio do Portal do Forms (Identificador para serviço de dados de envio (<strong>submit.data.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitDataServiceRemoteImpl<br /> </td>
  </tr>
  <tr>
   <td>Serviço de Metadados de Envio do Portal do Forms (Identificador para serviço de metadados de envio (<strong>submit.metadata.service</strong>))</td>
   <td>com.adobe.fd.fp.service.impl.SubmitMetadataServiceRemoteImpl<br /> </td>
  </tr>
 </tbody>
</table>

Além da configuração especificada acima, forneça informações sobre a instância de processamento remoto configurada.

Na Configuração do console da Web do AEM ( `https://[host]:'port'/system/console/configMgr`), clique para abrir o Serviço **de configurações do** AEM DS no modo de edição. Na caixa de diálogo Serviço de configurações do AEM DS, forneça informações sobre o processamento do URL do servidor, o nome de usuário do servidor de processamento e a senha.

>[!NOTE]
>
>Uma implementação de amostra também é fornecida para armazenar dados do usuário em um banco de dados. Para entender como configurar os serviços de dados e metadados para armazenar dados do usuário em um banco de dados externo, consulte [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md).

