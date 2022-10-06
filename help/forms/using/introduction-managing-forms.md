---
title: Introdução ao gerenciamento de formulários
seo-title: Introduction to managing forms
description: O AEM Forms fornece ferramentas para gerenciar o Adaptive Forms e ativos relacionados. Este artigo apresenta os principais recursos de gerenciamento de formulários e elementos da interface do usuário.
seo-description: AEM Forms provides tools to manage Adaptive Forms and related assets. This article introduces you to the key forms management capabilities and user interface elements.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 1%

---

# Introdução ao gerenciamento de formulários {#introduction-to-managing-forms}

AEM [!DNL Forms] O oferece interface de usuário simplificada, mas eficiente, para criar e gerenciar formulários, documentos, temas, cartas, fragmentos de documento, dicionários de dados e ativos relacionados. Ajuda a gerenciar todo o ciclo de vida de formulários, documentos e ativos relacionados, desde o desktop de um desenvolvedor até oferecê-lo em um servidor de portal para usuários finais. Você pode usar o AEM [!DNL Forms] interface do usuário para:

* AEM de acesso [!DNL Forms] componentes
* AEM de acesso [!DNL Forms] configurações

>[!NOTE]
>
>Para obter informações detalhadas sobre outras ferramentas e opções de AEM, consulte [Criação](/help/sites-authoring/author.md).

## Acessar componentes do AEM Forms {#access-aem-forms-components}

Juntamente com as opções para criar formulários, documentos e ativos relacionados, o AEM fornece opções para criar sites, ativos, gerenciar uma instância de AEM e muito mais. Você pode clicar no botão ![adobeexperiencemanager](assets/adobeexperiencemanager.png) Logotipo do Experience Manager para navegar até todas as ferramentas disponíveis. Juntamente com os links para os consoles de outros componentes, também contém links para o AEM [!DNL Forms]. Para navegar até AEM [!DNL Forms], clique no logotipo Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![bússola](assets/compass.png) > **[!UICONTROL Forms]**. Os links dos seguintes consoles são exibidos:

* Formulários e documentos
* Temas
* Cartas
* Fragmentos do documento
* Dicionários de dados

   ![Console do AEM Forms](assets/aem_forms_console_new.png)

### Formulários e documentos  {#forms-documents}

O Forms &amp; Documents fornece opções para criar uma Comunicação interativa, formulário adaptável, fragmento de formulário adaptável e conjunto de formulários. Somente para AEM [!DNL Forms] no JEE, o Forms &amp; Documents fornece uma opção para importar arquivos do armazenamento local e sincronizar AEM [!DNL Forms] ativos com o Workbench.

O botão criar é o ponto de partida do processo de criação ou upload de AEM [!DNL Forms] ativo. Ele fornece opções para criar:

* **Comunicação interativa**: Uma Comunicação interativa é uma correspondência digital, declaração ou documento personalizado, interativo e amigável para dispositivos com base em HTML. As Comunicações interativas são responsivas em natureza e alteram o layout e o design automaticamente com base no dispositivo e nas configurações do usuário. Para obter informações detalhadas, consulte [Visão geral das comunicações interativas](/help/forms/using/interactive-communications-overview.md)

* **Formulário adaptável:** Um formulário adaptável é um formulário envolvente e responsivo. Você pode criar um formulário adaptável para se adaptar dinamicamente às entradas do usuário, adicionando ou removendo seções de formulário com base na resposta do usuário, no dispositivo ou no ambiente de trabalho. O [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md) este artigo fornece informações detalhadas sobre os formulários adaptáveis.

* **Fragmento de formulário adaptável:** Embora cada formulário seja projetado para uma finalidade específica, há alguns segmentos comuns na maioria das formas, como para fornecer detalhes pessoais, como nome e endereço, detalhes familiares, detalhes de renda etc. Você pode criar um ativo individual para essas seções. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptáveis. Para obter informações detalhadas, consulte [fragmentos de formulário adaptáveis](../../forms/using/adaptive-form-fragments.md) artigo 10. o

* **Conjunto de formulários:** Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais começam a preencher um conjunto de formulários, eles são perfeitamente transitados de um formulário para outro. No final, um usuário pode enviar todos os formulários, como uma única entidade, com apenas um clique. Para obter informações detalhadas, consulte [Conjunto de formulários no AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Pasta:** AEM [!DNL Forms] a interface do usuário usa pastas para organizar ativos. Ele suporta dois tipos de pastas:

   * **Pasta Geral:** Essas pastas são usadas para ativos criados no AEM [!DNL Forms] interface do usuário. Essas pastas não têm uma estrutura de pastas estrita. É possível renomear, criar subpastas e armazenar formulários adaptáveis, Comunicações interativas, fragmentos de formulário adaptáveis, Modelos de formulário (XDPs), PDF forms, Documentos e ativos relacionados nessas pastas.
   * **Pasta Forms Workflow:** As pastas de fluxo de trabalho do Forms são criadas quando os processos do Workbench (arquivos do LiveCycle) são migrados e sincronizados com AEM [!DNL Forms] interface do usuário. Não é permitido renomear, criar uma subpasta, criar uma Comunicação interativa, um fragmento de formulário adaptável ou uma Comunicação interativa. Também não é permitido excluir uma pasta de versão ou criar e carregar um formulário adaptável, um fragmento de formulário adaptável ou uma Comunicação interativa em paralelo à pasta de versão.

   ![pastas](assets/folders.png)

   **A.** Pasta geral **B.** pasta Forms Workflow

O painel Forms e Documento também fornece opções para:

* **Importar arquivos do armazenamento local:** É possível importar PDF forms &amp; Documents, Form templates (formulários XFA) e outros recursos (esquema Imagem e XML para XSDs). Para obter instruções passo a passo, consulte [Importação e exportação de ativos para o AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizar ativos do AEM Forms com o Workbench:** Você pode usar a opção Arquivos do Workbench para sincronizar ativos entre a interface do usuário do AEM Forms e o Workbench. Isso garante que todos os ativos estejam disponíveis no AEM [!DNL Forms] interface de usuário e seleção de ativos crx-repository do Workbench.

### Temas  {#themes}

Um tema contém detalhes de estilo para componentes e painéis. Os temas têm uma identidade independente. Assim, você pode reutilizar um tema em várias formas adaptáveis. Você pode especificar estilos para um componente ou modificar as propriedades de CSS de vários componentes usados em seus formulários. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência e tamanho. É possível salvar personalizações em um tema e exportá-las para componentes do formulário como uma predefinição. Ao adicionar o tema ao formulário, o estilo especificado reflete nos componentes correspondentes do formulário. Com AEM 6.2 [!DNL Forms], é possível criar temas e aplicá-los aos formulários.

Para obter informações sobre como criar e usar temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

### Cartas  {#letters}

Um AEM [!DNL Forms] a carta é uma correspondência segura, personalizada e interativa. Você pode usar AEM [!DNL Forms] para reunir rapidamente cartas (também conhecidas como correspondências) de conteúdo pré-aprovado e de autoria personalizada em um processo simplificado.

Para obter informações sobre como criar e usar letras, consulte [Criar carta](../../forms/using/create-letter.md).

### Fragmentos do documento {#document-fragments}

Fragmentos de documento são partes reutilizáveis ou componentes de uma correspondência que pode ser usada para compor cartas. Os fragmentos de documento são do tipo texto, lista, condição e fragmento de layout. Para obter informações sobre como criar e usar fragmentos de documento, consulte [criação de fragmentos de documento](/help/forms/using/document-fragments.md).

### Dicionários de dados {#data-dictionaries}

Normalmente, os usuários corporativos não exigem conhecimento de representações de metadados, como XSD (esquema XML) e classes Java. No entanto, elas geralmente exigem acesso a essas estruturas de dados e atributos para criar soluções. AEM [!DNL Forms] O usa o dicionário de dados que permite que usuários corporativos usem informações de fontes de dados de back-end sem saber detalhes técnicos sobre seus modelos de dados subjacentes.

Para obter informações sobre como criar e usar dicionários de dados, consulte criação [artigo do dicionário de dados](../../forms/using/data-dictionary.md)

## Acessar AEM [!DNL Forms] Configurações {#accessing-aem-forms-configurations}

AEM painel Ferramentas contém ferramentas para vários componentes. Para navegar até ferramentas específicas do AEM Forms, clique no logotipo do Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > ferramentas ![martelo](assets/hammer.png) > **[!UICONTROL Forms]**. As ferramentas para executar as seguintes funções são exibidas:

* **Configurar pasta assistida:** Um administrador pode configurar uma pasta de rede, conhecida como pasta assistida, de modo que, quando um usuário colocar um arquivo (como um arquivo PDF) na pasta assistida, uma operação pré-configurada será iniciada e manipulará o arquivo. Para obter informações detalhadas, consulte [Criar e configurar uma pasta monitorada](/help/forms/using/creating-configure-watched-folder.md).
* **Configurar o serviço offline do aplicativo Forms:** O AEM [!DNL Forms] o serviço offline de aplicativo armazena em cache os caminhos ou URLs dos recursos usados em um formulário. O armazenamento em cache de caminhos ou URLs dos recursos usados em um formulário melhora o desempenho do lado do servidor. Para configurar o componente offline do lado do servidor do aplicativo AEM Forms, consulte [Trabalhar no modo offline](/help/forms/using/work-offline-mode.md).

   ![Ferramentas do AEM Forms](assets/aem_forms_tools_new.png)

* **Configurar gerador de PDF:** Um administrador pode configurar AEM [!DNL Forms] Configurações do Gerador de PDF, adicione contas de usuário e importe ou exporte configurações para o Gerador de PDF.
* **Publicar ativos de gerenciamento de correspondência:** AEM [!DNL Forms] permite publicar todas as Cartas, Fragmentos de documento e Dicionários de dados e dependências relacionadas de uma instância do autor ao mesmo tempo. Os ativos publicados incluem todos os ativos de Gerenciamento de correspondência e dependências relacionadas. Para obter informações detalhadas, consulte [Publicar e desfazer a publicação de formulários e documentos](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Exportar ativos de gerenciamento de correspondência:** Você pode baixar todos os ativos de Gerenciamento de correspondência e dependências relacionadas como um pacote de um AEM [!DNL Forms] instância. Para obter etapas detalhadas, consulte [Importação e exportação de ativos para o AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementos comuns da interface do usuário {#commonelements}

* **Painel esquerdo:** Você pode clicar no ícone do painel à esquerda ![railleftpng](assets/railleftpng.png) para revelar os recursos Linha do tempo e Referências de AEM [!DNL Forms].

   * **Linha do tempo:** É possível adicionar e exibir comentários em um ativo que está disponível para revisão na linha do tempo. Para obter instruções detalhadas, consulte [Criar e gerenciar revisões de ativos nos formulários](../../forms/using/create-reviews-forms.md).
   * **Referências:** Um AEM [!DNL Forms] ativo pode ser usado em vários AEM [!DNL Forms] ativos. Por exemplo, um fragmento de documento pode ser usado em várias letras. Referências é uma lista de ativos (outras formas ou recursos) em que o ativo selecionado é usado e também a lista de outros ativos que o ativo selecionado está usando.

* **Navegação estrutural:** Uma navegação estrutural representa o título do console ou da pasta atual. Você pode clicar na opção Caminho da navegação para navegar entre o nível de pastas mais alto na hierarquia.
* **Alternador de visualização:** Você pode clicar no ícone Exibir Alternador ![lista de exibição](assets/viewlist.png) ou ![visor](assets/viewcard.png) para alternar rapidamente entre a lista e a exibição de cartão. Para obter mais informações sobre componentes comuns da interface do usuário, consulte [Criação](/help/sites-authoring/author.md).
* **Pesquisar:** A opção de pesquisa ![pesquisa](assets/search.png) O oferece a capacidade de encontrar e acessar rapidamente o conteúdo e as ferramentas necessárias. Digite o nome do conteúdo ou da capacidade do produto e selecione entre as sugestões, por exemplo, digite &quot;Documentos&quot; para encontrar e navegar rapidamente para **[!UICONTROL Forms &amp; Documents]** ou do console Fragmentos de documento . Para obter mais informações sobre a pesquisa, consulte AEM 6.2 [pesquisa](/help/sites-authoring/search.md) artigo

* **Barra de ferramentas Ações**: Ao selecionar um ativo, a barra de ferramentas de ações aparece acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento do ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para ver a dica de ferramenta que descreve sua funcionalidade

>[!NOTE]
>
>Quando um usuário faz uma pesquisa em qualquer console de Forms &amp; Documents, o painel contém somente **Filtros e opções**. Você pode usar Filtros e opções para realizar uma pesquisa avançada.

* **Barra de ferramentas Ações**: Ao selecionar um ativo, a barra de ferramentas de ações aparece acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento do ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para ver a dica de ferramenta que descreve sua funcionalidade

   ![Barra de ferramentas Ação para um formulário adaptável](assets/action_toolbar_new.png)

   Barra de ferramentas Ação para um formulário adaptável
