---
title: Pacote de compatibilidade
seo-title: Compatibility Package
description: A instalação do pacote de compatibilidade no AEM Forms 6.5 permite usar os ativos do Gerenciamento de correspondências do AEM Forms 6.4 e versões anteriores, bem como modelos e páginas de formulários adaptáveis obsoletos
seo-description: Installing the Compatibility package on AEM Forms 6.4 allows you to use the Correspondence Management assets from AEM Forms 6.4 and deprecated adaptive forms templates and pages
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 2%

---

# Pacote de compatibilidade{#compatibility-package}

## Visão geral {#overview}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com o cliente no AEM Forms 6.5. Para continuar usando as letras no AEM Forms 6.5, é necessário instalar o mais recente [Pacote de compatibilidade do AEMFD](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

O pacote de compatibilidade do AEMFD também permite [usar os seguintes ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos do documento
* Cartas
* Dicionários de dados
* Modelos e páginas obsoletas dos formulários adaptáveis

Para obter mais informações, consulte [Os ativos são compatíveis com o AEM Forms 6.5 ao instalar o pacote de compatibilidade](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Adicionar suporte para ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Depois de executar uma atualização, faça o seguinte para instalar o pacote de compatibilidade do AEMFD e tornar seus ativos compatíveis com o 6.5:

Certifique-se de que [Pacote de compatibilidade do AEM](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) pré-instalado.

1. Instalação do 6.5 mais recente [Pacote de compatibilidade](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Para obter mais informações sobre o upload e a instalação do pacote, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

1. Depois que os registros estiverem estabilizados, reinicie o servidor.
1. Use o utilitário de migração para tornar seus ativos compatíveis com o 6.5.

   Para obter mais informações, consulte [utilitário de migração](../../forms/using/migration-utility.md).

## Os ativos são compatíveis com o AEM Forms 6.5 ao instalar o pacote de compatibilidade {#assetsmadecompatible}

Ao instalar o pacote de compatibilidade, é possível tornar os seguintes ativos e modelos compatíveis com o AEM Forms 6.5:

* Ativos do gerenciamento de correspondência do AEM 6.4 e anterior:

   * [Cartas](../../forms/using/create-letter.md)
   * [Dicionários de dados](/help/forms/using/data-dictionary.md)
   * Fragmentos do documento

* Modelos obsoletos do formulário adaptável:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Páginas obsoletas dos formulários adaptáveis:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advanced/enrollment
