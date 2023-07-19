---
title: Personalização de exibições das propriedades da página
seo-title: Customizing Views of Page Properties
description: Cada página tem um conjunto de propriedades que podem ser editadas conforme necessário
seo-description: Every page has a set of properties that you can edit as required
uuid: cbfca6e6-cb9e-43b1-8889-09a7cc9f8a51
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6f8e08d1-831e-441a-ad1a-f5c8788f32d7
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 1%

---

# Personalização de exibições das propriedades da página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-authoring/editing-page-properties.md) que podem ser visualizadas e editadas pelos usuários; algumas são necessárias ao criar a página (criar visualização), outras podem ser visualizadas e editadas (editar visualização) em um estágio posterior. Essas propriedades da página são definidas e disponibilizadas pela caixa de diálogo ( `cq:dialog`) do componente de página apropriado.

>[!CAUTION]
>
>A personalização da visualização das propriedades da página não está disponível na interface clássica.

O estado padrão de cada propriedade de página é:

* oculto na visualização criar (por exemplo, **Criar página** assistente)

* disponível na visualização de edição (por exemplo, **Propriedades da exibição**)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades apropriadas do nó:

* A propriedade da página que estará disponível na visualização de criação (por exemplo, **Criar página** assistente):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* A propriedade da página que estará disponível na visualização de edição (por exemplo, **Exibir**/**Editar**) **Propriedades** opção):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por exemplo, consulte as configurações para campos agrupados na **Mais títulos e descrições** no **Básico** para o componente de página de base. Eles são visíveis na **Criar página** assistente como `cq:showOnCreate` foi definido como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte a [Tutorial de extensão das propriedades da página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html) para obter um guia sobre como personalizar as propriedades da página.

## Configuração das propriedades da página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, a variável [**Criar página** assistente](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra os campos agrupados em **Mais títulos e descrições**. Para ocultá-los, você configura:

1. Crie seu componente de página em `/apps`.
1. Criar uma substituição (usando *diff da caixa de diálogo* fornecido pelo [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md)) para o `basic` do seu componente de página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referência, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   No entanto, você ***deve*** não alterar nada no `/libs` caminho.
   >
   Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).
   >
   O método recomendado para configuração e outras alterações é:
   >
   1. Recriar o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
   1. Fazer alterações em `/apps`

1. Defina o `path` propriedade em `basic` para apontar para a substituição da guia básica (consulte a próxima etapa também). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Criar uma substituição de `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade do nó apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   A variável **Mais títulos e descrições** A seção não será mais exibida na **Criar página** assistente.

>[!NOTE]
>
Ao configurar propriedades de página para uso com live copies, consulte [Configuração de bloqueios do MSM nas propriedades da página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obter mais detalhes.

## Exemplo de configuração das propriedades da página {#sample-configuration-of-page-properties}

Esta amostra demonstra a técnica de diálogo diff do [Fusão de recursos do Sling](/help/sites-developing/sling-resource-merger.md)incluindo a utilização de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Ilustra igualmente a utilização de `cq:showOnCreate` e `cq:hideOnEdit`.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-page-dialog no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
