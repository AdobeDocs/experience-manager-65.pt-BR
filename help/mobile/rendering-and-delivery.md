---
title: Renderização e entrega
description: Saiba como renderizar conteúdo do Adobe Experience Manager por meio dos Servlets padrão do Sling para renderizar o JSON e outros formatos.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
exl-id: f0c543ae-33ed-40bb-9eb7-0dc3bdea69e0
solution: Experience Manager
feature: Mobile
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 6%

---

# Renderização e entrega{#rendering-and-delivery}

{{ue-over-mobile}}

O conteúdo do Adobe Experience Manager (AEM) pode ser facilmente renderizado por meio dos [Servlets Padrão de Sling](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html) para renderizar o [JSON](https://sling.apache.org/documentation/bundles/rendering-content-default-get-servlets.html#default-json-rendering) e outros formatos.

Essas renderizações prontas para uso normalmente orientam o repositório e retornam o conteúdo como está.

O AEM, por meio do Sling, também oferece suporte ao desenvolvimento e à implantação de renderizadores de sling personalizados para assumir o controle total do esquema e do conteúdo renderizados.

Os Renderizadores padrão dos serviços de conteúdo preenchem a lacuna entre Padrões do Sling prontos para uso e Desenvolvimento personalizado, permitindo a personalização e o controle de vários aspectos do conteúdo renderizado sem desenvolvimento.

O diagrama a seguir mostra a renderização dos serviços de conteúdo.

![chlimage_1-15](assets/chlimage_1-15.png)

## Solicitação de JSON {#requesting-json}

Use **&lt;RESOURCE.caas[.&lt;EXPORT-CONFIG][.&lt;EXPORT-CONFIG].json** para solicitar JSON.

<table>
 <tbody>
  <tr>
   <td>RECURSO</td>
   <td>um recurso de entidade em /content/entities<br /> ou <br /> um recurso de conteúdo em /content</td>
  </tr>
  <tr>
   <td>EXPORT-CONFIG</td>
   <td><p><strong>OPCIONAL</strong><br /> </p> <p>uma configuração de exportação foi encontrada em /apps/mobileapps/caas/exportConfigs/EXPORT-CONFIG<br /> <br /> Se omitida, a configuração de exportação padrão será aplicada </p> </td>
  </tr>
  <tr>
   <td>DEPTH-INT</td>
   <td><strong>OPCIONAL</strong><br /> <br /> recursão de profundidade para renderização de filhos conforme usado na renderização de Sling</td>
  </tr>
 </tbody>
</table>

## Criação de configurações de exportação {#creating-export-configs}

Configurações de exportação podem ser criadas para personalizar a renderização JSON.

Você pode criar um nó de configuração em */apps/mobileapps/caas/exportConfigs.*

| Nome do nó | Nome da configuração (para renderização do seletor) |
|---|---|
| jcr:primaryType | nt:unstructured |

A tabela a seguir mostra as propriedades das Configurações de Exportação:

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
   <td>String[]</td>
   <td>incluir tudo</td>
   <td>sling:resourceType</td>
   <td>excluir detalhes de nós com sling:resourceType especificado da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeComponents</td>
   <td>String[]</td>
   <td>não excluir nada</td>
   <td>sling:resourceType</td>
   <td>inclua detalhes apenas para nós com sling:resourceType especificado da exportação JSON</td>
  </tr>
  <tr>
   <td>excludePropertyPrefixes</td>
   <td>String[]</td>
   <td>não excluir nada</td>
   <td>Prefixos de propriedade</td>
   <td>excluir propriedades que começam com prefixos especificados da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeProperties</td>
   <td>String[]</td>
   <td>não excluir nada</td>
   <td>Nomes de propriedades</td>
   <td>excluir propriedades especificadas da exportação JSON</td>
  </tr>
  <tr>
   <td>includeProperties</td>
   <td>String[]</td>
   <td>incluir tudo</td>
   <td>Nomes de propriedades</td>
   <td><p>se excludePropertyPrefixes definido como <br />, isso inclui propriedades especificadas, apesar de corresponder ao prefixo que está sendo excluído,</p> <p>else (excluir propriedades ignoradas) incluir somente estas propriedades</p> </td>
  </tr>
  <tr>
   <td>includeChildren</td>
   <td>String[]</td>
   <td>incluir tudo</td>
   <td>nomes secundários</td>
   <td>excluir filhos especificados da exportação JSON</td>
  </tr>
  <tr>
   <td>excludeChildren</td>
   <td>String[]<br /> <br /> </td>
   <td>não excluir nada</td>
   <td>nomes secundários</td>
   <td>incluir somente filhos especificados da exportação JSON, excluir outros</td>
  </tr>
  <tr>
   <td>renameProperties</td>
   <td>String[]<br /> <br /> </td>
   <td>não renomear</td>
   <td>&lt;nome_da_propriedade_real&gt;,&lt;nome_da_propriedade_de_substituição&gt;</td>
   <td>renomear propriedades usando substituições</td>
  </tr>
 </tbody>
</table>

### Sobreposições de exportação de tipo de recurso {#resource-type-export-overrides}

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
   <td>&lt;SELETOR_TO_INC&gt;</td>
   <td>String[] </td>
   <td>-</td>
   <td>sling:resourceType</td>
   <td>Para os seguintes tipos de recursos sling, não retorne a exportação json CaaS padrão.<br /> Retorne uma exportação json do cliente renderizando o recurso como;<br /> &lt;RESOURCE&gt;.&lt;SELETOR_TO_INC&gt;.json </td>
  </tr>
 </tbody>
</table>

### Configurações de exportação existentes do Content Services {#existing-content-services-export-configs}

Os Content Services incluem duas configurações de exportação:

* padrão (nenhuma configuração especificada)
* página (para renderizar páginas do site)

#### Configuração de exportação padrão {#default-export-configuration}

A configuração de exportação padrão do Content Services é aplicada se uma configuração for especificada no URI solicitado.

&lt;RESOURCE>.caas[.&lt;DEPTH-INT>].json

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
   <td>Substituições do Sling JSON</td>
   <td>foundation/components/image<br /> wcm/foundation/components/image<br /> mobileapps/caas/components/data/contentReference<br /> mobileapps/caas/components/data/assetlist</td>
  </tr>
 </tbody>
</table>

#### Configuração de exportação de página {#page-export-configuration}

Essa configuração estende o padrão para incluir o agrupamento de filhos em um nó filho.

&lt;PÁGINA_SITE>.caas.page[.&lt;DEPTH-INT>].json

### Recursos adicionais {#additional-resources}

Consulte os recursos abaixo para saber mais sobre tópicos em Serviços de conteúdo:

* [Desenvolvimento de modelos](/help/mobile/administer-mobile-apps.md)
* [Criação dos serviços de conteúdo](/help/mobile/develop-content-as-a-service.md)
* [Administração dos serviços de conteúdo](/help/mobile/developing-content-services.md)
