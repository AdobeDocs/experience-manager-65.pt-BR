---
title: Pré-visualização de ativos 3D
description: Saiba como visualizar ativos 3D
contentOwner: Rick Brough
docset: aem65
feature: 3D Assets
role: Business Practitioner
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 16%

---


# Visualização de ativos 3D no AEM{#previewing-3d-assets-aem}

O Adobe Experience Manager oferece suporte para upload, delivery e visualização interativa de ativos 3D como parte do processo de criação.

O visualizador 3D interativo está disponível na página de detalhes do ativo no AEM. O visualizador inclui, entre outras coisas, uma coleção de controles de câmera interativos que permitem girar, aplicar zoom e deslocar o ativo 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formatos compatíveis com a visualização 3D em AEM {#supported-3d-previewing-assets}

A visualização 3D interativa é compatível com os seguintes formatos de arquivo:

| extensão de arquivo 3D | Formato de arquivo | Tipo MIME | Notas |
|---|---|---|---|
| GLB | Transmissão binária GL | model/gltf-binário |  |
| GLTF | Formato de transmissão GL | model/gltf+json | Consulte **Observação** abaixo. |
| OBJ | Arquivo de objeto 3D WaveFront | application/x-tgif |  |
| STL | Estereolitografia | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Suporte apenas para ingestão; visualização não disponível. |
| USDZ | Arquivo Zip de descrição da cena universal | model/vnd.usdz+zip | Suporte apenas para ingestão; visualização não disponível. |

**Observação**: Se os materiais não forem renderizados na pré-visualização de um modelo GLTF, verifique se eles estão nomeados corretamente e localizados em uma  `textures` pasta na mesma pasta raiz do modelo, semelhante ao seguinte:

    Ativo (pasta)
    model.
    gltfmodel.
    bintextures (pasta)
    material_0_baseColor.
    jpegmaterial_0_normal.jpeg

## Considerações de desempenho ao visualizar ativos 3D no AEM{#performance-3d-previewing-assets}

O tempo necessário para abrir um ativo 3D na página de visualização de detalhes do ativo depende de vários fatores, como largura de banda, complexidade da imagem e latências para o servidor.

Além disso, os recursos do computador cliente, como uma estação de trabalho, um notebook ou um dispositivo de toque móvel, também são importantes a ser considerados ao manipular a câmera interativamente. Um sistema bastante eficiente com bons recursos gráficos pode tornar a experiência de visualização interativa em 3D mais fácil e favorável.

**Visualização de ativos 3D no AEM**

1. Verifique se você fez upload dos ativos 3D no AEM.
Consulte [Formatos compatíveis com a visualização 3D](#supported-3d-previewing-assets) e [Fazer upload de ativos](/help/assets/manage-assets.md#uploading-assets).
1. Em AEM, na página **[!UICONTROL Navegação]**, toque em **[!UICONTROL Ativos > Arquivos.]**

   ![Página de navegação](/help/assets/assets-dm/navigation-assets.png)

1. Próximo ao canto superior direito da página, na lista suspensa Exibição, toque em **[!UICONTROL Exibição de cartão]** e navegue até um ativo 3D que deseja visualizar.

   ![Seleção de cartão 3D](/help/assets/assets-dm/3d-card-select.png)
   _Na Exibição de cartão, toque no cartão do ativo 3D que deseja visualizar._

1. Toque no cartão do ativo 3D para abri-lo na página de exibição de detalhes do ativo.

   ![Visualização 3D interativa](/help/assets/assets-dm/3d-preview.png)
   _Visualização interativa de um ativo 3D na página de visualização de detalhes do ativo._
1. Na página de exibição de detalhes do ativo para o ativo 3D, siga um destes procedimentos:
   * **Vire sua câmera**—Órbita sua exibição ao redor da cena e dos objetos 3D.
      * _Rato_: Clique com o botão esquerdo e arraste.
      * _Tela_ sensível ao toque: Pressione com um único dedo e arraste.
   * **Deslocar sua câmera** - Deslocar sua exibição para a esquerda, para a direita, para cima ou para baixo.
      * _Rato_: Clique com o botão direito + arraste.
      * _Tela_ sensível ao toque: Pressione com dois dedos e arraste.
   * **Ampliação da câmera** - Amplie a câmera para mover-se de áreas da cena 3D.
      * _Rato_: Roda de rolagem.
      * _Tela_ sensível ao toque: Um beliscão de dois dedos.
   * **Recenter sua câmera** — Insira novamente sua câmera em um ponto de um objeto na cena 3D.
      * _Rato_: Clique duas vezes.
      * _Tela_ sensível ao toque: Toque duas vezes.
   * **Redefinir** — Próximo ao canto inferior direito da página, toque no ícone Redefinir para restaurar o ponto de destino da exibição para o centro do ativo 3D. A redefinição também aproxima ou afasta a câmera para mostrar o ativo inteiro e com um tamanho de visualização razoável.
   * **Modo** de tela cheia—Para entrar no modo de tela cheia, no canto inferior direito da página, toque no ícone Tela cheia.

1. Quando terminar, próximo ao canto superior direito da página, toque em **[!UICONTROL Fechar.]**
