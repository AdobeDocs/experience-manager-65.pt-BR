---
title: Ativando a exportação JSON para um componente
seo-title: Ativando a exportação JSON para um componente
description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
seo-description: Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.
uuid: d7cc3347-2adb-4ea5-94a4-a847a2e66d28
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 448ad337-d4bb-4603-a27b-77da93feadbd
translation-type: tm+mt
source-git-commit: a430c4de89bde3b907d342106465d3b5a7c75cc8
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 4%

---


# Ativando a exportação JSON para um componente{#enabling-json-export-for-a-component}

Os componentes podem ser adaptados para gerar a exportação JSON de seu conteúdo com base em uma estrutura de modelador.

## Visão geral {#overview}

A exportação JSON é baseada em [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) e na estrutura [Exportador de Modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que depende ela própria de [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Isso significa que o componente deve ter um Modelo Sling se precisar exportar JSON. Portanto, você precisará seguir estas duas etapas para ativar a exportação JSON em qualquer componente.

* [Definir um Modelo Sling para o componente](/help/sites-developing/json-exporter-components.md#define-a-sling-model-for-the-component)
* [Anotar na interface do Sling Model](#annotate-the-sling-model-interface)

## Definir um Modelo Sling para o Componente {#define-a-sling-model-for-the-component}

Primeiro, um Modelo Sling deve ser definido para o componente.

>[!NOTE]
>
>Para obter um exemplo de uso de Modelos Sling, consulte o artigo [Desenvolvimento de exportadores de modelos Sling em AEM](https://helpx.adobe.com/experience-manager/kt/platform-repository/using/sling-model-exporter-tutorial-develop.html).

A classe de implementação do Modelo Sling deve ser anotada com o seguinte:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Isso garante que seu componente possa ser exportado sozinho, usando o seletor `.model` e a extensão `.json`.

Além disso, isso especifica que a classe Sling Model pode ser adaptada à interface `ComponentExporter`.

>[!NOTE]
>
>As anotações Jackson geralmente não são especificadas no nível de classe do Sling Model, mas sim no nível de interface do Modelo. Isso garante que a exportação JSON seja considerada como parte da API do componente.

>[!NOTE]
>
>As classes `ExporterConstants` e `ComponentExporter` vêm do pacote `com.adobe.cq.export.json`.

### Usando vários seletores {#multiple-selectors}

Embora não seja um caso de uso padrão, é possível configurar vários seletores além do seletor `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Entretanto, nesse caso, o seletor `model` deve ser o primeiro seletor e a extensão deve ser `.json`.

## Anotar na interface do modelo Sling {#annotate-the-sling-model-interface}

Para ser tida em conta pelo quadro do Exportador JSON, a interface Model deve implementar a interface `ComponentExporter` (ou `ContainerExporter`, no caso de um componente de container).

A interface correspondente do Modelo Sling ( `MyComponent`) seria anotada usando [anotações Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir como deve ser exportada (serializada).

A interface Modelo precisa ser anotada corretamente para definir quais métodos devem ser serializados. Por padrão, todos os métodos que respeitam a convenção de nomenclatura comum para getters serão serializados e derivarão seus nomes de propriedades JSON naturalmente dos nomes do getter. Isso pode ser evitado ou substituído usando `@JsonIgnore` ou `@JsonProperty` para renomear a propriedade JSON.

## Exemplo {#example}

Os Componentes principais têm suporte para exportação JSON desde a versão [1.1.0 dos componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) e podem ser usados como referência.

Para ver um exemplo, consulte a implementação do Modelo Sling do Componente principal de imagem e sua interface anotada.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-core-wcm-components no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/archive/master.zip)

## Documentação relacionada {#related-documentation}

Para mais informações, consulte:

* O tópico [Fragmentos de conteúdo no guia do usuário Ativos](https://helpx.adobe.com/experience-manager/6-4/assets/user-guide.html?topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md)
* [Exportador JSON para serviços de conteúdo](/help/sites-developing/json-exporter.md)
* [Componentes principais ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) e o componente Fragmento  [do conteúdo](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)

