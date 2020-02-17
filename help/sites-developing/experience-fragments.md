---
title: Fragmentos de experiência
seo-title: Fragmentos de experiência
description: Saiba mais sobre como personalizar Fragmentos de experiência.
seo-description: Saiba mais sobre como personalizar Fragmentos de experiência.
uuid: fc9f7e59-bd7c-437a-8c63-de8559b5768d
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: c02e713e-15f3-408b-879a-d5eb014aef02
docset: aem65
translation-type: tm+mt
source-git-commit: 25eff10d4be811774e7a25cebf7e0506acfd5b0b

---


# Fragmentos de experiência{#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-authoring/experience-fragments.md) é um grupo de um ou mais componentes, incluindo o conteúdo e o layout que podem ser referenciados nas páginas.

Um fragmento de experiência mestre e/ou variável usa:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html` ele volta para

* `sling:resourceSuperType` : `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Usando o `.plain.` seletor no URL, você pode acessar a execução HTML simples.

Isso está disponível no navegador, mas seu objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos da Web de terceiros, implementações móveis personalizadas) acessem o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A execução HTML simples adiciona o protocolo, o host e o caminho de contexto aos caminhos que são:

* do tipo: `src`, `href`ou `action`

* ou terminar com: `-src`, ou `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles devem ser consumidos por terceiros, de modo que o link sempre será chamado da instância de publicação, não do autor.

![xf-14](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais; o [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como o transformador. Isso está configurado em

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variações sociais {#social-variations}

As variantes sociais podem ser postadas em redes sociais (texto e imagem). No AEM, essas variantes sociais podem conter componentes; por exemplo, componentes de texto, componentes de imagem.

A imagem e o texto da publicação social podem ser obtidos de qualquer tipo de recurso de imagem ou de recurso de texto em qualquer nível de profundidade (no bloco de construção ou no contêiner de layout).

As variações sociais também permitem blocos de construção e os consideram ao realizar ações sociais (no ambiente de publicação).

Para publicar o texto e a imagem corretos na rede de mídia social, algumas convenções precisam ser respeitadas se você estiver desenvolvendo seus próprios componentes personalizados.

Para isso, as seguintes propriedades devem ser usadas:

* Para extrair a imagem

   * `fileReference`
   * `fileName`

* Para extrair o texto

   * `text`

Os componentes que não usam esta convenção não serão considerados.

## Modelos para fragmentos de experiência {#templates-for-experience-fragments}

>[!CAUTION]
>
>***Somente*** modelos [](/help/sites-developing/page-templates-editable.md) editáveis são suportados em Fragmentos de experiência.

Ao desenvolver um novo modelo para Fragmentos de experiência, você pode seguir as práticas padrão de um modelo [](/help/sites-developing/page-templates-editable.md)editável.

Para criar um modelo de fragmento de experiência detectado pelo assistente **Criar fragmento** de experiência, siga um destes conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do modelo (o nó inicial) deve herdar de:
      `cq/experience-fragments/components/xfpage`

   1. E o nome do modelo deve começar com:
      `experience-fragments`
Isso permite que os usuários criem fragmentos de experiência em /content/experience-fragments, já que a `cq:allowedTemplates` propriedade dessa pasta inclui todos os modelos que têm nomes começando com `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seus próprios esquemas de nomeação ou locais de modelo.

1. [Modelos](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) permitidos podem ser configurados no console Fragmentos de experiência.
<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

[O desenvolvimento de componentes](/help/sites-developing/components.md) para uso com/em Fragmentos de experiência segue as práticas padrão.

A única configuração adicional é garantir que os componentes sejam [permitidos no modelo, isso é feito com a Política](/help/sites-developing/page-templates-editable.md#content-policies)de conteúdo.

## O provedor de regravação do link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

No AEM, você tem a possibilidade de criar Fragmentos de experiência. Um fragmento de experiência:

* consista num grupo de componentes e num esquema,
* pode existir independentemente de uma página do AEM.

Um dos casos de uso desses grupos é para incorporar conteúdo em pontos de contato de terceiros, como o Adobe Target.

### Regravação de link padrão {#default-link-rewriting}

Usando o recurso [Exportar para o Target](/help/sites-administering/experience-fragments-target.md) , é possível:

* criar um fragmento de experiência,
* adicionar componentes a ele,
* e, em seguida, exporte-o como uma oferta do Adobe Target, em Formato HTML ou Formato JSON.

Esse recurso pode ser [ativado em uma instância do autor do AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Ela requer uma Configuração válida do Adobe Target e configurações para o Externalizador de links.

O Externalizador de links é usado para determinar os URLs corretos necessários ao criar a versão HTML da oferta do Target, que é enviada subsequentemente ao Adobe Target. Isso é necessário, pois o Adobe Target exige que todos os links dentro da oferta HTML do Target possam ser acessados publicamente; isso significa que todos os recursos que os links referenciam e o próprio Fragmento de experiência devem ser publicados antes de serem usados.

Por padrão, quando você cria uma oferta HTML do Target, uma solicitação é enviada para um seletor Sling personalizado no AEM. Este seletor é chamado `.nocloudconfigs.html`. Como seu nome implica, cria uma renderização em HTML simples de um Fragmento de experiência, mas não inclui configurações em nuvem (que seriam informações supérfluas).

Depois de gerar a página HTML, o pipeline do Sling Rewriter faz modificações na saída:

1. Os elementos `html`, `head`e `body` são substituídos por `div` elementos. Os elementos `meta`, `noscript` e `title` são removidos (são elementos filho do `head` elemento original e não são considerados quando este é substituído pelo `div` elemento).

   Isso é feito para garantir que a oferta do Target HTML possa ser incluída nas atividades do Target.

1. O AEM modifica todos os links internos presentes no HTML para que apontem para um recurso publicado.

   Para determinar os links a serem modificados, o AEM segue este padrão para atributos de elementos HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src etc)
   1. `*-href` atributos (como `data-href`, `custom-href`, `img-href`etc)
   >[!NOTE]
   >
   >Na maioria dos casos, os links internos no HTML são links relativos, mas pode haver casos em que componentes personalizados fornecem URLs completos no HTML. Por padrão, o AEM ignora esses URLs completos e não faz modificações.

   Os links nesses atributos são executados pelo Externalizador de links do AEM `publishLink()` para recriar o URL como se ele estivesse em uma instância publicada e, como tal, disponível ao público.

Ao usar uma implementação predefinida, o processo descrito acima deve ser suficiente para gerar a oferta do Target a partir do Fragmento de experiência e exportá-la para o Adobe Target. No entanto, existem alguns casos de utilização que não são contabilizados neste processo; eles incluem:

* Mapeamento Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Para esses casos de uso, o AEM fornece a Interface do provedor de regravação de links.

### Interface do provedor de regravador de links {#link-rewriter-provider-interface}

>[!NOTE]
>
>Essa interface foi introduzida no [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Para casos mais complicados, não cobertos pelo [padrão](#default-link-rewriting), o AEM oferece a Interface do provedor de regravação de links. Esta é uma `ConsumerType` interface que você pode implementar em seus pacotes, como um serviço. Ele ignora as modificações que o AEM realiza em links internos de uma oferta HTML como renderizado de um Fragmento de experiência. Essa interface permite que você personalize o processo de regravação de links HTML internos para se alinhar às suas necessidades comerciais.

Exemplos de casos de uso para implementar essa interface como um serviço incluem:

* Mapeamentos Sling são ativados nas instâncias de publicação, mas não na instância do autor
* Um dispatcher ou uma tecnologia semelhante é usada para redirecionar URLs internamente
* Existem recursos `sling:alias mechanisms` disponíveis

>[!NOTE]
>
>Essa interface só processa os links HTML internos da Oferta do Target gerada.

A Interface do provedor de regravação de links ( `ExperienceFragmentLinkRewriterProvider`) é a seguinte:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Como usar a interface do provedor de regravação de links {#how-to-use-the-link-rewriter-provider-interface}

Para usar a interface, primeiro é necessário criar um pacote contendo um novo componente de serviço que implemente a interface do provedor de regravação de links.

Esse serviço será usado para conectar-se à regravação Exportar fragmento de experiência para o Target para ter acesso aos vários links.

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

Para que o serviço funcione, há agora três métodos que precisam ser implementados dentro do serviço:

* ` [shouldRewrite](#shouldrewrite)`
* ` [rewriteLink](#rewritelink)`

   * `rewriteLinkExample2`

* ` [getPriority](#priorities-getpriority)`

#### shouldRewrite {#shouldrewrite}

É necessário indicar ao sistema se ele precisa regravar os links quando uma chamada é feita para Exportar para o Target em uma certa variação do Fragmento de experiência. Você faz isso implementando o método:

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

* para um fragmento de experiência específico:
   `/content/experience-fragment/master`

Quaisquer outros Fragmentos de experiência que passarem pelo sistema Exportar para o Target são ignorados e não são afetados pelas alterações implementadas neste Serviço.

#### rewriteLink {#rewritelink}

Para a variação do Fragmento de experiência impactada pelo processo de regravação, ele continuará permitindo que o serviço controle a regravação do link. Sempre que um link é encontrado no HTML interno, o seguinte método é chamado:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, o método recebe os parâmetros:

* `link`
A `String` representação do link que está sendo processado no momento. Normalmente, é um URL relativo que aponta para o recurso na instância do autor.

* `tag`
O nome do elemento HTML que está sendo processado no momento.

* `attribute`
O nome exato do atributo.

Se, por exemplo, o sistema Exportar para o Target estiver processando esse elemento no momento, você pode definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para o `rewriteLink()` método é feita usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, você pode tomar decisões com base na entrada fornecida e, em seguida, reescrever o link de acordo.

Para nosso exemplo, gostaríamos de remover a parte `/etc.clientlibs` do URL e adicionar o domínio externo apropriado. Para simplificar, consideraremos que temos acesso a um Resolvedor de recursos para seu serviço, como em `rewriteLinkExample2`:

>[!NOTE]
>
>Para obter mais informações sobre como obter um resolvedor de recursos por meio de um usuário de serviço, consulte Usuários [de serviço no AEM](/help/sites-administering/security-service-users.md).

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

Não é incomum precisar de vários serviços para atender a diferentes tipos de Fragmentos de experiência, ou mesmo para ter um Serviço genérico que lida com a externalização e o mapeamento de todos os Fragmentos de experiência. Nesses casos, surgem conflitos sobre qual serviço usar, de modo que o AEM oferece a possibilidade de definir **Prioridades** para diferentes serviços. As prioridades são especificadas usando o método:

* `getPriority()`

Esse método permite o uso de vários serviços nos quais o `shouldRewrite()` método retorna true para o mesmo Fragmento de experiência. O serviço que retorna o maior número de seu `getPriority()`método é o serviço que lida com a Variação do fragmento de experiência.

Por exemplo, você pode ter uma regra `GenericLinkRewriterProvider` que manipula o mapeamento básico de todos os Fragmentos de experiência e quando o `shouldRewrite()` método retorna `true` para todas as Variações de fragmento de experiência. Para vários Fragmentos de experiência específicos, talvez você queira manuseio especial, portanto, nesse caso, você pode fornecer um método `SpecificLinkRewriterProvider` para o qual o `shouldRewrite()` método retorna verdadeiro somente para algumas Variações de fragmento de experiência. Para garantir que `SpecificLinkRewriterProvider` seja escolhido para lidar com essas variações do fragmento de experiência, ele deve retornar em seu `getPriority()` método um número maior que `GenericLinkRewriterProvider.`
