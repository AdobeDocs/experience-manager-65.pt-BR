---
title: 'Tutorial: Criar modelos'
description: Criar modelos de impressão e da Web para a comunicação interativa
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 1%

---

# Tutorial: Criar modelos{#tutorial-create-templates}

![07-aplicar-regras-ao-formulário-adaptável_pequeno](assets/07-apply-rules-to-adaptive-form_small.png)

Este tutorial é uma etapa da série [Criar sua primeira Comunicação Interativa](/help/forms/using/create-your-first-interactive-communication.md). É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

Para criar uma comunicação interativa, você deve ter modelos disponíveis no servidor AEM para impressão e canais da Web.

Os modelos para o canal de impressão são criados no Adobe Forms Designer e carregados no servidor de AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os templates para o canal da Web são criados no AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Este tutorial o guiará pelas etapas para criar modelos para canais de Impressão e da Web, de modo que fiquem disponíveis para uso durante a criação de Comunicações interativas. Ao final deste tutorial, você será capaz de:

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Fazer upload dos modelos XDP para o servidor do AEM Forms
* Criar e habilitar modelos para o canal da Web

## Criar modelo para canal de impressão {#create-template-for-print-channel}

Crie e gerencie um modelo para o canal de impressão de comunicação interativa usando as seguintes tarefas:

* [Criar um modelo XDP usando o Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Fazer upload de um modelo XDP para o servidor do AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Criar um modelo XDP para fragmentos de layout](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Criar um modelo XDP usando o Forms Designer {#create-xdp-template-using-forms-designer}

Com base no [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e na [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes subformulários no modelo XDP:

* Detalhes da Lista: Inclui um Fragmento de Documento
* Detalhes do cliente: inclui um fragmento de documento
* Sumário da Lista: Inclui um Fragmento de Documento
* Sumário: Inclui um Fragmento de Documento (subformulário Encargos) e um gráfico (subformulário Gráficos)
* Chamadas discriminadas: inclui uma tabela (fragmento de layout)
* Pagar agora: inclui uma imagem
* Serviços de valor agregado: inclui uma imagem

![criar_modelo_de_impressão](assets/create_print_template.gif)

Esses subformulários são exibidos como áreas de destino no modelo de Impressão depois de fazer upload do arquivo XDP para o servidor do Forms. Todas as entidades, como fragmentos de documento, gráficos, fragmentos de layout e imagens, são adicionadas às áreas de destino ao criar a Comunicação interativa.

Para criar um modelo XDP para o canal de impressão, faça o seguinte:

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Usar um formulário em branco**, selecione **Avançar** e **Concluir** para abrir o formulário para criação de modelo.

   Verifique se as opções **Biblioteca de Objetos** e **Objeto** estão selecionadas no menu **Janela**.

1. Arraste e solte o componente **Subformulário** da **Biblioteca de Objetos** no formulário.
1. Selecione o subformulário para que você possa ver as opções do subformulário na janela **Objeto** no painel direito.
1. Selecione a guia **Subformulário** e selecione **Fluxo** na lista suspensa **Conteúdo**. Para ajustar o comprimento, arraste a extremidade esquerda do subformulário.
1. Na guia **Ligações**:

   1. Especifique **BillDetails** no campo **Name**.

   1. Selecione **Nenhuma associação de dados** na lista suspensa **Associação de Dados**.

   ![Subformulário do Designer](assets/forms_designer_subform_new.png)

1. Da mesma forma, selecione o subformulário raiz, selecione a guia **Subformulário** e selecione **Fluxado** na lista suspensa **Conteúdo**. Na guia **Ligações**:

   1. Especifique **TelecaBill** no campo **Name**.

   1. Selecione **Nenhuma associação de dados** na lista suspensa **Associação de Dados**.

   ![Subformulário para modelo de impressão](assets/root_subform_print_template_new.png)

1. Repita as etapas 2 - 5 para criar os seguintes subformulários:

   * Detalhes da Fatura
   * DetalhesDoCliente
   * Resumo da fatura
   * Resumo - Selecione a guia **Subformulário** e selecione **Posicionado** na lista suspensa **Conteúdo** para este subformulário. Insira os seguintes subformulários no subformulário **Resumo**.

      * Encargos
      * Gráficos

   * ChamadasDiscriminadas
   * PayNow
   * ValueAddedServices

   Para economizar tempo, também é possível copiar e colar subformulários existentes para criar subformulários adicionais.

   Para deslocar o subformulário **Gráficos** para a direita do subformulário Encargos, selecione o subformulário **Gráficos** no painel esquerdo, selecione a guia **Layout** e especifique um valor para o campo **AnchorX**. O valor deve ser maior que o valor do campo **Largura** para o subformulário **Encargos**. Selecione o subformulário **Encargos** e selecione a guia **Layout** para exibir o valor do campo **Largura**.

1. Arraste e solte o objeto **Texto** da **Biblioteca de Objetos** no formulário e insira o texto **Discar XXXX para assinar** na caixa.
1. Clique com o botão direito do mouse no objeto de texto no painel esquerdo, selecione **Renomear Objeto** e insira o nome do objeto de texto como **Assinar**.

   ![Modelo XDP](assets/print_xdp_template_subform_new.png)

1. Selecione **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local onde você pode salvar o arquivo e especifique o nome como **create_first_ic_print_template**.
   1. Selecione **.xdp** na lista suspensa **Salvar como tipo**.

   1. Selecione **Salvar**.

### Fazer upload de um modelo XDP para o servidor do AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Depois de criar um modelo XDP usando o Forms Designer, você deve carregá-lo no AEM Forms Server para que o modelo fique disponível para uso ao criar a Comunicação interativa.

1. Selecione **[!UICONTROL Forms]** > **[!UICONTROL Forms e Documentos]**.
1. Selecione **Criar** > **Carregar arquivo**.

   Navegue e selecione o **create_first_ic_print_template** template (XDP) e selecione **Abrir** para importar o modelo XDP para o AEM Forms Server.

### Criar um modelo XDP para fragmentos de layout {#create-xdp-template-for-layout-fragments}

Para criar um fragmento de layout para o canal de impressão da comunicação interativa, crie um XDP usando o Forms Designer e faça upload dele para o servidor do AEM Forms.

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Usar um formulário em branco**, selecione **Avançar** e **Concluir** para abrir o formulário para criação de modelo.

   Verifique se as opções **Biblioteca de Objetos** e **Objeto** estão selecionadas no menu **Janela**.

1. Arraste e solte o componente **Tabela** da **Biblioteca de Objetos** no formulário.
1. Na caixa de diálogo Inserir tabela:

   1. Especifique o número de colunas como **5**.
   1. Especifique o número de linhas do corpo como **1**.
   1. Marque a caixa de seleção **Incluir linha de cabeçalho na tabela**.
   1. Guia **OK**.

1. Selecione **+** no painel esquerdo ao lado de **Tabela** 1 e clique com o botão direito em **Célula1** e selecione **Renomear Objeto** para **Data**.

   Da mesma forma, renomeie **Célula2**, **Célula3**, **Célula4** e **Célula5** para **Hora**, **Número**, **Duração** e **Encargos**, respectivamente.

1. Clique nos campos de texto do Cabeçalho no **Modo de Exibição do Designer** e renomeie-os como **Hora**, **Número**, **Duração** e **Encargos**.

   ![Fragmento do layout](assets/layout_fragment_print_new.png)

1. Selecione **Linha 1** no painel esquerdo e selecione **Objeto** > **Associação** > **Repetir Linha para Cada Item de Dados**.

   ![Repetir propriedades do fragmento de layout](assets/layout_fragment_print_repeat_new.png)

1. Arraste e solte o componente **Campo de Texto** da **Biblioteca de Objetos** na **Exibição do Designer**.

   ![Campo de texto do fragmento de layout](assets/layout_fragment_print_text_field_new.png)

   Da mesma forma, arraste e solte o componente **Campo de Texto** nas linhas **Hora**, **Número**, **Duração** e **Encargos**.

1. Selecione **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local onde você pode salvar o arquivo e especifique o nome como **table_lf**.
   1. Selecione **.xdp** na lista suspensa **Salvar como tipo**.

   1. Selecione **Salvar**.

   Depois de criar um modelo XDP para fragmento de layout usando o Forms Designer, você deve [carregá-lo](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) no AEM Forms Server para que o modelo fique disponível para uso durante a criação de fragmentos de layout.

## Criar um modelo para o canal da Web {#create-template-for-web-channel}

Crie e gerencie um modelo para o canal da Web de Comunicação Interativa usando as seguintes tarefas:

* [Criar pasta para modelos](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Criar o modelo](../../forms/using/create-templates-print-web.md#create-the-template)
* [Ativar o modelo](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Ativação de botões nas Comunicações interativas](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Criar uma pasta para modelos {#create-folder-for-templates}

Para criar um modelo de canal da Web, defina uma pasta onde você possa salvar os modelos criados. Depois de criar um modelo dentro dessa pasta, ative o modelo para permitir que os usuários de formulários criem um canal da Web de uma Comunicação interativa com base no modelo.

Para criar uma pasta para os modelos editáveis, faça o seguinte:

1. Selecione **Ferramentas** ![ícone-martelo](assets/hammer-icon.svg) > **Navegador de Configuração**.
   * Consulte a documentação do [Navegador de Configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Na página Navegador de Configuração, selecione **Criar**.
1. Na caixa de diálogo **Criar Configuração**, especifique **Create_First_IC_templates** como o título da pasta, marque **Modelos Editáveis** e selecione **Criar**.

   ![Configurar modelos da Web](assets/create_first_ic_web_template_new.png)

   A pasta **Create_First_IC_templates** foi criada e listada na página **Navegador de Configuração**.

### Criar o modelo {#create-the-template}

Com base no [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e na [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes painéis no modelo da Web:

* Detalhes da Lista: Inclui um Fragmento de Documento
* Detalhes do cliente: inclui um fragmento de documento
* Sumário da Lista: Inclui um Fragmento de Documento
* Resumo de Encargos: inclui um Fragmento de Documento e um gráfico (layout de duas colunas)
* Chamadas Discriminadas: Inclui uma tabela
* Pagar Agora: Inclui um botão **Pagar Agora** e uma imagem
* Serviços de valor agregado: inclui uma imagem e um botão **Assinar**.

![criar_modelo_da_Web](assets/create_web_template.gif)

Todas as entidades, como fragmentos de documento, gráficos, tabelas, imagens e botões, são adicionadas ao criar a Comunicação interativa.

Para criar um modelo para o canal Web na pasta **Create_First_IC_templates**, siga estas etapas:

1. Navegue até a pasta de modelo apropriada, selecionando a pasta **Ferramentas** > **Modelos** > **Criar_Primeiro_Modelos**.
1. Selecione **Criar**.
1. No assistente de configuração **Escolher um Tipo de Modelo**, selecione **Comunicação Interativa - Canal da Web** e selecione **Avançar**.
1. No assistente de configuração de **Detalhes do Modelo**, especifique **Create_First_IC_Web_Template** como o título do modelo. Especifique uma descrição opcional e selecione **Criar**.

   Uma mensagem de confirmação de que o **Create_First_IC_Web_Template** é exibida.

1. Selecione **Abrir** para abrir o modelo no editor de modelos.
1. Selecione **Conteúdo inicial** na lista suspensa ao lado da opção **Visualizar**.

   ![Editor de modelo](assets/template_editor_initial_content_new.png)

1. Selecione **Painel Raiz** e **+** para exibir a lista de componentes que você pode adicionar ao modelo.
1. Para adicionar um painel acima do **Painel raiz**, selecione **Painel** na lista.
1. Selecione a guia **Conteúdo** no painel esquerdo. O novo painel adicionado na etapa 8 é exibido no **Painel raiz** da árvore de conteúdo.

   ![Árvore de conteúdo](assets/content_tree_root_panel_new.png)

1. Selecione o painel e selecione ![configure_icon](assets/configure_icon.png) (Configurar).
1. No painel Propriedades:

   1. Especifique **billdetails** no campo Nome.
   1. Especifique **Detalhes da Lista** no campo Título.
   1. Selecione **1** na lista suspensa **Número de Colunas**.

   1. Para salvar as propriedades, selecione ![Salvar](/help/forms/using/assets/done_icon.png).

   O nome do painel foi atualizado para **Detalhes da Lista** na árvore de conteúdo.

1. Repita as etapas 7 - 11 para adicionar painéis com as seguintes propriedades ao modelo:

   | Nome | Título | Número de colunas |
   |---|---|---|
   | customerdetails | Detalhes do cliente | 1 |
   | resumo de faturamento | Sumário da Lista | 1 |
   | encargos resumidos | Resumo de Encargos | 2 |
   | itemisedcalls | Chamadas discriminadas | 1 |
   | paynow | Pagar agora | 2 |
   | vas | Serviços de valor agregado | 1 |

   A imagem a seguir representa a árvore de conteúdo após adicionar todos os painéis ao modelo:

   ![Árvore de conteúdo para todos os painéis](assets/content_tree_all_panels_new.png)

### Ativar o modelo {#enable-the-template}

Depois de criar o modelo da Web, você deve habilitá-lo para usar o modelo ao criar a Comunicação interativa.

Para habilitar o modelo da Web, faça o seguinte:

1. Selecione **Ferramentas** ![ícone de martelo](assets/hammer-icon.svg) > **Modelos**.
1. Navegue até o modelo **Create_First_IC_Web_Template**, selecione-o e **Enable**.
1. Selecione **Habilitar** novamente para confirmar.

   O modelo é ativado e seu status é exibido como Enabled. Você pode usar esse template ao criar a Comunicação interativa para o canal da Web.

### Ativação de botões nas Comunicações interativas {#enabling-buttons-in-interactive-communications}

Com base no caso de uso, você deve incluir os botões **Pagar agora** e **Assinar** (componentes de formulários adaptáveis) na Comunicação interativa. Para habilitar o uso desses botões na Comunicação interativa, faça o seguinte:

1. Selecione **Estrutura** na lista suspensa ao lado da opção **Visualizar**.
1. Selecione o painel raiz do **Contêiner de documentos** usando a árvore de conteúdo e selecione **Política** para selecionar os componentes permitidos para uso na comunicação interativa.

   ![Configurar política](assets/structure_configure_policy_new.png)

1. Na guia **Componentes Permitidos** da seção **Propriedades**, selecione **Botão** nos componentes do **Formulário Adaptável**.

   ![Componentes permitidos](assets/allowed_components_af_new.png)

1. Para salvar as propriedades, selecione ![salvar](assets/done_icon.png).
