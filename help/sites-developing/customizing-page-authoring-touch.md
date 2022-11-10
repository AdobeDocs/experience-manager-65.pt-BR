---
title: Personalização da criação de página
seo-title: Customizing Page Authoring
description: O AEM fornece vários mecanismos para permitir a personalização da funcionalidade de criação de página
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '1354'
ht-degree: 2%

---

# Personalização da criação de página{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento descreve como personalizar a criação de páginas na interface do usuário moderna e habilitada para toque e não se aplica à interface do usuário clássica.

O AEM fornece vários mecanismos para permitir a personalização da funcionalidade de criação de página (e o [consoles](/help/sites-developing/customizing-consoles-touch.md)) da sua instância de criação.

* Clientlibs

   Clientlibs permitem estender a implementação padrão para realizar novas funcionalidades, enquanto reutiliza as funções, objetos e métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` A nova clientlib deve:

   * dependa da clientlib de criação `cq.authoring.editor.sites.page`
   * fazer parte do `cq.authoring.editor.sites.page.hook` categoria

* Sobreposições

   As sobreposições são baseadas nas definições de nó e permitem que você sobreponha a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, não é necessária uma cópia 1:1 do original, já que [fusão de recursos sling](/help/sites-developing/sling-resource-merger.md) permite herança.

>[!NOTE]
>
>Para obter mais informações, consulte o [Conjunto de documentação JS](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

Elas podem ser usadas de várias maneiras para estender a funcionalidade de criação de página na sua instância do AEM. Uma seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte:
>
>* Uso e criação [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso e criação [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estrutura da interface de usuário habilitada para toque do AEM](/help/sites-developing/touch-ui-structure.md) para obter detalhes sobre as áreas estruturais usadas para criação de página.
>



>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) `/apps`
>1. Faça quaisquer alterações no `/apps`


## Adicionar nova camada (modo) {#add-new-layer-mode}

Quando você edita uma página, há várias [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponível. Esses modos são implementados usando [camadas](/help/sites-developing/touch-ui-structure.md#layer). Eles permitem o acesso a diferentes tipos de funcionalidade para o mesmo conteúdo da página. As camadas padrão são: editar, visualizar, anotar, desenvolvedor e definição de metas.

### Exemplo de camada: Status da Live Copy {#layer-example-live-copy-status}

Uma instância de AEM padrão fornece a camada MSM. Isso acessa dados relacionados a [gerenciamento de vários sites](/help/sites-administering/msm.md) e o destaca na camada.

Para vê-lo em ação, você pode editar qualquer [Cópia de idioma We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) e selecione a página (ou qualquer outra página de Live Copy) **Status da Live Copy** modo.

Você pode encontrar a definição de camada do MSM (para referência) em:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Amostra de código {#code-sample}

Este é um pacote de amostra que mostra como criar uma nova camada (modo), que é uma nova camada para a exibição MSM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-new-layer-mode no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Adicionar nova categoria de seleção ao navegador de ativos {#add-new-selection-category-to-asset-browser}

O navegador de ativos mostra ativos de vários tipos/categorias (por exemplo, imagem, documentos etc.). Os ativos também podem ser filtrados por essas categorias de ativos.

### Amostra de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` é um pacote de amostra que mostra como adicionar um novo grupo ao localizador de ativos. Este exemplo se conecta a [Flickr](https://www.flickr.com)O fluxo público do e o exibe no painel lateral.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-assetfinder-flickr no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrar recursos {#filtering-resources}

Ao criar páginas, o usuário geralmente deve selecionar entre os recursos (por exemplo, páginas, componentes, ativos etc.). Isso pode assumir a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado na forma de um predicado personalizado. Por exemplo, se a variável [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) é usado para permitir que o usuário selecione o caminho para um recurso específico, os caminhos apresentados podem ser filtrados da seguinte maneira:

* Implementar o predicado personalizado ao implementar [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) interface.
* Especifique um nome para o predicado e faça referência a esse nome ao usar a variável `pathbrowser`.

Para obter mais detalhes sobre como criar um predicado personalizado, consulte [este artigo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementar um predicado personalizado ao implementar `com.day.cq.commons.predicate.AbstractNodePredicate` A interface do também funciona na interface clássica.
>
>Consulte [este artigo da base de conhecimento](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) para obter um exemplo da implementação de um predicado personalizado na interface clássica.

## Adicionar nova ação a uma barra de ferramentas de componentes {#add-new-action-to-a-component-toolbar}

Cada componente (geralmente) tem uma barra de ferramentas que fornece acesso a uma variedade de ações que podem ser executadas nesse componente.

### Amostra de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` é um pacote de amostra que mostra como criar uma ação personalizada da barra de ferramentas para renderizar componentes.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-toolbar-screenshot no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Adicionar novo editor no local {#add-new-in-place-editor}

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

            Define o tipo de editor em linha que será usado quando a edição no local for acionada para esse componente; por exemplo `text`, `textimage`, `image`, `title`.

1. Detalhes adicionais de configuração do editor podem ser configurados usando um `config` nó contendo configurações, bem como um outro `plugin` nó para conter os detalhes necessários da configuração do plug-in.

   Veja a seguir um exemplo de definição de taxas de proporção para o plug-in de corte de imagem do componente de imagem. Observe que devido ao potencial do tamanho de tela muito limitado, as proporções do corte de corte foram movidas para o editor de tela cheia e só podem ser vistas lá.

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
   >Observe que, em AEM proporções de corte, conforme definido pela variável `ratio` , são definidas como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários da criação não estarão cientes de qualquer diferença desde que você defina a variável `name` claramente, já que isso é exibido na interface do usuário.

#### Criação de um novo editor no local {#creating-a-new-in-place-editor}

Para implementar um novo editor no local (na clientlib):

>[!NOTE]
>
>Por exemplo, consulte:
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. Implementar:

   * `setUp`
   * `tearDown`

1. Registre o editor (inclui o construtor):

   * `editor.register`

1. Forneça a conexão entre o editor e cada tipo de recurso (como no componente) que pode usá-lo.

#### Amostra de código para criar um novo editor no local {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` é um pacote de amostra que mostra como criar um novo editor no local no AEM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-in-place-editor no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuração de vários editores no local {#configuring-multiple-in-place-editors}

É possível configurar um componente para que ele tenha vários editores no local. Quando vários editores no local estiverem configurados, você poderá selecionar o conteúdo apropriado e abrir o editor apropriado. Consulte a [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md) documentação para obter mais informações.

## Adicionar uma nova ação de página {#add-a-new-page-action}

Para adicionar uma nova ação de página à barra de ferramentas da página, por exemplo, uma **Voltar aos sites** (console).

### Amostra de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` é um pacote de exemplo que mostra como criar uma ação personalizada da barra de cabeçalho para saltar de volta para o console Sites .

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-header-backtosites no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Baixe o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalização do fluxo de trabalho da solicitação de ativação {#customizing-the-request-for-activation-workflow}

O fluxo de trabalho pronto para uso, **Solicitação de ativação**:

* Será exibido automaticamente no menu apropriado quando um autor de conteúdo **não tem** os direitos de replicação apropriados, mas **tem** associação de usuários e autores do DAM.

* Caso contrário, nada será exibido, pois os direitos de replicação foram removidos.

Para ter um comportamento personalizado nessa ativação, você pode sobrepor o **Solicitação de ativação** fluxo de trabalho:

1. Em `/apps` sobreponha a **Sites** assistente:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Isso mesmo substitui a instância comum de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Atualize o [modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md) e configurações/scripts relacionados, conforme necessário.
1. Remova o direito do [ `replicate` ação](/help/sites-administering/security.md#actions) de todos os utilizadores apropriados para todas as páginas relevantes; para que esse fluxo de trabalho seja acionado como uma ação padrão quando qualquer um dos usuários tentar publicar (ou replicar) uma página.
