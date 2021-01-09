---
title: Configurações do Cloud Service
seo-title: Configurações do Cloud Service
description: Você pode estender as instâncias existentes para criar suas próprias configurações
seo-description: Você pode estender as instâncias existentes para criar suas próprias configurações
uuid: 9d20c3a4-2a12-4d3c-80c3-fcac3137a675
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: d25c03bf-6eaa-45f4-ab60-298865935a62
translation-type: tm+mt
source-git-commit: 801d57bbe8a1bede6dcb4bf7884e5f71ddea1e83
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 4%

---


# Configurações do Cloud Service{#cloud-service-configurations}

As configurações são projetadas para fornecer a lógica e a estrutura para armazenar configurações de serviço.

É possível estender as instâncias existentes para criar suas próprias configurações.

## Conceitos {#concepts}

Os princípios utilizados no desenvolvimento das configurações basearam-se nos seguintes conceitos:

* Serviços/Adaptadores são usados para recuperar as configurações.
* As configurações (por exemplo, propriedades/parágrafos) são herdadas dos pais.
* Referenciado de nó(s) do Analytics por caminho.
* Facilmente extensível.
* Tem a flexibilidade de atender a configurações mais complexas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Suporte para dependências (por exemplo, [Os plug-ins Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) precisam de uma configuração [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)).

## Estrutura {#structure}

O caminho básico das configurações é:

`/etc/cloudservices`.

Para cada tipo de configuração, um modelo e um componente serão fornecidos.Isso possibilita a existência de modelos de configuração que possam atender à maioria das necessidades após serem personalizados.

Para fornecer uma configuração para novos serviços, é necessário:

* criar uma página de serviço em

   `/etc/cloudservices`

* nesta rubrica:

   * um modelo de configuração
   * um componente de configuração

O modelo e o componente devem herdar `sling:resourceSuperType` do modelo base:

`cq/cloudserviceconfigs/templates/configpage`

ou componente de base, respectivamente

`cq/cloudserviceconfigs/components/configpage`

O provedor de serviço também deve fornecer a página de serviço:

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

Depois de configurar seu modelo e componente, você pode adicionar sua configuração adicionando subpáginas em:

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

* As propriedades fixas, definidas em uma caixa de diálogo, devem ser armazenadas diretamente em `jcr:node`.
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

### Integração AEM {#aem-integration}

Os serviços disponíveis são listados na guia **Cloud Services** da caixa de diálogo **Propriedades da página** (de qualquer página herdada de `foundation/components/page` ou `wcm/mobile/components/page`).

A guia também fornece:

* um link para o local onde você pode ativar o serviço
* escolha uma configuração (subnó do serviço) de um campo de caminho

#### Criptografia de senha {#password-encryption}

Ao armazenar credenciais de usuário para o serviço, todas as senhas devem ser criptografadas.

Para isso, adicione um campo de formulário oculto. Esse campo deve ter a anotação `@Encrypted` no nome da propriedade; Ou seja, para o campo `password`, o nome seria escrito como:

`password@Encrypted`

A propriedade será automaticamente criptografada (usando o serviço `CryptoSupport`) pelo `EncryptionPostProcessor`.

>[!NOTE]
>
>Isso é semelhante às anotações padrão ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)`.

>[!NOTE]
>
>Por padrão, as solicitações `EcryptionPostProcessor` somente criptografam `POST` feitas para `/etc/cloudservices`.

#### Propriedades adicionais do jcr da página de serviço:nós de conteúdo {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Caminho de referência para um componente a ser incluído automaticamente na página.<br /> Isso é usado para funcionalidade adicional e inclusões de JS.<br /> Isso inclui o componente na página em <br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> que está incluído (normalmente antes da  <code>body</code> tag).<br /> No caso de o Analytics e o Público alvo usarmos isso para incluir funcionalidades adicionais, como chamadas de JavaScript para rastrear o comportamento do visitante.</td>
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

### Casos de uso {#use-cases}

Esses serviços são fornecidos por padrão:

* [Trechos](/help/sites-administering/external-providers.md)  do rastreador (Google, WebTrends etc.)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
* [Pesquisar e promover](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote)
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte também [Criação de um Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).

