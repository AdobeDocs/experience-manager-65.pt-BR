---
title: Renderização e Delivery
seo-title: Renderização e Delivery
description: 'null'
seo-description: nulo
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 8%

---


# Renderização e Delivery{#rendering-and-delivery}

>[!NOTE]
>
>A Adobe recomenda o uso do Editor de SPA para projetos que exigem renderização do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

AEM conteúdo pode ser facilmente renderizado por [Servlets padrão Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) para renderizar [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e outros formatos.

Essas renderizações predefinidas normalmente caminham pelo repositório e retornam o conteúdo como está.

AEM, via Sling, também oferece suporte ao desenvolvimento e implantação de renderizadores personalizados de sling para ter total controle do schema e conteúdo renderizados.

Os renderizadores padrão dos serviços de conteúdo preenchem a lacuna entre os Sling Defaults predefinidos e o Custom Development que permite a personalização e o controle de muitos aspectos do conteúdo renderizado sem desenvolvimento.

O diagrama a seguir mostra a renderização dos serviços de conteúdo.

![chlimage_1-15](assets/chlimage_1-15.png)

## Solicitando JSON {#requesting-json}

Use **&lt;RESOURCE.caas[.&lt;export-config>.][&lt;export-config>.] jsonto solicita JSON.**

<table>
 <tbody>
  <tr>
   <td>RECURSO</td>
   <td>um recurso de entidade em /content/entity<br /> ou <br /> um recurso de conteúdo em /content</td>
  </tr>
  <tr>
   <td>CONFIGURAÇÃO DE EXPORTAÇÃO</td>
   <td><p><strong>OPCIONAL</strong><br /> </p> <p>uma configuração de exportação encontrada em /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Se omitida, a configuração de exportação padrão será aplicada </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>recursão de profundidade </strong><br /> <br /> OPCIONAL para renderização de filhos como usado na renderização de Sling</td>
  </tr>
 </tbody>
</table>

## Criando Configurações de Exportação {#creating-export-configs}

As configurações de exportação podem ser criadas para personalizar a renderização JSON.

Você pode criar um nó de configuração em */apps/mobileapps/caas/exportConfigs.*

| Nome do nó | Nome da configuração (para o seletor de renderização) |
|---|---|
| jcr:primaryType | nt:unstructured |

A tabela a seguir mostra as propriedades das Configurações de exportação:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Padrão (se, não definido)</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td>Sequência de caracteres[]</td>
   <td>incluir tudo</td>
   <td>sling:resourceType</td>
   <td>excluir detalhes para nós com sling especificado:resourceType da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>Sequência de caracteres[]</td>
   <td>excluir nada</td>
   <td>sling:resourceType</td>
   <td>incluir detalhes somente para nós com sling especificado:resourceType da exportação JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>Sequência de caracteres[]</td>
   <td>excluir nada</td>
   <td>Prefixos de propriedade</td>
   <td>excluir propriedades que start com prefixos especificados da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>Sequência de caracteres[]</td>
   <td>excluir nada</td>
   <td>Nomes de propriedade</td>
   <td>excluir propriedades especificadas da exportação JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>Sequência de caracteres[]</td>
   <td>incluir tudo</td>
   <td>Nomes de propriedade</td>
   <td><p>se excludePropertyPrefixes definido<br />, isso inclui as propriedades especificadas, apesar de corresponder ao prefixo que está sendo excluído,</p> <p>else (excluir propriedades ignoradas) inclui somente essas propriedades</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>Sequência de caracteres[]</td>
   <td>incluir tudo</td>
   <td>nomes de filhos</td>
   <td>excluir filhos especificados da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>Sequência de caracteres[]<br /> <br /> </td>
   <td>excluir nada</td>
   <td>nomes de filhos</td>
   <td>incluir somente filhos especificados da exportação JSON, excluir outros</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>Sequência de caracteres[]<br /> <br /> </td>
   <td>renomear nada</td>
   <td>&lt;actual_property_name&gt;,&lt;replacement_property_name&gt;</td>
   <td>renomear propriedades usando substituições</td>
  </tr>
 </tbody>
</table>

### Substituições de exportação de tipo de recurso {#resource-type-export-overrides}

Crie um nó de configuração em */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:PrimaryType | nt:não estruturado |

A tabela a seguir mostra as propriedades:

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Tipo</strong></td>
   <td><strong>Padrão (se, não definido)</strong></td>
   <td><strong>Valor</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>&lt;selector_to_inc&gt;</td>
   <td>Sequência de caracteres[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Para os seguintes tipos de recursos de sling, não retorne a exportação padrão do CaaS json.<br /> Retorne uma exportação json do cliente renderizando o recurso como;<br /> &lt;resource&gt;.&lt;selector_to_inc&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurações de exportação do Content Services existentes {#existing-content-services-export-configs}

Os Serviços de conteúdo incluem duas configurações de exportação:

* padrão (nenhuma configuração especificada)
* página (para renderizar páginas do site)

#### Configuração de exportação padrão {#default-export-configuration}

A configuração de exportação padrão do Content Services será aplicada se uma configuração for especificada no URI solicitado.

&lt;resource>.caas[.&lt;depth-int>].json

<table>
 <tbody>
  <tr>
   <td><strong>Nome</strong></td>
   <td><strong>Valor</strong></td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>jcr:,sling:,cq:,oak:,pge-</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>jcr:text,text<br /> jcr:title,title<br /> jcr:description,description<br /> jcr:lastModified,lastModified<br /> cq:tags,tags<br /> cq:lastModified,lastModified</td>
  </tr>
  <tr>
   <td>includeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td> </td>
  </tr>
  <tr>
   <td>Substituições JSON Sling</td>
   <td>fundação/componentes/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuração de exportação de página {#page-export-configuration}

Essa configuração estende o padrão para incluir o agrupamento de filhos em um nó filho.

&lt;site_page>.caas.page[.&lt;depth-int>].json

### Recursos adicionais {#additional-resources}

Consulte os recursos abaixo para saber mais sobre tópicos adicionais nos Serviços de conteúdo:

* [Modelos de desenvolvimento](/help/mobile/administer-mobile-apps.md)
* [Criação de serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)
* [Administração de serviços de conteúdo](/help/mobile/developing-content-services.md)

