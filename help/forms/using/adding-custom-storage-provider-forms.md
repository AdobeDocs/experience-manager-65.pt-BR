---
title: armazenamento personalizado para componentes de rascunhos e envios
seo-title: armazenamento personalizado para componentes de rascunhos e envios
description: Veja como personalizar o armazenamento de dados do usuário para rascunhos e envios.
seo-description: Veja como personalizar o armazenamento de dados do usuário para rascunhos e envios.
uuid: ac2e80ee-a9c7-44e6-801e-fe5a840cb7f8
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 154255e7-468a-42e6-a33d-eee691cf854d
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---


# armazenamento personalizado para componentes de rascunhos e envios {#custom-storage-for-drafts-and-submissions-component}

## Visão geral {#overview}

O AEM Forms permite salvar um formulário como rascunho. A funcionalidade de rascunho permite manter um formulário de trabalho em andamento, que pode ser preenchido e enviado posteriormente de qualquer dispositivo.

Por padrão, o AEM Forms armazena os dados do usuário associados ao rascunho e ao envio de um formulário no `/content/forms/fp` nó da instância Publicar. Além disso, os componentes do portal do AEM Forms fornecem serviços de dados, que podem ser usados para personalizar a implementação do armazenamento de dados do usuário para rascunhos e envios. Por exemplo, você pode armazenar dados do usuário em um armazenamento de dados.

## Pré-requisitos  {#prerequisites}

* Ativar componentes do portal de [formulários](/help/forms/using/enabling-forms-portal-components.md)
* Criar uma página do portal de [formulários](/help/forms/using/creating-form-portal-page.md)
* Ativar formulários [adaptáveis para o portal de formulários](/help/forms/using/draft-submission-component.md)
* Saiba mais sobre detalhes de [implementação do armazenamento personalizado](/help/forms/using/draft-submission-component.md#customizing-the-storage)

## Serviço de rascunho de dados {#draft-data-service}

Para personalizar o armazenamento de dados do usuário para rascunhos, é necessário implementar todos os métodos da `DraftDataService` interface. O código de amostra a seguir descreve os métodos e argumentos.

```java
/**
 * DraftDataService service will get/delete/save user data (attachments and form data) filled with a draft instance of Form
 */

public interface DraftDataService {

    /**
     * To save/modify user data for this userDataID, it will be null in case of creation
     * @param draftDataID: unique identifier associated with the form data
     * @param formName: name of the form whose draft is being saved
     * @param formData: user data associated with this draft
     * @return userdataID corresponding to which user data has been stored and which can be used later to retrieve this user data
     * @throws FormsPortalException
     */
    public String saveData (String draftDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Returns the user data stored against the ID passed as the argument
     * @param userDataID: unique data id for user data associated with a draft
     * @return user data associated with this data ID
     * @throws FormsPortalException
     */

    public byte[] getData (String userDataID) throws FormsPortalException;

    /**
     * To delete data associated with this draft
     * @param userDataID: unique data id for data associated with a draft
     * @return status of delete operation on data associated with this draft
     * @throws FormsPortalException
     */

    public boolean deleteData (String userDataID) throws FormsPortalException;

    /**
     * Saves the attachment for current form instance
     * @param attachmentsBytes: byte array of the attachment to be saved
     * @return unique id (attachmentID) for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment (byte[] attachmentBytes) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

## Serviço de dados de envio {#submission-data-service}

Para personalizar o armazenamento de dados do usuário para envios, é necessário implementar todos os métodos da `SubmitDataService` interface. O código de amostra a seguir descreve os métodos e argumentos.

```java
/**
 * SubmitDataService service will get/delete/submit user data (attachments and form data) filled with a submission of Form
 */
public interface SubmitDataService {

    /**
     * Submits the user data passed in argument map
     * @param userDataID, unique identifier associated with this user data
     * @param formName, name of the form whose draft is being submitted
     * @param formData, user data associated with this submission
     * @return userdataID, corresponding to which the user data has been stored and which can be used later to retrieve this data
     * @throws FormsPortalException
     */
    public String saveData (String userDataID, String formName, String formData) throws FormsPortalException;

    /**
     * Submits the user data provided as byte array
     * @param id
     * @param data
     * @return id corresponding to saved data
     * @throws FormsPortalException
     */
    public String saveData (String id, byte[] data) throws FormsPortalException;

    /** Submits the user data provided as byte array asynchronously for the user name provided in the options map
     * @param data data to be saved in bytes
     * @param options map containing options that affect this save
     * @return id of the saved data instance
     */
    public String saveDataAsynchronusly(byte[] data, Map<String, Object> options) throws FormsPortalException;

    /**
     * Gets the user data stored against the ID passed as argument
     * @param userDataID: unique id associated with this user data for this submission
     * @return user data associated with this submission
     * @throws FormsPortalException
     */
    public byte[] getData(String userDataID) throws FormsPortalException;

    /**
     * Deletes user data stored against the userDataID
     * @param userDataID: unique id associated with this user data for this submission
     * @return status of the delete operation on this submission
     * @throws FormsPortalException
     */

    public boolean deleteData(String userDataID) throws FormsPortalException;

    /**
     * Submits the attachment bytes passed as argument
     * @param attachmentsBytes: would expect byte array of the attachment for this submission
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachment(byte[] attachmentBytes) throws FormsPortalException;

    /** Submits the attachment bytes passed as argument asynchronously for the user id provided in options map.
     * @param attachmentBytes would expect byte array of the attachment for this submission
     * @param options map containing options that affect this save
     * @return attachmentID for the attachment just saved (so that it could be retrieved later)
     * @throws FormsPortalException
     */
    public String saveAttachmentAsynchronously(byte[] attachmentBytes, Map<String, Object> options) throws FormsPortalException;

    /**
     * To delete an attachment
     * @param attachmentID: Unique id for this attachment
     * @return status of delete operation performed on attachment corresponding to this attachment ID
     * @throws FormsPortalException
     */
    public boolean deleteAttachment (String attachmentID) throws FormsPortalException;

    /**
     * To get attachment bytes
     * @param attachmentID: unique id for this attachment
     * @return data corresponding to this attachmentID
     * @throws FormsPortalException
     */
    public byte[] getAttachment (String attachmentID) throws FormsPortalException;
}
```

O portal de formulários usa o conceito de identificador universalmente exclusivo (UUID) para gerar uma ID exclusiva para cada rascunho e formulário enviado. Você também pode gerar uma ID exclusiva própria. Você pode implementar a interface FPKeyGeneratorService, substituir seus métodos e desenvolver uma lógica personalizada para gerar uma ID exclusiva personalizada para cada rascunho e formulário enviado. Além disso, defina a classificação de serviço da implementação de geração de ID personalizada superior a 0. Ela garante que a implementação personalizada seja usada em vez da implementação padrão.

```java
public interface FPKeyGeneratorService {
    /**
     * returns a unique id for draft and submission
     *
     * @param none
     * @return unique id in string format as per the implementation
     * @throws FormsPortalException
     */
    public String getUniqueId() throws FormsPortalException;
}
```

Você pode usar a anotação abaixo para aumentar a classificação do serviço da ID personalizada gerada com o código acima:

`@Properties(value = { @Property(name = "service.ranking", intValue = 15) } )`

Para usar a anotação acima, importa o seguinte para o seu projeto:

```java
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
```

