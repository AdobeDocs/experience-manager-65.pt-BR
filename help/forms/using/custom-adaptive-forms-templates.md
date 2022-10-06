---
title: Criação de um modelo de formulário adaptável personalizado
seo-title: Creating a custom adaptive form template
description: Este artigo descreve como criar modelos de formulário adaptáveis personalizados.
seo-description: This article describes how to create custom adaptive form templates.
uuid: 11b5f8cd-c56a-4525-97d5-1938ef5f183d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
discoiquuid: affba49e-9712-4d29-858b-2f8ec4f2b1f1
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# Criação de um modelo de formulário adaptável personalizado{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>A AEM Forms introduziu modelos dinâmicos. Você pode usar o editor de modelos do AEM Sites para [criar ou editar modelos dinâmicos](../../forms/using/template-editor.md). Os modelos mencionados no artigo abaixo são modelos estáticos. Eles não estão disponíveis em uma instalação padrão. [Pacote de compatibilidade de instalação](../../forms/using/compatibility-package.md) para colocar esses modelos no seu ambiente.

## Pré-requisitos {#prerequisites}

* Noções básicas sobre AEM [Modelo de página](/help/sites-authoring/templates.md) e [Criação de formulários adaptáveis](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Noções básicas sobre AEM [Bibliotecas do lado do cliente](/help/sites-developing/clientlibs.md)

## Modelo de formulário adaptável {#adaptive-form-template}

Um modelo de formulário adaptável é especializado AEM modelo de página, com determinadas propriedades e estrutura de conteúdo usadas para criar o formulário adaptável. O modelo tem layouts pré-configurados, estilos e estrutura básica do conteúdo inicial.

Depois de criar um formulário, as alterações feitas na estrutura de conteúdo do modelo original não são refletidas no formulário.

## Modelos de formulário adaptável padrão {#default-adaptive-form-templates}

AEM QuickStart fornece os seguintes modelos de formulário adaptáveis:

* Modelo de pesquisa: Permite criar um formulário adaptável de página única usando o layout responsivo que tem várias colunas configuradas. O layout se ajusta automaticamente com base nas dimensões das várias telas nas quais deseja exibir o formulário.
* Modelo de Inscrição Simples: Permite criar um formulário adaptável de várias etapas usando um layout de assistente. Nesse layout, é possível especificar uma expressão de conclusão de etapa para cada etapa, que é validada antes de o assistente prosseguir para a próxima etapa.
* Modelo de Inscrição com Guias: Permite criar um formulário adaptável com várias guias usando um layout de guias à esquerda, onde é possível visitar guias em qualquer ordem aleatória.
* Modelo de Inscrição Avançada: Permite criar um formulário com várias guias e um assistente. Ele usa um layout de guias à esquerda que permite visitar as guias em qualquer ordem. Ele usa os serviços de design da Adobe Document Cloud para assinatura e verificação.
* Modelo em branco: Permite criar um formulário sem qualquer cabeçalho, rodapé e conteúdo inicial. Você pode adicionar componentes, como caixas de texto, botões e imagens. O template em branco permite criar um formulário que pode ser [incorporar em AEM páginas do site](/help/forms/using/embed-adaptive-form-aem-sites.md).

Esses modelos têm a variável `sling:resourceType` propriedade definida como o componente de página correspondente. O componente de página renderiza a página CQ, contendo contêiner de formulário adaptável, que, por sua vez, renderiza um formulário adaptável.

A tabela a seguir lista a associação entre modelos e componentes de página:

<table>
 <tbody>
  <tr>
   <td><p><strong>Modelo</strong></p> </td>
   <td><p><strong>Componente de Página </strong></p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/surveyTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/survey</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/simpleEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/base</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/af/templates/tabbedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/af/components/page/tabbedenrollment</p> </td>
  </tr>
  <tr>
   <td><p>/libs/fd/afaddon/templates/advancedEnrollmentTemplate</p> </td>
   <td><p>/libs/fd/afaddon/components/page/advancedenrollment</p> </td>
  </tr>
 </tbody>
</table>

## Criação de um modelo de formulário adaptável usando o editor de modelo {#creating-an-adaptive-form-template-using-template-editor}

Você pode especificar a estrutura e o conteúdo inicial de um formulário adaptável usando o Editor de modelos. Por exemplo, você deseja que todos os autores de formulários tenham poucas caixas de texto, botões de navegação e um botão Enviar em um formulário de inscrição. É possível criar um modelo que os autores possam usar para criar um formulário consistente com outros formulários de inscrição. AEM Editor de modelo permite:

* Adicionar componentes de cabeçalho e rodapé de um formulário na camada de estrutura
* Forneça o conteúdo inicial do formulário.
* Especifique um tema.
* Especifique ações como enviar, redefinir e navegar.

Para obter mais informações, consulte [Editor de modelos](../../forms/using/template-editor.md).

## Criação de um modelo de formulário adaptável a partir do CRXDE {#creating-an-adaptive-form-template-from-crxde}

Em vez de usar os modelos disponíveis, você pode criar um modelo e usá-lo para criar formulários adaptáveis. Os modelos personalizados são baseados em vários componentes de página que fazem referência a contêineres de formulário adaptáveis e elementos de página, como cabeçalho e rodapé.

Você pode criar esses componentes usando o componente de página base do seu site. Como alternativa, é possível estender o componente de página do formulário adaptável usado pelos modelos prontos para uso.

Execute as etapas a seguir para criar um modelo personalizado, como simpleEnrollmentTemplate.

1. Navegue até o CRXDE Lite na sua instância de criação.

1. No diretório /apps , crie a estrutura de pastas para seu aplicativo. Por exemplo, se o nome do aplicativo for minha empresa, crie uma pasta com esse nome. Normalmente, a pasta do aplicativo contém componentes, configuração, modelos, src e diretórios de instalação. Para este exemplo, crie as pastas componentes, configuração e modelos.

1. Navegue até a pasta /libs/fd/af/templates.
1. Copie o `simpleEnrollmentTemplate` nó .
1. Navegue até a pasta /apps/mycompany/templates. Clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.
1. Se necessário, renomeie o nó do modelo copiado. Por exemplo, renomeie-o como modelo de inscrição.

1. Navegue até o local /apps/mycompany/templates/enrollment-template.

1. Modifique o `jcr:title` e `jcr:description` para a `jcr:content` para distinguir o modelo do modelo copiado.

1. O `jcr:content` o nó do template modificado contém o `guideContainer` e `guideformtitle` componentes. `guideContainer` é o contêiner que contém o formulário adaptável. O `guideformtitle` componente exibe o nome do aplicativo, a descrição e assim por diante.

   Em vez de `guideformtitle`, é possível incluir um componente personalizado ou a variável `parsys` componente. Por exemplo, remover `guideformtitle`e adicione um componente personalizado ou a `parsys` nó do componente. Certifique-se de que `sling:resourceType` a propriedade do componente faz referência ao componente e o mesmo é definido na página `component.jsp` arquivo.

1. Navegue até o local /apps/mycompany/templates/enrollment-template/jcr:content.

1. Abra o **[!UICONTROL Propriedades]** e altere o valor da variável `cq:designPath` propriedade para /etc/designs/mycompany.

1. Agora crie um nó /etc/designs/mycompany para `cq:Page` tipo .

## Criar um componente de página de formulário adaptável {#create-an-adaptive-form-page-component}

O modelo personalizado tem o mesmo estilo que o modelo padrão, pois ele faz referência ao componente de página /libs/fd/af/components/page/base. Você pode encontrar a referência do componente como a propriedade `sling:resourceType` definido no nó /apps/mycompany/templates/enrollment-template/jcr:content. Como a base é um componente de produto principal, não modifique esse componente.

1. Navegue até o nó /apps/mycompany/templates/enrollment-template/jcr:content e modifique o valor da propriedade `sling:resourceType` para /apps/mycompany/components/page/enrollmentpage
1. Copie o nó /libs/fd/af/components/page/base para a pasta /apps/mycompany/components/page.

1. Renomeie o componente copiado para `enrollmentpage`.

1. **(Somente se você já tiver uma página de conteúdo)** Execute as seguintes etapas (a-d), se você tiver um `contentpage`para seu site. Se você não tiver um `contentpage`para o seu site, você pode sair do `resourceSuperType`propriedade para apontar para a página base OOTB.

   1. Para o `enrollmentpage` nó , defina o valor da propriedade `sling:resourceSuperType` para mycompany/components/page/contentpage. O `contentpage` é o componente base da página do site. Outros componentes de página podem estendê-la. Remover arquivos de script em `enrollmentpage`, exceto `head.jsp`, `content.jsp`e `library.jsp`. O `sling:resourceSuperType` componente, que é `contentpage` nesse caso, inclui todos esses scripts. Os cabeçalhos, incluindo a barra de navegação e o rodapé, são herdados do `contentpage` componente.

   1. Abra o arquivo `head.jsp`.

      O arquivo JSP contém a linha `<cq.include script="library.jsp"/>`.

      O `library.jsp` O arquivo contém o `guide.theme.simpleEnrollment` biblioteca do cliente, que contém o estilo do formulário adaptável.

      O componente de página `enrollmentpage` tem uma `head.jsp` arquivo que substitui o `head.jsp` do `contentpage` componente.

   1. Inclua todos os scripts na `head.jsp` para o `contentpage` para o `head.jsp` para o `enrollmentpage` componente.
   1. No `content.jsp` , é possível adicionar mais conteúdo de página ou referências a outros componentes incluídos quando uma página é renderizada. Por exemplo, se você adicionar o componente personalizado `applicationformheader`, adicione a seguinte referência ao componente no arquivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Da mesma forma, se você adicionar uma `parsys` na estrutura do nó do modelo, inclua também o componente personalizado .

## Criação de uma biblioteca de cliente de formulário adaptável {#creating-an-adaptive-form-client-library}

O `head.jsp` do `enrollmentpage` o componente para o novo modelo inclui uma biblioteca do cliente `guide.theme.simpleEnrollment`. O template padrão também usa essa biblioteca do cliente. Altere o estilo no novo modelo usando um destes métodos:

* Definir um tema personalizado e substituir o tema padrão `guide.theme.simpleEnrollment` com o tema personalizado.
* Defina uma nova biblioteca do cliente em /etc/designs/mycompany. Inclua a biblioteca do cliente após a entrada de tema padrão na página jsp. Inclua todos os estilos substituídos e arquivos Java Script adicionais nesta biblioteca do cliente.

>[!NOTE]
>
>Tema refere-se a uma biblioteca do cliente incluída no componente de página usado para renderizar um formulário adaptável. A biblioteca do cliente governa principalmente a aparência de um formulário adaptável.
