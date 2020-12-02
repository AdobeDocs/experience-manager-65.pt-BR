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
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 3%

---


# Fragmentos de experiência{#experience-fragments}

## Noções básicas {#the-basics}

Um [Fragmento de experiência](/help/sites-authoring/experience-fragments.md) é um grupo de um ou mais componentes, incluindo o conteúdo e o layout que podem ser referenciados nas páginas.

Um Fragmento de experiência Principal e/ou uma Variante usa:

* `sling:resourceType` : `/libs/cq/experience-fragments/components/xfpage`

Como não há `/libs/cq/experience-fragments/components/xfpage/xfpage.html`, ele reverte para

* `sling:resourceSuperType` :  `wcm/foundation/components/page`

## A representação HTML simples {#the-plain-html-rendition}

Usando o seletor `.plain.` no URL, você pode acessar a execução HTML simples.

Isso está disponível no navegador, mas seu objetivo principal é permitir que outros aplicativos (por exemplo, aplicativos da Web de terceiros, implementações móveis personalizadas) acessem o conteúdo do Fragmento de experiência diretamente, usando apenas o URL.

A execução HTML simples adiciona o protocolo, o host e o caminho de contexto aos caminhos que são:

* do tipo: `src`, `href` ou `action`

* ou terminar com: `-src`, ou `-href`

Por exemplo:

`.../brooklyn-coat/master.plain.html`

>[!NOTE]
>
>Os links sempre fazem referência à instância de publicação. Eles devem ser consumidos por terceiros, de modo que o link sempre será chamado da instância de publicação, não do autor.

![xf-12](assets/xf-14.png)

O seletor de representação simples usa um transformador em vez de scripts adicionais; o [Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) é usado como o transformador. Isso está configurado em

* `/libs/experience-fragments/config/rewriter/experiencefragments`

## Variações sociais {#social-variations}

As variantes sociais podem ser postadas em redes sociais (texto e imagem). AEM estas variantes sociais podem conter componentes; por exemplo, componentes de texto, componentes de imagem.

A imagem e o texto da publicação social podem ser obtidos de qualquer tipo de recurso de imagem ou de recurso de texto em qualquer nível de profundidade (no bloco de construção ou no container de layout).

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
>****** [Somente ](/help/sites-developing/page-templates-editable.md) modelos editáveis são suportados em Fragmentos de experiência.

Ao desenvolver um novo modelo para Fragmentos de experiência, você pode seguir as práticas padrão para um [modelo editável](/help/sites-developing/page-templates-editable.md).

Para criar um modelo de fragmento de experiência detectado pelo assistente **Criar fragmento de experiência**, siga um destes conjuntos de regras:

1. Ambos:

   1. O tipo de recurso do modelo (o nó inicial) deve herdar de:
      `cq/experience-fragments/components/xfpage`

   1. E o nome do modelo deve começar com:
      `experience-fragments`
Isso permite que os usuários criem fragmentos de experiência em /content/experience-fragments como a variável 
`cq:allowedTemplates` a propriedade desta pasta inclui todos os modelos que têm nomes começando com  `experience-fragment`. Os clientes podem atualizar essa propriedade para incluir seus próprios esquemas de nomeação ou locais de modelo.

1. [Os ](/help/sites-authoring/experience-fragments.md#configure-allowed-templates-folder) modelos permitidos podem ser configurados no console Fragmentos de experiência.

<!--
1. Add the template details manually in `cq:allowedTemplates` on the `/content/experience-fragment` node.
-->

<!-- >[!NOTE]
>
>[Allowed templates](/help/sites-authoring/experience-fragments.md#configuring-allowed-templates) can be configured in the Experience Fragments console.
-->

## Componentes para fragmentos de experiência {#components-for-experience-fragments}

[O desenvolvimento de ](/help/sites-developing/components.md) componentes para uso com/em Fragmentos de experiência segue as práticas padrão.

A única configuração adicional é garantir que os componentes sejam [permitidos no modelo, isso é obtido com a Política de conteúdo](/help/sites-developing/page-templates-editable.md#content-policies).

## O provedor de regravação do link do fragmento de experiência - HTML {#the-experience-fragment-link-rewriter-provider-html}

AEM você tem a possibilidade de criar Fragmentos de experiência. Um fragmento de experiência:

* consista num grupo de componentes e num esquema,
* pode existir independentemente de uma página AEM.

Um dos casos de uso desses grupos é para a incorporação de conteúdo em pontos de contato de terceiros, como o Adobe Target.

### Regravação de link padrão {#default-link-rewriting}

Usando o recurso [Exportar para Público alvo](/help/sites-administering/experience-fragments-target.md), você pode:

* criar um fragmento de experiência,
* adicionar componentes a ele,
* e, em seguida, exporte-o como uma Oferta Adobe Target, em Formato HTML ou Formato JSON.

Este recurso pode ser [ativado em uma instância do autor de AEM](/help/sites-administering/experience-fragments-target.md#Prerequisites). Requer uma Configuração Adobe Target válida e configurações para o Externalizador de links.

O Externalizador de links é usado para determinar os URLs corretos necessários ao criar a versão HTML da Oferta do Público alvo, que é enviada subsequentemente à Adobe Target. Isso é necessário, pois a Adobe Target exige que todos os links dentro da Oferta HTML do Público alvo possam ser acessados publicamente; isso significa que todos os recursos que os links referenciam e o próprio Fragmento de experiência devem ser publicados antes que possam ser usados.

Por padrão, quando você constrói uma Oferta HTML de Público alvo, uma solicitação é enviada para um seletor Sling personalizado no AEM. Este seletor é chamado `.nocloudconfigs.html`. Como seu nome implica, cria uma renderização em HTML simples de um Fragmento de experiência, mas não inclui configurações em nuvem (que seriam informações supérfluas).

Depois de gerar a página HTML, o pipeline do Sling Rewriter faz modificações na saída:

1. Os elementos `html`, `head` e `body` são substituídos pelos elementos `div`. Os elementos `meta`, `noscript` e `title` são removidos (são elementos filho do elemento `head` original e não são considerados quando este é substituído pelo elemento `div`).

   Isso é feito para garantir que a Oferta Público alvo HTML possa ser incluída nas Atividades do Público alvo.

1. AEM modifica todos os links internos presentes no HTML para que apontem para um recurso publicado.

   Para determinar os links a serem modificados, AEM este padrão para os atributos de elementos HTML:

   1. `src` atributos
   1. `href` atributos
   1. `*-src` atributos (como data-src, custom-src etc)
   1. `*-href` atributos (como  `data-href`,  `custom-href`,  `img-href`etc)

   >[!NOTE]
   >
   >Na maioria dos casos, os links internos no HTML são links relativos, mas pode haver casos em que os componentes personalizados fornecem URLs completos no HTML. Por padrão, o AEM ignora esses URLs completos e não faz modificações.

   Os links nesses atributos são executados pelo AEM Link Externalizer `publishLink()` para recriar o URL como se ele estivesse em uma instância publicada e, como tal, disponível ao público.

Ao usar uma implementação predefinida, o processo descrito acima deve ser suficiente para gerar a Oferta do Público alvo a partir do Fragmento de experiência e exportá-la para a Adobe Target. No entanto, existem alguns casos de utilização que não são tidos em conta neste processo; eles incluem:

* Mapeamento Sling disponível somente na instância de publicação
* Redirecionamentos do Dispatcher

Para esses casos de uso, AEM fornece a Interface do provedor de regravação de links.

### Interface do provedor de regravação de links {#link-rewriter-provider-interface}

>[!NOTE]
>
>Essa interface foi introduzida em [AEM 6.5 SP1 (6.5.1.0)](/help/release-notes/sp-release-notes.md).

Para casos mais complicados, não abordados pelo [default](#default-link-rewriting), AEM a Interface do provedor de regravação de links. Esta é uma interface `ConsumerType` que você pode implementar em seus pacotes, como um serviço. Ele ignora as modificações AEM executadas em links internos de uma oferta HTML como renderizado de um Fragmento de experiência. Essa interface permite que você personalize o processo de regravação de links HTML internos para alinhar-se às suas necessidades comerciais.

Exemplos de casos de uso para implementar essa interface como um serviço incluem:

* Mapeamentos Sling são ativados nas instâncias de publicação, mas não na instância do autor
* Um dispatcher ou uma tecnologia semelhante é usada para redirecionar URLs internamente
* Há `sling:alias mechanisms` no lugar para recursos

>[!NOTE]
>
>Essa interface só processa os links HTML internos da Oferta de Público alvo gerada.

A Interface do provedor do regrador de links ( `ExperienceFragmentLinkRewriterProvider`) é a seguinte:

```java
public interface ExperienceFragmentLinkRewriterProvider {

    String rewriteLink(String link, String tag, String attribute);

    boolean shouldRewrite(ExperienceFragmentVariation experienceFragment);

    int getPriority();

}
```

### Como usar a Interface do provedor de regravação de links {#how-to-use-the-link-rewriter-provider-interface}

Para usar a interface, primeiro é necessário criar um pacote contendo um novo componente de serviço que implemente a interface do provedor de regravação de links.

Esse serviço será usado para conectar-se à Exportação de fragmento de experiência para regravação de Público alvo, a fim de ter acesso aos vários links.

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

É necessário indicar ao sistema se ele precisa regravar os links quando uma chamada for feita para Exportar para o Público alvo em uma certa variação do Fragmento de experiência. Você faz isso implementando o método:

`shouldRewrite(ExperienceFragmentVariation experienceFragment);`

Por exemplo:

```java
@Override
public boolean shouldRewrite(ExperienceFragmentVariation experienceFragment) {
    return experienceFragment.getPath().equals("/content/experience-fragment/master");
}
```

Esse método recebe, como parâmetro, a Variação do fragmento de experiência que o sistema Exportar para o Público alvo está reescrevendo no momento.

No exemplo acima, gostaríamos de reescrever:

* links presentes em `src`

* `href` somente atributos

* para um fragmento de experiência específico:
   `/content/experience-fragment/master`

Quaisquer outros Fragmentos de experiência que passarem pelo sistema Exportar para o Público alvo são ignorados e não são afetados pelas alterações implementadas neste Serviço.

#### rewriteLink {#rewritelink}

Para a variação do Fragmento de experiência impactada pelo processo de regravação, ele continuará permitindo que o serviço controle a regravação do link. Sempre que um link é encontrado no HTML interno, o seguinte método é chamado:

`rewriteLink(String link, String tag, String attribute)`

Como entrada, o método recebe os parâmetros:

* `link`
A 
`String` representação do link que está sendo processado no momento. Normalmente, é um URL relativo que aponta para o recurso na instância do autor.

* `tag`
O nome do elemento HTML que está sendo processado no momento.

* `attribute`
O nome exato do atributo.

Se, por exemplo, o sistema Exportar para Público alvo estiver processando atualmente esse elemento, você pode definir `CSSInclude` como:

```java
<link rel="stylesheet" href="/etc.clientlibs/foundation/clientlibs/main.css" type="text/css">
```

A chamada para o método `rewriteLink()` é feita usando estes parâmetros:

```java
rewriteLink(link="/etc.clientlibs/foundation/clientlibs/main.css", tag="link", attribute="href" )
```

Ao criar o serviço, você pode tomar decisões com base na entrada fornecida e, em seguida, reescrever o link de acordo.

Para nosso exemplo, gostaríamos de remover a parte `/etc.clientlibs` do URL e adicionar o domínio externo apropriado. Para simplificar, consideraremos que temos acesso a um Resolvedor de Recursos para seu serviço, como em `rewriteLinkExample2`:

>[!NOTE]
>
>Para obter mais informações sobre como obter um resolvedor de recursos por meio de um usuário de serviço, consulte [Usuários do serviço em AEM](/help/sites-administering/security-service-users.md).

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
>Se o método acima retornar `null`, o sistema Exportar para o Público alvo deixará o link como está, um link relativo para um recurso.

#### Prioridades - getPriority {#priorities-getpriority}

Não é incomum precisar de vários serviços para atender a diferentes tipos de Fragmentos de experiência, ou mesmo para ter um Serviço genérico que lida com a externalização e o mapeamento de todos os Fragmentos de experiência. Nesses casos, surgem conflitos sobre qual serviço usar, portanto AEM a possibilidade de definir **Prioridades** para diferentes serviços. As prioridades são especificadas usando o método:

* `getPriority()`

Este método permite o uso de vários serviços nos quais o método `shouldRewrite()` retorna verdadeiro para o mesmo Fragmento de experiência. O serviço que retorna o maior número de seu método `getPriority()`é o serviço que lida com a Variação do fragmento de experiência.

Como exemplo, você pode ter um `GenericLinkRewriterProvider` que manipula o mapeamento básico de todos os Fragmentos de experiência e quando o método `shouldRewrite()` retorna `true` para todas as Variações de fragmento de experiência. Para vários Fragmentos de experiência específicos, talvez você queira manuseio especial, portanto, nesse caso, você pode fornecer um `SpecificLinkRewriterProvider` para o qual o método `shouldRewrite()` retorna verdadeiro somente para algumas Variações de fragmento de experiência. Para garantir que `SpecificLinkRewriterProvider` seja escolhido para lidar com essas Variações de fragmento de experiência, ele deve retornar em seu método `getPriority()` um número maior que `GenericLinkRewriterProvider.`
