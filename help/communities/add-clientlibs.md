---
title: Adicionar Clientlibs
seo-title: Add Clientlibs
description: Adicionar uma pastaBibliotecaCliente
seo-description: Add a ClientLibraryFolder
uuid: 2944923d-caca-4607-81a4-4122a2ce8e41
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 46f81c3f-6512-43f1-8ec1-cc717ab6f6ff
docset: aem65
exl-id: 569f2052-b4fe-4f7f-aec9-657217cba091
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 2%

---

# Adicionar Clientlibs {#add-clientlibs}

## Adicionar uma ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crie uma ClientLibraryFolder com o nome `clientlibs` que conterão o JS e o CSS usados para renderizar as páginas do site.

O `categories` o valor da propriedade dado a essa biblioteca do cliente é o identificador usado para incluir diretamente essa clientlib de uma página de conteúdo ou para incorporá-la a outras clientlibs.

1. Usando **CRXDE Lite**, expandir `/etc/designs`

1. Clique com o botão direito do mouse `an-scf-sandbox` e selecione `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clique em **OK**

![add-client-library](assets/add-client-library.png)

No **Propriedades** para o novo `clientlibs` , insira o **categorias** propriedade:

* Nome : **categorias**
* Tipo : **String**
* Valor : **apps.an-scf-sandbox**
* Clique em **Adicionar**
* Clique em **Salvar tudo**

Observação : apresentando o valor das categorias como &quot;aplicativos&quot;. é uma convenção para identificar o &quot;aplicativo proprietário&quot; como sendo da pasta /apps, não /libs.  IMPORTANTE : Adicionar espaço reservado `js.tx`t e **`css.txt`** arquivos. (Não é oficialmente uma cq:ClientLibraryFolder sem eles.)

1. Clique com o botão direito do mouse **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Selecionar **Criar arquivo...**
1. Enter **Nome:** `css.txt`
1. Selecionar **Criar arquivo...**
1. Enter **Nome:** `js.txt`
1. Clique em **Salvar tudo**

![clientlibs-css](assets/clientlibs-css.png)

A primeira linha do css.txt e do js.txt identifica o local base do qual as listas de arquivos a seguir devem ser encontradas.

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

No **Propriedades** para o `clientlibs` nó , insira a propriedade String de vários valores **embed**. Isso incorpora o necessário [bibliotecas do lado do cliente (clientlibs) para componentes SCF](/help/communities/client-customize.md#clientlibs-for-scf). Neste tutorial, muitas das clientlibs necessárias para os componentes das Comunidades são adicionadas.

**Observação** que essa pode ou não ser a abordagem desejada para usar em um site de produção, pois há considerações de conveniência versus tamanho/velocidade das clientlibs baixadas para cada página.

Se estiver usando apenas um recurso em uma página, você pode incluir a clientlib completa desse recurso diretamente na página, por exemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Nesse caso, incluindo todos e, portanto, as clientlibs do SCF mais básicas, que são as clientlibs do autor, são preferidas:

* Nome : **`embed`**
* Tipo : **`String`**
* Clique em **`Multi`**
* Valor: **`cq.social.scf`**

   * Uma caixa de diálogo será exibida, clique em **`+`** após cada entrada para adicionar as seguintes categorias clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * Clique em **OK**

* Clique em **Salvar tudo**

![scf-clientlibs](assets/scf-clientlibs.png)

É assim que `/etc/designs/an-scf-sandbox/clientlibs` agora deve aparecer no repositório :

![scf-clientlibs-view](assets/scf-clientlibs1.png)

### Incluir clientlibs no modelo do PlayPage {#include-clientlibs-in-playpage-template}

Sem incluir a variável `apps.an-scf-sandbox` Categoria ClientLibraryFolder na página, os componentes do SCF não serão funcionais nem estilizados, pois os Javascript e o(s) estilo(s) necessários não estarão disponíveis.

Por exemplo, sem incluir as clientlibs, o componente de comentários do SCF aparece sem o estilo :

![clientlibs-comment](assets/clientlibs-comment.png)

Uma vez que apps.an-scf-sandbox clientlibs é incluído, o componente SCF comments aparece no estilo :

![clientlibs-estilo-comentário](assets/clientlibs-comment1.png)

A instrução include pertence ao `head` da seção `html` script. O padrão **`foundation head.jsp`** inclui um script que pode ser sobreposto : **`headlibs.jsp`**.

**Copie headlibs.jsp e inclua clientlibs:**

1. Usando **CRXDE Lite**, selecione **`/libs/foundation/components/page/headlibs.jsp`**

1. Clique com o botão direito do mouse e selecione **Copiar** (ou selecione Copiar na barra de ferramentas)
1. Selecionar **`/apps/an-scf-sandbox/components/playpage`**
1. Clique com o botão direito do mouse e selecione **Colar** (ou selecione Colar na barra de ferramentas)
1. Clique duas vezes **`headlibs.jsp`** para abri-lo
1. Anexe a seguinte linha ao final do arquivo
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

Carregue seu site na Web no navegador e veja se o plano de fundo não é uma sombra de azul.

[https://localhost:4502/content/an-scf-sandbox/en/play.html](https://localhost:4502/content/an-scf-sandbox/en/play.html)

![community-play](assets/community-play.png)

### Salvando Seu Trabalho Até Agora {#saving-your-work-so-far}

Neste ponto, existe uma sandbox minimalista e pode valer a pena salvar como um pacote para que, durante a reprodução, se o repositório ficar corrompido e você desejar iniciar novamente, você possa desativar, renomear ou excluir o servidor da pasta crx-quickstart/, ativar, carregar e instalar o pacote salvo e não precisar repetir essas etapas mais básicas.

Este pacote existe no [Criar uma página de exemplo](/help/communities/create-sample-page.md) tutorial para aqueles que não podem esperar apenas para entrar e começar a jogar!..

Para criar um pacote:

* No CRXDE Lite, clique no [Ícone Pacote](https://localhost:4502/crx/packmgr/)
* Clique em **Criar pacote**

   * Nome do pacote: an-scf-sandbox-Minimum-pkg
   * Versão: 0,1
   * Grupo: `leave as default`
   * Clique em **OK**

* Clique em **Editar**

   * Selecionar **Filtros** guia

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


* Clique em **Criar**

Agora você pode selecionar **Baixar** para salvá-lo em disco e **Fazer upload do pacote** em outro lugar, bem como selecionar **Mais > Replicar** para enviar a sandbox para uma instância de publicação de host local, expanda o realm da sandbox.
