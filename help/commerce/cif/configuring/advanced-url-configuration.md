---
title: Configurações avançadas de URL
description: Saiba como personalizar os URLs das páginas de produto e categoria. Isso permite que as implementações otimizem URLs para mecanismos de pesquisa e promovam a descoberta.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Estrutura de integração de comércio
kt: 4933
thumbnail: 34350.jpg
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 88%

---

# Configurações avançadas de URL {#url}

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem configurações avançadas para personalizar os URLs das páginas de produto e categoria. Muitas implementações personalizam esses URLs para fins de otimização de mecanismo de pesquisa (SEO). O vídeo a seguir mostra detalhes sobre como configurar o serviço `UrlProvider` e os recursos do [Mapeamento do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o serviço `UrlProvider` de acordo com os requisitos e necessidades de SEO, o projeto deve fornecer uma configuração OSGI para a &quot;Configuração do provedor de URL da CIF&quot; e configurar o serviço conforme descrito abaixo.

>[!NOTE]
>
> O projeto da [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) inclui configurações de exemplo para demonstrar o uso de URLs personalizados para páginas de produto e categoria.

### Modelo de URL da página do produto {#product}

O modelo configura os URLs das páginas de produto com as seguintes propriedades:

* **Modelo de URL do produto**: define o formato de URLs com um conjunto de espaços reservados. O valor padrão é `{{page}}.{{url_key}}.html#{{variant_sku}}`, o que acaba gerando URLs como `/content/venia/us/en/products/product-page.chaz-kangeroo-hoodie.html#MH01-M-Orange`, em que
   * `{{page}}` foi substituída por `/content/venia/us/en/products/product-page`
   * `{{url_key}}` foi substituída pela propriedade `url_key` do produto da Magento, neste caso `chaz-kangeroo-hoodie`
   * `{{variant_sku}}` foi substituída pela variante selecionada no momento, neste caso `MH01-M-Orange`
* **Localização do identificador de produto**: define o local do identificador que será usado para buscar os dados do produto. O valor padrão é `SELECTOR`, o outro valor possível é `SUFFIX`. Com o URL de exemplo anterior, o identificador `chaz-kangeroo-hoodie` será usado para buscar os dados do produto.
* **Tipo de identificador de produto**: define o tipo do identificador que será usado ao buscar os dados do produto. O valor padrão é `URL_KEY`, o outro valor possível é `SKU`. Com o URL de exemplo anterior, os dados do produto serão obtidos com um filtro GraphQL da Magento, como `filter:{url_key:{eq:"chaz-kangeroo-hoodie"}}`.

### Modelo de URL da página da lista de produtos {#product-list}

O modelo configura os URLs das páginas de categoria ou lista de produtos com as seguintes propriedades:

* **Modelo de URL de categoria**: define o formato de URLs com um conjunto de espaços reservados. O valor padrão é `{{page}}.{{id}}.html`, o que acaba gerando URLs como `/content/venia/us/en/products/category-page.3.html`, em que
   * `{{page}}` foi substituída por `/content/venia/us/en/products/category-page`
   * `{{id}}` foi substituída pela propriedade `id` da categoria da Magento, neste caso `3`
* **Localização do identificador de categoria**: define o local do identificador que será usado para buscar os dados do produto. O valor padrão é `SELECTOR`, o outro valor possível é `SUFFIX`. Com o URL de exemplo anterior, o identificador `3` será usado para buscar os dados do produto.
* **Tipo de identificador de categoria**: define o tipo do identificador que será usado ao buscar os dados do produto. O valor padrão e compatível no momento é `ID`. Com o URL de exemplo anterior, os dados da categoria serão obtidos com um filtro GraphQL da Magento, como `category(id:3)`.

É possível adicionar propriedades personalizadas para cada modelo, desde que os dados correspondentes estejam sendo definidos pelos componentes que usam o `UrlProvider`. Verifique, por exemplo, o código da classe `ProductListItemImpl` para descobrir como ele é implementado.

Também é possível substituir o serviço `UrlProvider` por um serviço OSGi totalmente personalizado. Nesse caso, é necessário implementar a interface `UrlProvider` e registrá-la com uma classificação de serviço mais alta para substituir a implementação padrão.

## Combinar com Mapeamentos do Sling {#sling-mapping}

Além do `UrlProvider`, também é possível configurar os [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para substituir e processar URLs. O Arquétipo do AEM também fornece [um exemplo de configuração](https://github.com/adobe/aem-cif-project-archetype/tree/master/src/main/archetype/samplecontent/src/main/content/jcr_root/etc/map.publish) para definir alguns Mapeamentos do Sling para as portas 4503 (Publish) e 80 (Dispatcher).

## Combinar com o AEM Dispatcher {#dispatcher}

As substituições de URL também podem ser obtidas usando o servidor HTTP do AEM Dispatcher com o módulo `mod_rewrite`. O [Arquétipo de projeto do AEM](https://github.com/adobe/aem-project-archetype) fornece uma configuração de referência do AEM Dispatcher que já inclui [regras de substituição](https://github.com/adobe/aem-project-archetype/tree/master/src/main/archetype/dispatcher.cloud) básicas para o tamanho gerado.

## Exemplo

O projeto da [loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia) inclui configurações de exemplo para demonstrar o uso de URLs personalizados para páginas de produto e categoria. Isso permite que cada projeto configure padrões de URL individuais para páginas de produto e categoria de acordo com suas necessidades de SEO. Usa-se uma combinação do `UrlProvider` da CIF e os Mapeamentos do Sling conforme descrito acima.

>[!NOTE]
>
>Essa configuração deve ser ajustada com o domínio externo usado pelo projeto. Os Mapeamentos do Sling estão funcionando com base no nome do host e no domínio. Portanto, essa configuração é desativada por padrão e deve ser ativada antes da implantação. Para fazer isso, renomeie a pasta `hostname.adobeaemcloud.com` do Mapeamento do Sling em `ui.content/src/main/content/jcr_root/etc/map.publish/https` de acordo com o nome de domínio usado e ative essa configuração adicionando `resource.resolver.map.location="/etc/map.publish"` à configuração `JcrResourceResolver` do projeto.

## Recursos adicionais

* [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia)
* [Mapeamento de recursos do AEM](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/resource-mapping.html)
* [Mapeamentos do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html)
