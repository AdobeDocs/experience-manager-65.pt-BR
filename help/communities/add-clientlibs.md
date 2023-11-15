---
title: Adicionar Clientlibs
description: Saiba como adicionar uma ClientLibraryFolder (clientlibs) usada para conter as Folhas de estilo em cascata e JavaScript usadas para renderizar as páginas do site.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Adicionar Clientlibs {#add-clientlibs}

## Adicionar uma ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crie uma ClientLibraryFolder chamada `clientlibs` que contém o JavaScript (JS) e as folhas de estilos em cascata (CSS) usadas para renderizar as páginas do site.

A variável `categories` o valor da propriedade fornecido a esta biblioteca do cliente é o identificador usado para incluir diretamente esta clientlib de uma página de conteúdo ou para incorporá-la a outras clientlibs.

1. Usar **CRXDE Lite**, expandir `/etc/designs`

1. Clique com o botão direito do mouse `an-scf-sandbox` e selecione `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clique em **OK**

![add-client-library](assets/add-client-library.png)

No **Propriedades** para o novo `clientlibs` , insira o **categorias** propriedade:

* Nome: **categorias**
* Tipo: **String**
* Valor: **apps.an-scf-sandbox**
* Clique em **Adicionar**
* Clique em **Salvar tudo**

Observação: prefixar o valor das categorias com &quot;aplicativos&quot;. é uma convenção para identificar o &#39;aplicativo proprietário&#39; como estando na pasta /apps, não /libs. IMPORTANTE: adicionar espaço reservado `js.tx`t e **`css.txt`** arquivos. (Não é oficialmente um cq:ClientLibraryFolder sem eles.)

1. Clique com o botão direito do mouse **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Selecionar **Criar arquivo...**
1. Enter **Nome:** `css.txt`
1. Selecionar **Criar arquivo...**
1. Enter **Nome:** `js.txt`
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

No **Propriedades** para a `clientlibs` insira a propriedade multi-value String **incorporar**. Isso incorpora o necessário [bibliotecas do lado do cliente (clientlibs) para componentes SCF](/help/communities/client-customize.md#clientlibs-for-scf). Para este tutorial, muitas das bibliotecas de clientes necessárias para os componentes do Communities são adicionadas.

Essa pode ou não ser a abordagem desejada para usar em um site de produção, pois há considerações de conveniência em relação ao tamanho/velocidade das bibliotecas de clientes baixadas para cada página.

Se estiver usando apenas um recurso em uma página, você pode incluir a clientlib completa desse recurso diretamente na página, por exemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Nesse caso, incluindo todos eles e, portanto, os clientlibs SCF mais básicos que são os clientlibs do autor são preferidos:

* Nome : **`embed`**
* Tipo : **`String`**
* Clique em **`Multi`**
* Valor: **`cq.social.scf`**

   * Uma caixa de diálogo será exibida, clique em **`+`** após cada entrada, para adicionar as seguintes categorias clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clique em **OK**

* Clique em **Salvar tudo**

![scf-clientlibs](assets/scf-clientlibs.png)

É assim que `/etc/designs/an-scf-sandbox/clientlibs` agora devem aparecer no repositório:

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Incluir clientlibs no modelo PlayPage {#include-clientlibs-in-playpage-template}

Sem incluir o `apps.an-scf-sandbox` ClientLibraryFolder na página, os componentes SCF não são funcionais nem estilizados, pois os estilos JavaScript e CSS necessários não estão disponíveis.

Por exemplo, sem incluir as clientlibs, o componente de comentários do SCF aparece sem estilo:

![clientlibs-comment](assets/clientlibs-comment.png)

Depois que apps.an-scf-sandbox clientlibs é incluído, o componente de comentários SCF aparece com o estilo:

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

A instrução include pertence a `head` seção do `html` script. O padrão **`foundation head.jsp`** inclui um script que pode ser sobreposto: **`headlibs.jsp`**.

**Copie headlibs.jsp e inclua clientlibs:**

1. Usar **CRXDE Lite**, selecione **`/libs/foundation/components/page/headlibs.jsp`**

1. Clique com o botão direito e selecione **Copiar** (ou selecione Copiar na barra de ferramentas)
1. Selecione **`/apps/an-scf-sandbox/components/playpage`**
1. Clique com o botão direito e selecione **Colar** (ou selecione Colar na barra de ferramentas)
1. Clique duas vezes **`headlibs.jsp`** para que você possa abri-lo
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

![community-play](assets/community-play.png)

### Salvando seu trabalho até agora {#saving-your-work-so-far}

Neste ponto, existe uma sandbox minimalista. Pode valer a pena salvar como um pacote para que, durante a reprodução, se o repositório for corrompido e você desejar recomeçar, possa desativar o servidor. Em seguida, renomeie ou exclua a pasta crx-quickstart/, ative o servidor, carregue e instale este pacote salvo e não precise repetir as etapas mais básicas.

Este pacote existe no [Criar uma página de exemplo](/help/communities/create-sample-page.md) tutorial para quem não pode esperar para saltar em e começar a jogar!...

Para criar um pacote:

* No CRXDE Lite, clique no botão [Ícone do pacote](https://localhost:4502/crx/packmgr/)
* Clique em **Criar pacote**

   * Nome do pacote: an-scf-sandbox-minimal-pkg
   * Versão: 0.1
   * Grupo: `leave as default`
   * Clique em **OK**

* Clique em **Editar**

   * Selecionar **Filtros** guia

      * Clique em **Adicionar filtro**
      * Caminho raiz: navegar até `/apps/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho raiz: navegar até `/etc/designs/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho raiz: navegar até `/content/an-scf-sandbox**`
      * Clique em **Concluído**

   * Clique em **Salvar**

* Clique em **Build**

Agora é possível selecionar **Baixar** para salvá-lo em disco e **Fazer upload do pacote** em outro lugar e selecione **Mais > Replicar** para enviar a sandbox para uma instância de publicação de host local para expandir o realm da sandbox.
