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
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Previewing assets{#previewing-assets}

Você pode usar a opção Visualizar para ver como um ativo digital que você carregou é exibido quando exibido por um cliente em seu próprio navegador da Web. O visualizador incorporado e entre dispositivos padrão atribuído ao ativo é usado para a Visualização.

Um visualizador é uma coleção de várias configurações ou &quot;predefinições&quot;, como tamanho de exibição do visualizador, comportamento de zoom, esquemas de cores, bordas, fontes e assim por diante, que determinam como os usuários visualizam ativos de mídia avançada em suas telas de computadores e dispositivos móveis.

Além de usar o recurso de Visualização dedicado para vídeos, conjuntos de rotação e conjuntos de imagens, também é possível visualizar um ativo usando as predefinições do visualizador que você criou. Ou use predefinições de imagens para visualizar representações de imagens.

* [Aplicar predefinições de imagens](/help/assets/image-presets.md)
* [Aplicar predefinições do visualizador](/help/assets/viewer-presets.md)

>[!NOTE]
>
>Quando você está em uma página da Web (Sites) no AEM, não pode visualizar ativos no modo **Editar** . Você precisa ir para o modo **Visualizar** clicando em **Visualizar** no canto superior direito.

Para ativar ou desativar as predefinições do visualizador na interface do usuário, consulte [Gerenciamento de predefinições](/help/assets/managing-viewer-presets.md)do visualizador.

**Para visualizar ativos**

1. No **[!UICONTROL Adobe Experience Manager**, na página **[!UICONTROL Navigation** , toque em **[!UICONTROL Ativos]** e, em seguida, em **[!UICONTROL Arquivos]** para acessar ativos.
1. Near the upper-right corner of the page, from the **[!UICONTROL View]** drop-down list, tap **[!UICONTROL List View]**.
1. (Opcional) Use a coluna **[!UICONTROL Tipo]** para classificar os ativos pelo tipo que deseja visualizar.
1. Na coluna **[!UICONTROL Título]** , clique no nome do título (não na imagem em miniatura) do ativo que deseja visualizar.
1. Dependendo do tipo de ativo clicado, execute um dos procedimentos a seguir:

   <table>
    <tbody>
      <tr>
      <td><strong>Tipo de ativo que você clicou</strong><br /> </td>
      <td><strong>Pode visualizar o ativo em uma representação específica?</strong></td>
      <td><strong>Pode visualizar o ativo em um visualizador específico?</strong></td>
      </tr>
      <tr>
      <td><p>Imagem</p> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar o ativo em uma representação específica</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
        </ul> <p><strong>Para visualizar o ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> <p>Use os <strong>ícones</strong> + <strong>e </strong>- para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em um dispositivo móvel, toque duas vezes na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Multimídia</td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar o ativo em uma representação específica</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Representações </strong>na lista e selecione uma representação específica que deseja visualizar.</li>
        </ul> <p>Selecionar uma execução de vídeo de resolução mais alta para visualização pode fazer com que o vídeo apareça truncado. Isso ocorre porque a visualização da execução mostra a resolução exata que seus clientes verão, tudo isso no contexto do visualizador incorporado usado para a visualização.</p> <p>Ao visualizar um conjunto de vídeo adaptável no nível do ativo, as renderizações são agrupadas em uma única experiência de reprodução. Ou seja, o vídeo adaptável é dimensionado corretamente para exibição e reprodução usando a melhor resolução no contexto do dispositivo de exibição e da velocidade da conexão.<br /> </p> <p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>Conjunto de imagens</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> <p>Use os <strong>ícones</strong> + <strong>e </strong>- para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em um dispositivo móvel, toque duas vezes na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de rotação</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> <p>Use os <strong>ícones</strong> + <strong>e </strong>- para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em um dispositivo móvel, toque duas vezes na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de mídia mista</td>
      <td>Não</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar um ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Clique em <strong>Visualizadores</strong> na lista e selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> <p>Use os <strong>ícones</strong> + <strong>e </strong>- para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em um dispositivo móvel, toque duas vezes na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
      <tr>
      <td>Conjunto de carrossel</td>
      <td>Não</td>
      <td>Sim</td>
      <td><strong>Para visualizar um ativo em um visualizador específico</strong>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, clique no ícone para que a lista suspensa seja exibida. Selecione um visualizador que você deseja aplicar ao ativo.</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360 Video<br /> </td>
      <td>Sim</td>
      <td>Sim</td>
      <td><p><strong>Para visualizar o ativo em uma representação específica</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Representações</strong>e selecione a representação que deseja visualizar.</li>
        </ul> <p><strong>Para visualizar o ativo em um visualizador específico</strong></p>
        <ul>
        <li>Próximo ao canto superior esquerdo da página, toque no ícone para que a lista suspensa seja exibida. Selecione <strong>Visualizadores</strong>e, em seguida, selecione um visualizador que deseja aplicar ao ativo.</li>
        </ul> <p>Use os <strong>ícones</strong> + <strong>e </strong>- para aumentar ou diminuir o zoom da imagem selecionada, respectivamente. Clique em <strong>Redefinir</strong> para retornar a imagem ao zoom original.<br /> Se você estiver em um dispositivo móvel, toque duas vezes na imagem para ampliar pelas etapas. Quando você atingir o zoom máximo, toque duas vezes na imagem novamente para redefinir o estado de zoom. Arraste pela imagem para deslocar.</p> </td>
      </tr>
    </tbody>
    </table>
