---
title: Visualizar ativos
description: Saiba como visualizar ativos, como vídeos e imagens, no Dynamic Media aplicando predefinições de imagens e predefinições do visualizador.
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: 7f8cfe155af3b8831e746ced89c11c971e429f69
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 1%

---

# Visualizar ativos usando a interface de software {#previewing-assets}

Você pode usar a Visualização para ver a aparência de um ativo digital carregado quando ele é visualizado por um cliente em seu próprio navegador da Web. O visualizador padrão incorporado entre dispositivos atribuído ao ativo é usado para a Pré-visualização.

Um visualizador é uma coleção de várias configurações ou *predefinições*, como tamanho de exibição do visualizador, comportamento de zoom, esquemas de cores, bordas e fontes. Essas predefinições determinam como os usuários visualizam os ativos de mídia avançada nas telas dos computadores e nos dispositivos móveis.

Além de usar o recurso de Visualização dedicado para vídeo, conjuntos de rotação e conjuntos de imagem, também é possível visualizar um ativo usando as predefinições do visualizador criadas. Ou use predefinições de imagens para visualizar representações de imagens.

* [Aplicar predefinições da imagem](/help/assets/image-presets.md)
* [Aplicar predefinições do visualizador](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando você está em uma página da Web (Sites) no Adobe Experience Manager, não pode visualizar ativos no **Editar** modo. Acesse o modo Visualização clicando em **[!UICONTROL Visualizar]** no canto superior direito da página.

Para ativar ou desativar as predefinições do visualizador na interface do usuário, consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

**Para visualizar ativos usando a interface do software:**

1. De **[!UICONTROL Adobe Experience Manager]**, no **[!UICONTROL Navegação]** selecione **[!UICONTROL Assets]**, depois **[!UICONTROL Arquivos]** para acessar ativos.
1. Próximo ao canto superior direito da página, no **[!UICONTROL Exibir]** selecione **[!UICONTROL Exibição de lista]**.
1. (Opcional) Use o **[!UICONTROL Tipo]** para classificar os ativos pelo tipo que deseja visualizar.
1. No **[!UICONTROL Título]** clique no nome do título (não na imagem em miniatura) do ativo que deseja visualizar.
1. Dependendo do tipo de ativo em que você clicou, execute um dos procedimentos a seguir:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de ativo em que você clicou</strong><br /> </td>
      <td><strong>É possível visualizar o ativo em uma representação específica?</strong></td>
      <td><strong>É possível visualizar o ativo em um visualizador?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo 3D no visualizador Dimensional</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e, em seguida, selecione o visualizador Dimensional.</li>
      <li>Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.</li>
      <li>Selecionar <strong>Tela cheia</strong> para maximizar o visualizador no dispositivo de exibição.</li>
      </ul>
      <p><strong>Navegar pela cena 3D</strong></p>
      <ul>
      <li><p><strong>Girar sua câmera 3D</strong> - Gire a visualização em torno da cena 3D e dos objetos.</p> Mouse: Clique com o botão esquerdo + arraste </p> Tela sensível ao toque: pressione + arraste</p></li>
      <li><p><strong>Deslocar a câmera</strong> - Desloque sua visualização para a esquerda, direita, para cima e para baixo.</p> Mouse: clique com o botão direito do mouse + arraste </p> Tela sensível ao toque: pressione dois dedos + arraste</p></li>
      <li><p><strong>Aplicar zoom à sua câmera</strong> - Use o zoom da câmera para que você possa mover para dentro e para fora das áreas na cena 3D.</p> Mouse: roda de rolagem </p> Tela sensível ao toque: pinça no dedo</p></li>
      <li><p><strong>Recentralize sua câmera</strong> - Gire a visualização em torno da cena 3D e dos objetos.</p> Mouse: clique duas vezes </p> Tela sensível ao toque: toque duas vezes</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagem</p> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use o <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.<br /> Se você estiver em uma tela de toque, toque duas vezes na imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Multimídia</td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p>Selecionar uma representação de vídeo de resolução mais alta para visualizar pode fazer com que o vídeo apareça truncado. Esse problema ocorre porque a pré-visualização de representação mostra a resolução exata que seus clientes verão tudo no contexto do visualizador incorporado usado para a pré-visualização.</p> <p>Ao visualizar um conjunto de vídeos adaptáveis no nível do Ativo, as representações são agrupadas em uma experiência de reprodução. Ou seja, o vídeo adaptável é dimensionado corretamente para exibição e reprodução usando a melhor resolução no contexto do dispositivo de visualização e da velocidade de conexão.<br /> </p> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imagens</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use o <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.<br /> Se você estiver em uma tela de toque, toque duas vezes na imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Grupo de rotação</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use o <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.<br /> Se você estiver em uma tela de toque, toque duas vezes na imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de mix de mídia</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use o <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.<br /> Se você estiver em uma tela de toque, toque duas vezes na imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Conjunto do Carousel</td>
      <td>Não</td>
      <td>Sim</td>
      <td><strong>Para visualizar um ativo em um visualizador específico</strong>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione um visualizador que você deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Vídeo 360<br /> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, selecione o ícone para que a lista suspensa seja exibida. Selecionar <strong>Representações</strong>, em seguida, selecione a representação que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, selecione o ícone para que a lista suspensa seja exibida. Selecionar <strong>Visualizadores</strong>, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use o <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecionar <strong>Redefinir</strong> se quiser retornar a imagem para o zoom original.<br /> Se você estiver em uma tela de toque, toque duas vezes na imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
    </tbody>
    </table>

## Visualizar ativos usando um teclado {#keyboard-navigation-asset-preview}

1. Na interface do Assets, navegue até uma pasta que contenha um ativo que você deseja visualizar.

1. Na pasta, pressione a &lt;barra de espaço> `<Tab>` teclas de seta ou no teclado para selecionar o ativo.

1. Pressione `<Enter>` para que você possa abrir o ativo selecionado no modo Visualização.

1. Siga um destes procedimentos:

   * Para ampliar, pressione `<Tab>` para mover o foco para o ícone de zoom de aproximação (+), pressione `<Enter>` uma ou mais vezes para ampliar de forma incremental.
   * Para reduzir, pressione `<Tab>` para mover o foco para o ícone de diminuição de zoom (-), pressione `<Enter>` uma ou mais vezes para diminuir o zoom de forma incremental.
   * Para mover a exibição de um *ampliado* horizontalmente ou verticalmente, pressione as respectivas teclas de seta.
   * Pressione `<Shift>` + `<Tab>` para que você possa redefinir a exibição e colocar o foco de volta no ativo.
