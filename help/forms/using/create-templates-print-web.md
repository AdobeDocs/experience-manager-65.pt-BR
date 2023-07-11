---
title: "Tutorial: Criar modelos"
seo-title: Create Print and Web templates for Interactive Communication
description: Criar modelos de impressão e da Web para a comunicação interativa
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 0%

---

# Tutorial: Criar modelos{#tutorial-create-templates}

![07-aplicar-regras-ao-formulário-adaptável_pequeno](assets/07-apply-rules-to-adaptive-form_small.png)

Este tutorial é uma etapa da [Criar a primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso completo do tutorial.

Para criar uma comunicação interativa, você deve ter modelos disponíveis no servidor AEM para impressão e canais da Web.

Os modelos para o canal de impressão são criados no Adobe Forms Designer e carregados no servidor AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os templates para o canal da Web são criados no AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Este tutorial o guiará pelas etapas para criar modelos para canais de Impressão e da Web, de modo que fiquem disponíveis para uso durante a criação de Comunicações interativas. Ao final deste tutorial, você será capaz de:

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Fazer upload dos modelos XDP para o servidor do AEM Forms
* Criar e habilitar modelos para o canal da Web

## Criar modelo para canal de impressão {#create-template-for-print-channel}

Crie e gerencie o modelo para o canal de impressão de comunicação interativa usando as seguintes tarefas:

* [Criar modelo XDP usando o Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Fazer upload do modelo XDP para o servidor do AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Criar modelo XDP para fragmentos de layout](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Criar modelo XDP usando o Forms Designer {#create-xdp-template-using-forms-designer}

Com base no [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes subformulários no modelo XDP:

* Detalhes da lista: inclui um fragmento de documento
* Detalhes do cliente: inclui um fragmento de documento
* Resumo da Lista: Inclui um fragmento de documento
* Resumo: inclui um fragmento de documento (subformulário Encargos) e um gráfico (subformulário Gráficos)
* Chamadas discriminadas: inclui uma tabela (fragmento de layout)
* Pagar agora: inclui uma imagem
* Serviços de valor agregado: inclui uma imagem

![create_print_template](assets/create_print_template.gif)

Esses subformulários são exibidos como áreas de destino no modelo de Impressão depois de fazer upload do arquivo XDP para o servidor do Forms. Todas as entidades, como fragmentos de documento, gráficos, fragmentos de layout e imagens, são adicionadas às áreas de destino ao criar a Comunicação interativa.

Execute as seguintes etapas para criar um modelo XDP para o canal de impressão:

1. Abra o Forms Designer e selecione **Arquivo** > **Novo** > **Use um formulário em branco,** toque **Próxima** e toque em **Concluir** para abrir o formulário para criação de modelo.

   Certifique-se de que o **Biblioteca de objetos** e **Objeto** opções são selecionadas no **Janela** menu.

1. Arraste e solte a variável **Subformulário** componente do **Biblioteca de objetos** ao formulário.
1. Selecione o subformulário para exibir as opções do subformulário no **Objeto** no painel direito.
1. Selecione o **Subformulário** e selecione **Fluxado** do **Conteúdo** lista suspensa. Arraste a extremidade esquerda do subformulário para ajustar o comprimento.
1. No **Associações** guia:

   1. Especificar **Detalhes da Fatura** no **Nome** campo.

   1. Selecionar **Sem associação de dados** do **Vinculação de dados** lista suspensa.

   ![Subformulário do designer](assets/forms_designer_subform_new.png)

1. Da mesma forma, selecione o subformulário raiz, selecione o **Subformulário** e selecione **Fluxado** do **Conteúdo** lista suspensa. No **Associações** guia:

   1. Especificar **TelecaBill** no **Nome** campo.

   1. Selecionar **Sem associação de dados** do **Vinculação de dados** lista suspensa.

   ![Subformulário para modelo de impressão](assets/root_subform_print_template_new.png)

1. Repita as etapas 2 - 5 para criar os seguintes subformulários:

   * Detalhes da Fatura
   * DetalhesDoCliente
   * Resumo da fatura
   * Resumo - Selecione o **Subformulário** e selecione **Posicionado** do **Conteúdo** lista suspensa para este subformulário. Insira os seguintes subformulários na **Resumo** subformulário.

      * Encargos
      * Gráficos

   * ChamadasDiscriminadas
   * PayNow
   * ValueAddedServices

   Para economizar tempo, também é possível copiar e colar subformulários existentes para criar novos subformulários.

   Para deslocar o **Gráficos** à direita do subformulário Encargos, selecione o **Gráficos** subformulário no painel esquerdo, selecione a **Layout** e especifique um valor para **ÂncoraX** campo. O valor deve ser maior do que o valor de **Largura** campo para o **Encargos** subformulário. Selecione o **Encargos** subformulário e selecione o **Layout** para exibir o valor da variável **Largura** campo.

1. Arraste e solte a variável **Texto** objeto do **Biblioteca de objetos** ao formulário e insira o **Disque XXXX para assinar** texto na caixa.
1. Clique com o botão direito do mouse no objeto de texto no painel esquerdo e selecione **Renomear objeto** e insira o nome do objeto de texto como **Assinar**.

   ![Modelo XDP](assets/print_xdp_template_subform_new.png)

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local em que o arquivo será salvo e especifique o nome como **create_first_ic_print_template**.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.

### Fazer upload do modelo XDP para o servidor do AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Depois de criar um modelo XDP usando o Forms Designer, você deve carregá-lo no servidor do AEM Forms para que o modelo esteja disponível para uso ao criar a Comunicação interativa.

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Forms e documentos]**.
1. Toque **Criar** > **Upload de arquivo**.

   Navegue e selecione o **create_first_ic_print_template** modelo (XDP) e toque em **Abertura** para importar o modelo XDP para o servidor do AEM Forms.

### Criar modelo XDP para fragmentos de layout {#create-xdp-template-for-layout-fragments}

Para criar um fragmento de layout para o canal de impressão da Comunicação interativa, crie um XDP usando o Forms Designer e faça upload dele para o servidor do AEM Forms.

1. Abra o Forms Designer e selecione **Arquivo** > **Novo** > **Use um formulário em branco,** toque **Próxima** e toque em **Concluir** para abrir o formulário para criação de modelo.

   Certifique-se de que o **Biblioteca de objetos** e **Objeto** opções são selecionadas no **Janela** menu.

1. Arraste e solte a variável **Tabela** componente do **Biblioteca de objetos** ao formulário.
1. Na caixa de diálogo Inserir tabela:

   1. Especifique o número de colunas como **5**.
   1. Especifique o número de linhas do corpo como **1**.
   1. Selecione o **Incluir linha de cabeçalho na tabela** caixa de seleção
   1. Guia **OK**.

1. Toque **+** no painel esquerdo ao lado de **Tabela** 1 e clique com o botão direito do mouse em **Célula1** e selecione **Renomear objeto** para **Data**.

   Da mesma forma, renomeie **Célula2**, **Célula3**, **Célula4**, e **Célula5** para **Hora**, **Número**, **Duração**, e **Encargos** respectivamente.

1. Clique nos campos de texto do Cabeçalho na **Visualização do Designer** e renomeie-os como **Hora**, **Número**, **Duração**, e **Encargos**.

   ![Fragmento de layout](assets/layout_fragment_print_new.png)

1. Selecionar **Linha 1** no painel esquerdo e selecione **Objeto** > **Vinculação** > **Repetir Linha para Cada Item de Dados**.

   ![Repetir propriedades do fragmento de layout](assets/layout_fragment_print_repeat_new.png)

1. Arraste e solte a variável **Campo de texto** componente do **Biblioteca de objetos** para o **Visualização do Designer**.

   ![Campo de texto do fragmento de layout](assets/layout_fragment_print_text_field_new.png)

   Da mesma forma, arrastar e soltar **Campo de texto** componente para a **Hora**, **Número**, **Duração**, e **Encargos** linhas.

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local em que o arquivo será salvo e especifique o nome como **table_lf**.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.

   Depois de criar um modelo XDP para fragmento de layout usando o Forms Designer, você deve [upload](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) para o servidor do AEM Forms, para que o modelo fique disponível para uso ao criar fragmentos de layout.

## Criar modelo para canal da Web {#create-template-for-web-channel}

Crie e gerencie o modelo para o canal da Web de Comunicação Interativa usando as seguintes tarefas:

* [Criar pasta para modelos](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Criar o modelo](../../forms/using/create-templates-print-web.md#create-the-template)
* [Ativar o modelo](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Ativação de botões nas Comunicações interativas](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Criar pasta para modelos {#create-folder-for-templates}

Para criar um modelo de canal da Web, defina uma pasta onde você possa salvar os modelos criados. Depois de criar um modelo dentro dessa pasta, ative o modelo para permitir que os usuários de formulários criem o canal da Web de uma comunicação interativa com base no modelo.

Execute as seguintes etapas para criar uma pasta para os modelos editáveis:

1. Toque **Ferramentas** ![ícone de martelo](assets/hammer-icon.svg) > **Navegador de configuração**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) para obter mais informações.
1. Na página Navegador de configuração, toque em **Criar**.
1. No **Criar configuração** caixa de diálogo, especificar **Create_First_IC_templates** como o título da pasta, marque **Modelos editáveis** e toque em **Criar**.

   ![Configurar modelos da Web](assets/create_first_ic_web_template_new.png)

   A variável **Create_First_IC_templates** a pasta é criada e listada no **Navegador de configuração** página.

### Criar o modelo {#create-the-template}

Com base no [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes painéis no modelo da Web:

* Detalhes da lista: inclui um fragmento de documento
* Detalhes do cliente: inclui um fragmento de documento
* Resumo da Lista: Inclui um fragmento de documento
* Resumo de Encargos: inclui um fragmento de documento e um gráfico (layout de duas colunas)
* Chamadas Discriminadas: Inclui uma tabela
* Pagar agora: inclui um **Pagar agora** botão e uma imagem
* Serviços de valor agregado: inclui uma imagem e um **Assinar** botão.

![create_web_template](assets/create_web_template.gif)

Todas as entidades, como fragmentos de documento, gráficos, tabelas, imagens e botões, são adicionadas ao criar a Comunicação interativa.

Execute as seguintes etapas para criar um modelo para o canal da Web no **Create_First_IC_templates** pasta:

1. Navegue até a pasta de modelo apropriada selecionando **Ferramentas** > **Modelos** > **Create_First_IC_templates** pasta.
1. Toque **Criar**.
1. No **Escolher um tipo de modelo** assistente de configuração, selecione **Comunicação interativa - Canal da Web** e toque em **Próxima**.
1. No **Detalhes do modelo** assistente de configuração, especifique **Create_First_IC_Web_Template** como o título do modelo. Especifique uma descrição opcional e toque em **Criar**.

   Uma mensagem de confirmação de que o **Create_First_IC_Web_Template** é exibido.

1. Toque **Abertura** para abrir o modelo no editor de modelos.
1. Selecionar **Conteúdo inicial** na lista suspensa ao lado da guia **Visualizar** opção.

   ![Editor de modelo](assets/template_editor_initial_content_new.png)

1. Toque **Painel raiz** e toque em **+** para exibir a lista de componentes que podem ser adicionados ao modelo.
1. Selecionar **Painel** na lista para adicionar um painel acima de **Painel raiz**.
1. Selecione o **Conteúdo** no painel esquerdo. O novo painel adicionado na etapa 8 é exibido sob o **Painel raiz** na árvore de conteúdo.

   ![Árvore de conteúdo](assets/content_tree_root_panel_new.png)

1. Selecione o painel e toque em ![configure_icon](assets/configure_icon.png) (Configurar).
1. No painel Propriedades:

   1. Especificar **detalhes da cobrança** no campo Nome.
   1. Especificar **Detalhes da Lista** no campo Título.
   1. Selecionar **1** do **Número de colunas** lista suspensa.

   1. Toque ![Salvar](/help/forms/using/assets/done_icon.png) para salvar as propriedades.

   O nome do painel é atualizado para **Detalhes da Lista** na árvore de conteúdo.

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

Execute as seguintes etapas para ativar o modelo da Web:

1. Toque **Ferramentas** ![ícone de martelo](assets/hammer-icon.svg) > **Modelos**.
1. Navegue até a **Create_First_IC_Web_Template** selecione-o e toque em **Ativar**.
1. Guia **Ativar** novamente para confirmar.

   O modelo é ativado e seu status é exibido como Enabled. Você pode usar esse template ao criar a Comunicação interativa para o canal da Web.

### Ativação de botões nas Comunicações interativas {#enabling-buttons-in-interactive-communications}

Com base no caso de uso, você deve incluir o **Pagar agora** e **Assinar** botões (componentes de formulários adaptáveis) na Comunicação interativa. Para habilitar o uso desses botões na Comunicação interativa, execute as seguintes etapas:

1. Selecionar **Estrutura** na lista suspensa ao lado da guia **Visualizar** opção.
1. Selecione o **Contêiner de documentos** painel raiz usando a árvore de conteúdo e toque em **Política** para selecionar os componentes permitidos para uso na Comunicação interativa.

   ![Configurar política](assets/structure_configure_policy_new.png)

1. No **Componentes permitidos** guia de **Propriedades** , selecione **Botão** do **Formulário adaptável** componentes.

   ![Componentes permitidos](assets/allowed_components_af_new.png)

1. Toque ![save](assets/done_icon.png) para salvar as propriedades.
