---
title: Desenvolver aplicativo de sandbox
description: Saiba como desenvolver um aplicativo de sandbox que use scripts de base e inclua a capacidade de habilitar a criação com componentes de Comunidades.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# Desenvolver aplicativo de sandbox  {#develop-sandbox-application}

Nesta seção, agora que o modelo está configurado na seção [aplicativo inicial](initial-app.md) e nas páginas iniciais estabelecidas na seção [conteúdo inicial](initial-content.md), você pode desenvolver o aplicativo. Você faz isso usando scripts de base que incluem a capacidade de ativar a criação com componentes de Comunidades. No final desta seção, você tem um site que é totalmente funcional.

## Uso de Scripts de Página de Base {#using-foundation-page-scripts}

O script padrão, criado quando o componente que renderiza o modelo da página de reprodução foi adicionado, é modificado para incluir head.jsp da página de fundação e um body.jsp local.

### Tipo de Super Resource {#super-resource-type}

A primeira etapa é adicionar uma propriedade de supertipo de recurso ao nó `/apps/an-scf-sandbox/components/playpage` para que ele herde os scripts e as propriedades do supertipo.

Utilização do CRXDE Lite:

1. Selecione o nó `/apps/an-scf-sandbox/components/playpage`.
1. Na guia Propriedades, insira uma nova propriedade com os seguintes valores:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valor: `foundation/components/page`

1. Clique no botão verde **[!UICONTROL +Adicionar]**.
1. Clique em **[!UICONTROL Salvar tudo]**.

   ![script-página](assets/page-script.png)

### Scripts de cabeçalho e corpo {#head-and-body-scripts}

1. No painel do explorador **CRXDE Lite**, navegue até `/apps/an-scf-sandbox/components/playpage` e clique duas vezes no arquivo `playpage.jsp` para abri-lo no painel de edição.

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

1. Estando ciente das tags de script abrir/fechar, substitua &quot; // TODO ...&quot; por `includes` de scripts para as partes de cabeçalho e corpo de &lt;html>.

   Com um supertipo de `foundation/components/page`, qualquer script não definido nessa mesma pasta é resolvido para um script na pasta `/apps/foundation/components/page` (se existir) ou para um script na pasta `/libs/foundation/components/page`.

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

1. Sobrepor o script de base `head.jsp` não é necessário, mas o script de base `body.jsp` está vazio.

   Para configurar a criação, sobreponha `body.jsp` com um script local e inclua um sistema de parágrafo (parsys) no corpo:

   1. Vá até `/apps/an-scf-sandbox/components`.
   1. Selecione o nó `playpage`.
   1. Clique com o botão direito e selecione `Create > Create File...`

      * Nome: **body.jsp**

   1. Clique em **[!UICONTROL Salvar tudo]**.

   Abra `/apps/an-scf-sandbox/components/playpage/body.jsp` e cole no seguinte texto:

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

**Exibir a página em um navegador no modo de edição:**

* Interface do usuário padrão: `http://localhost:4502/editor.html/content/an-scf-sandbox/en/play.html`

Você não deve ver apenas o cabeçalho **Jogo da comunidade**, mas também a interface do usuário para editar o conteúdo da página.

O painel lateral do Assets/Componente é visto quando o painel lateral é alternado para aberto e a janela é larga o suficiente para que o conteúdo lateral e o conteúdo da página sejam exibidos.

![exibir-página](assets/view-page.png)

* Interface clássica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

A seguir, veja como a página de reprodução aparece na interface clássica, incluindo com o localizador de conteúdo (cf):

![reproduzir-exibição-página](assets/play-page-view.png)

## Componentes das comunidades {#communities-components}

Para ativar os componentes do Communities para criação, comece seguindo estas instruções:

* [Acesso aos componentes das comunidades](basics.md#accessing-communities-components)

Para os fins desta sandbox, comece com estes **Comunidades** componentes (habilite marcando a caixa):

* Comentários
* Fórum
* Avaliação
* Revisões
* Resumo das análises (exibir)
* Votação

Além disso, escolha **[!UICONTROL Geral]** componentes, como

* Imagem
* Tabela
* Texto
* Título (Fundação)

>[!NOTE]
>
>Os componentes habilitados para o par de páginas são armazenados no repositório como o valor da propriedade `components` do
>
>Nó `/etc/designs/an-scf-sandbox/jcr:content/playpage/par`.

## Página de aterrissagem {#landing-page}

Em um ambiente multilíngue, a página raiz incluiria um script que analisaria a solicitação do cliente para determinar o idioma preferencial.

Neste exemplo, a página raiz está sendo definida estaticamente para redirecionar para a página em inglês, que pode ser desenvolvida no futuro para ser a página inicial principal com um link para a página de reprodução.

Alterar a URL do navegador para a página raiz: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Selecione o ícone Informações da página
* Selecionar **[!UICONTROL Abrir Propriedades]**
* Na guia AVANÇADO

   * Para a entrada de Redirecionamento, navegue até **[!UICONTROL Sites]** > **[!UICONTROL Site de Sandbox SCF]** > **[!UICONTROL Sandbox SCF]**
   * Clique em **[!UICONTROL OK]**

* Clique em **[!UICONTROL OK]**

Depois que o site é publicado, navegar até a página raiz em uma instância de publicação redireciona para a página em inglês.

A última etapa antes de jogar com os componentes do SCF de comunidades é adicionar uma Pasta de biblioteca do cliente (clientlibs) .... [Adicionar Clientlibs](add-clientlibs.md)
