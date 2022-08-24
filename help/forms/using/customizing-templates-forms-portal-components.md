---
title: Personalização de modelos para componentes do portal de formulários
seo-title: Customizing templates for forms portal components
description: Exibir metadados personalizados na lista de formulários
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

O Portal Forms permite usar metadados personalizados em listas de formulários. Ao criar modelos personalizados para ativos, você pode modificar o layout e usar metadados personalizados com seu conjunto de estilos CSS.

Execute as etapas a seguir para criar um modelo personalizado para vários componentes do Portal Forms.

## Criação de um modelo personalizado {#creating-a-nbsp-custom-template}

1. Criar um nó sling:Folder em /apps

   Adicione uma propriedade &quot;fpContentType&quot;. Especifique os valores apropriados para a propriedade, dependendo do componente para o qual você está definindo o modelo personalizado.

   * Componente Pesquisar e lister: &quot;/libs/fd/fp/formTemplate&quot;
   * Componente Rascunhos e envios:

      * Seção de rascunhos: /libs/fd/fp/rascunhosModelo
      * Seção Submissões: /libs/fd/fp/enviosTemplate
   * Componente do link: /libs/fd/fp/linkTemplate

   Adicione um título que deseja exibir ao selecionar modelos de layout.

   >[!NOTE]
   >
   >O título pode ser diferente do nome do nó de sling:Folder que você criou.

   A imagem a seguir descreve a configuração do componente Pesquisa e Lister .
   ![Criar um sling:Folder](assets/1.png)

1. Crie um arquivo template.html nesta pasta para servir como modelo personalizado.
1. Escreva o modelo personalizado e use os metadados personalizados conforme descrito abaixo.

## Exemplo de trabalho {#working-example}

A seguir encontra-se uma amostra da implementação de um modelo personalizado em que o Portal do Forms adquire um Layout de Cartão Governador do Geometrixx personalizado para o componente Pesquisar e Listar .

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

Um modelo personalizado para qualquer componente do Portal Forms inclui entradas repetíveis e não repetitivas. As entradas repetíveis são entidades básicas para listagem. Exemplos de entradas repetíveis são os componentes Pesquisa e Lister, Rascunhos e Envio e Link .

O Portal Forms fornece uma sintaxe para os titulares locais exibirem metadados personalizados/OOTB. Os espaços reservados são preenchidos após a exibição dos resultados de formulários, rascunhos ou envios.

Para incluir uma entrada repetível, configure o valor do atributo **dados repetíveis** para **true**.

*No exemplo discutido, dois elementos Div estão presentes na parte superior do modelo personalizado. A primeira, com a classe CSS &quot;__FP_boxes-container&quot;, funciona como um elemento de contêiner para os formulários listados. O segundo, com a classe CSS &quot;__FP_boxes&quot;, é um modelo para as entidades básicas, neste caso um Formulário. O **dados repetíveis**atributo presente no elemento Div tem o valor **true**.*

Cada espaço reservado tem um conjunto exclusivo de metadados OOTB. Para exibir metadados personalizados em um local específico do formulário, adicione o **propriedade ${metadata_prop}** no lugar.

*No exemplo, a propriedade de metadados é usada em várias instâncias. Por exemplo, é usado em **descrição**,**name**,**formUrl**,**htmlStyle**,**pdfUrl**,**pdfStyle**e **caminho**da forma prescrita.*

## Metadados prontos para uso {#out-of-the-box-metadata}

Vários componentes do Forms Portal fornecem conjuntos exclusivos de metadados OOTB que podem ser usados para listagem.

### Componente Pesquisar e listar {#search-amp-lister-component}

* **Título:** Título do formulário
* **name**: Nome do formulário (em sua maioria, é o mesmo que o título)
* **descrição**: Descrição do formulário
* **formUrl**: URL para renderizar o formulário como HTML
* **pdfUrl**: URL para renderizar o formulário como PDF
* **assetType**: Tipo do ativo. Os valores válidos incluem **Formulário**,**Formulário PDF**, **Formulário impresso** e **Formulário adaptável**

* **htmlStyle**&amp; **pdfStyle**: Exiba o estilo dos ícones HTML e PDF, respectivamente, usados para renderização. Os valores válidos são &quot;**__FP_display_none**&quot; ou em branco.

>[!NOTE]
>
>Lembre-se de usar a classe __FP_display_none em sua folha de estilos personalizada.

* **downloadUrl**: URL para baixar um ativo.

Suporte para localização, classificação e uso de propriedades de configuração na interface do usuário (somente Pesquisa e Lister):

1. **Suporte à localização**: Para localizar qualquer texto estático, use o atributo `${localize-YOUR_TEXT}` e disponibilize o valor localizado, caso ainda não exista.
   *No exemplo discutido, os atributos `${localize-Apply}` e `${localize-Download}` são usados para localizar o texto Aplicar e baixar .*

1. **Suporte para classificação**: Clique no elemento HTML para classificar os resultados da pesquisa. Para implementar a classificação em um layout com tabelas, adicione o atributo &quot;data-sortKey&quot; no cabeçalho da tabela específica. Além disso, adicione seu valor como metadados para os quais deseja classificar.
Por exemplo, para o cabeçalho &quot;Título&quot; na exibição de grade, o valor do cabeçalho &quot;data-sortKey&quot; é &quot;title&quot;. Clique no cabeçalho para classificar os valores em uma coluna específica.

1. **Uso das propriedades de configuração**: O componente Pesquisar e listar tem várias configurações que você pode usar na interface do usuário. Por exemplo, para exibir o texto HTML ToolTip salvo na caixa de diálogo de edição, use a opção `${config-htmlLinkText}` atributo. **Da mesma forma, para o texto da dica de ferramenta do PDF, use o** `${config-pdfLinkText}` atributo.

### Componente Link {#link-component}

* **Título:** Título do formulário
* **formUrl**: URL para renderizar o formulário como HTML
* **target**: Atributo de meta do link. Os valores válidos são &quot;_blank&quot; e &quot;_self&quot;.
* **linkText**: Legenda do link

### Componente Rascunhos e envios {#drafts-amp-submissions-component}

* **Caminho**: Caminho do nó de metadados de rascunho/envios. Use-o com a extensão .HTML como um URL para abrir um rascunho ou envio.
* **contextPath**: Caminho de contexto da instância de AEM
* **firstLetter**: Primeira letra (maiúscula) do título do formulário adaptável, que foi salva como Rascunho ou enviada.
* **formName**: O título do formulário adaptável, que foi salvo como Rascunho ou enviado.
* **rascunhoID**: ID do rascunho listado (Use somente no modelo para a seção Rascunho).
* **submitID**: ID do envio listado (Use somente no modelo para a seção Envio).
* **status**: Status do formulário enviado. (Use somente no modelo para a seção Enviar ).
* **descrição**: Descrição do formulário adaptável associado ao rascunho ou ao envio.
* **diffTime**: Diferença entre a hora atual e a última ação de salvamento do rascunho. Como alternativa, a diferença entre a hora atual e a última ação de envio para o envio.
* **iconClass**: Classe CSS usada para exibir a primeira letra do rascunho/envio. O Portal do Forms inclui as seguintes classes, que fornecem vários planos de fundo coloridos.
* **proprietário**: Usuário que criou o rascunho/envio.
* **Hoje**: Data de criação do projeto ou de apresentação em DD:MM:Formato YYYY.
* **TimeNow**: Hora de criação do rascunho ou da apresentação em HH:MM:Formato SS de 24 horas

*Nota:*

1. Para a opção de exclusão na seção Rascunhos sob o componente Rascunhos e envios, nomeie a classe CSS &quot;__FP_deleteDraft.&quot; Além disso, inclua o atributo &quot;rascunhoID&quot; com o valor **${DraftID}**, que é o projeto de id do projeto correspondente.

1. Ao criar links para rascunhos e envios abertos, é possível especificar **${path}.html** como o valor da variável **href** para a tag de âncora.

![Rascunhos e nó de envio](assets/raw-image-with-index.png)

**A**. Elemento do contêiner

**B.** Metadados de &quot;caminho&quot; com uma hierarquia fixa para obter a miniatura armazenada para cada formulário.

**C.** Atributo repetível de dados usado para a seção de modelo para cada formulário

**D.** Para localizar a sequência de caracteres &quot;Aplicar&quot;

**E.** Uso da propriedade de configuração pdfLinkText

**F.** Usar os metadados &quot;pdfUrl&quot;

## Dicas, truques e problemas conhecidos {#tips-tricks-and-known-issues}

1. Não use aspas simples (&#39;) em nenhum modelo personalizado.
1. Para metadados personalizados, armazene essa propriedade no **jcr:content/metadata** somente nó . Se você armazená-lo em qualquer outro lugar, o Portal do Forms não poderá exibir os metadados.
1. Certifique-se de que o nome de qualquer metadado personalizado ou existente não inclua dois pontos ( : ). Se isso acontecer, você não poderá exibi-lo na interface do usuário.
1. **dados repetíveis** não tem nenhum significado para uma **Link** componente. O Adobe recomenda evitar o uso dessa propriedade no modelo para um componente de Link.

## Artigos relacionados

* [Ativar componentes do portal de formulários](/help/forms/using/enabling-forms-portal-components.md)
* [Criar página do portal de formulários](/help/forms/using/creating-form-portal-page.md)
* [Listar formulários em uma página da Web usando APIs](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Usar componente Rascunhos e Envios](/help/forms/using/draft-submission-component.md)
* [Personalizar o armazenamento de rascunhos e formulários enviados](/help/forms/using/draft-submission-component.md)
* [Amostra para integrar o componente de rascunhos e envios ao banco de dados](/help/forms/using/integrate-draft-submission-database.md)
* [Personalização de modelos para componentes do portal de formulários](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Introdução à publicação de formulários em um portal](/help/forms/using/introduction-publishing-forms.md)
