---
title: Personalização da criação de página
description: O Adobe Experience Manager (AEM) fornece vários mecanismos para permitir personalizar a funcionalidade de criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 2%

---

# Personalização da criação de página{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento descreve como personalizar a criação de página na interface moderna e habilitada para toque, e não se aplica à interface clássica.

O Adobe Experience Manager (AEM) fornece vários mecanismos para permitir personalizar a funcionalidade de criação de página (e o [consoles](/help/sites-developing/customizing-consoles-touch.md)) da sua instância de criação.

* Clientlibs

  As clientlibs permitem estender a implementação padrão para obter uma nova funcionalidade, além de reutilizar as funções, os objetos e os métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` A nova clientlib deve:

   * depende da clientlib de criação `cq.authoring.editor.sites.page`
   * fazer parte dos procedimentos `cq.authoring.editor.sites.page.hook` categoria

* Sobreposições

  As sobreposições são baseadas nas definições do nó e permitem sobrepor a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (no `/apps`). Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, pois a [fusão de recursos do sling](/help/sites-developing/sling-resource-merger.md) permite a herança.

>[!NOTE]
>
>Para obter mais informações, consulte [Conjunto de documentação JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Eles podem ser usados de várias maneiras para estender a funcionalidade de criação de página na instância do AEM. Uma seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte o seguinte:
>
>* Uso e criação [clientlibs](/help/sites-developing/clientlibs.md).
>* Uso e criação [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estrutura da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-structure.md) para obter detalhes das áreas estruturais usadas para a criação de páginas.
>


>[!CAUTION]
>
>***Não*** alterar qualquer item no `/libs` caminho.
>
>O motivo é porque o conteúdo de `/libs` for substituído, na próxima vez que você atualizar sua instância (e poderá ser substituído ao aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recrie o item necessário (ou seja, como ele existe em `/libs`) em `/apps`
>1. Fazer alterações em `/apps`

## Adicionar nova camada (modo) {#add-new-layer-mode}

Quando você está editando uma página, há vários [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponíveis. Esses modos são implementados usando [camadas](/help/sites-developing/touch-ui-structure.md#layer). Eles permitem acesso a diferentes tipos de funcionalidade para o mesmo conteúdo de página. As camadas padrão são: editar, visualizar, anotar, desenvolvedor e direcionamento.

### Exemplo de camada: status da Live Copy {#layer-example-live-copy-status}

Uma instância AEM padrão fornece a camada MSM. Isso acessa dados relacionados ao [gerenciamento multisite](/help/sites-administering/msm.md) e o realça na camada.

Para vê-lo em ação, você pode editar qualquer [Cópia de idioma do We.Retail](/help/sites-developing/we-retail-globalized-site-structure.md) (ou qualquer outra página de live copy) e selecione a **Status da Live Copy** modo.

Você pode encontrar a definição da camada MSM (para referência) em:

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### Amostra de código {#code-sample}

Este é um exemplo de pacote que mostra como criar uma camada (modo), que é uma nova camada para a visualização do MSM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-new-layer-mode no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## Adicionar nova categoria de seleção ao navegador de ativos {#add-new-selection-category-to-asset-browser}

O navegador de ativos mostra ativos de vários tipos/categorias (por exemplo, imagens e documentos). Os ativos também podem ser filtrados por essas categorias de ativos.

### Amostra de código {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` é um exemplo de pacote que mostra como adicionar um grupo ao localizador de ativos. Este exemplo se conecta a [Flickr](https://www.flickr.com)fluxo público do e os mostra no painel lateral.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-assetfinder-flickr no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrar recursos {#filtering-resources}

Ao criar páginas, o usuário geralmente deve selecionar entre os recursos (por exemplo, páginas, componentes e ativos). Isso pode tomar a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado no formato de um predicado personalizado. Por exemplo, se a variável [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) for usado para permitir que o usuário selecione o caminho para um recurso específico, os caminhos apresentados poderão ser filtrados da seguinte maneira:

* Implementar o predicado personalizado implementando o [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html) interface.
* Especifique um nome para o predicado e consulte esse nome ao usar o `pathbrowser`.

Para obter mais detalhes sobre como criar um predicado personalizado, consulte [este artigo](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>Implementar um predicado personalizado implementando o `com.day.cq.commons.predicate.AbstractNodePredicate` A interface do também funciona na interface clássica.
>
>Consulte [este artigo da knowledge base](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) para obter um exemplo de implementação de um predicado personalizado na interface clássica.

## Adicionar nova ação a uma barra de ferramentas do componente {#add-new-action-to-a-component-toolbar}

Cada componente (geralmente) tem uma barra de ferramentas que fornece acesso a uma variedade de ações que podem ser executadas nesse componente.

### Amostra de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` é um pacote de amostra que mostra como criar uma ação personalizada da barra de ferramentas para renderizar componentes.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-toolbar-screenshot no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## Adicionar novo editor no local {#add-new-in-place-editor}

### Editor padrão no local {#standard-in-place-editor}

Em uma instalação padrão do AEM:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   Mantém as definições dos vários editores disponíveis.

1. Há uma conexão entre o editor e cada tipo de recurso (como no componente ) que pode usá-lo:

   * `cq:inplaceEditing`

     por exemplo:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * propriedade: `editorType`

           Define o tipo de editor em linha usado quando a edição no local é acionada para esse componente; por exemplo, `text`, `textimage`, `image`, `title`.

1. Detalhes adicionais de configuração do editor podem ser configurados usando um `config` nó contendo configurações e um `plugin` para conter os detalhes necessários da configuração do plug-in.

   Veja a seguir um exemplo de definição de proporções de aspecto para o plug-in de recorte de imagem do componente de imagem. Devido ao potencial de tamanho limitado da tela, as taxas de proporções de corte foram movidas para o editor de tela cheia e só podem ser vistas lá.

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
   >Rácio de colheita de AEM, tal como estabelecido pelo `ratio` são definidos como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários de criação não estarão cientes de qualquer diferença desde que você defina o `name` é exibida claramente, pois é o que é exibido na interface do usuário.

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

`aem-authoring-extension-inplace-editor` é um pacote de amostra que mostra como criar um editor no local no AEM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-inplace-editor no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuração de vários editores no local {#configuring-multiple-in-place-editors}

É possível configurar um componente para que ele tenha vários editores no local. Quando vários editores no local são configurados, é possível selecionar o conteúdo apropriado e abrir o editor apropriado. Consulte a [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md) para obter mais informações.

## Adicionar uma nova ação de página {#add-a-new-page-action}

Para adicionar uma nova ação de página à barra de ferramentas da página, por exemplo, uma **Voltar ao Sites** (console) ação.

### Amostra de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` é um pacote de amostra que mostra como criar uma ação de barra de cabeçalho personalizada para voltar ao console Sites.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abra o projeto aem-authoring-extension-header-backtosites no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizar a solicitação para o fluxo de trabalho de ativação {#customizing-the-request-for-activation-workflow}

O workflow predefinido, **Solicitação para ativação**:

* Será exibido automaticamente no menu apropriado quando um autor de conteúdo **não tem** os direitos de replicação apropriados, mas **tem** associação de usuários e autores do DAM.

* Caso contrário, nada será exibido, pois os direitos de replicação foram removidos.

Para personalizar o comportamento nessa ativação, é possível sobrepor o **Solicitação para ativação** workflow:

1. Entrada `/apps` sobrepor o **Sites** assistente:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Ele mesmo substitui a instância comum de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Atualize o [modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md) e configurações/scripts relacionados, conforme necessário.
1. Remova a direita para a [`replicate` ação](/help/sites-administering/security.md#actions) de todos os usuários apropriados para todas as páginas relevantes; para que esse fluxo de trabalho seja acionado como uma ação padrão quando qualquer um dos usuários tentar publicar (ou replicar) uma página.
