---
title: Configure o Editor de Rich Text para criar conteúdo no Adobe Experience Manager.
description: Saiba como configurar o Editor de rich text do Adobe Experience Manager para criar conteúdo no Adobe Experience Manager.
contentOwner: AG
exl-id: 2e7ec22f-0856-44c4-bb15-1086dae0b85a
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2887'
ht-degree: 0%

---

# Configurar o editor de rich text {#configure-the-rich-text-editor}

O Editor de Rich Text (RTE) fornece aos autores uma ampla variedade de funcionalidades para editar seu conteúdo de texto. Ícones, caixas de seleção, barra de ferramentas e menus são fornecidos para uma experiência de edição de texto WYSIWYG.

Para saber como usar os recursos de RTE para criação, consulte [Usar editor de rich text para criação](/help/sites-authoring/rich-text-editor.md). O RTE pode ser configurado para ativar, desativar e estender os recursos disponíveis nos componentes de criação. O fluxo de trabalho a seguir ilustra uma ordem recomendada para concluir as tarefas de configuração de RTE no Experience Manager.

![Sequência de etapas para saber como configurar o RTE](assets/rte_workflow_v1.png)

*Figura: Sequência de etapas para saber como configurar o RTE*

## Compreender a interface habilitada para toque e a interface clássica {#understand-touch-enabled-ui-and-classic-ui}

A interface habilitada para toque é a interface padrão do usuário para Experience Manager. O Adobe introduziu a interface habilitada para toque com [design responsivo](/help/sites-authoring/responsive-layout.md) para ambiente de criação. A interface habilitada para toque foi projetada para dispositivos de toque e desktop. A interface difere consideravelmente da interface clássica original.

![Barra de ferramentas do Editor de Rich Text na interface habilitada para toque](assets/chlimage_1-35.png)

*Figura: barra de ferramentas do Editor de rich text na interface habilitada para toque*

![Barra de ferramentas do Editor de Rich Text na interface clássica](assets/rtedefault.png)

*Figura: Barra de ferramentas do Editor de Rich Text na interface clássica*

>[!MORELIKETHIS]
>
>* [Recomendações da interface](/help/sites-deploying/ui-recommendations.md)
>* Sobre a descontinuação da interface clássica, consulte [Notas de versão do Experience Manager 6.5](/help/release-notes/deprecated-removed-features.md)
>* Para saber as diferenças entre as interfaces do usuário, consulte [Interface do usuário para toque e interface do usuário clássica](https://aemcq5pedia.wordpress.com/2018/01/05/touch-enabled-ui-aem6-3/)
>* Para entender a interface habilitada para toque em detalhes, consulte [Conceitos da interface do usuário para toque do Experience Manager](/help/sites-developing/touch-ui-concepts.md)

## Vários modos de edição {#editingmodes}

Os autores podem criar e editar conteúdo textual no Experience Manager usando os diferentes modos de componentes. As opções da barra de ferramentas para criação e formatação de conteúdo e a experiência do usuário de componentes habilitados para RTE em modos de edição diferentes variam de acordo com as configurações de RTE.

| Modo de edição | Área de edição | Recursos recomendados para serem habilitados | Interface de toque | IU Clássica |
|--- |--- |--- |--- |--- |
| Em linha | Edição no local para edições secundárias rápidas; Formatar sem abrir uma caixa de diálogo | Recursos mínimos de RTE | Y | Y |
| Tela cheia do RTE | Abrange a página inteira | Todos os recursos de RTE necessários | Y | N |
| Caixa de diálogo | Caixa de diálogo na parte superior do conteúdo da página, mas não cobre a página inteira | Todos os recursos de RTE necessários na interface clássica; habilite os recursos na interface de toque com precisão | Y | Y |
| Tela cheia do diálogo | Igual ao modo de tela cheia; contém campos da caixa de diálogo junto com o RTE | Todos os recursos de RTE necessários | Y | N |

>[!NOTE]
>
>O recurso de edição de origem não está disponível no modo de edição em linha na interface habilitada para toque. Não é possível arrastar imagens no modo de tela cheia. Todos os outros recursos funcionam em todos os modos.

### Edição em linha {#inline-editing}

Quando aberto (com um clique duplo lento), o conteúdo pode ser editado dentro da página. Uma barra de ferramentas compacta com opções muito básicas é apresentada.

![Edição em linha com a barra de ferramentas básica na interface habilitada para toque](assets/chlimage_1-36.png)

*Figura: edição em linha com a barra de ferramentas básica na interface habilitada para toque*

Na interface clássica, um clique duplo lento no componente permite a edição em linha e um contorno laranja destaca o conteúdo. Se o Localizador de conteúdo estiver aberto, uma barra de ferramentas com as opções de formatação de RTE disponíveis será exibida na parte superior da janela. Se o Localizador de conteúdo não estiver aberto, as opções de formatação não serão exibidas e você poderá fazer somente edições básicas de texto.

### Edição em tela cheia {#full-screen-editing}

Os componentes de Experience Manager podem ser abertos na visualização de tela cheia, que oculta o conteúdo da página e ocupa a tela disponível. Considere a edição em tela cheia como uma versão detalhada da edição em linha, pois ela oferece a maioria das opções de edição. Ele pode ser aberto clicando em ![rte_fullscreen](assets/rte_fullscreen.png), na barra de ferramentas compacta, ao usar o modo de edição em linha.

No modo de tela cheia da caixa de diálogo, juntamente com uma barra de ferramentas detalhada do RTE, as opções e os componentes disponíveis em uma caixa de diálogo também estão disponíveis. Ela é aplicável somente para uma caixa de diálogo que contém o RTE junto com outros componentes.

![A barra de ferramentas detalhada do RTE ao editar no modo de tela cheia na interface habilitada para toque](assets/chlimage_1-37.png)

*Figura: a barra de ferramentas detalhada do RTE ao editar no modo de tela cheia na interface habilitada para toque*

### Edição de diálogo {#dialog-editing}

Quando um componente é clicado duas vezes, uma caixa de diálogo é aberta para editar o conteúdo. A caixa de diálogo é aberta na parte superior da página existente. Em alguns cenários específicos, a caixa de diálogo é aberta como uma janela pop-up. Por exemplo, quando um componente de Texto faz parte de uma coluna em um layout de página de várias colunas e a área disponível para a caixa de diálogo é menor.

![Modo de edição de caixa de diálogo na interface habilitada para toque](assets/dialog_editing_modetouchui.png)

*Figura: Modo de edição da caixa de diálogo na interface habilitada para toque*

![Caixa de diálogo na interface clássica que contém uma barra de ferramentas detalhada para edição](assets/chlimage_1-38.png)

*Figura: Caixa de diálogo na interface clássica que contém uma barra de ferramentas detalhada para edição*

## Sobre plug-ins do RTE e os recursos associados {#aboutplugins}

A funcionalidade é disponibilizada por meio de uma série de plug-ins, cada um com:

* A `features` propriedade:

   * Usado para ativar ou desativar a funcionalidade básica desse plug-in
   * Que pode ser configurado usando um procedimento padronizado

* Quando apropriado, propriedades e opções adicionais que exigem configuração especializada.

Os recursos básicos do RTE são ativados ou desativados pelo valor do `features` em um nó específico do plug-in apropriado.

A tabela a seguir lista os plug-ins atuais, mostrando:

* IDs de plug-in com um link para a documentação da API. A ID é usada como o nome do nó quando [ativação de um plug-in](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin).
* Valores permitidos para o `features` propriedade.
* Uma descrição da funcionalidade fornecida pelo plug-in.

| ID do plug-in | recursos | Descrição |
|--- |--- |--- |
| editar | recortar copiar colar-padrão colar-texto sem formatação colar-wordhtml | [Recortar, copiar e, os três modos de colagem](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| findreplace | localizar substituir | Localizar e substituir. |
| formato | negrito e itálico | [Formatação básica de texto](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles). |
| imagem | imagem | Suporte básico de imagem (arrastar do conteúdo ou do Localizador de conteúdo). Dependendo do navegador, o suporte tem comportamentos diferentes para autores |
| chaves |  | Para definir esse valor, consulte [tamanho da guia](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tabsize). |
| justificar | justifyleft justifycenter justifcopyright | Alinhamento de parágrafo. |
| links | modificar a âncora de desvinculação do link | [Hiperlinks e âncoras](/help/sites-administering/configure-rich-text-editor-plug-ins.md#linkstyles). |
| listas | recuo não ordenado recuo para a esquerda | Este plug-in controla os dois [recuo e listas](/help/sites-administering/configure-rich-text-editor-plug-ins.md#indentmargin); incluindo listas aninhadas. |
| misctools | specialchars sourceedit | Ferramentas diversas permitem que os autores insiram [caracteres especiais](/help/sites-administering/configure-rich-text-editor-plug-ins.md#spchar) ou edite a origem do HTML. Além disso, você pode adicionar um inteiro [intervalo de caracteres especiais](/help/sites-administering/configure-rich-text-editor-plug-ins.md#definerangechar) se quiser definir sua própria lista. |
| Paraformat | paraformat | Os formatos de parágrafo padrão são Parágrafo, Cabeçalho 1, Cabeçalho 2 e Cabeçalho 3 (`<p>`, `<h1>`, `<h2>`, e `<h3>`). Você pode [adicionar mais formatos de parágrafo](/help/sites-administering/configure-rich-text-editor-plug-ins.md#paraformats) ou estenda a lista. |
| spellcheck | checktext | [Verificador ortográfico com reconhecimento de idioma](/help/sites-administering/configure-rich-text-editor-plug-ins.md#adddict). |
| estilos | estilos | Suporte para estilo usando uma classe CSS. [Adicionar novos estilos de texto](/help/sites-administering/configure-rich-text-editor-plug-ins.md#textstyles) se quiser adicionar (ou estender) sua própria variedade de estilos para usar com texto. |
| subsobrescrito | sobrescrito subscrito | Extensões para os formatos básicos, adicionando sub e superscript. |
| tabela | tabela removível insertrow removerow insertcolumn removecolumn cellprops mergecells splitcell selectrow selectcolumns | Consulte [configurar estilos de tabela](/help/sites-administering/configure-rich-text-editor-plug-ins.md#tablestyles), se quiser adicionar estilos para tabelas inteiras ou células individuais. |
| desfazer | desfazer refazer | Tamanho do histórico de [desfazer e refazer](/help/sites-administering/configure-rich-text-editor-plug-ins.md#undohistory) operações. |

>[!NOTE]
>
>O plug-in de tela cheia não é compatível com o modo de caixa de diálogo. Utilização do `dialogFullScreen` configuração para configurar a barra de ferramentas para o modo de tela cheia.

## Compreender os caminhos e os locais de configuração {#understand-the-configuration-paths-and-locations}

A variável [modo de edição do RTE (e a interface do usuário)](#editingmodes) que você fornece aos autores, decida o local para os detalhes de configuração quando estiver [ativação de plug-ins do RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md#activateplugin):

| Modo de edição | Localização da interface para toque | Local para a interface clássica |
|---|---|---|
| Em linha | `cq:editConfig/cq:inplaceEditing` | `cq:editConfig/cq:inplaceEditing` |
| Tela cheia | `cq:editConfig/cq:inplaceEditing` | Não aplicável |
| Caixa de diálogo | `cq:dialog` | `dialog` |
| Caixa de diálogo de tela cheia | `cq:dialog` | Não aplicável |

>[!NOTE]
>
>Não nomeie o nó sob `cq:inplaceEditing` as `config`. Ligado `cq:inplaceEditing` defina as seguintes propriedades:
>* **Nome**: `configPath`
>* **Tipo**: `String`
>* **Valor**: caminho do nó que contém a configuração real
>
>Não nomeie o nó de configuração do RTE como `config`. Caso contrário, as configurações do RTE serão aplicadas apenas aos administradores e não aos usuários do grupo `content-author`.

Configure as seguintes propriedades que se aplicam ao modo de edição da caixa de diálogo somente na interface para toque:

* `useFixedInlineToolbar`: Defina essa propriedade Booliana definida no nó RTE (uma com sling:resourceType= `cq/gui/components/authoring/dialog/richtext`) para `True`, para tornar a barra de ferramentas do RTE fixa em vez de flutuante.

  Quando essa propriedade é verdadeira, a edição de Richtext é, por padrão, iniciada no evento &quot;foundation-contentloaded&quot;.

  Para evitar que isso aconteça, defina a propriedade `customStart` para `True`e acionar o evento &quot;rte-start&quot; para iniciar a edição do RTE. Quando essa propriedade é &#39;true&#39;, o comportamento padrão, rte start on click, não funciona.

* `customStart`: Defina essa propriedade Booliana definida no nó RTE como `True`, para controlar quando iniciar o RTE acionando o evento `rte-start`.

* `rte-start`: Acione esse evento no `contenteditable-div` do RTE, quando iniciar a edição do RTE. Isso funciona somente se `customStart` foi definido como verdadeiro.

Quando o RTE é usado na caixa de diálogo habilitada para toque, definir a propriedade `useFixedInlineToolbar` para evitar problemas, é obrigatório indicar &quot;true&quot;.

## Personalização da edição no local {#customizing-in-place-editing}

Você pode definir em qual seletor de HTML o editor de texto é iniciado configurando as seguintes propriedades:

* **`editElementQuery`** - Definido em `cq:InplaceEditingConfig`, essa propriedade é usada para especificar um seletor do elemento de HTML no qual a edição em linha do componente de Texto será iniciada. Se não especificado, a edição em linha é iniciada diretamente no HTML do componente de Texto.
* **`textPropertyName`** - Definido em `cq:InplaceEditingConfig`, essa propriedade é usada para especificar o nome da propriedade que será salva no nó de conteúdo em que o valor HTML do componente de texto será mantido após a edição em linha.

A propriedade correspondente do modo de diálogo é `name`.

## Ativar funcionalidades do RTE ativando plug-ins {#enable-rte-functionalities-by-activating-plug-ins}

As funcionalidades do RTE são disponibilizadas por meio de uma série de plug-ins, cada um com a propriedade de recursos. É possível configurar a propriedade features para ativar ou desativar os vários recursos de cada plug-in.

Para obter configurações detalhadas dos plug-ins do RTE, consulte [como ativar e configurar os plug-ins do RTE](/help/sites-administering/configure-rich-text-editor-plug-ins.md).

**Amostra**: Download [esta configuração de exemplo](/help/sites-administering/assets/rte-sample-all-features-enabled-10.zip) que ilustra como configurar o RTE. Neste pacote, todos os recursos estão habilitados.

>[!NOTE]
>
>A variável [Componente de texto dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/text.html#the-text-component-and-the-rich-text-editor) O permite que os editores de modelo configurem muitos plug-ins de RTE em uma GUI como políticas de conteúdo, eliminando a necessidade de configuração técnica. As políticas de conteúdo podem funcionar com as configurações da interface do usuário de RTE conforme descrito neste documento.
>
>Para obter mais informações, consulte [Configurações da interface do usuário do RTE e políticas de conteúdo](/help/sites-administering/rich-text-editor.md) seção deste documento e [Criação de modelos de página](/help/sites-authoring/templates.md) e a variável [Documentação do desenvolvedor dos Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/developing.html).

>[!NOTE]
>
>Para fins de referência, os componentes de Texto padrão (fornecidos como parte de uma instalação padrão) podem ser encontrados em:
>
>* `/libs/wcm/foundation/components/text`
>* `/libs/foundation/components/text`
>
>Para criar seu próprio componente de texto, copie o componente acima em vez de editar esses componentes.

## Configurar a barra de ferramentas do RTE {#dialogfullscreen}

O AEM permite configurar a interface do Editor de Rich Text de forma diferente para os diferentes modos de edição. As configurações padrão são fornecidas abaixo. Você pode sobrepor esses valores-padrão com base em suas necessidades. Você personaliza apenas os recursos da barra de ferramentas que deseja fornecer aos autores. Não é necessário especificar todas as configurações da barra de ferramentas.

Para configurar a barra de ferramentas para `dialogFullScreen`, use o exemplo de configuração a seguir.

```java
<uiSettings jcr:primaryType="nt:unstructured">
  <cui jcr:primaryType="nt:unstructured">
    <inline
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,#justify,#lists,links#modifylink,links#unlink,#paraformat]">
      <popovers jcr:primaryType="nt:unstructured">
        <justify
          jcr:primaryType="nt:unstructured"
          items="[justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify]"
          ref="justify"/>
        <lists
          jcr:primaryType="nt:unstructured"
          items="[lists#unordered,lists#ordered,lists#outdent,lists#indent]"
          ref="lists"/>
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </inline>
    <dialogFullScreen
      jcr:primaryType="nt:unstructured"
      toolbar="[format#bold,format#italic,format#underline,justify#justifyleft,justify#justifycenter,justify#justifyright,justify#justifyjustify,lists#unordered,lists#ordered,lists#outdent,lists#indent,links#modifylink,links#unlink,table#createoredit,#paraformat,image#imageProps]">
      <popovers jcr:primaryType="nt:unstructured">
        <paraformat
          jcr:primaryType="nt:unstructured"
          items="paraformat:getFormats:paraformat-pulldown"
          ref="paraformat"/>
      </popovers>
    </dialogFullScreen>
    <tableEditOptions
      jcr:primaryType="nt:unstructured"
      toolbar="[table#insertcolumn-before,table#insertcolumn-after,table#removecolumn,-,table#insertrow-before,table#insertrow-after,table#removerow,-,table#mergecells-right,table#mergecells-down,table#mergecells,table#splitcell-horizontal,table#splitcell-vertical,-,table#selectrow,table#selectcolumn,-,table#ensureparagraph,-,table#modifytableandcell,table#removetable,-,undo#undo,undo#redo,-,table#exitTableEditing,-]">
    </tableEditOptions>
  </cui>
</uiSettings>
```

Diferentes configurações de interface do usuário são usadas para o modo em linha e o modo de tela cheia. A propriedade da barra de ferramentas é usada para especificar os botões da barra de ferramentas.

Por exemplo, se o botão for um recurso (por exemplo, `Bold`), é especificado como `PluginName#FeatureName` (por exemplo, `links#modifylink`).

Se o botão for um popover (contendo alguns recursos de um plug-in), ele será especificado como `#PluginName` (por exemplo, `#format`).

Separadores (`|`) entre um grupo de botões pode ser especificado com `-`.

O nó pop-up no modo em linha ou tela cheia contém uma lista dos pop-ups que estão sendo usados. Cada nó filho no nó &quot;popovers&quot; é nomeado com base no plug-in (por exemplo, format). Ele tem uma propriedade &quot;items&quot; contendo uma lista de recursos do plug-in (por exemplo, format#bold).

## Configurações da interface do usuário e políticas de conteúdo do RTE {#rtecontentpolicies}

Os administradores podem controlar as opções de RTE usando políticas de conteúdo, digamos, em vez de fazer a configuração conforme descrito acima. As políticas de conteúdo definem as propriedades de design de um componente quando usado como parte de um [modelo editável](/help/sites-authoring/templates.md). Por exemplo, se um componente de texto que usa o RTE for usado com um modelo editável, a política de conteúdo poderá definir que a opção de negrito esteja disponível e que algumas opções de formatação de parágrafo estejam disponíveis. As políticas de conteúdo são reutilizáveis e podem ser aplicadas a vários modelos.

As opções disponíveis no fluxo de RTE downstream das configurações da interface do usuário para as políticas de conteúdo.

* As configurações da interface do usuário definem quais opções estão disponíveis para as políticas de conteúdo.
* Se a configuração da interface do usuário do RTE tiver sido removida ou não ativar um item, a política de conteúdo não poderá configurá-lo.
* Um autor tem acesso somente a essas funcionalidades, conforme disponibilizado pelas configurações da interface do usuário e pelas políticas de conteúdo.

Como exemplo, você pode ver a variável [Documentação do componente principal de Texto](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/text.html#the-text-component-and-the-rich-text-editor).

## Personalizar o mapeamento entre ícones e comandos da barra de ferramentas {#iconstoolbar}

Você pode personalizar o mapeamento entre ícones Coral exibidos na barra de ferramentas do RTE e os comandos disponíveis. Você não pode usar outros ícones além dos ícones Coral.

1. Crie um nó chamado `icons` em `uiSettings/cui`.

1. Crie nós para ícones individuais abaixo dele.
1. Em cada um dos nós de ícone individuais, especifique um ícone Coral e um comando para mapear para o ícone.

Abaixo está um trecho de amostra para mapear o comando Negrito para o ícone Coral chamado `textItalic`.

```java
<text jcr:primaryType="nt:unstructured" sling:resourceType="cq/gui/components/authoring/dialog/richtext" name="./text" useFixedInlineToolbar="{Boolean}true">
    <rtePlugins jcr:primaryType="nt:unstructured">
        <format jcr:primaryType="nt:unstructured" features="bold,italic"/>
    </rtePlugins>
    <uiSettings jcr:primaryType="nt:unstructured">
        <cui jcr:primaryType="nt:unstructured">
            <inline jcr:primaryType="nt:unstructured"
                toolbar="[format#bold,format#italic,format#underline,links#modifylink,links#unlink]">
            </inline>
            <icons jcr:primaryType="nt:unstructured">
                <bold jcr:primaryType="nt:unstructured"
                    command="format#bold"
                    icon="textItalic"/>
            </icons>
        </cui>
    </uiSettings>
</text>
```

## Alternar para o editor de rich text CoralUI 2 {#switch-to-coralui-rich-text-editor}

Em uma página, você pode incluir a biblioteca cliente CoralUI 2 RTE ou a biblioteca cliente CoralUI 3 RTE. Por padrão, o Editor de Rich Text inclui a clientlib CoralUI 3 RTE. Para alternar para o CoralUI 2 RTE, execute as seguintes etapas.

>[!NOTE]
>
>O Adobe não o recomenda como prática recomendada. Alterne para o CoralUI 2 RTE como último recurso. Os plug-ins personalizados para o CoralUI 2 RTE funcionam com o CoralUI 3 RTE se os plug-ins não dependerem dos internos de RTE, como classes.
>
>Se você estiver usando plug-ins personalizados para CoralUI3 RTE, use `rte.coralui3` biblioteca.


1. Sobrepor o nó `/libs/cq/gui/components/authoring/editors/clientlibs/core` em `/apps`e faça o seguinte:

   * Substituir `rte.coralui3` com `rte.coralui2` para a propriedade dependencies.
   * Substituir `cq.authoring.editor.core.inlineediting.rte.coralui3` com `cq.authoring.editor.core.inlineediting.rte.coralui2` para a propriedade embed.
   * Substituir `cq.authoring.rte.coralui3` com `cq.authoring.rte.coralui2` para a propriedade embed.

1. Sobrepor os nós `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` e `/libs/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2` em `/apps`.

   Remover categoria `cq.authoring.dialog` de `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui3` e adicioná-lo a `/apps/cq/gui/components/authoring/dialog/richtext/clientlibs/rte/coralui2`.

1. Altere qualquer outra dependência que esteja sendo incluída na página de `rte.coralui3` para `rte.coralui2`. Por exemplo, depois de sobrepor o nó `/libs/mcm/campaign/components/touch-ui/clientlibs/rte` em `/apps`, altere qualquer dependência dela de `rte.coralui3` para `rte.coralui2`.

1. Sobrepor o nó `cq/ui/widgets` em `/apps`. Substituir a dependência `cq.rte` no nó `/apps/cq/ui/widgets` com `cq.coralui2.rte`.

>[!NOTE]
>
>O CoralUI 2 RTE usa modelos de handlebars para caixas de diálogo de plug-in. Portanto, a clientlib RTE CoralUI 2 tinha uma dependência na clientlib handlebars. O CoralUI 3 RTE não usa modelos handlebars e não tem nenhuma dependência associada. Se os plug-ins personalizados usarem modelos handlebars, inclua a clientlib handlebars na página da Web.

## Informações adicionais {#further-information}

Para obter mais informações sobre como configurar o RTE, consulte a [API do widget AEM](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) referência.

Em particular, para ver os plug-ins e as opções relacionadas disponíveis:

* A variável [CQ.form.RichText](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.RichText) O componente fornece um campo de formulário para editar informações de texto estilizado (rich text). Para conhecer todos os parâmetros disponíveis para o formulário rich text, consulte as Opções de configuração.
* O componente RichText fornece uma ampla variedade de funcionalidades usando plug-ins listados em [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin). Para cada plugin:

   * consulte os Recursos para obter detalhes sobre a funcionalidade que pode ser ativada (ou desativada)
   * Consulte as Opções de configuração para todos os parâmetros disponíveis para obter a configuração detalhada do plug-in apropriado

* Mais informações sobre Regras de HTML para links também estão disponíveis.

Eles podem ser usados para estender e personalizar seu próprio RTE. Por exemplo, para listar as âncoras disponíveis na página ao criar um link, você pode fornecer sua própria implementação do `LinkPlugin`.

## Limitações conhecidas {#known-limitations}

O recurso RTE do AEM tem as seguintes limitações:

* Os recursos de RTE são compatíveis somente nas caixas de diálogo do componente AEM. O RTE não é compatível com assistentes ou formulários fundamentais como [Propriedades da página](/help/sites-developing/page-properties-views.md) e [Andaime](/help/sites-authoring/scaffolding.md) na interface habilitada para toque.

* O AEM não funciona no [Dispositivos híbridos](/help/release-notes/release-notes.md).

* Não nomeie o nó de configuração do RTE `config`. Caso contrário, a configuração do RTE será aplicada somente para os administradores e não para os usuários do grupo `content-author`.

* O RTE não é compatível com quadro embutido ou iframe para incorporar conteúdo.

## Práticas recomendadas e dicas {#best-practices-and-tips}

* Habilitar somente os plug-ins sem pop-up para uma caixa de diálogo flutuante. Plug-ins sem pop-up são menores em tamanho e são mais adequados para uma caixa de diálogo flutuante.
* Ative os plug-ins com pop-ups maiores, como o `Paste` plug-in, somente no modo de caixa de diálogo de tela cheia ou no modo de tela cheia. Os plug-ins com pop-ups grandes precisam de mais espaço na tela para fornecer uma boa experiência de criação.
* Se você estiver usando plug-ins personalizados para CoralUI3 RTE, use `rte.coralui3` biblioteca.

## Solução de problemas frequentes com o RTE {#troubleshoot-issues-with-aem-rich-text-editor}

**Como selecionar várias células de tabela?**

Para selecionar várias células em uma tabela, pressione `Ctrl` ou `Cmd` e, em seguida, clique nas células da tabela uma por uma.

Agora, execute a operação na seleção, digamos, defina as propriedades das células selecionadas.

**Os hiperlinks são perdidos ao editar um componente usando o botão Configurar**

Adicione um hiperlink em um componente de texto editando-o usando o botão Configurar. Você pode perder o hiperlink ao editá-lo novamente e validar o hiperlink pela segunda vez.

Uma solução alternativa é clicar no componente de texto quando a caixa de diálogo de edição for exibida pela segunda vez e executar a validação do link.

Esse problema é resolvido no AEM 6.3 e posterior.

**O conteúdo de HTML adicionado no modo de edição de origem é perdido**

Não adicione um HTML propenso a XSS. O AEM, e não o RTE, pode remover algum conteúdo de HTML para aderir às regras de antisamia XSS.

Para verificar se o HTML colado está salvo, verifique o conteúdo salvo no CRXDE (no nó de conteúdo).

Se não for salvo, o HTML deve ter sido removido pelo RTE, pois não aderiu às regras do RTE.

Se salvo no CRXDE, mas não renderizado na página (para verificar a renderização, consulte as [pré-visualização](/help/sites-authoring/editing-content.md#preview-mode), ele é removido pelas regras XSS do AEM.

**O componente de vários campos não está funcionando como esperado**

Para criar um componente de vários campos, use o CoralUI 3 exclusivamente. Não use caixas de diálogo do componente CoralUI 2.

Além disso, verifique se o código de implementação de vários campos e a estrutura do nó estão corretos.

**A configuração disponível para administradores não está disponível para autores**

Se as atualizações de configurações da interface forem refletidas para administradores, mas não para contas de autor, verifique se o nó de configuração não está nomeado `config`. Use o [`configPath` propriedade](/help/sites-developing/components-basics.md#cq-inplaceediting).

>[!MORELIKETHIS]
>
>* [Configurar plug-ins do RTE](configure-rich-text-editor-plug-ins.md)
>* [Usar editor de rich text para criação](../sites-authoring/rich-text-editor.md)
>* [Configurar o RTE para sites acessíveis](rte-accessible-content.md)
>* [Paridade de recursos da interface de toque e da interface clássica](../release-notes/touch-ui-features-status.md)
>* [Exemplo de tutorial para criar componente composto de vários campos](https://experience-aem.blogspot.com/2019/05/aem-65-touchui-composite-multifield-with-coral3-rte-rich-text.html?lang=pt-BR)
