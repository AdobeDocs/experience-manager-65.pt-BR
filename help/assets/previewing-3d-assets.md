---
title: Pré-visualizar ativos 3D
description: Saiba como visualizar ativos 3D no Experience Manager.
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: User
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
hide: true
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 8%

---

# Pré-visualizar ativos 3D no Adobe Experience Manager {#previewing-3d-assets-aem}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/previewing-3d-assets.html?lang=en) |
| AEM 6.5 | Este artigo |

O Experience Manager é compatível com upload, entrega e pré-visualização interativa de ativos 3D como parte do processo de criação.

O visualizador 3D interativo está disponível na página de detalhes do ativo no Experience Manager. O visualizador inclui, entre outras coisas, uma coleção de controles de câmera interativos que permitem girar, aplicar zoom e deslocar o ativo 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos compatíveis com a visualização 3D no Experience Manager {#supported-3d-previewing-assets}

A visualização 3D interativa é compatível com os seguintes formatos de arquivo:

| Extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão GL Binária | model/gltf-binary | |
| GLTF | Formato de Transmissão GL | model/gltf+json | Consulte **Nota** abaixo. |
| OBJ | Arquivo de objeto 3D do WaveFront | application/x-tgif | |
| STL | Estereolitografia | application/vnd.ms-pki.stl | |
| DN | Adobe Dimension | model/x-adobe-dn | Suporte somente para assimilação; visualização não disponível. |
| USDZ | Arquivo Zip de Descrição de Cena Universal | model/vnd.usdz+zip | Suporte somente para assimilação; visualização não disponível. |

>[!NOTE]
>
>Se os materiais não renderizam na pré-visualização de um modelo gLTF, certifique-se de que sejam nomeados corretamente e em uma `textures` pasta na mesma pasta raiz do modelo, semelhante ao seguinte:

    Ativo (pasta)
    model.gltf
    model.bin
    texturas (pasta)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considerações de desempenho ao pré-visualizar ativos 3D no Experience Manager{#performance-3d-previewing-assets}

O tempo necessário para abrir um ativo 3D na página de visualização de detalhes do ativo depende de vários fatores, como largura de banda, complexidade da imagem e latências para o servidor.

Além disso, os recursos do computador cliente - como estação de trabalho, notebook ou dispositivo de toque móvel - também são importantes ao manipular a câmera interativamente. Um sistema razoavelmente eficiente com boas capacidades gráficas pode tornar a experiência de visualização 3D interativa mais suave e favorável.

**Para visualizar ativos 3D no Experience Manager:**

1. Verifique se você carregou ativos 3D no Experience Manager.
Consulte [Formatos compatíveis com a visualização 3D](#supported-3d-previewing-assets) e [Fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).
1. Do Experience Manager, no **[!UICONTROL Navegação]** selecione **[!UICONTROL Assets]** > **[!UICONTROL Arquivos]**.

   ![Página de navegação](/help/assets/assets-dm/navigation-assets.png)

1. Próximo ao canto superior direito da página, na lista suspensa Exibir, selecione **[!UICONTROL Exibição de cartão]**, em seguida, navegue até um ativo 3D que deseja visualizar.

   ![Seleção de cartão 3D](/help/assets/assets-dm/3d-card-select.png)
   _Na Exibição de cartão, selecione o cartão do ativo 3D que deseja visualizar._

1. Selecione o cartão do ativo 3D.

   ![Visualização interativa em 3D](/help/assets/assets-dm/3d-preview.png)
   _Visualização interativa de um ativo 3D na página de exibição de detalhes do ativo._
1. Na página da exibição Detalhes do ativo do ativo 3D, siga um destes procedimentos:

   | Exibir | Descrição | Ação do mouse | Ação da tela de toque |
   | --- | --- | --- | --- |
   | **Girar a câmera** | Gire a visualização em torno da cena 3D e dos objetos. | Clique com o botão esquerdo + arraste. | Pressione com um dedo + arraste. |
   | **Deslocar a câmera** | Desloque sua exibição para a esquerda, direita, para cima ou para baixo. | Clique com o botão direito do mouse e arraste. | Pressione com dois dedos + arraste. |
   | **Aplicar zoom à sua câmera** | Mova para dentro e para fora das áreas na cena 3D. | Roda de rolagem. | Pinça de dois dedos. |
   | **Recentralize sua câmera** | Recentralize sua câmera em um ponto sobre um objeto na cena 3D. | Clique duas vezes em. | Toque duas vezes. |
   | **Redefinir** | Próximo ao canto inferior direito da página, selecione o ícone Redefinir para restaurar o ponto de destino de exibição para o centro do ativo 3D. A redefinição também move a câmera para mais perto ou mais longe, para mostrar o ativo em sua totalidade e em um tamanho de visualização razoável. |   |   |
   | **Modo de tela cheia** | Para entrar no modo de tela cheia, no canto inferior direito da página, selecione o ícone Tela cheia. |   |   |

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Fechar]**.
