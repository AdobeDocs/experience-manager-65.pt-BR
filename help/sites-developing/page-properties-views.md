---
title: Personalização de exibições das propriedades da página
description: Cada página tem um conjunto de propriedades que podem ser editadas conforme necessário
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 292874bf-2ee6-4638-937c-f8f26c93ca65
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 0%

---

# Personalização de exibições das propriedades da página{#customizing-views-of-page-properties}

Cada página tem um conjunto de [propriedades](/help/sites-authoring/editing-page-properties.md) que podem ser visualizadas e editadas pelos usuários. Algumas são necessárias ao criar a página (criar exibição), outras podem ser visualizadas e editadas (editar exibição) em um estágio posterior. Essas propriedades de página são definidas e disponibilizadas pela caixa de diálogo ( `cq:dialog`) do componente de página apropriado.

>[!CAUTION]
>
>A personalização da visualização das propriedades da página não está disponível na interface clássica.

O estado padrão de cada propriedade de página é:

* oculto na exibição de criação (por exemplo, assistente **Criar página**)

* disponível no modo de edição (por exemplo, **Propriedades do Modo de Exibição**)

Os campos devem ser configurados especificamente se qualquer alteração for necessária. Isso é feito usando as propriedades apropriadas do nó:

* Propriedade da página a ser disponibilizada no modo de exibição de criação (por exemplo, assistente **Criar Página**):

   * Nome: `cq:showOnCreate`
   * Tipo: `Boolean`

* Propriedade da página a ser disponibilizada no modo de edição (por exemplo, **Modo de Exibição**/**Editar**) **Propriedades** opção):

   * Nome: `cq:hideOnEdit`
   * Tipo: `Boolean`

Por exemplo, consulte as configurações para campos agrupados em **Mais Títulos e Descrição** na guia **Básico** para o componente de Página de base. Estes estão visíveis no assistente **Criar página**, pois `cq:showOnCreate` foi definido como `true`:

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/moretitles
```

>[!TIP]
>
>Consulte o [tutorial Extensão das propriedades de página](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/page-properties-technical-video-develop.html?lang=pt-BR) para obter um guia sobre como personalizar as propriedades de página.

## Configuração das propriedades da página {#configuring-your-page-properties}

Você também pode configurar os campos disponíveis configurando a caixa de diálogo do componente de página e aplicando as propriedades de nó apropriadas.

Por exemplo, por padrão, o assistente [**Criar página**](/help/sites-authoring/managing-pages.md#creating-a-new-page) mostra os campos agrupados em **Mais títulos e descrições**. Para ocultá-los, você configura:

1. Crie seu componente de página em `/apps`.
1. Crie uma substituição (usando a *diff de caixa de diálogo* fornecida pelo [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md)) para a seção `basic` do seu componente de página; por exemplo:

   ```xml
   <your-page-component>/cq:dialog/content/items/tabs/items/basic
   ```

   >[!NOTE]
   >
   >Como referência, consulte:
   >
   >    `/libs/wcm/foundation/components/basicpage/v1/basicpage/cq:dialog`
   >
   >No entanto, você ***deve*** não alterar nada no caminho `/libs`.
   >
   >Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >1. Recriar o item necessário (isto é, como ele existe em `/libs`) em `/apps`
   >1. Fazer alterações em `/apps`

1. Defina a propriedade `path` em `basic` para apontar para a substituição da guia básica (veja a próxima etapa também). Por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic
   ```

1. Crie uma substituição da seção `basic` - `moretitles` no caminho correspondente; por exemplo:

   ```xml
   /apps/demos/components/page/tabs/basic/items/column/items/moretitles
   ```

1. Aplique a propriedade do nó apropriada:

   * **Nome**: `cq:showOnCreate`
   * **Tipo**: `Boolean`
   * **Valor**: `false`

   A seção **Mais Títulos e Descrição** não será mais exibida no assistente **Criar Página**.

>[!NOTE]
>
>Ao configurar propriedades de página para uso com live copies, consulte [Configurando Bloqueios do MSM nas Propriedades da Página](/help/sites-developing/extending-msm.md#configuring-msm-locks-on-page-properties-touch-enabled-ui) para obter mais detalhes.

## Exemplo de configuração das propriedades da página {#sample-configuration-of-page-properties}

Esta amostra demonstra a técnica de diálogo diff do [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md); incluindo o uso de [`sling:orderBefore`](/help/sites-developing/sling-resource-merger.md#properties). Também ilustra o uso de `cq:showOnCreate` e `cq:hideOnEdit`.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-page-dialog no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-page-dialog)
