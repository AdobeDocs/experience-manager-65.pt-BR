---
title: Visualizar ativos
description: Saiba como visualizar ativos no Dynamic Media
uuid: 09e97245-373b-4d50-8ba3-5d1034a29988
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: bb8c355c-4475-45ec-9096-0975f0ce2c27
docset: aem65
feature: Gerenciamento de ativos
role: Business Practitioner, Administrator
exl-id: 84f0c406-4ab6-48c7-8223-61a8c3ade363
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1346'
ht-degree: 3%

---

# Visualização de ativos usando a interface de software {#previewing-assets}

Você pode usar a Visualização para ver como um ativo digital que você carregou é exibido por um cliente em seu próprio navegador da Web. O visualizador padrão incorporado entre dispositivos atribuído ao ativo é usado para a Visualização.

Um visualizador é uma coleção de várias configurações ou &quot;predefinições&quot;, como o tamanho de exibição do visualizador, comportamento de zoom, esquemas de cores, bordas, fontes e assim por diante, que determinam como os usuários visualizam ativos de mídia avançada em suas telas de computadores e dispositivos móveis.

Além de usar o recurso de Visualização dedicado para vídeos, conjuntos de rotação e conjuntos de imagens, você também pode visualizar um ativo usando predefinições do visualizador que você criou. Ou use predefinições de imagens para visualizar representações de imagens.

* [Aplicação de predefinições da imagem](/help/assets/image-presets.md)
* [Aplicação de predefinições do visualizador](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando você está em uma página da Web (Sites) no AEM, não pode visualizar ativos no modo **Editar**. Você precisa acessar o modo **Preview** clicando em **Preview** no canto superior direito da página.

Para ativar ou desativar as predefinições do visualizador na interface do usuário, consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md).

**Visualização de ativos usando a interface de software**

1. Em **[!UICONTROL Adobe Experience Manager]**, na página **[!UICONTROL Navegação]**, toque em **[!UICONTROL Ativos]** e em **[!UICONTROL Arquivos]** para acessar os ativos.
1. Próximo ao canto superior direito da página, na lista suspensa **[!UICONTROL View]**, toque em **[!UICONTROL List View]**.
1. (Opcional) Use a coluna **[!UICONTROL Type]** para classificar os ativos pelo tipo que deseja visualizar.
1. Na coluna **[!UICONTROL Título]**, clique no nome do título (não na imagem em miniatura) do ativo que deseja visualizar.
1. Dependendo do tipo de ativo que você clicou, siga um destes procedimentos:


   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de ativo que você clicou</strong><br /> </td>
      <td><strong>Pode visualizar o ativo em uma representação específica?</strong></td>
      <td><strong>É possível visualizar o ativo em um visualizador?</strong></td>
      <td> </td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Visualização de um ativo 3D no visualizador Dimensional</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione o visualizador Dimensional.</li>
      <li>Toque em <strong>Redefinir</strong> para retornar a imagem ao zoom original.</li>
      <li>Toque em <strong>Tela cheia</strong> para maximizar o visualizador no dispositivo de exibição.</li>
      </ul>
      <p><strong>Navegar pela cena 3D</strong></p>
      <ul>
      <li><p><strong>Rode sua câmera</strong>  3D - Órbita sua exibição ao redor da cena e dos objetos 3D.</p> Rato: Clique com o botão esquerdo do mouse + Arraste. </p> Tela sensível ao toque: Pressione + Arraste.</p></li>
      <li><p><strong>Deslocar sua câmera</strong>  - Desloque sua exibição para a esquerda, para a direita, para cima e para baixo.</p> Rato: Clique com o botão direito + arraste. </p> Tela sensível ao toque: Pressione com dois dedos + Arraste.</p></li>
      <li><p><strong>Zoom da câmera</strong>  - Zoom da câmera para mover para dentro e para fora de áreas da cena 3D.</p> Rato: Roda de rolagem. </p> Tela sensível ao toque: Aperte o dedo.</p></li>
      <li><p><strong>Recenter sua câmera</strong>  - Órbita sua visualização em torno da cena 3D e dos objetos.</p> Rato: Clique duas vezes. </p> Tela sensível ao toque: Toque duas vezes.</li></ul></td>
      </tr>
      <tr>
      <td><p>Imagem</p> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar o ativo em um visualizador específico</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Reset</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque duas vezes na imagem para ampliar pelas etapas. Quando atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado do zoom. Arraste a imagem para o panorama.</p> </td>
      </tr>
      <tr>
      <td>Multimídia</td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
      </ul> <p>Selecionar uma representação de vídeo de resolução mais alta para visualização pode fazer com que o vídeo apareça truncado. Isso ocorre porque a visualização da representação mostra a resolução exata que seus clientes a verão, tudo no contexto do visualizador incorporado usado para a visualização.</p> <p>Ao visualizar um conjunto de vídeos adaptáveis no nível do Ativo, as representações são agrupadas em uma experiência de reprodução. Ou seja, o vídeo adaptável é dimensionado corretamente para exibição e reprodução usando a melhor resolução no contexto do dispositivo de exibição e velocidade de conexão.<br /> </p> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imagens</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Reset</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque duas vezes na imagem para ampliar pelas etapas. Quando atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado do zoom. Arraste a imagem para o panorama.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de rotação</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Reset</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque duas vezes na imagem para ampliar pelas etapas. Quando atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado do zoom. Arraste a imagem para o panorama.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de mídias mistas</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Reset</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque duas vezes na imagem para ampliar pelas etapas. Quando atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado do zoom. Arraste a imagem para o panorama.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carrossel</td>
      <td>Não</td>
      <td>Sim</td>
      <td><strong>Para visualizar um ativo em um visualizador específico</strong>
      <ul>
      <li>Ao lado do canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> </td>
      </tr>
      <tr>
      <td>Vídeo 360<br /> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Visualização de ativos em uma representação específica</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Representações</strong> e selecione a representação que deseja visualizar.</li>
      </ul> <p><strong>Para visualizar o ativo em um visualizador específico</strong></p>
      <ul>
      <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong> e selecione um visualizador que deseja aplicar ao ativo.</li>
      </ul> <p>Use os ícones <strong>+</strong> e <strong>-</strong> para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Reset</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em uma tela sensível ao toque, toque duas vezes na imagem para ampliar pelas etapas. Quando atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado do zoom. Arraste a imagem para o panorama.</p> </td>
      </tr>
    </tbody>
    </table>

## Visualização de ativos usando um teclado {#keyboard-navigation-asset-preview}

1. Na interface do usuário do Assets, navegue até uma pasta que contenha um ativo que deseja visualizar.

1. Na pasta , pressione a tecla `<Tab>` ou as teclas de seta no teclado para selecionar o ativo.

1. Pressione `<Enter>` para abrir o ativo selecionado no modo de visualização.

1. Siga um destes procedimentos:

   * Para ampliar, pressione `<Tab>` para mover o foco para o ícone de zoom (+) e pressione `<Enter>` uma ou mais vezes para ampliar de forma incremental.

   * Para diminuir o zoom, pressione `<Tab>` para mover o foco para o ícone de saída de zoom (-) e pressione `<Enter>` uma ou mais vezes para diminuir o zoom de forma incremental.

   * Para mover a exibição de um ativo com *zoom* horizontalmente ou verticalmente, pressione as respectivas teclas de seta.

   * Pressione `<Shift>` + `<Tab>` para redefinir a exibição e colocar o foco de volta no ativo.
