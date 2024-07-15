---
title: Pacote de compatibilidade
description: A instalação do pacote de compatibilidade no AEM Forms 6.5 permite usar os ativos do Gerenciamento de correspondências do AEM Forms 6.4 e versões anteriores, bem como modelos e páginas de formulários adaptáveis obsoletos
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Pacote de compatibilidade{#compatibility-package}

## Visão geral {#overview}

A comunicação interativa é a abordagem padrão e recomendada para criar comunicações com o cliente no AEM Forms 6.5. Para continuar usando as letras no AEM Forms 6.5, é necessário instalar o [pacote de Compatibilidade do AEMFD](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) mais recente.

O pacote de Compatibilidade do AEMFD também permite [usar os seguintes ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragmentos do documento
* Cartas
* Dicionários de dados
* Modelos e páginas obsoletas dos formulários adaptáveis

Para obter mais informações, consulte [Compatibilidade do Assets com o AEM Forms 6.5 ao instalar o pacote de Compatibilidade](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Adicionar suporte para ativos do AEM Forms 6.4, 6.3 e 6.2 no AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Depois de executar uma atualização, faça o seguinte para instalar o pacote de compatibilidade do AEMFD e tornar seus ativos compatíveis com o 6.5:

Verifique se você tem o [pacote de Compatibilidade com AEM](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) pré-instalado.

1. Instale o [Pacote de compatibilidade](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) do 6.5 mais recente.

   Para obter mais informações sobre como carregar e instalar o pacote, consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md).

1. Depois que os registros estiverem estabilizados, reinicie o servidor.
1. Use o utilitário de migração para tornar seus ativos compatíveis com o 6.5.

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

   Para obter mais informações, consulte [utilitário de migração](../../forms/using/migration-utility.md).

## O Assets tornou-se compatível com o AEM Forms 6.5 ao instalar o pacote Compatibility {#assetsmadecompatible}

Ao instalar o pacote de compatibilidade, é possível tornar os seguintes ativos e modelos compatíveis com o AEM Forms 6.5:

* Gerenciamento de correspondência Assets do AEM 6.4 e versões anteriores:

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
