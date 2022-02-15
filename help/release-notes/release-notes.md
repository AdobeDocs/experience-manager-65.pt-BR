---
title: ' [!DNL Adobe Experience Manager] '
description: '[!DNL Adobe Experience Manager]As notas o 6.5 que descrevem as informações da versão, novidades, como instalar e listas detalhadas de modificação.'
exl-id: 0288aa12-8d9d-4cec-9a91-7a4194dd280a
source-git-commit: b36b7b0dafbce3aa75afff60fae3cc714b6ac902
workflow-type: tm+mt
source-wordcount: '3887'
ht-degree: 4%

---

# [!DNL Adobe Experience Manager] {#aem-service-pack-release-notes}

## Informações da versão {#release-information}

| Produtos | [!DNL Adobe Experience Manager] 6.5 |
| -------- | ---------------------------- |
| Versão | 6.5.11.0 |
| Tipo | Lançamento do Service Pack |
| Data | 25 de novembro de 2021 |
| URL de download | [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip) |

## [!DNL Adobe Experience Manager] {#what-is-included-in-aem}

[!DNL Adobe Experience Manager] [!DNL Adobe Experience Manager]

[!DNL Adobe Experience Manager]

* Added multifield support for multiline text data type.

* Enhancement to make users aware of the asynchronous job currently running in the background to prevent them from triggering multiple asynchronous operations on same path.

* [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip) [!DNL Core Components]

* A user experience enhancements displays the number of assets present in a folder. [!DNL Assets]

   ![](/help/assets/assets/browse-folder-number-of-assets.png)

* Business profiles support for Adobe Asset Link.

* [!DNL Dynamic Media][!DNL Dynamic Media Classic] [](/help/assets/dm-general-settings.md)

   ![](/help/assets/assets-dm/dm-general-settings.png)

* [!DNL Dynamic Media][!DNL Dynamic Media Classic] [](/help/assets/dm-publish-settings.md)

   ![](/help/assets/assets-dm/dm-publish-setup.png)

* The built-in repository (Apache Jackrabbit Oak) is updated to 1.22.9.

[!DNL Experience Manager]

### [!DNL Sites] {#sites-65110}

>[!WARNING]
>
>A new version of the &quot;index definition&quot; package is being developed. The link below will be published as soon as it is made available.

To access headless content delivery using Content Fragments with GraphQL and use the enhanced Content Fragment Models and Editor capabilities, install the index definition package, and reindex the following asynchronous AEM index definitions:

* `/oak:index/assetPrefixNodename`

* `/oak:index/fragments`

* `/oak:index/graphqlConfig`

[!DNL Sites]

* Template to create a content fragment is not visible when creating a content fragment (SITES-3365).

* 

* `/apps/system``/libs`

* Features making use of content fragments are not functioning as usual on installing the previous service pack (SITES-3151).

* 

* GraphiQL is not loading models (schemas) and is encountering error for endpoint JSON (SITES-2428).

* 

* Tags data type does not support certain data types (SITES-2390).

* 

* Arrow in breadcrumb is not aligned properly in Content Fragments Editor (SITES-2341).

* Content fragment reference search is slow for large datasets (SITES-2147).

* 

* No warning is displayed when content fragment is published along with an associated model and the model introduces braking changes (SITES-1988).

* URL editing of content fragment model is different for different use cases of editing content fragment models (SITES-1980).

* 

* 

* 

* Global search in fragment picker path is not working (SITES-1973).

* References are updating when moving a content fragment (SITES-1897).

* Option to create page is missing in Card view and Column view (NPR-37549).

* When reordering components on a Launch page, promoting the Launch does not preserve the reordering of components (NPR-37539).

* The option to select all the items in a list is not working on the rollout page (NPR-37443).

* `wcm-workflow-service`

* Move operation on folders in the Sites console is failing with an error message &quot;Failed to retrieve launches information for selected item”(NPR-37340).

* When generating a thumbnail for blueprint and rolling out to live copies, the inheritance for tabs after thumbnail in live copies is broken (NPR-37190).

* The filter predicate to display Live Copy does not display all the live copies (NPR-37126).

* Replication event does not return the list of all the parent and children pages that were marked for deletion when the replication event handler is called on the author (NPR-37123).

* When saving a multi-valued property using Bulk Editor, then the comma-separated string is stored as the first element of the array (NPR-37089).

* The component layout resizing does not work in mobile layout (NPR-37086).

* A new node is incorrectly created at the live copy level on saving page properties after adding rollout configurations (NPR-37084).

* User cannot create live copies or roll out using page properties for new master pages (SITES-3442).

* Tags display tag names instead of title and close option does not remove the tags completely due to tags property working incorrectly when inheritance is cancelled at property level (NPR-36831).

* Option to deselect all items is not working and header overlaps with first row in table, of the page which displays a list of live copies (NPR-37070).

* In a custom dialog used in a workflow, when trying to validate the dialog, Experience Manager fails with an error in the browser console (GRANITE-35049).

[!DNL Adobe Experience Manager Sites]

* 

* The order of browser mode focus now moves sequentially on various options on User interface (SITES-1791).

* Screen readers now narrate whether the selected tree item is in selected state and also announces to the user that the action region is displayed (SITES-2109).

* Screen readers now announce when there is a loading indicator on selecting filter or searching a page (SITES-1790).

* 

* When navigating in browse mode, screen readers narrate the role of the content page and selected state of a page when enter key is pressed (SITES-1579).

* 

* Form fields now have visual labels apart from the placeholders, so that screen reader users are guided appropriately when entering the field values (SITES-1258).

### [!DNL Assets] {#assets-65110}

[!DNL Assets]

* [!DNL Assets]`Tab`
* [!DNL Dynamic Media] Keyboard users are not able to focus the input and screen readers do not announce the state for the control as disabled.
* [!DNL Dynamic Media]

* [!DNL Experience Manager Assets]

[!DNL Assets]

* `POST` `POST`

* When creating a live copy of the blueprint having a nested folder structure, the modified properties of the source folder are not updated in the live copy folder (NPR-37449).

* When selecting multiple assets and modifying the metadata field values, saving the assets does not retain the values. Also, the metadata changes are not applied (NPR-37341).

* When selecting multiple assets and modifying the properties, the custom properties (dropdowns) values are overridden by the default values (NPR-36437).

* Incorrect PDF rendition is generated for the brochure, flyer, and InDesign templates (NPR-36433).

* [!DNL Adobe Target][!DNL Experience Manager][!DNL Adobe Analytics]

* [!DNL Asset Link]

<!-- Add 
* [!DNL Adobe Asset Link] is not able to access the digital assets even when the [!DNL Creative Cloud] and [!DNL Experience Management] entitlements are provided by two different organizations. -->

* Adding a video with custom metadata generated upon upload to a page displays an error about unknown namespace, even if the namespace is registered (CQ-4331471).

* [!DNL Assets][!DNL Launcher]

### [!DNL Dynamic Media] {#dynamic-media-65110}

[!DNL Dynamic Media]

* [!DNL Dynamic Media][!DNL Experience Manager]

* ECatalogs are not published on publishing PDF files (CQ-4329886).

* 3D assets do not load when the published page is opened in case the component is using out-of-the-box preset (CQ-4329205).

* Issues in PDF asset processing in case of large repositories (CQ-4328711).

* [!DNL Experience Manager][!DNL Scene7]

* Users are not able to see the default metadata properties for a .MOV asset (CQ-4332546).

* [!DNL Dynamic Media][!DNL Experience Manager]

* Upload issues when custom company root is setup (CQ-4332800).

* [!DNL Experience Manager]`ActivationModel` (CQ-4330512).

* `DamEventRecorder`

* If a shoppable video hyperlink (linked-URL) contains special characters, the target URL gets encoded by the viewer and results as an incorrect product page (CQ-4331639).

* In a video profile page, the toolbar options disappear if the user selects a video profile immediately on page load (CQ-4308521).

* DM asset processing failure due to JCR concurrent writes (CQ-4333489).

* Accessing the Video Profiles page fails if user&#39;s video profile root has custom access policies defined on video profiles root node (CQ-4332941).

* In a zoomable image, using the shortcut keys (&#39;+&#39;, &#39;-&#39;) or &#39;Esc&#39; key traps the screen readers focus (CQ-4290719).

* 

* When using keyboard navigation to open the email link popup window, the error suggestions displayed on the user interface for the &#39;To&#39; and &#39;From&#39; fields are not descriptive (CQ-4290930).

* When navigating to the email link dialog box, the screen reader does not narrate the label information for the newly added edit fields on using the down arrow and form mode shortcut key (&#39;F&#39;) (CQ-4290934).

* When navigating to the email link dialog box, the screen reader does not reflect the visual asterisk (*) symbol for the &#39;To&#39; and &#39;From&#39; mandatory fields (CQ-4290935).

* The users are not able to identify the landmark and region using the shortcut keys (&#39;D&#39;, &#39;R&#39;) (CQ-4312118).

<!-- Anuj to check if this section is required or not. We have an enh. in CIF area that is mentioned. It is added above and not part of this bug fix section.
-->

### Commerce {#commerce-65110}

* 

* Unpublishing a folder does not unpublish the products of that folder completely, the products are removed from the publisher but still exists in the author instance (CQ-4332731).

### Plataforma {#platform-65110}

* When a user clicks on the reorder icon for a multifield option, the scroll bar disappears from the user interface (CQ-4331100).

* After upgrade, when a user opens the workplace login container component, the header of the dialog box are not visible on the user interface (CQ-4316173).

### Integrações {#integrations-65110}

* [!DNL Adobe Target][!DNL Experience Manager][!DNL Adobe Analytics]

### Projetos {#projects-65110}

* [!DNL Experience Manager]`/content/dam/projects` It resets the assigned metadata schema and properties of the folder to default (NPR-37124).

### Interface do usuário {#user-interface-65110}

* The folder icon representing the model is incorrect (NPR-37176).

* When a user performs a search or browses using the path field browser, incorrect nodes are displayed (NPR-37175).

* On the publish instance, the incoming requests are blocked for several minutes (NPR-37169).

* When adding a multifield property in a dialog box for a custom workflow, the dialog box fails to proceed and the user is not able to close the dialog box (NPR-37075).

### Translation projects {#translation-65110}

* Auto-promotion of the translation launch fails with an exception (NPR-37528).

* Translation of the Experience Fragment does not update the references for the language copy of the URL (NPR-37522).

* When an Experience Fragment is created in a path that does not match the path of the language root structure, adding that page to a translation project reflects a blank error message (NPR-37425).

* When a page (English) containing Experience Fragments is modified and sent for translation, the already translated Experience Fragments are overwritten by English content (NPR-37283).

* Translation provider filter is not working appropriately (NPR-37186).

* Experience Fragment and Accordion components are not getting translated out-of-the-box for the sample site content (NPR-37170).

* [!DNL Experience Manager]

* When adding pages inside launch, the translation pages having similar names are not included in the project (NPR-37082).

* When exporting a forms dictionary as a .xliff file using the translator interface, the field order of the exported file is incorrect (NPR-37048).

* When rolling out a parent page from a translation project, the language-specific child pages are deleted (NPR-36998).

* When creating a translation project, cyclic referencing of the pages triggers a launch which results in an error (CQ-4332982).

* The experience fragment link in the translated experience fragment and page contains the launch reference (NPR-37649).

### Sling {#sling-65110}

* When uploading a new package, the memory alias in the MapEntries map is removed (NPR-37067).

### Fluxo de trabalho {#workflow-65110}

* `Deactivate``InboxOmniSearchHandler`

### [!DNL Communities] {#communities-65110}

* `Post`

* When deploying the application, a segment not found exception is observed due to the long running session of SyncManager (NPR-37351).

* The user is not able to see the thread replies on the forum discussion post (NPR-37083).




<!--
Need to verify with Engineering, the status is currently showing as Resolved
-->


<!--
### [!DNL Brand Portal] {#brandportal-65110}

*

-->

### [!DNL Forms] {#forms-65110}


>[!NOTE]
>
>* O [!DNL Experience Manager Forms] lança os pacotes complementares uma semana após a data programada de lançamento do [!DNL Experience Manager] Service Pack.


**Formulários adaptáveis**

* `Wizard`

* Validations on a date field in an adaptive form does not work, as expected (NPR-37556).

* When the label text for the Checkbox and Radio Button components is long, the text does not fit appropriately (NPR-37294).

* When you apply styling changes to the Thank You message of the AEM Forms Container component, the changes do not replicate in the source adaptive form (NPR-37284).

* `Switch`

* `Submit``Enter`

* The Remove operation for the File Attachment component does not work, as expected (NPR-37376).

* When a label for a field exceeds 1000 characters in an adaptive form that translates to various languages, the dictionary fails to retrieve the translation of the label (CQ-4329290).

**Serviços de documento**

* An error displays while using the Assembler service (NPR-37606):

   ```TXT
     500 Internal Server Error
   ```

* When the document attachments are passed to the Assembler service, the following exception displays (NPR-37582):

   ```TXT
     com.adobe.livecycle.assembler.client.ProcessingException: ⁪: Failed to execute the DDX
   ```

* Missing closing parenthesis from data after converting a PDF document to a PDF-A/1B PDF document (NPR-37608).

**Formulários HTML5**

* When you install AEM 6.5.10.0, the HTML preview for an XDP form does not work (NPR-37503, CQ-4331926).

* Text overlapping issues while migrating the PDF forms to HTML 5 forms in various languages (NPR-37173).

**Cartas**

* When you submit a letter and reopen it in HTML view, the position of text document fragments does not remain the same (NPR-37307).

**Fluxo de trabalho dos formulários**

* `Notify on Complete of Container Workflow`

**Foundation JEE**

* After installing AEM 6.5 Forms Service Pack 9, the CRX repository URLs are no longer available (NPR-37592).

****

>[!NOTE]
>
>If you have not upgraded to AEM 6.5.11.0 Forms, install the AEM Forms 6.5.11.1 add-on package directly. If you have installed AEM 6.5.11.0 Forms, Adobe recommends to upgrade to AEM 6.5.11.1 Forms.

* Submit actions, Send Email and Invoke an AEM Workflow stop working after installing the Forms 6.5.11.0 add-on package.
* CreatePDF operation stops converting Microsoft Word documents to PDF documents after installing the Forms 6.5.11.0 add-on package.
* (Somente JEE) Vulnerabilidades críticas de segurança (CVE-2021-44228 e CVE-2021-45046) relatadas para o Apache Log4j2.
* (JEE only) Assembler DSC in 6.5.11.0 patch contains incorrect metainfo like specification version and impl version.


[[!DNL Experience Manager] ](https://helpx.adobe.com/security/products/experience-manager.html)

## Instalar 6.5.11.0 {#install}

****

* [](/help/sites-deploying/upgrade.md)
* [](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html)
* On a deployment with MongoDB and multiple instances, install Experience Manager 6.5.11.0 on one of the Author instances using the Package Manager.

>[!NOTE]
>
>[!DNL Adobe Experience Manager]

### Install the service pack {#install-service-pack}

[!DNL Adobe Experience Manager]

1. Restart the instance before installation if the instance is in update mode (when the instance was updated from an earlier version). Adobe recommends a restart if the current uptime for an instance is high.

1. [!DNL Experience Manager]

1. [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.11.zip)

1. Abra Gerenciador de pacotes e clique em **[!UICONTROL Fazer upload de pacote]** para fazer upload do pacote. [](/help/sites-administering/package-manager.md)

1. ****

1. To update the S3 connector, stop the instance after installation of the Service Pack, replace the existing connector with a new binary file provided in the install folder, and restart the instance. [](/help/sites-deploying/data-store-config.md#upgrading-to-a-new-version-of-the-s-connector)

>[!NOTE]
>
>Dialog on Package Manager UI sometimes exits during the installation of the service pack. Adobe recommends that you wait for error logs to stabilize before accessing the deployment. Wait for the specific logs related to the uninstall of the updater bundle before being assured that the installations is successful. [!DNL Safari]

**Instalação automática**

[!DNL Experience Manager]

`../crx-quickstart/install` The package is automatically installed.

[](/help/sites-administering/package-manager.md#package-share) `cmd=install&recursive=true`

>[!NOTE]
>
>Adobe Experience Manager 6.5.11.0 does not support Bootstrap installation.

****

1. `/system/console/productinfo``Adobe Experience Manager (6.5.11.0)`

1. ********`/system/console/bundles`

1. `org.apache.jackrabbit.oak-core``/system/console/bundles`

[](/help/sites-deploying/technical-requirements.md)

<!-- 

### Install Adobe Experience Manager Forms add-on package {#install-aem-forms-add-on-package}

>[!NOTE]
>
>Skip if you are not using Experience Manager Forms. Fixes in Experience Manager Forms are delivered through a separate add-on package a week after the scheduled [!DNL Experience Manager] Service Pack release.

1. Ensure that you have installed the Adobe Experience Manager Service Pack.
1. Download the corresponding Forms add-on package listed at [AEM Forms releases](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#forms-updates) for your operating system.
1. Install the Forms add-on package as described in [Installing AEM Forms add-on packages](/help/forms/using/installing-configuring-aem-forms-osgi.md#install-aem-forms-add-on-package).

>[!NOTE]
>
>Experience Manager 6.5.10.0 includes a new version of [AEM Forms Compatibility Package](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html#aem-65-forms-releases). If you are using an older version of AEM Forms Compatibility Package and updating to Experience Manager 6.5.10.0, install the latest version of the package post installation of Forms Add-On Package.

### Install Adobe Experience Manager Forms on JEE {#install-aem-forms-jee-installer}

>[!NOTE]
>
>Skip if you are not using AEM Forms on JEE. Fixes in Adobe Experience Manager Forms on JEE are delivered through a separate installer.

For information about installing the cumulative installer for Experience Manager Forms on JEE and post-deployment configuration, see the [release notes](jee-patch-installer-65.md).

>[!NOTE]
>
>After installing the cumulative installer for Experience Manager Forms on JEE, install the latest Forms add-on package, delete the Forms add-on package from the `crx-repository\install` folder, and restart the server.

-->

### UberJar {#uber-jar}

[](https://repo.maven.apache.org/maven2/com/adobe/aem/uber-jar/6.5.11/)

[](/help/sites-developing/ht-projects-maven.md)

```shell
<dependency>
     <groupId>com.adobe.aem</groupId>
     <artifactId>uber-jar</artifactId>
     <version>6.5.11</version>
     <scope>provided</scope>
</dependency>
```

>[!NOTE]
>
>`repo.adobe.com` `uber-jar-<version>.jar` `classifier``apis``dependency`

## Recursos obsoletos {#removed-deprecated-features}

[!DNL Experience Manager] An alternate option is provided.

Review if you use a feature or a capability in a deployment. Also, plan to change the implementation to use an alternate option.

| Área | Recurso | Substituição |
|---|---|---|
| Integrações | ****[!DNL Experience Manager][!DNL Adobe Target] [!DNL Adobe I/O][!DNL Experience Manager] | [!DNL Adobe I/O][!DNL Experience Manager] |
| Conectores | The Adobe JCR Connector for Microsoft® SharePoint 2010 and Microsoft® SharePoint 2013 is deprecated for Experience Manager 6.5. | N/A |

## Problemas conhecidos {#known-issues}

* When you install AEM 6.5 Service Pack 11 and try to download the status ZIP file, Experience Manager downloads a corrupt file. [](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/featurepack/sites-seo-index-content-1.0.0.zip)

* [!DNL Microsoft Windows Server 2019][!DNL MySQL 5.7][!DNL JBoss EAP 7.1][!DNL Microsoft Windows Server 2019][!DNL AEM Forms 6.5.10.0]

* [!DNL Experience Manager]`RRD4JReporter``error.log` To resolve the issue, restart the instance.

* [!DNL Experience Manager][!DNL Experience Manager]`/var/workflow/models/dam`
To retrieve your runtime copy, Adobe recommends to synchronize the design-time copy of the custom workflow model with its runtime copy using the HTTP API:
   `<designModelPath>/jcr:content.generate.json`.

* [!DNL Assets][!DNL Brand Portal] [!DNL Brand Portal]

* When a user selects to configure a field for the first time in an adaptive form, the option to save a configuration does not display in Properties Browser. Selecting to configure some other field of the adaptive form in the same editor resolves the issue.

* The following errors and warning messages may display during installation of Experience Manager 6.5.x.x:
   * “When the Adobe Target integration is configured in Experience Manager using the Target Standard API (IMS authentication), then exporting Experience Fragments to Target results in wrong offer types getting created. Em vez do tipo &quot;Fragmento de experiência&quot;/fonte &quot;Adobe Experience Manager&quot;, o Target cria várias ofertas com o tipo &quot;HTML&quot;/fonte &quot;Adobe Target Classic&quot;.
   * `com.adobe.granite.maintenance.impl.TaskScheduler`
   * Adaptive Form server-side validation fails when aggregate functions such as SUM, MAX, and MIN are used (CQ-4274424).
   * `com.adobe.granite.maintenance.impl.TaskScheduler`
   * Hotspot in a Dynamic Media interactive image is not visible when previewing the asset through Shoppable Banner viewer.
   * `com.adobe.cq.social.cq-social-jcr-provider bundle com.adobe.cq.social.cq-social-jcr-provider:1.3.5 (395)[com.adobe.cq.social.provider.jcr.impl.SpiSocialJcrResourceProviderImpl(2302)]`

* When trying to move/delete/publish either Content Fragments or Sites/Pages, there is an issue when Content Fragment references are fetched, as the background query will fail; i.e. the functionality will not work.
`/oak:index/damAssetLucene`

   ```xml
   "tags": [
       "visualSimilaritySearch"
     ]
   "refresh": true
   ```

## OSGi bundles and content packages included {#osgi-bundles-and-content-packages-included}

[!DNL Experience Manager]

* [List of OSGi bundles included in Experience Manager 6.5.11.0](assets/65110_bundles.txt)

* [List of Content Packages included in Experience Manager 6.5.11.0](assets/65110_packages.txt)

## Restricted websites {#restricted-sites}

These websites are only available to customers. Se você for um cliente e precisar de acesso, entre em contato com o gerente de contas da Adobe.

* [Baixe o produto em licensing.adobe.com](https://licensing.adobe.com/)
* [](https://experienceleague.adobe.com/docs/customer-one/using/home.html)

## [!DNL Adobe Experience Manager]{#key-releases-since-last-sp}

Between August 26, 2021, and November 25, 2021, Adobe released the following, in addition to the Service Packs:

* [!DNL Adobe Experience Manager][](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/2021/release-notes-2021-9-0.html)[](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/release-notes/release-notes-current.html?lang=pt-BR)

* [[!DNL Experience Manager] ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/release-notes.html)

* [](https://experienceleague.adobe.com/docs/experience-manager-screens/user-guide/release-notes/release-notes-fp-202109.html)


>[!MORELIKETHIS]
>
>* [[!DNL Experience Manager] ](https://business.adobe.com/products/experience-manager/adobe-experience-manager.html)
>* [[!DNL Experience Manager] ](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=pt-BR)
>* [Inscreva-se em Atualizações de produtos de prioridade da Adobe](https://www.adobe.com/subscription/priority-product-update.html)

