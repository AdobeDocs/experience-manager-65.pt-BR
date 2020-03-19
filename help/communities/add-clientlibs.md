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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Adicionar Clientlibs {#add-clientlibs}

## Adicionar uma ClientLibraryFolder (clientlibs) {#add-a-clientlibraryfolder-clientlibs}

Crie uma ClientLibraryFolder com o nome `clientlibs`que conterá o JS e o CSS usados para renderizar as páginas do site.

O valor de `categories`propriedade fornecido para essa biblioteca de cliente é o identificador usado para incluir diretamente essa clientlib de uma página de conteúdo ou para incorporá-la a outras clientlibs.

1. Usando o **CRXDE Lite**, expanda `/etc/designs`

1. Clique com o botão direito do mouse `an-scf-sandbox` e selecione `Create Node`

   * Nome : `clientlibs`
   * Tipo : `cq:ClientLibraryFolder`

1. Clique em **OK**

![chlimage_1-47](assets/chlimage_1-47.png)

Na guia **Propriedades** do novo `clientlibs` nó, digite a propriedade **category** :

* Nome : **categorias**
* Tipo: **String**
* Valor : **apps.an-scf-sandbox**
* Clique em **Adicionar**
* Clique em **Salvar tudo**

Observação: como pré-visualizar o valor das categorias com &quot;aplicativos&quot;. é uma convenção para identificar o &quot;aplicativo proprietário&quot; como estando na pasta /apps, não /libs.  IMPORTANTE: Adicione espaço reservado `js.tx`a e **`css.txt`** arquivos. (Não é oficialmente uma cq:ClientLibraryFolder sem eles.)

1. Clique com o botão direito do mouse em **`/etc/designs/an-scf-sandbox/clientlibs`**
1. Selecione **Criar Arquivo...**
1. Enter **Name:** `css.txt`
1. Selecione **Criar Arquivo...**
1. Enter **Name:** `js.txt`
1. Clique em **Salvar tudo**

![chlimage_1-48](assets/chlimage_1-48.png)

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

Na guia **Propriedades** do `clientlibs` nó, digite a propriedade String com vários valores **incorporada**. Isso incorpora as bibliotecas necessárias do lado do [cliente (clientlibs) para componentes](/help/communities/client-customize.md#clientlibs-for-scf)SCF. Neste tutorial, muitas das clientlibs necessárias para os componentes Comunidades são adicionadas.

**Observe** que essa pode ou não ser a abordagem desejada para usar em um site de produção, pois há considerações de conveniência em relação ao tamanho/velocidade dos clientlibs baixados para cada página.

Se apenas estiver usando um recurso em uma página, você poderá incluir a clientlib completa desse recurso diretamente na página, por exemplo,

`% ui:includeClientLib categories=cq.social.hbs.forum" %`

Nesse caso, incluindo todos e, portanto, os clientlibs SCF mais básicos que são os clientlibs do autor são preferidos:

* Nome : **`embed`**
* Tipo : **`String`**
* Clique em **`Multi`**
* Valor: **`cq.social.scf`**

   * Ela abrirá uma caixa de diálogo, clique **`+`** depois de cada entrada para adicionar as seguintes categorias clientlib:

      * **`cq.ckeditor`**
      * **`cq.social.author.hbs.comments`**
      * **`cq.social.author.hbs.forum`**
      * **`cq.social.author.hbs.rating`**
      * **`cq.social.author.hbs.reviews`**
      * **`cq.social.author.hbs.voting`**
      * click **OK**

* Clique em **Salvar tudo**

![chlimage_1-49](assets/chlimage_1-49.png)

É assim que agora `/etc/designs/an-scf-sandbox/clientlibs` deve aparecer no repositório:

![chlimage_1-50](assets/chlimage_1-50.png)

### Incluir Clientlibs no modelo PlayPage {#include-clientlibs-in-playpage-template}

Sem incluir a categoria `apps.an-scf-sandbox` ClientLibraryFolder na página, os componentes do SCF não serão funcionais nem estilizados, pois os Javascript e os estilos necessários não estarão disponíveis.

Por exemplo, sem incluir clientlibs, o componente de comentários SCF aparece sem estilo:

![chlimage_1-51](assets/chlimage_1-51.png)

Depois que apps.an-scf-sandbox clientlibs é incluído, o componente de comentários SCF aparece no estilo :

![chlimage_1-52](assets/chlimage_1-52.png)

A instrução include pertence à seção `head` do `html` script. O padrão **`foundation head.jsp`** inclui um script que pode ser sobreposto: **`headlibs.jsp`**.

**Copie headlibs.jsp e inclua clientlibs:**

1. Usando o **CRXDE Lite**, selecione **`/libs/foundation/components/page/headlibs.jsp`**

1. Clique com o botão direito do mouse e selecione **Copiar** (ou selecione Copiar na barra de ferramentas)
1. Selecionar **`/apps/an-scf-sandbox/components/playpage`**
1. Clique com o botão direito do mouse e selecione **Colar** (ou selecione Colar na barra de ferramentas)
1. Clique duas vezes **`headlibs.jsp`** para abri-lo
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

![chlimage_1-53](assets/chlimage_1-53.png)

### Salvando Seu Trabalho Até Agora {#saving-your-work-so-far}

Nesse ponto, existe uma caixa de proteção minimalista e pode valer a pena salvar como um pacote para que, durante a reprodução, se o repositório ficar corrompido e você desejar iniciar novamente, você possa desligar, renomear ou excluir a pasta crx-quickstart/, ligar o servidor, carregar e instalar esse pacote salvo e não precisar repetir essas etapas mais básicas.

Este pacote existe no tutorial [Criar uma página](/help/communities/create-sample-page.md) de amostra para aqueles que não podem esperar para pular e começar a reproduzir!...

Para criar um pacote:

* No CRXDE Lite, clique no ícone [Pacote](https://localhost:4502/crx/packmgr/)
* Clique em **Criar pacote**

   * Nome do pacote: an-scf-sandbox-Minimum-pkg
   * Versão: 0,1
   * Grupo: `leave as default`
   * Clique em **OK**

* Clique em **Editar**

   * Guia Selecionar **filtros**

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


* Clique em **Criar**

Agora você pode selecionar **Download** para salvá-lo em disco e **Carregar pacote** em outro lugar, bem como selecionar **Mais > Replicar** para encaminhar a caixa de proteção para uma instância de publicação de host local a fim de expandir o realm da sua caixa de proteção.