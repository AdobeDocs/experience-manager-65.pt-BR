---
title: Vídeo
seo-title: Vídeo
description: Diretamente no Assets, com o gerenciamento centralizado de ativos de vídeo, é possível fazer upload de vídeos para codificar para o Scene7 e acessar vídeos do Scene7, para fins de criação de página.
seo-description: Diretamente no Assets, com o gerenciamento centralizado de ativos de vídeo, é possível fazer upload de vídeos para codificar para o Scene7 e acessar vídeos do Scene7, para fins de criação de página.
uuid: 46da7a0d-d17b-4716-a304-ce5496421b5a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: df89d5cfd5060d493babb89e92a9a98e851b8879
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 42%

---


# Vídeo{#video}

Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os Ativos para autocodificação para o Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente dos Ativos para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas (detecção automática de dispositivo e largura de banda).

* O componente de vídeo do Dynamic Media Classic (Scene7) executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato correto e o vídeo de qualidade correta em desktops, tablets e dispositivos móveis.
* Assets: é possível incluir conjuntos de vídeos adaptáveis, em vez de somente ativos de vídeo individuais. Um conjunto de vídeos adaptáveis é um contêiner para todas as representações de vídeo necessárias para reproduzir o vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo que são codificadas em diferentes taxas de bits e formatos, como 400 kbps, 800 kbps e 1000 kbps. Você usa um conjunto de vídeos adaptáveis, juntamente com o componente de vídeo do S7, para transmitir vídeo adaptável em vários tipos de telas, incluindo telas de computadores, e dispositivos móveis com iOS, Android, Blackberry e Windows. Consulte a [documentação do Scene7 sobre conjuntos de vídeos adaptáveis](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html) para obter mais informações.

## Sobre o FFMPEG e o Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão se baseia no uso da integração em FFMPEG com perfis de vídeo. Therefore, the out-of-the-box [!UICONTROL DAM Update Asset] workflow contains the following two ffmpeg-based workflow steps:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Be aware that enabling and configuring the Dynamic Media Classic integration does not automatically remove or deactivate these two workflow steps from the out-of-the-box [!UICONTROL DAM Update Asset] ingestion workflow. Se você já usa a codificação de vídeo baseada em FFMPEG no AEM, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando Ativos seria codificado duas vezes: uma vez do codificador FFMPEG e uma vez da integração com o Dynamic Media Classic.

If you have the FFMPEG-based video encoding in AEM configured and FFMPEG installed, Adobe recommends that you remove the two FFMPEG workflows from your [!UICONTROL DAM Update Asset] workflows.

### Formatos suportados {#supported-formats}

Os formatos a seguir são suportados pelo componente Vídeo clássico do Dynamic Media:

* F4V H.264
* MP4 H.264

### Como decidir onde fazer upload de seu vídeo {#deciding-where-to-upload-your-video}

Para decidir onde fazer upload de seus ativos de vídeo, considere o seguinte:

* O ativo de vídeo requer um fluxo de trabalho?
* O ativo de vídeo requer controle de versão?

Se a resposta for “sim” para ambas as perguntas, faça upload do vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; para ambas as perguntas, faça upload do vídeo diretamente para o Dynamic Media Classic. O fluxo de trabalho referente a cada cenário é descrito na próxima seção.

#### Se estiver fazendo upload do vídeo diretamente no Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se for necessário um fluxo de trabalho ou controle de versão para seus ativos, você deverá fazer upload primeiro no Adobe Assets. Este é o fluxo de trabalho recomendado:

1. Faça upload do ativo de vídeo para o Adobe Assets e codifique e publique automaticamente no Dynamic Media Classic.
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Autor com vídeo do Dynamic Media Classic ou componente de vídeo de base.

#### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se você não precisar de um fluxo de trabalho ou controle de versão para seus ativos, faça upload dos ativos para o Dynamic Media Classic. Este é o fluxo de trabalho recomendado:

1. No Dynamic Media Classic, [configure um carregamento e codificação FTP programados para o Dynamic Media Classic (sistema automatizado)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. In AEM, access video assets in WCM in the **[!UICONTROL Dynamic Media Classic]** tab of the Content Finder.
1. Autor com o componente de vídeo do Dynamic Media Classic.

### Configuração da integração com o Dynamic Media Classic Video {#configuring-integration-with-scene-video}

**Para configurar predefinições universais**:

1. In **[!UICONTROL Cloud Services]**, navigate to your **[!UICONTROL Dynamic Media Classic]** configuration and click **[!UICONTROL Edit]**.
1. Selecione a guia **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não possuir uma configuração de nuvem. Consulte [Ativação do Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >For more information about what the video presets mean, see the [Dynamic Media Classic documentation](https://help.adobe.com/en_US/scene7/using/WSE86ACF2B-BD50-4c48-A1D7-9CD4405B62D0.html).
   >
   >A Adobe recomenda selecionar ambos os conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecionar a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta do público alvo CQ DAM que você configurou para esta configuração de nuvem do Dynamic Media Classic. Você pode configurar várias configurações de nuvem do Dynamic Media Classic com diferentes pastas de público alvo para aplicar diferentes perfis de codificação, conforme necessário.

### Atualizar as predefinições de codificação e do visualizador {#updating-viewer-and-encoding-presets}

If you need to update the viewer and encoding presets for video in AEM because the presets have been updated in Dynamic Media Classic, navigate to the Dynamic Media Classic configuration in the cloud configuration and click **Update the viewer and encoding presets**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Fazer upload do vídeo de origem primária {#uploading-your-master-video}

Para carregar seu vídeo de origem principal no Dynamic Media Classic a partir do Adobe DAM:

1. Navegue até a pasta do público alvo CQ DAM na qual você configurou a configuração da nuvem com perfis de codificação do Dynamic Media Classic.
1. Clique em **[!UICONTROL Carregar]** para carregar o vídeo de origem primária. Video uploading and encoding is complete after the [!UICONTROL DAM Update Asset] workflow is complete and **[!UICONTROL Publish to Dynamic Media Classic]** has a checkmark.

   >[!NOTE]
   >
   >Pode levar algum tempo para gerar as miniaturas de vídeo.

   Dragging the DAM primary source video on to the video component accesses *all* of the Dynamic Media Classic encoded proxy renditions for delivery.

### Componente de vídeo básico versus Componente de vídeo clássico do Dynamic Media {#foundation-video-component-versus-scene-video-component}

Ao usar o AEM, você tem acesso ao componente Vídeo disponível no Sites e ao componente de vídeo do Dynamic Media Classic (Scene7). Esses componentes não são intercambiáveis.

O componente de vídeo do Dynamic Media Classic só funciona para vídeos do Dynamic Media Classic. O componente básico funciona com vídeos armazenados do AEM (usando o ffmpeg) e vídeos do Dynamic Media Classic.

A seguinte matriz explica quando você deve usar cada componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>O componente de vídeo do Dynamic Media Classic usa o perfil de vídeo universal. No entanto, você pode obter o player de vídeo baseado em HTML5 para uso pelo AEM. No Dynamic Media Classic, copie o código incorporado do player de vídeo HTML5 e coloque-o na página do AEM.


## Componente de vídeo do AEM {#aem-video-component}

Mesmo se o componente de vídeo do Dynamic Media Classic for recomendado para exibir vídeos do Dynamic Media Classic, esta seção descreve o uso de vídeos do Dynamic Media Classic com o componente [!UICONTROL de vídeo da] base no AEM, para fins de integridade.

### Comparação entre vídeo AEM e vídeo clássico do Dynamic Media {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação avançada dos recursos suportados entre o Componente de vídeo de base do AEM e o Componente de vídeo do Scene7:

|  | Vídeo de base do AEM | Vídeo Dynamic Media Classic |
|---|---|---|
| Abordagem | Abordagem de HTML5 primeiro. O Flash é usado somente para o fallback não-HTML5. | Flash na maioria dos computadores. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressiva | Transmissão adaptável |
| Acompanhamento | Sim | Sim |
| Extensibilidade | Sim | Sim (com o SDK do visualizador do Dynamic Media Classic) |
| Vídeo móvel | Sim | Sim |

### Configuração {#setting-up}

#### Criação de perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do Dynamic Media Classic selecionadas na configuração da nuvem do Dynamic Media Classic. Para que o componente de vídeo de base os utilize, é necessário criar um perfil de vídeo para cada predefinição de codificação do Dynamic Media Classic selecionada. Isso permite que o componente de vídeo selecione as execuções de DAM apropriadas.

>[!NOTE]
>
>Os novos perfis de vídeo e as alterações a eles devem ser ativados para publicação.

1. No AEM, acesse as **[!UICONTROL Ferramentas]** e selecione o **[!UICONTROL Console de configuração]**. In the Configuration Console navigate to **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Video Profiles]** in the navigation tree.
1. Crie um novo Perfil Dynamic Media Classic Video. In the **[!UICONTROL New...]** menu, select **[!UICONTROL Create Page]** and then select the Dynamic Media Classic Video Profile template. Forneça um nome para a nova página de perfil de vídeo e clique em **[!UICONTROL Criar]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite o novo perfil de vídeo. Selecione primeiro a configuração de nuvem. Em seguida, selecione a mesma predefinição de codificação selecionada na configuração de nuvem.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriedade | Descrição |
   |---|---|
   | Configuração da nuvem do Dynamic Media Classic (Scene7) | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Dynamic Media Classic (Scene7) | A predefinição de codificação para mapear este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite definir o valor da propriedade type do elemento de fonte de vídeo HTML5. Essas informações não são fornecidas pelas predefinições de codificação do Dynamic Media Classic, mas são necessárias para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas eles podem ser substituídos por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração de nuvem que você deseja usar no componente de vídeo.

#### Configuração do design {#configuring-design}

O componente de vídeo de base deve saber quais perfis de vídeo usar para que possa construir a lista de origens de vídeo. É preciso abrir a caixa de diálogo dos componentes de vídeo e configurar o design dos componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usa o componente de vídeo de base em uma página para dispositivos móveis, talvez seja necessário repetir essas etapas no design da página móvel.

>[!NOTE]
>
>As alterações feitas no design exigem que ele seja aplicado para serem aplicadas na publicação.

1. Abra a caixa de diálogo de design do componente de vídeo de base e altere para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis predefinidos e adicione os novos perfis de vídeo do Dynamic Media Classic. A ordem da lista do perfil na caixa de diálogo de design também define a ordem do elemento de fontes de vídeo ao renderizar.
1. Para os navegadores que não oferecem suporte ao HTML5, o componente de vídeo permite configurar um fallback de flash. Abra a caixa de diálogo de design dos componentes de vídeo e altere para a guia **[!UICONTROL Flash]**. Ajuste as configurações do flash player e atribua um perfil de fallback a ele.

#### Lista de verificação {#checklist}

1. Crie uma configuração de nuvem do Dynamic Media Classic (Scene7). Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do Dynamic Media Classic para cada predefinição de codificação de vídeo selecionada na configuração da nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente de vídeo de base na sua página.
1. Ative o design após finalizar as alterações no design.

