---
title: Personalização da criação de página
seo-title: Personalização da criação de página
description: O AEM fornece vários mecanismos para permitir que você personalize a funcionalidade de criação de página
seo-description: O AEM fornece vários mecanismos para permitir que você personalize a funcionalidade de criação de página
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Personalização da criação de página{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento descreve como personalizar a criação de páginas na interface moderna e habilitada para toque e não se aplica à interface clássica.

O AEM fornece vários mecanismos para permitir que você personalize a funcionalidade de criação de página (e os [consoles](/help/sites-developing/customizing-consoles-touch.md)) da sua instância de criação.

* Clientlibs

   Clientlibs permitem estender a implementação padrão para obter novas funcionalidades, reutilizando funções, objetos e métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` A nova clientlib deve:

   * depender da clientlib de criação `cq.authoring.editor.sites.page`
   * fazer parte da `cq.authoring.editor.sites.page.hook` categoria adequada

* Sobreposições

   As sobreposições são baseadas em definições de nó e permitem que você sobreponha a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, já que a fusão [de recursos](/help/sites-developing/sling-resource-merger.md) sling permite herança.

>[!NOTE]
>
>Para obter mais informações, consulte o conjunto [de documentação do](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)JS.

Eles podem ser usados de várias maneiras para estender a funcionalidade de criação de página na sua instância do AEM. Uma seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Usar e criar [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso e criação de [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estrutura da interface do usuário](/help/sites-developing/touch-ui-structure.md) habilitada para toque do AEM para obter detalhes das áreas estruturais usadas para a criação de página.
>
>
Este tópico também é abordado na sessão do [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) - personalização da interface do [usuário para o AEM 6.0](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>Você não ***deve*** alterar nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recriar o item desejado (isto é, como ele existe em `/libs`) em `/apps`
>1. Faça quaisquer alterações em `/apps`


## Adicionar nova camada (modo) {#add-new-layer-mode}

Quando você está editando uma página, há vários [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponíveis. Esses modos são implementados usando [camadas](/help/sites-developing/touch-ui-structure.md#layer). Eles permitem acesso a diferentes tipos de funcionalidade para o mesmo conteúdo de página. As camadas padrão são: editar, visualizar, anotar, desenvolvedor e segmentação.

### Exemplo de camada: Status da Live Copy {#layer-example-live-copy-status}

Uma instância AEM padrão fornece a camada MSM. Isso acessa dados relacionados ao gerenciamento [de](/help/sites-administering/msm.md) vários sites e os destaca na camada.

Para vê-la em ação, você pode editar qualquer página de cópia [de idioma](/help/sites-developing/we-retail-globalized-site-structure.md) We.Retail (ou qualquer outra página de cópia ao vivo) e selecionar o modo Status **da Cópia** online.

Você pode encontrar a definição de camada MSM (para referência) em:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Exemplo de código {#code-sample}

Este é um pacote de amostra que mostra como criar uma nova camada (modo), que é uma nova camada para a exibição MSM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir projeto aem-authoring-new-layer-mode no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Adicionar nova categoria de seleção ao navegador de ativos {#add-new-selection-category-to-asset-browser}

O navegador de ativos mostra ativos de vários tipos/categorias (por exemplo, imagem, documentos etc.). Os ativos também podem ser filtrados por essas categorias de ativos.

### Exemplo de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` é um pacote de amostra que mostra como adicionar um novo grupo ao localizador de ativos. Este exemplo se conecta ao fluxo público do [Flickr](https://www.flickr.com)e os mostra no painel lateral.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-assetfinder-flickr no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrar recursos {#filtering-resources}

Durante a criação de páginas, o usuário geralmente deve selecionar entre os recursos (por exemplo, páginas, componentes, ativos etc.). Isso pode assumir a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado na forma de um predicado personalizado. Por exemplo, se o componente [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) Granite [](/help/sites-developing/touch-ui-concepts.md#granite-ui) for usado para permitir que o usuário selecione o caminho para um recurso específico, os caminhos apresentados podem ser filtrados da seguinte maneira:

* Implemente o predicado personalizado implementando a [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) interface.
* Especifique um nome para o predicado e consulte esse nome ao usar o `pathbrowser`.

Para obter mais detalhes sobre como criar um predicado personalizado, consulte [este artigo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>A implementação de um predicado personalizado por meio da implementação da interface também funciona na interface clássica. `com.day.cq.commons.predicate.AbstractNodePredicate`
>
>Consulte [este artigo](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) da base de conhecimento para obter um exemplo de como implementar um predicado personalizado na interface clássica.

## Adicionar nova ação a uma barra de ferramentas do componente {#add-new-action-to-a-component-toolbar}

Cada componente (normalmente) tem uma barra de ferramentas que fornece acesso a uma variedade de ações que podem ser realizadas nesse componente.

### Exemplo de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` é um pacote de amostra que mostra como criar uma ação personalizada da barra de ferramentas para renderizar componentes.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-toolbar-screenshot no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Adicionar novo editor local {#add-new-in-place-editor}

### Editor no local padrão {#standard-in-place-editor}

Em uma instalação padrão do AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Mantém definições dos vários editores disponíveis.

1. Há uma conexão entre o editor e cada tipo de recurso (como no componente) que pode usá-lo:

   * `cq:inplaceEditing`

      por exemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propriedade: `editorType`

            Define o tipo de editor em linha que será usado quando a edição no local for acionada para esse componente;por exemplo `text`, `textimage`, `image`, `title`.

1. Detalhes adicionais de configuração do editor podem ser configurados usando um `config` nó contendo configurações, bem como um outro `plugin` nó para conter os detalhes necessários de configuração do plug-in.

   A seguir está um exemplo de definição de proporções para o plug-in de corte de imagem do componente de imagem. Observe que, devido ao potencial de tamanho de tela muito limitado, as proporções de aspecto de corte foram movidas para o editor de tela cheia e só podem ser vistas lá.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >Observe que nas relações de corte do AEM, conforme definidas pela `ratio` propriedade, são definidas como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. The authoring users will not be aware of any difference provided you define the `name` property clearly since this is what is displayed in the UI.

#### Criar um novo editor no local {#creating-a-new-in-place-editor}

Para implementar um novo editor no local (na clientlib):

>[!NOTE]
>
>Por exemplo, consulte:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementação:

   * `setUp`
   * `tearDown`

1. Registre o editor (inclui o construtor):

   * `editor.register`

1. Forneça a conexão entre o editor e cada tipo de recurso (como no componente) que pode usá-lo.

#### Amostra de código para criar um novo editor no local {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` é um pacote de amostra que mostra como criar um novo editor no local no AEM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-inplace-editor no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuração de vários editores no local {#configuring-multiple-in-place-editors}

É possível configurar um componente para que ele tenha vários editores no local. Quando vários editores no local estiverem configurados, você poderá selecionar o conteúdo apropriado e abrir o editor apropriado. Consulte a documentação [Configuração de vários editores](/help/sites-developing/multiple-inplace-editors.md) no local para obter mais informações.

## Add a New Page Action {#add-a-new-page-action}

Para adicionar uma nova ação de página à barra de ferramentas da página, por exemplo, uma ação **Voltar aos sites** (console).

### Exemplo de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` é um exemplo de pacote que mostra como criar uma ação personalizada da barra de cabeçalho para voltar ao console Sites.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-header-backtosites no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalização do fluxo de trabalho de solicitação de ativação {#customizing-the-request-for-activation-workflow}

O fluxo de trabalho predefinido, **Solicitação de ativação**, é acionado automaticamente quando um autor de conteúdo não tem os direitos de replicação apropriados.

Para ter um comportamento personalizado nessa ativação, é possível sobrepor o fluxo de trabalho **Solicitar ativação** :

1. Em `/apps` sobrepor o assistente **Sites** :

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Isso mesmo substitui a instância comum de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Atualize o modelo [de](/help/sites-developing/workflows-models.md) fluxo de trabalho e as configurações/scripts relacionados, conforme necessário.
1. Retirar o direito à [`replicate` ação](/help/sites-administering/security.md#actions) de todos os utilizadores apropriados para todas as páginas relevantes; para que esse fluxo de trabalho seja acionado como uma ação padrão quando qualquer um dos usuários tentar publicar (ou replicar) uma página.

