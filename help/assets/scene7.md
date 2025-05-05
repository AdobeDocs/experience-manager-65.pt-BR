---
title: Adicionar recursos do Dynamic Media Classic às páginas
description: Como adicionar recursos e componentes do Dynamic Media Classic a uma página no Adobe Experience Manager.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
feature: Dynamic Media Classic
role: User, Admin
mini-toc-levels: 3
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2851'
ht-degree: 0%

---

# Adicionar recursos do Dynamic Media Classic às páginas {#adding-scene-features-to-your-page}

O [Adobe Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=pt-BR) é uma solução hospedada para gerenciamento, aprimoramento, publicação e fornecimento de ativos de mídia avançada para Web, dispositivos móveis, email e exibições e impressões conectadas à Internet.

Você pode visualizar ativos do Experience Manager publicados no Dynamic Media Classic em vários visualizadores:

* Zoom
* Flyout
* Vídeo
* Modelo da imagem
* Imagem

Você pode publicar ativos digitais diretamente do Experience Manager para o Dynamic Media Classic e também do Dynamic Media Classic para o Experience Manager.

Este documento descreve como publicar ativos digitais do Experience Manager para o Dynamic Media Classic e vice-versa. Os visualizadores também são descritos em detalhes. Para obter informações sobre como configurar o Experience Manager para o Dynamic Media Classic, consulte [Integrar o Dynamic Media Classic com o Experience Manager](/help/sites-administering/scene7.md).

Consulte também [Adicionar mapas de imagem](image-maps.md).

Para obter mais informações sobre o uso de componentes de vídeo com o Experience Manager, consulte [Vídeo](video.md).

>[!NOTE]
>
>Se os ativos do Dynamic Media Classic não forem exibidos corretamente, verifique se o Dynamic Media está [desabilitado](config-dynamic.md#disabling-dynamic-media) e atualize a página.

## Publicar manualmente no Dynamic Media Classic a partir de ativos {#manually-publishing-to-scene-from-assets}

Você pode publicar ativos digitais no Dynamic Media Classic da seguinte maneira:

* [Na interface de usuário clássica do console do Assets](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Na interface clássica do usuário de um ativo](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Na interface de usuário clássica fora da pasta do CQ Target](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>O Experience Manager publica no Dynamic Media Classic de forma assíncrona. Após selecionar **[!UICONTROL Publish]**, levará vários segundos para seu ativo ser publicado no Dynamic Media Classic.
>

## Componentes do Dynamic Media Classic {#scene-components}

Os seguintes componentes do Dynamic Media Classic estão disponíveis no Experience Manager:

* Zoom
* Submenu (Zoom)
* Modelo da imagem
* Imagem
* Vídeo

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser selecionados no modo **[!UICONTROL Design]** antes de usar.

Depois que eles forem disponibilizados no modo **[!UICONTROL Design]**, você poderá adicionar os componentes à sua página como qualquer outro componente de Experience Manager. Os Assets que ainda não foram publicados no Dynamic Media Classic são publicados no Dynamic Media Classic se estiverem em uma pasta sincronizada ou em uma página ou com uma configuração de nuvem do Dynamic Media Classic.

>[!NOTE]
>
>Se você estiver criando e desenvolvendo visualizadores personalizados e estiver usando o Localizador de Conteúdo, será necessário adicionar explicitamente o parâmetro `allowfullscreen`.

### Aviso de fim de vida útil de visualizadores do Flash {#flash-viewers-end-of-life-notice}

A partir de 31 de janeiro de 2017, a Adobe Dynamic Media Classic encerrou o suporte à plataforma de visualizador de Flashes.

### Adicionar um componente do Dynamic Media Classic (Scene7) a uma página {#adding-a-scene-component-to-a-page}

Adicionar um componente do Dynamic Media Classic (Scene7) a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes do Dynamic Media Classic são descritos detalhadamente nas seções a seguir.

**Para adicionar um componente do Dynamic Media Classic (Scene7) a uma página:**

1. No Experience Manager, abra a página em que deseja adicionar o componente **[!UICONTROL Dynamic Media Classic (Scene7)]**.

1. Se nenhum componente do Dynamic Media Classic estiver disponível, selecione o modo **[!UICONTROL Design]**, selecione qualquer componente com uma borda azul, selecione o ícone **[!UICONTROL Pai]** e depois o ícone **[!UICONTROL Configuração]**. Em **[!UICONTROL Parsys (Design)]**, selecione todos os componentes do Dynamic Media Classic para torná-los disponíveis e selecione **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Selecione **[!UICONTROL Editar]** para retornar ao modo **[!UICONTROL Editar]**.

1. Arraste um componente do grupo Dynamic Media Classic no sidekick para a página no local desejado.

1. Selecione o ícone **[!UICONTROL Configuração]** para poder abrir o componente.

1. Edite o componente conforme necessário e selecione **[!UICONTROL OK]** para salvar as alterações.
1. Arraste a imagem ou o vídeo do navegador de conteúdo para o componente Dynamic Media Classic adicionado à página.

   >[!NOTE]
   >
   >Somente na interface para toque, você deve arrastar e soltar a imagem ou o vídeo no componente do Dynamic Media Classic inserido na página. Não há suporte para selecionar e editar o componente Dynamic Media Classic e depois escolher o ativo.

### Adicionar uma experiência de visualização interativa a um site responsivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

O design responsivo para seus ativos significa que seu ativo se adapta dependendo de onde é exibido. Com um design responsivo, os mesmos ativos podem ser exibidos de maneira eficaz em vários dispositivos.

Consulte também [Design responsivo para páginas da Web](/help/sites-developing/responsive.md).

**Para adicionar uma experiência de exibição interativa a um site responsivo:**

1. Faça logon no Experience Manager e verifique se você tem o [Adobe Dynamic Media Classic Cloud Service](/help/sites-administering/scene7.md#configuring-scene-integration) configurado e se os componentes do Dynamic Media Classic estão disponíveis.

   >[!NOTE]
   >
   >Se os componentes do Dynamic Media Classic não estiverem disponíveis, [habilite-os por meio do Modo de design](/help/sites-authoring/default-components-designmode.md).

1. Em um site com os componentes **[!UICONTROL Dynamic Media Classic]** habilitados, arraste um componente **[!UICONTROL Image]** para a página.
1. Selecione o componente e selecione o ícone de configuração.
1. Na guia **[!UICONTROL Configurações do Dynamic Media Classic]**, ajuste os pontos de interrupção.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Confirme se os visualizadores estão redimensionando com agilidade e se todas as interações estão otimizadas para desktop, tablet e dispositivos móveis.

### Configurações comuns a todos os componentes do Dynamic Media Classic {#settings-common-to-all-scene-components}

Embora as opções de configuração variem, as seguintes opções são comuns a todos os componentes do [!UICONTROL Dynamic Media Classic]:

* **[!UICONTROL Referência de arquivo]** - Procure um arquivo que você deseja referenciar. A referência de arquivo mostra o URL do ativo e não necessariamente o URL completo do Dynamic Media Classic, incluindo os comandos e parâmetros do URL. Não é possível adicionar comandos e parâmetros de URL do Dynamic Media Classic neste campo. Em vez disso, você as adiciona por meio da funcionalidade correspondente no componente.
* **[!UICONTROL Largura]** - Permite definir a largura.
* **[!UICONTROL Altura]** - Permite definir a altura.

Você define estas opções de configuração abrindo (clicando duas vezes) um componente do Dynamic Media Classic, por exemplo, quando você abre um componente **[!UICONTROL Zoom]**:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

O componente de HTML5 Zoom exibe uma imagem maior quando você pressiona o botão **[!UICONTROL +]**.

O ativo tem ferramentas de zoom na parte inferior. Selecione **[!UICONTROL +]** se quiser ampliar; selecione **[!UICONTROL -]** se quiser reduzir. Tocar em **[!UICONTROL x]** ou na seta de redefinição de zoom traz a imagem de volta ao tamanho original como foi importada. Selecione as setas diagonais para usá-las em tela cheia. Selecione **[!UICONTROL Editar]** para poder configurar o componente. Com este componente, você pode definir [configurações comuns a todos os [!UICONTROL componentes do Dynamic Media Classic]](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flyout {#flyout}

No componente HTML5 **[!UICONTROL Flyout]**, o ativo é exibido como tela dividida; deixa o ativo no tamanho especificado; à direita, é exibida a parte de zoom. Selecione **[!UICONTROL Editar]** para poder configurar o componente. Com este componente, você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Se o componente **[!UICONTROL Submenu]** usar um tamanho personalizado, esse tamanho personalizado será usado e a configuração responsiva do componente será desabilitada.
>
>Se o componente **[!UICONTROL Submenu]** usar o tamanho padrão, conforme definido em **[!UICONTROL Modo de Exibição de Design]**, o tamanho padrão será usado e o componente será estendido para acomodar o tamanho do layout da página com a configuração responsiva do componente habilitada. Há uma limitação na configuração responsiva do componente. Ao usar o componente **[!UICONTROL Flyout]** com configuração responsiva, não o use com ampliação de página inteira. Caso contrário, o **[!UICONTROL Flyout]** se estenderá além da borda direita da página.

![chlimage_1-228](assets/chlimage_1-228.png)

### Imagem {#image}

O componente **[!UICONTROL Imagem]** do Dynamic Media Classic permite adicionar a funcionalidade Dynamic Media Classic às suas imagens, como modificadores Dynamic Media Classic, predefinições de imagens ou visualizadores e nitidez. O componente **[!UICONTROL Imagem]** do Dynamic Media Classic é semelhante a outros componentes de imagem no Experience Manager com funcionalidade especial do Dynamic Media Classic. Neste exemplo, a imagem tem o modificador de URL do Dynamic Media Classic, `&op_invert=1` aplicado.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Título, Texto Alternativo]** - Na guia **[!UICONTROL Avançado]**, adicione um título à imagem e um texto alternativo para os usuários que têm gráficos desativados.

**[!UICONTROL URL, Abrir em]** - Você pode definir um ativo de para abrir um link. Defina o **[!UICONTROL URL]** e em **[!UICONTROL Abrir em]** indique se você deseja que ele seja aberto na mesma janela ou em uma nova janela.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Predefinição do visualizador]** - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Configuração do Dynamic Media Classic]** - Selecione a configuração do Dynamic Media Classic que deseja usar para buscar predefinições de imagens ativas do SPS.

**[!UICONTROL Predefinição de imagem]** - Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, será necessário torná-la visível. Consulte [Gerenciar predefinições de imagem](/help/assets/managing-image-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Formato de saída]** - Selecione o formato de saída da imagem, por exemplo, jpeg. Dependendo do formato de saída selecionado, há opções de configuração adicionais. Consulte [Práticas recomendadas de predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Nitidez]** - Selecione como deseja nitidez da imagem. A nitidez é explicada detalhadamente nas [Práticas recomendadas de predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options) e [Práticas recomendadas de nitidez](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL Modificadores de URL]** - Você pode alterar efeitos de imagem fornecendo comandos de imagem Dynamic Media Classic adicionais. Estes comandos estão descritos em [Predefinições de imagem](/help/assets/managing-image-presets.md) e na [Referência de comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Pontos de interrupção]** - Se o site for responsivo, ajuste os pontos de interrupção. Os pontos de interrupção devem ser separados por vírgulas ( , ).

### Modelo da imagem {#image-template}

[Modelos de imagem do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) são conteúdos em camadas do Photoshop que foram importados para o Dynamic Media Classic, onde o conteúdo e as propriedades foram parametrizados para fins de variabilidade. O componente **[!UICONTROL Modelo de imagem]** permite importar imagens e alterar o texto dinamicamente no Experience Manager. Além disso, você pode configurar o componente **[!UICONTROL Modelo de imagem]** para usar valores do contexto do cliente, para que cada usuário experimente a imagem de forma personalizada.

Selecione **[!UICONTROL Editar]** se desejar configurar o componente. Você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic](#settings-common-to-all-scene-components) e outras configurações descritas nesta seção.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Referência de arquivo, Largura, Altura]** - Consulte as configurações comuns a todos os componentes do ScDynamic Media Classicene7.

>[!NOTE]
>
>Os comandos e parâmetros de URL do Dynamic Media Classic não podem ser adicionados diretamente ao URL de referência de arquivo. Eles só podem ser definidos na interface do usuário do componente no painel **[!UICONTROL Parâmetro]**.

**[!UICONTROL Título, Texto Alternativo]** - Na guia Modelo de Imagem do Dynamic Media Classic, adicione um título à imagem e um texto alternativo para os usuários que têm gráficos desativados.

**[!UICONTROL URL, Abrir em]** - Você pode definir um ativo de para abrir um link. Defina o URL e, em Abrir no, indique se deseja abri-lo na mesma janela ou em uma nova janela.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Painel de Parâmetros]** - Ao importar uma imagem, os parâmetros são pré-preenchidos com informações da imagem. Se não houver conteúdo que possa ser alterado dinamicamente, essa janela ficará vazia.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Alterar texto dinamicamente {#changing-text-dynamically}

Para alterar o texto dinamicamente, insira um novo texto nos campos e selecione **[!UICONTROL OK]**. Neste exemplo, o **[!UICONTROL Preço]** agora é de $50 e o frete é de 99 centavos.

![chlimage_1-234](assets/chlimage_1-234.png)

O texto na imagem é alterado. Você pode redefinir o texto para o valor original tocando em **[!UICONTROL Redefinir]** ao lado do campo.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Alterar texto para refletir o valor de um valor de contexto do cliente {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular um campo a um valor de contexto de cliente, selecione **[!UICONTROL Selecionar]** para abrir o menu de contexto de cliente, selecione o contexto de cliente e selecione **[!UICONTROL OK]**. Neste exemplo, o nome muda com base na vinculação do Name com o nome formatado no perfil.

![chlimage_1-236](assets/chlimage_1-236.png)

O texto reflete o nome do usuário conectado no momento. Você pode redefinir o texto para o valor original clicando em **[!UICONTROL Redefinir]** ao lado do campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Transforme o modelo de imagem do Dynamic Media Classic em um link {#making-the-scene-image-template-a-link}

1. Na página com o componente **[!UICONTROL Modelo de imagem]** do Dynamic Media Classic, selecione **[!UICONTROL Editar]**.
1. No campo **[!UICONTROL URL]**, insira a URL para a qual os usuários vão quando a imagem é tocada. No campo **[!UICONTROL Abrir em]**, selecione se deseja abrir o destino (uma nova janela ou a mesma janela).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Selecione **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

O componente de **[!UICONTROL Vídeo]** do Dynamic Media Classic (disponível na seção Dynamic Media Classic do sidekick) usa detecção de dispositivo e largura de banda para veicular o vídeo correto em cada tela. Esse componente é um reprodutor de vídeo HTML5; é um único visualizador que pode ser usado entre canais.

Ele pode ser usado para conjuntos de vídeos adaptáveis, um único vídeo MP4 ou um único vídeo F4V.

Consulte [Vídeo](s7-video.md) para obter mais informações sobre como os vídeos funcionam com a integração do Dynamic Media Classic. Além disso, consulte [o componente de Vídeo do Dynamic Media Classic versus o componente de Vídeo do Foundation](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Limitações conhecidas do componente de vídeo {#known-limitations-for-the-video-component}

O DAM do Adobe e o WCM mostram se um vídeo de origem primária foi carregado. Eles não mostram esses ativos proxy:

* Representações codificadas do Dynamic Media Classic
* Conjuntos de vídeo adaptável do Dynamic Media Classic

Ao usar um conjunto de vídeos adaptáveis com o componente de vídeo do Dynamic Media Classic, você deve redimensionar o componente para ajustá-lo às dimensões do vídeo.

## Navegador de conteúdo do Dynamic Media Classic {#scene-content-browser}

O navegador de conteúdo do Dynamic Media Classic permite exibir o conteúdo do Dynamic Media Classic diretamente no Experience Manager. Para acessar o navegador de conteúdo, no **[!UICONTROL Localizador de Conteúdo]**, selecione **[!UICONTROL Dynamic Media Classic]** na interface de usuário otimizada para toque ou o ícone **[!UICONTROL S7]** na interface de usuário clássica. A funcionalidade é idêntica entre as duas interfaces do usuário.

Se você tiver várias configurações, o Experience Manager, por padrão, exibe a [configuração padrão](/help/sites-administering/scene7.md#configuring-a-default-configuration). Você pode selecionar configurações diferentes diretamente no navegador de conteúdo do Dynamic Media Classic no menu suspenso.

>[!NOTE]
>
>* O Assets na pasta on-demand não aparece no navegador de conteúdo do Dynamic Media Classic.
>* Quando a [Visualização Segura está habilitada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), tanto os ativos publicados quanto os não publicados no Dynamic Media Classic aparecem no navegador de conteúdo do Dynamic Media Classic.
>* Se você não vir o ícone **[!UICONTROL Dynamic Media Classic]** ou **[!UICONTROL S7]** como uma opção no navegador de conteúdo, deverá [configurar o Dynamic Media Classic para funcionar com o Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, o navegador de conteúdo do Dynamic Media Classic é compatível com:
>
>   * Conjuntos de vídeos adaptados: contêiner de todas as representações de vídeo necessárias para a reprodução contínua em várias telas
>   * Vídeo MP4 único
>   * Vídeo F4V único

### Procurar conteúdo na interface otimizada para toque {#browsing-content-in-the-touch-optimized-ui}

Você pode acessar o navegador de conteúdo na interface otimizada para toque ou na interface clássica. Atualmente, o otimizado para toque tem a seguinte limitação:

* Os ativos FXG e Flash do Dynamic Media Classic não são compatíveis.

Procure ativos do Dynamic Media Classic selecionando **[!UICONTROL Dynamic Media Classic]** no terceiro menu suspenso. O Dynamic Media Classic não será exibido na lista se você não tiver configurado a integração Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* O navegador de conteúdo do Dynamic Media Classic carrega cerca de 100 ativos e os classifica por nome.
>* Se você tiver um servidor de visualização seguro definido, o navegador usará esse servidor de visualização para renderizar miniaturas e ativos.
>

![chlimage_1-240](assets/chlimage_1-240.png)

Além disso, você pode navegar pelas informações de resolução, tamanho, dias desde a modificação e nome do arquivo, passando o cursor do mouse sobre o ativo no navegador.

![chlimage_1-241](assets/chlimage_1-241.png)

* Para Conjuntos e modelos de vídeo adaptável, nenhuma informação de tamanho é gerada para miniaturas.
* Para Conjuntos de vídeos adaptados, nenhuma resolução é gerada para miniaturas.

### Pesquisar ativos do Dynamic Media Classic com o navegador de conteúdo {#searching-for-scene-assets-with-the-content-browser}

Pesquisar ativos no Dynamic Media Classic é semelhante à pesquisar ativos no Experience Manager Assets. No entanto, ao pesquisar, você está vendo uma visualização remota dos ativos no sistema Dynamic Media Classic, em vez de importá-los diretamente para o Experience Manager.

Você pode usar a interface clássica ou a interface otimizada para toque para visualizar e pesquisar ativos. Dependendo da interface, a forma como você pesquisa será um pouco diferente.

Ao pesquisar em qualquer uma das interfaces do usuário, você pode filtrar pelos seguintes critérios (mostrados aqui na interface otimizada para toque):

**[!UICONTROL Inserir palavras-chave]** - Você pode pesquisar ativos por nome. Ao pesquisar, as palavras-chave digitadas são aquelas com as quais o nome do arquivo começa. Por exemplo, digitar a palavra &quot;natação&quot; procuraria qualquer nome de arquivo de ativo que começasse com essas letras nessa ordem. Certifique-se de pressionar Enter depois de digitar o termo para localizar o ativo.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Pasta/caminho]** - O nome da pasta que é vista baseia-se na configuração selecionada. Você pode detalhar os níveis inferiores tocando no ícone de pasta e selecionando uma subpasta e, em seguida, tocando na marca de seleção para selecioná-la.

Se você inserir uma palavra-chave e selecionar uma pasta, o Experience Manager pesquisará essa pasta e todas as subpastas. No entanto, se você não inserir nenhuma palavra-chave ao pesquisar, selecionar a pasta mostrará apenas os ativos nessa pasta e não incluirá nenhuma subpasta.

Por padrão, o Experience Manager pesquisa a pasta selecionada e todas as subpastas.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo de ativo]** - Selecione **[!UICONTROL Dynamic Media Classic]** para procurar conteúdo do Dynamic Media Classic. Essa opção só estará disponível se o Dynamic Media Classic tiver sido configurado.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuração]** - Se você tiver mais de uma configuração Dynamic Media Classic definida em [!UICONTROL Cloud Service], selecione-a aqui. Como resultado, a pasta muda com base na configuração escolhida.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo de ativo]** - No navegador Dynamic Media Classic, você pode filtrar os resultados para incluir qualquer um dos seguintes itens: imagens, modelos, vídeos e conjuntos de vídeos adaptáveis. Se você não selecionar nenhum tipo de ativo, o Experience Manager, por padrão, pesquisa todos os tipos de ativos.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Na interface clássica, você também pode procurar por **Flash** e **FXG**. A filtragem desses tipos na interface otimizada para toque não é compatível.
>
>* Ao pesquisar vídeos, você pesquisa uma única representação. Os resultados retornam a representação original (somente &ast;.mp4) e a representação codificada.
>* Ao pesquisar um conjunto de vídeos adaptáveis, você pesquisa a pasta e todas as subpastas, mas somente se tiver adicionado uma palavra-chave à pesquisa. Se você não tiver adicionado uma palavra-chave, o Experience Manager não pesquisará nas subpastas.
>

**[!UICONTROL Status do Publish]** - Você pode filtrar por ativos com base no status da publicação: **[!UICONTROL Não publicado]** ou **[!UICONTROL Publicado]**. Se você não selecionar nenhum **[!UICONTROL Status do Publish]**, o Experience Manager, por padrão, pesquisará todos os status de publicação.

![chlimage_1-247](assets/chlimage_1-247.png)
