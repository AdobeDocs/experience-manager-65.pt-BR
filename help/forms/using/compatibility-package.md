---
title: Pacote de compatibilidade
seo-title: Pacote de compatibilidade
description: A instalação do pacote de compatibilidade no AEM Forms 6.5 permite que você use os ativos de Gerenciamento de correspondência do AEM Forms 6.4 e versões anteriores e modelos e páginas de formulários adaptáveis obsoletos
seo-description: A instalação do pacote de compatibilidade no AEM Forms 6.4 permite que você use os ativos de Gerenciamento de correspondência do AEM Forms 6.4 e as páginas e modelos de formulários adaptáveis obsoletos
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 6%

---


# Pacote de compatibilidade{#compatibility-package}

## Visão geral {#overview}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com o cliente no AEM Forms 6.5. Para continuar usando letras no AEM Forms 6.5, é necessário instalar o pacote [de compatibilidade do](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)AEMFD mais recente.

O pacote Compatibilidade do AEMFD também permite [usar os seguintes ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos de documento
* Cartas
* Dicionários de dados
* Formulários adaptáveis modelos e páginas obsoletos

Para obter mais informações, consulte [Ativos compatíveis com o AEM Forms 6.5 instalando o pacote](../../forms/using/compatibility-package.md#assetsmadecompatible)Compatibilidade.

## Adicione suporte para ativos AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Após executar uma atualização, faça o seguinte para instalar o pacote de compatibilidade do AEMFD e tornar seus ativos compatíveis com o 6.5:

Verifique se você tem [AEM pacote](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) de compatibilidade pré-instalado.

1. Instale o pacote [de](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html)compatibilidade 6.5 mais recente.

   Para obter mais informações sobre como carregar e instalar o pacote, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

1. Depois que os registros estiverem estabilizados, reinicie o servidor.
1. Use o utilitário de migração para tornar seus ativos compatíveis com a versão 6.5.

   Para obter mais informações, consulte Utilitário [de](../../forms/using/migration-utility.md)migração.

## Ativos compatíveis com o AEM Forms 6.5 ao instalar o pacote de compatibilidade {#assetsmadecompatible}

Ao instalar o pacote de compatibilidade, você pode tornar os seguintes ativos e modelos compatíveis com o AEM Forms 6.5:

* Ativos do AEM 6.4 e anteriores:

   * [Cartas](../../forms/using/create-letter.md)
   * [Dicionários de dados](/help/forms/using/data-dictionary.md)
   * Fragmentos do documento

* Modelos obsoletos de formulário adaptativo:

   * /libs/fd/af/models/blankTemplate2
   * /libs/fd/af/models/simpleEnrollmentTemplate
   * /libs/fd/af/models/simpleEnrollmentTemplate2
   * /libs/fd/af/models/surveyTemplate
   * /libs/fd/af/models/surveyTemplate2
   * /libs/fd/af/models/tabbedEnrollmentTemplate
   * /libs/fd/af/models/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/models/advancedEnrollmentTemplate
   * /libs/fd/afaddon/models/advancedEnrollmentTemplate2

* Páginas obsoletas para formulários adaptativos:

   * /libs/fd/af/components/page/pesquisa
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

