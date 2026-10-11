---
title: Configurar sua página para edição em massa das propriedades da página
description: A edição em massa das propriedades da página permite editar as propriedades de várias páginas de uma só vez
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 1787e643-fc8e-40e0-8e14-97b222a7c320
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 5%
---
# Configurar sua página para edição em massa das propriedades da página {#configuring-your-page-for-bulk-editing-of-page-properties}

[A edição em massa das propriedades da página](/help/sites-authoring/editing-page-properties.md#from-the-sites-console-multiple-pages) permite editar as propriedades de várias páginas de uma só vez.

Devido à possibilidade de valores diferentes, as propriedades de página não são ativadas para edição em massa como padrão. Eles devem ser explicitamente permitidos (ativados). Ao definir as propriedades de página para que estejam disponíveis para edição de itens em massa, você precisa considerar certas implicações, como:

* Determinados campos normalmente são exclusivos; por exemplo, um título de página. Decida se é significativo ativar esses campos para edição de itens em massa, quando um valor será aplicado.
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
>A edição em massa também está disponível para o Assets. É muito semelhante, mas difere em alguns pontos. Consulte [Editando Propriedades de Várias Assets](/help/assets/metadata.md) para obter informações completas. Você pode personalizar os campos no editor de Metadados em massa do Assets usando o [editor de esquemas](/help/assets/metadata-schemas.md).

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

Campos são habilitados no componente de página (*não* no modelo):

1. Usando o CRXDE Lite (ou um método equivalente), abra o componente de página.

   Por exemplo: `/apps/core/wcm/components/page/v1/page`

   >[!NOTE]
   >
   >Este exemplo presume que os Componentes principais foram instalados na instância, que é o caso se a instância estiver em execução com conteúdo de amostra We.Retail. Consulte a [documentação dos Componentes principais](https://experienceleague.adobe.com/pt-br/docs/experience-manager-core-components/using/introduction) para obter mais informações.

1. Navegue até o campo obrigatório dentro da definição `cq:dialog`.
1. Defina a seguinte propriedade no nó do campo:

   * **Nome**: `allowBulkEdit`
   * **Tipo**: `Boolean`
   * **Valor**: `true`

   Por exemplo, para a página padrão [componente de fundação](/help/sites-authoring/default-components-foundation.md):

   `/libs/foundation/components/page`

   A propriedade seria definida em:

   `cq:dialog/content/items/tabs/items/basic/items/column/items/onofftime/items/ondate`

   >[!CAUTION]
   >
   >Você ***deve*** não alterar nada no caminho `/libs`.
   >
   >Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
   >
   >O método recomendado para configuração e outras alterações é:
   >
   >    1. Recriar o item necessário (isto é, como ele existe em `/libs`) em `/apps`
   >    1. Fazer alterações em `/apps`

1. Selecione **Salvar tudo** para manter suas atualizações.
