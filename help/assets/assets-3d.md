---
title: Trabalhar com ativos 3D no Dynamic Media
description: Saiba como trabalhar com ativos 3D no Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
source-git-commit: 787c0c25da2258f234d3c821038d62bf8ef68932
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 4%

---

# Trabalhar com ativos 3D no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media permite carregar, gerenciar, visualizar e fornecer ativos 3D como experiências imersivas.

* Publicação com um clique (usando **[!UICONTROL Publicação rápida]** na barra de ferramentas) de ativos 3D para gerar um URL.
* Suporte otimizado para visualizar ativos 3D com a predefinição interativa de visualizador Dimensional de alta qualidade fornecida pela Adobe Dimension.
* O componente WCM Mídia 3D permite adicionar facilmente ativos 3D às páginas do Adobe Experience Manager Sites.

Não há nenhuma configuração adicional necessária para usar ativos 3D no Dynamic Media.

![Sapato em 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *Página de detalhes de um sapato tridimensional.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatíveis com o Dynamic Media {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos 3D.

Consulte também [Formatos 3D compatíveis](/help/assets/assets-formats.md).

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | modelo/gltf-binário | Inclui os materiais e as texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | *Suporte apenas para ingestão; nenhuma visualização ou interação está disponível.* USDZ é um formato 3D proprietário que pode ser visualizado originalmente por dispositivos Safari e iOS. |

>[!NOTE]
>
>O componente do WCM de mídia 3D e a visualização 3D na página Detalhes de um ativo não são compatíveis com a versão mais recente do Chrome (97.x). Em vez disso, para trabalhar com ativos 3D, use o Firefox ou o Safari ou use uma versão anterior do Chrome (96.x).

## Início rápido: Ativos 3D no Dynamic Media {#quick-start-three-d}

A seguinte descrição passo a passo do fluxo de trabalho foi criada para ajudar você a ativar e executar rapidamente com ativos 3D no modo Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Os ativos 3D não são compatíveis com o Dynamic Media - Modo híbrido.

Antes de trabalhar com ativos 3D no Dynamic Media, verifique se o administrador do Experience Manager já ativou e configurou o Dynamic Media Cloud Services no modo Dynamic Media - Scene7.

Consulte [Configurar Dynamic Media Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo Scene7 e [Solução de problemas do Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).

1. **Fazer upload de ativos 3D**

   * [Faça upload de seus ativos 3D para usar no Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formatos de arquivo 3D compatíveis para upload no Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organizar ativos digitais](/help/assets/organize-assets.md#organize-digital-assets).
      * [Pesquisar ativos 3D](/help/assets/search-assets.md).
      * [Usar predicados personalizados para filtrar os resultados da pesquisa](/help/assets/search-assets.md#custompredicates).
   * Exibir ativos 3D

      * [Exibir e interagir com ativos 3D](#viewing-three-d-assets).
      * [Gerenciar a predefinição do visualizador dimensional](/help/assets/managing-viewer-presets.md).
   * Trabalhar com metadados de ativos 3D

      * [Gerenciar metadados para ativos digitais](/help/assets/metadata.md).
      * [Esquemas de metadados](/help/assets/metadata-schemas.md).



1. **Publicar ativos 3D**

   * [Publicar ativos estáticos em Dynamic Media 3D](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional](#alternate-publish-methods)

## Sobre a visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualizar e interagir com ativos 3D de duas maneiras diferentes: na página Detalhes do ativo e a partir do componente Mídia 3D no Experience Manager Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

O tempo que leva para abrir um ativo 3D na exibição de página Detalhes do ativo depende de vários fatores. Esses fatores incluem informações como as seguintes:

* Largura de banda para o servidor.
* Latências para o servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes a serem considerados ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

>[!TIP]
>
>Você pode abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação de um ativo 3D sem a necessidade de fazer upload primeiro de qualquer arquivo 3D. A predefinição do visualizador Dimensional tem um ativo 3D integrado com o qual você pode interagir.
>
>Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

## Exibir e interagir com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualizar ativos usando a interface do software](/help/assets/previewing-assets.md).

**Para visualizar e interagir com um ativo 3D na página de detalhes do ativo:**

1. Certifique-se de ter carregado ativos 3D no Experience Manager.

   Consulte [Faça upload de seus ativos 3D para usar no Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. De Experience Manager, no **[!UICONTROL Navegação]** página, vá para **[!UICONTROL Ativos]** > **[!UICONTROL Arquivos]**.
1. Próximo ao canto superior direito da página, da **[!UICONTROL Exibir]** , selecione **[!UICONTROL Exibição de cartão]**.
1. Navegue até o ativo 3D que deseja visualizar.
1. Selecione o cartão do ativo 3D.
1. Na página de visualização de detalhes do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Rode a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo e arraste. | Pressione com um único dedo e arraste. |
   | **Deslocar a câmera** | Deslocar a vista para a esquerda, para a direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos e arraste. |
   | **Zoom da câmera** | Mova para dentro e para fora de áreas na cena 3D. | Roda de rolagem. | Um beliscão de dois dedos. |
   | **Recenter a câmera** | Insira novamente sua câmera em um ponto em um objeto na cena 3D. | Duplo clique. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável. |  |  |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone de tela cheia. |  |  |

1. No canto superior direito da página, selecione **[!UICONTROL Fechar]** para retornar à página Ativos .

## Visualização e interação com um ativo 3D dentro de um componente de mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está em **[!UICONTROL Editar]** , nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o **[!UICONTROL Visualizar]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

>[!IMPORTANT]
>
>Essa tarefa só pode ser realizada depois de ter adicionado um componente de mídia 3D a uma página da Web e atribuído um ativo 3D ao componente. Consulte [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page) e [Atribuição de um ativo 3D a um componente de mídia 3D](#assigning-a-three-d-asset-to-the-component).

Consulte também [Visualizar ativos usando a interface do software](/help/assets/previewing-assets.md).

**Para visualizar e interagir com um ativo 3D dentro de um componente de mídia 3D:**

1. Enquanto uma página da Web está em **[!UICONTROL Editar]** , execute um dos seguintes procedimentos:

   * Próximo ao canto superior direito da página, selecione **[!UICONTROL Visualizar]** para inserir **[!UICONTROL Visualizar]** modo.
   * Excluir `/editor.html` no URL da página no navegador.

Um ativo 3D totalmente interativo, como exibido em    ![Ativo 3D exibido dentro do componente Mídia 3D](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Um ativo 3D totalmente interativo, como exibido em **[!UICONTROL Visualizar]** modo.

1. Enquanto em **[!UICONTROL Visualizar]** , execute um dos seguintes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Rode a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo e arraste. | Pressione com um único dedo e arraste. |
   | **Deslocar a câmera** | Deslocar a vista para a esquerda, para a direita, para cima ou para baixo. | Clique com o botão direito + arraste. | Pressione com dois dedos e arraste. |
   | **Zoom da câmera** | Mova para dentro e para fora de áreas na cena 3D. | Roda de rolagem. | Um beliscão de dois dedos. |
   | **Recenter a câmera** | Insira novamente sua câmera em um ponto em um objeto na cena 3D. | Duplo clique. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável. |  |  |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone de tela cheia. |  |  |

## Sobre como trabalhar com o componente de mídia 3D {#working-with-three-d-media-component}

O Dynamic Media inclui um componente de mídia 3D do Dynamic Media que pode ser usado no Adobe Experience Manager Sites para permitir a visualização interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de mídia 3D ao modelo da página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configurar o componente de mídia 3D](#configuring-the-three-d-component)
* [Atribuir um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component)

## Adicionar o componente de mídia 3D ao modelo da página {#adding-three-d-media-component-to-page-template}

1. Navegar para **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**.
1. Navegue até o modelo de página no qual você deseja ativar o componente 3D e selecione o modelo.
1. Selecionar **[!UICONTROL Editar]** para que você possa abrir o template.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione **[!UICONTROL Estrutura]** , se ainda não estiver ativo.

   ![3d-media-component-structure](/help/assets/assets-dm/3d-media-component-structure.png)

1. Selecione uma área vazia no **[!UICONTROL Contêiner de layout]** região para selecioná-la e abrir a barra de ferramentas associada.
1. Na barra de ferramentas, selecione o **[!UICONTROL Política]** ícone para abrir o **[!UICONTROL Editor de políticas]**.
1. No **[!UICONTROL Propriedades]** na seção **[!UICONTROL Componentes permitidos]** guia , role até **[!UICONTROL Dynamic Media]**, em seguida, expanda a lista e marque **[!UICONTROL Mídia 3D]**.
1. Selecionar **[!UICONTROL Concluído]** para salvar as alterações e fechar o **[!UICONTROL Editor de políticas]**.

   Agora é possível colocar o componente de mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de mídia 3D em uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se você usa o Experience Manager como seu sistema de gerenciamento de conteúdo da Web, é possível adicionar ativos 3D às suas páginas da Web por meio do componente Mídia 3D.

Consulte também [Adicionar ativos do Dynamic Media nas páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para adicionar o componente de mídia 3D em uma página da Web:**

1. Abra o Experience Manager Sites e selecione a página da Web à qual deseja adicionar o componente de mídia 3D do Dynamic Media.
1. Selecione o **[!UICONTROL Editar]** (lápis) para que você possa abrir a página no editor de páginas. Certifique-se de que **[!UICONTROL Editar]** O modo é selecionado próximo ao canto superior direito da página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Na barra de ferramentas, selecione o ícone do painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, selecione o ícone de sinal de mais para abrir o **[!UICONTROL Componentes]** lista.

   ![3d-mídia-componente-arrastar-soltar](/help/assets/assets-dm/3d-assets-filter.png)

1. Arraste o **[!UICONTROL Mídia 3D]** do **[!UICONTROL Componentes]** liste para o local na página onde você deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuir um ativo 3D ao componente de mídia 3D](#assigning-a-three-d-asset-to-the-component).

### Opcional - Configurar o componente de mídia 3D {#configuring-the-three-d-component}

1. No editor de páginas do Experience Manager Sites, selecione o **[!UICONTROL Visualizador de mídia 3D]** componente adicionado anteriormente à página.
1. Selecione o **[!UICONTROL Configuração]** ícone (chave) para abrir a caixa de diálogo configuração do componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinição do visualizador , selecione **[!UICONTROL Dimensões]** para atribuir a predefinição do visualizador Dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. No canto superior direito, selecione a marca de seleção para salvar suas alterações.

## Atribuir um ativo 3D ao componente de mídia 3D {#assigning-a-three-d-asset-to-the-component}

Após adicionar um componente de Mídia 3D a uma página da Web, é possível atribuir um ativo 3D a ela.

Consulte [Adicionar o componente de mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page).

**Para atribuir um ativo 3D ao componente de mídia 3D:**

1. No editor de páginas do Experience Manager Sites, selecione o **[!UICONTROL Ativos]** ícone para abrir **[!UICONTROL Ativos]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar apenas tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que deseja visualizar na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral Ativos e solte-o no **[!UICONTROL Mídia 3D]** componente adicionado anteriormente à página.

   ![Atribuir ativo 3D ao componente de mídia 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Enquanto uma página da Web estiver na Experience Manager Sites **[!UICONTROL Editar]** modo , o componente Mídia 3D exibe o ativo 3D, mas nenhuma interação com o ativo é possível. Para tornar o ativo interativo, você pode usar o **[!UICONTROL Visualizar]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de mídia 3D.

## Publicar ativos estáticos em Dynamic Media 3D {#publishing-three-d-assets}

O Dynamic Media aceita vários formatos de arquivo 3D compatíveis com *conteúdo estático* no Dynamic Media. O conteúdo estático significa que você pode fazer upload e publicar ativos 3D, mas não há suporte para *imagem variável* ou reversão de imagem associada ao ativo 3D. Isso ocorre porque o Dynamic Media Imaging Server não reconhece formatos 3D. Dessa forma, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL para o ativo 3D segue a estrutura normal de URL do Dynamic Media. No entanto, não é possível editar nenhum parâmetro no URL do ativo, ao contrário dos ativos de imagem tradicionais na Dynamic Media.

Consulte também [Obter um URL para um ativo estático](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

No **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda de sua data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se você usa o Experience Manager como WCM, use esse método de publicação para adicionar os ativos 3D do Dynamic Media diretamente na página da Web.

Consulte também [Publicar ativos do Dynamic Media](publishing-dynamicmedia-assets.md).

Consulte também [Publicar páginas](/help/sites-authoring/publishing-pages.md).

**Para publicar ativos 3D estáticos do Dynamic Media:**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL) para exibi-lo na página de detalhes do ativo.
1. Na barra de ferramentas, selecione **[!UICONTROL Publicação rápida]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Selecionar **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome de arquivo do ativo 3D, selecione **[!UICONTROL Representações]**.

   ![3d-representação de ativos](/help/assets/assets-dm/3d-asset-renditions.png)

1. Selecionar **[!UICONTROL original]**. Quando um ativo 3D é publicado (ou &quot;ativado&quot;), a variável **[!UICONTROL URL]** será exibido próximo ao canto inferior esquerdo da página se todas as seguintes condições de ativos 3D forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado no Sistema de produção de imagem da Dynamic Media (IPS).
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Selecionar **[!UICONTROL URL]** para que você possa exibir o URL de produção direta do ativo 3D, que pode ser copiado e usado nas páginas da Web.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos 3D do Dynamic Media se você *not* use o Experience Manager como o WCM.

* **[!UICONTROL URL]** - Uso **[!UICONTROL URL]** se você estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros e quiser vincular ativos 3D do Dynamic Media às suas páginas da Web usando o visualizador Dimensional.

   Consulte [Vincular URLs ao aplicativo da Web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorporar]** - Uso **[!UICONTROL Incorporar]** quando quiser exibir um ativo 3D do Dynamic Media incorporado em uma página da Web usando o visualizador Dimensional. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na variável **[!UICONTROL Incorporar]** caixa de diálogo.

   Consulte [Incorporar o vídeo do Dynamic Media, o visualizador de imagens ou o visualizador dimensional em uma página da Web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
