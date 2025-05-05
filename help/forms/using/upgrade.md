---
title: Atualização para o AEM 6.5 Forms
description: Você pode realizar uma atualização direta do AEM 6.3 Forms e do AEM 6.4 Forms para o AEM 6.5 Forms.
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 6%

---

# Atualização para o AEM 6.5 Forms {#upgrade-to-aem-forms}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=pt-BR) |
| AEM 6.5 | Este artigo |


O AEM 6.5 Forms inclui vários novos recursos e melhorias que simplificam a criação, o gerenciamento e as experiências do usuário com formulários e correspondências. Para saber mais sobre todos os novos recursos e aprimoramentos do AEM 6.5 Forms, consulte [Documento de resumo dos novos recursos](../../forms/using/whats-new.md).

Você pode atualizar sua instalação existente do LiveCycle ou do AEM Forms para obter novos recursos e melhorias oferecidos no AEM 6.5 Forms e, ao mesmo tempo, manter intactos os dados, processos e ativos existentes. Na atualização, os metadados e o estado dos processos também são preservados. Você pode escolher um caminho de atualização para começar a atualizar.

O diagrama a seguir exibe os caminhos de atualização disponíveis para o AEM Forms no OSGi:

![Fluxo de atualização do OSGi](do-not-localize/osgi-upgrade-path.png)

Você pode executar uma atualização direta de:

* AEM 6.3 Forms no OSGi
* AEM 6.4 Forms no OSGi

Você também pode executar uma atualização multi-hop de

* AEM 6.0 Forms no OSGi
* AEM 6.1 Forms no OSGi
* AEM 6.2 Forms no OSGi

O diagrama a seguir exibe os caminhos de atualização disponíveis para o AEM Forms no JEE:

![Atualização do JEE 6.5](do-not-localize/jee-upgrade-6-5.png)


Você pode executar uma atualização direta de:

* AEM 6.3 Forms no JEE
* AEM 6.4 Forms no JEE
* AEM 6.5.x.x Forms no JEE

Você também pode executar uma atualização multi-hop de

* LiveCycle ES4 SP1
* AEM 6.0 Forms no JEE
* AEM 6.1 Forms no JEE
* AEM 6.2 Forms no JEE

O AEM 6.5.18.0 Forms no JEE fornece dois tipos de instaladores: [Instalador completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR) e [Instalador de patch](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=pt-BR).

**Instalador completo**: você pode usar o instalador completo para configurar novas instâncias do AEM Forms ou executar atualizações do AEM 6.5.x.x Forms AEM no JEE para o 6.5.18.0 Forms no JEE.

**Instalador de patch**: o instalador de patch é para clientes que já usam as versões AEM 6.5.x.x. Você pode usar o instalador de patches para atualizar para a versão mais recente do AEM Forms.

A imagem a seguir mostra cenários de uso do instalador de patch e completo.

![Instalador Completo e Instalador de Patch](/help/forms/using/assets/full-and-patch-installer.png)

Consulte o artigo [Instruções de instalação do Forms Service Pack do AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=pt-BR) para instalar o Service Pack mais recente do ambiente JEE.

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

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->


