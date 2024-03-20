---
title: Criação de um modelo de formulário adaptável personalizado
description: Este artigo descreve como criar modelos de formulário adaptáveis personalizados.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
docset: aem65
exl-id: 35b50573-0be8-469d-a1ac-f51b9aaa5fef
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# Criação de um modelo de formulário adaptável personalizado{#creating-a-custom-adaptive-form-template}

>[!NOTE]
>
>O AEM Forms introduziu os modelos dinâmicos. Você pode usar o editor de modelos do AEM Sites para [criar ou editar modelos dinâmicos](../../forms/using/template-editor.md). Os modelos mencionados no artigo abaixo são modelos estáticos. Eles não estão disponíveis em uma instalação padrão. [Instalar pacote de compatibilidade](../../forms/using/compatibility-package.md) para obter esses modelos no seu ambiente.

## Pré-requisitos {#prerequisites}

* Compreensão do AEM [Modelo da página](/help/sites-authoring/templates.md) e [Criação de formulário adaptável](https://helpx.adobe.com/aem-forms/6-1/introduction-forms-authoring.html)

* Compreensão do AEM [Bibliotecas do cliente](/help/sites-developing/clientlibs.md)

## Modelo de formulário adaptável {#adaptive-form-template}

Um modelo de formulário adaptável é um modelo de página AEM especializado, com determinadas propriedades e estrutura de conteúdo usada para criar o formulário adaptável. O modelo tem layouts, estilos e estrutura básica de conteúdo inicial pré-configurados.

Depois de criar um formulário, as alterações na estrutura do conteúdo do modelo original não serão refletidas no formulário.

## Modelos de formulário adaptável padrão {#default-adaptive-form-templates}

O AEM QuickStart fornece os seguintes modelos de formulário adaptáveis:

* Modelo de pesquisa: permite criar um formulário adaptável de página única usando o Layout responsivo que tem várias colunas configuradas. O layout é ajustado automaticamente com base nas dimensões das várias telas nas quais você deseja exibir o formulário.
* Modelo de inscrição simples: permite criar um formulário adaptável em várias etapas usando um layout de assistente. Nesse layout, você pode especificar uma expressão de conclusão de etapa para cada etapa, que é validada antes de o assistente prosseguir para a próxima etapa.
* Modelo de inscrição com guias: permite criar um formulário adaptável com várias guias usando um layout de guias à esquerda, onde você pode visitar as guias em qualquer ordem aleatória.
* Modelo de inscrição avançado: permite criar um formulário com várias guias e um assistente. Ele usa um layout de guias à esquerda que permite visitar guias em qualquer ordem. Ele usa os serviços de design da Adobe Document Cloud para assinatura e verificação.
* Modelo em branco: permite criar um formulário sem qualquer cabeçalho, rodapé e conteúdo inicial. Você pode adicionar componentes como caixas de texto, botões e imagens. O template em branco permite criar um formulário que você pode [incorporar em páginas do site AEM](/help/forms/using/embed-adaptive-form-aem-sites.md).

Esses modelos têm o `sling:resourceType` propriedade definida para o componente de página correspondente. O componente Página renderiza a página CQ, contendo o contêiner de formulário adaptável, que por sua vez renderiza o formulário adaptável.

A tabela a seguir enumera a associação entre os modelos e o componente de página:

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
   <td><p>/libs/fd/afaddon/components/page/advanced/enrollment</p> </td>
  </tr>
 </tbody>
</table>

## Criação de um modelo de formulário adaptável usando o editor de modelos {#creating-an-adaptive-form-template-using-template-editor}

Você pode especificar a estrutura e o conteúdo inicial de um formulário adaptável usando o Editor de modelos. Por exemplo, você deseja que todos os autores de formulário tenham poucas caixas de texto, botões de navegação e um botão de envio em um formulário de inscrição. Você pode criar um modelo que os autores podem usar para criar um formulário consistente com outros formulários de inscrição. O Editor de modelo AEM permite:

* Adicionar componentes de cabeçalho e rodapé de um formulário na camada da estrutura
* Forneça o conteúdo inicial para o formulário.
* Especifique um tema.
* Especifique ações como enviar, redefinir e navegar.

Para obter mais informações, consulte [Editor de modelo](../../forms/using/template-editor.md).

## Criação de um modelo de formulário adaptável a partir do CRXDE {#creating-an-adaptive-form-template-from-crxde}

Em vez de usar os modelos disponíveis, você pode criar um modelo e usá-lo para criar formulários adaptáveis. Os modelos personalizados são baseados em vários componentes de página que fazem referência a contêineres de formulário adaptável e elementos de página, como cabeçalho e rodapé.

Você pode criar esses componentes usando o componente de página base para seu site. Como alternativa, é possível estender o componente de página do formulário adaptável que os modelos prontos para uso usam.

Execute as seguintes etapas para criar um modelo personalizado, como simpleEnrollmentTemplate.

1. Navegue até o CRXDE Lite na instância de criação.

1. No diretório /apps, crie a estrutura de pastas para o aplicativo. Por exemplo, se o nome do aplicativo for mycompany, crie uma pasta com esse nome. Normalmente, a pasta do aplicativo contém componentes, configuração, modelos, src e diretórios de instalação. Para este exemplo, crie as pastas de componentes, configuração e modelos.

1. Navegue até a pasta /libs/fd/af/templates.
1. Copie o `simpleEnrollmentTemplate` nó.
1. Navegue até a pasta /apps/mycompany/templates. Clique com o botão direito do mouse e selecione **[!UICONTROL Colar]**.
1. Se necessário, renomeie o nó do modelo copiado. Por exemplo, renomeie-o como enrollment-template.

1. Navegue até o local /apps/mycompany/templates/enrollment-template.

1. Modifique o `jcr:title` e `jcr:description` propriedades para o `jcr:content` para distinguir o modelo do modelo copiado.

1. A variável `jcr:content` o nó do modelo modificado contém o `guideContainer` e `guideformtitle` componentes. `guideContainer` é o contêiner que contém o formulário adaptável. A variável `guideformtitle` exibe o nome, a descrição e assim por diante do aplicativo.

   Em vez de `guideformtitle`, você pode incluir um componente personalizado ou a variável `parsys` componente. Por exemplo, remover `guideformtitle`e adicione um componente personalizado ou a variável `parsys` nó do componente. Certifique-se de que o `sling:resourceType` propriedade do componente faz referência ao componente, e a mesma é definida na página `component.jsp` arquivo.

1. Navegue até o local /apps/mycompany/templates/enrollment-template/jcr:content.

1. Abra o **[!UICONTROL Propriedades]** e altere o valor da variável `cq:designPath` propriedade para /etc/designs/mycompany.

1. Agora crie um nó /etc/designs/mycompany para o `cq:Page` tipo.

## Criar um componente de página de formulário adaptável {#create-an-adaptive-form-page-component}

O modelo personalizado tem o mesmo estilo do modelo padrão, pois o modelo faz referência ao componente de página /libs/fd/af/components/page/base. Você pode encontrar a referência do componente como a propriedade `sling:resourceType` definido no nó /apps/mycompany/templates/enrollment-template/jcr:content. Como a base é um componente principal do produto, não modifique esse componente.

1. Navegue até o nó /apps/mycompany/templates/enrollment-template/jcr:content e modifique o valor da propriedade `sling:resourceType` para /apps/mycompany/components/page/enrollmentpage
1. Copie o nó /libs/fd/af/components/page/base para a pasta /apps/mycompany/components/page.

1. Renomear o componente copiado para `enrollmentpage`.

1. **(Somente se você já tiver uma página de conteúdo)** Execute as seguintes etapas (a-d), se você tiver uma `contentpage`para o seu site. Se você não tiver um `contentpage`para o seu site, você pode deixar o `resourceSuperType`para apontar para a página base pronta para uso.

   1. Para o `enrollmentpage` nó, defina o valor da propriedade `sling:resourceSuperType` para mycompany/components/page/contentpage. A variável `contentpage` é o componente da página base do site. Outros componentes da página podem estendê-la. Remover arquivos de script em `enrollmentpage`, exceto `head.jsp`, `content.jsp`, e `library.jsp`. A variável `sling:resourceSuperType` componente, que é `contentpage` nesse caso, inclui todos esses scripts. Os cabeçalhos, incluindo a barra de navegação e o rodapé, são herdados da `contentpage` componente.

   1. Abra o arquivo `head.jsp`.

      O arquivo JSP contém a linha `<cq.include script="library.jsp"/>`.

      A variável `library.jsp` o arquivo contém o `guide.theme.simpleEnrollment` biblioteca cliente, que contém o estilo do formulário adaptável.

      O componente da página `enrollmentpage` tem um `head.jsp` arquivo que substitui o `head.jsp` arquivo de `contentpage` componente.

   1. Incluir todos os scripts na variável `head.jsp` arquivo para o `contentpage` componente para a `head.jsp` arquivo para o `enrollmentpage` componente.
   1. No `content.jsp` você pode adicionar conteúdo de página adicional ou referências a outros componentes incluídos quando uma página é renderizada. Por exemplo, se você adicionar o componente personalizado `applicationformheader`, certifique-se de adicionar a seguinte referência ao componente no arquivo JSP:

      `<cq:include path="applicationformheader" resourceType="mycompany/components/applicationformheader"/>`

      Da mesma forma, se você adicionar um `parsys` na estrutura do nó do modelo, também inclua o componente personalizado.

## Criação de uma biblioteca de cliente de formulários adaptável {#creating-an-adaptive-form-client-library}

A variável `head.jsp` arquivo de `enrollmentpage` componente para o novo modelo inclui uma biblioteca do cliente `guide.theme.simpleEnrollment`. O template padrão também usa essa biblioteca do cliente. Altere o estilo no novo modelo usando um destes métodos:

* Definir um tema personalizado e substituir o tema padrão `guide.theme.simpleEnrollment` com o tema personalizado.
* Defina uma nova biblioteca do cliente em /etc/designs/mycompany. Inclua a biblioteca do cliente após a entrada de tema padrão na página jsp. Incluir todos os estilos substituídos e arquivos Java Script adicionais nesta biblioteca do cliente.

>[!NOTE]
>
>O tema se refere a uma biblioteca do cliente incluída no componente Página usado para renderizar um formulário adaptável. A biblioteca do cliente rege principalmente a aparência de um formulário adaptável.
