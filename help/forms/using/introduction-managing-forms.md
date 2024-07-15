---
title: Introdução ao gerenciamento de formulários
description: O AEM Forms fornece ferramentas para gerenciar o Adaptive Forms e ativos relacionados. Este artigo apresenta os principais recursos de gerenciamento de formulários e elementos da interface do usuário.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
docset: aem65
exl-id: 3e063456-7f96-483d-86a3-6a414746db8a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 1%

---

# Introdução ao gerenciamento de formulários {#introduction-to-managing-forms}

O AEM [!DNL Forms] fornece uma interface simplificada, mas poderosa, para criar e gerenciar formulários, documentos, temas, cartas, fragmentos de documentos, dicionários de dados e ativos relacionados. Ele ajuda a gerenciar o ciclo de vida completo de formulários, documentos e ativos relacionados, desde o desktop de um desenvolvedor até a oferta
em um servidor do portal para usuários finais. É possível usar a interface de usuário do AEM [!DNL Forms] para:

* Acessar componentes do AEM [!DNL Forms]
* Acessar configurações de AEM [!DNL Forms]

>[!NOTE]
>
>Para obter informações detalhadas sobre outras ferramentas e opções do AEM, consulte [Criação](/help/sites-authoring/author.md).

## Acessar componentes do AEM Forms {#access-aem-forms-components}

Juntamente com as opções para criar formulários, documentos e ativos relacionados, o AEM fornece opções para criar sites, ativos, gerenciar uma instância do AEM e muito mais. Você pode clicar no logotipo do Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) para navegar até todas as ferramentas disponíveis. Juntamente com links para os consoles de outros componentes, também contém links para AEM [!DNL Forms]. Para navegar até o AEM [!DNL Forms], clique no logotipo do Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > navegação ![bússola](assets/compass.png) > **[!UICONTROL Forms]**. Os links dos seguintes consoles são exibidos:

* Formulários e documentos
* Temas
* Cartas
* Fragmentos do documento
* Dicionários de dados

  ![Console do AEM Forms](assets/aem_forms_console_new.png)

### Formulários e documentos  {#forms-documents}

O Forms e Documentos fornece opções para criar uma Comunicação interativa, um formulário adaptável, um fragmento de formulário adaptável e um conjunto de formulários. Somente para AEM [!DNL Forms] em JEE, Forms &amp; Documents fornecem uma opção para importar arquivos do armazenamento local e sincronizar ativos AEM [!DNL Forms] com o Workbench.

O botão Criar é o ponto inicial do processo de criação ou carregamento do ativo AEM [!DNL Forms]. Ela fornece opções para criar:

* **Comunicação interativa**: uma comunicação interativa é uma correspondência, instrução ou documento digital baseado em HTML personalizado, interativo e amigável para o dispositivo. As Comunicações interativas têm natureza responsiva e alteram o layout e o design automaticamente com base no dispositivo e nas configurações do usuário. Para obter informações detalhadas, consulte [Visão Geral das Comunicações Interativas](/help/forms/using/interactive-communications-overview.md)

* **Formulário adaptável:** um formulário adaptável é um formulário envolvente e responsivo. Você pode criar um formulário adaptável para adaptar dinamicamente às entradas do usuário adicionando ou removendo seções de formulário com base na resposta do usuário, no dispositivo ou no ambiente de trabalho. O artigo [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md) fornece informações detalhadas sobre os formulários adaptáveis.

* **Fragmento de formulário adaptável:** Embora cada formulário seja criado para uma finalidade específica, há alguns segmentos comuns na maioria dos formulários, como o de fornecer detalhes pessoais, como nome e endereço, detalhes da família, detalhes de renda etc. É possível criar um ativo individual para essas seções. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptáveis. Para obter informações detalhadas, consulte o artigo [fragmentos de formulário adaptáveis](../../forms/using/adaptive-form-fragments.md).

* **Conjunto de formulários:** um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para os usuários finais. Quando os usuários finais começam a preencher um conjunto de formulários, os formulários são facilmente transicionados de um formulário para outro. Ao final, um usuário pode enviar todos os formulários, como uma única entidade, com apenas um clique. Para obter informações detalhadas, consulte [Conjunto de formulários no AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Pasta:** AEM [!DNL Forms] a interface de usuário usa pastas para organizar ativos. Ela é compatível com dois tipos de pastas:

   * **Pasta Geral:** Essas pastas são usadas para ativos criados na interface de usuário do AEM [!DNL Forms]. Essas pastas não têm uma estrutura de pastas rígida. É possível renomear, criar subpastas e armazenar formulários adaptáveis, Comunicações interativas, fragmentos de formulários adaptáveis, Modelos de formulário (XDPs), PDF forms, Documentos e ativos relacionados nessas pastas.
   * **pasta Forms Workflow:** as pastas de fluxo de trabalho do Forms são criadas quando os processos do Workbench (arquivos de LiveCycle AEM) são migrados e sincronizados com a interface de usuário [!DNL Forms]. Não é permitido renomear, criar uma subpasta, criar uma Comunicação interativa, um fragmento de formulário adaptável ou uma Comunicação interativa. Também não é permitido excluir uma pasta de versão ou criar e carregar um formulário adaptável, um fragmento de formulário adaptável ou uma Comunicação interativa em paralelo à pasta de versão.

  ![pastas](assets/folders.png)

  **A.** Pasta geral **B.** pasta Forms Workflow

O painel Forms e Documento também fornece opções para:

* **Importar arquivos do armazenamento local:** você pode importar PDF forms e Documentos, Modelos de formulário (formulários XFA) e outros recursos (Imagem e esquema XML para XSDs). Para obter instruções passo a passo, consulte [Importar e exportar ativos para o AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizar ativos do AEM Forms com o Workbench:** você pode usar a opção Arquivos do Workbench para sincronizar ativos entre a interface do usuário do AEM Forms e o Workbench. Isso garante que todos os ativos estejam disponíveis na interface de usuário AEM [!DNL Forms] e na seleção de ativos do repositório crx do Workbench.

### Temas  {#themes}

Um tema contém detalhes de estilo para componentes e painéis. Os temas têm uma identidade independente. Assim, você pode reutilizar um tema em múltiplos formulários adaptativos. Você pode especificar estilos para um componente ou modificar propriedades CSS para vários componentes usados em seus formulários. Os estilos incluem propriedades como cores de fundo, cores de estado, transparência e tamanho. É possível salvar personalizações em um tema e exportá-las em componentes do formulário como uma predefinição. Quando você adiciona o tema ao formulário, o estilo especificado é refletido nos componentes correspondentes do formulário. Com o AEM 6.2 [!DNL Forms], você pode criar temas e aplicá-los aos seus formulários.

Para obter informações sobre como criar e usar temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

### Cartas  {#letters}

Uma carta de AEM [!DNL Forms] é uma correspondência segura, personalizada e interativa. Você pode usar o AEM [!DNL Forms] para reunir rapidamente cartas (também conhecidas como correspondências) de conteúdo pré-aprovado e criado de forma personalizada em um processo simplificado.

Para obter informações sobre como criar e usar cartas, consulte [Criar Carta](../../forms/using/create-letter.md).

### Fragmentos do documento {#document-fragments}

Fragmentos de documento são partes reutilizáveis ou componentes de uma correspondência usando o qual você pode compor letras. Os fragmentos do documento são do tipo texto, lista, condição e fragmento de layout. Para obter informações sobre como criar e usar fragmentos de documento, consulte [criando fragmentos de documento](/help/forms/using/document-fragments.md).

### Dicionários de dados {#data-dictionaries}

Normalmente, os usuários empresariais não exigem conhecimento de representações de metadados, como XSD (esquema XML) e classes Java. No entanto, geralmente exigem acesso a essas estruturas de dados e atributos para criar soluções. O AEM [!DNL Forms] usa o dicionário de dados que permite aos usuários corporativos usar informações de fontes de dados de back-end sem conhecer detalhes técnicos sobre seus modelos de dados subjacentes.

Para obter informações sobre como criar e usar dicionários de dados, consulte criando [artigo sobre dicionário de dados](../../forms/using/data-dictionary.md)

## Acessando configurações de AEM [!DNL Forms] {#accessing-aem-forms-configurations}

O painel de ferramentas do AEM contém ferramentas para vários componentes. Para navegar até as ferramentas específicas do AEM Forms, clique no logotipo do Experience Manager ![adobeexperiencemanager](assets/adobeexperiencemanager.png) > ferramentas ![martelo](assets/hammer.png) > **[!UICONTROL Forms]**. As ferramentas para executar as seguintes funções são exibidas:

* **Configurar a pasta monitorada:** Um administrador pode configurar uma pasta de rede, conhecida como pasta monitorada, para que, quando um usuário colocar um arquivo (como um arquivo de PDF) na pasta monitorada, uma operação pré-configurada seja iniciada e manipule o arquivo. Para obter informações detalhadas, consulte [Criar e Configurar uma pasta monitorada](/help/forms/using/creating-configure-watched-folder.md).
* **Configurar o Serviço Offline do Aplicativo Forms:** o serviço offline do aplicativo AEM [!DNL Forms] armazena em cache os caminhos ou as URLs dos recursos usados em um formulário. O armazenamento em cache de caminhos ou URLs dos recursos usados em um formulário melhora o desempenho do lado do servidor. Para configurar o componente offline do lado do servidor do aplicativo AEM Forms, consulte [Trabalhando no modo offline](/help/forms/using/work-offline-mode.md).

  ![Ferramentas do AEM Forms](assets/aem_forms_tools_new.png)

* **Configurar PDF Generator:** Um administrador pode definir as configurações de PDF Generator AEM [!DNL Forms], adicionar contas de usuário e importar ou exportar a configuração para o PDF Generator.
* **O Publish Correspondence Management Assets:** AEM [!DNL Forms] permite publicar simultaneamente todas as Cartas, Fragmentos de documento e Dicionários de dados e dependências relacionadas de uma instância de autor. Os ativos publicados incluem todos os ativos do Gerenciamento de correspondências e dependências relacionadas. Para obter informações detalhadas, consulte [Publicar e desfazer a publicação de formulários e documentos](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Exportar Assets do Gerenciamento de Correspondência:** você pode baixar todos os ativos do Gerenciamento de Correspondência e dependências relacionadas como um pacote de uma instância AEM [!DNL Forms]. Para obter etapas detalhadas, consulte [Importar e exportar ativos para o AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementos comuns da interface do usuário {#commonelements}

* **Painel esquerdo:** Você pode clicar no ícone do painel esquerdo ![railleftpng](assets/railleftpng.png) para revelar os recursos de Linha do tempo e Referências do AEM [!DNL Forms].

   * **Linha do tempo:** Você pode adicionar e exibir comentários em um ativo que esteja disponível para revisão na linha do tempo. Para obter instruções detalhadas, consulte [Criação e gerenciamento de revisões para ativos em formulários](../../forms/using/create-reviews-forms.md).
   * **Referências:** um ativo AEM [!DNL Forms] pode ser usado em vários ativos AEM [!DNL Forms]. Por exemplo, um fragmento de documento pode ser usado em várias letras. Referências é uma lista de ativos (outros formulários ou recursos) em que o ativo selecionado é usado e também a lista de outros ativos que o ativo selecionado está usando.

* **Navegação estrutural:** uma navegação estrutural representa o título do console ou pasta atual. Você pode clicar na opção Navegação estrutural para navegar entre o nível de pastas que estão mais altos na hierarquia.
* **Alternador de Exibição:** Você pode clicar no ícone Alternador de Exibição ![viewlist](assets/viewlist.png) ou ![viewcard](assets/viewcard.png) para alternar rapidamente entre o modo de exibição de lista e cartão. Para obter mais informações sobre componentes comuns da interface do usuário, consulte [Criação](/help/sites-authoring/author.md).
* **Pesquisar:** a opção de pesquisa ![pesquisar](assets/search.png) fornece recursos para localizar e acessar rapidamente o conteúdo e as ferramentas necessárias. Digite o nome do conteúdo ou recurso do produto e selecione-o a partir das sugestões. Por exemplo, digite &quot;Documentos&quot; para localizar e navegar rapidamente pelo **[!UICONTROL Forms e Documentos]** ou pelo console Fragmentos de documento. Para obter mais informações sobre pesquisa, consulte o artigo [pesquisa](/help/sites-authoring/search.md) do AEM 6.2

* **Barra de ferramentas de ações**: ao selecionar um ativo, a barra de ferramentas de ações aparece acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento para o ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para visualizar a dica de ferramenta que descreve sua funcionalidade

>[!NOTE]
>
>Quando um usuário realiza uma pesquisa em qualquer console do Forms e Documentos, o painel contém apenas **Filtros e opções**. Você pode usar Filtros e opções para executar a pesquisa avançada.

* **Barra de ferramentas de ações**: ao selecionar um ativo, a barra de ferramentas de ações aparece acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento para o ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para visualizar a dica de ferramenta que descreve sua funcionalidade

  ![Barra de ferramentas de ações para um formulário adaptável](assets/action_toolbar_new.png)

  Barra de ferramentas de ações para um formulário adaptável
