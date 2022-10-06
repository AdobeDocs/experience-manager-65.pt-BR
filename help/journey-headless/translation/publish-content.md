---
title: Publicar conteúdo traduzido
description: Saiba como publicar seu conteúdo traduzido e atualizar as traduções como atualizações de conteúdo.
exl-id: 32c387fe-fa1b-499b-861f-b4822f5e139e
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 82%

---

# Publicar conteúdo traduzido {#publish-content}

Saiba como publicar seu conteúdo traduzido e atualizar as traduções como atualizações de conteúdo.

## A história até agora {#story-so-far}

No documento anterior da jornada de tradução AEM sem cabeçalho, [Traduzir conteúdo,](configure-connector.md) você aprendeu a usar AEM Projetos de tradução para traduzir seu conteúdo sem periféricos. Agora você deve:

* Entender o que é um projeto de tradução.
* Ser capaz de criar novos projetos de tradução.
* Use projetos de tradução para traduzir o conteúdo sem periféricos.

Agora que sua tradução inicial foi concluída, este artigo o orienta pela próxima etapa da publicação desse conteúdo e o que fazer para atualizar suas traduções como o conteúdo subjacente nas alterações de raiz do idioma.

## Objetivo {#objective}

Este documento ajuda você a entender como publicar conteúdo sem periféricos no AEM e como criar um fluxo de trabalho contínuo para manter suas traduções atualizadas. Após ler este documento, você deve:

* Entender o modelo de publicação do autor do AEM.
* Saber como publicar seu conteúdo traduzido.
* Ser capaz de implementar um modelo de atualização contínuo para o conteúdo traduzido.

## Modelo de publicação do autor do AEM {#author-publish}

Antes de publicar seu conteúdo, é uma boa ideia entender o modelo de publicação do autor do AEM. De forma simples, o AEM divide os usuários do sistema em dois grupos.

1. Aqueles que criam e gerenciam o conteúdo e o sistema
1. Aqueles que consomem o conteúdo do sistema

Portanto, o AEM é fisicamente separado em duas instâncias.

1. A instância do **autor** é o sistema no qual os autores e administradores de conteúdo trabalham para criar e gerenciar conteúdo.
1. A instância de **publicação** é o sistema que entrega o conteúdo para os consumidores.

Depois que o conteúdo é criado na instância do autor, ele deve ser transferido para a instância de publicação para que esteja disponível para consumo. O processo de transferência do autor para a publicação é chamado de **publicação**.

## Publicar seu conteúdo traduzido {#publishing}

Quando estiver satisfeito com o estado do seu conteúdo traduzido, ele deverá ser publicado para que os serviços sem periféricos possam consumi-lo. Normalmente, essa tarefa não é de responsabilidade do especialista em tradução, mas está documentada aqui para ilustrar o fluxo de trabalho completo.

>[!NOTE]
>
>Geralmente, quando a tradução é concluída, o especialista em tradução informa aos proprietários do conteúdo que as traduções estão prontas para publicação. Os proprietários do conteúdo os publicam.
>
>As etapas a seguir são fornecidas para fins de integridade.

A maneira mais simples de publicar as traduções é navegar até a pasta de ativos do projeto.

```text
/content/dam/<your-project>/
```

Nesse caminho, você tem subpastas para cada idioma de tradução e pode escolher qual publicar.

1. Ir para **Navegação** -> **Ativos** -> **Arquivos** e abra a pasta do projeto.
1. Aqui você vê a pasta raiz do idioma e todas as outras pastas de idioma. Selecione o idioma ou idiomas localizados que deseja publicar.
   ![Selecionar pasta de idioma](assets/select-language-folder.png)
1. Toque ou clique em **Gerenciar publicação**.
1. Na janela **Gerenciar publicação**, verifique se **Publicar** é automaticamente selecionado em **Ação** e se **Agora** é selecionado em **Agendamento**. Toque ou clique em **Próximo**.
   ![Gerenciar opções de publicação](assets/manage-publication-options.png)
1. Na próxima janela **Gerenciar publicação**, confirme se os caminhos adequados estão selecionados. Toque ou clique em **Publicar**.
   ![Gerenciar escopo de publicação](assets/manage-publication-scope.png)
1. AEM confirma a ação de publicação com uma mensagem pop-up na parte superior da tela.
   ![Banner de recursos publicados](assets/resources-published-message.png)

Seu conteúdo traduzido sem cabeçalho foi publicado! Agora ele pode ser acessado e consumido pelos serviços sem periféricos.

>[!TIP]
>
>Você pode selecionar vários itens (ou seja, várias pastas de idioma) durante a publicação para publicar várias traduções de uma vez.

Há opções adicionais ao publicar seu conteúdo, como agendar um horário de publicação, que estão além do escopo desta jornada. Consulte a seção [Recursos adicionais](#additional-resources) no final do documento para obter mais informações.

## Atualizar o conteúdo traduzido {#updating-translations}

A tradução raramente é uma atividade pontual. Normalmente, seus autores de conteúdo continuam a adicionar e modificar conteúdo na raiz do idioma depois que a tradução inicial é concluída. Isso significa que também é necessário atualizar o conteúdo traduzido.

Requisitos específicos do projeto definem a frequência com que você precisa atualizar suas traduções e qual processo de decisão é seguido antes de executar uma atualização. Depois de decidir atualizar suas traduções, o processo no AEM é muito simples. Como a tradução inicial foi baseada em um projeto de tradução, as atualizações também serão.

No entanto, assim como antes, o processo é um pouco diferente se você opta por criar automaticamente ou manualmente seu projeto de tradução.

### Atualizar um projeto de tradução criado automaticamente {#updating-automatic-project}

1. Navegue até **Navegação** -> **Ativos** -> **Arquivos**. Lembre-se de que o conteúdo sem periféricos no AEM é armazenado como ativos conhecidos como Fragmentos de conteúdo.
1. Selecione a raiz do idioma do projeto. Nesse caso, selecionamos `/content/dam/wknd/en`.
1. Toque ou clique no seletor do painel e exiba o painel **Referências**.
1. Toque ou clique em **Cópias de idioma**.
1. Marque a caixa de seleção **Cópias de idioma**.
1. Expanda a seção **Atualizar cópias de idioma** na parte inferior do painel de referências.
1. Na lista suspensa **Projeto**, selecione **Adicionar a um projeto de tradução existente**.
1. Na lista suspensa **Projeto de tradução existente**, selecione o projeto criado para a tradução inicial.
1. Toque ou clique **Iniciar**.

![Adicionar itens ao projeto de tradução existente](assets/add-to-existing-project.png)

O conteúdo é adicionado ao projeto de tradução existente. Para exibir o projeto de tradução:

1. Navegue até **Navegação** -> **Projetos**.
1. Toque ou clique no projeto que acabou de atualizar.
1. Toque ou clique no idioma ou em um dos idiomas atualizados.

Você vê que novos cartões de trabalho são adicionados ao projeto, conforme apropriado.

<!--
You see that a new job card was added to the project. In this example, another Spanish translation was added.

![Additional translation job added](assets/additional-translation-job.png)
-->

Observe que as estatísticas listadas no novo cartão (número de ativos e fragmentos de conteúdo) são diferentes. Isso ocorre porque o AEM reconhece o que mudou desde a última tradução e inclui apenas o conteúdo que precisa ser traduzido. Isso inclui a nova tradução do conteúdo atualizado, bem como a primeira tradução do novo conteúdo.

A partir deste ponto, você [inicia e gerencia seu trabalho de tradução da mesma forma que fazia com o original.](translate-content.md#using-translation-project)

### Atualizar um projeto de tradução criado manualmente {#updating-manual-project}

Para atualizar uma tradução, é possível adicionar um novo trabalho ao projeto existente, responsável pela tradução do conteúdo atualizado.

1. Navegue até **Navegação** -> **Projetos**.
1. Toque ou clique no projeto que precisa atualizar.
1. Toque ou clique no botão **Adicionar**, na parte superior da janela.
1. Na janela **Adicionar mosaico**, toque ou clique em **Tarefa de tradução** e depois em **Enviar**.

   ![Adicionar mosaico](assets/add-translation-job-tile.png)

1. No cartão do novo trabalho de tradução, toque ou clique no botão divisa na parte superior do cartão e selecione **Atualizar destino** para definir o idioma de destino da nova tarefa.

   ![Atualizar destino](assets/update-target.png)

1. Na caixa de diálogo **Selecionar idioma de destino**, use o menu suspenso para selecionar o idioma e toque ou clique em **Concluído**.

   ![Selecionar idioma de destino](assets/select-target-language.png)

1. Depois que o idioma de destino do novo trabalho de tradução for definido, toque ou clique no botão de reticências, na parte inferior do cartão de tarefa, para exibir os detalhes da tarefa.
1. A tarefa fica vazia quando é criada pela primeira vez. Adicione conteúdo à tarefa tocando ou clicando no botão **Adicionar** e usando o navegador de caminho [como você fez antes ao criar originalmente o projeto de tradução.](translate-content.md##manually-creating)

>[!TIP]
>
>Os filtros potentes do navegador de caminho podem ser úteis novamente para localizar apenas o conteúdo que foi atualizado.
>
>Você pode saber mais sobre o navegador de caminho na [seção recursos adicionais.](#additional-resources)

A partir deste ponto, [inicie e gerencie seu trabalho de tradução da mesma forma que fazia com o original.](translate-content.md#using-translation-project)

## Fim da jornada? {#end-of-journey}

Parabéns. Você concluiu a jornada de tradução sem cabeçalho! Agora você deve:

* Ter uma visão geral do que é a entrega de conteúdo sem periféricos.
* Tenha um Compreensão básica AEM recursos headless.
* Entenda AEM recursos de tradução e como eles estão relacionados ao conteúdo sem periféricos.
* Tenha a capacidade de começar a traduzir seu próprio conteúdo sem periféricos.

Agora você está pronto para traduzir seu próprio conteúdo sem periféricos em AEM. No entanto, o AEM é uma ferramenta poderosa e há muitas opções adicionais disponíveis. Confira alguns dos recursos adicionais disponíveis na [seção Recursos adicionais](#additional-resources) para saber mais sobre os recursos que você viu nesta jornada.

## Recursos adicionais {#additional-resources}

* [Gerenciamento de projetos de tradução](/help/sites-administering/tc-manage.md) - Saiba mais sobre os detalhes de projetos de tradução e recursos adicionais, como fluxos de trabalho de tradução humana e projetos multilíngues.
* [Conceitos de criação](/help/sites-authoring/author.md) - Saiba mais sobre o modelo de criação e publicação do AEM em detalhes. Este documento está focado na criação de páginas em vez de Fragmentos de conteúdo, mas a teoria ainda se aplica.
* [Publicar páginas](/help/sites-authoring/publishing-pages.md) - Saiba mais sobre os recursos adicionais disponíveis ao publicar conteúdo. Este documento está focado na criação de páginas em vez de Fragmentos de conteúdo, mas a teoria ainda se aplica.
* [Ambiente e ferramentas de criação](/help/sites-authoring/author-environment-tools.md##path-selection) - O AEM fornece vários mecanismos para organização e edição de conteúdo, incluindo um navegador de caminho robusto.
