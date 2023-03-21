---
title: Exportador JSON para serviços de conteúdo
seo-title: JSON Exporter for Content Services
description: Os Serviços de conteúdo do AEM foram criados para generalizar a descrição e a entrega de conteúdo de e para o AEM para além do foco em páginas da Web. Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente.
seo-description: AEM Content Services are designed to generalize the description and delivery of content in/from AEM beyond a focus on web pages. They provide the delivery of content to channels that are not traditional AEM web pages, using standardized methods that can be consumed by any client.
uuid: be6457b1-fa9c-4f3b-b219-01a4afc239e7
contentOwner: User
content-type: reference
topic-tags: components
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: 4c7e33ea-f2d3-4d69-b676-aeb50c610d70
exl-id: 647395c0-f392-427d-a998-e9ddf722b9f9
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 35%

---

# Exportador JSON para serviços de conteúdo{#json-exporter-for-content-services}

Os Serviços de conteúdo do AEM foram criados para generalizar a descrição e a entrega de conteúdo de e para o AEM para além do foco em páginas da Web.

Eles realizam a entrega de conteúdo para canais que não são páginas da Web tradicionais do AEM, usando métodos padronizados que podem ser consumidos por qualquer cliente. Esses canais podem incluir:

* [Aplicativos de página única](spa-walkthrough.md)
* Aplicativos nativos para dispositivos móveis
* outros canais e pontos de contato externos ao AEM

Com fragmentos de conteúdo que usam conteúdo estruturado, você pode fornecer serviços de conteúdo usando o exportador JSON para fornecer o conteúdo de qualquer página AEM no formato de modelo de dados JSON. Esse método pode ser consumido por seus próprios aplicativos.

>[!NOTE]
>
>A funcionalidade descrita aqui está disponível para todos os componentes principais desde que [versão 1.1.0 dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR).

## Exportador JSON com Componentes principais do fragmento de conteúdo {#json-exporter-with-content-fragment-core-components}

Usando o exportador JSON de AEM, você pode fornecer o conteúdo de qualquer página de AEM no formato de modelo de dados JSON. Esse método pode ser consumido por seus próprios aplicativos.

No AEM, o delivery é obtido usando o seletor `model` e `.json` extensão.

`.model.json`

1. Por exemplo, um URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en.model.json
   ```

1. Fornece conteúdo como:

   ![chlimage_1-192](assets/chlimage_1-192.png)

Como alternativa, você pode fornecer o conteúdo de um fragmento de conteúdo estruturado, direcionando-o especificamente.

Use o caminho inteiro para o fragmento (por meio do `jcr:content`); por exemplo, com um sufixo como.

`.../jcr:content/root/responsivegrid/contentfragment.model.json`

A página pode conter um único fragmento de conteúdo ou vários componentes de vários tipos. Você também pode usar mecanismos como componentes de lista para pesquisar automaticamente pelo conteúdo relevante.

* Por exemplo, um URL como:

   ```shell
   http://localhost:4502/content/we-retail/language-masters/en/manchester-airport/jcr:content/root/responsivegrid/contentfragment.model.json
   ```

* Fornece conteúdo como:

   ![chlimage_1-193](assets/chlimage_1-193.png)

   >[!NOTE]
   >
   >Você pode [adaptar seus próprios componentes](/help/sites-developing/json-exporter-components.md) para acessar e usar esses dados.

   >[!NOTE]
   >
   >Embora não seja uma implementação padrão, [vários seletores são suportados,](json-exporter-components.md#multiple-selectors) but `model` deve ser o primeiro.

### Informações adicionais {#further-information}

Consulte também:

* API HTTP de ativos

   * [API HTTP de ativos](/help/assets/mac-api-assets.md)

* Modelos sling:

   * [Modelos do Sling - Associando uma classe de modelo a um tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)

* AEM com JSON:

   * [Obter informações de página no formato JSON](/help/sites-developing/pageinfo.md)

## Documentação relacionada {#related-documentation}

Para obter mais detalhes, consulte:

* O [Tópico Fragmentos de conteúdo no guia do usuário Ativos](https://experienceleague.adobe.com/docs/experience-manager-64/assets/home.html?lang=en&amp;topic=/experience-manager/6-4/assets/morehelp/content-fragments.ug.js)

* [Modelos de fragmentos do conteúdo](/help/assets/content-fragments/content-fragments-models.md)
* [Criação com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md)
* [Ativação de exportação em JSON para um componente](/help/sites-developing/json-exporter-components.md)

* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) e [Componente do fragmento de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=en)
