---
title: Vídeo
description: Saiba mais sobre o gerenciamento centralizado de ativos de vídeo no AEM Assets, onde você pode fazer upload de vídeos para autocodificação no Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente da AEM Assets. A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas.
uuid: 8b3423f1-d96b-44d9-bdb7-e3b77875b25d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: managing-assets
content-type: reference
discoiquuid: 2685f9f3-0973-40a9-89b8-e7db0a6a75f2
translation-type: tm+mt
source-git-commit: 4333cfde433d00ddc4cb013b31fe52956791da46
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 54%

---


# Vídeo {#video}

Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os Ativos para autocodificação para o Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente dos Ativos para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas (detecção automática de dispositivo e largura de banda).

* O componente **[!UICONTROL Scene7 Video]** executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato correto e o vídeo de qualidade correta em desktops, tablets e dispositivos móveis.
* Assets: é possível incluir conjuntos de vídeos adaptáveis, em vez de somente ativos de vídeo individuais. Um conjunto de vídeos adaptáveis é um contêiner para todas as representações de vídeo necessárias para reproduzir o vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo que são codificadas em diferentes taxas de bits e formatos, como 400 kbps, 800 kbps e 1000 kbps. Você usa um conjunto de vídeos adaptáveis, juntamente com o componente de vídeo do S7, para transmitir vídeo adaptável em vários tipos de telas, incluindo telas de computadores, e dispositivos móveis com iOS, Android, Blackberry e Windows.
<!-- See [Scene7 documentation about adaptive video sets for more information](https://help.adobe.com/en_US/scene7/using/WS53492AE1-6029-45d8-BF80-F4B5CF33EB08.html). -->

## Sobre o FFMPEG e o Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão se baseia no uso da integração em FFMPEG com perfis de vídeo. Portanto, o fluxo de trabalho de ingestão DAM predefinido contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Lembre-se de que ativar e configurar a integração do Dynamic Media Classic não remove nem desativa automaticamente essas duas etapas do fluxo de trabalho do fluxo de trabalho de ingestão DAM predefinido. Se você já usa a codificação de vídeo baseada em FFMPEG no AEM, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando DAM seria codificado duas vezes: uma vez do codificador FFMPEG e uma vez da integração com o Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG em AEM configurada e FFMPEG instalada, o Adobe recomenda que você remova os dois workflows FFMPEG de seus workflows de ingestão de DAM.

## Formatos suportados {#supported-formats}

Os seguintes formatos são compatíveis com o componente de vídeo do Scene7:

* F4V H.264
* MP4 H.264

## Como decidir onde fazer upload de seu vídeo {#deciding-where-to-upload-your-video}

Para decidir onde fazer upload de seus ativos de vídeo, considere o seguinte:

* O ativo de vídeo requer um fluxo de trabalho?
* O ativo de vídeo requer controle de versão?

Se a resposta for “sim” para ambas as perguntas, faça upload do vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; para ambas as perguntas, faça upload do vídeo diretamente para o Dynamic Media Classic. O fluxo de trabalho referente a cada cenário é descrito na próxima seção.

### Se você estiver carregando seu vídeo diretamente para Adobe DAM {#if-you-are-uploading-your-video-directly-to-adobe-dam}

Se precisar de um fluxo de trabalho ou controle de versão para seus ativos, faça upload para o Adobe DAM primeiro. Este é o fluxo de trabalho recomendado:

1. Faça upload do ativo de vídeo para Adobe DAM e codifique e publique automaticamente no Dynamic Media Classic.
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Autor com o componente **[!UICONTROL Scene7 Video]** ou **[!UICONTROL Foundation Video]**.

### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se você não precisar de um fluxo de trabalho ou controle de versão para os ativos, faça upload deles no Scene7. Este é o fluxo de trabalho recomendado:

1. No Dynamic Media Classic, [configure um carregamento e codificação FTP programados para o Scene7 (automatizado pelo sistema)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/uploading-files.html#upload-files-using-via-ftp).
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Scene7]** do Localizador de conteúdo.
1. Autor com o componente **[!UICONTROL Scene7 Video]**.

## Configurar a integração de vídeo do Scene7 {#configuring-integration-with-scene-video}

Para configurar predefinições universais:

1. Em **[!UICONTROL Serviços em nuvem]**, navegue até a configuração do **[!UICONTROL Scene7]** e clique em **[!UICONTROL Editar.]**
1. Selecione a guia **[!UICONTROL Vídeo]**.

   ![chlimage_1-363](assets/chlimage_1-363.png)

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não possuir uma configuração de nuvem.

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que as predefinições de vídeo significam, consulte a [documentação do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html#video-presets-for-encoding-video-files).
   >
   >A Adobe recomenda selecionar ambos os conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecionar a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos enviados por upload para a pasta de destino DAM CQ configurada para essa configuração de nuvem do Scene7. É possível configurar várias configurações de nuvem do Scene7 com diferentes pastas de destino para aplicar diversos perfis de codificação, conforme necessário.

## Atualizar as predefinições de codificação e do visualizador  {#updating-viewer-and-encoding-presets}

Se você precisar atualizar as predefinições de codificação de vídeo e do visualizador no AEM porque elas foram atualizadas no Scene7, navegue até a configuração do Scene7 na configuração de nuvem e clique em **[!UICONTROL Atualizar as predefinições de codificação e do visualizador.]**

![chlimage_1-364](assets/chlimage_1-364.png)

## Carregar o vídeo de origem primária para o Scene7 a partir do Adobe DAM {#uploading-your-master-video}

1. Navegue até a pasta de destino DAM CQ onde você definiu as configurações de nuvem com os perfis de codificação do Scene7.
1. Clique em **[!UICONTROL Carregar]** para carregar o vídeo de origem primária. O upload e a codificação do vídeo são concluídos depois que o fluxo de trabalho [!UICONTROL DAM Update Asset] é concluído e **[!UICONTROL Publicar no Scene7]** tem uma marca de seleção.

   >[!NOTE]
   >
   >Pode levar algum tempo para gerar as miniaturas de vídeo.

   Arrastar o vídeo de origem primária do DAM para o componente de vídeo acessa *all* das renderizações de proxy codificadas do Scene7 para o delivery.

## Comparação do componente de vídeo de base com o componente de vídeo do Scene7 {#foundation-video-component-versus-scene-video-component}

Ao usar o AEM, você tem acesso ao componente de Vídeo disponível no Sites e o componente de vídeo do Scene7. Esses componentes não são intercambiáveis.

O componente de vídeo do Scene7 funciona somente para vídeos do Scene7. O componente de base funciona com os vídeos armazenados do AEM (usando ffmpeg) e com os vídeos do Scene7.

A seguinte matriz explica quando você deve usar cada componente:

![chlimage_1-365](assets/chlimage_1-365.png)

>[!NOTE]
>
>Pronto para uso, o componente de vídeo do S7 usa o perfil de vídeo universal. No entanto, você pode obter o player de vídeo baseado em HTML5 para uso AEM executando um dos procedimentos a seguir no Scene7: copie o código incorporado do player de vídeo HTML5 e coloque-o na sua página de AEM.

## Componente de vídeo do AEM {#aem-video-component}

Mesmo que o uso do componente de vídeo do Scene7 seja recomendado para visualizar os vídeos do Scene7, esta seção descreve o uso dos vídeos do Scene7 com o Componente de vídeo de base do AEM, por uma questão de completude.

### Comparação entre vídeos do Scene7 e do AEM  {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação avançada dos recursos suportados entre o Componente de vídeo de base do AEM e o Componente de vídeo do Scene7:

|  | Vídeo de base do AEM | Vídeo do Scene7 |
|---|---|---|
| Abordagem | Abordagem de HTML5 primeiro. O Flash é usado somente para o fallback não-HTML5. | Flash na maioria dos computadores. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressiva | Transmissão adaptável |
| Acompanhamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configuração  {#setting-up}

#### Criação de perfis de vídeo {#creating-video-profiles}

As diferentes codificações de vídeo são criadas de acordo com as predefinições de codificação do S7 selecionadas na configuração de nuvem do S7. Para que possam ser utilizadas pelo componente de vídeo de base, um perfil de vídeo deve ser criado para cada predefinição de codificação do S7 selecionada. Isso permite que o componente de vídeo selecione as execuções de DAM apropriadas.

>[!NOTE]
>
>Os novos perfis de vídeo e as alterações a eles devem ser ativados para publicação.

1. No AEM, toque em **[!UICONTROL Ferramentas] > [!UICONTROL Console de Configuração]**.
1. Na **[!UICONTROL Console de configuração]** navegue até **[!UICONTROL Ferramentas > DAM > Perfis de vídeo]** na árvore de navegação.
1. Crie um novo perfil de vídeo do S7. No **[!UICONTROL Novo...]**, selecione **[!UICONTROL Criar página]** e selecione o modelo de Perfil de vídeo Scene7. Forneça um nome para a nova página de perfil de vídeo e clique em **[!UICONTROL Criar.]**

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. Edite o novo perfil de vídeo. Selecione primeiro a configuração de nuvem. Em seguida, selecione a mesma predefinição de codificação selecionada na configuração de nuvem.

   ![chlimage_1-367](assets/chlimage_1-367.png)

   | Propriedade | Descrição |
   |---|---|
   | Configurações de nuvem do Scene7 | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Scene7 | A predefinição de codificação para mapear este perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite definir o valor da propriedade type do elemento de fonte de vídeo HTML5. Essa informação não é fornecida pelas predefinições de codificação do S7, mas é necessária para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas eles podem ser substituídos por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração de nuvem que você deseja usar no componente de vídeo.

#### Configurando o design {#configuring-design}

O componente **[!UICONTROL Foundation Video]** deve saber quais perfis de vídeo serão usados para criar a lista de fontes de vídeo. Você deve abrir a caixa de diálogo de design de componentes de vídeo e configurar o design de componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usar o componente **[!UICONTROL Foundation Video]** em uma página móvel, talvez seja necessário repetir essas etapas no design da página móvel.

>[!NOTE]
>
>As alterações feitas no design exigem que ele seja aplicado para serem aplicadas na publicação.

1. Abra a caixa de diálogo de design do componente **[!UICONTROL Foundation Video]** e mude para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis predefinidos e adicione os novos perfis de vídeo S7. A ordem da lista do perfil na caixa de diálogo de design define a ordem do elemento de fontes de vídeo ao renderizar.
1. Para navegadores que não suportam HTML5, o componente de vídeo permite configurar um fallback de Flash. Abra a caixa de diálogo de design de componentes de vídeo e mude para a guia **[!UICONTROL Flash]**. Configure as configurações do player de Flash e atribua um perfil de fallback ao player flash.

#### Lista de verificação {#checklist}

1. Crie uma configuração de nuvem do S7. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do S7 para cada predefinição de codificação de vídeo selecionada na configuração da nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente **[!UICONTROL Foundation Video]** na sua página.
1. Ative o design após finalizar as alterações no design.

