---
title: Uso de condições de ocultação
description: As condições de ocultação podem ser usadas para determinar se um recurso de componente é renderizado ou não.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Uso de condições de ocultação {#using-hide-conditions}

As condições de ocultação podem ser usadas para determinar se um recurso de componente é renderizado ou não. Um exemplo disso seria quando um autor de modelo configura o [componente de lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html) do Componente principal no [editor de modelos](/help/sites-authoring/templates.md) e decide desabilitar as opções para criar a lista com base em páginas secundárias. Desativar essa opção na caixa de diálogo de design define uma propriedade para que, quando o componente de lista for renderizado, a condição de ocultação seja avaliada e a opção para mostrar páginas secundárias não seja exibida.

## Visão geral {#overview}

As caixas de diálogo podem se tornar complexas com várias opções para o usuário, que pode usar apenas uma fração das opções que estão à sua disposição. Isso pode causar experiências esmagadoras na interface do usuário.

Ao usar as condições de ocultação, administradores, desenvolvedores e superusuários têm uma maneira de ocultar recursos com base em um conjunto de regras. Esse recurso permite que eles decidam quais recursos devem ser exibidos quando um autor editar o conteúdo.

>[!NOTE]
>
>Ocultar um recurso com base em uma expressão não substitui as permissões de ACL. O conteúdo permanece editável, mas não é exibido.

## Detalhes de implementação e uso {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` é responsável por filtrar os recursos com base na existência e no valor da propriedade `granite:hide`, localizada no campo a ser filtrado. A implementação de `/libs/cq/gui/components/authoring/dialog/dialog.jsp` inclui uma instância de `FilteringResourceWrapper.`

A implementação usa a [API ELResolver](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) do Granite e adiciona uma variável personalizada `cqDesign` por meio do ExpressionCustomizer.

Estes são alguns exemplos de condições de ocultação em um nó de design localizado em `etc/design` ou como uma Política de Conteúdo.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

Ao definir a expressão ocultar, lembre-se do seguinte:

* Para ser válido, o escopo no qual a propriedade é encontrada deve ser expresso (por exemplo, `cqDesign.myProperty`).
* Os valores são somente leitura.
* As funções (se necessário) devem ser limitadas a um determinado conjunto fornecido pelo serviço.

## Exemplo {#example}

Exemplos de condições de ocultação podem ser encontrados no AEM e nos [componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) em particular. Por exemplo, considere o [componente principal da lista](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html).

[Usando o editor de modelo](/help/sites-authoring/templates.md), o autor do modelo pode definir na caixa de diálogo de design quais opções do componente de lista estão disponíveis para o autor da página. É possível ativar ou desativar opções como permitir que a lista seja uma lista estática, uma lista de páginas secundárias, uma lista de páginas marcadas e assim por diante.

Se um autor do modelo optar por desativar a opção de páginas secundárias, uma propriedade de design será definida e uma condição de ocultação será avaliada em relação a ela, o que faz com que a opção não seja renderizada para o autor da página.

1. Por padrão, o autor da página pode usar o componente principal da lista para criar uma lista usando páginas secundárias ao escolher a opção **Páginas secundárias**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. Na caixa de diálogo de design do componente principal da lista, o autor do modelo pode escolher a opção **Desativar secundárias** para impedir que a opção para gerar uma lista com base em páginas secundárias seja exibida ao autor da página.

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. Um nó de política foi criado em `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` com uma propriedade `disableChildren` definida como `true`.
1. A condição de ocultação é definida como o valor de uma propriedade `granite:hide` no nó de propriedade de diálogo `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. O valor de `disableChildren` é extraído da configuração de design e a expressão `${cqDesign.disableChildren}` é avaliada como `false`, o que significa que a opção não será renderizada como parte do componente.

   Você pode exibir a expressão hide como o valor da propriedade `granite:hide` [no GitHub aqui](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. A opção **Páginas secundárias** não é mais renderizada para o autor da página ao usar o componente de lista.

   ![chlimage_1-221](assets/chlimage_1-221.png)
