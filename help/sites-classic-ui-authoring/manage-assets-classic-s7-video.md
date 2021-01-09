---
title: Vídeo
seo-title: Vídeo
description: Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os Ativos para autocodificação para o Dynamic Media Classic e acessar vídeos do dia diretamente dos Ativos para criação de página.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: dfaa4b3f-f65a-4fe3-87a7-f3bc71015e56
translation-type: tm+mt
source-git-commit: 801d57bbe8a1bede6dcb4bf7884e5f71ddea1e83
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 38%

---


# Vídeo{#video}

Os ativos fornecem gerenciamento centralizado de ativos de vídeo, onde você pode fazer upload de vídeos diretamente para os Ativos para autocodificação para o Dynamic Media Classic e acessar vídeos do Dynamic Media Classic diretamente dos Ativos para criação de página.

A integração de vídeo do Dynamic Media Classic estende o alcance do vídeo otimizado para todas as telas (detecção automática de dispositivo e largura de banda).

* O componente de vídeo do Dynamic Media Classic executa automaticamente a detecção de dispositivos e largura de banda para reproduzir o formato correto e o vídeo de qualidade correta em desktops, tablets e dispositivos móveis.
* Assets: é possível incluir conjuntos de vídeos adaptáveis, em vez de somente ativos de vídeo individuais. Um conjunto de vídeos adaptáveis é um contêiner para todas as representações de vídeo necessárias para reproduzir o vídeo de forma contínua em várias telas. Um Conjunto de vídeos adaptáveis agrupa versões do mesmo vídeo que são codificadas em diferentes taxas de bits e formatos, como 400 kbps, 800 kbps e 1000 kbps. Você usa um conjunto de vídeos adaptáveis, juntamente com o componente de vídeo do S7, para transmitir vídeo adaptável em vários tipos de telas, incluindo telas de computadores, e dispositivos móveis com iOS, Android, Blackberry e Windows. Consulte [a documentação do Dynamic Media Classic sobre conjuntos de vídeo adaptáveis para obter mais informações](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/video/quick-start-video.html#video).

## Sobre o FFMPEG e o Dynamic Media Classic {#about-ffmpeg-and-scene}

O processo de codificação de vídeo padrão se baseia no uso da integração em FFMPEG com perfis de vídeo. Portanto, o fluxo de trabalho predefinido [!UICONTROL Ativo de atualização do DAM] contém as duas etapas de fluxo de trabalho baseadas em ffmpeg a seguir:

* Miniaturas de FFMPEG
* Codificação FFMPEG

Lembre-se de que ativar e configurar a integração do Dynamic Media Classic não remove ou desativa automaticamente essas duas etapas do fluxo de trabalho do fluxo de trabalho de inclusão [!UICONTROL DAM Update Asset] predefinido. Se você já usa a codificação de vídeo baseada em FFMPEG no AEM, é provável que tenha o FFMPEG instalado em seus ambientes de criação. Nesse caso, um novo vídeo assimilado usando Ativos seria codificado duas vezes: uma vez do codificador FFMPEG e uma vez da integração com o Dynamic Media Classic.

Se você tiver a codificação de vídeo baseada em FFMPEG em AEM configurada e FFMPEG instalada, o Adobe recomenda que você remova os dois workflows FFMPEG dos workflows [!UICONTROL DAM Update Asset].

### Formatos suportados {#supported-formats}

Os formatos a seguir são suportados pelo componente Vídeo clássico do Dynamic Media:

* F4V H.264
* MP4 H.264

### Como decidir onde fazer upload de seu vídeo {#deciding-where-to-upload-your-video}

Para decidir onde fazer upload de seus ativos de vídeo, considere o seguinte:

* O ativo de vídeo requer um fluxo de trabalho?
* O ativo de vídeo requer controle de versão?

Se a resposta for “sim” para ambas as perguntas, faça upload do vídeo diretamente no Adobe DAM. Se a resposta for &quot;não&quot; para ambas as perguntas, faça upload do vídeo diretamente para o Dynamic Media Classic. O fluxo de trabalho referente a cada cenário é descrito na próxima seção.

#### Se estiver fazendo upload do vídeo diretamente no Adobe Assets  {#if-you-are-uploading-your-video-directly-to-adobe-assets}

Se for necessário um fluxo de trabalho ou controle de versão para seus ativos, você deverá fazer upload primeiro no Adobe Assets. Este é o fluxo de trabalho recomendado:

1. Faça upload do ativo de vídeo para os ativos Adobe e codifique e publique automaticamente no Dynamic Media Classic.
1. No AEM, acesse os ativos de vídeo no WCM na guia **[!UICONTROL Filmes]** do Localizador de conteúdo.
1. Autor com vídeo do Dynamic Media Classic ou componente de vídeo de base.

#### Se você estiver carregando seu vídeo no Dynamic Media Classic {#if-you-are-uploading-your-video-to-scene}

Se você não precisar de um fluxo de trabalho ou controle de versão para seus ativos, faça upload dos ativos para o Dynamic Media Classic. Este é o fluxo de trabalho recomendado:

1. No aplicativo de desktop Dynamic Media Classic, [configure um carregamento e codificação FTP programados para o Dynamic Media Classic (sistema automatizado)](https://help.adobe.com/en_US/scene7/using/WS70B173EC-4CAD-4b4c-BF9C-43A11F3A5950.html).
1. No AEM, acesse ativos de vídeo no WCM na guia **[!UICONTROL Dynamic Media Classic]** do Localizador de conteúdo.
1. Autor com o componente de vídeo do Dynamic Media Classic.

### Configuração da integração com o Dynamic Media Classic Video {#configuring-integration-with-scene-video}

**Para configurar predefinições universais**:

1. Em **[!UICONTROL Cloud Services]**, navegue até a configuração **[!UICONTROL Dynamic Media Classic]** e clique em **[!UICONTROL Editar.]**
1. Selecione a guia **[!UICONTROL Vídeo]**.

   >[!NOTE]
   >
   >A guia **[!UICONTROL Vídeo]** não será exibida se a página não possuir uma configuração de nuvem. Consulte [Ativando o Dynamic Media Classic para WCM](#enablingscene7forwcm).

1. Selecione o perfil de codificação de vídeo adaptável, um perfil de codificação de vídeo pronto para uso ou um perfil de codificação de vídeo personalizado.

   >[!NOTE]
   >
   >Para obter mais informações sobre o que as predefinições de vídeo significam, consulte [Predefinições de vídeo para codificação de arquivos de vídeo](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/setup/application-setup.html?lang=en#video-presets-for-encoding-video-files).
   >
   >A Adobe recomenda selecionar ambos os conjuntos de vídeos adaptáveis ao configurar as predefinições universais ou selecionar a opção **[!UICONTROL Codificação de vídeo adaptável]**.

1. Os perfis de codificação selecionados são aplicados automaticamente a todos os vídeos carregados na pasta do público alvo CQ DAM que você configurou para esta configuração de nuvem do Dynamic Media Classic. Você pode configurar várias configurações de nuvem do Dynamic Media Classic com diferentes pastas de público alvo para aplicar diferentes perfis de codificação, conforme necessário.

### Atualizar as predefinições de codificação e do visualizador {#updating-viewer-and-encoding-presets}

Se você precisar atualizar o visualizador e as predefinições de codificação para vídeo no AEM porque as predefinições foram atualizadas no Dynamic Media Classic, navegue até a configuração do Dynamic Media Classic na configuração da nuvem e clique em **Atualizar o visualizador e as predefinições de codificação**.

![chlimage_1-131](assets/chlimage_1-131.png)

### Carregando seu vídeo de origem primária {#uploading-your-master-video}

Para carregar seu vídeo de origem primária no Dynamic Media Classic a partir do Adobe DAM:

1. Navegue até a pasta do público alvo CQ DAM na qual você configurou a configuração da nuvem com perfis de codificação do Dynamic Media Classic.
1. Clique em **[!UICONTROL Carregar]** para carregar o vídeo de origem primária. O upload e a codificação do vídeo são concluídos depois que o fluxo de trabalho [!UICONTROL DAM Update Asset] é concluído e **[!UICONTROL Publicar no Dynamic Media Classic]** tem uma marca de seleção.

   >[!NOTE]
   >
   >Pode levar algum tempo para gerar as miniaturas de vídeo.

   Arrastar o vídeo de origem primária do DAM para o componente de vídeo acessa *all* das renderizações de proxy codificadas do Dynamic Media Classic para o delivery.

### Componente de vídeo básico versus Componente de vídeo clássico do Dynamic Media {#foundation-video-component-versus-scene-video-component}

Ao usar o AEM, você tem acesso ao componente Vídeo disponível no Sites e ao componente de vídeo do Dynamic Media Classic. Esses componentes não são intercambiáveis.

O componente de vídeo do Dynamic Media Classic só funciona para vídeos do Dynamic Media Classic. O componente básico funciona com vídeos armazenados do AEM (usando o ffmpeg) e do Dynamic Media Classic.

A seguinte matriz explica quando você deve usar cada componente:

![chlimage_1-132](assets/chlimage_1-132.png)

>[!NOTE]
>
>O componente de vídeo do Dynamic Media Classic usa o perfil de vídeo universal. No entanto, você pode obter o player de vídeo baseado em HTML5 para uso pelo AEM. No Dynamic Media Classic, copie o código incorporado do player de vídeo HTML5 pronto para uso e coloque-o na página de AEM.


## Componente de vídeo do AEM {#aem-video-component}

Mesmo se o componente de vídeo do Dynamic Media Classic for recomendado para exibir vídeos do Dynamic Media Classic, esta seção descreve o uso de vídeos do Dynamic Media Classic com o [!UICONTROL Componente de vídeo do Foundation] no AEM, para fins de integridade.

### Comparação de vídeo AEM e vídeo do Dynamic Media Classic {#aem-video-and-scene-video-comparison}

A tabela a seguir fornece uma comparação de alto nível dos recursos suportados entre o componente AEM Foundation Video e o componente Dynamic Media Classic Video:

|  | Vídeo de base do AEM | Vídeo Dynamic Media Classic |
|---|---|---|
| Abordagem | Abordagem de HTML5 primeiro. O Flash é usado somente para o fallback não-HTML5. | Flash na maioria dos computadores. O HTML5 é usado para dispositivos móveis e tablets. |
| Entrega | Progressiva | Transmissão adaptável |
| Acompanhamento | Sim | Sim |
| Extensibilidade | Sim | Não |
| Vídeo móvel | Sim | Sim |

### Configuração  {#setting-up}

#### Criação de perfis de vídeo {#creating-video-profiles}

As várias codificações de vídeo são criadas de acordo com as predefinições de codificação do Dynamic Media Classic selecionadas na configuração da nuvem do Dynamic Media Classic. Para que o componente de vídeo de base os utilize, é necessário criar um perfil de vídeo para cada predefinição de codificação do Dynamic Media Classic selecionada. Isso permite que o componente de vídeo selecione as execuções de DAM apropriadas.

>[!NOTE]
>
>Os novos perfis de vídeo e as alterações a eles devem ser ativados para publicação.

1. No AEM, acesse as **[!UICONTROL Ferramentas]** e selecione o **[!UICONTROL Console de configuração.]** No console de configuração, navegue até  **[!UICONTROL Ferramentas]** >  **[!UICONTROL Ativos]** >  **[!UICONTROL Perfis de]** vídeo na árvore de navegação.
1. Crie um novo Perfil Dynamic Media Classic Video. No **[!UICONTROL Novo...]**, selecione **[!UICONTROL Criar página]** e selecione o modelo de Perfil de vídeo do Dynamic Media Classic. Forneça um nome para a nova página de perfil de vídeo e clique em **[!UICONTROL Criar.]**

   ![chlimage_1-135](assets/chlimage_1-133.png)

1. Edite o novo perfil de vídeo. Selecione primeiro a configuração de nuvem. Em seguida, selecione a mesma predefinição de codificação selecionada na configuração de nuvem.

   ![chlimage_1-134](assets/chlimage_1-134.png)

   | Propriedade | Descrição |
   |---|---|
   | Configuração da Dynamic Media Classic Cloud | A configuração da nuvem a ser usada para as predefinições de codificação. |
   | Dynamic Media Classic Encoding Preset | A predefinição de codificação para mapear este perfil de vídeo. |
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

1. Abra a caixa de diálogo de design do componente de vídeo de base e altere para a guia **[!UICONTROL Perfis]**. Em seguida, exclua os perfis predefinidos e adicione os novos perfis de vídeo do Dynamic Media Classic. A ordem da lista do perfil na caixa de diálogo de design também define a ordem do elemento de fontes de vídeo ao renderizar.
1. Para os navegadores que não oferecem suporte ao HTML5, o componente de vídeo permite configurar um fallback de flash. Abra a caixa de diálogo de design dos componentes de vídeo e altere para a guia **[!UICONTROL Flash]**. Ajuste as configurações do flash player e atribua um perfil de fallback a ele.

#### Lista de verificação  {#checklist}

1. Criar uma configuração de nuvem do Dynamic Media Classic. Verifique se as predefinições de codificação de vídeo estão definidas e se o importador está em execução.
1. Crie um perfil de vídeo do Dynamic Media Classic para cada predefinição de codificação de vídeo selecionada na configuração da nuvem.
1. Os perfis de vídeo devem ser ativados.
1. Configure o design do componente de vídeo de base na sua página.
1. Ative o design após finalizar as alterações no design.

