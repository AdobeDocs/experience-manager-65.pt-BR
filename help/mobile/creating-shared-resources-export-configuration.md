---
title: Criando Configuração de Exportação de Recursos Compartilhados
seo-title: Creating Shared Resources Export Configuration
description: Siga esta página para saber mais sobre como exportar recursos compartilhados do Adobe Experience Manager (AEM) para upload para o AEM Mobile.
seo-description: Follow this page to learn about exporting shared resources from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Criando Configuração de Exportação de Recursos Compartilhados{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>A Adobe recomenda usar o Editor de SPA para projetos que exigem renderização do lado do cliente com base em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Pré-requisitos**:
>
>Antes de saber mais sobre como criar e modificar recursos compartilhados, consulte [Sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md) para compreender os conceitos básicos.

Os usuários do AEM Mobile usam a Sincronização de conteúdo para exportar conteúdo ao vivo para conteúdo estático, para uso em aplicativos móveis, e essa exportação ocorre quando o conteúdo é carregado nos Mobile On-Demand Services da AEM Mobile.

A propriedade ***dps-exportTemplate*** mencionado na tabela acima, define o caminho para as configurações de exportação do aplicativo. Defina essa propriedade para criar e modificar recursos compartilhados.

Os recursos a seguir descrevem a exportação de recursos compartilhados do Adobe Experience Manager (AEM) para upload para o AEM Mobile.

Os Recursos de HTML compartilhados permitem que os artigos compartilhem recursos de HTML que, de outra forma, precisariam ser duplicados para todos os artigos e podem incluir ícones, fontes, javascript e css.

A configuração da Sincronização de conteúdo encontrada em **&lt;dps-exporttemplate>/dps-HTMLResources>** deve ser configurado para exportar todo o conteúdo que um artigo requer para a renderização estática da propriedade no dispositivo.

>[!CAUTION]
>
>Você pode executar as etapas abaixo para exibir os recursos compartilhados de amostra, somente se tiver:
>
>* instalado o conteúdo da amostra
>* executando AEM instância
>* sem contexto personalizado configurado ou uma porta diferente
>


Para exibir o exemplo de recurso compartilhado, consulte as etapas abaixo:

1. Abra o CRXDE Lite no servidor AEM.
1. Navegue até este caminho *[/etc/contentsync/templates/dps-we-ilimitado-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)*, para exibir a amostra de recursos compartilhados.

   Você pode exibir todas as propriedades necessárias para criar seus recursos compartilhados, conforme mostrado na figura abaixo:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Os recursos compartilhados devem ser carregados ou exportados para a AEM Mobile On-demand Services quando qualquer um dos recursos compartilhados for alterado.
