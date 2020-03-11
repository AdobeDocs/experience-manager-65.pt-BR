---
title: Renderização e entrega
seo-title: Renderização e entrega
description: 'null'
seo-description: 'null'
uuid: 1253b6a5-6bf3-42b1-be3a-efa23b6ddb51
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 672d5b1e-6b2f-4afe-ab04-c398e5ef45d5
translation-type: tm+mt
source-git-commit: 7eb3529de1c99d09eaa78c7589320a85e729400b

---


# Renderização e entrega{#rendering-and-delivery}

>[!NOTE]
>
>A Adobe recomenda usar o Editor SPA para projetos que exigem renderização do lado do cliente baseada em estrutura de aplicativo de página única (por exemplo, Reagir). [Saiba mais](/help/sites-developing/spa-overview.md).

O conteúdo do AEM pode ser facilmente renderizado por meio de Servlets [padrão](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) Sling para renderizar [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e outros formatos.

Essas renderizações predefinidas normalmente caminham pelo repositório e retornam o conteúdo como está.

O AEM, via Sling, também oferece suporte ao desenvolvimento e implantação de renderizadores de sling personalizados para ter total controle do esquema renderizado e do conteúdo.

Os renderizadores padrão dos serviços de conteúdo preenchem a lacuna entre os Sling Defaults predefinidos e o Custom Development que permite a personalização e o controle de muitos aspectos do conteúdo renderizado sem desenvolvimento.

O diagrama a seguir mostra a renderização dos serviços de conteúdo.

![chlimage_1-15](assets/chlimage_1-15.png)

## Solicitando JSON {#requesting-json}

Use **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** para solicitar JSON.

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
   <td><strong>recursão de profundidade OPCIONAL</strong><br /> <br /> para renderização de filhos como usado na renderização de Sling</td>
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
   <td>excluir propriedades que começam com prefixos especificados da exportação JSON</td>
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
   <td><p>se excludePropertyPrefixes definir<br /> , isso inclui propriedades especificadas apesar de corresponder ao prefixo que está sendo excluído,</p> <p>else (excluir propriedades ignoradas) inclui somente essas propriedades</p> </td>
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
   <td>&lt;nome_propriedade_real&gt;,&lt;nome_propriedade_substituta&gt;</td>
   <td>renomear propriedades usando substituições</td>
  </tr>
 </tbody>
</table>

### Substituições de exportação de tipo de recurso {#resource-type-export-overrides}

Crie um nó de configuração em */apps/mobileapps/caas/exportConfigs.*

| name | resourceTypeOverrides |
|---|---|
| jcr:primaryType | nt:unstructured |

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
   <td>&lt;SELECTOR_TO_INC&gt;</td>
   <td>Sequência de caracteres[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Para os seguintes tipos de recursos de sling, não retorne a exportação padrão do CaaS json.<br /> Devolver uma exportação json do cliente ao apresentar o recurso como;<br /> &lt;RECURSO&gt;.&lt;SELECTOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurações de exportação dos serviços de conteúdo existentes {#existing-content-services-export-configs}

Os Serviços de conteúdo incluem duas configurações de exportação:

* padrão (nenhuma configuração especificada)
* página (para renderizar páginas do site)

#### Configuração de exportação padrão {#default-export-configuration}

A configuração de exportação padrão do Content Services será aplicada se uma configuração for especificada no URI solicitado.

&lt;RECURSO>.caas[.&lt;DEPTH-INT>].json

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
   <td>fundação/componentes/imagem<br /> wcm/fundação/componentes/imagem<br /> mobileapps/caas/components/data/contentReferência<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuração de exportação de página {#page-export-configuration}

Essa configuração estende o padrão para incluir o agrupamento de filhos em um nó filho.

&lt;SITE_PAGE>.caas.page[.&lt;DEPTH-INT>].json

### Additional Resources {#additional-resources}

Consulte os recursos abaixo para saber mais sobre tópicos adicionais nos Serviços de conteúdo:

* [Modelos de desenvolvimento](/help/mobile/administer-mobile-apps.md)
* [Criação de serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)
* [Administração de serviços de conteúdo](/help/mobile/developing-content-services.md)

