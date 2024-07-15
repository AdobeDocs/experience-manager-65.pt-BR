---
title: Visualizar ativos
description: Saiba como visualizar ativos, como vídeos e imagens, no Dynamic Media aplicando predefinições de imagens e predefinições do visualizador.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
feature: Asset Management
role: User, Admin
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1381'
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
>Quando você está em uma página da Web (Sites) no Adobe Experience Manager, não pode visualizar ativos no modo **Editar**. Vá para o modo de Visualização clicando em **[!UICONTROL Visualizar]** no canto superior direito da página.

Para habilitar ou desabilitar predefinições do visualizador na interface do usuário, consulte [Gerenciar Predefinições do Visualizador](/help/assets/managing-viewer-presets.md).

**Para visualizar ativos usando a interface de software:**

1. No **[!UICONTROL Adobe Experience Manager]**, na página **[!UICONTROL Navegação]**, selecione **[!UICONTROL Assets]** e depois **[!UICONTROL Arquivos]** para acessar os ativos.
1. Próximo ao canto superior direito da página, na lista suspensa **[!UICONTROL Exibição]**, selecione **[!UICONTROL Exibição de Lista]**.
1. (Opcional) Use a coluna **[!UICONTROL Tipo]** para classificar os ativos pelo tipo que deseja visualizar.
1. Na coluna **[!UICONTROL Título]**, clique no nome do título (não na imagem em miniatura) do ativo que deseja visualizar.
1. Dependendo do tipo de ativo em que você clicou, execute um dos procedimentos a seguir:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de ativo clicado</strong><br /> </td>
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
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione o visualizador Dimensional.</li>
      <li>Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.</li>
      <li>Selecione <strong>Tela cheia</strong> para maximizar o visualizador no dispositivo de exibição.</li>
      </ul>
      <p><strong>Navegar pela cena 3D</strong></p>
      <ul>
      <li><p><strong>Gire sua câmera 3D</strong> - Gire a exibição em torno da cena 3D e dos objetos.</p> Mouse: Clique com o botão esquerdo + arraste </p> Tela sensível ao toque: pressione + arraste</p></li>
      <li><p><strong>Deslocar sua câmera</strong> - Deslocar sua exibição para a esquerda, direita, para cima e para baixo.</p> Mouse: clique com o botão direito do mouse + arraste </p> Tela sensível ao toque: pressione dois dedos + arraste</p></li>
      <li><p><strong>Aplicar zoom à sua câmera</strong> - Aplicar zoom à sua câmera para que você possa mover para dentro e para fora das áreas na cena 3D.</p> Mouse: roda de rolagem </p> Tela sensível ao toque: pinça no dedo</p></li>
      <li><p><strong>Recentralize sua câmera</strong> - Gire a exibição em torno da cena 3D e de objetos.</p> Mouse: clique duas vezes </p> Tela sensível ao toque: seleção dupla</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagem</p> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, selecione duas vezes a imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, selecione novamente a imagem para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Multimídia</td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p>Selecionar uma representação de vídeo de resolução mais alta para visualizar pode fazer com que o vídeo apareça truncado. Esse problema ocorre porque a pré-visualização de representação mostra a resolução exata que seus clientes verão tudo no contexto do visualizador incorporado usado para a pré-visualização.</p> <p>Ao visualizar um conjunto de vídeos adaptáveis no nível do Ativo, as representações são agrupadas em uma experiência de reprodução. Ou seja, o vídeo adaptável é dimensionado corretamente para exibição e reprodução usando a melhor resolução no contexto do dispositivo de exibição e da velocidade da conexão.<br /> </p> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imagens</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, selecione duas vezes a imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, selecione novamente a imagem para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Grupo de rotação</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, selecione duas vezes a imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, selecione novamente a imagem para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de mix de mídia</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, selecione duas vezes a imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, selecione novamente a imagem para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
      <tr>
      <td>Conjunto do Carousel</td>
      <td>Não</td>
      <td>Sim</td>
      <td><strong>Para visualizar um ativo em um determinado visualizador</strong>
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
      <li>Próximo ao canto superior esquerdo da página, selecione o ícone para que a lista suspensa seja exibida. Selecione <strong>Representações</strong> e selecione a representação que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, selecione o ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> e, em seguida, selecione um visualizador que você deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Selecione <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, selecione duas vezes a imagem para aproximar o zoom por etapas. Ao atingir o zoom máximo, selecione novamente a imagem para redefinir o estado de zoom. Arraste pela imagem para deslocar-se.</p> </td>
      </tr>
    </tbody>
    </table>

## Visualizar ativos usando um teclado {#keyboard-navigation-asset-preview}

1. Na interface do usuário do Assets, navegue até uma pasta que contenha um ativo que você deseja visualizar.

1. Na pasta, pressione a tecla ou as teclas de seta `<Tab>` no teclado para selecionar o ativo.

1. Pressione `<Enter>` para abrir o ativo selecionado no modo de Visualização.

1. Siga um destes procedimentos:

   * Para ampliar, pressione `<Tab>` para mover o foco para o ícone de aumento (+) e pressione `<Enter>` uma ou mais vezes para aumentar o zoom.
   * Para reduzir, pressione `<Tab>` para mover o foco para o ícone de menos zoom (-) e pressione `<Enter>` uma ou mais vezes para diminuir o zoom incrementalmente.
   * Para mover a exibição de um ativo *com zoom* horizontal ou verticalmente, pressione as respectivas teclas de seta.
   * Pressione `<Shift>` + `<Tab>` para redefinir o modo de exibição e colocar o foco de volta no ativo.
