---
title: Criação da Configuração de Exportação de Recursos Compartilhados
description: Siga esta página para saber mais sobre como exportar recursos compartilhados do Adobe Experience Manager (AEM) para upload no AEM Mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 576b4567-c7b6-4196-84e7-47e980637540
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%
---
# Criação da Configuração de Exportação de Recursos Compartilhados{#creating-shared-resources-export-configuration}

{{ue-over-mobile}}

>[!CAUTION]
>
>**Pré-requisito**:
>
>Antes de aprender a criar e modificar recursos compartilhados, consulte [Sincronização de Conteúdo](/help/mobile/mobile-ondemand-contentsync.md) para entender os conceitos básicos.

Os usuários do Adobe Experience Manager (AEM) Mobile usam a Sincronização de conteúdo para exportar conteúdo ao vivo para conteúdo estático para uso em aplicativos móveis e essa exportação ocorre quando o conteúdo é carregado para o Mobile On-Demand Services a partir do AEM Mobile.

A propriedade ***dps-exportTemplate*** mencionada na tabela acima define o caminho para as configurações de exportação do aplicativo. Defina esta propriedade para criar e modificar recursos compartilhados.

Os recursos a seguir descrevem a exportação de recursos compartilhados do AEM para upload no AEM Mobile.

Os Recursos compartilhados do HTML permitem que os artigos compartilhem recursos do HTML que, de outra forma, seriam duplicados para todos os artigos e podem incluir ícones, fontes, JavaScript e css.

A configuração de Sincronização de Conteúdo encontrada em **&lt;dps-exportTemplate>/dps-HTMLResources>** deve ser configurada para exportar todo o conteúdo e um artigo necessários para a renderização estática de propriedade no dispositivo.

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
1. Navegue até o caminho *[/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources](http://localhost:4502/crx/de/index.jsp#/etc/contentsync/templates/dps-we-unlimited-app/dps-HTMLResources)* para exibir a amostra de recursos compartilhados.

   Você pode exibir todas as propriedades necessárias para criar seus recursos compartilhados, conforme mostrado na figura abaixo:

   ![chlimage_1-145](assets/chlimage_1-145.png)

>[!NOTE]
>
>Os recursos compartilhados devem ser carregados ou exportados para o AEM Mobile On-demand Services quando qualquer um dos recursos compartilhados for alterado.
