---
title: Fragmentos de conteúdo configuram componentes para renderização
seo-title: Fragmentos de conteúdo configuram componentes para renderização
description: Fragmentos de conteúdo configuram componentes para renderização
seo-description: Fragmentos de conteúdo configuram componentes para renderização
uuid: 3f5aaf36-e6a7-4a3c-b305-e35ebcc98d0d
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 2aef9048-9d6e-4f5d-b443-5e73f8066d76
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 9%

---


# Fragmentos de conteúdo configuram componentes para renderização{#content-fragments-configuring-components-for-rendering}

Há vários [serviços avançados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) relacionados à renderização de fragmentos de conteúdo. Para usar esses serviços, os tipos de recursos desses componentes devem se tornar conhecidos pela estrutura de fragmentos de conteúdo.

Isso é feito configurando o [Serviço OSGi - Configuração do componente de fragmento de conteúdo](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Se você não precisar dos [serviços avançados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) descritos abaixo, poderá ignorar esta configuração.

>[!CAUTION]
>
>Ao estender ou usar os componentes predefinidos, não é recomendável alterar a configuração.

>[!CAUTION]
>
>Você pode gravar um componente do zero que usa somente a API Fragmentos de conteúdo, sem serviços avançados. No entanto, nesse caso, você terá que desenvolver seu componente para que ele lide com o processamento apropriado.
>
>Portanto, é recomendável usar os componentes principais.

## Definição dos Serviços Avançados que precisam de Configuração {#definition-of-advanced-services-that-need-configuration}

Os serviços que exigem o registro de um componente são:

* Determinar as dependências corretamente durante a publicação (isto é, garantir que os fragmentos e modelos possam ser publicados automaticamente com uma página se tiverem sido alterados desde a última publicação).
* Suporte para fragmentos de conteúdo na pesquisa de texto completo.
* O gerenciamento/tratamento de *conteúdo intermediário.*
* O gerenciamento de *ativos de mídia mista.*
* O Dispatcher libera fragmentos referenciados (se uma página que contém um fragmento for republicada).
* Uso de renderização baseada em parágrafo.

Se você precisar de um ou mais desses recursos, então (normalmente) é mais fácil usar a funcionalidade predefinida, em vez de desenvolvê-la do zero.

## Serviço OSGi - Configuração do componente de fragmento de conteúdo {#osgi-service-content-fragment-component-configuration}

A configuração precisa estar vinculada ao serviço OSGi **Configuração do componente de fragmento de conteúdo**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configurando o OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes.

Por exemplo:

![cfm-01](assets/cfm-01.png)

A configuração do OSGi é:

<table>
 <tbody>
  <tr>
   <td>Etiqueta</td>
   <td>Configuração do OSGi<br /> </td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><strong>Tipo de recurso</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>O tipo de recurso a ser registrado; por exemplo, <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Propriedade de referência</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>O nome da propriedade que contém a referência ao fragmento; por exemplo, <code>fragmentPath</code> ou <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade do(s) elemento(s)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>O nome da propriedade que contém os nomes dos elementos a serem renderizados; por exemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade de variação</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>O nome da propriedade que contém o nome da variação a ser renderizada; por exemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algumas funcionalidades (por exemplo, para renderizar apenas um intervalo de parágrafos), você terá que aderir a algumas convenções:

<table>
 <tbody>
  <tr>
   <td>Nome da Propriedade</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Uma propriedade de string que define o intervalo de parágrafos a serem enviados se estiver em <em>modo de renderização de elemento único</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code></li>
     <li>avaliado somente se <code>paragraphScope</code> estiver definido como <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Uma propriedade de string que define como os parágrafos devem ser exibidos se em <em>modo de renderização de elemento único</em>.</p> <p>Valores:</p>
    <ul>
     <li><code>all</code> : para renderizar todos os parágrafos</li>
     <li><code>range</code> : para renderizar o intervalo de parágrafos fornecido por <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>Uma propriedade booleana que define se os cabeçalhos (por exemplo, <code>h1</code>, <code>h2</code>, <code>h3</code>) são contados como parágrafos (<code>true</code>) ou não (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

>[!CAUTION]
>
>Isso pode mudar em mais de 6,5 marcos.

## Exemplo {#example}

Como exemplo, consulte o seguinte (em uma instância AEM predefinida):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Ele contém:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```

