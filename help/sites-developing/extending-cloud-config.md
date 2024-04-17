---
title: Configurações do serviço de nuvem
description: É possível estender as instâncias existentes para criar suas próprias configurações
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 20a19ee5-7113-4aca-934a-a42c415a8d93
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 3%

---

# Configurações do serviço de nuvem{#cloud-service-configurations}

As configurações são projetadas para fornecer a lógica e a estrutura para armazenar configurações de serviço.

É possível estender as instâncias existentes para criar suas próprias configurações.

## Conceitos  {#concepts}

Os princípios usados no desenvolvimento das configurações foram baseados nos seguintes conceitos:

* Serviços/adaptadores são usados para recuperar as configurações.
* As configurações (por exemplo, propriedades/parágrafos) são herdadas dos pais.
* Referenciado a partir de nós do Analytics por caminho.
* Facilmente extensível.
* Tem flexibilidade para atender a configurações mais complexas, como [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics).
* Suporte para dependências (por exemplo, [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) Os plug-ins do precisam de um [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics) configuração).

## Estrutura {#structure}

O caminho base das configurações é:

`/etc/cloudservices`.

Para cada tipo de configuração, um modelo e um componente são fornecidos. Isso possibilita ter modelos de configuração que podem atender à maioria das necessidades após a personalização.

Para fornecer uma configuração para novos serviços, faça o seguinte:

* Criar uma página de serviço no

  `/etc/cloudservices`

* Nesta seção:

   * um modelo de configuração
   * um componente de configuração

O modelo e o componente devem herdar o `sling:resourceSuperType` a partir do modelo base:

`cq/cloudserviceconfigs/templates/configpage`

Ou componente base, respectivamente

`cq/cloudserviceconfigs/components/configpage`

O provedor de serviços também deve fornecer a página de serviço:

`/etc/cloudservices/<service-name>`

### Modelo {#template}

Seu modelo estende o modelo base:

`cq/cloudserviceconfigs/templates/configpage`

E definir um `resourceType` que aponta para o componente personalizado.

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

Depois de definir o modelo e o componente, é possível adicionar a configuração adicionando subpáginas em:

`/etc/cloudservices/<service-name>`

### Modelo do conteúdo {#content-model}

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
* Elementos dinâmicos (uso de `parsys` ou `iparsys`) usar um subnó para armazenar os dados do componente.

```xml
/etc/cloudservices/service/config/jcr:content as nt:unstructured
propertyname
*
par/component/ as cq:Component
propertyname
*
```

### API {#api}

Para obter a documentação de referência sobre a API, consulte [com.day.cq.wcm.webservicesupport](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/webservicesupport/package-summary.html).

### Integração com o AEM {#aem-integration}

Os serviços disponíveis estão listados na **Cloud Service** guia do **Propriedades da página** caixa de diálogo (de qualquer página que herde de `foundation/components/page` ou `wcm/mobile/components/page`).

A guia também fornece:

* um link para o local onde você pode habilitar o serviço
* escolha uma configuração (subnó do serviço) em um campo de caminho

#### Criptografia de senha {#password-encryption}

Ao armazenar credenciais de usuário para o serviço, todas as senhas devem ser criptografadas.

Você pode fazer isso adicionando um campo de formulário oculto. Este campo deve ter a anotação `@Encrypted` no nome da propriedade; ou seja, para a variável `password` o nome seria escrito como:

`password@Encrypted`

A propriedade será criptografada automaticamente (usando o `CryptoSupport` serviço) pela `EncryptionPostProcessor`.

>[!NOTE]
>
>É semelhante ao padrão ` [SlingPostServlet](https://sling.apache.org/site/manipulating-content-the-slingpostservlet-servletspost.html)` anotações.

>[!NOTE]
>
>Por padrão, a variável `EcryptionPostProcessor` somente criptografa `POST` pedidos feitos a `/etc/cloudservices`.

#### Propriedades adicionais para a página de serviço jcr:nós de conteúdo {#additional-properties-for-service-page-jcr-content-nodes}

<table>
 <tbody>
  <tr>
   <td><strong>Propriedade</strong></td>
   <td><strong>Descrição</strong></td>
  </tr>
  <tr>
   <td>componentReference</td>
   <td>Caminho de referência para um componente a ser incluído automaticamente na página.<br /> Isso é usado para funcionalidade adicional e inclusões de JS.<br /> Isso inclui o componente na página em que<br /> <code> cq/cloudserviceconfigs/components/servicecomponents</code><br /> está incluído (normalmente antes da <code>body</code> tag).<br /> No caso do Adobe Analytics e do Adobe Target, usamos isso para incluir funcionalidades adicionais, como chamadas JavaScript para rastrear o comportamento do visitante.</td>
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
   <td>Rótulo para URL de serviço.</td>
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

* [Trechos do rastreador](/help/sites-administering/external-providers.md) (Google, WebTrends e outros)
* [Adobe Analytics](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-analytics)
* [Test&amp;Target](/help/sites-administering/marketing-cloud.md#integrating-with-adobe-target)
<!-- Search&Promote is end of life as of September 1, 2022 * [Search&Promote](/help/sites-administering/marketing-cloud.md#integrating-with-search-promote) -->
* [Dynamic Media](/help/sites-administering/marketing-cloud.md#integrating-with-scene)

>[!NOTE]
>
>Consulte também [Criação de um Cloud Service personalizado](/help/sites-developing/extending-cloud-config-custom-cloud.md).
