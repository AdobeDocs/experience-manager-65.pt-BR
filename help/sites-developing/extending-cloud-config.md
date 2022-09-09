---
title: Configurações do Cloud Service
seo-title: Cloud Service Configurations
description: É possível estender as instâncias existentes para criar suas próprias configurações
seo-description: You can extend the existing instances to create your own configurations
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
source-git-commit: 58594be73372e128ba999a8290615fbcb447084e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Configurações do Cloud Service{#cloud-service-configurations}

As configurações são projetadas para fornecer a lógica e a estrutura para armazenar configurações de serviço.

É possível estender as instâncias existentes para criar suas próprias configurações.

## Conceitos  {#concepts}

Os princípios usados no desenvolvimento das configurações foram baseados nos seguintes conceitos:

* Os serviços/adaptadores são usados para recuperar as configurações.
* As configurações (por exemplo, propriedades/parágrafos) são herdadas dos pais.
* Referenciado a partir de nós do Analytics por caminho.
* Facilmente extensível.
* Tem flexibilidade para atender a configurações mais complexas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Suporte para dependências (por exemplo, [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) os plug-ins precisam de um [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) configuração).

## Estrutura {#structure}

O caminho base das configurações é:

`/etc/cloudservices`.

Para cada tipo de configuração, um modelo e um componente serão fornecidos.Isso possibilita ter modelos de configuração que podem atender à maioria das necessidades após serem personalizados.

Para fornecer uma configuração para novos serviços, você precisa:

* criar uma página de serviço em

   `/etc/cloudservices`

* nesta rubrica:

   * um template de configuração
   * um componente de configuração

O modelo e o componente devem herdar o `sling:resourceSuperType` do template base:

`cq/cloudserviceconfigs/templates/configpage`

ou componente base, respectivamente

`cq/cloudserviceconfigs/components/configpage`

O provedor de serviços também deve fornecer a página de serviço:

`/etc/cloudservices/<service-name>`

### Modelo {#template}

Seu modelo estenderá o modelo base:

`cq/cloudserviceconfigs/templates/configpage`

e defina uma `resourceType` que aponta para o componente personalizado.

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

Seu componente deve estender o componente base:

`cq/cloudserviceconfigs/templates/configpage`

```xml
/libs/cq/analytics/components/sitecatalystpage

/libs/cq/analytics/components/generictrackerpage
```

Após configurar o modelo e o componente, é possível adicionar a configuração adicionando subpáginas em:

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

As configurações são armazenadas no subnó `jcr:content`.

* As propriedades fixas, definidas em uma caixa de diálogo, devem ser armazenadas no `jcr:node` diretamente.
* Elementos dinâmicos (usando `parsys` ou `iparsys`) use um subnó para armazenar os dados do componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Para obter a documentação de referência sobre a API, consulte [com.day.cq.wcm.webservicesupport](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integração de AEM {#aem-integration}

Os serviços disponíveis estão listados na variável **Cloud Services** da guia **Propriedades da página** de qualquer página herdada de `foundation/components/page` ou `wcm/mobile/components/page`).

A guia também fornece:

* um link para o local onde você pode ativar o serviço
* escolha uma configuração (subnó do serviço) de um campo de caminho

#### Criptografia de senha {#password-encryption}

Ao armazenar credenciais do usuário para o serviço, todas as senhas devem ser criptografadas.

Para isso, adicione um campo de formulário oculto. Este campo deve ter a anotação `@Encrypted` no nome da propriedade; ou seja, para o `password` o nome seria escrito como:

`password@Encrypted`

A propriedade será automaticamente criptografada (usando o `CryptoSupport` pela `EncryptionPostProcessor`.

>[!NOTE]
>
>Isso é semelhante ao padrão ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anotações.

>[!NOTE]
>
>Por padrão, a variável `EcryptionPostProcessor` somente criptografia `POST` pedidos apresentados `/etc/cloudservices`.

#### Propriedades adicionais para a página de serviço jcr:nós de conteúdo {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Caminho de referência para um componente a ser incluído automaticamente na página.<br /> Isso é usado para funcionalidades adicionais e inclusões de JS.<br /> Isso inclui o componente na página em que<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> é incluída (normalmente antes da variável <code>body</code> tag).<br /> Caso o Analytics e o Target sejam usados para incluir funcionalidades adicionais, como chamadas de JavaScript para rastrear o comportamento do visitante.</td>
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
   <td>Classificação do serviço para uso em listas.</td>
  </tr>
  <tr>
   <td>seletedChildren</td>
   <td>Filtrar para exibir configurações na caixa de diálogo de propriedades da página.</td>
  </tr>
  <tr>
   <td>serviceUrl</td>
   <td>URL para o site do serviço.</td>
  </tr>
  <tr>
   <td>serviceUrlLabel</td>
   <td>Rótulo do URL de serviço.</td>
  </tr>
  <tr>
   <td>thumbnailPath</td>
   <td>Caminho para a miniatura do serviço.</td>
  </tr>
  <tr>
   <td>visível</td>
   <td>Visibilidade na caixa de diálogo de propriedades da página; visível por padrão (opcional)</td>
  </tr>
 </tbody>
</table>

### Casos de uso {#use-cases}

Esses serviços são fornecidos por padrão:

* [Trechos do rastreador](/help/sites-administering/external-providers.md) (Google, WebTrends etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)

<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte também [Criação de um Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).
