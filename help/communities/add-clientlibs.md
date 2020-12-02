---
title: Adicionar Clientlibs
seo-title: Adicionar Clientlibs
description: Adicionar uma ClientLibraryFolder
seo-description: Adicionar uma ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
translation-type: tm+mt
source-git-commit: fcdae5363e7a0070b5d6b76227e5c65efb71bc03
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 2%

---


# Adicionar Clientlibs {#add-clientlibs}

## Adicionar uma ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crie uma ClientLibraryFolder chamada `clientlibs` que conterá o JS e o CSS usados para renderizar as páginas do site.

O valor da propriedade `categories` fornecido para esta biblioteca de cliente é o identificador usado para incluir diretamente esta clientlib de uma página de conteúdo ou para incorporá-la a outras clientlibs.

1. Usando **CRXDE Lite**, expanda `/etc/designs`

1. Clique com o botão direito do mouse em `an-scf-sandbox` e selecione `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clique em **OK**

![add-client-library](assets/add-client-library.png)

Na guia **Propriedades** do novo nó `clientlibs`, digite a propriedade **categoria**:

* Nome : **categoria**
* Tipo: **String**
* Valor : **apps.an-scf-sandbox**
* Clique em **Adicionar**
* Clique em **Salvar tudo**

Observação: como visualizar o valor do categoria com &quot;aplicativos&quot;. é uma convenção para identificar o &quot;aplicativo proprietário&quot; como estando na pasta /apps, não /libs.  IMPORTANTE: Adicione arquivos de espaço reservado `js.tx`t e **`css.txt`**. (Não é oficialmente uma cq:ClientLibraryFolder sem eles.)

1. Clique com o botão direito do mouse em **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Selecione **Criar Arquivo...**
1. Digite **Nome:** `css.txt`
1. Selecione **Criar Arquivo...**
1. Digite **Nome:** `js.txt`
1. Clique em **Salvar tudo**

![clientlibs-css](assets/clientlibs-css.png)

A primeira linha do css.txt e do js.txt identifica o local base a partir do qual as seguintes listas de arquivos são encontradas.

Tente definir o conteúdo de css.txt como

```
#base=.
 style.css
```

Em seguida, crie um arquivo em clientlibs chamado style.css e defina o conteúdo como

`body {`

`background-color: #b0c4de;`

`}`

### Incorporar Clientlibs SCF {#embed-scf-clientlibs}

Na guia **Propriedades** do nó `clientlibs`, digite a propriedade String de vários valores **embed**. Isso incorpora as [bibliotecas do lado do cliente (clientlibs) necessárias para componentes SCF](/help/communities/client-customize.md#clientlibs-for-scf). Neste tutorial, muitas das clientlibs necessárias para os componentes Comunidades são adicionadas.

**** Observe que essa pode ser ou não a abordagem desejada para usar em um site de produção, pois há considerações de conveniência em relação ao tamanho/velocidade dos clientlibs baixados para cada página.

Se apenas estiver usando um recurso em uma página, você poderá incluir a clientlib completa desse recurso diretamente na página, por exemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Nesse caso, incluindo todos e, portanto, os clientlibs SCF mais básicos que são os clientlibs do autor são preferidos:

* Nome : **`embed`**
* Tipo : **`String`**
* Clique em **`Multi`**
* Valor: **`cq.social.scf`**

   * Vai abrir um diálogo,
clique em **`+`** após cada entrada para adicionar as seguintes categorias clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clique em **OK**

* Clique em **Salvar tudo**

![scf-clientlibs](assets/scf-clientlibs.png)

É assim que `/etc/designs/an-scf-sandbox/clientlibs` agora deve aparecer no repositório:

![scf-clientlibs-visualização](assets/scf-clientlibs1.png)

### Incluir Clientlibs no Modelo PlayPage {#include-clientlibs-in-playpage-template}

Sem incluir a categoria `apps.an-scf-sandbox` ClientLibraryFolder na página, os componentes do SCF não estarão funcionais nem com estilo, pois os Javascript(s) e o(s) estilo(s) necessários não estarão disponíveis.

Por exemplo, sem incluir clientlibs, o componente de comentários SCF aparece sem estilo:

![clientlibs-comment](assets/clientlibs-comment.png)

Depois que apps.an-scf-sandbox clientlibs é incluído, o componente de comentários SCF aparece no estilo :

![clientlibs-comment-styled](assets/clientlibs-comment1.png)

A instrução include pertence à seção `head` do script `html`. O padrão **`foundation head.jsp`** inclui um script que pode ser sobreposto: **`headlibs.jsp`**.

**Copie headlibs.jsp e inclua clientlibs:**

1. Usando **CRXDE Lite**, selecione **`/libs/foundation/components/page/headlibs.jsp`**

1. Clique com o botão direito do mouse e selecione **Copiar** (ou selecione Copiar na barra de ferramentas)
1. Selecionar **`/apps/an-scf-sandbox/components/playpage`**
1. Clique com o botão direito do mouse e selecione **Colar** (ou selecione Colar na barra de ferramentas)
1. Duplo clique em **`headlibs.jsp`** para abri-lo
1. Anexar a seguinte linha ao final do arquivo
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

Carregue seu site no navegador e veja se o plano de fundo não é uma sombra de azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![jogo comunitário](assets/community-play.png)

### Salvar seu trabalho até agora {#saving-your-work-so-far}

Nesse ponto, existe uma caixa de proteção minimalista e pode valer a pena salvar como um pacote para que, durante a reprodução, se o repositório ficar corrompido e você desejar start, desative, renomeie ou exclua a pasta crx-quickstart/, ligue o servidor, carregue e instale o pacote salvo e não precise repetir essas etapas mais básicas.

Este pacote existe no tutorial [Criar uma página de amostra](/help/communities/create-sample-page.md) para aqueles que não podem esperar para saltar e reproduzir start!...

Para criar um pacote:

* Na CRXDE Lite, clique no ícone [Pacote](https://localhost:4502/crx/packmgr/)
* Clique em **Criar pacote**

   * Nome do pacote: an-scf-sandbox-Minimum-pkg
   * Versão: 0,1
   * Grupo: `leave as default`
   * Clique em **OK**

* Clique em **Editar**

   * Selecione a guia **Filtros**

      * Clique em **Adicionar filtro**
      * Caminho raiz: navegue até `/apps/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho raiz: navegue até `/etc/designs/an-scf-sandbox`
      * Clique em **Concluído**
      * Clique em **Adicionar filtro**
      * Caminho raiz: navegue até `/content/an-scf-sandbox**`
      * Clique em **Concluído**
   * Clique em **Salvar**


* Clique em **Compilação**

Agora você pode selecionar **Download** para salvá-lo em disco e **Carregar pacote** em outro lugar, bem como selecionar **Mais > Replicar** para encaminhar a caixa de proteção para uma instância de publicação de host local para expandir o realm da sua caixa de proteção.