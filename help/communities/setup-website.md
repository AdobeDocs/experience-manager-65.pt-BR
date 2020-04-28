---
title: Setup Website Structure
seo-title: Setup Website Structure
description: Configurar diretórios
seo-description: Configurar diretórios
uuid: a31edcd5-dab8-4a42-953b-1d076c2182b2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: d18c0ece-4c4f-499c-ac94-a9aaa7f883c4
translation-type: tm+mt
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Setup Website Structure {#setup-website-structure}

Para configurar seu site, as instruções abaixo descrevem as pastas a serem criadas nos seguintes locais:

* `/apps/an-scf-sandbox`

   É aqui que residem os aplicativos e modelos personalizados.

* `/etc/designs/an-scf-sandbox`

   É aqui que residem os elementos de design disponíveis para download.

* `/content/an-scf-sandbox`

   É aqui que ficam as páginas da Web que podem ser baixadas.

O código neste tutorial dependerá do nome da pasta principal ser o mesmo para o aplicativo, design e conteúdo. If you choose some other name for your website, then always replace `an-scf-sandbox` with the name you have chosen.

>[!NOTE]
>
>Sobre nomes:
>
>* The names seen in CRXDE are node names which form the path to addressable content.
>* Nomes de nó podem conter espaços, mas quando usados em um URI, o espaço deve ser codificado como &#39;%20&#39; ou &#39;+&#39;.
>* Os nomes de nó podem conter hifens e sublinhados, mas devem ser codificados quando referenciados como um nome de pacote dentro de um arquivo Java. Os hífens e os sublinhados são escapados com o sublinhado seguido pelo valor unicode:
   >
   >   
   * hífen torna-se &#39;_002d&#39;
   >   * underscore torna-se &#39;_005f&#39;


## Configurar o diretório do aplicativo (/apps) {#setup-the-application-directory-apps}

O diretório /apps no repositório contém o código com implementa o comportamento e a renderização das páginas fornecidas do diretório /content.

O diretório /apps está protegido e não é acessível publicamente, como são os diretórios /content e /etc/designs.

1. Create `/apps/an-scf-sandbox` folder.

   Usando o **[!UICONTROL CRXDE Lite]**, no painel explorador

   1. Selecione a `/apps` pasta.
   1. Clique com o botão direito do mouse em **[!UICONTROL Criar]**... ou puxe para baixo a opção **[!UICONTROL Criar...]** menu.
   1. Selecione **[!UICONTROL Criar pasta...]**.
   1. Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite `an-scf-sandbox`.
   1. Clique em **[!UICONTROL OK]**.

1. Criar subpasta **[!UICONTROL de componentes]** .

   1. Selecione a `/apps/an-scf-sandbox` pasta.
   1. Clique em **[!UICONTROL Criar > Criar pasta]**.
   1. Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite **[!UICONTROL componentes]**.
   1. Clique em **[!UICONTROL OK]**.

1. Criar subpasta **[!UICONTROL de modelos]** .

   1. Selecione a `/apps/an-scf-sandbox` pasta.
   1. Clique em **[!UICONTROL Criar > Criar pasta]**.
   1. Na caixa de diálogo **[!UICONTROL Criar pasta]** , digite **[!UICONTROL modelos]**.
   1. Clique em **[!UICONTROL OK]**.
   1. Selecione novamente `/apps/an-scf-sandbox`.
   1. Selecione **[!UICONTROL Salvar tudo]**.
   Como em qualquer processo de edição, salve com frequência. Se você encontrar problemas com a inserção de dados, isso pode ocorrer porque seu login expirou ou você precisa salvar as edições anteriores.

1. A estrutura no painel do explorador do CRXDE Lite agora deve ser parecida com esta:

   ![chlimage_1-44](assets/chlimage_1-44.png)

## Set up the Design Directory (/etc/designs) {#setup-the-design-directory-etc-designs}

O diretório /etc/designs contém as imagens, scripts e folhas de estilo que serão baixadas juntamente com o conteúdo da página.

1. To use the Designer tool in the Classic UI, browse to [https://&lt;server>:&lt;port>/miscadmin](http://localhost:4502/miscadmin).

   Observação: Se você usar o CRXDE Lite para criar um Nó do tipo `cq:Page`, o Controle de acesso e a Replicação não serão definidos para as configurações padrão de uma página.

1. No painel explorador, selecione a pasta **[!UICONTROL Designs]** e clique em **[!UICONTROL Nova]** > **[!UICONTROL Nova página]**.

   Digite:

   * Título: Caixa de proteção **[!UICONTROL SCF]**
   * Nome: **[!UICONTROL an-scf-sandbox]**
   * Selecionar modelo de página **[!UICONTROL de design]**
   Clique em **[!UICONTROL Criar]**.

   ![chlimage_1-45](assets/chlimage_1-45.png)

1. Atualize o painel do explorador se a pasta &quot;Uma caixa de proteção SCF&quot; não for exibida.

1. Retorne ao CRXDE Lite (http:// localhost:4502/crx/de) e expanda /etc/designs para ver o nó chamado &quot;an-scf-sandbox&quot;.

   No painel inferior direito do CRXDE, você pode visualização a guia Propriedades, a guia Controle de acesso e a guia Replicação para ver o que foi definido usando o Modelo da página de design.

   ![chlimage_1-46](assets/chlimage_1-46.png)

## Configurar o Diretório de conteúdo (/content) {#setup-the-content-directory-content}

O diretório /content no repositório é onde o conteúdo do site reside. Os caminhos em /content compreendem os caminhos do URL para as solicitações do navegador.

*Depois* que o modelo [de](initial-app.md#createthepagetemplate) página é criado como parte do aplicativo inicial, o conteúdo da página inicial pode ser criado com base no modelo.... [**⇒**](initial-app.md)
