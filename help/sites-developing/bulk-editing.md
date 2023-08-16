---
title: Configurar sua página para edição em massa das propriedades da página
seo-title: Configuring your Page for Bulk Editing of Page Properties
description: A edição em massa das propriedades da página permite editar as propriedades de várias páginas de uma só vez
seo-description: Bulk editing of page properties lets you edit the properties of multiple pages at once
uuid: 1ad403d2-4b93-4943-ae45-74bf20705b81
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: fe61ee4b-51b6-4a6f-91d8-1c02b29cc1db
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 4%

---

# Configurar sua página para edição em massa das propriedades da página {#configuring-your-page-for-bulk-editing-of-page-properties}

[Edição em massa das propriedades da página](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) permite editar as propriedades de várias páginas de uma só vez.

Devido à possibilidade de valores diferentes, as propriedades de página não são ativadas para edição em massa como padrão. Eles devem ser explicitamente permitidos (ativados). Ao definir as propriedades de página para que estejam disponíveis para edição de itens em massa, você precisa considerar certas implicações, como:

* Determinados campos normalmente são exclusivos; por exemplo, um título de página. Você deve decidir se é significativo ativar esses campos para edição de itens em massa, quando um valor será aplicado.
* Determinados campos podem ter vários valores - isso precisa de representação significativa ao renderizar.

  Por exemplo, uma caixa de seleção indicando &quot;Pronto para publicação&quot;. Isso pode ter vários valores antes da edição em massa (por exemplo, pronto, em revisão, em andamento).

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
>A edição em massa também está disponível para o Assets. É muito semelhante, mas difere em alguns pontos. Consulte [Edição de propriedades de vários ativos](/help/assets/metadata.md) para obter informações completas. Você pode personalizar os campos no editor de metadados em massa para Ativos usando o [Editor de esquema](/help/assets/metadata-schemas.md).

## Ativar um campo {#enabling-a-field}

>[!NOTE]
>
>Determinados campos podem ter vários valores - isso precisa de representação significativa ao renderizar. Por esse motivo, você deve ativar apenas os seguintes tipos de campo:
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
   >Este exemplo presume que os Componentes principais foram instalados na instância, que é o caso se a instância estiver em execução com conteúdo de amostra We.Retail. Consulte a [Documentação dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) para obter mais informações.

1. Navegue até o campo obrigatório na `cq:dialog` definição.
1. Defina a seguinte propriedade no nó do campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por exemplo, para a página padrão [componente de fundação](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   A propriedade seria definida em:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Você ***deve*** não alterar nada no `/libs` caminho.
   >
   >Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >    1. Recriar o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
   >    1. Fazer alterações em `/apps`

1. Selecionar **Salvar tudo** para continuar com suas atualizações.
