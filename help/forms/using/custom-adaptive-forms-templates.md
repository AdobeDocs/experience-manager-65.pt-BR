---
title: Criação de um modelo de formulário adaptável personalizado
seo-title: Criação de um modelo de formulário adaptável personalizado
description: Este artigo descreve como criar modelos de formulário adaptáveis personalizados.
seo-description: Este artigo descreve como criar modelos de formulário adaptáveis personalizados.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe
workflow-type: tm+mt
source-wordcount: '1286'
ht-degree: 0%

---


# Criação de um modelo de formulário adaptável personalizado{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>A AEM Forms introduziu modelos dinâmicos. Você pode usar o editor de modelos do AEM Sites para [criar ou editar modelos dinâmicos](../../forms/using/template-editor.md). Os modelos mencionados no artigo abaixo são modelos estáticos. Eles não estão disponíveis em uma instalação padrão. [Instale o ](../../forms/using/compatibility-package.md) pacote de compatibilidade para obter esses modelos no seu ambiente.

## Pré-requisitos {#prerequisites}

* Noções básicas sobre AEM [Modelo de página](/help/sites-authoring/templates.md) e [Criação de formulário adaptável](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Noções básicas sobre AEM [bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md)

## Modelo de formulário adaptável {#adaptive-form-template}

Um modelo de formulário adaptável é especializado AEM modelo de página, com determinadas propriedades e estrutura de conteúdo usadas para criar o formulário adaptável. O modelo tem layouts pré-configurados, estilos e estrutura básica de conteúdo inicial.

Após a criação de um formulário, quaisquer alterações na estrutura de conteúdo do modelo original não serão refletidas no formulário.

## Modelos de formulário adaptável padrão {#default-adaptive-form-templates}

AEM QuickStart fornece os seguintes modelos de formulário adaptáveis:

* Template de pesquisa: Permite criar um formulário adaptável de página única usando o layout Responsivo que tem várias colunas configuradas. O layout se ajusta automaticamente com base nas dimensões das várias telas nas quais você deseja exibir o formulário.
* Modelo de inscrição simples: Permite criar um formulário adaptável de várias etapas usando um layout de assistente. Neste layout, você pode especificar uma expressão de conclusão de etapa para cada etapa, que é validada antes que o assistente prossiga para a próxima etapa.
* Modelo de Inscrição com Guias: Permite criar um formulário adaptável de várias guias usando um layout de guias à esquerda, onde é possível visitar guias em qualquer ordem aleatória.
* Modelo de inscrição avançada: Permite criar um formulário com várias guias e assistente. Ele usa um layout de guias à esquerda que permite que você visite guias em qualquer ordem. Ele usa os serviços de design da Adobe Document Cloud para assinatura e verificação.
* Modelo em branco: Permite criar um formulário sem qualquer cabeçalho, rodapé e conteúdo inicial. Você pode adicionar componentes, como caixas de texto, botões e imagens. O modelo em branco permite criar um formulário que pode ser [incorporado AEM páginas do Site](/help/forms/using/embed-adaptive-form-aem-sites.md).

Esses modelos têm a propriedade `sling:resourceType` definida como o componente de página correspondente. O componente de página renderiza a página CQ, contendo o container de formulário adaptável, que por sua vez renderiza o formulário adaptável.

A tabela a seguir enumera a associação entre modelos e componentes de página:

<table>
 <tbody>
  <tr>
   <td><p><strong>Modelo</strong></p> </td>
   <td><p><strong>Componente da página</strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/models/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/pesquisa</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/models/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/models/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/models/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Criação de um modelo de formulário adaptável usando o editor de modelo {#creating-an-adaptive-form-template-using-template-editor}

É possível especificar a estrutura e o conteúdo inicial de um formulário adaptável usando o Editor de modelos. Por exemplo, você deseja que todos os autores de formulários tenham poucas caixas de texto, botões de navegação e um botão Enviar em um formulário de inscrição. É possível criar um modelo que os autores possam usar para criar um formulário consistente com outros formulários de inscrição. AEM Editor de modelos permite:

* Adicionar componentes de cabeçalho e rodapé de um formulário na camada de estrutura
* Forneça o conteúdo inicial do formulário.
* Especifique um tema.
* Especifique ações como enviar, redefinir e navegar.

Para obter mais informações, consulte [Editor de modelos](../../forms/using/template-editor.md).

## Criação de um modelo de formulário adaptável a partir do CRXDE {#creating-an-adaptive-form-template-from-crxde}

Em vez de usar os modelos disponíveis, você pode criar um modelo e usá-lo para criar formulários adaptáveis. Os modelos personalizados baseiam-se em vários componentes de página que fazem referência a container de formulário adaptáveis e elementos de página, como cabeçalho e rodapé.

Você pode criar esses componentes usando o componente de página base para seu site. Como alternativa, você pode estender o componente de página do formulário adaptável que os modelos usam para uso imediato.

Execute as seguintes etapas para criar um modelo personalizado, como simpleEnrollmentTemplate.

1. Navegue até CRXDE Lite na sua instância de criação.

1. No diretório /apps, crie a estrutura de pastas para seu aplicativo. Por exemplo, se o nome do aplicativo for minha empresa, crie uma pasta com esse nome. Normalmente, a pasta do aplicativo contém componentes, configuração, modelos, src e diretórios de instalação. Neste exemplo, crie as pastas de componentes, configuração e modelos.

1. Navegue até a pasta /libs/fd/af/models.
1. Copie o nó `simpleEnrollmentTemplate`.
1. Navegue até a pasta /apps/mycompany/models. Clique com o botão direito do mouse nele e selecione **[!UICONTROL Colar]**.
1. Se necessário, renomeie o nó de modelo copiado. Por exemplo, renomeie-o como modelo de inscrição.

1. Navegue até o local /apps/mycompany/models/enrollment-template.

1. Modifique as propriedades `jcr:title` e `jcr:description` do nó `jcr:content` para distinguir o modelo do modelo copiado.

1. O nó `jcr:content` do modelo modificado contém os componentes `guideContainer` e `guideformtitle`. `guideContainer` é o container que contém o formulário adaptável. O componente `guideformtitle` exibe o nome do aplicativo, a descrição e assim por diante.

   Em vez de `guideformtitle`, você pode incluir um componente personalizado ou o componente `parsys`. Por exemplo, remova `guideformtitle` e adicione um componente personalizado ou o nó do componente `parsys`. Certifique-se de que a propriedade `sling:resourceType` do componente referencie o componente e que o mesmo esteja definido no arquivo de página `component.jsp`.

1. Navegue até o local /apps/mycompany/models/enrollment-template/jcr:content.

1. Abra a guia **[!UICONTROL Propriedades]** e altere o valor da propriedade `cq:designPath` para /etc/designs/mycompany.

1. Agora, crie um nó /etc/designs/mycompany para o tipo `cq:Page`.

## Criar um componente de página de formulário adaptável {#create-an-adaptive-form-page-component}

O modelo personalizado tem o mesmo estilo que o modelo padrão, pois o modelo faz referência ao componente de página /libs/fd/af/components/page/base. Você pode encontrar a referência do componente como a propriedade `sling:resourceType` definida no nó /apps/mycompany/models/enrollment-template/jcr:content. Como a base é um componente principal do produto, não modifique esse componente.

1. Navegue até o nó /apps/mycompany/models/enrollment-template/jcr:content e modifique o valor da propriedade `sling:resourceType` para /apps/mycompany/components/page/enrollmentpage
1. Copie o nó /libs/fd/af/components/page/base para a pasta /apps/mycompany/components/page.

1. Renomeie o componente copiado para `enrollmentpage`.

1. **(Somente se você já tiver uma página de conteúdo)** Execute as seguintes etapas (a-d), se você tiver um  `contentpage`componente existente para seu site. Se você não tiver um `contentpage`componente existente para seu site, poderá deixar a propriedade `resourceSuperType`para apontar para a página base OOTB.

   1. Para o nó `enrollmentpage`, defina o valor da propriedade `sling:resourceSuperType` como mycompany/components/page/contentpage. O componente `contentpage` é o componente básico da página do site. Outros componentes da página podem estendê-la. Remova os arquivos de script em `enrollmentpage`, exceto `head.jsp`, `content.jsp` e `library.jsp`. O componente `sling:resourceSuperType`, que é `contentpage` nesse caso, inclui todos esses scripts. Os cabeçalhos, incluindo a barra de navegação e o rodapé, são herdados do componente `contentpage`.

   1. Abra o arquivo `head.jsp`.

      O arquivo JSP contém a linha `<cq.include script="library.jsp"/>`.

      O arquivo `library.jsp` contém a biblioteca do cliente `guide.theme.simpleEnrollment`, que contém o estilo do formulário adaptável.

      O componente de página `enrollmentpage` tem um arquivo `head.jsp` exclusivo que substitui o arquivo `head.jsp` do componente `contentpage`.

   1. Inclua todos os scripts no arquivo `head.jsp` do componente `contentpage` no arquivo `head.jsp` do componente `enrollmentpage`.
   1. No script `content.jsp`, é possível adicionar conteúdo de página ou referências adicionais a outros componentes incluídos quando uma página é renderizada. Por exemplo, se você adicionar o componente personalizado `applicationformheader`, certifique-se de adicionar a seguinte referência ao componente no arquivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Da mesma forma, se você adicionar um componente `parsys` na estrutura do nó do modelo, inclua também o componente personalizado.

## Criação de uma biblioteca de cliente de formulário adaptável {#creating-an-adaptive-form-client-library}

O arquivo `head.jsp` do componente `enrollmentpage` do novo modelo inclui uma biblioteca de cliente `guide.theme.simpleEnrollment`. O modelo padrão também usa essa biblioteca de cliente. Altere o estilo no novo modelo usando um destes métodos:

* Defina um tema personalizado e substitua o tema padrão `guide.theme.simpleEnrollment` pelo tema personalizado.
* Defina uma nova biblioteca de cliente em /etc/designs/mycompany. Inclua a biblioteca do cliente após a entrada do tema padrão na página jsp. Inclua todos os estilos substituídos e arquivos Java Script adicionais nesta biblioteca de cliente.

>[!NOTE]
>
>O tema refere-se a uma biblioteca de cliente incluída no componente de página usado para renderizar um formulário adaptável. A biblioteca cliente governa principalmente a aparência de um formulário adaptável.

