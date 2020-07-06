---
title: Desenvolver aplicativo Sandbox
seo-title: Desenvolver aplicativo Sandbox
description: Desenvolver aplicativo usando scripts de fundação
seo-description: Desenvolver aplicativo usando scripts de fundação
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
translation-type: tm+mt
source-git-commit: d0b333ffa6cad4841e70e652328e92554fb2a7a1
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 4%

---


# Desenvolver aplicativo Sandbox  {#develop-sandbox-application}

Nesta seção, agora que o modelo foi configurado na seção do aplicativo [](initial-app.md) inicial e as páginas iniciais estabelecidas na seção de conteúdo [](initial-content.md) inicial, o aplicativo pode ser desenvolvido usando scripts de base, incluindo a capacidade de habilitar a criação com componentes do Communities. No final desta seção, o site estará funcional.

## Uso de scripts de página do Foundation {#using-foundation-page-scripts}

O script padrão, criado quando o componente que renderiza o modelo da página de reprodução foi adicionado, é modificado para incluir o head.jsp da página de base e um body.jsp local.

### Tipo de superrecurso {#super-resource-type}

A primeira etapa é adicionar uma propriedade de supertipo de recurso ao `/apps/an-scf-sandbox/components/playpage` nó para que herde os scripts e as propriedades do supertipo.

Usando o CRXDE Lite:

1. Selecione o nó `/apps/an-scf-sandbox/components/playpage`.
1. Na guia Propriedades, digite uma nova propriedade com os seguintes valores:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valor: `foundation/components/page`

1. Clique no botão verde **[!UICONTROL +Adicionar]** .
1. Clique em **[!UICONTROL Salvar tudo]**.

   ![chlimage_1-231](assets/chlimage_1-231.png)

### Scripts de cabeça e corpo {#head-and-body-scripts}

1. No painel do **CRXDE Lite** Explorer, navegue até `/apps/an-scf-sandbox/components/playpage` e clique com o duplo no arquivo `playpage.jsp` para abri-lo no painel de edição.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
     An SCF Sandbox Play Component component.
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %><%
   %><%
    // TODO add your code here
   %>
   ```

1. Tendo em conta as tags de script open/close, substitua &quot; // TODO ...&quot; com inclui scripts para partes do cabeçalho e do corpo de &lt;html>.

   Com um supertipo de `foundation/components/page`, qualquer script não definido nessa mesma pasta será resolvido para um script na `/apps/foundation/components/page` pasta (se existir), caso contrário, para um script na `/libs/foundation/components/page` pasta.

   `/apps/an-scf-sandbox/components/playpage/playpage.jsp`

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: playpage.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <html>
     <cq:include script="head.jsp"/>
     <cq:include script="body.jsp"/>
   </html>
   ```

1. O script de base não `head.jsp` precisa ser sobreposto, mas o script de base `body.jsp` está vazio.

   Para configurar a criação, sobreponha-se `body.jsp` a um script local e inclua um sistema de parágrafo (parsys) no corpo:

   1. Vá até `/apps/an-scf-sandbox/components`.
   1. Select the `playpage` node.
   1. Clique com o botão direito do mouse e selecione `Create > Create File...`

      * Nome: **body.jsp**
   1. Clique em **[!UICONTROL Salvar tudo]**.

   Abra `/apps/an-scf-sandbox/components/playpage/body.jsp` e cole o seguinte texto:

   ```xml
   <%--
   
       An SCF Sandbox Play Component component: body.jsp
   
     This is the component which renders content for An SCF Sandbox page.
   
   --%><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   %><%@page session="false" %>
   <body>
       <h2>Community Play</h2>
       <cq:include path="par" resourceType="foundation/components/parsys" />
   </body>
   ```

1. Clique em **[!UICONTROL Salvar tudo]**.

**Visualização a página em um navegador no modo de edição:**

* Interface padrão: [http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html](http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.md)

Você deve ver não apenas o cabeçalho **Community Play**, mas também a interface do usuário para edição de conteúdo da página.

O painel lateral Ativos/Componentes é visto quando o painel lateral é alternado e a janela é larga o suficiente para que o conteúdo lateral e o conteúdo da página sejam exibidos.

![chlimage_1-232](assets/chlimage_1-232.png)

* Interface clássica: [http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html](http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html)

Veja como a página de reprodução aparece na interface clássica, incluindo o localizador de conteúdo (cf):

![chlimage_1-233](assets/chlimage_1-233.png)

## Componentes do Communities {#communities-components}

Para ativar os componentes Comunidades para criação, start seguindo estas instruções:

* [Acessar componentes das comunidades](basics.md#accessing-communities-components)

Para os fins desta caixa de proteção, start com estes componentes **Comunidades** (ativar marcando a caixa):

* Comentários
* Fórum
* Classificação
* Revisões
* Resumo das revisões (Exibição)
* Votação

Além disso, escolha os componentes **[!UICONTROL Gerais]** , como

* Imagem
* Tabela
* Texto
* Título (Base)

>[!NOTE]
>
>Os componentes ativados para o par de páginas são armazenados no repositório como o valor da `components` propriedade da variável
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` node.


## Página de aterrissagem {#landing-page}

Em um ambiente de vários idiomas, a página raiz incluiria um script que analisaria a solicitação do cliente para determinar o idioma preferencial.

Neste exemplo simples, a página raiz está sendo configurada estaticamente para redirecionar para a página em inglês, que pode ser desenvolvida no futuro para ser a landing page principal com um link para a página de reprodução.

Altere o URL do navegador para a página raiz: [http://localhost:4502/editor.html/content/an-scf-sandbox.html](https://locahost:4502/editor.html/content/an-scf-sandbox.html)

* Selecione o ícone Informações da página
* Selecionar propriedades **[!UICONTROL abertas]**
* Na guia AVANÇADO

   * Para a entrada Redirecionar, navegue até **[!UICONTROL Sites]** > Site **[!UICONTROL da caixa de proteção]** SCF > Caixa de proteção **[!UICONTROL SCF]**
   * Clique em **[!UICONTROL OK]**

* Clique em **[!UICONTROL OK]**

Depois que o site é publicado, navegar até a página raiz em uma instância de publicação redirecionará para a página em inglês.

A última etapa antes de reproduzir com as comunidades componentes do SCF é adicionar uma Pasta da biblioteca do cliente (clientlibs) .... [Adicionar Clienlibs](add-clientlibs.md)