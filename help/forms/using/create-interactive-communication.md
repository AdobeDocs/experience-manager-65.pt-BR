---
title: Criar uma comunicação interativa
seo-title: Create an Interactive Communication
description: Crie uma Comunicação interativa usando o editor de Comunicação interativa. Use a funcionalidade de arrastar e soltar para criar a Comunicação interativa e pré-visualize as saídas de impressão e da Web em diferentes tipos de dispositivos.
seo-description: Create an Interactive Communication using the Interactive Communication editor. Use drag-and-drop functionality to build the Interactive Communication, and preview both print and web outputs on different device types.
uuid: d524a3de-00b4-444f-b3c7-be443fa24ec8
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f4d98cb9-84d8-4735-91d2-b9ceec861e5e
docset: aem65
feature: Interactive Communication
exl-id: 1f89c3bf-e67e-4d13-9285-3367be1ac8f8
source-git-commit: 92092e1c050c9264c19e3cd9da9b240607af7bab
workflow-type: tm+mt
source-wordcount: '6178'
ht-degree: 1%

---

# Criar uma comunicação interativa{#create-an-interactive-communication}

## Visão geral {#overview}

As Comunicações interativas centralizam e gerenciam a criação, montagem e delivery personalizado e correspondências interativas. Utilize a impressão como canal principal para a Web, você pode minimizar a duplicação de esforços na criação da saída da Web da Comunicação interativa.

### Pré-requisitos {#prerequisites}

A seguir estão os pré-requisitos para a criação de uma Comunicação Interativa:

* Configure um [Modelo de dados do formulário](/help/forms/using/data-integration.md) contendo dados de teste ou com uma fonte de dados real, como uma instância do Microsoft® Dynamics.
* Certifique-se de ter a [Fragmentos de documento](/help/forms/using/document-fragments.md).
* Certifique-se de que [Modelos para impressão e canal da Web](/help/forms/using/web-channel-print-channel.md).
* Certifique-se de que você tenha o [tema](/help/forms/using/themes.md) para o canal da Web.

## Criar a comunicação interativa {#createic}

1. Faça logon na instância do autor do AEM e navegue até **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque **[!UICONTROL Criar]** e selecione **[!UICONTROL Comunicação interativa]**. A página Criar comunicação interativa é exibida.

   ![create-interative-communication](assets/create-interactive-communication.png)

1. Insira as seguintes informações. :

   * **[!UICONTROL Título]**: Insira o título da Comunicação interativa.
   * **[!UICONTROL Nome]**: O nome da Comunicação interativa é derivado do título inserido. Edite-a, se necessário.
   * **[!UICONTROL Descrição]**: Insira uma descrição sobre a Comunicação interativa.
   * **[!UICONTROL Modelo de dados do formulário]**: Navegue e selecione o modelo de dados de formulário. Para obter mais informações sobre o Modelo de dados de formulário, consulte [Integração de dados do AEM Forms](/help/forms/using/data-integration.md).

   * **[!UICONTROL Serviço de preenchimento prévio]**: Selecione o serviço de preenchimento prévio para recuperar os dados e preencher previamente a Comunicação interativa.
   * **[!UICONTROL Tipo de pós-processo]**: Você pode selecionar AEM ou Forms workflow a ser acionado quando a Comunicação interativa for enviada. Selecione o tipo de workflow a ser acionado.

   * **[!UICONTROL Processo de postagem]**: Selecione o nome do workflow a ser acionado. Ao selecionar AEM fluxo de trabalho, forneça Attachment Path, Layout Path, PDF Path, Print Data Path e Web Data Path.
   * **[!UICONTROL Tags]**: Selecione as tags a serem aplicadas à Comunicação interativa. Você também pode digitar um nome de tag novo/personalizado e pressionar Enter para criá-lo.
   * **[!UICONTROL Autor]**: o nome do autor é obtido automaticamente do nome de usuário do usuário conectado.
   * **[!UICONTROL Data de publicação:]** Insira a data para publicar a Comunicação interativa.
   * **[!UICONTROL Data de cancelamento da publicação]**: Insira a data para cancelar a publicação da Comunicação interativa.

1. Toque **[!UICONTROL Próximo]**. A tela para especificar detalhes do canal da Web e da impressão é exibida.
1. Insira o seguinte:

   * **[!UICONTROL Imprimir]**: Selecione essa opção para gerar o canal de impressão da Comunicação interativa.
   * **[!UICONTROL Modelo de impressão]**: Procure e selecione um XDP como modelo de impressão.
   * **[!UICONTROL Web]**: Selecione essa opção para gerar o canal da Web ou o resultado responsivo da Comunicação interativa.
   * **[!UICONTROL Modelo Web de Comunicação Interativa]**: Procure e selecione o modelo da Web.
   * **[!UICONTROL Tema]** e **[!UICONTROL Selecionar Tema]**: Navegue e selecione o tema para criar um estilo no canal da Web da Comunicação interativa. Para obter mais informações, consulte [Temas no AEM Forms](/help/forms/using/themes.md).

   * **[!UICONTROL Usar Imprimir como Principal para Canal da Web]**: Selecione essa opção para criar o canal da Web em sincronia com o canal de impressão. Usar o canal de impressão como principal para o canal da Web garante que o conteúdo e o vínculo de dados do canal da Web sejam derivados do canal de impressão e as alterações feitas no canal de impressão sejam refletidas no canal da Web quando você tocar em Sincronizar. Os autores, no entanto, têm permissão para quebrar a herança de componentes específicos no canal da Web, conforme necessário. Para obter mais informações, consulte [Sincronizar canal Web com canal de impressão](../../forms/using/create-interactive-communication.md#synchronize).
Se você selecionar a variável **[!UICONTROL Usar Imprimir como Principal para Canal da Web]** , você pode selecionar qualquer um dos seguintes modos para gerar o canal da Web:

      * **[!UICONTROL Layout automático]**: Selecione esse modo para gerar automaticamente espaços reservados, conteúdo e vínculo de dados para o canal da Web do canal de Impressão.
      * **[!UICONTROL Organizar manualmente]**: Selecione esse modo para selecionar e adicionar manualmente os elementos do canal de impressão ao canal da Web usando o conteúdo principal disponível na **[!UICONTROL Fontes de dados]** guia . Para obter mais informações, consulte [Selecione Print channel elements para criar o conteúdo do canal da Web](#selectprintchannelelements).

   Para obter mais informações sobre canal de impressão e canal da Web, consulte [Canal de impressão e canal da Web](/help/forms/using/web-channel-print-channel.md).

1. Toque **[!UICONTROL Criar]**. A Comunicação interativa é criada e uma caixa de alerta é exibida. Toque **[!UICONTROL Editar]** para começar a criar o conteúdo da Comunicação interativa, conforme explicado em [Adicionar conteúdo usando a interface do usuário de criação do Interative Communication](#step2). Como alternativa, toque em **[!UICONTROL Concluído]** e opte por editar a Comunicação interativa posteriormente.

## Adicionar conteúdo à comunicação interativa {#step2}

Após criar uma Comunicação interativa, você pode usar a interface de criação Comunicação interativa para construir seu conteúdo.

Para obter mais informações sobre a interface de criação do Interative Communication, consulte [Introdução à criação de Comunicações interativas](/help/forms/using/introduction-interactive-communication-authoring.md).

1. A interface de criação da Comunicação interativa é iniciada quando você toca em Editar, como mencionado em [Criar comunicação interativa](#createic). Como alternativa, você pode navegar até um ativo de Comunicação interativa existente no AEM, selecioná-lo e tocar em **[!UICONTROL Editar]** para iniciar a interface de criação da Comunicação interativa .

   Por padrão, o canal de impressão da Comunicação interativa é exibido, a menos que a Comunicação interativa seja somente de canal da Web. O canal Imprimir da Comunicação Interativa exibe áreas de destino, conforme disponível no modelo de canal XDP/impressão selecionado. Nesses campos e áreas de destino, é possível adicionar componentes ou ativos.

1. Com o canal Imprimir selecionado, selecione o **[!UICONTROL Componentes]** guia . Os seguintes componentes estão disponíveis no canal de impressão:

   | **Componente** | **Funcionalidade** |
   |---|---|
   | Gráfico | Adiciona um gráfico que pode ser usado na Comunicação interativa para representação visual de dados bidimensionais recuperados de uma coleção de modelo de dados de formulário. Para obter mais informações, consulte [Uso de gráficos em Comunicações interativas](/help/forms/using/chart-component-interactive-communications.md). |
   | Fragmento do documento | Permite adicionar um componente reutilizável, como texto, lista ou condição, a uma Comunicação interativa. O componente adicionado pode ser baseado em modelo de dados de formulário ou sem um modelo de dados de formulário. |
   | Imagem | Permite inserir uma imagem. |

   Arraste e solte os componentes em sua Comunicação interativa e configure-os conforme necessário.

   Você também pode usar as operações de desfazer e refazer ao criar uma Comunicação interativa para os canais Imprimir e Web.

   Use a operação de desfazer para descartar a última ação executada e a operação de refazer para incorporar novamente a ação descartada. Por exemplo, se você tiver inserido uma imagem ou criado um vínculo de dados em uma Comunicação interativa e precisar descartá-la, use a operação desfazer.

   ![Desfazer ações Refazer](assets/undo_redo_actions_new.png)

   As opções de desfazer e refazer são exibidas na barra de ferramentas da página da interface do usuário de criação. A opção de desfazer é exibida somente após executar uma ação. A opção de refazer é exibida na barra de ferramentas da página somente após executar uma operação de desfazer. Essas ações são redefinidas na atualização da página.

1. Com o canal de impressão selecionado, vá para a função **[!UICONTROL Ativos]** e aplique o filtro para exibir somente os ativos que deseja visualizar.

   Usando o navegador Ativos, também é possível arrastar e soltar ativos diretamente nas áreas de destino da Comunicação interativa .

   ![assets-docfragments](assets/assets-docfragments.png)

1. Arraste e solte os fragmentos de documento na Comunicação interativa. A seguir estão os tipos de fragmentos de documento que você pode usar no canal de impressão da Comunicação interativa.

<table>
 <tbody>
  <tr>
   <td><strong>Tipo do fragmento do documento</strong></td>
   <td><strong>Exemplo de finalidade</strong></td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/texts-interactive-communications.md" target="_blank">Texto</a></td>
   <td>Texto para adicionar endereço, email do destinatário e texto do corpo da carta </td>
  </tr>
  <tr>
   <td><a href="/help/forms/using/conditions-interactive-communications.md" target="_blank">Condição</a></td>
   <td>Condição para adicionar a imagem de cabeçalho apropriada à comunicação com base no tipo da política: Standard ou Premium. <br /> </td>
  </tr>
  <tr>
   <td>Lista</td>
   <td>Grupo de fragmentos de documento, incluindo texto, condições, outras listas e imagens. <br /> </td>
  </tr>
 </tbody>
</table>

Você também pode substituir o vínculo entre uma área de destino e um fragmento de documento soltando o novo fragmento na área de destino usando o **[!UICONTROL Ativos]** guia . O sombreamento de cor azul da área de destino ao arrastar o fragmento indica que o fragmento do documento pode ser solto na área de destino.

Para obter mais informações sobre fragmentos de documento, consulte [Fragmentos de documento](/help/forms/using/document-fragments.md).

A interface de criação permite distinguir entre os campos não vinculados e vinculados e as variáveis em uma Comunicação interativa. A interface realça os campos não vinculados e as variáveis usando uma borda laranja.

![unbound_fields_variables_highlight_dc](assets/unbound_fields_variables_highlights_dc.jpg)

Além disso, ao passar o mouse sobre esses elementos, uma dica de ferramenta é exibida com a mensagem Campo (não vinculado) ou Variável (não vinculado).

Uma variável não vinculada usada em um fragmento de documento às vezes pode não ser exibida na interface de criação. Isso pode ocorrer devido a uma regra de texto em linha em um fragmento de documento ou no caso de um fragmento de condição. Nesses casos, uma dica de ferramenta, destacada em azul, é exibida como parte do fragmento do documento. A dica de ferramenta exibe o número de variáveis não vinculadas usadas em um fragmento de documento.

![Variável não vinculada](assets/df_unbound_variable_new.png)

Toque no fragmento do documento, toque em ![configure_icon](assets/configure_icon.png) (Configurar) e toque em **[!UICONTROL Propriedades]** do sidekick da Comunicação interativa. O **[!UICONTROL Variáveis e objetos do modelo de dados]** lista as variáveis, incluindo as variáveis ocultas, e os objetos de modelo de dados usados nos fragmentos de documento. Use o ![editar](assets/edit.svg) (Editar) ícone ao lado de cada objeto ou variável do modelo de dados para editar as propriedades.

1. Para configurar o vínculo de variáveis, toque em uma variável e selecione ![configure_icon](assets/configure_icon.png) (Configure) e configure as propriedades de vínculo no painel Propriedades na barra lateral.

   * **Nenhum**: O agente preencherá o valor da variável .
   * **Fragmento de texto**: Se selecionada, você pode procurar e selecionar um fragmento de documento de texto cujo conteúdo é renderizado no campo. Somente esses fragmentos de documento de texto podem ser vinculados a variáveis que não têm variáveis no .
   * **Objeto do Modelo de Dados**: Selecione uma propriedade de modelo de dados de formulário cujo valor é preenchido no campo .
   * **Valor padrão:** Você pode definir um valor padrão para a variável usando esse campo. O valor é exibido ao visualizar a Comunicação interativa ou na interface do usuário do agente.
   * **Padrão de exibição:** Também é possível definir um formato de exibição para uma variável. Selecione qualquer uma das opções predefinidas no **Tipo** lista suspensa para aplicar um formato de exibição a uma variável. Selecionar **Personalizado** para definir um padrão de exibição que não esteja disponível na lista. Para obter mais informações, consulte [Padrões de exibição de dados](../../forms/using/create-interactive-communication.md#datadisplaypatterns).

   Navegar para [Variáveis e objetos do modelo de dados](../../forms/using/create-interactive-communication.md#hiddenvariables) para configurar o vínculo de variáveis ocultas no fragmento do documento.

   Também é possível arrastar e soltar elementos de fonte de dados ou fragmentos de documento de texto para configurar o vínculo de variáveis.  Para criar um vínculo com qualquer um dos elementos da fonte de dados, selecione o **Fontes de dados** e arraste e solte o elemento no nome da variável. O elemento e a variável da fonte de dados devem ser do mesmo tipo para configurar o vínculo com êxito. Se você arrastar e soltar um elemento de fonte de dados em uma variável já vinculada, o novo elemento substituirá o anterior para criar um novo vínculo com a variável . Da mesma forma, selecione o **Ativos** e arraste e solte o fragmento do documento de texto no nome da variável para configurar o vínculo entre eles. O fragmento do documento de texto não deve conter variáveis.

1. Para adicionar uma tabela, com o canal de impressão selecionado, no **[!UICONTROL Ativos]** aplique o filtro para exibir somente os Fragmentos de layout. Arraste e solte o fragmento de layout necessário para a Comunicação interativa. Um fragmento de layout é baseado em um XDP e pode ser usado para criar layouts gráficos ou tabelas estáticas e dinâmicas no Interative Communication que são preenchidas com dados dinâmicos.

   Exemplo: Uma tabela de layout para exibir prêmio bruto, % de desconto de fidelidade e disponibilidade de assistência de emergência para políticas antigas e novas.

   Para obter mais informações sobre fragmentos de layout, consulte [Fragmentos de documento](/help/forms/using/document-fragments.md).

1. Com o canal de impressão selecionado, no **[!UICONTROL Ativos]** aplique o filtro para exibir imagens. Arraste e solte as imagens necessárias para a Comunicação interativa, como para o logotipo da empresa.

   Além disso, gerencie o seguinte na Comunicação interativa:

   * [Adição e configuração de gráficos](/help/forms/using/chart-component-interactive-communications.md)
   * [Sincronização do canal da Web com o canal de impressão](../../forms/using/create-interactive-communication.md#synchronize)

      * Sincronização automática
      * Cancelar herança
      * Reativar herança
      * Sincronizar
   * [Anexos e acesso à biblioteca](../../forms/using/create-interactive-communication.md#attachmentslibrary)
   * [Propriedades do campo XDP/Layout](../../forms/using/create-interactive-communication.md#xdplayoutfieldproperties)
   * [Adicionar regras aos componentes](../../forms/using/create-interactive-communication.md#rules)


1. Mudar para **[!UICONTROL Canal da Web]**. O canal da Web é exibido no editor de Comunicação interativa. Ao alternar do canal Impressão para o canal Web pela primeira vez, a sincronização automática ocorre. Para obter mais informações, consulte [Sincronização do canal da Web do canal de impressão](../../forms/using/create-interactive-communication.md#synchronize).

   Como estamos usando Imprimir como principal para a Web neste exemplo, os espaços reservados no canal Imprimir, o conteúdo e o vínculo de dados são sincronizados com o canal da Web. No entanto, você pode alterar e personalizar o conteúdo específico no canal da Web. [Cancelar herança](#cancelinheritance) para as áreas de destino e variáveis que foram geradas usando o canal de impressão para personalizar o conteúdo.

   ![webchannelassets](assets/webchannelassets.png)

   Toque no fragmento do documento, toque em ![configure_icon](assets/configure_icon.png) (Configurar) e toque em **[!UICONTROL Propriedades]** do sidekick da Comunicação interativa. O **[!UICONTROL Variáveis e objetos do modelo de dados]** lista as variáveis, incluindo as variáveis ocultas, e os objetos de modelo de dados usados nos fragmentos de documento. Use o ![editar](assets/edit.svg) (Editar) ícone ao lado de cada objeto ou variável do modelo de dados para editar as propriedades. Além disso, para fragmentos de documento que foram [gerado automaticamente](#synchronize) no canal da Web usando o canal Imprimir, use o ![cancelar herança](assets/cancelinheritance.png) Ícone (Cancelar herança) ao lado de cada objeto de modelo de dados e variável para [cancelar herança](#cancelinheritance) e para poder editá-las.

1. Para adicionar componentes adicionais ao canal da Web, com o canal da Web selecionado, toque em **[!UICONTROL Componentes]**. Arraste e solte componentes no canal da Web da Comunicação interativa, conforme necessário, e continue a configurá-los.

   | Componentes | Funcionalidade |
   |---|---|
   | Gráfico | Adiciona um gráfico que pode ser usado na Comunicação interativa para representação visual de dados bidimensionais recuperados de uma coleção de modelo de dados de formulário. Para obter mais informações, consulte [Uso do componente de gráfico](../../forms/using/chart-component-interactive-communications.md). |
   | Fragmento do documento | Permite adicionar um componente, texto, lista ou condição reutilizável a uma Comunicação interativa. O componente reutilizável adicionado a uma Comunicação interativa pode ser baseado em modelo de dados de formulário ou sem um modelo de dados de formulário. |
   | Imagem | Permite inserir uma imagem. |
   | Painel | Permite adicionar um [Painel](../../forms/using/create-interactive-communication.md#add-panel-component-to-the-web-channel) à comunicação interativa. |
   | Tabela | Adiciona uma tabela que permite organizar dados em linhas e colunas. |
   | Área de destino | Insere uma área de destino em um canal da Web para organizar os componentes específicos do canal da Web. A área de destino é um contêiner simples que permite agrupar componentes específicos de canais da Web. |
   | Texto | Adiciona rich text ao canal da Web de uma Comunicação interativa. O texto também pode usar objetos de modelo de dados de formulário para tornar o conteúdo dinâmico. |
   | Botão | Permite adicionar um [Botão](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) à comunicação interativa. Você pode usar o componente Botão para navegar para outras Comunicações interativas, formulários adaptáveis, outros ativos, como imagens ou fragmentos de documento, ou um URL externo. |
   | Separador | Permite inserir uma linha horizontal em uma Comunicação interativa. Use esse componente para distinguir entre seções em uma correspondência. Por exemplo, você pode usar o componente Separador para distinguir entre as seções Detalhes do cliente e Detalhes do cartão de crédito em uma declaração de cartão de crédito. |

1. Conforme necessário, insira ativos no canal da Web.

   Você pode [visualizar sua comunicação interativa](#previewic) para ver a aparência da impressão e dos resultados da Web da Comunicação interativa e continuar fazendo alterações, conforme necessário.

## Visualizar a comunicação interativa {#previewic}

Você pode usar o **Opção Visualizar** para avaliar a aparência da Comunicação interativa. O canal da Web de Comunicação interativa também fornece uma opção para Emular a experiência de uma Comunicação interativa para vários dispositivos. Por exemplo, iPhone, iPad e Desktop. Você pode usar ambos **Visualizar** e **Emulador** ![régua](assets/ruler.png) opções em conjunto entre si para visualizar as saídas da Web de dispositivos de tamanhos de tela diferentes. Os dados de amostra na visualização são preenchidos a partir do modelo de dados de formulários especificado.

1. Selecione o canal (impressão ou Web) para visualizar e toque em visualização. A Comunicação interativa é exibida.

   >[!NOTE]
   >
   >A visualização é preenchida com os dados de amostra do modelo de dados de formulário especificado. Para obter mais informações sobre como visualizar a Comunicação interativa com alguns outros dados ou usar o serviço de preenchimento prévio, consulte [Usar modelo de dados de formulário](/help/forms/using/using-form-data-model.md) e [Trabalhar com o modelo de dados de formulário](/help/forms/using/work-with-form-data-model.md).

1. Para o canal da Web, use ![régua](assets/ruler.png) para exibir a aparência da Comunicação interativa em vários dispositivos.

   ![webchannelpreview](assets/webchannelpreview.png)

Além disso, você pode [Preparar e enviar comunicação interativa usando a interface do usuário do agente](/help/forms/using/prepare-send-interactive-communication.md).

## Configurar propriedades no Interative Communication  {#configure-properties-in-interactive-communication}

### Anexos e acesso à biblioteca {#attachmentslibrary}

No canal Imprimir, você pode configurar os anexos e o acesso à biblioteca para permitir que o Agente gerencie anexos na interface do agente para a Comunicação interativa:

1. No canal Impressão, realce o Contêiner de documento e toque em **Propriedades**.

   ![documentcontainerproperties](assets/documentcontainerproperties.png)

   O painel Propriedades é exibido na barra lateral.

   ![propriedades, anexos](assets/propertiesattachments.png)

1. Expandir **Anexos** e especifique as seguintes propriedades:

   * **[!UICONTROL Permitir acesso à biblioteca]**: Selecione para habilitar o acesso da biblioteca para o agente na interface do usuário do agente. Se ativado, o Agente pode adicionar arquivos da biblioteca enquanto prepara a Comunicação interativa.
   * **[!UICONTROL Permitir Reordenação De Anexos]**: Selecione para permitir que o Agente reordene os anexos com a Comunicação interativa.
   * **[!UICONTROL Número Máximo De Anexos Permitidos]**: Especifique o número máximo de anexos permitidos com a Comunicação interativa.
   * **[!UICONTROL Arquivos a serem anexados]**: Toque **[!UICONTROL Adicionar]** e navegue para selecionar os arquivos a serem anexados e especifique o seguinte:

      * **[!UICONTROL Anexar este arquivo ao documento por padrão]**: É possível alterar essa opção se somente o anexo não for Obrigatório.
      * **[!UICONTROL Obrigatório:]** O agente não poderá remover o anexo na interface do agente.

   ![arquivos anexos](assets/attachfiles.png)

1. Toque **[!UICONTROL Concluído]**.

### Propriedades do campo XDP/Layout {#xdplayoutfieldproperties}

1. Ao editar o canal Imprimir de uma Comunicação interativa, passe o mouse sobre um campo, que é criado no modelo de canal Imprimir, e selecione ![configure_icon](assets/configure_icon.png) (Configurar).

   A caixa de diálogo Propriedades é exibida na barra lateral.

   ![data_display_pattern_fields](assets/data_display_patterns_fields.jpg)

1. Especifique o seguinte:

   * **[!UICONTROL Nome]**: Nome do nó JCR.
   * **[!UICONTROL Título]**: Insira um título que será visível para o Agente na interface do usuário do agente e na árvore Contêiner de documento.
   * **[!UICONTROL Tipo de vínculo]**: Selecione um dos seguintes tipos de vínculo para o campo .

      * Nenhum: O agente preencherá o valor da propriedade.
      * Fragmento de texto: Se selecionada, você pode procurar e selecionar um fragmento de documento de texto cujo conteúdo é renderizado no campo. Como alternativa, arraste e solte o fragmento do documento de texto no nome do campo para configurar o vínculo entre eles. O fragmento do documento de texto não deve conter variáveis.
      * Objeto do modelo de dados: Selecione uma propriedade de modelo de dados de formulário cujo valor é preenchido no campo . Como alternativa, selecione o **Fontes de dados** e arraste e solte a propriedade no campo.
   * **[!UICONTROL Valores padrão]**: O valor padrão garante que o campo não fique vazio quando não houver um valor fornecido pelo objeto de modelo de dados ou fragmento de texto especificado. Se o tipo de vínculo de dados for nenhum, o valor padrão será preenchido previamente no campo.
   * **[!UICONTROL Padrão de exibição]**: Também é possível definir um formato de exibição para um campo. Selecione qualquer uma das opções predefinidas no **Tipo** lista suspensa para aplicar um formato de exibição a um campo. Selecionar **Personalizado** para definir um padrão de exibição que não esteja disponível na lista. Para obter mais informações, consulte [Padrões de exibição de dados](../../forms/using/create-interactive-communication.md#datadisplaypatterns)

   * **[!UICONTROL Editável por agente]**: Selecione para permitir que o agente edite o valor no campo na interface do usuário do agente. Essa configuração não se aplica se o Tipo de vínculo for Fragmento de texto.
   * **[!UICONTROL Rótulo]**: Especifique uma sequência de texto exibida com o campo para o Agente na interface do usuário do agente. Essa configuração não se aplica se o Tipo de vínculo for Fragmento de texto.
   * **[!UICONTROL Dica de ferramenta]**: Insira uma string de texto que estará visível com o mouse sobre o Agente na interface do usuário do agente. Essa configuração não se aplica se o Tipo de vínculo for Fragmento de texto.
   * **[!UICONTROL Obrigatório]**: Selecione para tornar o campo obrigatório para o Agente. Essa configuração não se aplica se o Tipo de vínculo for Fragmento de texto.
   * **[!UICONTROL Permitir várias linhas]**: Selecione esse campo para permitir várias linhas de texto como entrada no campo. Essa configuração não se aplica se o Tipo de vínculo for Fragmento de texto.


1. Toque ![done_icon](assets/done_icon.png).

### Padrões de exibição de dados {#datadisplaypatterns}

A interface de criação permite definir padrões de exibição de dados para campos, variáveis e elementos de modelo de dados de formulário disponíveis ao criar uma Comunicação interativa para canais de impressão e da Web.

Para configurar o padrão de exibição de dados, toque no elemento, selecione ![configure_icon](assets/configure_icon.png) (Configurar) e configure o padrão de exibição no **[!UICONTROL Propriedades]** na barra lateral. Selecione qualquer opção predefinida no **[!UICONTROL Tipo]** lista suspensa para exibir o padrão associado ao tipo selecionado. Selecionar **[!UICONTROL Personalizado]** do **[!UICONTROL Tipo]** lista suspensa para definir um padrão que não esteja disponível na lista. Editar valores no **[!UICONTROL Padrão]** O campo modifica automaticamente o tipo para **[!UICONTROL Personalizado]**.

Para aplicar o padrão de exibição, o número de caracteres ou dígitos definidos no campo Padrão deve corresponder ou exceder os caracteres ou dígitos definidos no valor para campos, variáveis e elementos do modelo de dados de formulário. Para obter mais informações, consulte [exemplo](../../forms/using/create-interactive-communication.md#greaternumberofdigits).

![data_display_pattern_example](assets/data_display_patterns_ssn_new.png)

Você pode redefinir o padrão de exibição para um campo, variável ou um elemento de modelo de dados de formulário depois de gerar conteúdo da Web do canal de impressão. Como resultado, um elemento pode ter diferentes padrões de exibição definidos para canais de impressão e da Web. Se você não definir um padrão de exibição para um elemento em um canal de impressão e gerar conteúdo da Web automaticamente usando o canal de impressão, o vínculo de dados definido para o elemento em um canal de impressão definirá as opções de padrão de exibição disponíveis na variável **[!UICONTROL Tipo]** lista suspensa. Se não houver vínculo definido para o elemento, o tipo de dados do elemento definirá as opções de padrão de exibição disponíveis. Por exemplo, se você criar um vínculo de dados do tipo Number para um elemento no canal de impressão, as opções de padrão de exibição estarão disponíveis na variável **[!UICONTROL Tipo]** as listas suspensas são do tipo Number em vários formatos.

Alterne para **Visualizar** ou abra a interface do usuário do agente para exibir o padrão de exibição aplicado a esses elementos.

A tabela a seguir lista um exemplo dos valores exibidos como resultado da configuração do padrão de exibição de dados para uma variável:

| Tipo | Valor padrão | Padrão de exibição | Exibir valor | Descrição |
|---|---|---|---|---|
| SocialSecurityNumber | 123456789 | text{999-99-9999} | 123-45-6789 | O número de dígitos no campo de valor padrão corresponde ao número de dígitos no campo Padrão. O valor baseado no padrão é exibido com êxito. |
| SocialSecurityNumber | 1234567 | text{999-99-9999} | 1-23-4567 | O número de dígitos no campo de valor padrão é menor que o número de dígitos no campo Padrão. O padrão se aplica aos 7 dígitos disponíveis. |
| SocialSecurityNumber | 1234567890 | text{999-99-9999} | 1234567890 | O número de dígitos no campo de valor padrão é maior que o número de dígitos no campo Padrão. Como resultado, não há alteração no valor de exibição. |

Se um padrão de exibição não for especificado para uma variável ou um elemento de modelo de dados de formulário, a variável [configuração de fragmento de documento global](https://helpx.adobe.com//experience-manager/6-5/forms/using/interactive-communication-configuration-properties.html) é usada por padrão.

Se você não aplicar um padrão de exibição a uma variável do tipo de dados de número, a visualização de Impressão exibirá o padrão de acordo com a configuração global do fragmento do documento. Se você aplicar alterações na configuração padrão do fragmento de documento global, a interface do usuário do agente ainda exibirá o padrão de acordo com os separadores padrão definidos para a localidade.

Da mesma forma, para campos, se o padrão de exibição não for especificado, o padrão definido durante a criação do modelo Imprimir (XDP) será aplicado ao campo. Se não houver padrão ao criar o template de impressão, os padrões padrão baseados nas especificações XFA serão aplicados aos campos.

Além disso, se o padrão de exibição especificado estiver incorreto ou não puder ser aplicado, os padrões padrão baseados nas especificações XFA serão aplicados aos campos, variáveis ou elementos do modelo de dados de formulário.

## Aplicar regras aos componentes de Comunicação interativa {#rules}

Para condicionar componentes ou conteúdo na comunicação interativa, toque no componente/parte de conteúdo e selecione ![createruleicon](assets/createruleicon.png) (Criar regra) para iniciar o Editor de regras.

Para obter mais informações, consulte:

* [Editor de regras](/help/forms/using/rule-editor.md)
* [Introdução à criação de Comunicações interativas](/help/forms/using/introduction-interactive-communication-authoring.md)

## Uso de tabelas {#tables}

### Tabelas dinâmicas em comunicação interativa {#dynamic-tables-in-interactive-communication}

É possível adicionar tabelas dinâmicas em Comunicação interativa usando fragmentos de layout. As etapas a seguir usam um exemplo de declaração de cartão de crédito para ilustrar o uso de um fragmento de layout para criar uma tabela dinâmica em uma Comunicação interativa.

1. Verifique se o fragmento de layout necessário para criar a tabela está disponível no AEM.
1. No canal de impressão da Comunicação interativa, arraste e solte um fragmento de layout (com uma tabela de várias colunas) em uma Área de destino no navegador Ativo.

   ![lf_dragdrop](assets/lf_dragdrop.png)

   Uma tabela é exibida na área de layout Comunicação interativa .

   ![lf_dragdrop_table](assets/lf_dragdrop_table.png)

1. Especifique o vínculo de dados para cada uma das células da tabela. Para criar uma linha repetível, insira as propriedades do modelo de dados de formulário na linha pertencente a uma propriedade de coleção comum.

   1. Toque em uma célula na tabela e selecione ![configure_icon](assets/configure_icon.png) (Configurar).

      A caixa de diálogo Propriedades é exibida na barra lateral.

      ![lf_cell_properties](assets/lf_cell_properties.png)

   1. Configure as propriedades:

      * **[!UICONTROL Nome]**: Nome do nó JCR.
      * **[!UICONTROL Título]**: Insira um título que será visível no editor de Comunicação interativa.
      * **[!UICONTROL Tipo de vínculo]**: Selecione um dos seguintes tipos de vínculo para o campo .

         * **[!UICONTROL Nenhum]**
         * **[!UICONTROL Objeto do modelo de dados]**: O valor de uma propriedade do modelo de dados de formulário é preenchido no campo . Como alternativa, selecione o **Fontes de dados** e arraste e solte a propriedade no campo.
      * **[!UICONTROL Objeto do Modelo de Dados]**: A propriedade do modelo de dados de formulário cujo valor é preenchido no campo .
      * **[!UICONTROL Valor padrão]**: O valor padrão garante que o campo não fique vazio quando não houver um valor fornecido pelo objeto de modelo de dados especificado. O valor padrão é pré-preenchido no campo .

      * **[!UICONTROL Editável por agente]**: Selecione para permitir que o agente edite o valor no campo na interface do usuário do agente.
   1. Toque ![done_icon](assets/done_icon.png).



1. Visualize a Comunicação interativa para ver a tabela renderizada com os dados.

   ![lf_preview](assets/lf_preview.png)

### Tabelas somente de canal da Web {#webchanneltables}

Toque no painel raiz no modelo da Web e toque em **+** para adicionar uma **Tabela** para a Comunicação interativa. Uma tabela que inclui duas linhas é inserida na Comunicação interativa. A primeira linha da tabela representa o cabeçalho da Tabela.

#### Adicionar linhas e colunas à tabela {#addrowscolumnstable}

**Para adicionar ou excluir colunas:**

1. Toque na caixa de texto padrão na linha de cabeçalho da tabela para exibir a barra de ferramentas do componente.
1. Selecionar **Adicionar coluna** ou **Excluir coluna** para adicionar ou excluir colunas de tabela, respectivamente.

![component_toolbar_table1](assets/component_toolbar_table1.png)

**Para adicionar ou excluir linhas:**

1. Toque em qualquer linha da tabela para exibir a barra de ferramentas do componente. Você também pode selecionar uma linha de tabela usando o navegador Conteúdo no sidekick da Comunicação interativa.
1. Selecionar **Adicionar linha** ou **Excluir linha** para adicionar ou excluir linhas de tabela, respectivamente. Use o **Mover para cima** e **Mover para baixo** opções disponíveis na barra de ferramentas para reorganizar linhas na tabela.

![Component Toolbar](assets/component_toolbar_table_row_new.png)

**A.** Adicionar linha **B.** Excluir linha **C.** Mover para cima **D.** Mover para baixo

#### Adicionar ou editar texto nas células da tabela {#addedittexttable}

1. Selecione a caixa de texto padrão na célula da tabela e toque em ![editar](assets/edit.png) (Editar).
1. Digite o texto na célula da tabela e toque em ![done_icon](assets/done_icon.png) para salvá-lo.

#### Criar vínculo entre células de tabela e elementos de objeto do modelo de dados {#createbindingtablecells}

1. Selecione a caixa de texto padrão na linha da tabela e toque em ![editar](assets/edit.png) (Editar).
1. Toque na lista suspensa Objetos do Modelo de dados e selecione a propriedade.
1. Toque em para salvar e criar um vínculo entre a célula da tabela e a propriedade de objeto do modelo de dados.

![Criar vínculo de dados](assets/create_data_binding_table_new.png)

#### Criar um hiperlink para texto na célula da tabela {#createhyperlinktable}

1. Selecione a caixa de texto padrão na célula da tabela e toque em ![editar](assets/edit.svg) (Editar).
1. Selecione o texto na célula da tabela e toque no ícone Hiperlink.
1. Especifique o URL no **Caminho** campo.
1. Toque ![done_icon](assets/done_icon.png) para salvar as propriedades do hiperlink.

![Criar hiperlink](assets/create_hyperlink_table_new.png)

#### Criar tabelas dinâmicas {#createdynamictables}

Você pode criar uma tabela dinâmica somente de canal da Web em uma Comunicação interativa usando uma propriedade de modelo de dados de coleção do tipo . Essa tabela é uma representação das propriedades filhas de uma propriedade de coleção. É possível editar apenas as propriedades de formatação das várias células na tabela.

1. Alterne para o canal da Web e escolha exibir o navegador das Fontes de Dados.
1. Arraste e solte uma propriedade de coleção em um subformulário. Uma tabela é criada no subformulário.
1. Visualize a tabela na pré-visualização da Web da Comunicação interativa.

#### Classificar colunas em uma tabela {#sortcolumns}

Você pode classificar dados com base em qualquer coluna em uma tabela na Comunicação interativa. Os valores na coluna podem ser classificados em ordem crescente ou decrescente.

A classificação pode ser aplicada a colunas de tabelas contendo:

* Texto estático
* Propriedades do objeto do modelo de dados
* Combinação de propriedades de objetos de texto estático e de modelo de dados

Para ativar a classificação:

1. Selecione a tabela e toque em ![configure_icon](assets/configure_icon.png) (Configurar). Também é possível selecionar a tabela usando o **Conteúdo** no sidekick da Comunicação interativa.
1. Selecionar **Habilite Classificação.**
1. Toque ![done_icon](assets/done_icon.png) para salvar as propriedades da tabela. Os ícones de classificação, setas para cima e para baixo, em cabeçalhos de colunas representam que a classificação foi ativada.

   ![Habilitar classificação](assets/enable_sorting_new-1.png)

1. Alterne para **Visualizar** para visualizar a saída. A tabela é automaticamente classificada com base na primeira coluna da tabela.
1. Clique no cabeçalho da coluna para classificar os valores com base na coluna.

   Um cabeçalho de coluna com uma seta para cima representa que:

   * A tabela é classificada com base nessa coluna.
   * na coluna são exibidos na ordem crescente.

   ![Classificação crescente](assets/sorting_ascending_new-1.png)

   Da mesma forma, um cabeçalho de coluna com uma seta para baixo representa que os valores na coluna são exibidos na ordem decrescente.

## Editar propriedades de comunicação interativa {#edit-interactive-communication-properties}

Depois de criar uma Comunicação interativa, você pode editar suas propriedades em um estágio posterior.

Use o **Propriedades** página para:

* Edite os valores dos campos especificados durante a criação da Comunicação interativa, como Título e Descrição.
* Adicione ou exclua um canal da Web para uma Comunicação interativa existente.
* Visualizar, baixar ou excluir a Comunicação interativa
* Abra o [Interface do usuário do agente](/help/forms/using/prepare-send-interactive-communication.md).

Para acessar o **Propriedades** página:

1. Faça logon na instância do autor do AEM e navegue até **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents**.
1. Selecione a Comunicação interativa e toque em **Propriedades**.
1. Selecione o **Geral** para editar a guia **Título** e **Descrição** campos.

### Adicionar ou excluir o canal da Web {#add-or-delete-the-web-channel}

Execute as etapas a seguir para adicionar o canal da Web a uma Comunicação interativa existente:

1. No **Propriedades** selecione o **Canais** guia .
1. Selecione o **Web** e selecione um template para o canal da Web.
1. Selecionar **Usar Imprimir como Principal para Canal da Web** para habilitar a sincronização entre o canal da Web e o canal de impressão.
1. Toque **Salvar e fechar** para salvar as alterações.

   Da mesma forma, é possível tocar no botão **Web** na caixa de seleção **Canais** para excluir o canal Web da Comunicação interativa.

## Componente Adicionar botão ao canal da Web {#add-button-component-to-the-web-channel}

É possível adicionar um botão como um componente ao canal da Web da Comunicação interativa. Defina as regras usando o [editor de regras](../../forms/using/rule-editor.md) para poder navegar para outras Comunicações interativas, formulários adaptáveis, outros ativos, como imagens ou fragmentos de documento, ou um URL externo no toque do botão.

Para adicionar um botão e definir regras nele:

1. Toque no painel raiz no modelo da Web e toque em **+** para adicionar o **Botão** para a Comunicação interativa.
1. Toque no componente de botão e toque em ![editar regras](assets/edit-rules.png) para definir regras no toque do botão.
1. No **When** seção , selecione **clicado** no estado da lista suspensa de botões.
1. No **Então** seção:

   1. Selecione uma ação na lista suspensa. Por exemplo, selecione **Navegar para** como o tipo de ação.

   1. Especifique o URL da Comunicação interativa, formulário adaptável, um ativo ou uma página da Web. Por exemplo, especifique o URL no seguinte formato para navegar para outra Comunicação interativa: https://&lt;server-name>:&lt;port>/editor.html/content/forms/af/&lt;interactive communication=&quot;&quot; name=&quot;&quot;>/channels/&lt;channel name=&quot;&quot; print=&quot;&quot; or=&quot;&quot; web=&quot;&quot;>.html
   1. Especifique a opção para abrir o ativo na mesma guia, nova guia ou nova janela.
   1. Toque **Concluído** em seguida, toque em **Fechar** para salvar a regra.

   Da mesma forma, é possível selecionar outras opções disponíveis na lista suspensa tipo de ação, como Chamar serviço e Enviar formulário. Para obter mais informações, consulte [editor de regras](../../forms/using/rule-editor.md).

1. Visualize a Comunicação interativa e toque no botão para exibir a Comunicação interativa, o formulário adaptável, um ativo ou uma página da Web especificada na etapa 4(b).

## Adicionar o componente Painel ao canal da Web {#add-panel-component-to-the-web-channel}

O componente Painel é um espaço reservado para agrupar outros componentes e controla como um grupo de componentes, como acordeão e guias, é apresentado na Comunicação interativa. Um componente de painel também permite tornar um grupo de componentes repetíveis para o usuário final, como em várias entradas necessárias para preencher as credenciais educacionais.

Execute as etapas a seguir para adicionar um componente Painel ao canal da Web:

1. Insira o **Painel** no canal da Web usando qualquer uma das seguintes opções:

   * Toque em um componente, toque em **+** e selecione o **Painel** componente.

   * No **Componente** painel do navegador, arraste e solte o **Painel** componente na Comunicação interativa.

   * Toque no **Painel** no **Conteúdo** painel do navegador e toque **Adicionar painel filho**. Selecionar o **Adicionar painel filho** exibe a **Adicionar painel filho** caixa de diálogo. Insira o título e uma descrição e nome opcionais para o componente Painel .

1. Toque no painel do **Conteúdo** navegador para executar ações adicionais no Painel, como configurar, editar regras, copiar, excluir e inserir componente.

   Você também pode arrastar e soltar um painel dentro do **Conteúdo** navegador para refletir a alteração na estrutura da Comunicação interativa no painel direito.

## Sincronização do canal da Web com o canal de impressão {#synchronize}

Ao selecionar Imprimir como Principal para Canal da Web ao criar uma Comunicação Interativa, o canal da Web é criado em sincronia com o canal Imprimir e o conteúdo e o vínculo de dados do canal da Web são derivados do canal de impressão e as alterações feitas no canal de impressão podem ser refletidas no canal da Web quando você toca em Sincronizar.

Os autores, no entanto, têm permissão para quebrar a herança de componentes no canal da Web, conforme necessário.

![Criar impressão Principal](assets/create_ic_print_master_new-1.png) ![Imprimir Web Principal](assets/create_ic_print_master_web_new-1.png)

### Sincronização automática {#autosync}

Se você selecionar a variável **[!UICONTROL Usar Imprimir como Principal para Canal da Web]** , você pode selecionar qualquer um dos seguintes modos para gerar o canal da Web:

* **[!UICONTROL Layout automático]**: Selecione esse modo para gerar automaticamente espaços reservados, conteúdo e vínculo de dados para o canal da Web do canal de Impressão.
* **[!UICONTROL Organizar manualmente]**: Selecione esse modo para selecionar e adicionar manualmente os elementos do canal de impressão ao canal da Web usando o conteúdo principal disponível na guia Fontes de dados . Para obter mais informações, consulte [Selecione Print channel elements para criar o conteúdo do canal da Web](#selectprintchannelelements).

![Criar opções de IC](assets/create_ic_options_updated_new.png)

>[!NOTE]
>
>A sincronização dos canais sincroniza apenas os fragmentos de documento, imagens, condições, listas e fragmentos de layout do canal de impressão para o canal da Web. Os subformulários ou nós primários que incluem esses elementos não são sincronizados.

### Selecione Print channel elements para criar o conteúdo do canal da Web {#selectprintchannelelements}

Se você selecionar Imprimir como principal ao criar a Comunicação interativa e não selecionar a opção de sincronização automática, também poderá arrastar e soltar elementos do canal de Impressão na interface de criação do canal da Web.

Navegar para **Fontes de dados** > **Conteúdo principal** para exibir os elementos Print channel . Arraste e solte as áreas, campos ou tabelas de destino na interface de criação do canal da Web. Um ícone de círculo azul ao lado do nome do elemento indica que o elemento Canal de impressão já foi incluído no canal da Web.

![Conteúdo principal](assets/master_content.png)

### Cancelar herança {#cancelinheritance}

No canal da Web, os componentes são incorporados nas áreas de destino.

Passe o mouse sobre a área de destino ou variável relevante no canal da Web e selecione ![cancelar herança](assets/cancelinheritance.png) (Cancelar herança) e, na caixa de diálogo Cancelar herança, toque em **[!UICONTROL Sim]**.

A herança dos componentes na área de destino é cancelada e agora você pode editá-los conforme necessário.

### Reativar herança {#re-enable-inheritance}

No canal da Web, se você cancelou a herança de um componente, é possível reativá-la. Para reativar a herança, passe o mouse sobre o limite da área de destino relevante, que inclui o componente, e toque em ![reabilitar herança](assets/reenableinheritance.png).

A caixa de diálogo Reverter herança é exibida.

![revertinheridade](assets/revertinheritance.png)

Se necessário, selecione **[!UICONTROL Sincronizar A Página Após Reverter A Herança]**. Selecione esta opção para sincronizar toda a comunicação interativa. Se você não selecionar essa opção, somente a área de destino relevante será sincronizada ao restabelecer a herança.

Toque **[!UICONTROL Sim]**.

### Sincronizar {#synchronize-1}

Se estiver usando Imprimir como Principal para Canal da Web e fizer alterações no canal Imprimir, você poderá sincronizar o conteúdo para trazer as alterações recém-feitas para o canal da Web.

1. Para sincronizar o canal Web com o canal Imprimir, alterne para o canal Web e toque no ícone Mais opções.

   ![Opções de sincronização automática](assets/auto_sync_options_new.png)

1. Toque em uma das seguintes opções:

   * **[!UICONTROL Sincronizar com Imprimir]**: Sincroniza o conteúdo somente das áreas de destino nas quais a herança não é cancelada.
   * **[!UICONTROL Redefinir]**: Sincroniza o conteúdo do canal da Web com o canal Imprimir e descarta todas as alterações feitas no canal da Web.

### Use a barra de ferramentas do componente para executar ações em componentes herdados {#componenttoolbar}

Depois de ter o conteúdo gerado automaticamente no canal da Web usando a opção Sincronizar, você pode executar mais ações nos componentes sem cancelar a herança.

![Component Toolbar](assets/component_toolbar_inherited_web_new.png)

Toque no componente para exibir as seguintes opções:

* **Copiar:** Copie um componente e cole-o em outros locais na Comunicação interativa.
* **Recortar:** Mova um componente de um local para outro na Comunicação interativa.
* **Inserir componente:** Insira um componente acima do componente selecionado.
* **Colar:** Cole o componente recortado ou copiado usando as opções descritas acima.
* **Grupo:** Selecione vários componentes se quiser cortar, copiar ou colar mais de um componente.
* **Pai:** Selecione o pai de um componente.
* **Exibir expressão SOM:** Visualize o [Expressão SOM](../../forms/using/using-som-expressions-adaptive-forms.md) para o componente.

* **Agrupar objetos no painel:** Agrupe os componentes em um painel para poder executar operações nesses componentes simultaneamente. Para obter detalhes, consulte [Agrupar objetos no Painel](#groupobjectspanel).

* **Cancelar herança:** [Cancelar a herança](#cancelinheritance) dos componentes dentro da área de destino para editá-los.

### Agrupar objetos no Painel {#groupobjectspanel}

A interface de criação do canal da Web facilita o agrupamento dos componentes em um painel para poder executar operações nesses componentes simultaneamente. O **Conteúdo** lista os componentes agrupados como elementos filho do painel na árvore de conteúdo.

1. Toque em um componente e selecione o Grupo ( ![grupo](assets/group.jpg)).
1. Selecionar vários componentes e tocar **Agrupar objetos no Painel**.

   ![Agrupar objetos](assets/component_toolbar_group_objects_new.png)

1. No **Agrupar objetos no painel** digite um nome para o Painel.
1. Insira um título e uma descrição opcionais para o Painel.
1. Clique em ![marcador_marcador](assets/bullet_checkmark.png).

   Os componentes agrupados são exibidos como elementos filhos do Painel na árvore de conteúdo.

   ![content_tree_grouping](assets/content_tree_grouping.png)

## Formato de saída para o canal de impressão {#output-format-print-channel}

Use a API PrintChannel para definir o formato de saída para o canal Print de uma Comunicação interativa. Se você não definir um formato de saída, o AEM Forms gera a saída no formato PDF.

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
PrintDocument printDocument = printChannel.render(renderOptions);
```

Para gerar a saída em qualquer outro formato, especifique o tipo de formato de saída. Consulte [API PrintChannel](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/PrintConfig.html) para a lista de tipos de formatos de saída suportados.

Por exemplo, você pode usar a seguinte amostra para definir PCL como formato de saída para uma Comunicação interativa:

```javascript
//options for rendering print channel of a multi-channel document
PrintChannelRenderOptions renderOptions = new PrintChannelRenderOptions();
renderOptions.setRenderFormat(PrintConfig.HP_PCL_5e);
PrintDocument printDocument = printChannel.render(renderOptions);
```
