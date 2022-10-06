---
title: Editor de imagem
seo-title: Image Editor
description: O Editor de imagens é uma peça central de AEM e pode ser aproveitada por componentes para facilitar a manipulação de imagens por autores de conteúdo.
seo-description: The Image Editor is a core piece of AEM and can be leveraged by components to facilitate the manipulation of images by content authors.
uuid: de6ac71b-380a-4b67-b697-ac34a79a9cc4
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: components
discoiquuid: f6347492-cf48-4835-b8fd-ce9a75a09abe
exl-id: af6cf1e0-8901-4621-9f72-e791cb8d68ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 14%

---

# Editor de imagem {#image-editor}

O Editor de imagens é uma peça central de AEM e pode ser aproveitada por componentes para facilitar a manipulação de imagens por autores de conteúdo.

>[!CAUTION]
>
>Para usar os recursos do Editor de imagens descritos neste artigo, [feature pack 24267](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/featurepack/cq-6.4.0-featurepack-24267) deve ser instalado.

## Unidades relativas do mapa de imagem {#relative-units-for-image-map}

O Editor de imagens mantém as áreas do mapa de imagem como unidades absolutas e relativas. As unidades relativas são úteis quando fornecidas como atributos de dados para redimensionar dinamicamente um mapa de imagem (em relação ao tamanho da imagem) no lado do cliente em um componente de imagem responsiva.

### Propriedade imageMap {#imagemap-property}

As coordenadas do mapa de imagem são persistentes para o JCR como um `imageMap` propriedade pelo Editor de imagens. Ele tem o seguinte formato:

Os armazenamentos de propriedade mapeiam as áreas da seguinte maneira:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Exemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Suporte para imagens SVG {#support-for-svg-images}

Os Gráficos de vetor dimensionáveis (SVG) são compatíveis com o Editor de imagens.

* O arrastar e soltar um ativo SVG do DAM e fazer upload de um arquivo SVG de um sistema de arquivos local são suportados.

## Ativar plug-ins por tipo MIME {#enabling-plugins-by-mime-type}

Em determinadas situações, as ações de criação devem ser restritas para determinados tipos MIME, devido à falta de suporte no processamento do lado do servidor. Por exemplo, a edição de imagens SVG pode não ser permitida.

Os plug-ins no Editor de imagens podem ser ativados seletivamente pelo tipo MIME, definindo uma `supportedMimeTypes` no nó de configuração do plug-in individual.

### Exemplo {#example}

Como exemplo, digamos que a capacidade de cortar só deve ser permitida para imagens GIF, JPEG, PNG, WEBP e TIFF.

O `supportedMimeTypes` deve ser definida como uma string dos tipos MIME permitidos no nó de configuração do plug-in no `cq:editConfig` nó do componente de imagem.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
