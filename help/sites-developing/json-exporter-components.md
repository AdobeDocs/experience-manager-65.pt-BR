---
title: Ativação de exportação em JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
exl-id: 6d127e14-767e-46ad-aaeb-0ce9dd14d553
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 6%

---

# Ativação de exportação em JSON para um componente{#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) e na estrutura [Exportador de Modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que depende de [Anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, siga estas duas etapas para ativar a exportação JSON em qualquer componente.

* [Definir um modelo do Sling para o componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anotar a interface do Modelo do Sling](#annotate-the-sling-model-interface)

## Definir um modelo do Sling para o componente {#define-a-sling-model-for-the-component}

Primeiro, um modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de Modelos Sling, consulte [Desenvolvendo exportadores de modelo Sling no AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=pt-BR).

A classe de implementação do Modelo do Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o seletor `.model` e a extensão `.json`.

Além disso, isso especifica que a classe Sling Model pode ser adaptada à interface `ComponentExporter`.

>[!NOTE]
>
>As anotações Jackson não são especificadas no nível de classe do Modelo Sling, mas no nível da interface do Modelo. Isso garante que a Exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As classes `ExporterConstants` e `ComponentExporter` vêm do pacote `com.adobe.cq.export.json`.

### Uso de vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do seletor `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

No entanto, nesse caso, o seletor `model` deve ser o primeiro e a extensão deve ser `.json`.

## Anotar a interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser considerada pela estrutura do Exportador JSON, a interface Modelo deve implementar a interface `ComponentExporter` (ou `ContainerExporter`, se houver um componente de contêiner).

A interface do Modelo Sling correspondente ( `MyComponent`) seria então anotada usando [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como ela deve ser exportada (serializada).

A interface do modelo deve ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura usual para getters são serializados e derivam os nomes de propriedade JSON naturalmente dos nomes de getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

Os Componentes Principais têm suporte para exportação JSON desde a versão [1.1.0 dos componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e podem ser usados como referência.

Para obter um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-core-wcm-components no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentação relacionada {#related-documentation}

Para obter mais detalhes, consulte o seguinte:

* O [tópico Fragmentos de conteúdo no guia do usuário do Assets](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md)
* [Exportador JSON para serviços de conteúdo](/help/sites-developing/json-exporter.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e o [componente de Fragmento de Conteúdo](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)
