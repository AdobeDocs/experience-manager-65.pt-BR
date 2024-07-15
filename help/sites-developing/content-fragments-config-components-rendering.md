---
title: Fragmentos de conteúdo configuram componentes para renderização
description: Fragmentos de conteúdo configuram componentes para renderização
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 9ef9ae75-cd8c-4adb-9bcb-e951d200d492
solution: Experience Manager, Experience Manager Sites
feature: Content Fragments
role: Developer
source-git-commit: 2e141ab04be33fea09ed7f6608dc9dcfaf2e50f1
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 6%

---

# Fragmentos de conteúdo configuram componentes para renderização{#content-fragments-configuring-components-for-rendering}

Há vários [serviços avançados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) relacionados à renderização de fragmentos de conteúdo. Para usar esses serviços, os tipos de recursos desses componentes devem se tornar conhecidos pela estrutura de fragmentos de conteúdo.

Isso é feito configurando o [Serviço OSGi - Configuração do componente de fragmento de conteúdo](#osgi-service-content-fragment-component-configuration).

>[!CAUTION]
>
>Se você não precisa dos [serviços avançados](/help/sites-developing/content-fragments-config-components-rendering.md#definition-of-advanced-services-that-need-configuration) descritos abaixo, ignore essa configuração.

>[!CAUTION]
>
>Ao estender ou usar os componentes prontos para uso, não é recomendável alterar a configuração.

>[!CAUTION]
>
>Você pode gravar um componente do zero que use somente a API de fragmentos de conteúdo, sem serviços avançados. No entanto, nesse caso, será necessário desenvolver o componente para que ele manipule o processamento apropriado.
>
>Portanto, é recomendável usar os componentes principais.

## Definição de serviços avançados que precisam de configuração {#definition-of-advanced-services-that-need-configuration}

Os serviços que exigem o registro de um componente são:

* Determinar as dependências corretamente durante a publicação (ou seja, verifique se os fragmentos e modelos podem ser publicados automaticamente com uma página se foram alterados desde a última publicação).
* Suporte para fragmentos de conteúdo na pesquisa de texto completo.
* O gerenciamento/manuseio de *conteúdo intermediário.*
* O gerenciamento/manuseio de *ativos de mídia mista.*
* Limpeza do Dispatcher para fragmentos referenciados (se uma página contendo um fragmento for republicada).
* Uso da renderização baseada em parágrafo.

Se você precisar de um ou mais desses recursos, então (normalmente) é mais fácil usar a funcionalidade pronta para uso, em vez de desenvolvê-la do zero.

## Serviço OSGi - Configuração do componente de fragmento de conteúdo {#osgi-service-content-fragment-component-configuration}

A configuração precisa ser associada à **Configuração do componente de fragmento de conteúdo** do serviço OSGi:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Consulte [Configurar OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes.

Por exemplo:

![cfm-01](assets/cfm-01.png)

A configuração do OSGi é:

<table>
 <tbody>
  <tr>
   <td>Rótulo</td>
   <td>Configuração OSGi<br /> </td>
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
   <td><strong>Propriedade dos elementos</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>O nome da propriedade que contém o(s) nome(s) do(s) elemento(s) a serem renderizados; por exemplo,<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Propriedade de variação</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>O nome da propriedade que contém o nome da variação a ser renderizada; por exemplo,<code>variationName</code></td>
  </tr>
 </tbody>
</table>

Para algumas funcionalidades (por exemplo, para renderizar apenas um intervalo de parágrafo), é necessário seguir algumas convenções:

<table>
 <tbody>
  <tr>
   <td>Nome de propriedade</td>
   <td>Descrição</td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>Uma propriedade de cadeia de caracteres que define o intervalo de parágrafos a ser gerado se estiver em <em>modo de renderização de elemento único</em>.</p> <p>Formato:</p>
    <ul>
     <li><code>1</code> ou <code>1-3</code> ou <code>1-3;6;7-8</code> ou <code>*-3;5-*</code></li>
     <li>avaliado somente se <code>paragraphScope</code> estiver definido como <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>Uma propriedade de cadeia de caracteres que define como os parágrafos devem ser gerados se estiverem no <em>modo de renderização de elemento único</em>.</p> <p>Valores:</p>
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
>Isso pode mudar em marcos posteriores ao 6.5.

## Exemplo {#example}

Como exemplo, consulte o seguinte (em uma instância de AEM pronta para uso):

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
