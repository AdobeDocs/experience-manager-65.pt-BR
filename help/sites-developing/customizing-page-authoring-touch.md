---
title: Personalização da criação de página
description: O Adobe Experience Manager (AEM) fornece vários mecanismos para permitir personalizar a funcionalidade de criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 3aa55b88f589749fb49d5ff46340b0912d490157
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---

# Personalização da criação de página{#customizing-page-authoring}

>[!CAUTION]
>
>Este documento descreve como personalizar a criação de página na interface moderna e habilitada para toque, e não se aplica à interface clássica.

O Adobe Experience Manager (AEM) fornece vários mecanismos para permitir que você personalize a funcionalidade de criação de página (e os [consoles](/help/sites-developing/customizing-consoles-touch.md)) da sua instância de criação.

* Clientlibs

  As clientlibs permitem estender a implementação padrão para obter uma nova funcionalidade, além de reutilizar as funções, os objetos e os métodos padrão. Ao personalizar, você pode criar sua própria clientlib em `/apps.` A nova clientlib deve:

   * depende da clientlib de criação `cq.authoring.editor.sites.page`
   * fazer parte da categoria `cq.authoring.editor.sites.page.hook` apropriada

* Sobreposições

  As sobreposições são baseadas nas definições de nó e permitem sobrepor a funcionalidade padrão (em `/libs`) com sua própria funcionalidade personalizada (em `/apps`). Ao criar uma sobreposição, uma cópia 1:1 do original não é necessária, pois a [fusão de recursos de sling](/help/sites-developing/sling-resource-merger.md) permite a herança.

>[!NOTE]
>
>Para obter mais informações, consulte [Conjunto de documentação JS](https://developer.adobe.com/experience-manager/reference-materials/6-5/jsdoc/ui-touch/editor-core/index.html).

Eles podem ser usados de várias maneiras para estender a funcionalidade de criação de página na instância do AEM. Uma seleção é abordada abaixo (em um nível alto).

>[!NOTE]
>
>Para obter mais informações, consulte o seguinte:
>
>* Usando e criando [clientlibs](/help/sites-developing/clientlibs.md).
>* Usando e criando [sobreposições](/help/sites-developing/overlays.md).
>* [Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [Estrutura da interface habilitada para toque por AEM](/help/sites-developing/touch-ui-structure.md) para obter detalhes das áreas estruturais usadas para criação de página.
>


>[!CAUTION]
>
>***Não*** altere nada no caminho `/libs`.
>
>O motivo é que o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).
>
>O método recomendado para configuração e outras alterações é:
>
>1. Recriar o item necessário (isto é, como ele existe em `/libs`) em `/apps`
>1. Fazer alterações em `/apps`

## Adicionar nova camada (modo) {#add-new-layer-mode}

Quando você está editando uma página, há vários [modos](/help/sites-authoring/author-environment-tools.md#page-modes) disponíveis. Estes modos são implementados usando [camadas](/help/sites-developing/touch-ui-structure.md#layer). Eles permitem acesso a diferentes tipos de funcionalidade para o mesmo conteúdo de página. As camadas padrão são: editar, visualizar, anotar, desenvolvedor e direcionamento.

### Exemplo de camada: status da Live Copy {#layer-example-live-copy-status}

Uma instância AEM padrão fornece a camada MSM. Isso acessa os dados relacionados ao [gerenciamento multissite](/help/sites-administering/msm.md) e os destaca na camada.

Para vê-lo em ação, você pode editar qualquer página do [We.Retail de cópia de idioma](/help/sites-developing/we-retail-globalized-site-structure.md) (ou qualquer outra página de live copy) e selecionar o modo **Status da Live Copy**.

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

`aem-authoring-extension-assetfinder-flickr` é um exemplo de pacote que mostra como adicionar um grupo ao localizador de ativos. Este exemplo conecta-se ao fluxo público do [Flickr](https://www.flickr.com) e os mostra no painel lateral.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-assetfinder-flickr no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## Filtrar recursos {#filtering-resources}

Ao criar páginas, o usuário geralmente deve selecionar entre os recursos (por exemplo, páginas, componentes e ativos). Isso pode tomar a forma de uma lista, por exemplo, da qual o autor deve escolher um item.

Para manter a lista em um tamanho razoável e também relevante para o caso de uso, um filtro pode ser implementado no formato de um predicado personalizado. Por exemplo, se o componente [`pathbrowser`](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) for usado para permitir que o usuário selecione o caminho para um recurso específico, os caminhos apresentados poderão ser filtrados da seguinte maneira:

* Implemente o predicado personalizado implementando a interface [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/commons/predicate/package-summary.html).
* Especifique um nome para o predicado e consulte esse nome ao usar o `pathbrowser`.

Para obter mais detalhes sobre como criar um predicado personalizado, consulte [Implementando um Avaliador de Predicado Personalizado para o Construtor de Consultas](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>A implementação de um predicado personalizado implementando a interface `com.day.cq.commons.predicate.AbstractNodePredicate` também funciona na interface clássica.
>
>Consulte [este artigo da base de dados de conhecimento](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) para obter um exemplo de implementação de um predicado personalizado na interface clássica.

## Adicionar nova ação a uma barra de ferramentas do componente {#add-new-action-to-a-component-toolbar}

Cada componente (geralmente) tem uma barra de ferramentas que fornece acesso a uma variedade de ações que podem ser executadas nesse componente.

### Amostra de código {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` é um exemplo de pacote que mostra como criar uma ação personalizada na barra de ferramentas para renderizar componentes.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-toolbar-screenshot no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
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

           Define o tipo de editor embutido usado quando a edição no local é acionada para esse componente; por exemplo, `text`, `textimage`, `image`, `title`.

1. Detalhes adicionais de configuração do editor podem ser configurados usando um nó `config` contendo configurações e um nó `plugin` para conter os detalhes necessários de configuração do plug-in.

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
   >As taxas de corte do AEM, conforme definidas pela propriedade `ratio`, estão definidas como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários da criação não estarão cientes de qualquer diferença desde que você defina a propriedade `name` claramente, pois ela é exibida na interface do usuário.

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

`aem-authoring-extension-inplace-editor` é um exemplo de pacote que mostra como criar um editor local no AEM.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-inplace-editor no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### Configuração de vários editores no local {#configuring-multiple-in-place-editors}

É possível configurar um componente para que ele tenha vários editores no local. Quando vários editores no local são configurados, é possível selecionar o conteúdo apropriado e abrir o editor apropriado. Consulte a documentação [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md) para obter mais informações.

## Adicionar uma nova ação de página {#add-a-new-page-action}

Para adicionar uma nova ação de página à barra de ferramentas da página, por exemplo, uma ação **Voltar aos Sites** (console).

### Amostra de código {#code-sample-3}

`aem-authoring-extension-header-backtosites` é um exemplo de pacote que mostra como criar uma ação de barra de cabeçalho personalizada para voltar ao console de Sites.

CÓDIGO NO GITHUB

Você pode encontrar o código desta página no GitHub

* [Abrir o projeto aem-authoring-extension-header-backtosites no GitHub](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* Baixar o projeto como [um arquivo ZIP](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## Personalizar a solicitação para o fluxo de trabalho de ativação {#customizing-the-request-for-activation-workflow}

O workflow predefinido, **Solicitação de ativação**:

* Aparecerá automaticamente no menu apropriado quando um autor de conteúdo **não tiver** os direitos de replicação apropriados, mas **tiver** associação de Usuários e Autores do DAM.

* Caso contrário, nada será exibido, pois os direitos de replicação foram removidos.

Para personalizar o comportamento nessa ativação, é possível sobrepor o fluxo de trabalho **Solicitação de ativação**:

1. Em `/apps` sobrepor o assistente de **Sites**:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >Ele mesmo substitui a instância comum de:
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. Atualize o [modelo de fluxo de trabalho](/help/sites-developing/workflows-models.md) e as configurações/scripts relacionados, conforme necessário.
1. Remova o direito à ação [`replicate`](/help/sites-administering/security.md#actions) de todos os usuários apropriados para todas as páginas relevantes; para que esse fluxo de trabalho seja acionado como uma ação padrão quando qualquer um dos usuários tentar publicar (ou replicar) uma página.
