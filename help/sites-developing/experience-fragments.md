---
title: Fragmentos de experiência
seo-title: Experience Fragments
description: Saiba mais sobre como personalizar Fragmentos de experiência.
seo-description: Learn about customizing Experience Fragments.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
exl-id: c4fb1b5e-e15e-450e-b882-fe27b165ff9f
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '1660'
ht-degree: 3%

---

# Fragmentos de experiência{#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-authoring/experience-fragments.md) é um grupo de um ou mais componentes, incluindo o conteúdo e o layout que podem ser referenciados nas páginas.

Um Fragmento de experiência Principal e/ou Variante usa:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html` reverte para

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Usar o `.plain.` no URL, você pode acessar a representação de HTML simples.

Isso está disponível no navegador, mas o objetivo principal é permitir outros aplicativos (por exemplo, aplicativos da Web de terceiros, implementações móveis personalizadas) para acessar o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A representação de HTML simples adiciona o protocolo, host e caminho de contexto aos caminhos que são:

* do tipo: `src`, `href`ou `action`

* ou terminar com: `-src`ou `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles devem ser consumidos por terceiros, de modo que o link sempre será chamado da instância de publicação, não do autor.

![xf-14](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais; o [Reescrita Sling](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como o transformador. Isso é configurado em

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variações sociais {#social-variations}

As variantes do Social podem ser postadas nas redes sociais (texto e imagem). AEM essas variantes sociais podem conter componentes; por exemplo, componentes de texto, componentes de imagem.

A imagem e o texto da publicação social podem ser obtidos de qualquer tipo de recurso de imagem ou tipo de recurso de texto em qualquer nível de profundidade (no bloco de construção ou no contêiner de layout).

As variações sociais também permitem blocos de construção e os consideram ao realizar ações sociais (no ambiente de publicação).

Para postar o texto e a imagem corretos na rede social, algumas convenções precisam ser respeitadas se você estiver desenvolvendo seus próprios componentes personalizados.

Para isso, as seguintes propriedades devem ser usadas:

* Para extrair a imagem

   * `fileReference`
   * `fileName`

* Para extrair o texto

   * `text`

Os componentes que não usam essa convenção não serão considerados.

## Modelos para Fragmentos de experiência {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Somente*** [modelos editáveis](/help/sites-developing/page-templates-editable.md) são compatíveis com Fragmentos de experiência.

Ao desenvolver um novo modelo para Fragmentos de experiência, você pode seguir as práticas padrão de um [modelo editável](/help/sites-developing/page-templates-editable.md).

Para criar um modelo de fragmento de experiência detectado pelo **Criar fragmento de experiência** assistente, você deve seguir um desses conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do template (o nó inicial) deve herdar de:
      `cq/experience-fragments/components/xfpage`

   1. E o nome do template deve começar com:
      `experience-fragments`
Isso permite que os usuários criem fragmentos de experiência em /content/experience-fragments como o 
`cq:allowedTemplates` a propriedade desta pasta inclui todos os modelos com nomes começando com `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seu próprio esquema de nomenclatura ou locais de modelo.

1. [Modelos permitidos](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) pode ser configurado no console Fragmentos de experiência.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

[Desenvolvimento de componentes](/help/sites-developing/components.md) para uso com/nos Fragmentos de experiência, siga as práticas padrão.

A única configuração adicional é garantir que os componentes sejam [permitido no modelo, isso é obtido com a Política de conteúdo](/help/sites-developing/page-templates-editable.md#content-policies).

## O provedor de regravação do link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

No AEM você tem a possibilidade de criar Fragmentos de experiência. Um fragmento de experiência:

* consiste em um grupo de componentes junto com um layout,
* pode existir independentemente de uma página de AEM.

Um dos casos de uso desses grupos é a incorporação de conteúdo em pontos de contato de terceiros, como o Adobe Target.

### Regravação de link padrão {#default-link-rewriting}

Usar o [Exportar para o Target](/help/sites-administering/experience-fragments-target.md) , é possível:

* criar um fragmento de experiência,
* adicionar componentes a ele,
* e, em seguida, exportá-la como uma Oferta Adobe Target, no Formato HTML ou JSON.

Esse recurso pode ser [ativado em uma instância de autor de AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Requer uma configuração válida do Adobe Target e configurações para o Link Externalizer.

O Link Externalizer é usado para determinar os URLs corretos necessários ao criar a versão do HTML da Oferta do Target, que é enviada subsequentemente para o Adobe Target. Isso é necessário, pois o Adobe Target exige que todos os links dentro da Oferta de HTML do Target possam ser acessados publicamente; isso significa que todos os recursos que os links referenciam e o próprio Fragmento de experiência devem ser publicados antes de serem usados.

Por padrão, ao criar uma Oferta do HTML do Target, uma solicitação é enviada para um seletor do Sling personalizado no AEM. Este seletor é chamado `.nocloudconfigs.html`. Como o nome implica, ele cria uma renderização de HTML simples de um Fragmento de experiência, mas não inclui configurações de nuvem (que seriam informações supérfluas).

Depois de gerar a página HTML, o pipeline do Sling Rewriter faz modificações na saída:

1. O `html`, `head`e `body` são substituídos por `div` elementos. O `meta`, `noscript` e `title` são removidos (são elementos filho do original `head` e não são considerados quando é substituído pelo elemento `div` elemento).

   Isso é feito para garantir que a Oferta do HTML Target possa ser incluída nas Atividades do Target.

1. AEM modifica todos os links internos presentes no HTML, para que apontem para um recurso publicado.

   Para determinar os links a serem modificados, AEM segue este padrão para atributos de elementos de HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src etc)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href`, etc.)

   >[!NOTE]
   >
   >Na maioria dos casos, os links internos no HTML são links relativos, mas pode haver casos em que componentes personalizados fornecem URLs completos no HTML. Por padrão, o AEM ignora esses URLs totalmente fornecidos e não faz modificações.

   Os links nesses atributos são executados pelo AEM Link Externalizer `publishLink()` para recriar o URL como se ele estivesse em uma instância publicada e, como tal, disponível publicamente.

Ao usar uma implementação pronta para uso, o processo descrito acima deve ser suficiente para gerar a Oferta do Target a partir do Fragmento de experiência e, em seguida, exportá-la para o Adobe Target. No entanto, existem alguns casos de uso que não são contabilizados neste processo; estes incluem:

* Mapeamento do Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Para esses casos de uso, AEM fornece a Interface do provedor de regravação de links.

### Interface do provedor de regravação de links {#link-rewriter-provider-interface}

>[!NOTE]
>
>Essa interface foi introduzida em [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/previous/6.5.1.md).

Para casos mais complicados, não abrangidos pelo [default](#default-link-rewriting), AEM oferece a Interface do provedor de regravação de links. Isso é uma `ConsumerType` interface que você pode implementar em seus pacotes, como um serviço. Ele ignora as modificações AEM são executadas em links internos de uma oferta do HTML como renderizada de um Fragmento de experiência. Essa interface permite personalizar o processo de reescrita de links de HTML internos para alinhar-se às necessidades de sua empresa.

Exemplos de casos de uso para implementar essa interface como um serviço incluem:

* Os Mapeamentos do Sling são ativados nas instâncias de publicação, mas não na instância do autor
* Um dispatcher ou tecnologia semelhante é usada para redirecionar URLs internamente
* Existem `sling:alias mechanisms` em vigor para recursos

>[!NOTE]
>
>Essa interface só processa os links de HTML internos da Oferta do Target gerada.

A Interface Do Provedor De Reescrita De Link ( `ExperienceFragmentLinkRewriterProvider`) é o seguinte:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Como usar a interface do provedor de regravação de links {#how-to-use-the-link-rewriter-provider-interface}

Para usar a interface, primeiro é necessário criar um pacote contendo um novo componente de serviço que implemente a interface do Provedor de regravação de links .

Esse serviço será usado para se conectar à regravação Exportar fragmento de experiência para o Target para ter acesso aos vários links.

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

Para que o serviço funcione, agora há três métodos que precisam ser implementados dentro do serviço:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

Você precisa indicar ao sistema se ele precisa reescrever os links quando uma chamada é feita para Exportar para Target em uma determinada variação de Fragmento de experiência. Para isso, implemente o método :

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por exemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Esse método recebe, como parâmetro, a Variação do fragmento de experiência que o sistema Exportar para o Target está reescrevendo no momento.

No exemplo acima, gostaríamos de reescrever:

* links presentes em `src`

* `href` somente atributos

* para um Fragmento de experiência específico:
   `/content/experience-fragment/master`

Quaisquer outros Fragmentos de experiência transmitidos pelo sistema Exportar para o Target são ignorados e não são afetados pelas alterações implementadas neste Serviço.

#### rewriteLink {#rewritelink}

Para a variação do Fragmento de experiência afetada pelo processo de regravação, ele continuará permitindo que o serviço gerencie a regravação do link. Sempre que um link é encontrado no HTML interno, o seguinte método é chamado:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, o método recebe os parâmetros:

* `link`
As ações 
`String` representação do link que está sendo processado no momento. Normalmente, é um URL relativo que aponta para o recurso na instância do autor.

* `tag`
O nome do elemento HTML que está sendo processado no momento.

* `attribute`
O nome exato do atributo.

Se, por exemplo, o sistema Exportar para o Target estiver processando esse elemento no momento, você pode definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para a `rewriteLink()` é feito usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, você pode tomar decisões com base em determinada entrada e, em seguida, reescrever o link adequadamente.

Para nosso exemplo, gostaríamos de remover a variável `/etc.clientlibs` parte do URL e adicione o domínio externo apropriado. Para simplificar, consideraremos que temos acesso a um Resolvedor de Recursos para seu serviço, como em `rewriteLinkExample2`:

>[!NOTE]
>
>Para obter mais informações sobre como obter um resolvedor de recursos por meio de um usuário de serviço, consulte [Usuários do serviço no AEM](/help/sites-administering/security-service-users.md).

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
>Se o método acima retornar `null`, o sistema Exportar para o Target deixará o link como está, um link relativo para um recurso.

#### Prioridades - getPriority {#priorities-getpriority}

Não é incomum precisar de vários serviços para atender a diferentes tipos de Fragmentos de experiência ou até mesmo ter um Serviço genérico que lida com a externalização e o mapeamento para todos os Fragmentos de experiência. Nesses casos, podem surgir conflitos sobre qual serviço usar, de modo que o AEM oferece a possibilidade de definir **Prioridades** para diferentes serviços. As prioridades são especificadas usando o método :

* `getPriority()`

Este método permite o uso de vários serviços, onde a variável `shouldRewrite()` retorna true para o mesmo Fragmento de experiência. O serviço que retorna o número mais alto de sua `getPriority()`é o serviço que lida com a Variação do fragmento de experiência.

Como exemplo, você pode ter uma `GenericLinkRewriterProvider` que manipula o mapeamento básico para todos os Fragmentos de experiência e quando a variável `shouldRewrite()` retornos de método `true` para todas as variações de fragmento de experiência. Para vários Fragmentos de experiência específicos, você pode desejar um manuseio especial; nesse caso, você pode fornecer um `SpecificLinkRewriterProvider` em que `shouldRewrite()` retorna true somente para algumas variações do fragmento de experiência. Para garantir que `SpecificLinkRewriterProvider` é escolhido para manipular essas variações do fragmento de experiência, deve retornar em `getPriority()` um número maior que `GenericLinkRewriterProvider.`
