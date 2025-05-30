---
title: Fragmentos de experiência no desenvolvimento do Adobe Experience Manager Sites
description: Saiba como personalizar fragmentos de experiência do Adobe Experience Manager.
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: e1acbef9b75af865ca07c41f318d21166227aa33
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 0%

---

# Fragmentos de experiência {#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-authoring/experience-fragments.md) é um grupo de um ou mais componentes, incluindo conteúdo e layout, que podem ser referenciados nas páginas.

Um fragmento de experiência principal e/ou variante usa:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, ele é revertido para

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Usando o seletor `.plain.` no URL, você poderá acessar a representação de HTML simples.

Isso está disponível por meio do navegador, mas seu objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos Web de terceiros, implementações personalizadas de publicações de conteúdo para dispositivos móveis) acessem o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A representação de HTML simples adiciona o protocolo, o host e o caminho de contexto aos caminhos que são:

* do tipo: `src`, `href` ou `action`

* ou terminar com: `-src` ou `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles são consumidos por terceiros, portanto, o link é sempre chamado da instância do Publish, não da instância do Autor.
>
>Para obter mais informações, consulte [Externalizar URLs](/help/sites-developing/externalizer.md).

![xf-14](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais; o [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como transformador. Isso é configurado em

* `/libs/experience-fragments/config/rewriter/experiencefragments`

### Configuração da geração de representação de HTML {#configuring-html-rendition-generation}

A representação de HTML é gerada usando os Pipelines de reescrita do Sling. O pipeline está definido em `/libs/experience-fragments/config/rewriter/experiencefragments`. O Transformador de HTML suporta as seguintes opções:

* `allowedCssClasses`
   * Uma expressão RegEx que corresponde às classes CSS que devem ser deixadas na representação final.
   * Isso é útil se o cliente quiser eliminar algumas classes CSS específicas
* `allowedTags`
   * Uma lista de tags HTML a serem permitidas na representação final.
   * Por padrão, as seguintes tags são permitidas (nenhuma configuração é necessária): html, head, title, body, img, p, span, ul, li, a, b, i, em, strong, h1, h2, h3, h4, h5, h6, br, noscript, div, link e script

É recomendável configurar a reescrita usando uma sobreposição. Consulte [Sobreposições](/help/sites-developing/overlays.md)

## Variações sociais {#social-variations}

As variantes sociais podem ser publicadas em redes sociais (texto e imagem). No Adobe Experience Manager (AEM), essas variantes sociais podem conter componentes; por exemplo, componentes de texto, componentes de imagem.

A imagem e o texto da publicação social podem ser obtidos de qualquer tipo de recurso de imagem ou de texto em qualquer nível de profundidade (no bloco de construção ou no contêiner de layout).

As variações sociais também permitem a criação de blocos e os consideram ao realizar ações sociais (no ambiente de publicação).

Para publicar o texto e a imagem corretos na rede social, algumas convenções precisam ser respeitadas se você estiver desenvolvendo seus próprios componentes personalizados.

Para isso, as seguintes propriedades devem ser usadas:

* Para extrair a imagem

   * `fileReference`
   * `fileName`

* Para extrair o texto

   * `text`

Os componentes que não usam essa convenção não serão considerados.

## Modelos para fragmentos de experiência {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Somente*** [modelos editáveis](/help/sites-developing/page-templates-editable.md) têm suporte para Fragmentos de experiência.
>
>Os Fragmentos de experiência só podem ser usados em páginas baseadas em modelos editáveis.

Ao desenvolver um novo modelo para fragmentos de experiência, você pode seguir as práticas padrão para um [modelo editável](/help/sites-developing/page-templates-editable.md).

Para criar um modelo de fragmento de experiência detectado pelo assistente **Criar Fragmento de Experiência**, siga um destes conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do template (o nó inicial) deve herdar de:

      `cq/experience-fragments/components/xfpage`

   1. E o nome do template deve começar com:

      `experience-fragments`
Isso permite que os usuários criem fragmentos de experiência em /content/experience-fragments, pois a propriedade `cq:allowedTemplates` dessa pasta inclui todos os modelos com nomes que começam com `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seu próprio esquema de nomenclatura ou locais do modelo.

1. [Modelos permitidos](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) podem ser configurados no console Fragmentos de experiência.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

[Os componentes de desenvolvimento](/help/sites-developing/components.md) para uso com/nos Fragmentos de experiência seguem as práticas padrão.

A única configuração adicional é garantir que os componentes sejam [permitidos no modelo, isso é obtido com a Política de Conteúdo](/help/sites-developing/page-templates-editable.md#content-policies).

## O provedor de reescrita de link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

No AEM, é possível criar Fragmentos de experiência. Um fragmento de experiência:

* consiste em um grupo de componentes juntamente com um layout,
* O pode existir independentemente de uma página AEM.

Um dos casos de uso para esses grupos é para incorporar conteúdo em pontos de contato de terceiros, como o Adobe Target.

### Reescrita de link padrão {#default-link-rewriting}

Usando o recurso [Exportar para o Destino](/help/sites-administering/experience-fragments-target.md), você pode:

* criar um fragmento de experiência,
* adicionar componentes a ele,
* e, em seguida, exporte-a como uma Oferta do Adobe Target, no Formato HTML ou JSON.

Este recurso pode ser [habilitado em uma instância de autor do AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Ele requer uma configuração válida do Adobe Target e configurações para o Externalizador de links.

O Externalizador de links é usado para determinar os URLs corretos necessários ao criar a versão do HTML da oferta do Target, que é então enviada para o Adobe Target. Isso é necessário, pois o Adobe Target exige que todos os links dentro da Oferta de HTML do Target possam ser acessados publicamente. Isso significa que todos os recursos aos quais os links fazem referência e o próprio Fragmento de experiência devem ser publicados antes de serem usados.

Por padrão, quando você constrói uma Oferta de HTML do Target, uma solicitação é enviada para um seletor de Sling personalizado no AEM. Este seletor é chamado `.nocloudconfigs.html`. Como o nome indica, ele cria uma renderização de HTML simples de um Fragmento de experiência, mas não inclui configurações de nuvem (que seriam informações supérfluas).

Depois de gerar a página HTML, o pipeline de reescrita do Sling faz modificações na saída:

1. Os elementos `html`, `head` e `body` são substituídos por elementos `div`. Os elementos `meta`, `noscript` e `title` são removidos (são elementos secundários do elemento `head` original e não são considerados quando este é substituído pelo elemento `div`).

   Isso é feito para garantir que a Oferta do HTML Target possa ser incluída nas Atividades do Target.

1. O AEM modifica todos os links internos presentes no HTML, para que eles apontem para um recurso publicado.

   Para determinar os links a serem modificados, o AEM segue esse padrão para atributos de elementos HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src e assim por diante)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href` e assim por diante)

   >[!NOTE]
   >
   >Normalmente, os links internos no HTML são links relativos, mas pode haver casos em que os componentes personalizados fornecem URLs completos no HTML. Por padrão, o AEM ignora esses URLs completos e não faz modificações.

   Os links nesses atributos são executados por meio do AEM Link Externalizer `publishLink()` para recriar a URL como se ela estivesse em uma instância publicada e, como tal, disponibilizada publicamente.

Ao usar uma implementação pronta para uso, o processo descrito acima deve ser suficiente para gerar a oferta do Target a partir do fragmento de experiência e, em seguida, exportá-la para o Adobe Target. No entanto, há alguns casos de uso que não são considerados nesse processo; eles incluem:

* Mapeamento do Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Nesses casos de uso, o AEM fornece a interface do provedor de reescrita de links.

### Interface do provedor de reescrita de links {#link-rewriter-provider-interface}

>[!NOTE]
>
>Esta interface foi introduzida no [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/previous/6-5-1.md).

Para casos mais complicados, não cobertos pelo [padrão](#default-link-rewriting), o AEM oferece a Interface do Provedor de Reescrita de Link. Esta é uma interface `ConsumerType` que você pode implementar em seus pacotes, como um serviço. Ele ignora as modificações que o AEM executa nos links internos de uma oferta de HTML, conforme renderizado a partir de um Fragmento de experiência. Essa interface permite personalizar o processo de reescrita de links de HTML internos para alinhar-se às suas necessidades comerciais.

Exemplos de casos de uso para implementar essa interface como um serviço incluem:

* Os Mapeamentos do Sling são ativados nas instâncias de publicação, mas não na instância do autor
* Um dispatcher ou tecnologia semelhante é usada para redirecionar URLs internamente
* Há `sling:alias mechanisms` disponíveis para recursos

>[!NOTE]
>
>Essa interface só processa os links de HTML internos da Oferta do Target gerada.

A Interface do Provedor de Reescrita de Link ( `ExperienceFragmentLinkRewriterProvider`) é a seguinte:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Como usar a interface do provedor de reescrita de links {#how-to-use-the-link-rewriter-provider-interface}

Para usar a interface, primeiro é necessário criar um pacote contendo um novo componente de serviço que implemente a interface do Provedor de reescrita de link.

Esse serviço é usado para conectar a regravação da Exportação do fragmento de experiência para o Target para ter acesso aos vários links.

Por exemplo, `ComponentService`:

```java
import com.adobe.cq.xf.ExperienceFragmentLinkRewriterProvider;
import com.adobe.cq.xf.ExperienceFragmentVariation;
import org.osgi.service.component.annotations.Service;
import org.osgi.service.component.annotations.Component;

@Component
@Service
public class GeneralLinkRewriter implements ExperienceFragmentLinkRewriterProvider {

    @Override
    public String rewriteLink(String link, String tag, String attribute) {
        return null;
    }

    @Override
    public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
        return false;
    }

    @Override
    public int getPriority() {
        return 0;
    }

}
```

Para que o serviço funcione, agora há três métodos que precisam ser implementados dentro dele:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Você precisa indicar ao sistema se ele precisa regravar os links quando for feita uma chamada para Export to Target em uma determinada variação de Fragmento de experiência. Para fazer isso, implemente o método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por exemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Esse método recebe como parâmetro a variação do Fragmento de experiência que o sistema de Exportação para o Target está reescrevendo no momento.

No exemplo acima, gostaríamos de reescrever:

* links presentes em `src`

* Somente atributos de `href`

* para um Fragmento de experiência específico:
  `/content/experience-fragment/master`

Quaisquer outros Fragmentos de experiência que passam pelo sistema Exportar para o Target são ignorados e não são afetados pelas alterações implementadas neste Serviço.

#### rewriteLink {#rewritelink}

Para a variação do Fragmento de experiência afetada pelo processo de regravação, ele continuará a permitir que o serviço lide com a regravação do link. Sempre que um link é encontrado no HTML interno, o seguinte método é chamado:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, o método recebe os parâmetros:

* `link`
A representação `String` do link que está sendo processado. Normalmente, esse é um URL relativo que aponta para o recurso na instância do autor.

* `tag`
O nome do elemento HTML que está sendo processado.

* `attribute`
O nome exato do atributo.

Por exemplo, se o sistema Exportar para Destino estiver processando esse elemento, você poderá definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para o método `rewriteLink()` é feita usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, você pode tomar decisões com base na entrada fornecida e, em seguida, reescrever o link de acordo.

Para o nosso exemplo, gostaríamos de remover a parte `/etc.clientlibs` da URL e adicionar o domínio externo apropriado. Para simplificar, consideraremos que temos acesso a um Resource Resolver para o seu serviço, como em `rewriteLinkExample2`:

>[!NOTE]
>
>Para obter mais informações sobre como obter um resolvedor de recursos por meio de um usuário de serviço, consulte [Usuários de serviço no AEM](/help/sites-administering/security-service-users.md).

```java
private ResourceResolver resolver;

private Externalizer externalizer;

@Override
public String rewriteLink(String link, String tag, String attribute) {

    // get the externalizer service
    externalizer = resolver.adaptTo(Externalizer.class);
    if(externalizer == null) {
        // if there was an error, then we do not modify the link
        return null;
    }

    // remove leading /etc.clientlibs from resource link before externalizing
    link = link.replaceAll("/etc.clientlibs", "");

    // considering that we configured our publish domain, we directly apply the publishLink() method
    link = externalizer.publishLink(resolver, link);

    return link;
}
```

>[!NOTE]
>
>Se o método acima retornar `null`, o sistema Export to Target deixará o link como está, um link relativo para um recurso.

#### Prioridades - getPriority {#priorities-getpriority}

Não é incomum precisar de vários serviços para atender a diferentes tipos de Fragmentos de experiência, ou até mesmo ter um Serviço genérico que lida com a externalização e o mapeamento de todos os Fragmentos de experiência. Nesses casos, podem surgir conflitos sobre qual serviço usar, portanto, o AEM oferece a possibilidade de definir **Prioridades** para serviços diferentes. As prioridades são especificadas usando o método:

* `getPriority()`

Este método permite o uso de vários serviços em que o método `shouldRewrite()` retorna &quot;true&quot; para o mesmo Fragmento de experiência. O serviço que retorna o número mais alto de seu método `getPriority()` é o que manipula a variação do fragmento de experiência.

Como exemplo, você pode ter um `GenericLinkRewriterProvider` que manipula o mapeamento básico para todos os Fragmentos de experiência e quando o método `shouldRewrite()` retorna `true` para todas as Variações de Fragmento de experiência. Para vários Fragmentos de experiência específicos, talvez você queira manuseio especial; portanto, nesse caso, você pode fornecer um `SpecificLinkRewriterProvider` para o qual o método `shouldRewrite()` retorna &quot;true&quot; somente para algumas Variações de Fragmento de experiência. Para garantir que `SpecificLinkRewriterProvider` seja escolhido para lidar com essas Variações de Fragmento de Experiência, ele deve retornar em seu método `getPriority()` um número maior que `GenericLinkRewriterProvider.`
