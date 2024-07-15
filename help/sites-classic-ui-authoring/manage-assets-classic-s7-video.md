---
title: Criação de vídeos no Sites Classic
description: O Assets fornece um gerenciamento centralizado de ativos de vídeo, em que você pode fazer upload de vídeos diretamente no Assets para codificação automática no Dynamic Media Classic e acessar vídeos diários diretamente do Assets para criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: c540aa49-9981-4e8c-97df-972085b26490
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 1%

---

# Vídeo{#video}

O Assets fornece um gerenciamento centralizado de ativos de vídeo, em que você pode fazer upload de vídeos diretamente no Assets para codificação automática no Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente do Assets para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado a todas as telas (detecção automática de dispositivo e largura de banda).

* O componente de vídeo do Dynamic Media Classic executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato e o vídeo com a qualidade ideais em desktops, tablets e dispositivos móveis.
* Assets - É possível incluir conjuntos de vídeos adaptáveis em vez de apenas ativos de vídeo únicos. Um conjunto de vídeos adaptáveis é um container para todas as representações de vídeo necessárias para reproduzir vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptados agrupa versões do mesmo vídeo codificadas em taxas de bits e formatos diferentes, como 400 kbps, 800 kbps e 1000 kbps. Use um Conjunto de vídeos adaptados, juntamente com o componente de vídeo S7, para transmissão de vídeo adaptado em várias telas, incluindo dispositivos móveis para desktop, iOS, Android™, BlackBerry® e Windows. Consulte a [documentação do Dynamic Media Classic sobre conjuntos de vídeos adaptáveis para obter mais informações](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Sobre FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão é baseado no uso da integração baseada em FFMPEG com perfis de vídeo. Portanto, o fluxo de trabalho pronto para uso [!UICONTROL Ativo de atualização do DAM] contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Habilitar e configurar a integração do Dynamic Media Classic não remove nem desativa automaticamente essas duas etapas do fluxo de trabalho do fluxo de trabalho de assimilação pronto para uso do [!UICONTROL Ativo de atualização do DAM]. Se você já usa a codificação de vídeo baseada em FFMPEG no Adobe Experience Manager, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando o Experience Manager Assets é codificado duas vezes: uma vez do codificador FFMPEG e outra da integração do Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG no Experience Manager configurada e o FFMPEG instalado, o Adobe recomenda remover os dois fluxos de trabalho FFMPEG dos fluxos de trabalho do [!UICONTROL Ativo de atualização do DAM].

### Formatos compatíveis {#supported-formats}

Os seguintes formatos são compatíveis com o componente de Vídeo do Dynamic Media Classic:

* F4V H.264
* MP4 H.264

### Decida onde carregar seu vídeo {#deciding-where-to-upload-your-video}

A decisão sobre onde carregar seus ativos de vídeo depende do seguinte:

* Você precisa de um fluxo de trabalho para o ativo de vídeo?
* Você precisa do controle de versão para o ativo de vídeo?

Se a resposta for &quot;sim&quot; a uma ou ambas as perguntas, carregue o vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; às duas perguntas, carregue o vídeo diretamente no Dynamic Media Classic. O fluxo de trabalho para cada cenário é descrito na seção a seguir.

#### Se você estiver carregando o vídeo diretamente no Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se precisar de um fluxo de trabalho ou controle de versão para seus ativos, você deve fazer upload para o Adobe Assets primeiro. O fluxo de trabalho recomendado é o seguinte:

1. Faça upload do ativo de vídeo no Adobe Assets e codifique e publique automaticamente no Dynamic Media Classic.
1. No Experience Manager, acesse ativos de vídeo no WCM na guia **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Crie com o vídeo do Dynamic Media Classic ou o componente de vídeo da fundação.

#### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se não precisar de um fluxo de trabalho ou controle de versão para seus ativos, você deve fazer upload dos ativos para a Dynamic Media Classic. O fluxo de trabalho recomendado é o seguinte:

1. No aplicativo de desktop do Dynamic Media Classic, [configure um carregamento e uma codificação de FTP agendados para o Dynamic Media Classic (automatizado pelo sistema)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html?lang=pt-BR#upload-options).
1. No Experience Manager, acesse ativos de vídeo no WCM na guia **[!UICONTROL Dynamic Media Classic]** do Localizador de conteúdo.
1. Crie com o componente de vídeo do Dynamic Media Classic.

### Configurar integração com o Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. Em **[!UICONTROL Cloud Service]**, navegue até a configuração do **[!UICONTROL Dynamic Media Classic]** e selecione **[!UICONTROL Editar]**.
1. Selecione a guia **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não tiver uma configuração de nuvem. Consulte [Habilitar Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo único pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que significam predefinições de vídeo, consulte [Predefinições de vídeo para codificação de arquivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >A Adobe recomenda que você selecione os dois conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecione a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta de destino do CQ DAM que você configurou para esta configuração de nuvem do Dynamic Media Classic. É possível definir várias configurações de nuvem do Dynamic Media Classic com pastas de destino diferentes para aplicar perfis de codificação diferentes, conforme necessário.

### Atualização de predefinições do visualizador e de codificação {#updating-viewer-and-encoding-presets}

Atualize as predefinições do visualizador e de codificação para vídeo no Experience Manager se as predefinições tiverem sido atualizadas no Dynamic Media Classic. Nesse caso, navegue até a configuração do Dynamic Media Classic na configuração da nuvem e selecione **Atualizar as predefinições de visualizador e codificação**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Fazer upload do vídeo de origem principal {#uploading-your-master-video}

Para carregar o vídeo de origem principal no Dynamic Media Classic a partir do Adobe DAM:

1. Navegue até a pasta de destino do CQ DAM, na qual você definiu a configuração da nuvem com perfis de codificação do Dynamic Media Classic.
1. Selecione **[!UICONTROL Carregar]** para carregar o vídeo de origem primária. O carregamento e a codificação de vídeos estão concluídos após a conclusão do fluxo de trabalho do [!UICONTROL Ativo de atualização do DAM] e da marca de seleção do **[!UICONTROL Publish para Dynamic Media Classic]**.

   >[!NOTE]
   >
   >Pode levar algum tempo para que as miniaturas de vídeo sejam geradas.

   Ao arrastar o vídeo de origem primária DAM para o componente de vídeo, ele acessa *todas* as representações de proxy codificadas do Dynamic Media Classic para entrega.

### Componente de vídeo do Foundation versus componente de vídeo do Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Ao usar o Experience Manager, você tem acesso ao componente de Vídeo disponível no Sites e ao componente de Vídeo do Dynamic Media Classic. Esses componentes não são intercambiáveis.

O componente de vídeo do Dynamic Media Classic só funciona para vídeos do Dynamic Media Classic. O componente de base funciona com vídeos armazenados em Experience Manager (usando ffmpeg) e vídeos do Dynamic Media Classic.

A matriz a seguir explica quando você deve usar qual componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Pronto para uso, o componente de vídeo do Dynamic Media Classic usa o perfil de vídeo universal. Entretanto, é possível obter o reprodutor de vídeo baseado em HTML para uso pelo Experience Manager. No Dynamic Media Classic, copie o código incorporado do reprodutor de vídeo HTML5 pronto para uso e coloque-o na página Experience Manager.
>

## Componente de vídeo do Experience Manager {#aem-video-component}

Mesmo que o uso do componente de Vídeo do Dynamic Media Classic seja recomendado para visualizar vídeos do Dynamic Media Classic, esta seção descreve o uso de vídeos do Dynamic Media Classic com o [!UICONTROL Componente de Vídeo de Base] no Experience Manager para integridade.

### Comparação entre Experience Manager Video e Dynamic Media Classic Video {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação de alto nível de recursos compatíveis entre o componente de Vídeo de base do Experience Manager e o componente de Vídeo do Dynamic Media Classic:

|   | Vídeo do Experience Manager Foundation | Vídeo do Dynamic Media Classic |
|---|---|---|
| Abordagem | HTML5 primeira abordagem. O Flash é usado somente para fallback não HTML 5. | Flash na maioria dos desktops. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressivo | Streaming adaptável |
| Rastreamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configurar {#setting-up}

#### Criar perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do Dynamic Media Classic selecionadas na Configuração da nuvem do Dynamic Media Classic. Para que o componente de Vídeo de base os use, é necessário criar um perfil de vídeo para cada predefinição de codificação do Dynamic Media Classic selecionada. Ele permite que o componente de vídeo selecione as representações do DAM de acordo.

>[!NOTE]
>
>Novos perfis de vídeo e alterações neles devem ser ativados para publicar.

1. No Experience Manager, vá para **[!UICONTROL Ferramentas]** e selecione **[!UICONTROL Console de Configuração]**.
1. No Console de Configuração, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de Vídeo]** na árvore de navegação.
1. Crie um perfil de vídeo do Dynamic Media Classic. No menu **[!UICONTROL Novo]**, selecione **[!UICONTROL Criar página]**.
1. Selecione o modelo de perfil do Dynamic Media Classic Video. Dê um nome à nova página de perfil de vídeo e selecione **[!UICONTROL Criar]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite o novo perfil de vídeo. Selecione a configuração de nuvem primeiro. Em seguida, selecione a mesma predefinição de codificação que foi selecionada na configuração da nuvem.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriedade | Descrição |
   |---|---|
   | Configuração da nuvem do Dynamic Media Classic | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Dynamic Media Classic | A predefinição de codificação para mapear esse perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite que você defina o valor da propriedade type do elemento de fonte de vídeo HTML5. Essas informações não são fornecidas pelas predefinições de codificação do Dynamic Media Classic, mas são necessárias para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas pode ser substituída por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração da nuvem que você deseja usar no componente de vídeo.

#### Configurar design {#configuring-design}

O componente de vídeo de base deve saber quais perfis de vídeo usar para criar a lista de fontes de vídeo. Abra a caixa de diálogo de design de componentes de vídeo e configure o design de componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usar o componente de Vídeo de base em uma página móvel, repita essas etapas no design da página móvel.

>[!NOTE]
>
>As alterações feitas no design exigem a ativação do design para entrar em vigor na publicação.

1. Abra a caixa de diálogo de design do componente de vídeo de base e altere para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis prontos para uso e adicione os novos perfis de vídeo do Dynamic Media Classic. A ordem da lista de perfis na caixa de diálogo de design também define a ordem do elemento de fontes de vídeo durante a renderização.
1. Para navegadores não compatíveis com o HTML5, o componente de Vídeo permite configurar um fallback flash. Abra a caixa de diálogo de design dos componentes de vídeo e altere para a guia **[!UICONTROL Flash]**. Defina as configurações do flash player e atribua um perfil de fallback para o flash player.

#### Lista de verificação {#checklist}

1. Criar uma configuração de nuvem do Dynamic Media Classic. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do Dynamic Media Classic para cada predefinição de codificação de vídeo selecionada na configuração de nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente de vídeo base na sua página.
1. Ative o design depois de concluir as alterações de design.
