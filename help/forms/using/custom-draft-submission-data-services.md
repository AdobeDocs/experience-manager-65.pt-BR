---
title: Personalização de serviços de dados de Rascunho e Submissão
description: O AEM Forms, por padrão, armazena rascunhos e formulários adaptáveis enviados em um nó padrão na instância de Publicação. No entanto, você pode configurar os serviços de dados de rascunho e envio do AEM Forms para personalizar o armazenamento de rascunho e formulários adaptáveis enviados.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: ed10ef8c-7b9c-43cf-bea8-7cf9742a8cac
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 7da902b6-fe94-5180-8e7c-f6d1e38d01d5
    internal-label: Foundation Components
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---
# Personalização de serviços de dados de Rascunho e Submissão {#customizing-draft-and-submission-data-services}

## Visão geral {#overview}

O AEM Forms permite que os usuários salvem um formulário adaptável como um rascunho. A funcionalidade de rascunho fornece aos usuários a opção de manter um formulário de trabalho em andamento. O usuário pode então preencher e enviar o formulário a qualquer momento de qualquer dispositivo.

Por padrão, o AEM Forms armazena dados do usuário associados ao rascunho e ao envio na instância de Publicação no nó `/content/forms/fp`.

No entanto, os componentes do AEM Forms Portal fornecem serviços de dados que permitem personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Por exemplo, você pode armazenar os dados em um armazenamento de dados implementado atualmente em sua organização.

Para personalizar o armazenamento de dados do usuário, você deve implementar os serviços [Dados de Rascunho](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) e [Dados de Envio](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Pré-requisitos {#prerequisites}

* Habilitar [componentes do Forms Portal](/help/forms/using/enabling-forms-portal-components.md)
* Criar uma [página do Portal Forms](/help/forms/using/creating-form-portal-page.md)
* Habilitar [formulários adaptáveis para o Portal do Forms](/help/forms/using/draft-submission-component.md)
* Saiba mais sobre [detalhes de implementação do armazenamento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Serviço de dados de rascunho {#draft-data-service}

Para personalizar o armazenamento de dados de rascunho do usuário, você deve fornecer implementação para todos os métodos da interface `DraftAFDataService`.

Uma descrição dos métodos e seus argumentos é fornecida na seguinte amostra de código da interface:

```java
public interface DraftAFDataService {

 /**
  * Deletes the user data stored against the ID passed as the argument
  *
  * @param draftDataID
  * @return status for the just occurred delete draft UserData operation
  * @throws FormsPortalException
  */
 public Boolean deleteAFDraftUserData (String draftDataID) throws FormsPortalException;

 /**
  * Saves user data provided in the argument map
  *
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") if there is update
  * @return userData ID would be returned which needs to be saved in metadata node
  * @throws FormsPortalException
  */
 public String saveAFUserData (Map<String, Object> draftUserDataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as the argument
  *
  * @param Draft DataID
  * @return guideState (which would then be populated in adaptive form to reload the draft) which is stored against draftDataID
  * @throws FormsPortalException
  */
 public byte[] getAFDraftUserData(String draftDataID) throws FormsPortalException;

 /**
  * Saves the attachments for current adaptive form instance
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String saveAttachments(byte[] attachmentBytes) throws FormsPortalException;
}
```

## Serviço de dados de envio {#submission-data-service}

Para personalizar o armazenamento de dados de envio do usuário, você deve fornecer implementação para todos os métodos da interface `SubmittedAFDataService`.

Uma descrição dos métodos e seus argumentos é fornecida na seguinte amostra de código da interface:

```java
public interface SubmittedAFDataService {

 /**
  * Submits the user data passed in argument map
  *
  * @param submittedAFUserdataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID")
  * @return userData ID is returned that needs to be saved in the metadata node
  * @throws FormsPortalException
  */
 public String submitAFUserData (Map<String, Object> submittedAFUserdataMap) throws FormsPortalException;

 /**
  * Gets the user data stored against the ID passed as argument
  *
  * @param submitDataID
  * @return guideState which would be used to open DOR
  * @throws FormsPortalException
  */
 public byte[] getSubmittedAFUSerData(String submitDataID) throws FormsPortalException;

 /**
  * Deletes user data stored against the ID passed as argument
  *
  * @param Submit DataID
  * @return status of the delete operation on Submitted User data
  * @throws FormsPortalException
  */

 public Boolean deleteSubmittedAFUserData(String submitDataID) throws FormsPortalException;

 /**
  * Submits the attachment bytes passed as argument
  *
  * @param attachmentsBytes would expect byte array of the attachment to be saved
  * @return id for the attachment just saved (so that it could be retrieved later)
  * @throws FormsPortalException
  */
 public String submitAttachments(Object attachmentBytes) throws FormsPortalException;

}
```
