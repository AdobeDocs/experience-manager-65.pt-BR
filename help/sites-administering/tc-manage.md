---
title: Gerenciamento de projetos de tradução
seo-title: Gerenciamento de projetos de tradução
description: Saiba como gerenciar projetos de tradução em AEM.
seo-description: Saiba como gerenciar projetos de tradução em AEM.
uuid: f6f79b5b-dc08-4dde-b464-719345d233a6
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: c8672774-6911-497d-837b-1e5953c4226a
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3427'
ht-degree: 1%

---


# Gerenciando projetos de tradução{#managing-translation-projects}

Depois de preparar o conteúdo para tradução, você precisa concluir a estrutura do idioma criando cópias de idioma ausentes e criar projetos de tradução.

Os projetos de tradução permitem gerenciar a tradução de AEM conteúdo. Um projeto de tradução é um tipo de AEM [project](/help/sites-authoring/projects.md) que contém recursos que devem ser traduzidos para outros idiomas. Esses recursos são as páginas e os ativos de [cópias de idioma](/help/sites-administering/tc-prep.md) criados a partir do idioma principal.

Quando os recursos são adicionados a um projeto de tradução, um trabalho de tradução é criado para eles. Os trabalhos fornecem comandos e informações de status que você usa para gerenciar os workflows de tradução automática e de tradução automática que são executados nos recursos.

>[!NOTE]
>
>Um projeto de tradução pode conter vários trabalhos de tradução.

Os projetos de tradução são itens de longa duração, definidos por idioma e método/provedor de tradução para alinhar-se ao controle organizacional para a globalização. Eles devem ser iniciados uma vez, durante a tradução inicial ou manualmente, e permanecer em vigor durante as atividades de atualização de conteúdo e tradução.

Os projetos de tradução e os empregos são criados com workflows de preparação da tradução. Esses workflows têm três opções, tanto para a tradução inicial (Create&amp;Translate) quanto para as atualizações (Update Translation):

1. [Criar novo projeto](#creating-translation-projects-using-the-references-panel)
1. [Adicionar ao projeto existente](#adding-pages-to-a-translation-project)
1. [Somente estrutura de conteúdo](#creating-the-structure-of-a-language-copy)

>[!NOTE]
>
>A opção 3 não está relacionada ao trabalho/projeto de tradução. Permite copiar o conteúdo e as alterações estruturais no idioma principal às cópias de idioma (não traduzidas). Você pode usar isso para manter seus mestres em sincronia, mesmo sem tradução.

## Execução de traduções iniciais e Atualização de traduções existentes {#performing-initial-translations-and-updating-existing-translations}

AEM detecta se um projeto de tradução está sendo criado para a tradução inicial do conteúdo ou para atualizar cópias de idioma já traduzidas. Quando você cria um projeto de tradução para uma página e indica as cópias de idioma para as quais você está traduzindo, AEM detecta se a página de origem já existe nas cópias de idioma direcionado:

* **A cópia de idioma não inclui a página:** AEM trata essa situação como a tradução inicial. A página é imediatamente copiada para a cópia de idioma e incluída no projeto. Quando a página traduzida é importada para o AEM, AEM a copia diretamente para a cópia do idioma.
* **A cópia de idioma já inclui a página:** AEM trata essa situação como uma tradução atualizada. Uma inicialização é criada e uma cópia da página é adicionada à inicialização e incluída no projeto. As inicializações permitem que você revise as traduções atualizadas antes de confirmá-las na cópia do idioma:

   * Quando a página traduzida é importada para o AEM, ela substitui a página na inicialização.
   * A página traduzida substitui a cópia de idioma somente quando o lançamento é promovido.

Por exemplo, a raiz de idioma /content/geometrixx/fr é criada para a tradução em francês do idioma principal /content/geometrixx/en. Não há outras páginas na cópia em francês.

* Um projeto de tradução é criado para a página /content/geometrixx/en/products e para todas as páginas secundárias, direcionando a cópia em francês. Como a cópia de idioma não inclui a página /content/geometrixx/fr/products, AEM copia imediatamente a página /content/geometrixx/en/products e todas as páginas filhas para a cópia em francês. As cópias também estão incluídas no projeto de tradução.
* Um projeto de tradução é criado para a página /content/geometrixx/en e para todas as páginas secundárias, direcionando a cópia em francês. Como a cópia do idioma inclui a página que corresponde à página /content/geometrixx/en (a raiz do idioma), AEM copia a página /content/geometrixx/en e todas as páginas secundárias e as adiciona a uma inicialização. As cópias também estão incluídas no projeto de tradução.

## Criando projetos de tradução usando o painel Referências {#creating-translation-projects-using-the-references-panel}

Crie projetos de tradução para que você possa executar e gerenciar o fluxo de trabalho para traduzir os recursos do seu idioma principal. Ao criar projetos, você especifica a página no idioma principal que está sendo traduzido e as cópias de idioma para as quais está executando a tradução:

* A configuração em nuvem da estrutura de integração de tradução associada à página selecionada determina muitas propriedades dos projetos de tradução, como o fluxo de trabalho de tradução a ser usado.
* Um projeto é criado para cada cópia de idioma selecionada.
* Uma cópia da página selecionada e dos ativos associados são criados e adicionados a cada projeto. Essas cópias são enviadas posteriormente ao provedor de tradução para tradução.

Você pode especificar que as páginas secundárias da página selecionada também sejam selecionadas. Nesse caso, cópias das páginas secundárias também são adicionadas a cada projeto para que sejam traduzidas. Quando qualquer página secundária é associada a diferentes configurações de estrutura de integração de tradução, AEM cria projetos adicionais.

Você também pode [criar projetos de tradução manualmente](#creating-a-translation-project-using-the-projects-console).

**Traduções iniciais e atualização de traduções**

O painel Referências indica se você está atualizando as cópias de idioma existentes ou criando a primeira versão das cópias de idioma. Quando existe uma cópia de idioma para a página selecionada, a guia Atualizar cópias de idioma é exibida para fornecer acesso aos comandos relacionados ao projeto.

![chlimage_1-239](assets/chlimage_1-239.png)

Depois de traduzir, você pode [revisar a tradução](#reviewing-and-promoting-updated-content) antes de substituir a cópia de idioma por ela. Quando não houver uma cópia de idioma para a página selecionada, a guia Criar e traduzir será exibida para fornecer acesso aos comandos relacionados ao projeto.

![chlimage_1-240](assets/chlimage_1-240.png)

### Criar projetos de tradução para uma nova cópia de idioma {#create-translation-projects-for-a-new-language-copy}

1. Use o console Sites para selecionar a página que você está adicionando aos projetos de tradução.

   Por exemplo, para traduzir as páginas em inglês do Site de demonstração do Geometrixx, selecione Site de demonstração do Geometrixx > Inglês.

1. Na barra de ferramentas, clique ou toque em Referências.

   ![chlimage_1-241](assets/chlimage_1-241.png)

1. Selecione Cópias de idioma e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.
1. Clique ou toque em Criar e traduzir e configure o trabalho de tradução:

   * Use o menu suspenso Idiomas para selecionar uma cópia de idioma para a qual você deseja traduzir. Selecione outros idiomas, conforme necessário. Os idiomas exibidos na lista correspondem às raízes de [idioma criadas](/help/sites-administering/tc-prep.md#creating-a-language-root).
   * Para traduzir a página selecionada e todas as páginas secundárias, selecione Selecionar todas as subpáginas. Para traduzir somente a página selecionada, desmarque a opção.
   * Para Projeto, selecione Criar novo projeto de tradução.
   * Digite um nome para o projeto.

   ![chlimage_1-242](assets/chlimage_1-242.png)

1. Clique ou toque em Criar.

### Criar projetos de tradução para uma cópia de idioma existente {#create-translation-projects-for-an-existing-language-copy}

1. Use o console Sites para selecionar a página que você está adicionando aos projetos de tradução.

   Por exemplo, para traduzir as páginas em inglês do Site de demonstração do Geometrixx, selecione Site de demonstração do Geometrixx > Inglês.

1. Na barra de ferramentas, clique ou toque em Referências.

   ![chlimage_1-243](assets/chlimage_1-243.png)

1. Selecione Cópias de idioma e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.
1. Clique ou toque em Atualizar Cópias de Idioma e configure o trabalho de tradução:

   * Para traduzir a página selecionada e todas as páginas secundárias, selecione Selecionar todas as subpáginas. Para traduzir somente a página selecionada, desmarque a opção.
   * Para Projeto, selecione Criar novo projeto de tradução.
   * Digite um nome para o projeto.

   ![chlimage_1-244](assets/chlimage_1-244.png)

1. Clique ou toque em Start.

## Adicionar páginas a um projeto de tradução {#adding-pages-to-a-translation-project}

Depois de criar um projeto de tradução, você pode usar o painel Recursos para adicionar páginas ao projeto. Adicionar páginas é útil quando você está incluindo páginas de diferentes ramificações no mesmo projeto.

Quando você adiciona páginas a um projeto de tradução, as páginas são incluídas em um novo trabalho de tradução. Você também pode [adicionar páginas a um trabalho existente](#adding-pages-assets-to-a-translation-job).

Como ao criar um novo projeto, ao adicionar páginas, cópias das páginas são adicionadas a uma inicialização quando necessário para evitar a substituição de cópias de idioma existentes. (Consulte [Criando Projetos de Tradução para Cópias de Idioma Existentes](#performing-initial-translations-and-updating-existing-translations).)

1. Use o console Sites para selecionar a página que você está adicionando ao projeto de tradução.

   Por exemplo, para traduzir as páginas em inglês do Site de demonstração do Geometrixx, selecione Site de demonstração do Geometrixx > Inglês.

1. Na barra de ferramentas, clique ou toque em Referências.

   ![chlimage_1-245](assets/chlimage_1-245.png)

1. Selecione Cópias de idioma e, em seguida, selecione as cópias de idioma para as quais você está traduzindo as páginas de origem.

   ![chlimage_1-35](assets/chlimage_1-35.jpeg)

1. Clique ou toque em Atualizar cópias de idioma e configure as propriedades:

   * Para traduzir a página selecionada e todas as páginas secundárias, selecione Selecionar todas as subpáginas. Para traduzir somente a página selecionada, desmarque a opção.
   * Para Projeto, selecione Adicionar a projeto de tradução existente.
   * Selecione o projeto.

   >[!NOTE]
   >
   >O idioma do público alvo definido no Projeto de tradução deve corresponder ao caminho da cópia do idioma, conforme mostrado no Painel de referências.

   ![chlimage_1-36](assets/chlimage_1-36.jpeg)

1. Clique ou toque em Start.

## Adicionar páginas/ativos a um trabalho de tradução {#adding-pages-assets-to-a-translation-job}

Você pode adicionar páginas, ativos, tags ou dicionários i18n ao trabalho de tradução do seu projeto de tradução. Para adicionar páginas ou ativos:

1. Na parte inferior do bloco Trabalho de tradução do seu projeto de tradução, clique ou toque nas reticências.

   ![chlimage_1-246](assets/chlimage_1-246.png)

1. Clique ou toque em Adicionar e Páginas/Ativos.

   ![chlimage_1-248](assets/chlimage_1-247.png)

1. Selecione o item na extremidade superior da ramificação que deseja adicionar e clique ou toque no ícone de marca de seleção. É possível selecionar várias vezes.

   ![chlimage_1-247](assets/chlimage_1-248.png)

1. Como alternativa, você pode selecionar o ícone de pesquisa para procurar facilmente páginas ou ativos que deseja adicionar ao trabalho de tradução.

   ![chlimage_1-249](assets/chlimage_1-249.png)

Suas páginas e/ou ativos são adicionados ao trabalho de tradução.

## Adicionar dicionários i18n a um trabalho de tradução {#adding-i-n-dictionaries-to-a-translation-job}

Você pode adicionar páginas, ativos, tags ou dicionários i18n ao trabalho de tradução do seu projeto de tradução. Para adicionar um dicionário i18n:

1. Na parte inferior do bloco Trabalho de tradução do seu projeto de tradução, clique ou toque nas reticências.

   ![chlimage_1-250](assets/chlimage_1-250.png)

1. Clique ou toque em Adicionar e no dicionário I18N.

   ![chlimage_1-251](assets/chlimage_1-251.png)

1. Selecione o dicionário que deseja adicionar e clique ou toque no botão Adicionar.

   ![chlimage_1-252](assets/chlimage_1-252.png)

Seu dicionário agora está no seu trabalho de tradução.

![chlimage_1-253](assets/chlimage_1-253.png)

>[!NOTE]
>
>Para obter mais informações sobre dicionários i18n, leia [Usando o Tradutor para gerenciar dicionários](/help/sites-developing/i18n-translator.md).

## Adicionar tags a um trabalho de tradução {#adding-tags-to-a-translation-job}

Você pode adicionar páginas, ativos, tags ou dicionários i18n ao trabalho de tradução do seu projeto de tradução. Para adicionar tags:

1. Na parte inferior do bloco Trabalho de tradução do seu projeto de tradução, clique ou toque nas reticências.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. Clique ou toque em Adicionar e em Tags.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Selecione as tags que deseja adicionar e clique ou toque no ícone de marca de seleção. É possível selecionar várias vezes.

   ![chlimage_1-256](assets/chlimage_1-256.png)

Suas tags agora são adicionadas ao trabalho de tradução.

![chlimage_1-257](assets/chlimage_1-257.png)

## Visualizando detalhes do projeto de tradução {#seeing-translation-project-details}

O bloco Resumo da tradução contém as propriedades que estão configuradas para um projeto de tradução. Além das [informações genéricas do projeto](/help/sites-authoring/projects.md#project-info), a guia Tradução contém propriedades específicas à tradução:

* Idioma de origem: O idioma das páginas que estão sendo traduzidas.
* Idioma do público alvo: O idioma no qual as páginas estão sendo traduzidas.
* Método de tradução: O fluxo de trabalho de tradução. Há suporte para Tradução Humana ou Tradução Automática.
* Provedor de Tradução: O provedor de serviço de tradução que está executando a tradução.
* Categoria de conteúdo: (Tradução automática) A categoria de conteúdo usada para tradução.
* Configuração da nuvem: A configuração de nuvem do conector de serviço de tradução usado para o projeto.

Quando um projeto é criado usando o painel Recursos de uma página, essas propriedades são configuradas automaticamente com base nas propriedades da página de origem.

![chlimage_1-258](assets/chlimage_1-258.png)

## Monitorando o Status de um Trabalho de Tradução {#monitoring-the-status-of-a-translation-job}

O mosaico Trabalho de Tradução de um projeto de Tradução fornece o status de um trabalho de tradução, bem como o número de páginas e ativos no trabalho.

![chlimage_1-259](assets/chlimage_1-259.png)

A tabela a seguir descreve cada status que uma ordem de produção ou um item na ordem de produção pode ter:

| Status | Descrição |
|---|---|
| Rascunho | O trabalho de tradução não foi iniciado. As tarefas de tradução estão no status RASCUNHO quando são criadas. |
| Enviado | Os arquivos no trabalho de tradução têm esse status quando foram enviados com êxito ao serviço de tradução. Esse status pode ocorrer após o comando Solicitar escopo ou o comando Start ser emitido. |
| Escopo solicitado | Para o fluxo de trabalho da Tradução Humana, os arquivos no trabalho foram enviados ao fornecedor da tradução para escopo. Esse status é exibido depois que o comando Solicitar escopo é emitido. |
| Escopo concluído | O fornecedor delimitou o trabalho de tradução. |
| Confirmado para tradução | O proprietário do projeto aceitou o escopo. Esse status indica que o fornecedor da tradução deve começar a traduzir os arquivos no trabalho. |
| Tradução em andamento | Para um trabalho, a tradução de um ou mais arquivos no trabalho ainda não foi concluída. Para um item na tarefa, o item está sendo traduzido. |
| Traduzido | Para um trabalho, a tradução de todos os arquivos no trabalho está concluída. Para um item no cargo, o item é convertido. |
| Pronto Para Revisão | O item no trabalho é traduzido e o arquivo foi importado para o AEM. |
| Concluir | O proprietário do projeto indicou que o contrato de tradução está concluído. |
| Cancelar | Indica que o fornecedor de tradução deve parar de trabalhar em um trabalho de tradução. |
| Atualização de erro | Ocorreu um erro ao transferir ficheiros entre o AEM e o serviço de tradução. |
| Estado desconhecido | Ocorreu um erro desconhecido. |

Para ver o status de cada arquivo no trabalho, clique ou toque nas reticências na parte inferior do bloco.

## Definindo a Data de Vencimento dos Trabalhos de Tradução {#setting-the-due-date-of-translation-jobs}

Especifique a data antes da qual seu fornecedor de tradução precisa retornar os arquivos traduzidos. Você pode definir a data de vencimento do projeto ou de um cargo específico:

* **Projeto:Trabalhos de** tradução no projeto herdam a data de vencimento.
* **Job:** A data de vencimento definida para o job substitui a data de vencimento definida para o projeto.

A configuração da data de vencimento funciona corretamente somente quando o fornecedor de tradução que você está usando suporta esse recurso.

O procedimento a seguir define a data de vencimento de um projeto.

1. Clique ou toque nas reticências na parte inferior do bloco Resumo da tradução.

   ![chlimage_1-260](assets/chlimage_1-260.png)

1. Na guia Básico, use o seletor de datas da propriedade Data de Vencimento para selecionar a data de vencimento.

   ![chlimage_1-261](assets/chlimage_1-261.png)

1. Clique ou toque em Concluído.

O procedimento a seguir define a data de vencimento de um trabalho de tradução.

1. No bloco Trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em Data de vencimento.

   ![chlimage_1-262](assets/chlimage_1-262.png)

1. Na caixa de diálogo, clique ou toque no ícone de calendário, selecione a data e a hora a serem usadas como data de vencimento e clique em Salvar.

   ![chlimage_1-263](assets/chlimage_1-263.png)

## Escopo de um trabalho de tradução {#scoping-a-translation-job}

Escopo um trabalho de tradução para obter uma estimativa do custo da tradução do seu provedor de serviço de tradução. Quando você faz o escopo de um trabalho, os arquivos de origem são enviados ao fornecedor da tradução que compara o texto ao pool de traduções armazenadas (memória de tradução). Normalmente, o escopo é o número de palavras que exigem tradução.

Para obter mais informações sobre os resultados do escopo, entre em contato com o fornecedor da tradução.

>[!NOTE]
>
>O escopo é opcional. Você pode start um trabalho de tradução sem escopo.

Quando você define o escopo de um trabalho de tradução, o status do trabalho é `Scope Requested`. Quando o fornecedor de tradução retorna o escopo, o status é alterado para `Scope Completed`. Quando o escopo for concluído, você poderá usar o comando Mostrar escopo para revisar os resultados do escopo.

O escopo funciona corretamente somente quando o fornecedor de tradução que você está usando suporta esse recurso.

1. No console Projetos, abra seu projeto de tradução.
1. No bloco Trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em Escopo da solicitação.

   ![chlimage_1-264](assets/chlimage_1-264.png)

1. Quando o status do job for alterado para SCOPE_COMPLETED, no bloco Trabalho de Tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em Mostrar escopo.

## Iniciando um trabalho de tradução {#starting-a-translation-job}

Start um trabalho de tradução para traduzir as páginas de origem para o idioma do público alvo. A tradução é executada de acordo com os valores de propriedade do bloco Resumo da Tradução.

Depois que você start o trabalho de tradução, o bloco Trabalho de tradução mostra o status Tradução em andamento.

![chlimage_1-265](assets/chlimage_1-265.png)

1. No console Projetos, abra o projeto de tradução.
1. No bloco Trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em Start.

   ![chlimage_1-266](assets/chlimage_1-266.png)

1. Na caixa de diálogo Ação que confirma o início da tradução, clique ou toque em Fechar.

## Cancelando um trabalho de tradução {#canceling-a-translation-job}

Cancele um trabalho de tradução para interromper o processo de tradução e impedir que o fornecedor de tradução execute outras traduções. Você pode cancelar um trabalho quando ele tiver o status `Committed For Translation` ou `Translation In Progress`.

1. No console Projetos, abra o projeto de tradução.
1. No bloco Trabalho de tradução, clique ou toque no menu de comandos e, em seguida, clique ou toque em Cancelar.
1. Na caixa de diálogo Ação que confirma o cancelamento da tradução, clique ou toque em OK.

## Aceitar/Rejeitar Fluxo de Trabalho {#accept-reject-workflow}

Quando o conteúdo volta após a tradução e está no status Pronto para revisão, você pode entrar no trabalho de tradução e aceitar/rejeitar o conteúdo.

![chlimage_1-267](assets/chlimage_1-267.png)

Se você selecionar Rejeitar tradução, terá a opção de adicionar um comentário.

![chlimage_1-268](assets/chlimage_1-268.png)

Rejeitar conteúdo o envia de volta ao fornecedor de tradução, onde ele poderá ver o comentário.

## Revisando e promovendo Conteúdo Atualizado {#reviewing-and-promoting-updated-content}

Quando o conteúdo for traduzido para uma cópia de idioma existente, reveja as traduções, faça alterações se necessário e promova as traduções para movê-lo para a cópia de idioma. Você pode revisar arquivos traduzidos quando o trabalho de tradução mostrar o status Pronto para revisão.

![chlimage_1-269](assets/chlimage_1-269.png)

1. Selecione a página no idioma principal, clique ou toque em Referências e, em seguida, clique ou toque em Cópias de idioma.
1. Clique ou toque na cópia de idioma para revisar.

   ![chlimage_1-270](assets/chlimage_1-270.png)

1. Clique ou toque em Iniciar para revelar os comandos relacionados à inicialização.

   ![chlimage_1-271](assets/chlimage_1-271.png)

1. Para abrir a cópia de inicialização da página para revisar e editar o conteúdo, clique em Abrir página.
1. Depois de revisar o conteúdo e fazer as alterações necessárias, para promover a cópia de inicialização, clique em Promover.
1. Na página Promover lançamento, especifique quais páginas serão promovidas e clique ou toque em Promover.

## Comparando Cópias de Idioma {#comparing-language-copies}

Para comparar as Cópias de idioma com o idioma Principal:

1. No console **Sites**, navegue até a cópia de idioma que deseja comparar.
1. Abra o painel **[Referências](/help/sites-authoring/basic-handling.md#references)**.
1. No cabeçalho **Cópias** selecione **Cópias de Idioma.**
1. Selecione sua cópia de idioma específica e clique em **Comparar com Principal **ou **Comparar com anterior **se aplicável.

   ![chlimage_1-37](assets/chlimage_1-37.jpeg)

1. As duas páginas (lançamento e origem) serão abertas lado a lado.

   Para obter informações completas sobre como usar esse recurso, consulte [Diferencial de página](/help/sites-authoring/page-diff.md).

## Concluindo e Arquivando Trabalhos de Tradução {#completing-and-archiving-translation-jobs}

Conclua um trabalho de tradução depois de revisar os arquivos traduzidos do fornecedor. Para os workflows de tradução humanos, o preenchimento de uma tradução indica ao vendedor que o contrato de tradução foi cumprido e que devem guardar a tradução na sua memória de tradução.

Após concluir o trabalho, ele terá o status Concluído.

![chlimage_1-272](assets/chlimage_1-272.png)

Arquive um trabalho de tradução após sua conclusão e não é mais necessário ver os detalhes do status do trabalho. Quando você arquiva o trabalho, o bloco Trabalho de tradução é removido do projeto.

## Criação da estrutura de uma cópia de idioma {#creating-the-structure-of-a-language-copy}

Preencha sua cópia de idioma para que contenha conteúdo do idioma principal que você está traduzindo. Antes de preencher sua cópia de idioma, você deve ter [criado a raiz de idioma](/help/sites-administering/tc-prep.md#creating-a-language-root) da cópia de idioma.

1. Use o console Sites para selecionar a raiz do idioma principal que você está usando como fonte. Por exemplo, para traduzir as páginas em inglês do Site de demonstração de Geometrixx, selecione Conteúdo > Site de demonstração de Geometrixx > Inglês.
1. Na barra de ferramentas, clique ou toque em Referências.

   ![chlimage_1-273](assets/chlimage_1-273.png)

1. Selecione Cópias de idioma e, em seguida, selecione as cópias de idioma que deseja preencher.

   ![chlimage_1-38](assets/chlimage_1-38.jpeg)

1. Clique ou toque em Atualizar cópias de idioma para revelar as ferramentas de tradução e configure as propriedades:

   * Selecione a opção Selecionar todas as subpáginas.
   * Para Projeto, selecione Criar somente estrutura.

   ![chlimage_1-39](assets/chlimage_1-39.jpeg)

1. Clique ou toque em Start.

## Criando um projeto de tradução usando o console Projetos {#creating-a-translation-project-using-the-projects-console}

Você pode criar manualmente um projeto de tradução se preferir usar o console Projetos.

Ao criar manualmente um projeto de tradução, você deve fornecer valores para as seguintes propriedades relacionadas à tradução, além das [propriedades básicas](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project):

* **Nome:nome** do projeto.
* **Idioma de origem:** o idioma do conteúdo de origem.
* **Idioma do público alvo:** o idioma no qual o conteúdo está sendo traduzido.
* **Método de tradução:** selecione Tradução humana para indicar que a tradução deve ser executada manualmente.

1. Na barra de ferramentas do console Projetos, clique ou toque em Criar.
1. Selecione o modelo Projeto de tradução e clique ou toque em Avançar.
1. Insira valores para as propriedades Básicas.
1. Clique ou toque em Avançado e forneça valores para as propriedades relacionadas à tradução.
1. Clique ou toque em Criar. Na caixa de confirmação, clique ou toque em Concluído para retornar ao console Projetos ou clique ou toque em Abrir projeto para abrir e start gerenciar o projeto.

## Exportando um trabalho de tradução {#exporting-a-translation-job}

Você pode baixar o conteúdo de um trabalho de tradução, por exemplo, para enviar a um provedor de tradução que não esteja integrado ao AEM por meio de um conector ou para revisar o conteúdo.

1. No menu suspenso do bloco Trabalho de tradução, clique ou toque em Exportar.
1. Na caixa de diálogo Exportar, clique ou toque em Baixar arquivo exportado e, se necessário, use a caixa de diálogo do navegador da Web para salvar o arquivo.
1. Na caixa de diálogo Exportar, clique ou toque em Fechar.

## Importando um trabalho de tradução {#importing-a-translation-job}

Você pode importar conteúdo convertido para o AEM, por exemplo, quando seu provedor de tradução o envia para você porque ele não está integrado ao AEM por meio de um conector.

1. No menu suspenso do bloco Trabalho de tradução, clique ou toque em Importar.
1. Use a caixa de diálogo do navegador da Web para selecionar o arquivo a ser importado.
1. Na caixa de diálogo Importar, clique ou toque em Fechar.

