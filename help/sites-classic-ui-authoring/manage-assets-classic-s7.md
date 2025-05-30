---
title: Adicionar recursos do Dynamic Media Classic (Scene7) à sua página
description: O Adobe Dynamic Media Classic (Scene7) é uma solução hospedada para gerenciar, aprimorar, publicar e fornecer ativos de mídia avançada para exibições e impressão na Web, em dispositivos móveis, por email e conectados à Internet.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: bc9c864b-8bc3-42b4-ba25-6c5108be4f65
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3545'
ht-degree: 0%

---

# Adicionar recursos do Dynamic Media Classic (Scene7) à sua página{#adding-scene-features-to-your-page}

O [Adobe Dynamic Media Classic (Scene7)](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/home.html?lang=pt-BR) é uma solução hospedada para gerenciamento, aprimoramento, publicação e fornecimento de ativos de mídia avançada para Web, dispositivos móveis, email e exibições e impressões conectadas à Internet.

Você pode visualizar ativos do Experience Manager publicados no Dynamic Media Classic (Scene7) em vários visualizadores:

* Zoom
* Flyout
* Vídeo
* Modelo da imagem
* Imagem

Você pode publicar ativos digitais diretamente do Experience Manager para o Dynamic Media Classic (Scene7) e pode publicar ativos digitais do Dynamic Media Classic (Scene7) para o Experience Manager.

Este documento descreve como publicar ativos digitais do Experience Manager para o Dynamic Media Classic (Scene7) e vice-versa. Os visualizadores também são descritos em detalhes. Para obter informações sobre como configurar o Experience Manager para o Dynamic Media Classic (Scene7), consulte [Integração do Dynamic Media Classic (Scene7) com o Experience Manager](/help/sites-administering/scene7.md).

Consulte também [Adicionar mapas de imagem](/help/assets/image-maps.md).

Para obter mais informações sobre o uso de componentes de vídeo com o Experience Manager, consulte o seguinte:

* [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md)

>[!NOTE]
>
>Se os ativos do Dynamic Media Classic (Scene7) não forem exibidos corretamente, verifique se o Dynamic Media está [desabilitado](/help/assets/config-dynamic.md#disabling-dynamic-media) e atualize a página.

## Publicação manual no Dynamic Media Classic (Scene7) a partir do Assets {#manually-publishing-to-scene-from-assets}

Você pode publicar ativos digitais no Dynamic Media Classic (Scene7) pelo console do Assets na interface clássica ou diretamente do ativo.

>[!NOTE]
>
>O Experience Manager publica no Dynamic Media Classic (Scene7) de forma assíncrona. Após selecionar **[!UICONTROL Publish]**, pode levar alguns segundos para que seu ativo seja publicado na Dynamic Media Classic (Scene7).
>

### Publicação por meio do console do Assets {#publishing-from-the-assets-console}

Publique no Dynamic Media Classic (Scene7) a partir do console do Assets se os ativos estiverem em uma pasta de destino do Dynamic Media Classic (Scene7).

1. Na interface clássica do Experience Manager, selecione **[!UICONTROL Digital Assets]** para acessar o gerenciador de ativos digitais.

1. Selecione o(s) ativo(s) ou pasta(s) dentro da pasta de destino que você deseja publicar no Dynamic Media Classic (Scene7), clique com o botão direito do mouse e selecione **[!UICONTROL Publish to Dynamic Media Classic (Scene7)]**. Como alternativa, você pode selecionar **[!UICONTROL Publish para Dynamic Media Classic (Scene7)]** no menu **[!UICONTROL Ferramentas]**.

   ![chlimage_1-48](assets/chlimage_1-48.png)

1. Acesse o Dynamic Media Classic (Scene7) e confirme se os ativos estão disponíveis.

   >[!NOTE]
   >
   >Se os ativos não estiverem em uma pasta sincronizada do Dynamic Media Classic (Scene7), o **[!UICONTROL Publish para o Dynamic Media Classic (Scene7)]** em ambos os menus estará visível, mas desabilitado.

### Publish de um ativo {#publishing-from-an-asset}

Você pode publicar manualmente um ativo, desde que ele esteja localizado na pasta Dynamic Media Classic sincronizada (Scene7).

>[!NOTE]
>
>Se o ativo não estiver na pasta sincronizada do Dynamic Media Classic (Scene7), o link para o **[!UICONTROL Publish para o Dynamic Media Classic (Scene7)]** não será exibido.

Para publicar no Dynamic Media Classic (Scene7) diretamente de um ativo digital:

1. No Experience Manager, selecione **[!UICONTROL Digital Assets]** para acessar o gerenciador de ativos digitais.

1. Clique duas vezes para abrir um ativo.

1. No painel de detalhes do ativo, selecione **[!UICONTROL Publish para Dynamic Media Classic (Scene7)]**.

   ![screen_shot_2012-02-22at34828pm](assets/screen_shot_2012-02-22at34828pm.png)

1. O link foi alterado para **[!UICONTROL Publicando...]** e depois **[!UICONTROL Publicado]**. Acesse Dynamic Media Classic (Scene7) e confirme se o ativo está disponível.

   >[!NOTE]
   >
   >Se o ativo não for publicado corretamente no Dynamic Media Classic (Scene7), o link será alterado para **[!UICONTROL Falha na publicação]**. Se o ativo já tiver sido publicado no Dynamic Media Classic (Scene7), o link exibirá **[!UICONTROL Re-Publish para o Dynamic Media Classic (Scene7)]**. A republicação permite alterar ativos no Experience Manager e republicá-los.

### Ativos do Publish de fora da pasta de destino do CQ {#publishing-assets-from-outside-the-cq-target-folder}

A Adobe recomenda publicar ativos no Dynamic Media Classic (Scene7) somente de ativos contidos na pasta de destino do Dynamic Media Classic (Scene7). No entanto, se você precisar fazer upload de ativos de uma pasta fora da pasta de destino, ainda será possível fazer isso carregando-os em uma pasta sob demanda no Dynamic Media Classic (Scene7). Primeiro, defina a Configuração da nuvem para a página em que deseja que o ativo apareça. Em seguida, você adiciona um componente Dynamic Media Classic (Scene7) à página e arrasta e solta um ativo no componente. Depois que as propriedades da página são definidas para essa página, um link **[!UICONTROL Publish para o Dynamic Media Classic (Scene7)]** é exibido e, quando selecionado, aciona o upload para o Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Os Assets que estão na pasta sob demanda não aparecem no Navegador de conteúdo do Dynamic Media Classic (Scene7).

**Para publicar ativos de fora da pasta de destino do CQ:**

1. Em Experience Manager na interface clássica, selecione **[!UICONTROL Sites]** e navegue até a página da Web à qual você deseja adicionar um ativo digital que ainda não foi publicado no Dynamic Media Classic (Scene7). (As regras normais de herança de página se aplicam.)

1. No sidekick, selecione o ícone **[!UICONTROL Página]** e selecione **[!UICONTROL Propriedades da página]**.

1. Selecione **[!UICONTROL Cloud Service]**.
1. Selecione **[!UICONTROL Adicionar serviços]**.
1. Selecione **[!UICONTROL Dynamic Media Classic (Scene7)]**.
1. Na lista suspensa **[!UICONTROL Adobe Dynamic Media Classic (Scene7)]**, selecione a configuração desejada e selecione **[!UICONTROL OK]**.

   ![chlimage_1-49](assets/chlimage_1-49.png)

1. Na página da Web, adicione um componente do Dynamic Media Classic (Scene7) ao local desejado na página.
1. No localizador de conteúdo, arraste um ativo digital para o componente. Você verá um link para **[!UICONTROL Verificar o Status de Publicação do Dynamic Media Classic (Scene7)]**.

   >[!NOTE]
   >
   >Se o ativo digital estiver na pasta de destino do CQ, nenhum link para **[!UICONTROL Verificar status de publicação do Dynamic Media Classic (Scene7)]** será exibido. Os ativos são colocados no componente.

   ![chlimage_1-50](assets/chlimage_1-50.png)

1. Selecione **[!UICONTROL Verificar Status de Publicação do Dynamic Media Classic (Scene7)]**. Se os ativos não forem publicados, o Experience Manager publicará o ativo no Dynamic Media Classic (Scene7). Depois de carregado, o ativo é encontrado na pasta sob demanda. Por padrão, a pasta sob demanda está no **[!UICONTROL name_of_the_company/CQ5_adhoc]**. Você pode [configurar a pasta por demanda, se necessário](#configuringtheadhocfolder).

   >[!NOTE]
   >
   >Se o ativo não estiver em uma pasta sincronizada do Dynamic Media Classic (Scene7) e não houver configuração de nuvem do Dynamic Media Classic (Scene7) associada à página atual, o upload falhará.

## Componentes do Dynamic Media Classic (Scene7) {#scene-components}

Os seguintes componentes do Dynamic Media Classic (Scene7) estão disponíveis no Experience Manager:

* Zoom
* Submenu (Zoom)
* Modelo da imagem
* Imagem
* Vídeo

>[!NOTE]
>
>Esses componentes não estão disponíveis por padrão e devem ser selecionados no modo Design antes de usar.

Depois que eles forem disponibilizados no modo Design, será possível adicionar os componentes à página como qualquer outro componente Experience Manager. Os Assets que ainda não foram publicados no Dynamic Media Classic (Scene7) são publicados no Dynamic Media Classic (Scene7) se estiverem em uma pasta sincronizada, em uma página ou com uma configuração de nuvem do Dynamic Media Classic (Scene7).

>[!NOTE]
>
>Se você estiver criando e desenvolvendo visualizadores S7 personalizados e estiver usando o Localizador de conteúdo, será necessário adicionar explicitamente o parâmetro `allowfullscreen`.

### Aviso de fim de vida útil de visualizadores do Flash {#flash-viewers-end-of-life-notice}

A partir de 31 de janeiro de 2017, o Adobe Dynamic Media Classic (Scene7) encerrou oficialmente o suporte para a plataforma de visualizador de Flashes.

### Adicionar um componente do Dynamic Media Classic (Scene7) a uma página {#adding-a-scene-component-to-a-page}

Adicionar um componente do Dynamic Media Classic (Scene7) a uma página é o mesmo que adicionar um componente a qualquer página. Os componentes do Dynamic Media Classic (Scene7) são descritos detalhadamente nas seções a seguir.

Para adicionar um componente/visualizador do Dynamic Media Classic (Scene7) a uma página na interface clássica:

1. No Experience Manager, abra a página em que deseja adicionar o componente Dynamic Media Classic (Scene7).

1. Se nenhum componente do Dynamic Media Classic (Scene7) estiver disponível, selecione a régua no sidekick para entrar no modo **Design**, selecione **[!UICONTROL Editar]** parsys e selecione todos os componentes do **[!UICONTROL Dynamic Media Classic (Scene7)]** para torná-los disponíveis.

1. Retorne ao modo **Editar** selecionando o lápis no sidekick.

1. Arraste um componente do grupo **[!UICONTROL Dynamic Media Classic (Scene7)]** no sidekick para a página no local desejado.

1. Selecione ***[!UICONTROL Editar]** para poder abrir o componente.

1. Edite o componente conforme necessário e selecione **[!UICONTROL OK]** para salvar as alterações.

### Adicionar experiências de visualização interativa a um site responsivo {#adding-interactive-viewing-experiences-to-a-responsive-website}

O design responsivo para seus ativos significa que seus ativos se adaptam dependendo de onde são exibidos. Com um design responsivo, os mesmos ativos podem ser exibidos de maneira eficaz em vários dispositivos.

Para adicionar uma experiência de visualização interativa a um site responsivo na interface clássica:

1. Faça logon no Experience Manager e verifique se você tem [Cloud Service do Adobe Dynamic Media Classic (Scene7) configurados](/help/sites-administering/scene7.md#configuring-scene-integration) e se os componentes do Dynamic Media Classic (Scene7) estão disponíveis.

   >[!NOTE]
   >
   >Se os componentes do WCM do Dynamic Media Classic (Scene7) não estiverem disponíveis, ative-os no modo Design.

1. Em um site com os componentes do Dynamic Media Classic (Scene7) habilitados, arraste um visualizador de **[!UICONTROL Imagem]** para a página.
1. Edite o componente e ajuste os pontos de interrupção na guia **[!UICONTROL Configurações do Dynamic Media Classic (Scene7)]**.

   ![chlimage_1-51](assets/chlimage_1-51.png)

1. Confirme se os visualizadores estão redimensionando com agilidade e se todas as interações estão otimizadas para desktop, tablet e dispositivos móveis.

### Configurações comuns a todos os componentes do Dynamic Media Classic (Scene7) {#settings-common-to-all-scene-components}

Embora as opções de configuração variem, as seguintes opções são comuns a todos os componentes do Dynamic Media Classic (Scene7):

* **Referência de arquivo**- Procure um arquivo que você deseja referenciar. A referência de arquivo mostra o URL do ativo e não necessariamente o URL completo do Dynamic Media Classic (Scene7), incluindo os comandos e parâmetros do URL. Não é possível adicionar comandos e parâmetros de URL do Dynamic Media Classic (Scene7) neste campo. Em vez disso, eles devem ser adicionados por meio da funcionalidade correspondente no componente.
* **Largura** - Permite definir a largura.
* **Altura** - Permite definir a altura.

Você define estas opções de configuração abrindo (clicando duas vezes) um componente do Dynamic Media Classic (Scene7), por exemplo, quando você abre um componente **Zoom**:

![chlimage_1-52](assets/chlimage_1-52.png)

### Zoom {#zoom}

O componente de HTML5 Zoom exibe uma imagem maior quando você pressiona o botão +.

O ativo tem ferramentas de zoom na parte inferior. Selecione **[!UICONTROL +]** para ampliar. Selecione **[!UICONTROL -]** para reduzir. Ao selecionar **[!UICONTROL x]** ou a seta para redefinir zoom, a imagem é retornada ao tamanho original para o qual foi importada. Selecione as setas diagonais para que você possa usá-las em tela cheia. Selecione **[!UICONTROL Editar]** para poder configurar o componente. Com este componente, você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic (Scene7)](#settings-common-to-all-scene-components).

![Imagem de flores de tulipa dentro do componente de HTML5 Zoom.](do-not-localize/chlimage_1-3.png)

### Flyout {#flyout}

No componente Flyout HTML5, o ativo é exibido como tela dividida; deixa o ativo no tamanho especificado; direita, a parte de zoom é exibida. Selecione **[!UICONTROL Editar]** para poder configurar o componente. Com este componente, você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Se o componente Submenu usar um tamanho personalizado, esse tamanho personalizado será usado e a configuração responsiva do componente será desativada.
>
>Se o componente Submenu usar o tamanho padrão, como definido na visualização Design, o tamanho padrão será usado. O componente se alonga para acomodar o tamanho do layout da página com a configuração responsiva do componente ativada. No entanto, esteja ciente de que há uma limitação na configuração responsiva do componente. Ao usar o componente Flyout com configuração responsiva, você não deve usá-lo com ampliação de página inteira. Caso contrário, o Submenu poderá se estender além da borda direita da página.

![chlimage_1-53](assets/chlimage_1-53.png)

### Imagem {#image}

O componente de Imagem do Dynamic Media Classic (Scene7) permite adicionar a funcionalidade do Dynamic Media Classic (Scene7) às suas imagens, como modificadores do Dynamic Media Classic (Scene7), predefinições de imagens ou do visualizador e nitidez. O componente de imagem do Dynamic Media Classic (Scene7) é semelhante a outros componentes de imagem no Experience Manager com funcionalidade especial do Dynamic Media Classic (Scene7). Neste exemplo, a imagem tem o modificador de URL do Dynamic Media Classic (Scene7), `&op_invert=1` aplicado.

![Imagem de uma esfera dentro do componente de imagem do Dynamic Media Classic (Scene 7)](do-not-localize/chlimage_1-4.png)

**Título, Texto Alternativo** - Na guia Avançado, adicione um título à imagem e um texto alternativo para os usuários que têm gráficos desativados.

**URL, Abrir em** - Você pode definir um ativo de para abrir um link. Defina o URL e, em Abrir no, indique se deseja abri-lo na mesma janela ou em uma nova janela.

![chlimage_1-54](assets/chlimage_1-54.png)

**Predefinição do visualizador** - Selecione uma predefinição do visualizador existente no menu suspenso. Se a predefinição do visualizador que você está procurando não estiver visível, é necessário torná-la visível. Consulte Gerenciamento de predefinições do visualizador. Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**Configuração do Dynamic Media Classic (Scene7)** - Selecione a configuração do Dynamic Media Classic (Scene7) que deseja usar para buscar predefinições de imagens ativas do SPS.

**Predefinição de imagem** - Selecione uma predefinição de imagem existente no menu suspenso. Se a predefinição de imagem que você está procurando não estiver visível, será necessário torná-la visível. Consulte Gerenciamento de predefinições de imagem. Não é possível selecionar uma predefinição do visualizador se você estiver usando uma predefinição de imagem e vice-versa.

**Formato de saída** - Selecione o formato de saída da imagem, por exemplo, jpeg. Dependendo do formato de saída selecionado, talvez você tenha opções de configuração adicionais. Consulte Práticas recomendadas de predefinição de imagem.

**Nitidez** - Selecione como deseja nitidez da imagem. A nitidez é explicada em detalhes em Práticas recomendadas de predefinição de imagem e Práticas recomendadas de nitidez.

**Modificadores de URL** - Você pode alterar efeitos de imagem fornecendo comandos de imagem S7 adicionais. Esses comandos são descritos em Predefinições de imagem e a referência do comando.

**Pontos de interrupção** - Se o site for responsivo, ajuste os pontos de interrupção. Os pontos de interrupção devem ser separados por vírgulas (,).

### Modelo da imagem {#image-template}

Os Modelos de imagem do Dynamic Media Classic (Scene7) são conteúdo em camadas do Photoshop que foi importado para o Dynamic Media Classic (Scene7), onde o conteúdo e as propriedades eram parametrizados para fins de variabilidade. O componente **[!UICONTROL Modelo de imagem]** permite importar imagens e alterar o texto dinamicamente no Experience Manager. Além disso, você pode configurar o componente **[!UICONTROL Modelo de imagem]** para usar valores do contexto do cliente, para que cada usuário experimente a imagem de forma personalizada.

Selecione **[!UICONTROL Editar]** - para configurar o componente. Você pode definir [configurações comuns a todos os componentes do Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components) e outras configurações descritas nesta seção.

![chlimage_1-55](assets/chlimage_1-55.png)

**Referência de arquivo, Largura, Altura** - Consulte [configurações comuns a todos os componentes do Dynamic Media Classic (Scene7)](/help/sites-administering/scene7.md#settingscommontoallscene7components).

>[!NOTE]
>
>Os comandos e parâmetros de URL do Dynamic Media Classic (Scene7) não podem ser adicionados diretamente ao URL de referência de arquivo. Eles só podem ser definidos na interface do usuário do componente no painel **[!UICONTROL Parâmetro]**.

**Título, Texto Alternativo** - Na guia Modelo de Imagem do Dynamic Media Classic (Scene7), adicione um título à imagem e um texto alternativo para os usuários que têm gráficos desativados.

**URL, Abrir em** - Você pode definir um ativo de para abrir um link. Defina o URL e, em Abrir no, indique se deseja abri-lo na mesma janela ou em uma nova janela.

![chlimage_1-56](assets/chlimage_1-56.png)

**Painel de Parâmetros** - Ao importar uma imagem, os parâmetros são pré-preenchidos com informações da imagem. Se não houver conteúdo que possa ser alterado dinamicamente, essa janela ficará vazia.

![chlimage_1-57](assets/chlimage_1-57.png)

#### Alteração dinâmica do texto {#changing-text-dynamically}

Para alterar o texto dinamicamente, insira um novo texto nos campos e selecione **[!UICONTROL OK]**. Neste exemplo, o **Preço** agora é de $50 e o frete é de 99 centavos.

![chlimage_1-58](assets/chlimage_1-58.png)

O texto na imagem é alterado. Você pode redefinir o texto de volta para o valor original selecionando **[!UICONTROL Redefinir]** ao lado do campo.

![chlimage_1-59](assets/chlimage_1-59.png)

#### Alterar texto para refletir o valor de um valor de contexto do cliente {#changing-text-to-reflect-the-value-of-a-client-context-value}

Para vincular um campo a um valor de contexto de cliente, selecione **[!UICONTROL Selecionar]** para abrir o menu de contexto de cliente, selecione o contexto de cliente e selecione **[!UICONTROL OK]**. Neste exemplo, o nome muda com base na vinculação do Name com o nome formatado no perfil.

![chlimage_1-60](assets/chlimage_1-60.png)

O texto reflete o nome do usuário conectado no momento. Você pode redefinir o texto de volta para o valor original selecionando **[!UICONTROL Redefinir]** ao lado do campo.

![chlimage_1-61](assets/chlimage_1-61.png)

#### Transforme o modelo de imagem do Dynamic Media Classic (Scene7) em um link {#making-the-scene-image-template-a-link}

Você pode tornar o componente de modelo de imagem do Dynamic Media Classic (Scene7) um link clicável.

1. Na página com o componente de modelo de imagem do Dynamic Media Classic (Scene7), selecione **[!UICONTROL Editar]**.
1. No campo **[!UICONTROL URL]**, insira a URL para a qual os usuários irão quando a imagem for clicada. No campo **[!UICONTROL Abrir em]**, selecione se deseja abrir o destino (uma nova janela ou a mesma janela).

   ![chlimage_1-62](assets/chlimage_1-62.png)

1. Selecione **[!UICONTROL OK]**.

### Componente de vídeo {#video-component}

O componente de **[!UICONTROL Vídeo]** do Dynamic Media Classic (Scene7) (disponível na seção Dynamic Media Classic (Scene7) do sidekick) usa detecção de dispositivo e largura de banda para veicular o vídeo correto em cada tela. Esse componente é um reprodutor de vídeo HTML5; é um único visualizador que pode ser usado entre canais.

Ele pode ser usado para conjuntos de vídeos adaptáveis, um único vídeo MP4 ou um único vídeo F4V.

Consulte [Vídeo](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md) para obter mais informações sobre como os vídeos funcionam com a integração do Dynamic Media Classic (Scene7). Além disso, veja como o componente de [vídeo **do** Dynamic Media Classic (Scene7) se compara ao componente de **vídeo** da base](/help/sites-classic-ui-authoring/manage-assets-classic-s7-video.md).

![chlimage_1-63](assets/chlimage_1-63.png)

### Limitações conhecidas do componente de vídeo {#known-limitations-for-the-video-component}

O DAM do Adobe e o WCM mostram se um vídeo de origem primária foi carregado. Eles não mostram esses ativos proxy:

* Representações codificadas do Dynamic Media Classic (Scene7)
* Conjuntos de vídeo adaptável do Dynamic Media Classic (Scene7)

Ao usar um conjunto de vídeos adaptáveis com o componente de vídeo do Dynamic Media Classic (Scene7), o componente deve ser redimensionado para se ajustar às dimensões do vídeo.

## Navegador de conteúdo do Dynamic Media Classic (Scene7) {#scene-content-browser}

O navegador de conteúdo do Dynamic Media Classic (Scene7) permite exibir o conteúdo do Dynamic Media Classic (Scene7) diretamente no Experience Manager. Para acessar o navegador de conteúdo, no Localizador de Conteúdo, selecione **Dynamic Media Classic (Scene7)** na interface otimizada para toque ou o ícone **S7** na interface de usuário clássica. A funcionalidade é idêntica entre as duas interfaces do usuário.

Se você tiver várias configurações, o Experience Manager, por padrão, exibe a [configuração padrão](/help/sites-administering/scene7.md#configuring-a-default-configuration). Você pode selecionar configurações diferentes diretamente no navegador de conteúdo do Dynamic Media Classic (Scene7) no menu suspenso.

>[!NOTE]
>
>* O Assets na pasta on-demand não aparece no navegador de conteúdo do Dynamic Media Classic (Scene7).
>* Quando a [Visualização Segura está habilitada](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene), tanto os ativos publicados quanto os não publicados no Dynamic Media Classic (Scene7) aparecem no navegador de conteúdo do Dynamic Media Classic (Scene7).
>* Se você não vir o ícone do **[!UICONTROL Dynamic Media Classic (Scene7)]** ou do **[!UICONTROL S7]** como uma opção no navegador de conteúdo, será necessário [configurar o Dynamic Media Classic (Scene7) para funcionar com o Experience Manager](/help/sites-administering/scene7.md).
>* Para vídeo, o navegador de conteúdo do Dynamic Media Classic (Scene7) é compatível com:
>   * Conjuntos de vídeos adaptados: contêiner de todas as representações de vídeo necessárias para a reprodução contínua em várias telas
>   * Vídeo MP4 único
>   * Vídeo F4V único

### Procurar conteúdo {#browsing-content-in-the-classic-ui}

Procure o conteúdo no Dynamic Media Classic (Scene7) selecionando a guia **[!UICONTROL S7]**.

Você pode alterar a configuração que está acessando selecionando a configuração. As pastas mudam, dependendo da configuração selecionada.

![chlimage_1-64](assets/chlimage_1-64.png)

Assim como no localizador de conteúdo para o Assets, você pode pesquisar por ativos e filtrar resultados. No entanto, ao contrário do localizador do Assets, ao inserir uma palavra-chave na guia **S7**, o nome de arquivo **começa com** a cadeia de caracteres inserida, em vez de **conter** a palavra-chave no nome de arquivo.

Por padrão, os ativos são exibidos por nome de arquivo. No entanto, também é possível filtrar os resultados por tipo de ativo.

>[!NOTE]
>
>Para vídeo, o navegador de conteúdo do Dynamic Media Classic (Scene7) do WCM é compatível com:
>
>* Conjuntos de vídeos adaptados: contêiner de todas as representações de vídeo necessárias para a reprodução contínua em várias telas
>* Vídeo MP4 único
>* Vídeo F4V único
>

### Pesquisar ativos do Dynamic Media Classic (Scene7) com o navegador de conteúdo {#searching-for-scene-assets-with-the-content-browser}

Pesquisar ativos do Dynamic Media Classic (Scene7) é semelhante a pesquisar ativos do Experience Manager. A exceção é que, ao pesquisar, você está vendo uma visualização remota dos ativos no sistema Dynamic Media Classic (Scene7), em vez de importá-los diretamente para o Experience Manager.

Você pode usar a interface clássica ou a interface otimizada para toque para visualizar e pesquisar ativos. Dependendo da interface, a forma como você pesquisa será um pouco diferente.

Ao pesquisar em qualquer uma das interfaces do usuário, você pode filtrar pelos seguintes critérios (mostrados aqui na interface otimizada para toque):

**Inserir palavras-chave** - Você pode pesquisar ativos por nome. Ao pesquisar as palavras-chave, digite é com o nome do arquivo que começa. Por exemplo, digitar a palavra &quot;natação&quot; procuraria qualquer nome de arquivo de ativo que começasse com essas letras nessa ordem. Certifique-se de selecionar `Enter` depois de digitar o termo para localizar o ativo.

![chlimage_1-65](assets/chlimage_1-65.png)

**Pasta/caminho** - O nome da pasta é baseado na configuração selecionada. Você pode detalhar os níveis inferiores selecionando o ícone de pasta e uma subpasta e, em seguida, marcando a marca de seleção para selecioná-la.

Se você inserir uma palavra-chave e selecionar uma pasta, o Experience Manager pesquisará essa pasta e todas as subpastas. No entanto, se você não inserir nenhuma palavra-chave ao pesquisar, selecionar a pasta mostrará apenas os ativos nessa pasta e não incluirá nenhuma subpasta.

Por padrão, o Experience Manager pesquisa a pasta selecionada e todas as subpastas.

![chlimage_1-66](assets/chlimage_1-66.png)

**Tipo de ativo** - Selecione Dynamic Media Classic (Scene7) para procurar conteúdo do Dynamic Media Classic (Scene7). Essa opção só estará disponível se o Dynamic Media Classic (Scene7) tiver sido configurado.

![chlimage_1-67](assets/chlimage_1-67.png)

**Configuração** - Se você tiver mais de uma configuração Dynamic Media Classic (Scene7) definida em Cloud Service, selecione-a aqui. Como resultado, a pasta muda com base na configuração escolhida.

![chlimage_1-68](assets/chlimage_1-68.png)

**Tipo de ativo** - No navegador Dynamic Media Classic (Scene7), você pode filtrar os resultados para incluir qualquer um dos seguintes itens: imagens, modelos, vídeos e conjuntos de vídeos adaptáveis. Se você não selecionar nenhum tipo de ativo, o Experience Manager, por padrão, pesquisará todos os tipos de ativos.

![chlimage_1-69](assets/chlimage_1-69.png)

>[!NOTE]
>
>* Na interface clássica, você também pode procurar por **Flash** e **FXG**. Não há suporte para a filtragem desses dois termos na interface otimizada para toque.
>
>* Ao pesquisar vídeos, você pesquisa uma única representação. Os resultados retornam a representação original (somente &#42;.mp4) e a representação codificada.
>* Ao pesquisar um conjunto de vídeos adaptáveis, você está pesquisando a pasta e todas as subpastas, mas somente se tiver adicionado uma palavra-chave à pesquisa. Se você não tiver adicionado uma palavra-chave, o Experience Manager não pesquisará nas subpastas.
>

**Status do Publish** - Você pode filtrar por ativos com base no status da publicação: Não publicado ou Publicado. Se você não selecionar nenhum Status do Publish, o Experience Manager, por padrão, pesquisará todos os status de publicação.

![chlimage_1-70](assets/chlimage_1-70.png)
