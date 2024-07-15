---
title: Trabalhar com ativos 3D no Dynamic Media
description: Saiba como fazer upload, gerenciar, visualizar e fornecer ativos 3D no Dynamic Media como uma experiência imersiva.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
feature: 3D Assets,Asset Management
role: User, Admin
exl-id: 01c96f1e-c0e6-497d-bd7a-c0fd547a34da
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2354'
ht-degree: 2%

---

# Trabalhar com ativos 3D no Dynamic Media {#working-with-three-d-assets-dm}

O Dynamic Media permite carregar, gerenciar, visualizar e fornecer ativos 3D como experiências imersivas.

* Publicação de ativos 3D com um clique (usando o **[!UICONTROL Quick Publish]** na barra de ferramentas) para gerar uma URL.
* Suporte otimizado para visualizar ativos 3D com a predefinição interativa e de alta qualidade do visualizador dimensional baseada no Adobe Dimension.
* O componente WCM do Media 3D permite adicionar facilmente ativos 3D às páginas do Adobe Experience Manager Sites.

Não há necessidade de configuração adicional para usar ativos 3D no Dynamic Media.

![Sapato em 3d](/help/assets/assets-dm/3d-dimensional-viewer-quickpublish-url-embed2.png) *Página de detalhes de um sapato tridimensional.*

<!-- See also [Dynamic Media 3D Release Notes](/help/release-notes/aem3d-release-notes.md). -->

## Formatos 3D compatíveis com o Dynamic Media {#supported-three-d-file-formats-in-dm}

O Dynamic Media é compatível com os seguintes formatos 3D.

Consulte também [formatos 3D compatíveis](/help/assets/assets-formats.md).

| Extensão de arquivo 3D | Formato do arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary | Inclui os materiais e texturas como um único ativo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| USDZ | Arquivo Zip de Descrição de Cena Universal | model/vnd.usdz+zip | *Suporte somente para assimilação; não há visualização ou interação disponíveis.O* USDZ é um formato 3D proprietário que pode ser visualizado nativamente por dispositivos Safari e iOS. |

>[!NOTE]
>
>O componente WCM do Media 3D e a visualização 3D na página Detalhes de um ativo não são compatíveis com a versão mais recente do Chrome (97.x). Em vez disso, para trabalhar com ativos 3D, use o Firefox ou o Safari, ou use uma versão anterior do Chrome (96.x).

## Início rápido: ativos 3D no Dynamic Media {#quick-start-three-d}

A descrição do fluxo de trabalho passo a passo a seguir foi projetada para ajudar você a começar a usar rapidamente os ativos 3D no modo Dynamic Media - Scene7.

>[!IMPORTANT]
>
>Os ativos 3D não são compatíveis com o Dynamic Media - modo híbrido.

Antes de trabalhar com ativos 3D no Dynamic Media, verifique se o administrador do Experience Manager já ativou e configurou o Dynamic Media Cloud Service no modo Dynamic Media - Scene7.

Consulte [Configurar Dynamic Media Cloud Service ](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services) em Configuração do Dynamic Media - Modo Scene7 e [Solução de problemas do Dynamic Media - Modo Scene7](/help/assets/troubleshoot-dms7.md).

1. **Carregar ativos 3D**

   * [Carregue seus ativos 3D para uso no Dynamic Media](/help/assets/manage-assets.md#uploading-assets).
   * [Formatos de arquivo 3D com suporte para carregamento no Dynamic Media](#supported-three-d-file-formats-in-dm).

1. **Gerenciar ativos 3D**

   * Organizar e pesquisar ativos 3D

      * [Organize ativos digitais](/help/assets/organize-assets.md#organize-digital-assets).
      * [Pesquisar ativos 3D](/help/assets/search-assets.md).
      * [Use predicados personalizados para filtrar os resultados da pesquisa](/help/assets/search-assets.md#custompredicates).

   * Exibir ativos 3D

      * [Exibir e interagir com ativos 3D](#viewing-three-d-assets).
      * [Gerenciar a predefinição do visualizador Dimensional](/help/assets/managing-viewer-presets.md).

   * Trabalhar com metadados de ativos 3D

      * [Gerenciar metadados para ativos digitais](/help/assets/metadata.md).
      * [Esquemas de metadados](/help/assets/metadata-schemas.md).

1. **Publish 3D Assets**

   * [Ativos estáticos do Dynamic Media 3D para Publish](#publishing-three-d-assets)
   * [Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional](#alternate-publish-methods)

## Sobre visualização e interação com ativos 3D {#viewing-three-d-assets}

Esta seção descreve como visualizar e interagir com ativos 3D de duas maneiras diferentes: na página Detalhes do ativo e no componente Mídia 3D no Experience Manager Sites.

O visualizador 3D interativo inclui, entre outras coisas, uma coleção de controles interativos de câmera que permitem que você orbite, amplie e desloque o ativo 3D.

O tempo necessário para abrir um ativo 3D na exibição de página Detalhes do ativo depende de vários fatores. Esses fatores incluem coisas como as seguintes:

* Largura de banda do servidor.
* Latências no servidor
* Complexidade da imagem.

Além disso, os recursos do computador cliente - como estação de trabalho, notebook ou dispositivo de toque móvel - também são importantes ao manipular a câmera interativamente. Um sistema razoavelmente eficiente com boas capacidades gráficas pode tornar a experiência de visualização 3D interativa mais suave e favorável.

>[!TIP]
>
>É possível abrir a predefinição do visualizador Dimensional no Editor de predefinições do visualizador para praticar a navegação em um ativo 3D sem precisar primeiro fazer upload de arquivos 3D. A predefinição do visualizador Dimensional tem um ativo 3D incorporado para você interagir.
>
>Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

## Exibir e interagir com um ativo 3D na página de detalhes do ativo {#viewing-three-d-assets-from-asset-details-page}

Consulte também [Visualizar ativos usando a interface de software](/help/assets/previewing-assets.md).

**Para exibir e interagir com um ativo 3D a partir da página de detalhes do ativo:**

1. Verifique se você carregou ativos 3D no Experience Manager.

   Consulte [Carregar seus ativos 3D para uso no Dynamic Media](/help/assets/manage-assets.md#uploading-assets).

1. No Experience Manager, na página **[!UICONTROL Navegação]**, vá para **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.
1. Próximo ao canto superior direito da página, na lista suspensa **[!UICONTROL Exibir]**, selecione **[!UICONTROL Exibição de Cartão]**.
1. Navegue até um ativo 3D que deseja visualizar.
1. Selecione o cartão do ativo 3D.
1. Na página da exibição de detalhes do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar sua câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar sua câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito do mouse e arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas na cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Selecione duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

1. No canto superior direito da página, selecione **[!UICONTROL Fechar]** para retornar à página do Assets.

## Visualização e interação com um ativo 3D dentro de um componente de Mídia 3D {#interacting-with-asset-inside-three-d-media-component}

Quando uma página da Web está no modo **[!UICONTROL Editar]**, nenhuma interação é possível com um ativo 3D. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de Mídia 3D.

>[!IMPORTANT]
>
>Essa tarefa só pode ser realizada após a adição de um componente de Mídia 3D a uma página da Web e a atribuição de um ativo 3D ao componente. Consulte [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page) e [Atribuir um ativo 3D a um componente de Mídia 3D](#assigning-a-three-d-asset-to-the-component).

Consulte também [Visualizar ativos usando a interface de software](/help/assets/previewing-assets.md).

**Para exibir e interagir com um ativo 3D dentro de um componente de Mídia 3D:**

1. Enquanto a página da Web estiver no modo **[!UICONTROL Editar]**, siga um destes procedimentos:

   * Próximo ao canto superior direito da página, selecione **[!UICONTROL Visualização]** para entrar no modo **[!UICONTROL Visualização]**.
   * Exclua `/editor.html` da URL da página no navegador.

   ![Ativo 3D sendo exibido dentro do componente de Mídia 3D](/help/assets/assets-dm/3d-asset-in-3d-media.png)
Um ativo 3D totalmente interativo conforme exibido no modo **[!UICONTROL Visualização]**.

1. No modo **[!UICONTROL Visualizar]**, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar sua câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar sua câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito do mouse e arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas na cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Selecione duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

## Como trabalhar com o componente de Mídia 3D {#working-with-three-d-media-component}

O Dynamic Media inclui um componente de mídia 3D do Dynamic Media que pode ser usado no Adobe Experience Manager Sites para permitir a visualização interativa de modelos 3D em suas páginas da Web.

* [Adicionar o componente de Mídia 3D ao modelo de página](#adding-three-d-media-component-to-page-template)
* [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page)
   * [Opcional - Configurar o componente de Mídia 3D](#configuring-the-three-d-component)
* [Atribuir um ativo 3D ao componente de Mídia 3D](#assigning-a-three-d-asset-to-the-component)

## Adicionar o componente de Mídia 3D ao modelo de página {#adding-three-d-media-component-to-page-template}

1. Navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]**.
1. Navegue até o modelo de página em que deseja ativar o componente 3D e selecione o modelo.
1. Selecione **[!UICONTROL Editar]** para poder abrir o modelo.
1. Próximo ao canto superior direito da página, no menu suspenso, selecione o modo **[!UICONTROL Estrutura]**, se ele ainda não estiver ativo.

   ![3d-estrutura-componente-de-mídia](/help/assets/assets-dm/3d-media-component-structure.png)

1. Selecione uma área vazia na região **[!UICONTROL Contêiner de layout]** para selecioná-la e abrir sua barra de ferramentas associada.
1. Na barra de ferramentas, selecione o ícone **[!UICONTROL Política]** para abrir o **[!UICONTROL Editor de Políticas]**.
1. Na seção **[!UICONTROL Propriedades]**, na guia **[!UICONTROL Componentes Permitidos]**, navegue até **[!UICONTROL Dynamic Media]**, expanda a lista e verifique a **[!UICONTROL Mídia 3D]**.
1. Selecione **[!UICONTROL Concluído]** para salvar as alterações e fechar o **[!UICONTROL Editor de Políticas]**.

   Agora é possível colocar o componente de Mídia 3D do Dynamic Media em todas as páginas que usam esse modelo.

## Adicionar o componente de Mídia 3D em uma página da Web {#adding-the-three-d-media-component-to-a-web-page}

Se você usa o Experience Manager como seu sistema de gerenciamento de conteúdo na Web, é possível adicionar ativos 3D às suas páginas da Web por meio do componente de Mídia 3D.

Consulte também [Adicionar ativos do Dynamic Media nas páginas](/help/assets/adding-dynamic-media-assets-to-pages.md).

**Para adicionar o componente de Mídia 3D em uma página da Web:**

1. Abra o Experience Manager Sites e selecione a página da Web à qual deseja adicionar o componente de Mídia Dynamic Media 3D.
1. Selecione o ícone **[!UICONTROL Editar]** (lápis) para abrir a página no editor de páginas. Verifique se o modo **[!UICONTROL Editar]** está selecionado próximo ao canto superior direito da página.

   ![3d-media-component-add](/help/assets/assets-dm/3d-media-component-edit.png)

1. Na barra de ferramentas, selecione o ícone Painel lateral para alternar ou &quot;ativar&quot; a exibição do painel.

1. No painel lateral, selecione o ícone de sinal de mais para abrir a lista **[!UICONTROL Componentes]**.

   ![3d-componente-mídia-arrastar-soltar](/help/assets/assets-dm/3d-assets-filter.png)

1. Arraste o componente **[!UICONTROL Mídia 3D]** da lista **[!UICONTROL Componentes]** para o local da página em que você deseja que o visualizador 3D apareça.

Agora você está pronto para atribuir um ativo 3D ao componente.

Consulte [Atribuir um ativo 3D ao componente de Mídia 3D](#assigning-a-three-d-asset-to-the-component).

### Opcional - Configurar o componente de Mídia 3D {#configuring-the-three-d-component}

1. No editor de páginas do Experience Manager Sites, selecione o componente **[!UICONTROL Visualizador de mídia 3D]** que você adicionou anteriormente à página.
1. Selecione o ícone (chave inglesa) **[!UICONTROL Configuração]** para abrir a caixa de diálogo de configuração do componente.

   ![3d-media-component-config](/help/assets/assets-dm/3d-media-component-config.png)

1. Na caixa de diálogo Mídia 3D, na lista suspensa Predefinição do visualizador, selecione **[!UICONTROL Dimensional]** para atribuir a predefinição do visualizador Dimensional ao componente.

   ![3d-media-component-edit-config](/help/assets/assets-dm/3d-media-component-edit-config.png)

1. No canto superior direito, selecione a marca de seleção para salvar as alterações.

## Atribuir um ativo 3D ao componente de Mídia 3D {#assigning-a-three-d-asset-to-the-component}

Depois de adicionar um componente de Mídia 3D a uma página da Web, é possível atribuir um ativo 3D a ele.

Consulte [Adicionar o componente de Mídia 3D a uma página da Web](#adding-the-three-d-media-component-to-a-web-page).

**Para atribuir um ativo 3D ao componente de Mídia 3D:**

1. No editor de páginas do Experience Manager Sites, selecione o ícone **[!UICONTROL Assets]** para abrir o **[!UICONTROL Assets]** no painel lateral.
1. Na lista suspensa, selecione **[!UICONTROL 3D]** para mostrar somente tipos de arquivos de ativos 3D.
1. No painel lateral, procure ou role até o ativo 3D que deseja visualizar na página que está sendo editada.
1. Arraste o ativo 3D do painel lateral do Assets e solte-o no componente **[!UICONTROL Mídia 3D]** adicionado anteriormente à página.

   ![Atribuir ativo 3D ao componente de Mídia 3D](/help/assets/assets-dm/3d-asset-add.png)

>[!NOTE]
>
>Enquanto a página da Web está no modo Experience Manager Sites **[!UICONTROL Editar]**, o componente de Mídia 3D exibe o ativo 3D, mas não é possível haver interação com ele. Para tornar o ativo interativo, você pode usar o recurso **[!UICONTROL Visualização]** para exibir a página da Web no editor de páginas com acesso total à funcionalidade do componente de Mídia 3D.

## Ativos estáticos do Dynamic Media 3D para Publish {#publishing-three-d-assets}

O Dynamic Media aceita vários formatos de arquivo 3D com suporte como *conteúdo estático* no Dynamic Media. O conteúdo estático significa que você pode carregar e publicar ativos 3D, mas não há suporte para *imagem variável* ou remontagem de imagens associada ao ativo 3D. O motivo é que o Dynamic Media Imaging Server não reconhece os formatos 3D. Assim, depois de publicar um ativo 3D no Dynamic Media, você tem um URL instantâneo que pode ser copiado. O URL do ativo 3D segue a estrutura normal do URL do Dynamic Media. No entanto, não é possível editar parâmetros no URL do ativo, ao contrário dos ativos de imagem tradicionais no Dynamic Media.

Consulte também [Obter uma URL para um ativo estático](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-a-static-asset).

Na **[!UICONTROL Exibição de cartão]**, um pequeno ícone de globo aparece logo abaixo do nome de um ativo e à esquerda de sua data e hora para indicar que ele foi publicado. Na **[!UICONTROL Exibição em lista]**, uma coluna **[!UICONTROL Publicado]** indica quais ativos foram publicados ou não.

Se você usar o Experience Manager como o WCM, use esse método de publicação para adicionar os ativos do Dynamic Media 3D diretamente na sua página da Web.

Consulte também [Publish Dynamic Media Assets](publishing-dynamicmedia-assets.md).

Consulte também [páginas do Publish](/help/sites-authoring/publishing-pages.md).

**Para publicar ativos 3D estáticos do Dynamic Media:**

1. Abra um ativo 3D (formato de arquivo GLB, OBJ ou STL) para exibi-lo na página de detalhes do ativo.
1. Na barra de ferramentas, selecione **[!UICONTROL Quick Publish]**.

   ![3d-asset-quick-publish](/help/assets/assets-dm/3d-asset-quick-publish.png)

1. Selecione **[!UICONTROL Fechar]** para sair da caixa de diálogo e retornar à página de detalhes do ativo.
1. Na lista suspensa à esquerda do nome do arquivo do ativo 3D, selecione **[!UICONTROL Representações]**.

   ![3d-asset-renditions](/help/assets/assets-dm/3d-asset-renditions.png)

1. Selecione **[!UICONTROL original]**. Quando um ativo 3D é publicado (ou &quot;ativado&quot;), o botão **[!UICONTROL URL]** é exibido próximo ao canto inferior esquerdo da página se todas as condições de ativos 3D a seguir forem atendidas:
   * O ativo 3D é um formato compatível (GLB, OBJ, STL e USDZ).
   * O ativo 3D foi assimilado no Sistema de produção de imagem (IPS) da Dynamic Media.
   * O ativo 3D é publicado.

   ![3d-asset-url](/help/assets/assets-dm/3d-asset-url.png)

1. Selecione **[!UICONTROL URL]** para exibir a URL de produção direta do ativo 3D, que pode ser copiada e usada em páginas da Web.

### Métodos alternativos para publicar ativos 3D do Dynamic Media usando o visualizador Dimensional {#alternate-publish-methods}

Use os dois métodos a seguir para publicar ativos 3D do Dynamic Media caso *não* use o Experience Manager como WCM.

* **[!UICONTROL URL]** - Use **[!UICONTROL URL]** se estiver usando um sistema de gerenciamento de conteúdo da Web de terceiros e quiser vincular ativos do Dynamic Media 3D às suas páginas da Web usando o visualizador Dimensional.

  Consulte [Vincular URLs ao aplicativo Web](/help/assets/linking-urls-to-yourwebapplication.md#obtaining-a-url-for-an-asset).

* **[!UICONTROL Incorporar]** - Use **[!UICONTROL Incorporar]** quando quiser exibir um ativo 3D do Dynamic Media inserido em uma página da Web usando o visualizador Dimensional. Copie o código incorporado na área de transferência para poder colá-lo nuas páginas da Web. A edição do código não é permitida na caixa de diálogo **[!UICONTROL Incorporar]**.

  Consulte [Incorporar o Vídeo do Dynamic Media, o Visualizador de imagens ou o Visualizador dimensional em uma página da Web](/help/assets/embed-code.md#embedding-the-video-or-image-viewer-on-a-web-page).
