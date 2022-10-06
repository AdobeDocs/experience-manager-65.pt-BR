---
title: "Tutorial: Criar modelos"
seo-title: Create Print and Web templates for Interactive Communication
description: Criar modelos de impressão e da Web para comunicação interativa
seo-description: Create Print and Web templates for Interactive Communication
uuid: 22256a61-bcf6-4b02-9ee6-0ffb1cc20a6e
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 879ff6ca-e5f3-451d-acc2-f75142101ddd
docset: aem65
feature: Interactive Communication
exl-id: bef1f05e-aea2-433e-b3d5-0b7ad8163fa7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1796'
ht-degree: 0%

---

# Tutorial: Criar modelos{#tutorial-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Este tutorial é uma etapa do [Criar sua primeira comunicação interativa](/help/forms/using/create-your-first-interactive-communication.md) série. É recomendável seguir a série em sequência cronológica para entender, executar e demonstrar o caso de uso tutorial completo.

Para criar uma Comunicação interativa, você deve ter modelos disponíveis no servidor de AEM para Canais de impressão e da Web.

Os modelos para o canal de impressão são criados no Adobe Forms Designer e carregados no servidor de AEM. Esses modelos ficam disponíveis para uso ao criar uma Comunicação interativa.

Os modelos para o canal Web são criados em AEM. Os autores e administradores de modelos podem criar, editar e ativar modelos da Web. Depois de criados e ativados, esses modelos estão disponíveis para uso ao criar uma Comunicação interativa.

Este tutorial o orienta pelas etapas para criar modelos para canais de Impressão e da Web para que eles estejam disponíveis para uso ao criar Comunicações interativas. Ao final deste tutorial, você poderá:

* Criar modelos XDP para canal de impressão usando o Adobe Forms Designer
* Fazer upload dos modelos XDP no servidor do AEM Forms
* Criar e ativar modelos para o canal Web

## Criar modelo para o canal Imprimir {#create-template-for-print-channel}

Crie e gerencie modelos para o Canal de impressão de comunicação interativa usando as seguintes tarefas:

* [Criar modelo XDP usando o Forms Designer](../../forms/using/create-templates-print-web.md#create-xdp-template-using-forms-designer)
* [Fazer upload do modelo XDP no servidor do AEM Forms](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server)
* [Criar modelo XDP para fragmentos de layout](../../forms/using/create-templates-print-web.md#create-xdp-template-for-layout-fragments)

### Criar modelo XDP usando o Forms Designer {#create-xdp-template-using-forms-designer}

Com base na [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes subformulários no modelo XDP:

* Detalhes da Lista: Inclui um fragmento de documento
* Detalhes do cliente: Inclui um fragmento de documento
* Resumo da Lista: Inclui um fragmento de documento
* Resumo: Inclui um fragmento de documento (subformulário Encargos) e um gráfico (subformulário Gráficos)
* Chamadas discriminadas: Inclui uma tabela (fragmento de layout)
* Pagar Agora: Inclui uma imagem
* Serviços de valor agregado: Inclui uma imagem

![create_print_template](assets/create_print_template.gif)

Esses subformulários são exibidos como áreas de destino no modelo Imprimir depois de fazer upload do arquivo XDP no servidor do Forms. Todas as entidades, como fragmentos de documento, gráficos, fragmentos de layout e imagens, são adicionadas às áreas de destino ao criar a Comunicação interativa.

Execute as seguintes etapas para criar um modelo XDP para o canal de impressão:

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Use um formulário em branco,** toque **Próximo** e toque em **Concluir** para abrir o formulário para criação de template.

   Certifique-se de que **Biblioteca de objetos** e **Objeto** são selecionadas da variável **Window** menu.

1. Arraste e solte a **Subformulário** do **Biblioteca de objetos** ao formulário.
1. Selecione o subformulário para exibir as opções do subformulário na **Objeto** no painel direito.
1. Selecione o **Subformulário** e selecione **Fluxo** do **Conteúdo** lista suspensa. Arraste o ponto de extremidade esquerdo do subformulário para ajustar o comprimento.
1. No **Ligações** guia :

   1. Especificar **Detalhes da Lista** no **Nome** campo.

   1. Selecionar **Sem vínculo de dados** do **Vínculo de dados** lista suspensa.

   ![Subformulário do Designer](assets/forms_designer_subform_new.png)

1. Da mesma forma, selecione o subformulário raiz e selecione a variável **Subformulário** e selecione **Fluxo** do **Conteúdo** lista suspensa. No **Ligações** guia :

   1. Especificar **TelecaBill** no **Nome** campo.

   1. Selecionar **Sem vínculo de dados** do **Vínculo de dados** lista suspensa.

   ![Subformulário para modelo de impressão](assets/root_subform_print_template_new.png)

1. Repita as etapas 2 a 5 para criar os seguintes subformulários:

   * Detalhes da Lista
   * Detalhes do cliente
   * Resumo da Lista
   * Resumo - Selecione o **Subformulário** e selecione **Posicionado** do **Conteúdo** lista suspensa desse subformulário. Insira os seguintes subformulários no **Resumo** subformulário.

      * Encargos
      * Gráficos
   * ItemizedCalls
   * PagarAgora
   * ValueAddedServices

   Para economizar tempo, também é possível copiar e colar subformulários existentes para criar novos subformulários.

   Para alterar a **Gráficos** à direita do subformulário Encargos , selecione o **Gráficos** no painel esquerdo, selecione o **Layout** e especifique um valor para **ÂncoraX** campo. O valor deve ser maior que o valor da variável **Largura** para o campo **Encargos** subformulário. Selecione o **Encargos** e selecione o **Layout** para exibir o valor da variável **Largura** campo.

1. Arraste e solte a **Texto** do **Biblioteca de objetos** ao formulário e insira o **Marque XXXX para assinar** texto na caixa.
1. Clique com o botão direito do mouse no objeto de texto no painel esquerdo e selecione **Renomear objeto** e insira o nome do objeto de texto como **Assinar**.

   ![Modelo XDP](assets/print_xdp_template_subform_new.png)

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local para salvar o arquivo e especifique o nome como **create_first_ic_print_template**.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.

### Fazer upload do modelo XDP no servidor do AEM Forms {#upload-xdp-template-to-the-aem-forms-server}

Depois de criar um modelo XDP usando o Forms Designer, você deve carregá-lo no servidor AEM Forms para que o modelo fique disponível para uso ao criar a Comunicação interativa.

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; Documents]**.
1. Toque **Criar** > **Upload de arquivo**.

   Navegue e selecione o **create_first_ic_print_template** modelo (XDP) e toque **Abrir** para importar o modelo XDP para o servidor do AEM Forms.

### Criar modelo XDP para fragmentos de layout {#create-xdp-template-for-layout-fragments}

Para criar um fragmento de layout para o canal Imprimir da Comunicação Interativa, crie um XDP usando o Forms Designer e faça upload dele para o servidor AEM Forms.

1. Abra o Forms Designer, selecione **Arquivo** > **Novo** > **Use um formulário em branco,** toque **Próximo** e toque em **Concluir** para abrir o formulário para criação de template.

   Certifique-se de que **Biblioteca de objetos** e **Objeto** são selecionadas da variável **Window** menu.

1. Arraste e solte a **Tabela** do **Biblioteca de objetos** ao formulário.
1. Na caixa de diálogo Inserir tabela:

   1. Especifique o número de colunas como **5**.
   1. Especifique o número de linhas de corpo como **1**.
   1. Selecione o **Incluir linha do cabeçalho na tabela** caixa de seleção.
   1. Tabulação **OK**.

1. Toque **+** no painel esquerdo ao lado de **Tabela** 1 e clique com o botão direito do mouse **Célula1** e selecione **Renomear objeto** para **Data**.

   Da mesma forma, renomeie **Célula2**, **Célula3**, **Célula4** e **Célula5** para **Hora**, **Número**, **Duração** e **Encargos** respectivamente.

1. Clique nos campos de texto Cabeçalho na guia **Exibição do Designer** e renomeie-os para **Hora**, **Número**, **Duração** e **Encargos**.

   ![Fragmento de layout](assets/layout_fragment_print_new.png)

1. Selecionar **Linha 1** no painel esquerdo e selecione **Objeto** > **Vínculo** > **Repetir linha para cada item de dados**.

   ![Repetir as propriedades do fragmento de layout](assets/layout_fragment_print_repeat_new.png)

1. Arraste e solte a **Campo de texto** do **Biblioteca de objetos** para **Exibição do Designer**.

   ![Campo de texto para fragmento de layout](assets/layout_fragment_print_text_field_new.png)

   Da mesma forma, arrastar e soltar **Campo de texto** para o **Hora**, **Número**, **Duração** e **Encargos** linhas.

1. Selecionar **Arquivo** > **Salvar como** para salvar o arquivo no sistema de arquivos local:

   1. Navegue até o local para salvar o arquivo e especifique o nome como **table_lf**.
   1. Selecionar **.xdp** do **Salvar como tipo** lista suspensa.

   1. Toque **Salvar**.
   Depois de criar um modelo XDP para o fragmento de layout usando o Forms Designer, você deve [fazer upload](../../forms/using/create-templates-print-web.md#upload-xdp-template-to-the-aem-forms-server) ele é enviado ao servidor do AEM Forms para que o modelo fique disponível para uso ao criar fragmentos de layout.

## Criar modelo para canal da Web {#create-template-for-web-channel}

Crie e gerencie modelos para o canal Web de Comunicação interativa usando as seguintes tarefas:

* [Criar pasta para modelos](../../forms/using/create-templates-print-web.md#create-folder-for-templates)
* [Criar o modelo](../../forms/using/create-templates-print-web.md#create-the-template)
* [Ativar o modelo](../../forms/using/create-templates-print-web.md#enable-the-template)
* [Ativação de botões em Comunicações interativas](../../forms/using/create-templates-print-web.md#enabling-buttons-in-interactive-communications)

### Criar pasta para modelos {#create-folder-for-templates}

Para criar um modelo de canal da Web, defina uma pasta onde possa salvar os modelos criados. Depois de criar um modelo dentro dessa pasta, ative o modelo para permitir que os usuários de formulários criem um canal da Web de uma Comunicação interativa com base no modelo.

Execute as seguintes etapas para criar uma pasta para os modelos editáveis:

1. Toque **Ferramentas** ![ícone de martelo](assets/hammer-icon.svg) > **Navegador de configuração**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.
1. Na página Navegador de configuração, toque em **Criar**.
1. No **Criar configuração** , especifique **Create_First_IC_templates** como o título da pasta, verifique **Modelos editáveis** e toque em **Criar**.

   ![Configurar modelos da Web](assets/create_first_ic_web_template_new.png)

   O **Create_First_IC_templates** é criada e listada na **Navegador de configuração** página.

### Criar o modelo {#create-the-template}

Com base na [caso de uso](/help/forms/using/create-your-first-interactive-communication.md) e [anatomia](/help/forms/using/planning-interactive-communications.md), crie os seguintes painéis no template Web:

* Detalhes da Lista: Inclui um fragmento de documento
* Detalhes do cliente: Inclui um fragmento de documento
* Resumo da Lista: Inclui um fragmento de documento
* Resumo dos Encargos: Inclui um fragmento de documento e um gráfico (layout de duas colunas)
* Chamadas discriminadas: Inclui uma tabela
* Pagar Agora: Inclui um **Pagar Agora** botão e uma imagem
* Serviços de valor agregado: Inclui uma imagem e um **Assinar** botão.

![create_web_template](assets/create_web_template.gif)

Todas as entidades, como fragmentos de documento, gráficos, tabelas, imagens e botões, são adicionadas ao criar a Comunicação interativa.

Execute as etapas a seguir para criar um modelo para o canal da Web no **Create_First_IC_templates** pasta:

1. Navegue até a pasta de modelo apropriada selecionando **Ferramentas** > **Modelos** > **Create_First_IC_templates** pasta.
1. Toque **Criar**.
1. No **Selecionar um Tipo de Modelo** assistente de configuração, selecione **Comunicação interativa - Canal da Web** e tocar **Próximo**.
1. No **Detalhes do modelo** assistente de configuração, especifique **Create_First_IC_Web_Template** como o título do modelo. Especificar uma descrição e um toque opcionais **Criar**.

   Uma mensagem de confirmação de que a variável **Create_First_IC_Web_Template** é exibida.

1. Toque **Abrir** para abrir o template no editor de modelo.
1. Selecionar **Conteúdo inicial** na lista suspensa ao lado do **Visualizar** opção.

   ![Editor de modelo](assets/template_editor_initial_content_new.png)

1. Toque **Painel raiz** em seguida, toque em **+** para exibir a lista de componentes que podem ser adicionados ao modelo.
1. Selecionar **Painel** na lista para adicionar um painel acima da **Painel raiz**.
1. Selecione o **Conteúdo** no painel esquerdo. O novo painel adicionado na etapa 8 é exibido sob a variável **Painel raiz** na árvore de conteúdo.

   ![Árvore de conteúdo](assets/content_tree_root_panel_new.png)

1. Selecione o painel e toque em ![configure_icon](assets/configure_icon.png) (Configurar).
1. No painel Propriedades:

   1. Especificar **detalhes** no campo Nome .
   1. Especificar **Detalhes da Lista** no campo Título.
   1. Selecionar **1** do **Número de colunas** lista suspensa.

   1. Toque ![](/help/forms/using/assets/done_icon.png) para salvar as propriedades.

   O nome do painel é atualizado para **Detalhes da Lista** na árvore de conteúdo.

1. Repita as etapas 7 a 11 para adicionar painéis com as seguintes propriedades ao modelo:

   | Nome | Título | Número de colunas |
   |---|---|---|
   | detalhes do cliente | Detalhes do cliente | 1 |
   | cédula | Resumo da Lista | 1 |
   | encargos sumariados | Resumo dos Encargos | 2 |
   | chamadas itemised | Chamadas discriminadas | 1 |
   | pagamento | Pagar Agora | 2 |
   | tela | Serviços de valor agregado | 1 |

   A imagem a seguir descreve a árvore de conteúdo após adicionar todos os painéis ao modelo:

   ![Árvore de conteúdo para todos os painéis](assets/content_tree_all_panels_new.png)

### Ativar o modelo {#enable-the-template}

Depois de criar o template Web, você deve habilitá-lo para usar o template ao criar a Comunicação interativa.

Execute as seguintes etapas para habilitar o template Web:

1. Toque **Ferramentas** ![ícone de martelo](assets/hammer-icon.svg) > **Modelos**.
1. Navegue até o **Create_First_IC_Web_Template** modelo, selecione-o e toque em **Habilitar**.
1. Tabulação **Habilitar** novamente para confirmar.

   O modelo é ativado e seu status é exibido como Ativado. Você pode usar esse modelo ao criar a Comunicação interativa para o canal da Web.

### Ativação de botões em Comunicações interativas {#enabling-buttons-in-interactive-communications}

Com base no caso de uso, você deve incluir a variável **Pagar Agora** e **Assinar** botões (componentes de formulários adaptáveis) em Comunicação interativa. Para habilitar o uso desses botões na Comunicação interativa, execute as seguintes etapas:

1. Selecionar **Estrutura** na lista suspensa ao lado do **Visualizar** opção.
1. Selecione o **Contêiner de documento** painel raiz usando a árvore de conteúdo e toque em **Política** para selecionar os componentes permitidos para uso na Comunicação interativa.

   ![Configurar política](assets/structure_configure_policy_new.png)

1. No **Componentes permitidos** guia de **Propriedades** seção , selecione **Botão** do **Formulário adaptável** componentes.

   ![Componentes permitidos](assets/allowed_components_af_new.png)

1. Toque ![done_icon](assets/done_icon.png) para salvar as propriedades.
