---
title: Adicionar Clientlibs
description: Saiba como adicionar uma ClientLibraryFolder (clientlibs) usada para conter a JavaScript e as Folhas de estilo em cascata usadas para renderizar as páginas do site.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Adicionar Clientlibs {#add-clientlibs}

## Adicionar uma ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crie uma ClientLibraryFolder chamada `clientlibs` que contém a JavaScript (JS) e as Folhas de Estilos em Cascata (CSS) usadas para renderizar as páginas do site.

O valor da propriedade `categories` fornecido a esta biblioteca do cliente é o identificador usado para incluir diretamente esta clientlib de uma página de conteúdo ou para incorporá-la a outras clientlibs.

1. Usando **CRXDE Lite**, expanda `/etc/designs`

1. Clique com o botão direito em `an-scf-sandbox` e selecione `Create Node`

   * Nome: `clientlibs`
   * Tipo: `cq:ClientLibraryFolder`

1. Clique em **OK**

![adicionar-biblioteca-cliente](assets/add-client-library.png)

Na guia **Propriedades** do novo nó `clientlibs`, insira a propriedade **categorias**:

* Nome : **categorias**
* Tipo: **Cadeia de caracteres**
* Valor: **apps.an-scf-sandbox**
* Clique em **Adicionar**
* Clique em **Salvar tudo**

Observação: prefixar o valor das categorias com &quot;aplicativos&quot;. é uma convenção para identificar o &#39;aplicativo proprietário&#39; como estando na pasta /apps, não /libs. IMPORTANTE: adicionar os arquivos de espaço reservado `js.tx`t e **`css.txt`**. (Não é oficialmente um cq:ClientLibraryFolder sem eles.)

1. Clique com o botão direito do mouse em **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Selecione **Criar arquivo...**
1. Inserir **Nome:** `css.txt`
1. Selecione **Criar arquivo...**
1. Inserir **Nome:** `js.txt`
1. Clique em **Salvar tudo**

![clientlibs-css](assets/clientlibs-css.png)

A primeira linha do css.txt e do js.txt identifica o local de base a partir do qual as listas de arquivos a seguir são encontradas.

Tente definir o conteúdo de css.txt para

```
#base=.
 style.css
```

Em seguida, crie um arquivo em clientlibs chamado style.css e defina o conteúdo como

`body {`

`background-color: #b0c4de;`

`}`

### Incorporar SCF Clientlibs {#embed-scf-clientlibs}

Na guia **Propriedades** do nó `clientlibs`, insira a propriedade de cadeia de caracteres de vários valores **embed**. Isso incorpora as [bibliotecas do lado do cliente (clientlibs) necessárias para os componentes SCF](/help/communities/client-customize.md#clientlibs-for-scf). Para este tutorial, muitas das bibliotecas de clientes necessárias para os componentes do Communities são adicionadas.

Essa pode ou não ser a abordagem desejada para usar em um site de produção, pois há considerações de conveniência em relação ao tamanho/velocidade das bibliotecas de clientes baixadas para cada página.

Se estiver usando apenas um recurso em uma página, você pode incluir a clientlib completa desse recurso diretamente na página, por exemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Nesse caso, incluindo todos eles e, portanto, os clientlibs SCF mais básicos que são os clientlibs do autor são preferidos:

* Nome: **`embed`**
* Tipo: **`String`**
* Clique em **`Multi`**
* Valor: **`cq.social.scf`**

   * Ele exibirá uma caixa de diálogo,
clique em **`+`** após cada entrada para adicionar as seguintes categorias de clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clique em **OK**

* Clique em **Salvar tudo**

![scf-clientlibs](assets/scf-clientlibs.png)

É assim que `/etc/designs/an-scf-sandbox/clientlibs` deve aparecer no repositório:

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Incluir clientlibs no modelo PlayPage {#include-clientlibs-in-playpage-template}

Sem incluir a categoria ClientLibraryFolder `apps.an-scf-sandbox` na página, os componentes do SCF não são funcionais nem estilizados, pois os estilos JavaScript e CSS necessários não estão disponíveis.

Por exemplo, sem incluir as clientlibs, o componente de comentários do SCF aparece sem estilo:

![clientlibs-comment](assets/clientlibs-comment.png)

Depois que apps.an-scf-sandbox clientlibs é incluído, o componente de comentários SCF aparece com o estilo:

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

A instrução include pertence à seção `head` do script `html`. O padrão **`foundation head.jsp`** inclui um script que pode ser sobreposto: **`headlibs.jsp`**.

**Copie headlibs.jsp e inclua clientlibs:**

1. Usando **CRXDE Lite**, selecione **`/libs/foundation/components/page/headlibs.jsp`**

1. Clique com o botão direito e selecione **Copiar** (ou selecione Copiar na barra de ferramentas)
1. Selecionar **`/apps/an-scf-sandbox/components/playpage`**
1. Clique com o botão direito e selecione **Colar** (ou selecione Colar na barra de ferramentas)
1. Clique duas vezes em **`headlibs.jsp`** para abri-lo
1. Acrescentar a seguinte linha ao final do arquivo
   **`<ui:includeClientLib categories="apps.an-scf-sandbox"/>`**

1. Clique em **Salvar tudo**

```xml
<%@ page session="false" %><%
%><%@include file="/libs/foundation/global.jsp" %><%
%><ui:includeClientLib categories="cq.foundation-main"/><%
%>
<cq:include script="/libs/cq/cloudserviceconfigs/components/servicelibs/servicelibs.jsp"/>
<% currentDesign.writeCssIncludes(pageContext); %>
<ui:includeClientLib categories="apps.an-scf-sandbox"/>
```

Carregue seu site no navegador e veja se o plano de fundo não é um tom de azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![jogo da comunidade](assets/community-play.png)

### Salvando seu trabalho até agora {#saving-your-work-so-far}

Neste ponto, existe uma sandbox minimalista. Pode valer a pena salvar como um pacote para que, durante a reprodução, se o repositório for corrompido e você desejar recomeçar, possa desativar o servidor. Em seguida, renomeie ou exclua a pasta crx-quickstart/, ative o servidor, carregue e instale este pacote salvo e não precise repetir as etapas mais básicas.

Este pacote existe no tutorial [Criar uma Página de Exemplo](/help/communities/create-sample-page.md) para aqueles que não podem esperar para começar a jogar.

Para criar um pacote:

* No CRXDE Lite, clique no [ícone Pacote](https://localhost:4502/crx/packmgr/)
* Clique em **Criar pacote**

   * Nome do pacote: an-scf-sandbox-minimal-pkg
   * Versão: 0.1
   * Grupo: `leave as default`
   * Clique em **OK**

* Clique em **Editar**

   * Selecione a guia **Filtros**

      * Clique em **Adicionar filtro**
      * Caminho Raiz: navegar até `/apps/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho Raiz: navegar até `/etc/designs/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho Raiz: navegar até `/content/an-scf-sandbox**`
      * Clique em **Concluído**

   * Clique em **Salvar**

* Clique em **Build**

Agora você pode selecionar **Baixar** para salvá-lo em disco e **Carregar Pacote** em outro lugar, e selecionar **Mais > Replicar** para encaminhar a sandbox para uma instância de publicação de host local para expandir o território de sua sandbox.
