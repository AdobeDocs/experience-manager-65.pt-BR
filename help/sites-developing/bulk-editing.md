---
title: Configuração da página para edição em massa das propriedades da página
seo-title: Configuração da página para edição em massa das propriedades da página
description: A edição em massa das propriedades da página permite que você edite as propriedades de várias páginas de uma só vez
seo-description: A edição em massa das propriedades da página permite que você edite as propriedades de várias páginas de uma só vez
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
translation-type: tm+mt
source-git-commit: b08149e00c418319ebacec71c56472ad4e8e1089
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 7%

---


# Configuring your Page for Bulk Editing of Page Properties {#configuring-your-page-for-bulk-editing-of-page-properties}

[A edição em massa das propriedades](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) da página permite que você edite as propriedades de várias páginas de uma só vez.

Devido à possibilidade de valores diferentes, as propriedades da página não estão habilitadas para edição em massa como padrão. Eles devem ser explicitamente permitidos (habilitados). Ao definir as propriedades da página que estarão disponíveis para a edição em massa, é necessário considerar algumas implicações, como:

* Certos campos são normalmente únicos; por exemplo, um título de página. Você deve decidir se é significativo ativar esses campos para edição em massa, quando um valor será aplicado.
* Alguns campos podem ter vários valores - isso precisa de uma representação significativa ao renderizar.

   Por exemplo, uma caixa de seleção que indica &quot;Pronto para publicação&quot;. Isso pode ter vários valores antes da edição em massa (por exemplo, pronto, em revisão, em andamento).

>[!CAUTION]
>
>A edição em massa das propriedades da página é:
>
>* Não disponível na interface clássica.
>* Não disponível para páginas em uma live copy.
>* Disponível somente para páginas com o mesmo tipo de recurso.

>



>[!NOTE]
>
>A edição em massa também está disponível para os Ativos. É muito semelhante, mas difere em alguns pontos. Consulte [Editar propriedades de vários ativos](/help/assets/metadata.md) para obter as informações completas. Você pode personalizar os campos no editor de Metadados em massa para Ativos usando o editor [de](/help/assets/metadata-schemas.md)Schemas.

## Ativação de um campo {#enabling-a-field}

>[!NOTE]
>
>Alguns campos podem ter vários valores - isso precisa de uma representação significativa ao renderizar. Por isso, você deve ativar apenas os seguintes tipos de campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`

>



Os campos são ativados no componente de página (*não* no modelo):

1. Usando o CRXDE Lite (ou um método equivalente), abra o componente de página.

   Por exemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Este exemplo presume que os Componentes principais foram instalados na instância, o que é o caso se a instância estiver sendo executada com conteúdo de amostra We.Retail. See the [Core Components documentation](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) for more information.

1. Navegue até o campo desejado dentro da `cq:dialog` definição.
1. Defina a seguinte propriedade no nó de campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por exemplo, para o componente [de](/help/sites-authoring/default-components-foundation.md)base de página padrão:

   `/libs/foundation/components/page`

   A propriedade seria definida em:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Você não ***deve*** alterar nada no `/libs` caminho.
   >
   >Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >    1. Recriar o item desejado (isto é, como ele existe em `/libs`) em `/apps`
   >    1. Faça quaisquer alterações em `/apps`


1. Selecione **Salvar tudo** para continuar suas atualizações.

