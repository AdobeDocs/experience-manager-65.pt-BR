---
title: Criação da configuração de exportação do artigo
seo-title: Creating Article Export Configuration
description: Siga esta página para saber mais sobre como exportar conteúdo do Adobe Experience Manager (AEM) para upload no AEM Mobile.
seo-description: Follow this page to learn about exporting content from Adobe Experience Manager (AEM) for upload to AEM Mobile.
uuid: 089bc15b-669e-4623-bdbb-fd9abf46e098
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: bc681589-5d46-44cd-888d-b0722a2fd006
exl-id: 5295f383-3b46-4456-9177-65de68e39a85
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Criação da configuração de exportação do artigo{#creating-article-export-configuration}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor SPA para projetos que exigem renderização no lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, React). [Saiba mais](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>**Pré-requisitos**:
>
>Antes de saber mais sobre criação e modificação de recursos compartilhados, consulte [Sincronização de conteúdo](/help/mobile/mobile-ondemand-contentsync.md) para compreender os conceitos básicos.

Os usuários do AEM Mobile usam a Sincronização de conteúdo para exportar conteúdo ao vivo para conteúdo estático para uso em aplicativos móveis e essa exportação ocorre quando o conteúdo é carregado para o Mobile On-Demand Services a partir do AEM Mobile.

A propriedade ***dps-exportTemplate*** mencionado na tabela acima, define o caminho para as configurações de exportação do aplicativo. Defina esta propriedade para criar e modificar recursos compartilhados.

Os recursos a seguir descrevem a exportação de conteúdo do Adobe Experience Manager (AEM) para upload no AEM Mobile.

Os artigos têm conteúdo que precisa ser exportado e carregado. Parte desse conteúdo pode ser compartilhada entre Artigos.

Uso [ContentSync](/help/mobile/mobile-ondemand-contentsync.md) para reunir o conteúdo e criar um ***Recursos compartilhados*** pacote.

A configuração ContentSync foi encontrada em **&lt;dps-exporttemplate>/dps-article>** O deve ser configurado para exportar todo o conteúdo e um artigo necessários para a renderização estática de propriedade no dispositivo.

>[!CAUTION]
>
>Você pode executar as etapas abaixo para exibir recursos compartilhados de amostra, somente se tiver:
>
>* instalou o conteúdo de amostra
>* execução da instância do AEM
>* nenhum contexto personalizado configurado ou uma porta diferente
>

Para exibir o recurso compartilhado de amostra, consulte as etapas abaixo:

1. Abra o CRXDE Lite no servidor AEM.
1. Navegar até este caminho [/etc/contentsync/templates/dps-we-unlimited-app/dps-article](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-article), para exibir a amostra de recursos compartilhados.

   Você pode exibir todas as propriedades necessárias para criar seus recursos compartilhados, conforme mostrado na figura abaixo:

   ![chlimage_1-134](assets/chlimage_1-134.png)

>[!NOTE]
>
>Os artigos devem ser carregados ou exportados para o AEM Mobile On-demand Services quando o conteúdo de um artigo for alterado.
