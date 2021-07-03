---
title: Adicionar recursos do Dynamic Media Classic à sua página
description: Saiba como adicionar recursos e componentes do Dynamic Media Classic à sua página do Adobe Experience Manager.
uuid: aa5a4735-bfec-43b8-aec0-a0c32bff134f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
topic-tags: managing-assets
discoiquuid: e7b95732-a571-48e8-afad-612059cdbde7
feature: Dynamic Media Classic
role: User, Admin
exl-id: 815f577d-4774-4830-8baf-0294bd085b83
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '2849'
ht-degree: 18%

---

# Adicionar recursos do Dynamic Media Classic à sua página {#adding-scene-features-to-your-page}

[O Adobe Dynamic Media ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html) Classic é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para Web, dispositivos móveis, email, impressão e monitores conectados à Internet.

Você pode visualizar ativos do Experience Manager publicados no Dynamic Media Classic em vários visualizadores:

* Zoom
* Flyout
* Vídeo
* Modelo de imagem
* Imagem

Você pode publicar ativos digitais diretamente do Experience Manager para o Dynamic Media Classic e publicar ativos digitais do Dynamic Media Classic para o Experience Manager.

Este documento descreve como publicar ativos digitais do Experience Manager para o Dynamic Media Classic e vice-versa. Os visualizadores também são descritos detalhadamente. Para obter informações sobre como configurar o Experience Manager para o Dynamic Media Classic, consulte [Integração do Dynamic Media Classic com o Experience Manager](/help/sites-administering/scene7.md).

Consulte também [Adição de mapas de imagem](image-maps.md).

Para obter mais informações sobre o uso de componentes de vídeo com Experience Manager, consulte [Vídeo](video.md).

>[!NOTE]
>
>Se os ativos do Dynamic Media Classic não forem exibidos corretamente, verifique se o Dynamic Media é [disabled](config-dynamic.md#disabling-dynamic-media) e atualize a página.

## Publicar manualmente no Dynamic Media Classic a partir de ativos {#manually-publishing-to-scene-from-assets}

Você pode publicar ativos digitais no Dynamic Media Classic da seguinte maneira:

* [Na interface do usuário clássica no console Assets](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-the-assets-console)
* [Na interface do usuário clássica de um ativo](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-from-an-asset)
* [Na interface do usuário clássica fora da pasta de destino CQ](/help/sites-classic-ui-authoring/manage-assets-classic-s7.md#publishing-assets-from-outside-the-cq-target-folder)

>[!NOTE]
>
>O Experience Manager publica no Dynamic Media Classic de forma assíncrona. Depois de clicar em **[!UICONTROL Publicar]**, leva vários segundos para que o ativo seja publicado no Dynamic Media Classic.


## Componentes do Dynamic Media Classic {#scene-components}

Os seguintes componentes do Dynamic Media Classic estão disponíveis no Experience Manager:

* Zoom
* Flyout (Zoom)
* Modelo de imagem
* Imagem
* Vídeo

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser selecionados no modo **[!UICONTROL Design]** antes de usar.

Depois que eles forem disponibilizados no modo **[!UICONTROL Design]**, você poderá adicionar os componentes à sua página como qualquer outro componente do Experience Manager. Os ativos que ainda não foram publicados no Dynamic Media Classic são publicados no Dynamic Media Classic se estiverem em uma pasta sincronizada ou em uma página ou com uma configuração de nuvem do Dynamic Media Classic.

>[!NOTE]
>
>Se você estiver criando e desenvolvendo visualizadores personalizados e usando o Localizador de conteúdo, deverá adicionar explicitamente o parâmetro `allowfullscreen`.

### Aviso de fim de vida útil de visualizadores Flash {#flash-viewers-end-of-life-notice}

A partir de 31 de janeiro de 2017, o Adobe Dynamic Media Classic encerrou o suporte para a plataforma do visualizador de Flashes.

<!-- For more information about this important change, see [Flash Viewer End-of-Life FAQs](https://docs.adobe.com/content/docs/en/aem/6-1/administer/integration/marketing-cloud/scene7/flash-eol.html). -->

### Adicionar um componente do Dynamic Media Classic (Scene7) a uma página {#adding-a-scene-component-to-a-page}

Adicionar um componente do Dynamic Media Classic (Scene7) a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes do Dynamic Media Classic são descritos detalhadamente nas seções a seguir.

**Para adicionar um componente do Dynamic Media Classic (Scene7) a uma página:**

1. No Experience Manager, abra a página onde deseja adicionar o componente **[!UICONTROL Dynamic Media Classic (Scene7)]**.

1. Se nenhum componente do Dynamic Media Classic estiver disponível, clique no modo **[!UICONTROL Design]**, toque em qualquer componente com uma borda azul, toque no ícone **[!UICONTROL Pai]** e, em seguida, no ícone **[!UICONTROL Configuração]**. Em **[!UICONTROL Parsys (Design)]**, selecione todos os componentes do Dynamic Media Classic para torná-los disponíveis e clique em **[!UICONTROL OK]**.

   ![chlimage_1-224](assets/chlimage_1-224.png)

1. Clique em **[!UICONTROL Editar]** para retornar ao modo **[!UICONTROL Editar]**.

1. Arraste um componente do grupo Dynamic Media Classic no sidekick até a página no local desejado.

1. Clique no ícone **[!UICONTROL Configuração]** para abrir o componente.

1. Edite o componente conforme necessário e clique em **[!UICONTROL OK]** para salvar as alterações.
1. Arraste a imagem ou o vídeo do navegador de conteúdo para o componente Dynamic Media Classic adicionado à página.

   >[!NOTE]
   >
   >Somente na interface de toque, você deve arrastar e soltar a imagem ou o vídeo no componente do Dynamic Media Classic que você colocou na página. Não há suporte para selecionar e editar o componente do Dynamic Media Classic e, em seguida, escolher o ativo.

### Adicionar experiências de visualização interativas a um site responsivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

Design responsivo para seus ativos significa que eles se adaptam dependendo de onde são exibidos. Com o design responsivo, os mesmos ativos podem ser exibidos de maneira eficaz em diversos dispositivos.

Consulte também [Design responsivo para páginas da Web](/help/sites-developing/responsive.md).

**Para adicionar uma experiência de visualização interativa a um site responsivo:**

1. Faça logon no Experience Manager e certifique-se de que você tenha [configurado o Adobe Classic Cloud Services](/help/sites-administering/scene7.md#configuring-scene-integration) e que os componentes do Dynamic Media Classic estejam disponíveis.

   >[!NOTE]
   >
   >Se os componentes do Dynamic Media Classic não estiverem disponíveis, certifique-se de [para ativá-los por meio do Modo de design](/help/sites-authoring/default-components-designmode.md).

1. Em um site com os componentes **[!UICONTROL Dynamic Media Classic]** ativados, arraste um componente **[!UICONTROL Image]** para a página.
1. Selecione o componente e toque no ícone de configuração.
1. Na guia **[!UICONTROL Configurações do Dynamic Media Classic]** , ajuste os pontos de interrupção.

   ![chlimage_1-225](assets/chlimage_1-225.png)

1. Verifique se os visualizadores estão sendo redimensionados de maneira adequada e de que todas as interações sejam otimizadas para desktop, tablet e dispositivo móvel.

### Configurações comuns a todos os componentes do Dynamic Media Classic {#settings-common-to-all-scene-components}

Embora as opções de configuração variem, as seguintes são comuns a todos os componentes do [!UICONTROL Dynamic Media Classic]:

* **[!UICONTROL Referência de arquivo]**: navegue até um arquivo que deseje referenciar. A referência de arquivo mostra o URL do ativo e não necessariamente o URL completo do Dynamic Media Classic, incluindo os comandos e parâmetros de URL. Não é possível adicionar comandos e parâmetros de URL do Dynamic Media Classic neste campo. Em vez disso, você os adiciona por meio da funcionalidade correspondente no componente.
* **[!UICONTROL Largura]**: permite definir a largura.
* **[!UICONTROL Altura]**: permite definir a altura.

Você define essas opções de configuração abrindo (clicando duas vezes em) um componente do Dynamic Media Classic, por exemplo, ao abrir um componente **[!UICONTROL Zoom]**:

![chlimage_1-226](assets/chlimage_1-226.png)

### Zoom {#zoom}

O componente de Zoom HTML5 exibe uma imagem maior quando você pressiona o botão **[!UICONTROL +]**.

O ativo tem ferramentas de zoom na parte inferior. Toque em **[!UICONTROL +]** se desejar ampliar; toque em **[!UICONTROL -]** se desejar reduzir. Tocar no **[!UICONTROL x]** ou na seta de redefinição do zoom traz a imagem de volta ao tamanho original de importação. Toque nas setas diagonais para torná-las em tela cheia. Toque em **[!UICONTROL Editar]** para configurar o componente. Com esse componente, você pode definir [configurações comuns a todos os [!UICONTROL componentes do Dynamic Media Classic]](#settings-common-to-all-scene-components).

![chlimage_1-227](/help/assets/assets/do-not-localize/chlimage_1-227.png)

### Flyout {#flyout}

No componente HTML5 **[!UICONTROL Flyout]**, o ativo é mostrado como tela dividida; deixou o ativo no tamanho especificado; à direita, a parte de zoom é exibida. Toque em **[!UICONTROL Editar]** para configurar o componente. Com esse componente, você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic](#settings-common-to-all-scene-components).

>[!NOTE]
>
>Se seu componente **[!UICONTROL Flyout]** usar um tamanho personalizado, esse tamanho personalizado será usado e a configuração responsiva do componente será desativada.
>
>Se o seu componente **[!UICONTROL Flyout]** usar o tamanho padrão, conforme definido em **[!UICONTROL Visualização de projeto]**, o tamanho padrão será usado e o componente será estendido para acomodar o tamanho do layout da página com a configuração responsiva do componente habilitado. Há uma limitação na configuração responsiva do componente. Ao usar o componente **[!UICONTROL Flyout]** com a configuração responsiva, não o use com o trecho de página completo. Caso contrário, o **[!UICONTROL Flyout]** se estende além da borda direita da página.

![chlimage_1-228](assets/chlimage_1-228.png)

### Imagem {#image}

O componente **[!UICONTROL Image]** do Dynamic Media Classic permite adicionar a funcionalidade Dynamic Media Classic às imagens, como modificadores do Dynamic Media Classic, predefinições de imagem ou visualizador e nitidez. O componente **[!UICONTROL Image]** do Dynamic Media Classic é semelhante a outros componentes de imagem no Experience Manager com funcionalidade especial do Dynamic Media Classic. Neste exemplo, a imagem tem o modificador de URL do Dynamic Media Classic, `&op_invert=1` aplicado.

![chlimage_1-229](assets/chlimage_1-229.png)

**[!UICONTROL Título, Texto alternativo]**  - Na guia  **** Avançado , adicione um título à imagem e um texto alternativo para os usuários que tenham os gráficos desativados.

**[!UICONTROL URL, Abrir em]**  - É possível definir um ativo de para abrir um link. Defina o **[!UICONTROL URL]** e, em **[!UICONTROL Abrir em]**, indique se você deseja que ele abra na mesma janela ou em uma nova.

![chlimage_1-230](assets/chlimage_1-230.png)

**[!UICONTROL Predefinição do visualizador]**  - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, você deve torná-la visível. Consulte [Gerenciar predefinições do visualizador](/help/assets/managing-viewer-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Configuração do Dynamic Media Classic]**  - Selecione a configuração do Dynamic Media Classic que deseja usar para buscar predefinições de imagens ativas do SPS.

**[!UICONTROL Predefinição de imagem]**  - Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, você deve torná-la visível. Consulte [Gerenciar predefinições de imagens](/help/assets/managing-image-presets.md). Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**[!UICONTROL Formato de saída]**  - Selecione o formato de saída da imagem, por exemplo jpeg. Dependendo do formato de saída selecionado, há opções de configuração adicionais. Consulte [Práticas recomendadas de predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options).

**[!UICONTROL Nitidez]**  - Selecione como deseja ajustar a nitidez da imagem. A nitidez é explicada detalhadamente em [Práticas recomendadas da predefinição de imagem](/help/assets/managing-image-presets.md#image-preset-options) e [Práticas recomendadas de nitidez](/help/assets/assets/sharpening_images.pdf).

**[!UICONTROL Modificadores de URL]**  - Você pode alterar os efeitos da imagem fornecendo comandos de imagem adicionais do Dynamic Media Classic. Esses comandos são descritos em [Predefinições de imagem](/help/assets/managing-image-presets.md) e [Referência de comando](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html).

**[!UICONTROL Pontos de interrupção]**  - se o seu site for responsivo, você deseja ajustar os pontos de interrupção. Os pontos de interrupção devem ser separados por vírgulas ( , ).

### Modelo de imagem {#image-template}

[Os ](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/template-basics/quick-start-template-basics.html) modelos de imagem do Dynamic Media Classic são conteúdo em camadas do Photoshop que foi importado para o Dynamic Media Classic, onde o conteúdo e as propriedades foram parametrizadas para oferecer variabilidade. O componente **[!UICONTROL Image template]** permite importar imagens e alterar o texto dinamicamente no Experience Manager. Além disso, é possível configurar o componente do **[!UICONTROL Modelo de imagem]** para usar valores do contexto de cliente, de modo que cada usuário experiencie a imagem de uma maneira personalizada.

Toque em **[!UICONTROL Editar]** se desejar configurar o componente. Você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic](#settings-common-to-all-scene-components) e outras configurações descritas nesta seção.

![chlimage_1-231](assets/chlimage_1-231.png)

**[!UICONTROL Referência de arquivo, Largura, Altura]**  - Consulte as configurações comuns a todos os componentes do ScDynamic Media Classic7.

>[!NOTE]
>
>Comandos e parâmetros de URL do Dynamic Media Classic não podem ser adicionados diretamente ao URL de referência de arquivo. Eles podem ser definidos somente na interface do componente no painel **[!UICONTROL Parâmetro]**.

**[!UICONTROL Título, Texto alternativo]**  - Na guia Modelo de imagem do Dynamic Media Classic, adicione um título à imagem e um texto alternativo para os usuários que tenham os gráficos desativados.

**[!UICONTROL URL, Abrir em]**  - É possível definir um ativo de para abrir um link. Defina o URL e, em Abrir em, indique se você deseja que ele abra na mesma janela ou em uma nova.

![chlimage_1-232](assets/chlimage_1-232.png)

**[!UICONTROL Painel de parâmetros]**  - Ao importar uma imagem, os parâmetros são preenchidos previamente com informações da imagem. Caso nenhum conteúdo possa ser alterado dinamicamente, essa janela fica vazia.

![chlimage_1-233](assets/chlimage_1-233.png)

#### Alterar o texto dinamicamente {#changing-text-dynamically}

Para alterar o texto dinamicamente, insira o novo texto nos campos e clique em **[!UICONTROL OK]**. Neste exemplo, o **[!UICONTROL Preço]** agora é $50 e o frete é de 99 centavos de dólar.

![chlimage_1-234](assets/chlimage_1-234.png)

O texto na imagem é alterado. Você pode redefinir o texto de volta para o valor original tocando em **[!UICONTROL Redefinir]** ao lado do campo.

![chlimage_1-235](assets/chlimage_1-235.png)

#### Alterar o texto para refletir o valor de contexto do cliente {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular um campo a um valor de contexto de cliente, toque em **[!UICONTROL Selecionar]** para abrir o menu de contexto de cliente, selecione o contexto de cliente e toque em **[!UICONTROL OK]**. Neste exemplo, o nome é alterado com base na vinculação do Nome com o nome formatado no perfil.

![chlimage_1-236](assets/chlimage_1-236.png)

O texto reflete o nome do cliente conectado no momento. É possível redefinir o texto de volta para o valor original ao clicar em **[!UICONTROL Redefinir]** próximo ao campo.

![chlimage_1-237](assets/chlimage_1-237.png)

#### Como tornar o modelo de imagem do Dynamic Media Classic um link {#making-the-scene-image-template-a-link}

1. Na página com o componente **[!UICONTROL Modelo de imagem do Dynamic Media Classic]**, toque em **[!UICONTROL Editar]**.
1. No campo **[!UICONTROL URL]**, insira o URL para o qual os usuários vão quando a imagem é tocada. No campo **[!UICONTROL Abrir em]**, selecione se deseja onde o destino seja aberto (uma nova janela ou na mesma).

   ![chlimage_1-238](assets/chlimage_1-238.png)

1. Toque em **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

O componente **[!UICONTROL Vídeo]** do Dynamic Media Classic (disponível na seção Dynamic Media Classic do sidekick) usa a detecção de dispositivo e de largura de banda para exibir o vídeo correto em cada tela. Este componente é um reprodutor de vídeo HTML5; é um visualizador único que pode ser usado em todos os canais.

Ele pode ser usado pra conjuntos de vídeos adaptáveis, um único vídeo MP4 ou um único vídeo F4V.

Consulte [Vídeo](s7-video.md) para obter mais informações sobre como os vídeos funcionam com a integração do Dynamic Media Classic. Além disso, consulte [o componente de Vídeo clássico do Dynamic Media versus o componente de Vídeo de base](s7-video.md).

![chlimage_1-239](assets/chlimage_1-239.png)

### Restrições conhecidas do componente de vídeo {#known-limitations-for-the-video-component}

O Adobe DAM e o WCM mostram se um vídeo de origem primária é carregado. Eles não mostram os ativos de proxy a seguir:

* Representações codificadas do Dynamic Media Classic
* Conjuntos de vídeo adaptáveis do Dynamic Media Classic

Ao usar um conjunto de vídeos adaptáveis com o componente de vídeo do Dynamic Media Classic, você deve redimensionar o componente para ajustar às dimensões do vídeo.

## Navegador de conteúdo do Dynamic Media Classic {#scene-content-browser}

O navegador de conteúdo do Dynamic Media Classic permite exibir o conteúdo do Dynamic Media Classic diretamente no Experience Manager. Para acessar o navegador de conteúdo, no **[!UICONTROL Localizador de conteúdo]**, selecione **[!UICONTROL Dynamic Media Classic]** na interface de usuário otimizada ao toque ou no ícone **[!UICONTROL S7]** na interface de usuário clássica. A funcionalidade é idêntica em ambas as interfaces do usuário.

Se você tiver várias configurações, o Experience Manager por padrão exibe a [configuração padrão](/help/sites-administering/scene7.md#configuring-a-default-configuration). Você pode selecionar configurações diferentes diretamente no navegador de conteúdo do Dynamic Media Classic no menu suspenso.

>[!NOTE]
>
>* Os ativos na pasta sob demanda não aparecem no navegador de conteúdo do Dynamic Media Classic.
>* Quando [A Visualização segura está ativada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), os ativos publicados e não publicados no Dynamic Media Classic aparecem no navegador de conteúdo do Dynamic Media Classic.
>* Se você não vir **[!UICONTROL Dynamic Media Classic]** ou o ícone **[!UICONTROL S7]** como uma opção no navegador de conteúdo, [configure o Dynamic Media Classic para funcionar com o Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, o navegador de conteúdo do Dynamic Media Classic é compatível com:

   >
   >   
   * Conjuntos de vídeos adaptáveis: contêiner de todas as representações de vídeo necessárias para uma reprodução perfeita em diversas telas
   >   * Vídeo MP4 único
   >   * Vídeo F4V único


### Navegação de conteúdo na interface otimizada para toque {#browsing-content-in-the-touch-optimized-ui}

Você pode acessar o navegador de conteúdo na interface otimizada para toque ou clássica. Atualmente, a interface otimizada para toque tem a seguinte limitação:

* FXG e ativos Flash do Dynamic Media Classic não são compatíveis.

Navegue pelos ativos do Dynamic Media Classic selecionando **[!UICONTROL Dynamic Media Classic]** no terceiro menu suspenso. O Dynamic Media Classic não será exibido na lista se você não tiver configurado a integração Dynamic Media Classic/Experience Manager.

>[!NOTE]
>
>* O navegador de conteúdo do Dynamic Media Classic carrega cerca de 100 ativos e os classifica por nome.
>* Se você tiver um servidor de visualização seguro definido, o navegador usará esse servidor de visualização para renderizar miniaturas e ativos.

>



![chlimage_1-240](assets/chlimage_1-240.png)

Além disso, você pode navegar pelas informações de resolução, tamanho, dias desde a modificação e nome do arquivo ao passar o mouse sobre o ativo no navegador.

![chlimage_1-241](assets/chlimage_1-241.png)

* Para Conjuntos de vídeos adaptáveis e Modelos, nenhuma informação de tamanho é gerada para miniaturas.
* Para Conjuntos de vídeos adaptáveis, nenhuma resolução é gerada para miniaturas.

### Pesquisar ativos do Dynamic Media Classic com o navegador de conteúdo {#searching-for-scene-assets-with-the-content-browser}

Pesquisar ativos no Dynamic Media Classic é semelhante a pesquisar ativos no Experience Manager Assets. No entanto, ao pesquisar, você está vendo uma visualização remota dos ativos no sistema Dynamic Media Classic, em vez de importá-los diretamente para o Experience Manager.

É possível usar a interface do usuário clássica ou a otimizada para toque para visualizar e pesquisar ativos. Dependendo da interface, a maneira como você pesquisa é levemente diferente.

Ao pesquisar em qualquer uma das interfaces de usuário, você pode filtrar pelos seguintes critérios (mostrados aqui na interface otimizada para toque):

**[!UICONTROL Inserir palavras-chave]**  - Você pode pesquisar ativos por nome. Ao pesquisar, as palavras-chave digitadas são o início do nome do arquivo. Por exemplo, digitar a palavra “nadar” pesquisaria todos os nomes de arquivo de ativo que comecem com as letras nessa ordem. Toque em Inserir depois de digitar o termo para localizar o ativo.

![chlimage_1-242](assets/chlimage_1-242.png)

**[!UICONTROL Pasta/caminho]**  - O nome da pasta que é vista é baseado na configuração selecionada. Você pode detalhar para níveis inferiores tocando no ícone de pasta e selecionando uma subpasta, em seguida tocando na marca de seleção para selecioná-la.

Se você inserir uma palavra-chave e selecionar uma pasta, o Experience Manager pesquisará essa pasta e quaisquer subpastas. No entanto, se você não inserir nenhuma palavra-chave ao pesquisar, selecionar a pasta somente mostrará os ativos nessa pasta e não incluirá nenhuma subpasta.

Por padrão, o Experience Manager pesquisa a pasta selecionada e todas as subpastas.

![chlimage_1-243](assets/chlimage_1-243.png)

**[!UICONTROL Tipo de ativo]**  - Selecione  **[!UICONTROL Dynamic Media]** Classic para navegar pelo conteúdo do Dynamic Media Classic. Essa opção só estará disponível se o Dynamic Media Classic tiver sido configurado.

![chlimage_1-244](assets/chlimage_1-244.png)

**[!UICONTROL Configuração]**  - Se você tiver mais de uma configuração do Dynamic Media Classic definida no  [!UICONTROL Cloud Services], poderá selecioná-la aqui. Como resultado, a pasta muda com base na configuração escolhida.

![chlimage_1-245](assets/chlimage_1-245.png)

**[!UICONTROL Tipo de ativo]**  - No navegador Dynamic Media Classic, você pode filtrar resultados para incluir qualquer um dos seguintes itens: imagens, modelos, vídeos e conjuntos de vídeos adaptáveis. Se você não selecionar nenhum tipo de ativo, o Experience Manager, por padrão, pesquisa todos os tipos de ativos.

![chlimage_1-246](assets/chlimage_1-246.png)

>[!NOTE]
>
>* Na interface do usuário clássica, também é possível procurar pelo **Flash** e pelo **FXG**. A filtragem desses tipos na interface otimizada para toque não é suportada.
   >
   >
* Ao pesquisar por vídeo, você estará procurando uma única representação. Os resultados retornam a representação original (somente o &amp;ast;.mp4) e a representação codificada.
>* Ao pesquisar um conjunto de vídeos adaptáveis, você está pesquisando a pasta e todas as subpastas, mas somente se tiver adicionado uma palavra-chave à pesquisa. Se você não tiver adicionado uma palavra-chave, o Experience Manager não pesquisará nas subpastas.

>



**[!UICONTROL Publicar status]**  - Você pode filtrar por ativos com base no status da publicação:  **** Não publicado ou  **[!UICONTROL publicado]**. Se você não selecionar nenhum **[!UICONTROL Publicar Status]**, o Experience Manager procura todos os status de publicação por padrão.

![chlimage_1-248](assets/chlimage_1-247.png)
