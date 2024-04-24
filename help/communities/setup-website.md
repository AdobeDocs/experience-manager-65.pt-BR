---
title: Configurar estrutura do site
description: Saiba como configurar a estrutura do site, incluindo as pastas a serem criadas.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 1f60a0d4-a272-45e8-9742-4b706be8502e
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 1%

---

# Configurar estrutura do site {#setup-website-structure}

Para configurar seu site, as instruções abaixo descrevem as pastas a serem criadas nos seguintes locais:

* `/apps/an-scf-sandbox`

  É aqui que residem os aplicativos e modelos personalizados.

* `/etc/designs/an-scf-sandbox`

  É aqui que ficam os elementos de design baixáveis.

* `/content/an-scf-sandbox`

  É aqui que as páginas da Web disponíveis para download residem.

O código deste tutorial depende do nome da pasta principal ser o mesmo para o aplicativo, design e conteúdo. Se você escolher algum outro nome para o seu site, sempre substitua `an-scf-sandbox` com o nome escolhido.

>[!NOTE]
>
>Sobre nomes:
>
>* Os nomes vistos no CRXDE são nomes de nó que formam o caminho para o conteúdo endereçável.
>* Os nomes de nós podem conter espaços, mas quando usados em um URI, o espaço deve ser codificado como &#39;%20&#39; ou &#39;+&#39;.
>* Os nomes de nó podem conter hifens e sublinhados, mas devem ser codificados quando referenciados como um nome de pacote em um arquivo Java™. Os hifens e sublinhados são escapados com um sublinhado seguido pelo valor Unicode:
>
>   * o hífen se torna &#39;_002d&#39;
>   * sublinhado torna-se &#39;_005f&#39;

## Configurar o Diretório de Aplicativos (/apps) {#setup-the-application-directory-apps}

O diretório /apps no repositório contém o código com o que implementa o comportamento e a renderização das páginas fornecidas pelo diretório /content.

O diretório /apps está protegido e não está acessível publicamente, assim como os diretórios /content e /etc/designs.

1. Criar `/apps/an-scf-sandbox` pasta.

   Usar **[!UICONTROL CRXDE Lite]**, no painel do explorador

   1. Selecione o `/apps` pasta.
   1. Clique com o botão direito do mouse **[!UICONTROL Criar]**... ou puxe para baixo o **[!UICONTROL Criar...]** menu.
   1. Selecionar **[!UICONTROL Criar pasta...]**.
   1. No **[!UICONTROL Criar pasta]** , insira `an-scf-sandbox`.
   1. Clique em **[!UICONTROL OK]**.

1. Criar **[!UICONTROL componentes]** subpasta.

   1. Selecione o `/apps/an-scf-sandbox` pasta.
   1. Clique em **[!UICONTROL Criar > Criar pasta]**.
   1. No **[!UICONTROL Criar pasta]** , insira **[!UICONTROL componentes]**.
   1. Clique em **[!UICONTROL OK]**.

1. Criar **[!UICONTROL modelos]** subpasta.

   1. Selecione o `/apps/an-scf-sandbox` pasta.
   1. Clique em **[!UICONTROL Criar > Criar pasta]**.
   1. No **[!UICONTROL Criar pasta]** , insira **[!UICONTROL modelos]**.
   1. Clique em **[!UICONTROL OK]**.
   1. Selecionar novamente `/apps/an-scf-sandbox`.
   1. Selecionar **[!UICONTROL Salvar tudo]**.

   Como em qualquer processo de edição, você deve salvar com frequência. Se você tiver problemas ao inserir dados, talvez o tempo limite do seu logon tenha expirado ou você precise salvar as edições anteriores.

1. A estrutura no painel do explorador do CRXDE Lite agora deve ser semelhante a esta:

   ![crxde-template](assets/crxde-template.png)

## Configurar o Diretório de design (/etc/designs) {#setup-the-design-directory-etc-designs}

O diretório /etc/designs contém as imagens, os scripts e as folhas de estilos a serem baixados junto com o conteúdo da página.

1. Para usar a ferramenta Designer na interface clássica, navegue até [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Observação: se você usar o CRXDE Lite para criar um Nó do tipo `cq:Page`, o Controle de acesso e a Replicação não seriam definidos como as configurações padrão para uma página.

1. No painel do explorador, selecione a variável **[!UICONTROL Designs]** e clique em **[!UICONTROL Novo]** > **[!UICONTROL Nova página]**.

   Insira:

   * Título: **[!UICONTROL Uma sandbox SCF]**
   * Nome: **[!UICONTROL an-scf-sandbox]**
   * Selecionar **[!UICONTROL Modelo de página de design]**

   Clique em **[!UICONTROL Criar]**.

   ![design-template](assets/design-template.png)

1. Atualize o painel do explorador se a pasta &quot;Uma sandbox SCF&quot; não for exibida.

1. Retorne ao CRXDE Lite (http:// localhost:4502/crx/de) e expanda /etc/designs para ver o nó chamado &quot;an-scf-sandbox&quot;.

   No painel inferior direito do CRXDE, você pode visualizar a guia Propriedades, a guia Controle de acesso e a guia Replicação para ver o que foi definido usando o Modelo de página de design.

   ![crxde-configure-template](assets/crxde-configure-template.png)

## Configurar o Diretório de conteúdo (/content) {#setup-the-content-directory-content}

O diretório /content no repositório é onde o conteúdo do site reside. Os caminhos em /content compreendem os caminhos do URL para solicitações do navegador.

*Depois* o [modelo de página](initial-app.md#createthepagetemplate) for criado como parte do aplicativo inicial, o conteúdo da página inicial poderá ser criado com base no modelo.... [**^**](initial-app.md)
