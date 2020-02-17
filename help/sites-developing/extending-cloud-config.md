---
title: Configurações do serviço de nuvem
seo-title: Configurações do serviço de nuvem
description: Você pode estender as instâncias existentes para criar suas próprias configurações
seo-description: Você pode estender as instâncias existentes para criar suas próprias configurações
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Configurações do serviço de nuvem{#cloud-service-configurations}

As configurações são projetadas para fornecer a lógica e estrutura para armazenar configurações de serviço.

É possível estender as instâncias existentes para criar suas próprias configurações.

##  Conceitos {#concepts}

Os princípios utilizados no desenvolvimento das configurações basearam-se nos seguintes conceitos:

* Serviços/Adaptadores são usados para recuperar as configurações.
* As configurações (por exemplo, propriedades/parágrafos) são herdadas dos pais.
* Referenciado de nó(s) de análise por caminho.
* Facilmente extensível.
* Tem a flexibilidade de atender a configurações mais complexas, como o [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Suporte para dependências (por exemplo, plug-ins do [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) precisam de uma configuração do [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) ).

## Estrutura {#structure}

O caminho básico das configurações é:

`/etc/cloudservices`.

Para cada tipo de configuração, um modelo e um componente serão fornecidos.Isso possibilita que os modelos de configuração atendam à maioria das necessidades após serem personalizados.

Para fornecer uma configuração para novos serviços, é necessário:

* criar uma página de serviço em

   `/etc/cloudservices`

* nesta rubrica:

   * um modelo de configuração
   * um componente de configuração

O modelo e o componente devem herdar o `sling:resourceSuperType` do modelo base:

`cq/cloudserviceconfigs/templates/configpage`

ou componente de base, respectivamente

`cq/cloudserviceconfigs/components/configpage`

O prestador de serviços também deve fornecer a página de serviço:

`/etc/cloudservices/<service-name>`

### Modelo {#template}

Seu modelo estenderá o modelo base:

`cq/cloudserviceconfigs/templates/configpage`

e defina um `resourceType` que aponte para o componente personalizado.

```xml
/libs/cq/analytics/templates/sitecatalyst
sling:resourceSuperType = cq/cloudserviceconfigs/templates/configpage
allowedChildren = /libs/cq/analytics/templates/sitecatalyst
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
componentReference = cq/analytics/components/sitecatalyst
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/sitecatalystpage

/libs/cq/analytics/templates/generictracker
sling:resourceSuperType = cq/cloudservices/templates/configpage
allowedChildren = /libs/cq/analytics/templates/generictracker
allowedPaths = /etc/cloudservices/analytics/*, /etc/cloudservices/analytics/.*
jcr:content/
cq:designPath = /etc/designs/cloudservices
sling:resourceType = cq/analytics/components/generictrackerpage
```

### Componentes {#components}

Seu componente deve estender o componente básico:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Após configurar seu modelo e componente, é possível adicionar sua configuração adicionando subpáginas em:

`/etc/cloudservices/<service-name>`

### Modelo de conteúdo {#content-model}

O modelo de conteúdo é armazenado como `cq:Page` em:

`/etc/cloudservices/<service-name>(/*)`

```xml
/etc/cloudservices
/etc/cloudservices/service-name
/etc/cloudservices/service-name/config
/etc/cloudservices/service-name/config/inherited-config
```

As configurações são armazenadas sob o subnó `jcr:content`.

* As propriedades fixas, definidas em uma caixa de diálogo, devem ser armazenadas `jcr:node` diretamente.
* Os elementos dinâmicos (usando `parsys` ou `iparsys`) usam um subnó para armazenar os dados do componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Para obter a documentação de referência sobre a API, consulte [com.day.cq.wcm.webservicessupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integração do AEM {#aem-integration}

Os serviços disponíveis são listados na guia Serviços **em** nuvem da caixa de diálogo Propriedades **da** página (de qualquer página que herda de `foundation/components/page` ou `wcm/mobile/components/page`).

A guia também fornece:

* um link para o local onde você pode ativar o serviço
* escolha uma configuração (subnó do serviço) de um campo de caminho

#### Criptografia de senha {#password-encryption}

Ao armazenar credenciais de usuário para o serviço, todas as senhas devem ser criptografadas.

Para isso, adicione um campo de formulário oculto. Este campo deve ter a anotação `@Encrypted` no nome da propriedade; ou seja, para o `password` campo, o nome deve ser escrito como:

`password@Encrypted`

A propriedade será automaticamente criptografada (usando o `CryptoSupport` serviço) pelo `EncryptionPostProcessor`.

>[!NOTE]
>
>Isso é semelhante às ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anotações padrão.

>[!NOTE]
>
>Por padrão, `EcryptionPostProcessor` somente criptografa `POST` solicitações feitas para `/etc/cloudservices`.

#### Propriedades adicionais para o jcr da página de serviço:nós de conteúdo {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Caminho de referência para um componente a ser incluído automaticamente na página.<br /> Isso é usado para funcionalidade adicional e inclusões de JS.<br /> Isso inclui o componente na página em que<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> está incluído (normalmente antes da <code>body</code> tag).<br /> No caso de o Analytics e o Target usarmos isso para incluir funcionalidades adicionais, como chamadas JavaScript para rastrear o comportamento do visitante.</td>
  </tr>
  <tr>
   <td>descrição</td>
   <td>Breve descrição do serviço.<br /> </td>
  </tr>
  <tr>
   <td>descriptionExtended</td>
   <td>Descrição estendida do serviço.</td>
  </tr>
  <tr>
   <td>classificação</td>
   <td>Classificação de serviço para uso em listagens.</td>
  </tr>
  <tr>
   <td>seletableChildren</td>
   <td>Filtro para exibir configurações na caixa de diálogo de propriedades da página.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL do site de serviço.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Rótulo do URL do serviço.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Caminho para a miniatura do serviço.</td>
  </tr>
  <tr>
   <td>visible</td>
   <td>Visibilidade na caixa de diálogo de propriedades da página; visível por padrão (opcional)</td>
  </tr>
 </tbody>
</table>

### Use Cases {#use-cases}

Esses serviços são fornecidos por padrão:

* [Trechos](/help/sites-administering/external-providers.md) do rastreador (Google, WebTrends etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Pesquisar e promover](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Scene7](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte também [Criação de um serviço](/help/sites-developing/extending-cloud-config-custom-cloud.md)da nuvem personalizada.

