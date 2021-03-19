---
title: Pacote de Compatibilidade
seo-title: Pacote de Compatibilidade
description: A instalação do pacote Compatibilidade no AEM Forms 6.5 permite usar os ativos de Gerenciamento de correspondência do AEM Forms 6.4 e versões anteriores e modelos e páginas de formulários adaptáveis obsoletos
seo-description: A instalação do pacote Compatibilidade no AEM Forms 6.4 permite usar os ativos de Gerenciamento de correspondência do AEM Forms 6.4 e modelos e páginas de formulários adaptáveis obsoletos
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 6%

---


# Pacote de Compatibilidade{#compatibility-package}

## Visão geral {#overview}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com clientes no AEM Forms 6.5. Para continuar usando cartas no AEM Forms 6.5, é necessário instalar o [pacote de compatibilidade do AEMFD](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) mais recente.

O pacote de compatibilidade do AEMFD também permite [usar os seguintes ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Dicionários de dados
* Modelos e páginas obsoletas de formulários adaptáveis

Para obter mais informações, consulte [Ativos compatíveis com o AEM Forms 6.5 instalando o pacote de Compatibilidade](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Adicionar suporte para ativos AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Depois de executar uma atualização, faça o seguinte para instalar o pacote de compatibilidade do AEMFD e tornar seus ativos compatíveis com o 6.5:

Certifique-se de ter [AEM pacote de compatibilidade](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) pré-instalado.

1. Instale o pacote de compatibilidade mais recente 6.5 [e ](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Para obter mais informações sobre como fazer upload e instalar o pacote, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

1. Depois que os logs forem estabilizados, reinicie o servidor.
1. Use o utilitário de migração para tornar seus ativos compatíveis com a 6.5.

   Para obter mais informações, consulte [utilitário de migração](../../forms/using/migration-utility.md).

## Ativos compatíveis com o AEM Forms 6.5 ao instalar o pacote de Compatibilidade {#assetsmadecompatible}

Ao instalar o pacote de Compatibilidade, você pode tornar os seguintes ativos e modelos compatíveis com o AEM Forms 6.5:

* Ativos de gerenciamento de correspondência da AEM 6.4 e anteriores:

   * [Cartas](../../forms/using/create-letter.md)
   * [Dicionários de dados](/help/forms/using/data-dictionary.md)
   * Fragmentos do documento

* Modelos de formulário adaptável obsoleto:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Páginas obsoletas para formulários adaptáveis:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

