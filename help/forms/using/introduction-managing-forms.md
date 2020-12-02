---
title: Introdução ao gerenciamento de formulários
seo-title: Introdução ao gerenciamento de formulários
description: A AEM Forms fornece ferramentas para gerenciar a Adaptive Forms e ativos relacionados. Este artigo apresenta os principais recursos de gerenciamento de formulários e elementos da interface do usuário.
seo-description: A AEM Forms fornece ferramentas para gerenciar a Adaptive Forms e ativos relacionados. Este artigo apresenta os principais recursos de gerenciamento de formulários e elementos da interface do usuário.
uuid: 2275a0b6-b31e-4d8e-8154-ccdfff3705aa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-manager, introduction
discoiquuid: c0e4c9bb-e12a-4f9a-a8fa-1a8ad41d3995
docset: aem65
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 1%

---


# Introdução ao gerenciamento de formulários {#introduction-to-managing-forms}

AEM [!DNL Forms] fornece interface de usuário simplificada, mas poderosa, para criar e gerenciar formulários, documentos, temas, letras, fragmentos de documento, dicionários de dados e ativos relacionados. Ele ajuda a gerenciar todo o ciclo de vida dos formulários, documentos e ativos relacionados - desde o desktop de um desenvolvedor até a oferta
em um servidor de portal para usuários finais. Você pode usar a interface do usuário AEM [!DNL Forms] para:

* Acessar AEM [!DNL Forms] componentes
* Acessar configurações AEM [!DNL Forms]

>[!NOTE]
>
>Para obter informações detalhadas sobre outras ferramentas e opções de AEM, consulte [Criação](/help/sites-authoring/author.md).

## Acessar componentes do AEM Forms {#access-aem-forms-components}

Juntamente com as opções para criar formulários, documentos e ativos relacionados, AEM fornece opções para criar sites, ativos, gerenciar uma instância AEM e muito mais. Você pode clicar no logotipo do Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) para navegar até todas as ferramentas disponíveis. Juntamente com os links para os consoles de outros componentes, também contém links para AEM [!DNL Forms]. Para navegar até AEM [!DNL Forms], clique no logotipo Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) > navigation ![compass](assets/compass.png) > **[!UICONTROL Forms]**. São exibidos links dos seguintes consoles:

* Formulários e documentos
* Temas
* Cartas
* Fragmentos do documento
* Dicionários de dados

   ![AEM Forms Console](assets/aem_forms_console_new.png)

### Formulários e documentos  {#forms-documents}

A Forms e os Documentos fornecem opções para criar uma Comunicação interativa, um formulário adaptável, um fragmento de formulário adaptável e um conjunto de formulários. Somente para AEM [!DNL Forms] no JEE, a Forms e Documentos fornece uma opção para importar arquivos do armazenamento local e sincronizar ativos AEM [!DNL Forms] com o Workbench.

O botão criar é o ponto de partida do processo de criação ou upload do ativo AEM [!DNL Forms]. Ele fornece opções para criar:

* **Comunicação** interativa: Uma comunicação interativa é uma correspondência digital baseada em HTML personalizada, interativa e fácil de usar em dispositivos, declaração ou documento. As Comunicações interativas são responsivas na natureza e alteram o layout e o design automaticamente com base no dispositivo do usuário e nas configurações. Para obter informações detalhadas, consulte [Visão Geral das Comunicações Interativas](/help/forms/using/interactive-communications-overview.md)

* **Formulário adaptável:** Um formulário adaptável é um formulário envolvente e responsivo. Você pode criar um formulário adaptável para se adaptar dinamicamente às entradas do usuário adicionando ou removendo seções de formulário com base na resposta do usuário, dispositivo ou ambiente de trabalho. O artigo [Introdução à criação de formulários adaptativos](../../forms/using/introduction-forms-authoring.md) fornece informações detalhadas sobre os formulários adaptáveis.

* **Fragmento de formulário adaptável:** enquanto cada formulário é projetado para uma finalidade específica, há alguns segmentos comuns na maioria dos formulários, como para fornecer detalhes pessoais como nome e endereço, detalhes familiares, detalhes de renda e assim por diante. É possível criar um ativo individual para essas seções. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptáveis. Para obter informações detalhadas, consulte o artigo [fragmentos de formulário adaptáveis](../../forms/using/adaptive-form-fragments.md).

* **Conjunto de formulários:** Um conjunto de formulários é uma coleção de formulários HTML5 agrupados e apresentados como um único conjunto de formulários para usuários finais. Quando os usuários finais start o preenchimento de um conjunto de formulários, os formulários são perfeitamente transitados de um formulário para outro. No final, um usuário pode enviar todos os formulários, como uma única entidade, em apenas um clique. Para obter informações detalhadas, consulte [Conjunto de formulários em AEM Forms](../../forms/using/formset-in-aem-forms.md).

* **Pasta:** AEM interface  [!DNL Forms] do usuário usa pastas para organizar ativos. Ele oferece suporte a dois tipos de pastas:

   * **Pasta geral:** essas pastas são usadas para ativos criados na interface AEM  [!DNL Forms] do usuário. Essas pastas não têm uma estrutura de pastas restrita. É possível renomear, criar subpastas e armazenar formulários adaptáveis, Comunicações interativas, fragmentos de formulário adaptáveis, Modelos de formulário (XDPs), PDF forms, Documentos e ativos relacionados nessas pastas.
   * **pasta Forms Workflow: as pastas de fluxo de trabalho do** Forms são criadas quando os processos do Workbench (arquivos de LiveCycles) são migrados e sincronizados com AEM interface  [!DNL Forms] do usuário. Não é permitido renomear, criar uma subpasta, criar uma Comunicação interativa, um fragmento de formulário adaptável ou uma Comunicação interativa. Também não é permitido excluir uma pasta de versão ou criar e carregar um formulário adaptável, um fragmento de formulário adaptável ou uma Comunicação interativa paralelamente à pasta de versão.

   ![pastas](assets/folders.png)

   **A.** Pasta geral  **B.** Forms Workflow

O painel Forms e Documento também oferece opções para:

* **Importar arquivos do armazenamento local:** você pode importar PDF forms e Documentos, modelos de formulário (formulários XFA) e outros recursos (schema de imagem e XML para XSDs). Para obter instruções passo a passo, consulte [Importar e exportar ativos para AEM Forms](../../forms/using/import-export-forms-templates.md).
* **Sincronizar ativos da AEM Forms com o Workbench:** Você pode usar a opção Arquivos do Workbench para sincronizar ativos entre a interface de usuário do AEM Forms e o Workbench. Ela garante que todos os ativos estejam disponíveis na AEM [!DNL Forms] interface do usuário e na seleção de ativos do repositório crx do Workbench.

### Temas  {#themes}

Um tema contém detalhes de estilização para componentes e painéis. Temas têm uma identidade independente. Assim, você pode reutilizar um tema em várias formas adaptativas. Você pode especificar estilos para um componente ou modificar as propriedades de CSS para vários componentes usados em seus formulários. Os estilos incluem propriedades como cores de plano de fundo, cores de estado, transparência e tamanho. É possível salvar personalizações em um tema e exportá-las para os componentes do formulário como uma predefinição. Quando o tema é adicionado ao formulário, o estilo especificado é refletido nos componentes correspondentes do formulário. Com AEM 6.2 [!DNL Forms], você pode criar temas e aplicá-los aos formulários.

Para obter informações sobre como criar e usar temas, consulte [Temas no AEM Forms](../../forms/using/themes.md).

### Cartas  {#letters}

Uma carta AEM [!DNL Forms] é uma correspondência segura, personalizada e interativa. Você pode usar AEM [!DNL Forms] para montar rapidamente letras (também conhecidas como correspondências) de conteúdo pré-aprovado e de autoria personalizada em um processo simplificado.

Para obter informações sobre como criar e usar letras, consulte [Criar letra](../../forms/using/create-letter.md).

### Fragmentos do documento {#document-fragments}

Os fragmentos de documento são partes reutilizáveis ou componentes de uma correspondência que podem ser usados para compor letras. Os fragmentos de documento são do tipo texto, lista, condição e fragmento de layout. Para obter informações sobre como criar e usar fragmentos de documento, consulte [criar fragmentos de documento](/help/forms/using/document-fragments.md).

### Dicionários de dados {#data-dictionaries}

Normalmente, os usuários corporativos não exigem conhecimento de representações de metadados, como XSD (schema XML) e classes Java. No entanto, eles geralmente exigem acesso a essas estruturas de dados e atributos para criar soluções. AEM [!DNL Forms] usa um dicionário de dados que permite aos usuários de negócios usar informações de fontes de dados back-end sem conhecer detalhes técnicos sobre seus modelos de dados subjacentes.

Para obter informações sobre como criar e usar dicionários de dados, consulte criar [artigo do dicionário de dados](../../forms/using/data-dictionary.md)

## Acessar AEM [!DNL Forms] Configurações {#accessing-aem-forms-configurations}

AEM painel de ferramentas contém ferramentas para vários componentes. Para navegar até as ferramentas específicas da AEM Forms, clique no logotipo Experience Manager ![adobeexperience emanager](assets/adobeexperiencemanager.png) > ferramentas ![martelo](assets/hammer.png) > **[!UICONTROL Forms]**. As ferramentas para executar as seguintes funções são exibidas:

* **Configurar pasta assistida:** um administrador pode configurar uma pasta de rede, conhecida como pasta assistida, para que quando um usuário colocar um arquivo (como um arquivo PDF) na pasta assistida, uma operação pré-configurada seja iniciada e manipule o arquivo. Para obter informações detalhadas, consulte [Criar e configurar uma pasta assistida](/help/forms/using/creating-configure-watched-folder.md).
* **Configurar o serviço offline do aplicativo Forms:** o serviço offline do  [!DNL Forms] aplicativo AEM armazena em cache os caminhos ou URLs dos recursos usados em um formulário. O cache de caminhos ou URLs dos recursos usados em um formulário melhora o desempenho do servidor. Para configurar o componente offline do lado do servidor do aplicativo AEM Forms, consulte [Trabalhar no modo offline](/help/forms/using/work-offline-mode.md).

   ![Ferramentas AEM Forms](assets/aem_forms_tools_new.png)

* **Configurar o Gerador de PDF:** um administrador pode configurar AEM Gerador de  [!DNL Forms] PDF, adicionar contas de usuário e importar ou exportar configurações para o Gerador de PDF.
* **Publicar ativos de gerenciamento de correspondência:** AEM  [!DNL Forms] permite que você publique todas as Cartas, Fragmentos de Documento e Dicionários de dados e dependências relacionadas de uma instância do autor ao mesmo tempo. Os ativos publicados incluem todos os ativos do Gerenciamento de Correspondência e dependências relacionadas. Para obter informações detalhadas, consulte [Publicar e cancelar a publicação de formulários e documentos](../../forms/using/publishing-unpublishing-forms.md#publishallthecorrespondencemanagementassets).
* **Exportar ativos de gerenciamento de correspondência:** você pode baixar todos os ativos de Gerenciamento de correspondência e as dependências relacionadas como um pacote de uma  [!DNL Forms] instância AEM. Para obter etapas detalhadas, consulte [Importar e exportar ativos para AEM Forms](../../forms/using/import-export-forms-templates.md#importandexportassetsincorrespondencemanagement)

## Elementos comuns da interface do usuário {#commonelements}

* **Painel esquerdo:** você pode clicar no ícone do painel esquerdo  ![](assets/railleftpng.png) railleftpngpara revelar os recursos Linha do tempo e Referências de AEM  [!DNL Forms].

   * **Linha do tempo:** você pode adicionar e visualização comentários em um ativo que está disponível para revisão na linha do tempo. Para obter instruções detalhadas, consulte [Criar e gerenciar revisões de ativos em formulários](../../forms/using/create-reviews-forms.md).
   * **Referências:** Um  [!DNL Forms] ativo AEM pode ser usado em vários  [!DNL Forms] ativos AEM. Por exemplo, um fragmento de documento pode ser usado em várias letras. Referências é uma lista de ativos (outras formas ou recursos) em que o ativo selecionado é usado e também a lista de outros ativos que o ativo selecionado está usando.

* **Trilhas de navegação:** Uma trilha de navegação representa o título do console ou da pasta atual. Você pode clicar na opção Navegação estrutural para navegar entre o nível de pastas mais alto na hierarquia.
* **Comutador de visualização:** Você pode clicar no ícone do Comutador de Visualização no  ![](assets/viewlist.png) visualizador ou no  ![](assets/viewcard.png) visualizador para alternar rapidamente entre a lista e a visualização do cartão. Para obter mais informações sobre componentes comuns da interface do usuário, consulte [Criação](/help/sites-authoring/author.md).
* **Pesquisa:** a opção de pesquisa  ![](assets/search.png) oferece a capacidade de localizar e ir rapidamente para o conteúdo e as ferramentas de que você precisa. Digite o nome do conteúdo ou da capacidade do produto e selecione uma das sugestões, por exemplo, digite &quot;Documentos&quot; para localizar e navegar rapidamente até **[!UICONTROL Forms &amp; Documentos]** ou o console Fragmentos de Documento. Para obter mais informações sobre a pesquisa, consulte o artigo AEM 6.2 [search](/help/sites-authoring/search.md)

* **Barra de ferramentas** Ações: Ao selecionar um ativo, a barra de ferramentas de ações é exibida acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento do ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para visualização da dica de ferramenta descrevendo sua funcionalidade

>[!NOTE]
>
>Quando um usuário faz uma pesquisa em qualquer console do Forms e Documentos, o painel contém apenas **Filtros e opções**. Você pode usar Filtros e opções para executar pesquisa avançada.

* **Barra de ferramentas** Ações: Ao selecionar um ativo, a barra de ferramentas de ações é exibida acima da lista de ativos. Ele contém todas as ferramentas de gerenciamento do ativo selecionado. Você pode passar o mouse sobre um ícone de ferramenta para visualização da dica de ferramenta descrevendo sua funcionalidade

   ![Barra de ferramentas de ação para um formulário adaptável](assets/action_toolbar_new.png)

   Barra de ferramentas de ação para um formulário adaptável
