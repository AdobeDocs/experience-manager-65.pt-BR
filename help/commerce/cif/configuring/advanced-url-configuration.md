---
title: Configurações avançadas de URL
description: Saiba como personalizar os URLs das páginas de produto e categoria. Isso permite que as implementações otimizem URLs para mecanismos de pesquisa e promovam a descoberta.
sub-product: Commerce
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 4933
thumbnail: 34350.jpg
exl-id: 0125021a-1c00-4ea3-b7fb-1533b7b9f4f2
source-git-commit: a5f3e33a6abe7ac1bbd610a8528fd599d1ffd2aa
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 35%

---

# Configurações avançadas de URL {#url}

>[!NOTE]
>
>A Otimização do mecanismo de pesquisa (SEO) se tornou uma preocupação principal para muitos comerciantes. Por conseguinte, é necessário dar resposta às preocupações relativas às SEO em muitos projetos AEM. Leia [Práticas recomendadas de gerenciamento de SEO e URL](https://experienceleague.adobe.com/docs/experience-manager-65/managing/managing-further-reference/seo-and-url-management.html) para obter mais informações.

Os [Componentes principais da CIF do AEM](https://github.com/adobe/aem-core-cif-components) fornecem configurações avançadas para personalizar os URLs das páginas de produto e categoria. Muitas implementações personalizam esses URLs para fins de otimização de mecanismo de pesquisa (SEO). O vídeo a seguir mostra detalhes sobre como configurar o serviço `UrlProvider` e os recursos do [Mapeamento do Sling](https://sling.apache.org/documentation/the-sling-engine/mappings-for-resource-resolution.html) para personalizar os URLs das páginas de produto e categoria.

>[!VIDEO](https://video.tv.adobe.com/v/34350/?quality=12)

## Configuração {#configuration}

Para configurar o `UrlProvider` de acordo com os requisitos e necessidades de SEO, um projeto deve fornecer uma configuração OSGI para a &quot;Configuração do provedor de URL da CIF&quot;.

>[!NOTE]
>
>Desde a versão 2.0.0 dos Componentes principais da CIF do AEM, a configuração do Provedor de URL fornece apenas formatos de url predefinidos, em vez dos formatos configuráveis de texto livre conhecidos das versões 1.x. Além disso, o uso de seletores para transmitir dados em URLs foi substituído por sufixos.

### Formato de URL da página do produto {#product}

Isso configura os URLs das páginas do produto e oferece suporte às seguintes opções:

* `{{page}}.html/{{sku}}.html#{{variant_sku}}` (default)
* `{{page}}.html/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_key}}.html#{{variant_sku}}`
* `{{page}}.html/{{url_path}}.html#{{variant_sku}}`
* `{{page}}.html/{{sku}}/{{url_path}}.html#{{variant_sku}}`

No caso de [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` será substituída por `/content/venia/us/en/products/product-page`
* `{{sku}}` será substituído pelo SKU do produto, por exemplo `VP09`
* `{{url_key}}` será substituído pelo `url_key` propriedade, por exemplo `lenora-crochet-shorts`
* `{{url_path}}` será substituído pelo `url_path`, por exemplo `venia-bottoms/venia-pants/lenora-crochet-shorts`
* `{{variant_sku}}` será substituída pela variante selecionada no momento, por exemplo, `VP09-KH-S`

Como a variável `url_path` Se for descontinuado, os formatos de URL de produto predefinidos usarão `url_rewrites` e escolha aquele com os segmentos de caminho mais alternativos se a variável `url_path` não está disponível.

Com os dados de exemplo acima, um URL de variante de produto formatado usando o formato de URL padrão será semelhante `/content/venia/us/en/products/product-page.html/VP09.html#VP09-KH-S`.

### Formato de URL da página de categoria {#product-list}

Isso configura os URLs das páginas de categoria ou lista de produtos e oferece suporte às seguintes opções:

* `{{page}}.html/{{url_path}}.html` (padrão)
* `{{page}}.html/{{url_key}}.html`

No caso de [Loja de referência Venia](https://github.com/adobe/aem-cif-guides-venia):

* `{{page}}` será substituída por `/content/venia/us/en/products/category-page`
* `{{url_key}}` será substituído por `url_key` propriedade
* `{{url_path}}` será substituído por `url_path`

Com os dados de exemplo acima, um URL de página de categoria formatado usando o formato de URL padrão terá a aparência `/content/venia/us/en/products/category-page.html/venia-bottoms/venia-pants.html`.

>[!NOTE]
> 
>O `url_path` é uma concatenação do `url_keys` dos ancestrais de um produto ou categoria e do produto ou categoria `url_key` separados por `/` barra.

### Páginas específicas de categoria/produto {#specific-pages}

É possível criar [várias páginas de categoria e produto](multi-template-usage.md) para apenas um subconjunto específico de categorias ou produtos de um catálogo.

O `UrlProvider` é pré-configurado para gerar deep links para essas páginas em instâncias da camada de criação. Isso é útil para editores que navegam em um site usando o modo de Visualização, navegam até uma página de produto ou categoria específica e alternam de volta para o modo de Edição para editar a página.

Por outro lado, em instâncias de nível de publicação, urls de página de catálogo devem ser mantidas estáveis para não perder ganhos nas classificações do mecanismo de pesquisa, por exemplo. Devido a essa situação, as instâncias de camada de publicação não renderizarão deep links para páginas de catálogo específicas por padrão. Para alterar esse comportamento, a variável _Estratégia da página específica do provedor de URL da CIF_ pode ser configurado para sempre gerar urls de página específicos.

## Formatos de URL personalizados {#custom-url-format}

Para fornecer um formato de URL personalizado, um projeto pode implementar [`ProductUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/ProductUrlFormat.html) ou [`CategoryUrlFormat`](https://javadoc.io/doc/com.adobe.commerce.cif/core-cif-components-core/latest/com/adobe/cq/commerce/core/components/services/urls/CategoryUrlFormat.html) e registre a implementação como serviço OSGI. Essas implementações, se disponíveis, substituirão o formato configurado e predefinido. Se houver várias implementações registradas, aquela com a classificação de serviço mais alta substitui aquela(s) pela classificação de serviço mais baixa.

As implementações de formato de URL personalizado devem implementar um par de métodos para criar um URL a partir de determinados parâmetros e para analisar um URL para retornar os mesmos parâmetros, respectivamente.

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
