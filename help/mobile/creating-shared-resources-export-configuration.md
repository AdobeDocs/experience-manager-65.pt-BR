---
title: Criando Configuração de Exportação de Recursos Compartilhados
seo-title: Criando Configuração de Exportação de Recursos Compartilhados
description: Siga esta página para saber mais sobre como exportar recursos compartilhados da Adobe Experience Manager (AEM) para upload para a AEM Mobile.
seo-description: Siga esta página para saber mais sobre como exportar recursos compartilhados da Adobe Experience Manager (AEM) para upload para a AEM Mobile.
uuid: 99b8ff94-8135-4643-a15b-aa6fb91f5401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 1edf6c76-ccb1-40b6-bdf6-924f1461cd28
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Criando Configuração de Exportação de Recursos Compartilhados{#creating-shared-resources-export-configuration}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Pré-requisitos**:
>
>Antes de saber mais sobre como criar e modificar recursos compartilhados, consulte [Sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md) para entender os conceitos básicos.

Os usuários do AEM Mobile usam o Content Sync para exportar conteúdo ao vivo para conteúdo estático para uso em aplicativos móveis e essa exportação ocorre quando o conteúdo é carregado nos Mobile On-Demand Services da AEM Mobile.

A propriedade ***dps-exportTemplate*** mencionada na tabela acima define o caminho para as configurações de exportação do aplicativo. Defina essa propriedade para criar e modificar recursos compartilhados.

Os recursos a seguir descrevem como exportar recursos compartilhados da Adobe Experience Manager (AEM) para upload para a AEM Mobile.

Recursos HTML compartilhados permitem que artigos compartilhem recursos HTML que, de outra forma, precisariam ser duplicados para todos os artigos e podem incluir ícones, fontes, javascript e css.

A configuração de Sincronização de conteúdo encontrada em **&lt;dps-exportTemplate>/dps-HTMLResources>** deve ser configurada para exportar todo o conteúdo necessário para a renderização estática de propriedade no dispositivo.

>[!CAUTION]
>
>Você pode executar as etapas abaixo para visualização de recursos compartilhados de amostra, somente se você tiver:
>
>* instalou o conteúdo da amostra
>* executando instância AEM
>* nenhum contexto personalizado configurado ou uma porta diferente

>



Para visualização de um recurso compartilhado de amostra, consulte as etapas abaixo:

1. Abra o CRXDE Lite no servidor AEM.
1. Navegue até esse caminho *[/etc/contentsync/models/dps-we-ilimitado-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* para visualização dos recursos compartilhados de amostra.

   Você pode visualização todas as propriedades necessárias para criar seus recursos compartilhados, conforme mostrado na figura abaixo:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Os recursos compartilhados devem ser carregados ou exportados para a AEM Mobile On-demand Services quando qualquer um dos recursos compartilhados mudar.

