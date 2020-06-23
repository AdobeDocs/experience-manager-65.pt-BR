---
title: Visualizar ativos
description: Saiba como pré-visualização ativos no Dynamic Media
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 4%

---


# Visualizar ativos usando a interface de software {#previewing-assets}

Você pode usar a Pré-visualização para ver como um ativo digital que você carregou é exibido quando exibido por um cliente em seu próprio navegador da Web. O visualizador incorporado e entre dispositivos padrão atribuído ao ativo é usado para a Pré-visualização.

Um visualizador é uma coleção de várias configurações ou &quot;predefinições&quot;, como tamanho de exibição do visualizador, comportamento de zoom, esquemas de cores, bordas, fontes e assim por diante, que determinam como os usuários visualizações ativos de mídia avançada em suas telas de computadores e dispositivos móveis.

Além de usar o recurso de Pré-visualização dedicada para vídeos, conjuntos de rotação e conjuntos de imagens, você também pode pré-visualização um ativo usando as predefinições do visualizador que você criou. Ou, use predefinições de imagens para representações de pré-visualização de imagens.

* [Aplicar predefinições de imagens](/help/assets/image-presets.md)
* [Aplicar predefinições do visualizador](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando você está em uma página da Web (Sites) no AEM, não pode visualizar ativos no modo **Editar**. You need to go to **Preview** mode by clicking **Preview** in the upper right-hand corner of the page.

Para ativar ou desativar as predefinições do visualizador na interface do usuário, consulte [Gerenciamento de predefinições](/help/assets/managing-viewer-presets.md)do visualizador.

**Para pré-visualização de ativos usando a interface de software**

1. No **[!UICONTROL Adobe Experience Manager**, na página **[!UICONTROL Navegação**, toque em **[!UICONTROL Ativos]** e em **[!UICONTROL Arquivos]** para acessar os ativos.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL List View.]**
1. (Opcional) Use a coluna **[!UICONTROL Tipo]** para classificar os ativos pelo tipo que deseja pré-visualização.
1. Na coluna **[!UICONTROL Título]** , clique no nome do título (não na imagem em miniatura) do ativo que deseja pré-visualização.
1. Dependendo do tipo de ativo clicado, execute um dos procedimentos a seguir:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de ativo que você clicou</strong><br /> </td>
      <td><strong>É capaz de pré-visualização de ativos em uma representação específica?</strong></td>
      <td><strong>Pode pré-visualização de ativos em um visualizador?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de um ativo 3D no visualizador Dimensional</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione o Visualizador Dimensional.</li>
      <li>Toque em <strong>Redefinir</strong> para retornar a imagem ao zoom original.</li>
      <li>Toque em <strong>Tela cheia</strong> para maximizar o visualizador no dispositivo de exibição.</li>
      </ul>
      <p><strong>Navegação na cena 3D</strong></p>
      <ul>
      <li><p><strong>Rode sua câmera</strong> 3D - Orbite sua visualização em torno da cena 3D e dos objetos.</p> Rato: Clique com o botão esquerdo + Arraste. </p> Tela sensível ao toque: Pressione + Arraste.</p></li>
      <li><p><strong>Deslocar sua câmera</strong> - Desloce sua visualização para a esquerda, direita, para cima e para baixo.</p> Rato: Clique com o botão direito do mouse + Arraste. </p> Tela sensível ao toque: Pressione com dois dedos + Arraste.</p></li>
      <li><p><strong>Zoom na sua câmera</strong> - Zoom na câmera para mover para dentro e para fora de áreas na cena 3D.</p> Rato: Roda de rolagem. </p> Tela sensível ao toque: Dedo apertado.</p></li>
      <li><p><strong>Recenter your camera</strong> - Faça a órbita de sua visualização em torno da cena 3D e dos objetos.</p> Rato: Duplo-clique. </p> Tela sensível ao toque: Toque em Duplo.</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagem</p> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja pré-visualização.</li>
      </ul> <p><strong>Para pré-visualização de ativos em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque com o duplo na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque com o duplo na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Multimídia</td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja pré-visualização.</li>
      </ul> <p>Selecionar uma execução de vídeo de resolução mais alta para a pré-visualização pode fazer com que o vídeo apareça truncado. Isso ocorre porque a pré-visualização de execução mostra a resolução exata que seus clientes verão, tudo isso no contexto do visualizador incorporado usado para a pré-visualização.</p> <p>Quando você pré-visualização um conjunto de vídeo adaptável no nível do ativo, as renderizações são agrupadas em uma única experiência de reprodução. Ou seja, o vídeo adaptável é dimensionado corretamente para exibição e reprodução usando a melhor resolução no contexto do dispositivo de exibição e da velocidade da conexão.<br /> </p> <p><strong>Para pré-visualização de um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imagens</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque com o duplo na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque com o duplo na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de rotação</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque com o duplo na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque com o duplo na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de mídia mista</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque com o duplo na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque com o duplo na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carrossel</td>
      <td>Não</td>
      <td>Sim</td>
      <td><strong>Para pré-visualização de um ativo em um visualizador específico</strong>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione um visualizador que você deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para pré-visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Representações</strong>e, em seguida, selecione a representação que deseja pré-visualização.</li>
      </ul> <p><strong>Para pré-visualização de ativos em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong>e, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque com o duplo na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque com o duplo na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
    </tbody>
    </table>

## Visualização de ativos usando um teclado {#keyboard-navigation-asset-preview}

1. Na interface do usuário Ativos, navegue até uma pasta que contém um ativo que você deseja pré-visualização.

1. Na pasta, pressione as teclas de seta ou `<Tab>` tecla no teclado para selecionar o ativo.

1. Pressione `<Enter>` para abrir o ativo selecionado no modo de pré-visualização.

1. Siga um destes procedimentos:

   * Para aumentar o zoom, pressione `<Tab>` para mover o foco para o ícone de zoom (+) e pressione `<Enter>` uma ou mais vezes para aumentar o zoom incrementalmente.

   * Para diminuir o zoom, pressione `<Tab>` para mover o foco para o ícone de afastar (-) e pressione `<Enter>` uma ou mais vezes para diminuir o zoom gradualmente.

   * Para mover a visualização de um ativo com *zoom* na horizontal ou na vertical, pressione as teclas de seta correspondentes.

   * Pressione `<Shift>` + `<Tab>` para redefinir a visualização e coloque o foco novamente no ativo.
