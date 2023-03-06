---
title: Criação de vídeos no Sites Classic
description: Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente no Assets para codificação automática no Dynamic Media Classic e acessar vídeos diários diretamente do Assets para a criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: 59e182c165f6fd4b822eaf0e34f6e4b3bb18eb14
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 26%

---

# Vídeo{#video}

Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente no Assets para codificação automática no Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente do Assets para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado a todas as telas (detecção automática de dispositivo e largura de banda).

* O componente de vídeo do Dynamic Media Classic executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato e o vídeo com a qualidade ideais em desktops, tablets e dispositivos móveis.
* Assets: é possível incluir conjuntos de vídeos adaptáveis, em vez de somente ativos de vídeo individuais. Um conjunto de vídeos adaptáveis é um container para todas as representações de vídeo necessárias para reproduzir vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptados agrupa versões do mesmo vídeo codificadas em taxas de bits e formatos diferentes, como 400 kbps, 800 kbps e 1000 kbps. Você usa um Conjunto de vídeos adaptados, juntamente com o componente de vídeo S7, para transmissão de vídeo adaptado em várias telas, incluindo dispositivos móveis para desktop, iOS, Android™, BlackBerry® e Windows. Consulte [Documentação do Dynamic Media Classic sobre conjuntos de vídeos adaptáveis para obter mais informações](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Sobre FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão se baseia no uso da integração em FFMPEG com perfis de vídeo. Portanto, a solução pronta para uso [!UICONTROL Ativo de atualização DAM] o fluxo de trabalho contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Habilitar e configurar a integração do Dynamic Media Classic não remove nem desativa automaticamente essas duas etapas do fluxo de trabalho, prontas para uso [!UICONTROL Ativo de atualização DAM] fluxo de trabalho de assimilação. Se você já usa a codificação de vídeo baseada em FFMPEG no Adobe Experience Manager, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando o Experience Manager Assets é codificado duas vezes: uma vez do codificador FFMPEG e outra da integração do Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG no Experience Manager configurada e o FFMPEG instalado, o Adobe recomenda remover os dois workflows FFMPEG do [!UICONTROL Ativo de atualização DAM] fluxos de trabalho.

### Formatos suportados {#supported-formats}

Os seguintes formatos são compatíveis com o componente de Vídeo do Dynamic Media Classic:

* F4V H.264
* MP4 H.264

### Decida onde carregar seu vídeo {#deciding-where-to-upload-your-video}

Para decidir onde fazer upload de seus ativos de vídeo, considere o seguinte:

* O ativo de vídeo requer um fluxo de trabalho?
* O ativo de vídeo requer controle de versão?

Se a resposta for “sim” para ambas as perguntas, faça upload do vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; às duas perguntas, carregue o vídeo diretamente no Dynamic Media Classic. O fluxo de trabalho referente a cada cenário é descrito na próxima seção.

#### Se estiver fazendo upload do vídeo diretamente no Adobe Assets {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se for necessário um fluxo de trabalho ou controle de versão para seus ativos, você deverá fazer upload primeiro no Adobe Assets. Este é o fluxo de trabalho recomendado:

1. Faça upload do ativo de vídeo para o Adobe Assets e codifique e publique automaticamente no Dynamic Media Classic.
1. No Experience Manager, acesse os ativos de vídeo no WCM no **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Crie com o vídeo do Dynamic Media Classic ou o componente de vídeo da fundação.

#### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se não precisar de um fluxo de trabalho ou controle de versão para seus ativos, você deve fazer upload dos ativos para a Dynamic Media Classic. Este é o fluxo de trabalho recomendado:

1. No aplicativo de desktop do Dynamic Media Classic, [configurar o upload e a codificação programados do FTP no Dynamic Media Classic (automatizado pelo sistema)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-options).
1. No Experience Manager, acesse os ativos de vídeo no WCM no **[!UICONTROL Dynamic Media Classic]** do Localizador de conteúdo.
1. Crie com o componente de vídeo do Dynamic Media Classic.

### Configurar integração com o Dynamic Media Classic Video {#configuring-integration-with-scene-video}

1. Entrada **[!UICONTROL Cloud Services]**, navegue até o **[!UICONTROL Dynamic Media Classic]** e selecione **[!UICONTROL Editar]**.
1. Selecione a guia **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não possuir uma configuração de nuvem. Consulte [Ativar o Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que significam as predefinições de vídeo, consulte [Predefinições de vídeo para codificar arquivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >A Adobe recomenda selecionar ambos os conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecionar a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta de destino do CQ DAM que você configurou para esta configuração de nuvem do Dynamic Media Classic. É possível definir várias configurações de nuvem do Dynamic Media Classic com pastas de destino diferentes para aplicar perfis de codificação diferentes, conforme necessário.

### Atualizar as predefinições de codificação e do visualizador {#updating-viewer-and-encoding-presets}

Atualize as predefinições do visualizador e de codificação para vídeo no Experience Manager se as predefinições tiverem sido atualizadas no Dynamic Media Classic. Nesse caso, navegue até a configuração do Dynamic Media Classic na configuração da nuvem e selecione **Atualizar o visualizador e as predefinições de codificação**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Fazer upload do vídeo de origem principal {#uploading-your-master-video}

Para carregar o vídeo de origem principal no Dynamic Media Classic a partir do Adobe DAM:

1. Navegue até a pasta de destino do CQ DAM, na qual você definiu a configuração da nuvem com perfis de codificação do Dynamic Media Classic.
1. Selecionar **[!UICONTROL Carregar]** para carregar o vídeo de origem principal. O upload e a codificação de vídeo são concluídos após a [!UICONTROL Ativo de atualização DAM] o fluxo de trabalho está concluído e **[!UICONTROL Publicar no Dynamic Media Classic]** tem uma marca de seleção.

   >[!NOTE]
   >
   >Pode levar algum tempo para gerar as miniaturas de vídeo.

   Ao arrastar o vídeo de origem primária DAM para o componente de vídeo, ele acessa *all* Representações de proxy codificadas do Dynamic Media Classic para entrega.

### Componente de vídeo do Foundation versus componente de vídeo do Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Ao usar o Experience Manager, você tem acesso ao componente de Vídeo disponível no Sites e ao componente de Vídeo do Dynamic Media Classic. Esses componentes não são intercambiáveis.

O componente de vídeo do Dynamic Media Classic só funciona para vídeos do Dynamic Media Classic. O componente de base funciona com vídeos armazenados em Experience Manager (usando ffmpeg) e vídeos do Dynamic Media Classic.

A seguinte matriz explica quando você deve usar cada componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Pronto para uso, o componente de vídeo do Dynamic Media Classic usa o perfil de vídeo universal. Entretanto, é possível obter o reprodutor de vídeo baseado em HTML para uso pelo Experience Manager. No Dynamic Media Classic, copie o código incorporado do reprodutor de vídeo HTML5 pronto para uso e coloque-o na página Experience Manager.

## Componente de vídeo do Experience Manager {#aem-video-component}

Mesmo que o uso do componente de Vídeo do Dynamic Media Classic seja recomendado para visualizar vídeos do Dynamic Media Classic, esta seção descreve o uso de vídeos do Dynamic Media Classic com o [!UICONTROL Componente de vídeo do Foundation] em Experience Manager para integridade.

### Comparação entre Experience Manager Video e Dynamic Media Classic Video {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação de alto nível de recursos compatíveis entre o componente de Vídeo de base do Experience Manager e o componente de Vídeo do Dynamic Media Classic:

|  | Vídeo do Experience Manager Foundation | Vídeo do Dynamic Media Classic |
|---|---|---|
| Abordagem | Abordagem de HTML5 primeiro. O Flash é usado somente para o fallback não-HTML5. | Flash na maioria dos computadores. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressiva | Transmissão adaptável |
| Acompanhamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configurar {#setting-up}

#### Criar perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do Dynamic Media Classic selecionadas na Configuração da nuvem do Dynamic Media Classic. Para que o componente de Vídeo de base os use, é necessário criar um perfil de vídeo para cada predefinição de codificação do Dynamic Media Classic selecionada. Ele permite que o componente de vídeo selecione as representações do DAM de acordo.

>[!NOTE]
>
>Os novos perfis de vídeo e as alterações a eles devem ser ativados para publicação.

1. No Experience Manager, acesse **[!UICONTROL Ferramentas]** e selecione **[!UICONTROL Console de configuração]**.
1. No Console de configuração, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Assets]** > **[!UICONTROL Perfis de vídeo]** na árvore de navegação.
1. Crie um perfil de vídeo do Dynamic Media Classic. No **[!UICONTROL Novo]** selecione **[!UICONTROL Criar página]**.
1. Selecione o modelo de perfil do Dynamic Media Classic Video. Nomeie a nova página de perfil de vídeo e selecione **[!UICONTROL Criar]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite o novo perfil de vídeo. Selecione primeiro a configuração de nuvem. Em seguida, selecione a mesma predefinição de codificação selecionada na configuração de nuvem.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriedade | Descrição |
   |---|---|
   | Configuração da nuvem do Dynamic Media Classic | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Dynamic Media Classic | A predefinição de codificação para mapear esse perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite que você defina o valor da propriedade type do elemento de fonte de vídeo HTML5. Essas informações não são fornecidas pelas predefinições de codificação do Dynamic Media Classic, mas são necessárias para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas eles podem ser substituídos por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração de nuvem que você deseja usar no componente de vídeo.

#### Configurar design {#configuring-design}

O componente de vídeo de base deve saber quais perfis de vídeo usar para que possa construir a lista de origens de vídeo. Abra a caixa de diálogo de design de componentes de vídeo e configure o design de componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usar o componente de Vídeo de base em uma página móvel, repita essas etapas no design da página móvel.

>[!NOTE]
>
>As alterações feitas no design exigem que ele seja aplicado para serem aplicadas na publicação.

1. Abra a caixa de diálogo de design do componente de vídeo de base e altere para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis prontos para uso e adicione os novos perfis de vídeo do Dynamic Media Classic. A ordem da lista de perfis na caixa de diálogo de design também define a ordem do elemento de fontes de vídeo durante a renderização.
1. Para navegadores não compatíveis com o HTML5, o componente de Vídeo permite configurar um fallback flash. Abra a caixa de diálogo de design dos componentes de vídeo e altere para a guia **[!UICONTROL Flash]**. Ajuste as configurações do flash player e atribua um perfil de fallback a ele.

#### Lista de verificação {#checklist}

1. Criar uma configuração de nuvem do Dynamic Media Classic. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do Dynamic Media Classic para cada predefinição de codificação de vídeo selecionada na configuração de nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente de vídeo de base na sua página.
1. Ative o design após finalizar as alterações no design.
