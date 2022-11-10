---
title: Configurar sua página para a edição de itens em massa das propriedades da página
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: A edição em massa das propriedades da página permite editar as propriedades de várias páginas de uma só vez
seo-description: Bulk editing of page properties allows you to edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 7%

---

# Configurar sua página para a edição de itens em massa das propriedades da página {#configuring-your-page-for-bulk-editing-of-page-properties}

[Edição em massa das propriedades da página](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) O permite editar as propriedades de várias páginas de uma só vez.

Devido à possibilidade de valores diferentes, as propriedades da página não são habilitadas para edição em massa como padrão. Eles devem ser explicitamente permitidos (ativados). Ao definir as propriedades da página que estarão disponíveis para a edição de itens em massa, você precisa considerar algumas implicações, como:

* Certos campos geralmente são únicos; por exemplo, um título de página. Você deve decidir se é significativo ativar esses campos para edição de itens em massa, quando um valor será aplicado.
* Determinados campos podem ter vários valores; isso precisa de representação significativa ao renderizar.

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
>A edição em massa também está disponível para Ativos. É muito semelhante, mas difere em alguns pontos. Consulte [Editar propriedades de vários ativos](/help/assets/metadata.md) para obter as informações completas. Você pode personalizar os campos no editor de Metadados em massa do Assets usando o [Editor de esquema](/help/assets/metadata-schemas.md).

## Ativar um campo {#enabling-a-field}

>[!NOTE]
>
>Determinados campos podem ter vários valores; isso precisa de representação significativa ao renderizar. Por isso, você deve ativar apenas os seguintes tipos de campo:
>
>* `/libs/granite/ui/components/foundation/form/textfield`
>* `/libs/granite/ui/components/foundation/form/textarea`
>* `/libs/granite/ui/components/foundation/form/tagspicker`
>* `/libs/granite/ui/components/foundation/form/datepicker`
>* `/libs/granite/ui/components/foundation/form/pathbrowser`
>* `/libs/granite/ui/components/foundation/form/checkbox`
>


Os campos são ativados no componente página (*not* no modelo):

1. Usar o CRXDE Lite (ou um método equivalente) para abrir o componente da página.

   Por exemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Esse exemplo assume que os Componentes principais foram instalados na instância, o que é o caso se a instância estiver em execução com conteúdo de amostra We.Retail. Consulte a [Documentação dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) para obter mais informações.

1. Navegue até o campo desejado dentro da variável `cq:dialog` definição.
1. Defina a seguinte propriedade no nó field :

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por exemplo, para a página padrão [componente base](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   A propriedade seria definida em:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Você ***must*** não altere nada no `/libs` caminho.
   >
   >Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >    1. Recrie o item necessário (ou seja, como ele existe em `/libs`) `/apps`
   >    1. Faça quaisquer alterações no `/apps`


1. Selecionar **Salvar tudo** para continuar suas atualizações.
