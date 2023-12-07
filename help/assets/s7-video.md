---
title: Vídeo
description: Saiba mais sobre a Adobe Experience Manager Assets de gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos para codificação automática no Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente da Experience Manager Assets. A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
role: User, Admin
mini-toc-levels: 3
exl-id: 56009925-1a36-48b5-b96c-ec2e468da106
feature: Video
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1551'
ht-degree: 1%

---

# Vídeo {#video}

O Adobe Experience Manager Assets fornece um gerenciamento centralizado de ativos de vídeo, em que você pode fazer upload de vídeos diretamente no Assets para codificação automática no Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente do Assets para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado a todas as telas (detecção automática de dispositivo e largura de banda).

* A variável **[!UICONTROL Vídeo do Scene7]** O componente executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato certo e o vídeo com a qualidade certa em desktops, tablets e dispositivos móveis.
* Ativos - É possível incluir conjuntos de vídeos adaptáveis em vez de apenas ativos de vídeo únicos. Um conjunto de vídeos adaptáveis contém todas as representações de vídeo necessárias para reproduzir vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptados agrupa versões do mesmo vídeo codificadas em taxas de bits e formatos diferentes, como 400 kbps, 800 kbps e 1000 kbps. Você usa um Conjunto de vídeos adaptados, juntamente com o componente de vídeo S7, para transmissão de vídeo adaptado em várias telas, incluindo dispositivos móveis para desktop, iOS, Android™, BlackBerry® e Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Sobre FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão é baseado no uso da integração baseada em FFMPEG com perfis de vídeo. Portanto, o fluxo de trabalho de assimilação do DAM pronto para uso contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

A ativação e a configuração da integração do Dynamic Media Classic não removem nem desativam automaticamente essas duas etapas do fluxo de trabalho de assimilação do DAM pronto para uso. Se você já usa a codificação de vídeo baseada em FFMPEG no Adobe Experience Manager, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando DAM seria codificado duas vezes: uma vez no codificador FFMPEG e outra na integração do Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG no Experience Manager configurada e o FFMPEG instalado, o Adobe recomenda remover os dois workflows FFMPEG dos workflows de assimilação do DAM.

## Formatos suportados {#supported-formats}

Os seguintes formatos são compatíveis com o componente de Vídeo do Scene7:

* F4V H.264
* MP4 H.264

## Decida onde carregar seu vídeo {#deciding-where-to-upload-your-video}

A decisão sobre onde carregar seus ativos de vídeo depende do seguinte:

* Você precisa de um fluxo de trabalho para o ativo de vídeo?
* Você precisa do controle de versão para o ativo de vídeo?

Se a resposta for &quot;sim&quot; a uma ou ambas as perguntas, carregue o vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; às duas perguntas, carregue o vídeo diretamente no Dynamic Media Classic. O fluxo de trabalho para cada cenário é descrito na seção a seguir.

### Se você estiver carregando o vídeo diretamente no DAM do Adobe {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Se precisar de um fluxo de trabalho ou controle de versão para seus ativos, carregue primeiro para o DAM do Adobe. O fluxo de trabalho recomendado é o seguinte:

1. Faça upload do ativo de vídeo para o DAM do Adobe e codifique e publique automaticamente no Dynamic Media Classic.
1. No Experience Manager, acesse os ativos de vídeo no WCM no **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Autor com **[!UICONTROL Vídeo do Scene7]** ou **[!UICONTROL Vídeo do Foundation]** componente.

### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se não precisar de um fluxo de trabalho ou controle de versão para seus ativos, faça upload dos ativos para a Scene7. O fluxo de trabalho recomendado é o seguinte:

1. No Dynamic Media Classic, [configurar o upload e a codificação programados do FTP no Scene7 (automatizado pelo sistema)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. No Experience Manager, acesse os ativos de vídeo no WCM no **[!UICONTROL Scene7]** do Localizador de conteúdo.
1. Autor com o **[!UICONTROL Vídeo do Scene7]** componente.

## Configurar integração com o Scene7 Video {#configuring-integration-with-scene-video}

1. Entrada **[!UICONTROL Cloud Service]**, navegue até o **[!UICONTROL Scene7]** e selecione **[!UICONTROL Editar]**.
1. Selecione o **[!UICONTROL Vídeo]** guia.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >A variável **[!UICONTROL Vídeo]** A guia não será exibida se a página não tiver uma configuração na nuvem.

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo único pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que significam as predefinições de vídeo, consulte [Documentação do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >Adobe recomenda selecionar os dois conjuntos de vídeo adaptável ao configurar as predefinições universais ou selecionar a variável **[!UICONTROL Codificação de vídeo adaptável]** opção.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta de destino do CQ DAM que você configurou para essa configuração de nuvem do Scene7. É possível definir várias configurações de nuvem do Scene7 com pastas de destino diferentes para aplicar perfis de codificação diferentes, conforme necessário.

## Atualizar predefinições do visualizador e de codificação {#updating-viewer-and-encoding-presets}

Para atualizar as predefinições do visualizador e de codificação para o vídeo porque as predefinições foram atualizadas no Scene7, navegue até a configuração do Scene7 na Configuração da nuvem e selecione **[!UICONTROL Atualizar o visualizador e as predefinições de codificação]**.

![chlimage_1-364](assets/chlimage_1-364.png)

## Faça upload do vídeo de origem principal para o Scene7 a partir do Adobe DAM {#uploading-your-master-video}

1. Navegue até a pasta de destino do CQ DAM, na qual você definiu a configuração da nuvem com perfis de codificação do Scene7.
1. Selecionar **[!UICONTROL Carregar]** para carregar o vídeo de origem principal. O upload e a codificação de vídeo são concluídos após a [!UICONTROL Ativo de atualização DAM] o fluxo de trabalho está concluído e **[!UICONTROL Publicar no Scene7]** tem uma marca de seleção.

   >[!NOTE]
   >
   >Demora até que as miniaturas de vídeo sejam geradas.

   Arrastar o vídeo de origem principal do DAM para o componente de vídeo acessa *all* Representações de proxy codificadas do Scene7 para entrega.

## Componente de vídeo do Foundation versus Componente de vídeo do Scene7 {#foundation-video-component-versus-scene-video-component}

Ao usar o Experience Manager, você tem acesso ao componente de Vídeo disponível no Sites e ao componente de Vídeo do Scene7. Esses componentes não são intercambiáveis.

O componente de vídeo do Scene7 só funciona para vídeos do Scene7. O componente de base funciona com vídeos armazenados em Experience Manager (usando ffmpeg) e vídeos do Scene7.

A matriz a seguir explica quando usar qual componente:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>Imediatamente, o componente de vídeo S7 usa o perfil de vídeo universal. Entretanto, você pode obter o reprodutor de vídeo baseado em HTML para uso pelo Experience Manager. No Scene7, copie o código incorporado do reprodutor de vídeo HTML5 pronto para uso e coloque-o na página Experience Manager.

## Componente de vídeo do Experience Manager {#aem-video-component}

Mesmo que o uso do componente de vídeo do Scene7 seja recomendado para visualizar vídeos do Scene7, esta seção descreve o uso de vídeos do Scene7 com o componente de vídeo de base no Experience Manager, para fins de integridade.

### Comparação entre Experience Manager Video e Scene7 Video {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação de alto nível de recursos compatíveis entre o componente de Vídeo de base do Experience Manager e o componente de Vídeo do Scene7:

|   | Vídeo do Experience Manager Foundation | Vídeo do Scene7 |
|---|---|---|
| Abordagem | HTML5 primeira abordagem. O Flash é usado somente para fallback não HTML 5. | Flash na maioria dos desktops. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressivo | Streaming adaptável |
| Rastreamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configurar {#setting-up}

#### Criar perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do S7 selecionadas na configuração da nuvem do S7. Para que o componente de vídeo de base os use, um perfil de vídeo deve ser criado para cada predefinição de codificação S7 selecionada. Esse método permite que o componente de vídeo selecione as representações do DAM de acordo.

>[!NOTE]
>
>Novos perfis de vídeo e alterações neles devem ser ativados para publicar.

1. No Experience Manager, selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Console de configuração]**.
1. No **[!UICONTROL Console de configuração]**, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL DAM]** > **[!UICONTROL Perfis de vídeo]** na árvore de navegação.
1. Crie um perfil de vídeo S7. No **[!UICONTROL Novo]**. selecione **[!UICONTROL Criar página]** e selecione o modelo Perfil de vídeo do Scene7. Nomeie a nova página de perfil de vídeo e selecione **[!UICONTROL Criar]**.

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Edite o novo perfil de vídeo. Selecione a configuração de nuvem primeiro. Em seguida, selecione a mesma predefinição de codificação que foi selecionada na configuração da nuvem.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propriedade | Descrição |
   |---|---|
   | Configurações de nuvem do Scene7 | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Scene7 | A predefinição de codificação para mapear esse perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite que você defina o valor da propriedade type do elemento de fonte de vídeo HTML5. Essas informações não são fornecidas pelas predefinições de codificação do S7, mas são necessárias para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas pode ser substituída por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração da nuvem que você deseja usar no componente de vídeo.

#### Configurar design {#configuring-design}

A variável **[!UICONTROL Vídeo do Foundation]** O componente de deve saber quais perfis de vídeo usar para criar a lista de fontes de vídeo. Abra a caixa de diálogo design de componentes de vídeo e configure o design de componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usar o **[!UICONTROL Vídeo do Foundation]** em uma página para dispositivos móveis, repita essas etapas no design da página para dispositivos móveis.

>[!NOTE]
>
>As alterações feitas no design exigem a ativação do design para entrar em vigor na publicação.

1. Abra o **[!UICONTROL Vídeo do Foundation]** caixa de diálogo design do componente e altere para a **[!UICONTROL Perfis]** guia. Em seguida, exclua os perfis prontos para uso e adicione os novos perfis de vídeo S7. A ordem da lista de perfis na caixa de diálogo design define a ordem do elemento de fontes de vídeo durante a renderização.
1. Para navegadores que não aceitam o HTML5, o componente de vídeo permite configurar um fallback de Flash. Abra a caixa de diálogo design de componentes de vídeo e altere para a **[!UICONTROL Flash]** guia. Defina as configurações do reprodutor Flash e atribua um perfil de fallback para o reprodutor flash.

#### Lista de verificação {#checklist}

1. Criar uma configuração de nuvem S7. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo S7 para cada predefinição de codificação de vídeo selecionada na configuração de nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configurar o design do **[!UICONTROL Vídeo do Foundation]** componente na sua página.
1. Ative o design depois de concluir as alterações de design.
