---
title: Personalização de serviços de dados de rascunho e envio
seo-title: Personalização de serviços de dados de rascunho e envio
description: Por padrão, a AEM Forms armazena formulários adaptativos de rascunho e enviados em um nó padrão na instância Publicar. No entanto, você pode configurar os serviços de dados de rascunho e envio da AEM Forms para personalizar o armazenamento de formulários adaptativos de rascunho e enviados.
seo-description: Por padrão, a AEM Forms armazena formulários adaptativos de rascunho e enviados em um nó padrão na instância Publicar. No entanto, você pode configurar os serviços de dados de rascunho e envio da AEM Forms para personalizar o armazenamento de formulários adaptativos de rascunho e enviados.
uuid: c3ec1708-3b11-4142-93f0-1cffb6643f34
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 602fd6a9-9a65-411c-8475-a4082a3fdee0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---


# Personalizar serviços de dados de rascunho e envio {#customizing-draft-and-submission-data-services}

## Visão geral {#overview}

O AEM Forms permite que os usuários salvem um formulário adaptável como rascunho. A funcionalidade de rascunho fornece aos usuários a opção de manter um formulário de trabalho em andamento. Em seguida, um usuário pode preencher e enviar o formulário a qualquer momento a partir de qualquer dispositivo.

Por padrão, a AEM Forms armazena os dados do usuário associados ao rascunho e ao envio na instância Publicar no nó `/content/forms/fp`.

No entanto, os componentes do portal da AEM Forms fornecem serviços de dados que permitem personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Por exemplo, você pode armazenar os dados em um armazenamento de dados implementado atualmente em sua organização.

Para personalizar o armazenamento dos dados do usuário, é necessário implementar os serviços [Rascunho de dados](/help/forms/using/custom-draft-submission-data-services.md#p-draft-data-service-p) e [Enviar dados](/help/forms/using/custom-draft-submission-data-services.md#p-submission-data-service-p).

## Pré-requisitos {#prerequisites}

* Habilitar [componentes do portal do Forms](/help/forms/using/enabling-forms-portal-components.md)
* Criar uma [página de portal de formulários](/help/forms/using/creating-form-portal-page.md)
* Habilitar [formulários adaptáveis para o portal de formulários](/help/forms/using/draft-submission-component.md)
* Saiba mais sobre [detalhes de implementação do armazenamento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Serviço de dados de rascunho {#draft-data-service}

Para personalizar o armazenamento dos dados de rascunho do usuário, é necessário fornecer a implementação de todos os métodos da interface `DraftAFDataService`.

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
  * @param draftUserDataMap contains Form Data (key - "guideState"), Adaptive Form Name (Key - "guideName"), and Draft DataID (Key - "userDataID") in case of update
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

Para personalizar o armazenamento dos dados de envio do usuário, é necessário fornecer a implementação de todos os métodos da interface `SubmittedAFDataService`.

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

