---
title: Vídeo
seo-title: Vídeo
description: Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os Ativos, com o objetivo de codificar automaticamente para o Dynamic Media Classic, e acessar os vídeos do dia diretamente dos Ativos, para criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
exl-id: c540aa49-9981-4e8c-97df-972085b26490
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '1699'
ht-degree: 38%

---

# Vídeo{#video}

Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os ativos para autocodificação para o Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente dos Ativos para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas (detecção automática de dispositivo e de largura de banda).

* O componente de vídeo do Dynamic Media Classic executa automaticamente a detecção de dispositivo e de largura de banda para reproduzir o vídeo no formato adequado e de qualidade certa em desktops, tablets e dispositivos móveis.
* Assets: é possível incluir conjuntos de vídeos adaptáveis, em vez de somente ativos de vídeo individuais. Um conjunto de vídeos adaptáveis é um contêiner para todas as representações de vídeo necessárias para reproduzir o vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo codificadas em diferentes formatos e taxas de bits, como 400 kbps, 800 kbps e 1000 kbps. Você usa um conjunto de vídeos adaptáveis, juntamente com o componente de vídeo do S7, para transmitir vídeo adaptável em vários tipos de telas, incluindo telas de computadores, e dispositivos móveis com iOS, Android, Blackberry e Windows. Consulte a [documentação do Dynamic Media Classic sobre conjuntos de vídeos adaptáveis para obter mais informações](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Sobre FFMPEG e Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão se baseia no uso da integração em FFMPEG com perfis de vídeo. Portanto, o fluxo de trabalho pronto para uso [!UICONTROL Ativo de atualização do DAM] contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Esteja ciente de que ativar e configurar a integração do Dynamic Media Classic não remove ou desativa automaticamente essas duas etapas do fluxo de trabalho do fluxo de trabalho de assimilação [!UICONTROL Ativo de atualização do DAM] pronto para uso. Se você já usa a codificação de vídeo baseada em FFMPEG no AEM, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando Ativos seria codificado duas vezes: uma vez no codificador FFMPEG e uma vez na integração do Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG AEM configurada e o FFMPEG instalado, o Adobe recomenda remover os dois workflows FFMPEG dos workflows [!UICONTROL Ativo de atualização DAM].

### Formatos suportados {#supported-formats}

Os seguintes formatos são compatíveis com o componente Vídeo do Dynamic Media Classic:

* F4V H.264
* MP4 H.264

### Como decidir onde fazer upload de seu vídeo {#deciding-where-to-upload-your-video}

Para decidir onde fazer upload de seus ativos de vídeo, considere o seguinte:

* O ativo de vídeo requer um fluxo de trabalho?
* O ativo de vídeo requer controle de versão?

Se a resposta for “sim” para ambas as perguntas, faça upload do vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; para ambas as perguntas, faça upload do vídeo diretamente no Dynamic Media Classic. O fluxo de trabalho referente a cada cenário é descrito na próxima seção.

#### Se estiver fazendo upload do vídeo diretamente no Adobe Assets  {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se for necessário um fluxo de trabalho ou controle de versão para seus ativos, você deverá fazer upload primeiro no Adobe Assets. Este é o fluxo de trabalho recomendado:

1. Faça upload do ativo de vídeo para Ativos Adobe e codifique e publique automaticamente no Dynamic Media Classic.
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Crie com o vídeo do Dynamic Media Classic ou componente de vídeo de base.

#### Se você estiver fazendo upload de seu vídeo para o Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se não precisar de um fluxo de trabalho ou controle de versão para seus ativos, faça upload dos ativos para o Dynamic Media Classic. Este é o fluxo de trabalho recomendado:

1. No aplicativo de desktop do Dynamic Media Classic, [configure um upload e uma codificação FTP programadas para o Dynamic Media Classic (automatizada pelo sistema)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Dynamic Media Classic]** do Localizador de conteúdo.
1. Crie com o componente de vídeo do Dynamic Media Classic.

### Configuração da integração com o Dynamic Media Classic Video {#configuring-integration-with-scene-video}

**Para configurar predefinições universais**:

1. Em **[!UICONTROL Cloud Services]**, navegue até a configuração **[!UICONTROL Dynamic Media Classic]** e clique em **[!UICONTROL Editar]**.
1. Selecione a guia **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não possuir uma configuração de nuvem. Consulte [Ativar o Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que significam as predefinições de vídeo, consulte [Predefinições de vídeo para codificação de arquivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files).
   >
   >A Adobe recomenda selecionar ambos os conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecionar a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta de destino do DAM CQ configurada para essa configuração de nuvem do Dynamic Media Classic. Você pode configurar várias configurações de nuvem do Dynamic Media Classic com diferentes pastas de destino para aplicar diferentes perfis de codificação, conforme necessário.

### Atualizar as predefinições de codificação e do visualizador {#updating-viewer-and-encoding-presets}

Se você precisar atualizar as predefinições de codificação e do visualizador de vídeo no AEM porque elas foram atualizadas no Dynamic Media Classic, navegue até a configuração do Dynamic Media Classic na configuração da nuvem e clique em **Atualizar as predefinições de codificação e do visualizador**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Fazer upload do vídeo de origem primária {#uploading-your-master-video}

Para fazer upload do vídeo de origem primária para o Dynamic Media Classic a partir do Adobe DAM:

1. Navegue até a pasta de destino DAM do CQ, onde você configurou sua configuração de nuvem com perfis de codificação do Dynamic Media Classic.
1. Clique em **[!UICONTROL Upload]** para fazer upload do vídeo de origem primária. O upload e a codificação do vídeo são concluídos depois que o fluxo de trabalho [!UICONTROL Ativo de atualização DAM] é concluído e **[!UICONTROL Publicar no Dynamic Media Classic]** tem uma marca de seleção.

   >[!NOTE]
   >
   >Pode levar algum tempo para gerar as miniaturas de vídeo.

   Arrastar o vídeo de origem primária do DAM para o componente de vídeo acessa *all* das representações de proxy codificadas do Dynamic Media Classic para entrega.

### Componente de vídeo de base versus Componente de vídeo do Dynamic Media Classic {#foundation-video-component-versus-scene-video-component}

Ao usar o AEM, você tem acesso ao componente Vídeo disponível no Sites e ao componente de vídeo do Dynamic Media Classic. Esses componentes não são intercambiáveis.

O componente de vídeo do Dynamic Media Classic só funciona para vídeos do Dynamic Media Classic. O componente de base funciona com vídeos armazenados do AEM (usando ffmpeg) e vídeos do Dynamic Media Classic.

A seguinte matriz explica quando você deve usar cada componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>Pronto para uso, o componente de vídeo do Dynamic Media Classic usa o perfil de vídeo universal. No entanto, você pode obter o reprodutor de vídeo baseado em HTML5 para uso pelo AEM. No Dynamic Media Classic, copie o código incorporado do reprodutor de vídeo HTML5 pronto para uso e coloque-o na página de AEM.


## Componente de vídeo do AEM {#aem-video-component}

Mesmo que o uso do componente de vídeo do Dynamic Media Classic seja recomendado para visualizar vídeos do Dynamic Media Classic, esta seção descreve o uso de vídeos do Dynamic Media Classic com o [!UICONTROL Componente de vídeo de base] no AEM, por uma questão de integridade.

### Comparação entre vídeo AEM e vídeo do Dynamic Media Classic {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação de alto nível dos recursos suportados entre o componente AEM Foundation Video e o componente Dynamic Media Classic Video:

|  | Vídeo de base do AEM | Vídeo do Dynamic Media Classic |
|---|---|---|
| Abordagem | Abordagem de HTML5 primeiro. O Flash é usado somente para o fallback não-HTML5. | Flash na maioria dos computadores. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressiva | Transmissão adaptável |
| Acompanhamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configuração  {#setting-up}

#### Criação de perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do Dynamic Media Classic selecionadas na configuração da nuvem do Dynamic Media Classic. Para que o componente de vídeo de base os use, um perfil de vídeo deve ser criado para cada predefinição de codificação do Dynamic Media Classic selecionada. Isso permite que o componente de vídeo selecione as execuções de DAM apropriadas.

>[!NOTE]
>
>Os novos perfis de vídeo e as alterações a eles devem ser ativados para publicação.

1. No Experience Manager, vá para **[!UICONTROL Ferramentas]** e selecione **[!UICONTROL Console de Configuração]**. No Console de configuração, navegue até **[!UICONTROL Ferramentas]** > **[!UICONTROL Ativos]** > **[!UICONTROL Perfis de vídeo]** na árvore de navegação.
1. Crie um novo perfil de vídeo do Dynamic Media Classic. No **[!UICONTROL Novo]**. selecione **[!UICONTROL Criar página]** e selecione o modelo de Perfil de vídeo do Dynamic Media Classic . Forneça um nome para a nova página de perfil de vídeo e clique em **[!UICONTROL Criar]**.

   ![chlimage_1-133](assets/chlimage_1-133.png)

1. Edite o novo perfil de vídeo. Selecione primeiro a configuração de nuvem. Em seguida, selecione a mesma predefinição de codificação selecionada na configuração de nuvem.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriedade | Descrição |
   |---|---|
   | Configuração da nuvem do Dynamic Media Classic | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Predefinição de codificação do Dynamic Media Classic | A predefinição de codificação com a qual mapear esse perfil de vídeo. |
   | Tipo de vídeo HTML5 | Essa propriedade permite definir o valor da propriedade type do elemento de fonte de vídeo HTML5. Essas informações não são fornecidas pelas predefinições de codificação do Dynamic Media Classic, mas são necessárias para renderizar corretamente os vídeos usando o elemento de vídeo HTML5. Uma lista de formatos comuns é fornecida, mas eles podem ser substituídos por outros formatos. |

   Repita essa etapa para todas as predefinições de codificação selecionadas na configuração de nuvem que você deseja usar no componente de vídeo.

#### Configuração do design  {#configuring-design}

O componente de vídeo de base deve saber quais perfis de vídeo usar para que possa construir a lista de origens de vídeo. É preciso abrir a caixa de diálogo dos componentes de vídeo e configurar o design dos componentes para usar os novos perfis de vídeo.

>[!NOTE]
>
>Se você usa o componente de vídeo de base em uma página para dispositivos móveis, talvez seja necessário repetir essas etapas no design da página móvel.

>[!NOTE]
>
>As alterações feitas no design exigem que ele seja aplicado para serem aplicadas na publicação.

1. Abra a caixa de diálogo de design do componente de vídeo de base e altere para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis prontos e adicione os novos perfis de vídeo do Dynamic Media Classic. A ordem da lista de perfis na caixa de diálogo de design também define a ordem do elemento de fontes de vídeo ao renderizar.
1. Para os navegadores que não oferecem suporte ao HTML5, o componente de vídeo permite configurar um fallback de flash. Abra a caixa de diálogo de design dos componentes de vídeo e altere para a guia **[!UICONTROL Flash]**. Ajuste as configurações do flash player e atribua um perfil de fallback a ele.

#### Lista de verificação {#checklist}

1. Crie uma configuração de nuvem do Dynamic Media Classic. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do Dynamic Media Classic para cada predefinição de codificação de vídeo selecionada na configuração de nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente de vídeo de base na sua página.
1. Ative o design após finalizar as alterações no design.
