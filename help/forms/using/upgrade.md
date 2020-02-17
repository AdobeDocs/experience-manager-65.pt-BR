---
title: Atualizar para o AEM 6.5 Forms
seo-title: Atualizar para o AEM 6.5 Forms
description: É possível fazer uma atualização direta do AEM 6.3 Forms e do AEM 6.4 Forms para o AEM 6.5 Forms.
seo-description: É possível fazer uma atualização direta do AEM 6.3 Forms e do AEM 6.4 Forms para o AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 43fe9540a3a29ae86f48756c77001c0a4b8ea3e4

---


# Atualizar para o AEM 6.5 Forms{#upgrade-to-aem-forms}

O AEM 6.5 Forms inclui vários novos recursos e melhorias que simplificam a criação, o gerenciamento e as experiências do usuário com formulários e correspondências. Para saber mais sobre todos os novos recursos e melhorias do AEM 6.5 Forms, consulte o documento [de resumo dos](../../forms/using/whats-new.md)novos recursos.

Você pode atualizar a instalação existente do LiveCycle ou AEM Forms para obter novos recursos e melhorias oferecidos no AEM 6.5 Forms, além de manter intactos os dados, processos e ativos existentes. Durante a atualização, os metadados e o estado dos processos também são preservados. Você pode escolher um caminho de atualização para começar a atualização.

O diagrama a seguir exibe os caminhos de atualização disponíveis para o AEM Forms no OSGi:

![](do-not-localize/osgi-upgrade-path.png)

Você pode fazer uma atualização direta de:

* Formulários AEM 6.3 no OSGi
* Formulários AEM 6.4 no OSGi

Você também pode fazer uma atualização de multi-hop de

* Formulários AEM 6.0 no OSGi
* Formulários AEM 6.1 no OSGi
* Formulários AEM 6.2 no OSGi

O diagrama a seguir exibe os caminhos de atualização disponíveis para o AEM Forms no JEE:

![](do-not-localize/jee-upgrade-6-5.png)

Você pode fazer uma atualização direta de:

* AEM 6.3 Forms em JEE
* AEM 6.3 Forms em JEE

Você também pode fazer uma atualização de multi-hop de

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* AEM 6.0 Forms em JEE
* AEM 6.1 Forms em JEE
* AEM 6.2 Forms em JEE

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM package share. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
