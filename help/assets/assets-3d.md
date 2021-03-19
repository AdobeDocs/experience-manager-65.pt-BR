---
title: Trabalhar com ativos 3D no Dynamic Media
seo-title: Trabalhar com ativos 3D no Dynamic Media
description: Saiba como trabalhar com ativos 3D no Dynamic Media
seo-description: Saiba como trabalhar com ativos 3D no Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: Ativos 3D,Gerenciamento de ativos
role: Profissional de negócios, Administrador
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '2319'
ht-degree: 5%

---


# Trabalhar com ativos 3D no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media permite carregar, gerenciar, visualizar e fornecer ativos 3D como experiências imersivas.

* Publicação com um clique (usando **[!UICONTROL Publicação rápida]** na barra de ferramentas) de ativos 3D para gerar um URL.
* Suporte otimizado para visualizar ativos 3D com a predefinição interativa de visualizador Dimensional de alta qualidade fornecida pela Adobe Dimension.
* O componente WCM Mídia 3D permite adicionar facilmente ativos 3D às páginas do AEM Sites.

Não há nenhuma configuração adicional necessária para usar ativos 3D no Dynamic Media.

![sapato em 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png)

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D suportados no Dynamic Media {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos 3D.

Consulte também [formatos 3D suportados.](/help/assets/assets-formats.md)

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | model/gltf-binário | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | *Suporte apenas para ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado originalmente por dispositivos Safari e iOS. |

## Início rápido: Ativos 3D no Dynamic Media {#quick-start-three-d}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudar você a ativar e executar rapidamente com ativos 3D no modo Dynamic Media - Scene7.

>[!NOTE]
>
>Os ativos 3D não são compatíveis com o Dynamic Media - Modo híbrido.

Antes de trabalhar com ativos 3D no Dynamic Media, verifique se o administrador do AEM já ativou e configurou o Dynamic Media Cloud Services no modo Dynamic Media - Scene7.

Consulte [Configuração do Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo Scene7 e [Solução de problemas do Dynamic Media - Modo Scene7.](/help/assets/troubleshoot-dms7.md)

1. **Fazer upload de ativos 3D**

   * [Fazer upload de ativos 3D para uso no Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formatos de arquivo 3D compatíveis para upload no Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organizar ativos digitais](/help/assets/organize-assets.md#organize-digital-assets).
      * [Pesquisar ativos 3D](/help/assets/search-assets.md).
      * [Usar predicados personalizados para filtrar os resultados](/help/assets/search-assets.md#custompredicates) de pesquisa.
   * Exibir ativos 3D

      * [Visualização e interação com ativos](#viewing-three-d-assets) 3D.
      * [Gerenciar a predefinição do visualizador Dimensional](/help/assets/managing-viewer-presets.md).
   * Trabalhar com metadados de ativos 3D

      * [Gerenciamento de metadados para ativos](/help/assets/metadata.md) digitais.
      * [Esquemas de metadados](/help/assets/metadata-schemas.md).



1. **Publicar ativos 3D**

   * [Publicação de ativos estáticos em Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional](#alternate-publish-methods)

## Sobre a visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualizar e interagir com ativos 3D de duas maneiras diferentes: na página de detalhes do ativo e a partir do componente Mídia 3D no Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

Esteja ciente de que o tempo necessário para abrir um ativo 3D na exibição de página Detalhes do ativo depende de vários fatores. Esses fatores incluem informações como as seguintes:

* Largura de banda para o servidor.
* Latências para o servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes a serem considerados ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

>[!TIP]
>
>Você pode abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação de um ativo 3D sem a necessidade de fazer upload primeiro de qualquer arquivo 3D. A predefinição do visualizador Dimensional tem um ativo 3D integrado com o qual você pode interagir.
>
>Consulte [Gerenciar predefinições do visualizador.](/help/assets/managing-viewer-presets.md)

## Visualização e interação com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualização de ativos usando a interface de software](/help/assets/previewing-assets.md).

**Para visualizar e interagir com um ativo 3D na página de detalhes do ativo**

1. Verifique se você fez upload dos ativos 3D no AEM.

   Consulte [Fazer upload de ativos 3D para uso no Dynamic Media.](/help/assets/manage-assets.md#uploading-assets)

1. Em AEM, na página **[!UICONTROL Navegação]**, toque em **[!UICONTROL Ativos > Arquivos.]**
1. Próximo ao canto superior direito da página, na lista suspensa **[!UICONTROL Exibir]**, toque em **[!UICONTROL Exibição de cartão.]**
1. Navegue até o ativo 3D que deseja visualizar.
1. Toque no cartão de ativo 3D para abri-lo na página de detalhes do ativo.
1. Na página de visualização de detalhes do ativo 3D, siga um destes procedimentos:

   * **Rode sua câmera**  - Órbita sua exibição ao redor da cena e dos objetos 3D.
      * _Rato_: Clique com o botão esquerdo e arraste.
      * _Tela_ sensível ao toque: Pressione com um único dedo e arraste.
   * **Deslocar sua câmera**  - Desloque sua exibição para a esquerda, para a direita, para cima ou para baixo.
      * _Rato_: Clique com o botão direito + arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Zoom da câmera**  - Zoom da câmera para mover para dentro e para fora de áreas da cena 3D.
      * _Rato_: Roda de rolagem.
      * _Tela_ sensível ao toque: Um beliscão de dois dedos.
   * **Recenter sua câmera**  - Insira novamente sua câmera a um ponto em um objeto na cena 3D.
      * _Rato_: Clique duas vezes.
      * _Tela_ sensível ao toque: Toque duas vezes.
   * **Redefinir**  - Próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável.
   * **Modo de tela cheia**  - Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

1. No canto superior direito da página, toque em **[!UICONTROL Fechar]** para voltar à página Assets.

## Visualização e interação com um ativo 3D dentro de um componente de mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está no modo **[!UICONTROL Edit]**, nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

>[!IMPORTANT]
>
>Essa tarefa só pode ser realizada depois de ter adicionado um componente de mídia 3D a uma página da Web e atribuído um ativo 3D ao componente. Consulte [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page) e [Atribuir um ativo 3D a um componente de Mídia 3D.](#assigning-a-three-d-asset-to-the-component)

Consulte também [Visualização de ativos usando a interface do software.](/help/assets/previewing-assets.md)

**Para visualizar e interagir com um ativo 3D dentro de um componente de mídia 3D**

1. Embora uma página da Web esteja no modo **[!UICONTROL Edit]**, siga um destes procedimentos:

   * Perto do canto superior direito da página, clique em **[!UICONTROL Preview]** para entrar no modo **[!UICONTROL Preview]**.
   * Exclua `/editor.html` do URL da página no navegador.

Um ativo 3D totalmente interativo, como exibido em    ![Ativo 3D exibido no ](/help/assets/assets-dm/3d-asset-in-3d-media.png)
componente Mídia 3Dum ativo 3D totalmente interativo, como exibido no modo  **** Visualização.

1. Enquanto estiver no modo **[!UICONTROL Preview]** , siga um destes procedimentos:

   * **Rode sua câmera**  - Órbita sua exibição ao redor da cena e dos objetos 3D.
      * _Rato_: Clique com o botão esquerdo e arraste.
      * _Tela_ sensível ao toque: Pressione com um único dedo e arraste.
   * **Deslocar sua câmera**  - Desloque sua exibição para a esquerda, para a direita, para cima ou para baixo.
      * _Rato_: Clique com o botão direito + arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Zoom da câmera**  - Zoom da câmera para mover para dentro e para fora de áreas da cena 3D.
      * _Rato_: Roda de rolagem.
      * _Tela_ sensível ao toque: Um beliscão de dois dedos.
   * **Recenter sua câmera**  - Insira novamente sua câmera a um ponto em um objeto na cena 3D.
      * _Rato_: Clique duas vezes.
      * _Tela_ sensível ao toque: Toque duas vezes.
   * **Redefinir**  - Próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável.
   * **Modo de tela cheia**  - Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

## Sobre como trabalhar com o componente de mídia 3D {#working-with-three-d-media-component}

O Dynamic Media inclui um componente de mídia 3D do Dynamic Media que pode ser usado no AEM Sites para permitir a visualização interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de mídia 3D ao modelo da página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configuração do componente de mídia 3D](#configuring-the-three-d-component)
* [Atribuição de um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component)


## Adicionar o componente de mídia 3D ao modelo de página {#adding-three-d-media-component-to-page-template}

1. Navegue até **[!UICONTROL Ferramentas > Geral > Modelos.]**
1. Navegue até o modelo de página no qual você deseja ativar o componente 3D e selecione o modelo.
1. Toque em **[!UICONTROL Editar]** para abrir o modelo.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione o modo **[!UICONTROL Estrutura]**, se ele ainda não estiver ativo.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Toque em uma área vazia na região **[!UICONTROL Contêiner de layout]** para selecioná-la e abrir a barra de ferramentas associada.
1. Na barra de ferramentas, toque no ícone **[!UICONTROL Política]** para abrir o **[!UICONTROL Editor de Políticas.]**
1. Na seção **[!UICONTROL Propriedades]**, na guia **[!UICONTROL Componentes permitidos]**, role até **[!UICONTROL Dynamic Media]**, expanda a lista e marque **[!UICONTROL Mídia 3D.]**
1. Toque em **[!UICONTROL Concluído]** para salvar as alterações e fechar o **[!UICONTROL Editor de Políticas.]**

   Agora é possível colocar o componente de mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de mídia 3D a uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se você estiver usando o Adobe Experience Manager como seu sistema de gerenciamento de conteúdo da Web, poderá adicionar ativos 3D às suas páginas da Web por meio do componente Mídia 3D.

Consulte também [Adicionar ativos do Dynamic Media às páginas.](/help/assets/adding-dynamic-media-assets-to-pages.md)

1. Abra o AEM Sites e selecione a página da Web à qual deseja adicionar o componente de mídia 3D do Dynamic Media.
1. Toque no ícone **[!UICONTROL Editar]** (lápis) para abrir a página no editor de páginas. Certifique-se de que o modo **[!UICONTROL Edit]** esteja selecionado perto do canto superior direito da página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Na barra de ferramentas, toque no ícone do Painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, toque no ícone de sinal de mais para abrir a lista **[!UICONTROL Componentes]**.

   ![3d-mídia-componente-arrastar-soltar](/help/assets/assets-dm/3d-assets-filter.png)

1. Arraste o componente **[!UICONTROL 3D Media]** da lista **[!UICONTROL Componentes]** para o local na página onde deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuir um ativo 3D a um componente de mídia 3D.](#assigning-a-three-d-asset-to-the-component)

### Opcional - Configuração do componente de mídia 3D {#configuring-the-three-d-component}

1. No editor de páginas do AEM Sites, selecione o componente **[!UICONTROL Visualizador de mídia 3D]** que você adicionou anteriormente à página.
1. Toque no ícone **[!UICONTROL Configuração]** (chave) para abrir a caixa de diálogo de configuração do componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinição do visualizador , selecione **[!UICONTROL Dimensional]** para atribuir a predefinição do visualizador dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. No canto superior direito, toque na marca de seleção para salvar as alterações.

## Atribuição de um ativo 3D ao componente de mídia 3D {#assigning-a-three-d-asset-to-the-component}

Após adicionar um componente de Mídia 3D a uma página da Web, é possível atribuir um ativo 3D a ela.

Consulte [Adicionar o componente de mídia 3D a uma página da Web.](#adding-the-three-d-media-component-to-a-web-page)

1. No editor de páginas do AEM Sites, clique no ícone **[!UICONTROL Assets]** para abrir **[!UICONTROL Assets]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar apenas os tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que deseja visualizar na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral Ativos e solte-o no componente **[!UICONTROL Mídia 3D]** que você adicionou anteriormente à página.

   ![Atribuir ativo 3d ao componente de mídia 3d](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Embora uma página da Web esteja no modo **[!UICONTROL Edit]** do AEM Sites, o componente de Mídia 3D exibe o ativo 3D, mas nenhuma interação com o ativo é possível. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

## Publicar ativos 3D estáticos do Dynamic Media {#publishing-three-d-assets}

O Dynamic Media aceita uma variedade de formatos de arquivo 3D compatíveis com *conteúdo estático* no Dynamic Media. O conteúdo estático significa que você pode fazer upload e publicar ativos 3D, mas não há suporte para *dynamic* criação de imagens ou ajuste de imagens associado ao ativo 3D. Isso ocorre porque o Dynamic Media Imaging Server não reconhece formatos 3D. Dessa forma, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL para o ativo 3D segue a estrutura normal de URL do Dynamic Media. No entanto, não é possível editar nenhum parâmetro no URL do ativo, ao contrário dos ativos de imagem tradicionais na Dynamic Media.

Consulte também [Obter um URL para um ativo estático.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset)

Na **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda de sua data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se estiver usando o AEM como o WCM, use esse método de publicação para adicionar os ativos 3D do Dynamic Media diretamente na página da Web.

Consulte também [Publicação de ativos do Dynamic Media.](publishing-dynamicmedia-assets.md)

Consulte também [Publicar páginas.](/help/sites-authoring/publishing-pages.md)

**Publicar ativos 3D estáticos do Dynamic Media**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL) para exibi-lo na página de detalhes do ativo.
1. Na barra de ferramentas, toque em **[!UICONTROL Publicação rápida.]**

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Toque em **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome de arquivo do ativo 3D, toque em **[!UICONTROL Representações.]**

   ![3d-representação de ativos](/help/assets/assets-dm/3d-asset-renditions.png)

1. Toque em **[!UICONTROL original.]** Quando um ativo 3D é publicado (ou &quot;ativado&quot;), o botão  **** URL aparece próximo ao canto inferior esquerdo da página se todas as condições de ativo 3D a seguir forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado no Sistema de Produção de Imagens da Dynamic Media (IPS).
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Toque em **[!UICONTROL URL]** para exibir o URL de produção direta do ativo 3D que você pode copiar e usar nas páginas da Web.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos 3D do Dynamic Media se você estiver *not* usando o AEM como WCM.

* **[!UICONTROL URL]**  - Use  **** URLs se estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros e quiser vincular ativos Dynamic Media 3D às suas páginas da Web usando o Visualizador de dimensões.

   Consulte [Vincular URLs ao aplicativo da Web.](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset)

* **[!UICONTROL Incorporar]**  - Use  **** Incorporar quando quiser visualizar um ativo Dynamic Media 3D incorporado em uma página da Web usando o Visualizador de dimensões. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar]**.

   Consulte [Incorporar o visualizador de vídeo, imagem ou visualizador de dimensões do Dynamic Media em uma página da Web.](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page)