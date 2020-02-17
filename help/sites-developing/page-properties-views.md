---
title: Personalização de exibições das propriedades da página
seo-title: Personalização de exibições das propriedades da página
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

---


# Personalização de exibições das propriedades da página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-authoring/editing-page-properties.md) que podem ser visualizadas e editadas pelos usuários; alguns são necessários ao criar a página (criar exibição), outros podem ser exibidos e editados (editar exibição) em um estágio posterior. Essas propriedades de página são definidas e disponibilizadas pela caixa de diálogo ( `cq:dialog`) do componente de página apropriado.

>[!CAUTION]
>
>A visualização personalizada das propriedades da página não está disponível na interface clássica.

O estado padrão para cada propriedade de página é:

* oculto na exibição de criação (por exemplo, assistente **Criar página** )

* disponível na exibição de edição (por exemplo, Propriedades **da** exibição)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades de nó apropriadas:

* Propriedade da página a ser disponibilizada na exibição de criação (por exemplo, assistente **Criar página** ):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propriedade da página a ser disponibilizada na exibição de edição (por exemplo, **opção** Exibir **/** Editar **)** Propriedades):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por exemplo, consulte as configurações de campos agrupados sob os **Mais títulos e Descrição** na guia **Básico** para o componente Página de base. Elas estão visíveis no assistente **Criar página** , como `cq:showOnCreate` foi definido como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte o tutorial [](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) Extensão das propriedades da página para obter um guia para personalizar as propriedades da página.

## Configuração das propriedades da página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de sua página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, o assistente [**para **Criar página](/help/sites-authoring/managing-pages.md#creating-a-new-page)mostra os campos agrupados em** Mais títulos e Descrição **. Para ocultá-los, configure:

1. Crie seu componente de página em `/apps`.
1. Criar uma substituição (usando o diff *de* diálogo fornecido pela Fusão [de Recursos do](/help/sites-developing/sling-resource-merger.md)`basic` Sling) para a seção do componente de sua página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referência, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   No entanto, você não ***deve*** alterar nada no `/libs` caminho.
   Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`
   O método recomendado para configuração e outras alterações é:
   1. Recriar o item desejado (isto é, como ele existe em `/libs`) em `/apps`
   1. Faça quaisquer alterações em `/apps`


1. Defina a `path` propriedade em `basic` para apontar para a substituição da guia básica (consulte a próxima etapa também). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Criar uma substituição da seção `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade node apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`
   A seção **Mais títulos e Descrição** não será mais exibida no assistente **Criar página** .

>[!NOTE]
Ao configurar as propriedades da página para uso com cópias online, consulte [Configuração de bloqueios MSM nas propriedades](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) da página para obter mais detalhes.

## Exemplo de configuração de propriedades da página {#sample-configuration-of-page-properties}

Esta amostra demonstra a técnica de diálogo diferente da [Sling Resource Fusão](/help/sites-developing/sling-resource-merger.md); incluindo a utilização de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Ele também ilustra o uso tanto `cq:showOnCreate` quanto `cq:hideOnEdit`.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-page-dialog no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
