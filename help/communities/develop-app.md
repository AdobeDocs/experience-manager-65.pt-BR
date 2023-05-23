---
title: Desenvolver aplicativo de sandbox
seo-title: Develop Sandbox Application
description: Desenvolver aplicativo usando scripts de base
seo-description: Develop application using foundation scripts
uuid: 572f68cd-9ecb-4b43-a7f8-4aa8feb6c64e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 910229a3-38b1-44f1-9c09-55f8fd6cbb1d
exl-id: 7ac0056c-a742-49f4-8312-2cf90ab9f23a
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 5%

---

# Desenvolver aplicativo de sandbox  {#develop-sandbox-application}

Nesta seção, agora que o modelo foi configurado no [aplicação inicial](initial-app.md) e as páginas iniciais estabelecidas na seção [conteúdo inicial](initial-content.md) , o aplicativo pode ser desenvolvido usando scripts de base, incluindo a capacidade de habilitar a criação com componentes do Communities. No final desta seção, o site estará funcional.

## Uso de Scripts de Página de Base {#using-foundation-page-scripts}

O script padrão, criado quando o componente que renderiza o modelo da página de reprodução foi adicionado, é modificado para incluir head.jsp da página de fundação e um body.jsp local.

### Tipo de Super Resource {#super-resource-type}

A primeira etapa é adicionar uma propriedade de supertipo de recurso à variável `/apps/an-scf-sandbox/components/playpage` para que ele herde os scripts e as propriedades do supertipo.

Uso do CRXDE Lite:

1. Selecionar nó `/apps/an-scf-sandbox/components/playpage`.
1. Na guia Propriedades, insira uma nova propriedade com os seguintes valores:

   Nome: `sling:resourceSuperType`

   Tipo: `String`

   Valor: `foundation/components/page`

1. Clique no botão verde **[!UICONTROL +Adicionar]** botão.
1. Clique em **[!UICONTROL Salvar tudo]**.

   ![page-script](assets/page-script.png)

### Scripts de cabeçalho e corpo {#head-and-body-scripts}

1. Entrada **CRXDE Lite** painel do explorador, navegue até `/apps/an-scf-sandbox/components/playpage` e clique duas vezes no arquivo `playpage.jsp` para abri-lo no painel de edição.

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

1. Estando ciente das tags de script de abertura/fechamento, substitua &quot; // TODO ...&quot; por inclusões de scripts para as partes do cabeçalho e corpo de &lt;html>.

   Com um supertipo de `foundation/components/page`, qualquer script não definido nesta mesma pasta resolverá para um script em `/apps/foundation/components/page` pasta (se existir), caso contrário para um script em `/libs/foundation/components/page` pasta.

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

1. O script de base `head.jsp` não é necessário sobrepor, mas o script de base `body.jsp` está vazio.

   Para configurar a criação, sobrepor `body.jsp` com um script local e incluir um sistema de parágrafo (parsys) no corpo:

   1. Vá até `/apps/an-scf-sandbox/components`.
   1. Selecione o `playpage` nó.
   1. Clique com o botão direito e selecione `Create > Create File...`

      * Nome: **body.jsp**
   1. Clique em **[!UICONTROL Salvar tudo]**.

   Abertura `/apps/an-scf-sandbox/components/playpage/body.jsp` e cole no seguinte texto:

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

Você não deve ver apenas o cabeçalho **Jogo da comunidade**, mas também a interface para editar o conteúdo da página.

O painel lateral Ativos/Componentes é visto quando o painel lateral é alternado para aberto e a janela é larga o suficiente para que o conteúdo lateral e o conteúdo da página sejam exibidos.

![view-page](assets/view-page.png)

* IU Clássica: `http://localhost:4502/cf#/content/an-scf-sandbox/en/play.html`

A seguir, veja como a página de reprodução aparece na interface clássica, incluindo com o localizador de conteúdo (cf):

![play-page-view](assets/play-page-view.png)

## Componentes das comunidades {#communities-components}

Para ativar os componentes do Communities para criação, comece seguindo estas instruções:

* [Acesso aos componentes das comunidades](basics.md#accessing-communities-components)

Para os fins desta sandbox, comece com esses **Communities** componentes (ative marcando a caixa):

* Comentários
* Fórum
* Avaliação
* Revisões
* Resumo das análises (exibir)
* Votação

Além disso, escolha **[!UICONTROL Geral]** componentes como

* Imagem
* Tabela
* Texto
* Título (Foundation)

>[!NOTE]
>
>Os componentes ativados para o par de páginas são armazenados no repositório como o valor do `components` propriedade do
>
>`/etc/designs/an-scf-sandbox/jcr:content/playpage/par` nó.

## Página de aterrissagem {#landing-page}

Em um ambiente multilíngue, a página raiz incluiria um script que analisaria a solicitação do cliente para determinar o idioma preferencial.

Neste exemplo simples, a página raiz está sendo definida estaticamente para redirecionar para a página em inglês, que pode ser desenvolvida no futuro para ser a página inicial principal com um link para a página de reprodução.

Altere o URL do navegador para a página raiz: `http://localhost:4502/editor.html/content/an-scf-sandbox.html`

* Selecione o ícone Informações da página
* Selecionar **[!UICONTROL Abrir propriedades]**
* Na guia AVANÇADO

   * Para a entrada de redirecionamento, navegue até **[!UICONTROL Sites]** > **[!UICONTROL Site de sandbox SCF]** > **[!UICONTROL Sandbox SCF]**
   * Clique em **[!UICONTROL OK]**

* Clique em **[!UICONTROL OK]**

Quando o site for publicado, navegar até a página raiz em uma instância de publicação redirecionará para a página em inglês.

A última etapa antes de jogar com os componentes SCF de comunidades é adicionar uma Pasta de biblioteca do cliente (clientlibs) .... [Adicionar Clienlibs](add-clientlibs.md)
