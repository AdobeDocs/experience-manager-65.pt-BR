---
title: Adicionar recursos do Dynamic Media Classic à sua página
description: Saiba como adicionar recursos e componentes do Dynamic Media Classic à sua página do AEM.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '2862'
ht-degree: 27%

---


# Adicionar recursos do Dynamic Media Classic à sua página {#adding-scene-features-to-your-page}

[O Adobe Dynamic Media Classic](https://help.adobe.com/en_US/scene7/using/WS26AB0D9A-F51C-464e-88C8-580A5A82F810.html) é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para Web, dispositivos móveis, email e telas e impressão conectadas à Internet.

Você pode visualização ativos AEM publicados no Dynamic Media Classic em vários visualizadores:

* Zoom
* Flyout
* Vídeo
* Modelo de imagem
* Imagem

Você pode publicar ativos digitais diretamente do AEM para o Dynamic Media Classic e pode publicar ativos digitais do Dynamic Media Classic para o AEM.

Este documento descreve como publicar ativos digitais do AEM para o Dynamic Media Classic e vice-versa. Os visualizadores também são descritos detalhadamente. Para obter informações sobre como configurar o AEM para Dynamic Media Classic, consulte [Integrar o Dynamic Media Classic ao AEM](/help/sites-administering/scene7.md).

Consulte também [Adição de mapas de imagem](image-maps.md).

For more information on using video components with AEM, see [Video](video.md).

>[!NOTE]
>
>If Dynamic Media Classic assets do not display properly, make sure that Dynamic media is [disabled](config-dynamic.md#disabling-dynamic-media) and then refresh the page.

## Publicar manualmente no Dynamic Media Classic a partir de ativos {#manually-publishing-to-scene-from-assets}

Você pode publicar ativos digitais no Dynamic Media Classic da seguinte maneira:

* [Na interface de usuário clássica do console Ativos](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Na interface de usuário clássica de um ativo](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Na interface de usuário clássica fora da pasta do Público alvo CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>O AEM publica no Dynamic Media Classic de forma assíncrona. After you click **[!UICONTROL Publish]**, it may take several seconds for your asset to publish to Dynamic Media Classic.


## Componentes do Dynamic Media Classic {#scene-components}

Os seguintes componentes do Dynamic Media Classic estão disponíveis no AEM:

* Zoom
* Flyout (Zoom)
* Modelo de imagem
* Imagem
* Vídeo

>[!NOTE]
>
>These components are not available by default and need to be selected in **[!UICONTROL Design]** mode before using.

After they are made available in **[!UICONTROL Design]** mode, you can add the components to your page like any other AEM component. Os ativos que ainda não foram publicados no Dynamic Media Classic são publicados no Dynamic Media Classic se estiverem em uma pasta sincronizada ou em uma página ou com uma configuração de nuvem do Dynamic Media Classic.

>[!NOTE]
>
>If you are creating and developing custom viewers and using the Content Finder, you need to explicity add the **[!UICONTROL allowfullscreen]** parameter.

### Aviso de fim de vida útil de visualizadores Flash {#flash-viewers-end-of-life-notice}

A partir de 31 de janeiro de 2017, o Adobe Dynamic Media Classic encerrou o suporte para a plataforma do visualizador Flash.

Para obter mais informações sobre essa alteração importante, consulte [Perguntas frequentes sobre o fim de vida útil do visualizador Flash](https://docs.adobe.com/content/docs/pt/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html).

### Adding a Dynamic Media Classic component (Scene7) to a page {#adding-a-scene-component-to-a-page}

Adicionar um componente do Dynamic Media Classic (Scene7) a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes do Dynamic Media Classic são descritos detalhadamente nas seções a seguir.

**Para adicionar um componente do Dynamic Media Classic (Scene7) a uma página**

1. No AEM, abra a página onde deseja adicionar o componente Dynamic Media Classic (Scene7).

1. Se nenhum componente do Dynamic Media Classic estiver disponível, clique em **[!UICONTROL Modo de design]** , toque em qualquer componente com uma borda azul, toque no ícone **[!UICONTROL Pai]** e no ícone **[!UICONTROL Configuração]** . Em **[!UICONTROL Parsys (Design)]**, selecione todos os componentes do Dynamic Media Classic para disponibilizá-los e clique em **[!UICONTROL OK.]**

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Clique em **[!UICONTROL Editar]** para retornar ao modo **[!UICONTROL Editar]** .

1. Arraste um componente do grupo do Dynamic Media Classic no sidekick para a página no local desejado.

1. Click the **[!UICONTROL Configuration]** icon to open the component.

1. Edite o componente conforme necessário e clique em **[!UICONTROL OK]** para salvar as alterações.
1. Arraste sua imagem ou vídeo do navegador de conteúdo até o componente Dynamic Media Classic que você adicionou à página.

   >[!NOTE]
   >
   >Somente na interface de usuário de toque, você deve arrastar e soltar a imagem ou o vídeo no componente do Dynamic Media Classic que você colocou na página. A seleção e edição do componente Dynamic Media Classic e a escolha do ativo não são suportadas.

### Adding interactive viewing experiences to a responsive site {#adding-interactive-viewing-experiences-to-a-responsive-website}

Design responsivo para seus ativos significa que eles se adaptam dependendo de onde são exibidos. Com o design responsivo, os mesmos ativos podem ser exibidos de maneira eficaz em diversos dispositivos.

Consulte também Design [responsivo para páginas](/help/sites-developing/responsive.md)da Web.

**Para adicionar uma experiência de visualização interativa a um site responsivo**

1. Log in to AEM, and ensure that you have [configured Adobe Dynamic Media Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) and that Dynamic Media Classic components are available.

   >[!NOTE]
   >
   >Se os componentes do Dynamic Media Classic não estiverem disponíveis, certifique-se [de ativá-los por meio do modo](/help/sites-authoring/default-components-designmode.md)Design.

1. In a website with the **[!UICONTROL Dynamic Media Classic]** components enabled, drag an **[!UICONTROL Image]** component to the page.
1. Selecione o componente e toque no ícone de configuração.
1. Na guia Configurações **[!UICONTROL do]** Dynamic Media Classic, ajuste os pontos de interrupção.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Verifique se os visualizadores estão sendo redimensionados de maneira adequada e de que todas as interações sejam otimizadas para desktop, tablet e dispositivo móvel.

### Configurações comuns a todos os componentes do Dynamic Media Classic {#settings-common-to-all-scene-components}

Although configuration options vary, the following are common to all [!UICONTROL Dynamic Media Classic] components:

* **[!UICONTROL Referência]** de arquivo - Navegue até um arquivo que deseja referenciar. A referência de arquivo mostra o URL do ativo e não necessariamente o URL completo do Dynamic Media Classic, incluindo os comandos e parâmetros do URL. Não é possível adicionar comandos e parâmetros de URL do Dynamic Media Classic neste campo. Eles devem ser adicionados por meio da funcionalidade correspondente no componente.
* **[!UICONTROL Largura]** - Permite definir a largura.
* **[!UICONTROL Altura]** - Permite definir a altura.

You set these configuration options by opening (double-clicking) a Dynamic Media Classic component, for example, when you open a **[!UICONTROL Zoom]** component:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

The HTML5 Zoom component displays a larger image when you press the **[!UICONTROL +]** button.

O ativo tem ferramentas de zoom na parte inferior. Toque em **[!UICONTROL +]** para ampliar. Toque **[!UICONTROL -]** para reduzir. Tapping the **[!UICONTROL x]** or the reset zoom arrow brings the image back to the original size it was imported as. Toque nas setas diagonais para torná-las em tela cheia. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all [!UICONTROL Dynamic Media Classic] components](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flyout {#flyout}

In the HTML5 **[!UICONTROL Flyout]** component, the asset is shown as split screen; left the asset in the specified size; right the zoom portion is displayed. Tap **[!UICONTROL Edit]** to configure the component. With this component, you can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components).

>[!NOTE]
>
>If your **[!UICONTROL Flyout]** component uses a custom size, then that custom size is used and responsive setup of the component is disabled.
>
>If your **[!UICONTROL Flyout]** component uses the default size, as set in the **[!UICONTROL Design View]**, then the default size is used and the component stretches to accomodate the page layout size with responsive setup of the component enabled. Esteja ciente, no entanto, de que há uma limitação na configuração responsiva do componente. When the you use the **[!UICONTROL Flyout]** component with responsive setup, you should not use it with full page stretch. Otherwise, the **[!UICONTROL Flyout]** may extend beyond the page&#39;s right border.

![chlimage_1-228](assets/chlimage_1-228.png)

### Imagem {#image}

O componente **[!UICONTROL Imagem]** clássica do Dynamic Media permite que você adicione a funcionalidade do Dynamic Media Classic às suas imagens, como modificadores do Dynamic Media Classic, predefinições de imagens ou visualizadores e nitidez. O componente **[!UICONTROL Imagem]** clássica do Dynamic Media é semelhante a outros componentes de imagem no AEM com funcionalidade especial do Dynamic Media Classic. Neste exemplo, a imagem tem o modificador de URL do Dynamic Media Classic, `&op_invert=1` aplicado.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Título, Texto]** alternativo - Na guia **[!UICONTROL Avançado]** , adicione um título à imagem e ao texto alternativo para os usuários que tiverem gráficos desativados.

**[!UICONTROL URL, Abrir]** - você pode definir um ativo de para abrir um link. Defina o **[!UICONTROL URL]** e, em **[!UICONTROL Abrir em]**, indique se você deseja que ele abra na mesma janela ou em uma nova.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Predefinição]** do visualizador - selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição de visualizador que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md). Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Configuração]** do Dynamic Media Classic - selecione a configuração do Dynamic Media Classic que deseja usar para buscar predefinições de imagens ativas do SPS.

**[!UICONTROL Predefinição]** de imagem - selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, pode ser necessário torná-la visível. Consulte [Gerenciar predefinições de imagens](/help/assets/managing-image-presets.md). Não é possível selecionar uma predefinição de visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Formato]** de saída - Selecione o formato de saída da imagem, por exemplo jpeg. Dependendo do formato de saída selecionado, você pode ter opções de configuração adicionais. Consulte [Práticas recomendadas de predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Nitidez]** - Selecione como deseja tornar a imagem nítida. A nitidez é explicada detalhadamente em [Práticas recomendadas da predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options) e [Práticas recomendadas de nitidez](/help/assets/assets/s7_sharpening_images.pdf).

**[!UICONTROL Modificadores]** de URL - você pode alterar os efeitos de imagem fornecendo comandos de imagem adicionais do Dynamic Media Classic. Eles estão descritos em [Predefinições de imagem](/help/assets/managing-image-presets.md) e na [Referência de comandos](https://docs.adobe.com/content/help/en/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Pontos de interrupção]** - se o site estiver respondendo, você deseja ajustar os pontos de interrupção. Os pontos de interrupção devem ser separados por vírgulas ( , ).

### Modelo de imagem {#image-template}

[Modelos](https://docs.adobe.com/help/en/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) de imagem do Dynamic Media Classic são conteúdo em camadas do Photoshop importado para o Dynamic Media Classic, onde o conteúdo e as propriedades foram parametrizados para variabilidade. O componente do **[!UICONTROL Modelo de imagem]** permite importar imagens e alterar dinamicamente o texto no AEM. Além disso, é possível configurar o componente do **[!UICONTROL Modelo de imagem]** para usar valores do contexto de cliente, de modo que cada usuário experiencie a imagem de uma maneira personalizada.

Tap **[!UICONTROL Edit]** to configure the component. You can configure [settings common to all Dynamic Media Classic components](#settings-common-to-all-scene-components) as well as other settings described in this section.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Referência de arquivo, Largura, Altura]** - Consulte as configurações comuns a todos os componentes do ScDynamic Media Classicene7.

>[!NOTE]
>
>Os parâmetros e comandos do URL do Dynamic Media Classic não podem ser adicionados diretamente ao URL de referência de arquivo. Eles podem ser definidos somente na interface do componente no painel **[!UICONTROL Parâmetro]**.

**[!UICONTROL Título, Texto]** alternativo - na guia Modelo de imagem clássica do Dynamic Media, adicione um título à imagem e ao texto alternativo para os usuários que tiverem gráficos desativados.

**[!UICONTROL URL, Abrir]** - você pode definir um ativo de para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Painel]** de parâmetros - ao importar uma imagem, os parâmetros são pré-preenchidos com informações da imagem. Caso nenhum conteúdo possa ser alterado dinamicamente, essa janela fica vazia.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Alterar o texto dinamicamente {#changing-text-dynamically}

Para alterar o texto dinamicamente, insira o novo texto nos campos e clique em **[!UICONTROL OK.]** Neste exemplo, o **[!UICONTROL Preço]** agora é $50 e o frete é de 99 centavos de dólar.

![chlimage_1-234](assets/chlimage_1-234.png)

O texto na imagem é alterado. You can reset the text back to the original value by tapping **[!UICONTROL Reset]** next to the field.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Alterar o texto para refletir o valor de contexto do cliente {#changing-text-to-reflect-the-value-of-a-client-context-value}

To link a field to a client context value, tap **[!UICONTROL Select]** to open the client-context menu, select the client context, and tap **[!UICONTROL OK.]** Neste exemplo, o nome é alterado com base na vinculação do Nome com o nome formatado no perfil.

![chlimage_1-236](assets/chlimage_1-236.png)

O texto reflete o nome do cliente conectado no momento. É possível redefinir o texto de volta para o valor original ao clicar em **[!UICONTROL Redefinir]** próximo ao campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Como tornar o modelo de imagem do Dynamic Media Classic um link {#making-the-scene-image-template-a-link}

1. Na página com o componente Modelo **[!UICONTROL de]** imagem do Dynamic Media Classic, toque em **[!UICONTROL Editar.]**
1. In the **[!UICONTROL URL]** field, enter the URL that users go to when the image is tapped. No campo **[!UICONTROL Abrir em]**, selecione se deseja onde o destino seja aberto (uma nova janela ou na mesma).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Toque em **[!UICONTROL OK.]**

### Componente de vídeo {#video-component}

The Dynamic Media Classic **[!UICONTROL Video]** component (available from the Dynamic Media Classic section of the sidekick) uses device and bandwidth detection to serve the right video to each screen. Este componente é um reprodutor de vídeo HTML5; é um visualizador único que pode ser usado em todos os canais.

Ele pode ser usado pra conjuntos de vídeos adaptáveis, um único vídeo MP4 ou um único vídeo F4V.

See [Video](s7-video.md) for more information on how videos work with Dynamic Media Classic integration. Além disso, consulte [o componente Dynamic Media Classic Video versus o componente](s7-video.md)Foundation Video.

![chlimage_1-239](assets/chlimage_1-239.png)

### Restrições conhecidas do componente de vídeo {#known-limitations-for-the-video-component}

O Adobe DAM e o WCM mostram se um vídeo de origem primária foi carregado. Eles não mostram os ativos de proxy a seguir:

* Execuções codificadas do Dynamic Media Classic
* Conjuntos de vídeo adaptativos Dynamic Media Classic

Ao usar um conjunto de vídeo adaptável com o componente de vídeo Dynamic Media Classic, é necessário redimensionar o componente para ajustar às dimensões do vídeo.

## Navegador de conteúdo do Dynamic Media Classic {#scene-content-browser}

O navegador de conteúdo do Dynamic Media Classic permite que você visualização conteúdo do Dynamic Media Classic diretamente no AEM. To access the content browser, in the **[!UICONTROL Content Finder]**, select **[!UICONTROL Dynamic Media Classic]** in the touch-optimized user interface or the **[!UICONTROL S7]** icon in the classic user interface. A funcionalidade é idêntica em ambas as interfaces do usuário.

Caso tenha diversas configurações, o AEM exibe, por padrão, a [configuração padrão](/help/sites-administering/scene7.md#configuring-a-default-configuration). Você pode selecionar configurações diferentes diretamente no navegador de conteúdo do Dynamic Media Classic no menu suspenso.

>[!NOTE]
>
>* Os ativos localizados na pasta ad-hoc não aparecerão no navegador de conteúdo do Dynamic Media Classic.
>* Quando a Pré-visualização [segura está ativada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), os ativos publicados e não publicados no Dynamic Media Classic são exibidos no navegador de conteúdo do Dynamic Media Classic.
>* If you do not see **[!UICONTROL Dynamic Media Classic]** or the **[!UICONTROL S7]** icon as an option in the content browser, you need to [configure Dynamic Media Classic to work with AEM](/help/sites-administering/scene7.md).
>* Para vídeo, o navegador de conteúdo do Dynamic Media Classic é compatível:

   >
   >   
   * Conjuntos de vídeos adaptáveis: contêiner de todas as representações de vídeo necessárias para uma reprodução perfeita em diversas telas
   >   * Vídeo MP4 único
   >   * Vídeo F4V único


### Browsing content in the touch-optimized UI {#browsing-content-in-the-touch-optimized-ui}

Você pode acessar o navegador de conteúdo na interface otimizada ao toque ou clássica. Atualmente, a interface otimizada para toque tem a seguinte limitação:

* Os ativos FXG e Flash do Dynamic Media Classic não são suportados.

Navegue pelos ativos do Dynamic Media Classic selecionando **[!UICONTROL Dynamic Media Classic]** no terceiro menu suspenso. O Dynamic Media Classic não será exibido na lista se você não tiver configurado a integração do Dynamic Media Classic/AEM.

>[!NOTE]
>
>* O navegador de conteúdo do Dynamic Media Classic carrega cerca de 100 ativos e os classifica pelo nome.
>* Se você tiver um servidor de pré-visualização seguro definido, o navegador usará esse servidor de pré-visualização para renderizar miniaturas e ativos.

>



![chlimage_1-240](assets/chlimage_1-240.png)

Além disso, você pode navegar pelas informações de resolução, tamanho, dias desde a modificação e nome do arquivo passando o mouse sobre o ativo no navegador.

![chlimage_1-241](assets/chlimage_1-241.png)

* Para conjuntos e modelos de vídeo adaptáveis, nenhuma informação de tamanho é gerada para miniaturas.
* Para Conjuntos de vídeos adaptáveis, nenhuma resolução é gerada para miniaturas.

### Como pesquisar ativos do Dynamic Media Classic com o navegador de conteúdo {#searching-for-scene-assets-with-the-content-browser}

Pesquisar ativos do Dynamic Media Classic é semelhante a pesquisar ativos do AEM, exceto que quando você pesquisa, você está vendo uma visualização remota dos ativos no sistema Dynamic Media Classic, em vez de importá-los diretamente para o AEM.

É possível usar a interface do usuário clássica ou a otimizada para toque para visualizar e pesquisar ativos. Dependendo da interface, a maneira como você pesquisa é levemente diferente.

Ao pesquisar em qualquer uma das interfaces de usuário, você pode filtrar pelos seguintes critérios (mostrados aqui na interface otimizada para toque):

**[!UICONTROL Digite palavras-chave]** - você pode pesquisar ativos por nome. Ao pesquisar, as palavras-chave inseridas corresponderão às palavras com as quais o nome de arquivo come. Por exemplo, digitar a palavra “nadar” pesquisaria todos os nomes de arquivo de ativo que comecem com as letras nessa ordem. Pressione Enter depois de digitar o termo para localizar o ativo.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Pasta/caminho]** - O nome da pasta que aparece é baseado na configuração selecionada. Você pode fazer o detalhamento para níveis inferiores tocando no ícone de pasta e selecionando uma subpasta e tocando na marca de seleção para selecioná-la.

Se você inserir uma palavra-chave e selecionar uma pasta, o AEM procura nessa pasta e em todas as subpastas. No entanto, se você não digitar nenhuma palavra-chave ao pesquisar, selecionar a pasta exibirá somente os ativos nessa pasta e não incluirá nenhuma subpasta.

Por padrão, o AEM procura na pasta selecionada e em todas as subpastas.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo de ativo]** - selecione **[!UICONTROL Dynamic Media Classic]** para navegar pelo conteúdo do Dynamic Media Classic. Essa opção só estará disponível se o Dynamic Media Classic tiver sido configurado.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuração]** - se você tiver mais de uma configuração do Dynamic Media Classic definida no [!UICONTROL Cloud Service], poderá selecioná-la aqui. Como resultado, a pasta será alterada com base na configuração escolhida.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo]** de ativo - No navegador Dynamic Media Classic, você pode filtrar os resultados para incluir qualquer um dos seguintes: imagens, modelos, vídeos e conjuntos de vídeo adaptáveis. Se você não selecionar nenhum tipo de ativo, o AEM procura todos os tipos de ativo por padrão.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Na interface do usuário clássica, também é possível procurar pelo **Flash** e pelo **FXG**. A filtragem para eles na interface otimizada para toque não é compatível atualmente.
   >
   >
* Ao pesquisar por vídeo, você estará procurando uma única representação. Os resultados retornam a execução original (somente &amp;ast;.mp4) e a execução codificada.
>* Ao pesquisar um conjunto de vídeos adaptáveis, você está pesquisando a pasta e todas as subpastas, mas somente se tiver adicionado uma palavra-chave à pesquisa. Caso não tenha adicionado uma palavra-chave, o AEM não pesquisará nas subpastas.

>



**[!UICONTROL Status]** da publicação - você pode filtrar ativos com base no status da publicação: **[!UICONTROL Não publicado]** ou **[!UICONTROL publicado.]** Se você não selecionar nenhum Status **[!UICONTROL de]** publicação, o AEM, por padrão, pesquisará todos os status de publicação.

![chlimage_1-247](assets/chlimage_1-247.png)

