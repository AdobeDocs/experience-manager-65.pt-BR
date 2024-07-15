---
title: Configure o Editor de Rich Text para criar páginas da Web e sites acessíveis.
description: Configure o Editor de Rich Text para criar páginas da Web e sites acessíveis.
contentOwner: AG
exl-id: d2451710-5abf-4816-8052-57d8f04a228e
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# Configurar o RTE para criar páginas da Web e sites acessíveis {#configure-rte-for-accessibility}

O Adobe Experience Manager oferece suporte a vários recursos de acessibilidade padrão de acordo com vários padrões de acessibilidade. Além disso, os desenvolvedores podem personalizar ou estender o para fornecer recursos que ajudam a criar conteúdo acessível usando componentes Experience Manager que usam o Rich Text Editor (RTE).

Ao projetar páginas da Web e adicionar conteúdo às páginas, os desenvolvedores e autores de conteúdo podem usar os recursos do RTE para fornecer informações relacionadas à acessibilidade. Por exemplo, adicione informações estruturais por meio de cabeçalhos e elementos de parágrafo.

Para configurar e personalizar esses recursos, [configure os plug-ins do RTE](#configure-the-plugin-features) para o componente. Por exemplo, o plug-in `paraformat` permite que você adicione outros elementos de semântica de nível de bloco, incluindo a extensão do número de níveis de cabeçalho com suporte além dos `H1` básicos, `H2` e `H3` fornecidos por padrão.

O RTE está disponível em vários componentes para a interface habilitada para toque e a interface de usuário clássica. No entanto, o componente principal que usará o RTE é o componente **Texto**, que está disponível para ambas as interfaces. As imagens a seguir mostram o RTE com um intervalo de plug-ins habilitado, incluindo `paraformat`:

![Componente de texto (RTE) no modo de tela cheia na interface habilitada para toque.](assets/chlimage_1-206.png)

*Figura: o componente de Texto na interface de usuário habilitada para toque.*

![Editar caixa de diálogo (RTE) do componente de texto na interface clássica.](assets/chlimage_1-207.png)

*Figura: o componente de Texto na interface de usuário Clássica.*

Para ver as diferenças entre os recursos de RTE disponíveis nas várias interfaces, consulte [Plug-ins e seus recursos](/help/sites-administering/rich-text-editor.md#aboutplugins).

## Configurar os recursos do plug-in {#configure-the-plugin-features}

Para obter as instruções completas para configurar o RTE, consulte [configurar a página Editor de Rich Text](/help/sites-administering/rich-text-editor.md). Isso abrange todos os problemas, incluindo as principais etapas:

* [Plug-ins e recursos](/help/sites-administering/rich-text-editor.md#aboutplugins).
* [Locais de configuração](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
* [Ative um plug-in e configure a propriedade de recursos](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
* [Configurar outras funcionalidades do RTE](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).

Ao configurar um plug-in na sub-ramificação `rtePlugins` apropriada no CRXDE Lite, você pode ativar todos os recursos ou recursos específicos desse plug-in.

![CRXDE Lite mostrando um exemplo de rtePlugin.](assets/chlimage_1-208.png)

### Exemplo - especificar formatos de parágrafo disponíveis no campo de seleção RTE {#example-specifying-paragraph-formats-available-in-rte-selection-field}

Novos formatos de blocos semânticos podem ser disponibilizados para seleção por:

1. Dependendo do seu RTE, determine e navegue até o [local de configuração](/help/sites-administering/rich-text-editor.md#understand-the-configuration-paths-and-locations).
1. [Habilite o campo de seleção de Parágrafos](/help/sites-administering/rich-text-editor.md); ao [ativar o plug-in](/help/sites-administering/rich-text-editor.md#enable-rte-functionalities-by-activating-plug-ins).
1. [Especifique os formatos que deseja disponibilizar no campo de seleção Parágrafos](/help/sites-administering/rich-text-editor.md).
1. Os formatos de parágrafo são disponibilizados ao autor de conteúdo a partir dos campos de seleção no RTE. Elas podem ser acessadas:

   * Uso do ícone de travesseiro de parágrafo na interface habilitada para toque.
   * Usando o campo **Formato** (seletor pop-up) na interface clássica.

Com elementos estruturais disponíveis no RTE por meio das opções de formato de parágrafo, o AEM fornece uma boa base para o desenvolvimento de conteúdo acessível. Os autores de conteúdo não podem usar o RTE para formatar o tamanho da fonte, as cores ou outros atributos relacionados, impedindo a criação de formatação em linha. Em vez disso, eles devem selecionar os elementos estruturais apropriados, como cabeçalhos, e usar estilos globais escolhidos na opção Estilos. Isso garante uma marcação limpa e opções melhores para os usuários que navegam com suas próprias folhas de estilos e conteúdo estruturado corretamente.

## Uso do recurso de edição de origem {#use-of-the-source-edit-feature}

Em alguns casos, os autores de conteúdo considerarão necessário examinar e ajustar o código-fonte HTML criado usando o RTE. Por exemplo, um conteúdo criado no RTE pode exigir marcação adicional para garantir a conformidade com a WCAG 2.0. Isso pode ser feito com a opção [edição de origem](/help/sites-administering/rich-text-editor.md#aboutplugins) do RTE. Você pode especificar o recurso [`sourceedit` no `misctools` plug-in](/help/sites-administering/rich-text-editor.md#aboutplugins).

>[!CAUTION]
>
>Use o recurso `sourceedit` com cuidado. Erros de digitação e/ou recursos não suportados podem causar mais problemas.

## Adicionar suporte para mais elementos e atributos de HTML {#add-support-for-more-html-elements-and-attributes}

Para estender ainda mais os recursos de acessibilidade do AEM, é possível estender os componentes existentes com base no RTE (como os componentes **Texto** e **Tabela**) com elementos e atributos adicionais.

O procedimento a seguir ilustra como estender o componente **Tabela** com um elemento **Legenda** que fornece informações sobre uma tabela de dados para usuários de tecnologia assistiva:

### Exemplo - adicionar a legenda à caixa de diálogo Propriedades da tabela {#example-adding-the-caption-to-the-table-properties-dialog}

No construtor do `TablePropertiesDialog`, adicione um campo de entrada de texto adicional que será usado para editar a legenda. Observe que `itemId` deve ser definido como `caption` (ou seja, o nome do atributo DOM) para manipular automaticamente seu conteúdo.

Em **Table**, defina explicitamente ou remova o atributo para/do elemento DOM. O valor é passado pela caixa de diálogo no objeto `config`. Observe que os atributos DOM devem ser definidos/removidos usando os métodos `CQ.form.rte.Common` correspondentes ( `com` é um atalho para `CQ.form.rte.Common`) para evitar armadilhas comuns nas implementações do navegador.

>[!NOTE]
>
>Este procedimento só é adequado para a interface clássica do usuário.

### Exemplo - criar HTML acessível ao usar ênfase em texto {#create-accessible-html-for-text}

O RTE pode usar as marcas `strong` e `em` no lugar de `b` e `i`. Adicione o nó a seguir como irmão aos nós `uiSettings` e `rtePlugins` na caixa de diálogo.

```HTML
<htmlRules jcr:primaryType="nt:unstructured">
    <docType jcr:primaryType="nt:unstructured">
        <typeConfig jcr:primaryType="nt:unstructured"
                useSemanticMarkup="{Boolean}true">
            <semanticMarkupMap
                    b="strong"
                    i="em"/>
        </typeConfig>
    </docType>
</htmlRules>
```

### Instruções passo a passo {#step-by-step-instructions}

1. Inicie o CRXDE Lite. Por exemplo: [http://localhost:4502/crx/de/](http://localhost:4502/crx/de/)
1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   para:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`

   >[!NOTE]
   >
   >Talvez seja necessário criar pastas intermediárias se elas ainda não existirem.

1. Copiar:

   `/libs/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

   para:

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`.

1. Abra o seguinte arquivo para edição (abra com um clique duplo):

   `/apps/cq/ui/widgets/source/widgets/form/rte/plugins/TablePropertiesDialog.js`

1. No método `constructor`, antes da leitura da linha:

   ```
   var dialogRef = this;
   ```

   Adicione o seguinte código:

   ```
   editItems.push({
       "itemId": "caption",
       "name": "caption",
       "xtype": "textfield",
       "fieldLabel": CQ.I18n.getMessage("Caption"),
       "value": (this.table && this.table.caption ? this.table.caption.textContent : "")
   });
   ```

1. Abra o seguinte arquivo:

   `/apps/cq/ui/widgets/source/widgets/form/rte/commands/Table.js`.

1. Adicione o seguinte código ao final do método `transferConfigToTable`:

   ```
   /**
    * Adds Caption Element
   */
   var captionElement;
   if (dom.firstChild && dom.firstChild.tagName.toLowerCase() == "caption")
   {
      captionElement = dom.firstChild;
   }
   if (config.caption)
   {
       var captionTextNode = document.createTextNode(config.caption)
       if (captionElement)
       {
          dom.replaceNode(captionElement.firstChild,captionTextNode);
       } else
       {
           captionElement = document.createElement("caption");
           captionElement.appendChild(captionTextNode);
           if (dom.childNodes.length>0)
           {
              dom.insertBefore(captionElement, dom.firstChild);
           } else
           {
              dom.appendChild(captionElement);
           }
       }
   } else if (captionElement)
   {
     dom.removeChild(captionElement);
   }
   ```

1. Salve as alterações usando **Salvar tudo...**

>[!NOTE]
>
>Um campo de texto sem formatação não é o único tipo de entrada permitido para o valor do elemento de legenda. Você pode usar qualquer widget ExtJS, que forneça o valor da legenda por meio de seu método `getValue()`.
>
>Para adicionar recursos de edição para elementos e atributos adicionais, verifique se:
>
>* A propriedade `itemId` para cada campo correspondente é definida como o nome do atributo DOM apropriado (`TablePropertiesDialog`).
>* O atributo está definido e/ou foi removido explicitamente no elemento DOM (`Table`).

>[!MORELIKETHIS]
>
>* [Guia Rápido para a WCAG 2.0](/help/managing/qg-wcag.md)
>* [Criar conteúdo acessível (conformidade com WCAG 2.0)](/help/sites-authoring/creating-accessible-content.md)
