---
title: Personalização de modelos para componentes do portal de formulários
seo-title: Customizing templates for forms portal components
description: Exibir metadados personalizados na listagem de formulários
seo-description: Display custom metadata in form listing
uuid: 212109ca-85c8-4915-82e5-a18a0443be1b
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: 7566203f-2f80-4ce7-bff9-073d67119f64
docset: aem65
feature: Forms Portal
exl-id: f889d996-77f7-4a4f-a637-da43fe1343c5
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Personalização de modelos para componentes do portal de formulários{#customizing-templates-for-forms-portal-components}

## Pré-requisitos {#prerequisites}

[Gerenciamento de metadados de formulário](../../forms/using/manage-form-metadata.md)

Conhecimento prático de HTML e CSS

## Visão geral {#overview}

A interface do usuário do AEM Forms permite adicionar metadados a qualquer formulário. Os metadados personalizados podem aprimorar a experiência do usuário ao listar e pesquisar formulários de sua organização.

O Forms Portal permite usar metadados personalizados em listagens de formulários. Ao criar modelos personalizados para ativos, você pode modificar o layout e usar metadados personalizados com o conjunto de estilos CSS.

Execute as etapas a seguir para criar um modelo personalizado para vários componentes do Forms Portal.

## Criação de um modelo personalizado {#creating-a-nbsp-custom-template}

1. Criar um nó sling:Folder em /apps

   Adicione uma propriedade &quot;fpContentType&quot;. Especifique valores apropriados para a propriedade, dependendo do componente para o qual você está definindo o modelo personalizado.

   * Componente de pesquisa e listagem: &quot;/libs/fd/fp/formTemplate&quot;
   * Componente de rascunhos e envios:

      * Seção Rascunhos: /libs/fd/fp/draftsTemplate
      * Seção de envios: /libs/fd/fp/submissionsTemplate
   * Componente do link: /libs/fd/fp/linkTemplate

   Adicione um título que você deseja exibir ao selecionar modelos de layout.

   >[!NOTE]
   >
   >O título pode ser diferente do nome do nó de sling:Folder que você criou.

   A imagem a seguir descreve a configuração do componente de Pesquisa e Lister.
   ![Criação de um sling:Folder](assets/1.png)

1. Crie um arquivo template.html nesta pasta para servir como modelo personalizado.
1. Grave o modelo personalizado e use os metadados personalizados conforme descrito abaixo.

## Exemplo de trabalho {#working-example}

Este é um exemplo de implementação de um modelo personalizado em que o Forms Portal adquire um Layout de cartão de visita de Geometrixx personalizado para o componente de Pesquisa e Lister.

```html
<div class="__FP_boxes-container __FP_single-color">
    <div class="boxes __FP_boxes __FP_single-color" data-repeatable="true">
 <div class="__FP_boxes-thumbnail">
     <img src ="${path}/jcr:content/renditions/cq5dam.thumbnail.319.319.png"/>
        </div>
        <h3 class="__FP_single-color" title="${name}" tabindex="0">${name}</h3>
        <p>${description}</p>
        <div class="boxes-icon-cont __FP_boxes-icon-cont">
            <div class="op-dow">
                <a href="${formUrl}" target="_blank" class="__FP_button ${htmlStyle}" title="${config-htmlLinkText}">${localize-Apply}</a>
                <a href="${pdfUrl}" class="__FP_button ${pdfStyle}" title="${config-pdfLinkText}">${localize-Download}</a>
            </div>
        </div>
    </div>
</div>
```

## Especificações técnicas para modelos personalizados {#technical-specifications-for-custom-templates}

Um modelo personalizado para qualquer componente do Forms Portal inclui entradas repetíveis e não repetíveis. As entradas repetíveis são entidades básicas para listagem. Exemplos de entradas repetíveis são Pesquisa e Listagem, Rascunhos e envios e Componentes de link.

O Forms Portal fornece uma sintaxe para que os marcadores de posição exibam metadados personalizados/OOTB. Os espaços reservados são preenchidos após a exibição dos resultados de formulários, rascunhos ou envios.

Para incluir uma entrada repetível, configure o valor do atributo **dados repetíveis** para **true**.

*No exemplo discutido, dois elementos Div estão presentes na parte superior do modelo personalizado. O primeiro, com a classe CSS &quot;__FP_boxes-container&quot;, funciona como um elemento de contêiner para os formulários listados. O segundo, com a classe CSS &quot;__FP_boxes&quot;, é um modelo para as entidades básicas, neste caso um Formulário. A variável **dados repetíveis**o atributo presente no elemento Div tem o valor **true**.*

Cada espaço reservado tem um conjunto exclusivo de metadados OOTB. Para exibir metadados personalizados em um local específico no formulário, adicione o **propriedade ${metadata_prop}** no lugar.

*No exemplo, a propriedade de metadados é usada em várias instâncias. Por exemplo, é usado em **descrição**,**name**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**, e **caminho**do modo prescrito.*

## Metadados prontos para uso {#out-of-the-box-metadata}

Vários componentes do Forms Portal fornecem conjuntos exclusivos de metadados OOTB que você pode usar para listagem.

### Componente de pesquisa e listagem {#search-amp-lister-component}

* **Título:** Título do formulário
* **name**: Nome do formulário (geralmente é o mesmo que o título)
* **descrição**: Descrição do formulário
* **formUrl**: URL para renderizar o formulário como HTML
* **pdfUrl**: URL para renderizar o formulário como PDF
* **assetType**: Tipo do ativo. Os valores válidos incluem **Formulário**,**Formulário PDF**, **Imprimir formulário**, e **Formulário adaptável**

* **htmlStyle**&amp; **pdfStyle**: Estilo de exibição dos ícones HTML e PDF, respectivamente, usados para renderização. Os valores válidos são &quot;**__FP_display_none**&quot; ou em branco.

>[!NOTE]
>
>Lembre-se de usar a classe __FP_display_none em sua folha de estilos personalizada.

* **downloadUrl**: o URL para baixar um ativo.

Suporte para localização, classificação e uso de propriedades de configuração na interface do usuário (somente Pesquisa e Lister):

1. **Suporte à localização**: Para localizar qualquer texto estático, use o atributo `${localize-YOUR_TEXT}` e disponibilize o valor localizado, se ainda não existir.
   *No exemplo discutido, os atributos `${localize-Apply}` e `${localize-Download}` são usados para localizar o texto Aplicar e Baixar.*

1. **Suporte para classificação**: Clique no elemento HTML para classificar os resultados da pesquisa. Para implementar a classificação em um layout apresentado, adicione o atributo &quot;data-sortKey&quot; ao cabeçalho de tabela específico. Além disso, adicione seu valor como os metadados para os quais deseja classificar.
Por exemplo, para o cabeçalho &quot;Título&quot; na exibição de grade, o valor do cabeçalho &quot;data-sortKey&quot; é &quot;título&quot;. Clique no cabeçalho para classificar os valores em uma coluna específica.

1. **Uso das propriedades de configuração**: o componente de Pesquisa e Lister tem várias configurações que você pode usar na interface do usuário. Por exemplo, para exibir o texto de Dica de ferramenta do HTML salvo por meio da caixa de diálogo de edição, use o `${config-htmlLinkText}` atributo. **Da mesma forma, para o texto da dica de ferramenta PDF, use o** `${config-pdfLinkText}` atributo.

### Vincular componente {#link-component}

* **Título:** Título do formulário
* **formUrl**: URL para renderizar o formulário como HTML
* **público alvo**: Atributo de direcionamento do link. Os valores válidos são &quot;_blank&quot; e &quot;_self&quot;.
* **linkText**: Legenda do link

### Rascunhos e componentes de envios {#drafts-amp-submissions-component}

* **Caminho**: Caminho do nó de metadados de rascunho/envios. Use-o com a extensão .HTML como um URL para abrir um rascunho ou envio.
* **contextPath**: caminho de contexto da instância AEM
* **firstLetter**: Primeira letra (maiúscula) do título do formulário adaptável, que foi salvo como rascunho ou enviado.
* **formName**: o título do formulário adaptável, que foi salvo como Rascunho ou enviado.
* **draftID**: ID do rascunho listado (use somente no modelo da seção Rascunho).
* **submitID**: ID do envio listado (use somente no modelo para a seção Envio ).
* **status**: Status do formulário enviado. (Use somente no modelo para a seção Envio).
* **descrição**: Descrição do formulário adaptável associado ao rascunho ou ao envio.
* **diffTime**: Diferença entre a hora atual e a última ação de salvamento do rascunho. Como alternativa, a diferença entre a hora atual e a última ação de envio para o envio.
* **iconClass**: classe CSS usada para exibir a primeira letra do rascunho/envio. O Forms Portal inclui as seguintes classes, que fornecem vários planos de fundo coloridos.
* **proprietário**: usuário que criou o rascunho/envio.
* **Hoje**: Data de criação do rascunho ou envio em DD:MM:formato AAAA.
* **TimeNow**: Hora de criação do rascunho ou envio em HH:MM:SS formato de 24 horas

*Nota:*

1. Para a opção de exclusão na seção Rascunhos, no componente Rascunhos e envios, nomeie a classe CSS &quot;__FP_deleteDraft&quot;. Além disso, inclua o atributo &quot;draftID&quot; com o valor **${draftID}**, que é a id de rascunho do rascunho correspondente.

1. Ao criar links para rascunhos e envios abertos, é possível especificar **${path}.html** como o valor de **href** para a tag de âncora.

![Nó Rascunhos e Envio](assets/raw-image-with-index.png)

**A**. Elemento de contêiner

**B.** metadados de &quot;caminho&quot; com uma hierarquia fixa para obter a miniatura armazenada para cada formulário.

**C** Atributo de repetição de dados usado para a seção de modelo para cada formulário

**D.** Para localizar a string &quot;Aplicar&quot;

**E** Uso da propriedade de configuração pdfLinkText

**F** Uso dos metadados &quot;pdfUrl&quot;

## Dicas, truques e problemas conhecidos {#tips-tricks-and-known-issues}

1. Não use aspas simples (&#39;) em nenhum modelo personalizado.
1. Para metadados personalizados, armazene essa propriedade no **jcr:content/metadata** somente nó. Se você o armazenar em qualquer outro lugar, o Forms Portal não poderá exibir os metadados.
1. Certifique-se de que o nome de qualquer metadado personalizado ou metadado existente não inclua dois pontos ( : ). Caso isso ocorra, não será possível exibi-lo na interface do usuário do.
1. **dados repetíveis** não tem significado para uma **Link** componente. A Adobe recomenda que você evite usar essa propriedade no modelo para um componente Link.

## Artigos relacionados

* [Habilitar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente de rascunhos e envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
