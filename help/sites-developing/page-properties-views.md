---
title: Personalização de Visualizações de propriedades da página
seo-title: Personalização de Visualizações de propriedades da página
description: Cada página tem um conjunto de propriedades que podem ser editadas conforme necessário
seo-description: Cada página tem um conjunto de propriedades que podem ser editadas conforme necessário
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
translation-type: tm+mt
source-git-commit: c38c27d6f7172734f80735dd2f42cfa7bf58ad1d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---


# Personalizar Visualizações de Propriedades da Página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-authoring/editing-page-properties.md) que podem ser visualizadas e editadas pelos usuários; alguns são necessários ao criar a página (criar visualização), outros podem ser visualizados e editados (editar visualização) em um estágio posterior. Essas propriedades de página são definidas e disponibilizadas pela caixa de diálogo ( `cq:dialog`) do componente de página apropriado.

>[!CAUTION]
>
>A personalização da visualização das propriedades da página não está disponível na interface clássica.

O estado padrão para cada propriedade de página é:

* oculto na visualização de criação (por exemplo, **Assistente Criar página**)

* disponível na visualização de edição (por exemplo, **Propriedades da Visualização**)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades de nó apropriadas:

* Propriedade da página a ser disponibilizada na visualização de criação (por exemplo, **Assistente para Criar página**):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propriedade da página a ser disponibilizada na visualização de edição (por exemplo, **Visualização**/**Editar**) **opção Propriedades**):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por exemplo, consulte as configurações de campos agrupados sob **Mais títulos e Descrição** na guia **Básico** para o componente Página de base. Elas estão visíveis no assistente **Criar página**, pois `cq:showOnCreate` foi definido como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte o tutorial [Extensão das propriedades da página](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obter um guia para personalizar as propriedades da página.

## Configuração das Propriedades da Página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de sua página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, o assistente [**Criar página**](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra os campos agrupados em **Mais títulos e Descrição**. Para ocultá-los, configure:

1. Crie seu componente de página em `/apps`.
1. Crie uma substituição (usando *dif de diálogo* fornecida pela [Fusão de Recursos de Sling](/help/sites-developing/sling-resource-merger.md)) para a seção `basic` do componente de sua página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referência, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   No entanto, você ***deve*** não alterar nada no caminho `/libs`.
   Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos).
   O método recomendado para configuração e outras alterações é:
   1. Recrie o item necessário (isto é, como ele existe em `/libs`) em `/apps`
   1. Faça quaisquer alterações em `/apps`


1. Defina a propriedade `path` em `basic` para apontar para a substituição da guia básica (consulte também a próxima etapa). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Crie uma substituição da seção `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade node apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**:  `false`

   A seção **Mais títulos e Descrição** não será mais exibida no assistente **Criar página**.

>[!NOTE]
Ao configurar as propriedades da página para uso com cópias online, consulte [Configuração de bloqueios MSM nas propriedades da página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obter mais detalhes.

## Exemplo de configuração de propriedades da página {#sample-configuration-of-page-properties}

Esta amostra demonstra a técnica de diferença de diálogo de [Sling Resource Fusão](/help/sites-developing/sling-resource-merger.md); incluindo o uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Também ilustra o uso de `cq:showOnCreate` e `cq:hideOnEdit`.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-page-dialog no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
