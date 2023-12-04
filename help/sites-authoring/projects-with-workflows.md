---
title: Trabalhar com fluxos de trabalho de projeto
seo-title: Working with Project Workflows
description: Vários fluxos de trabalho de projeto estão disponíveis imediatamente.
seo-description: A variety of project workflows are available out of the box.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
exl-id: 407fc164-291d-42f6-8c46-c1df9ba3d454
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 40%

---


# Trabalhar com fluxos de trabalho de projeto {#working-with-project-workflows}

Os fluxos de trabalho de projeto disponíveis prontos para uso incluem o seguinte:

* **Fluxo de trabalho para aprovação de projeto** - Esse fluxo de trabalho permite atribuir conteúdo a um usuário, analisar esse conteúdo e depois aprová-lo.
* **Solicitar inicialização** - um fluxo de trabalho que solicita uma inicialização.
* **Solicitar página de aterrissagem** - esse fluxo de trabalho solicita uma página de aterrissagem.
* **Solicitar email** - Fluxo de trabalho para solicitar um email.
* **Sessão fotográfica do produto e sessão fotográfica do produto (Commerce)** - Mapeia ativos com produtos
* **Criar e traduzir cópia do DAM e Criar cópia de idioma do DAM** - cria binários, metadados e tags traduzidos para arquivos e pastas.

Dependendo do modelo de projeto selecionado, há determinados fluxos de trabalho disponíveis:

|   | **Projeto simples** | **Projeto de mídia** | **Projeto de sessão de fotos do produto** | **Projeto de tradução** |
|---|:-:|:-:|:-:|:-:|
| Solicitar cópia |  | x |  |  |
| Sessão fotográfica do produto |  | x | x |  |
| Sessão fotográfica do produto (Commerce) |  |  | x |  |
| Aprovação de Projeto | x |  |  |  |
| Solicitar inicialização | x |  |  |  |
| Solicitar página de aterrissagem | x |  |  |  |
| Solicitar email | x |  |  |  |
| Criar cópia de idioma do DAM&amp;ast; |  |  |  | x |
| Criar e traduzir cópia de idioma do DAM;&amp;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast; Esses fluxos de trabalho não são iniciados no bloco **Fluxo de trabalho** em Projetos. Consulte [Criação de cópias de idioma para ativos.](/help/sites-administering/tc-manage.md)

As etapas para iniciar e concluir fluxos de trabalho são as mesmas, independentemente do fluxo de trabalho escolhido. Somente as etapas são alteradas.

Um fluxo de trabalho é iniciado diretamente em Projetos (exceto para Criar Cópia de Idioma do DAM ou Criar e Traduzir Cópia de Idioma do DAM). Informações sobre quaisquer tarefas pendentes em um projeto estão listadas no bloco **Tarefas**. As notificações para tarefas que precisam ser concluídas são exibidas ao lado do ícone do usuário.

Para obter mais informações sobre como trabalhar com fluxos de trabalho no AEM, consulte os seguintes documentos:

* [Participar de fluxos de trabalho](/help/sites-authoring/workflows-participating.md)
* [Aplicação de fluxos de trabalho a páginas](/help/sites-authoring/workflows-applying.md)
* [Configuração de fluxos de trabalho](/help/sites-administering/workflows.md)

Esta seção descreve os fluxos de trabalho disponíveis para Projetos.

## Solicitar fluxo de trabalho de cópia {#request-copy-workflow}

Esse fluxo de trabalho permite solicitar um manuscrito de um usuário e depois aprová-lo. Para iniciar o workflow de cópia da solicitação:

1. Em um projeto de mídia, clique na divisa para baixo na parte superior direita do **Fluxos de trabalho** mosaico e selecionar **Iniciar fluxo de trabalho**.
1. No assistente do workflow, selecione **Solicitar cópia** e clique em **Próxima**.
1. Insira um título de manuscrito e um breve resumo do que você está solicitando. Se aplicável, insira uma contagem de palavras de destino, uma prioridade de tarefa e uma data de vencimento.

   ![Solicitar fluxo de trabalho de cópia](assets/project-request-copy-workflow.png)

1. Clique em **Enviar**.

O fluxo de trabalho é iniciado. A tarefa aparece no **Tarefas** cartão.

## Fluxo de trabalho da sessão fotográfica do produto {#product-photo-shoot-workflow}

A variável **Sessão fotográfica do produto** os fluxos de trabalho (tanto comércio quanto sem comércio) são abordados detalhadamente no documento [Projetos criativos](/help/sites-authoring/managing-product-information.md)

## Fluxo de trabalho para aprovação do projeto {#project-approval-workflow}

No **Aprovação de Projeto** fluxo de trabalho, você atribui o conteúdo a um usuário, revisa e aprova o conteúdo.

1. Em um projeto simples, clique na divisa para baixo na parte superior direita do **Fluxos de trabalho** mosaico e selecionar **Iniciar fluxo de trabalho**.
1. No assistente do workflow, selecione **Fluxo de trabalho para aprovação de projeto** e clique em **Próxima**.
1. Insira um título e selecione a quem atribuí-lo. Se aplicável, insira uma descrição, o caminho do conteúdo, uma prioridade pra tarefa e um prazo.

   ![Fluxo de trabalho para aprovação de projeto](assets/project-approval-workflow.png)

1. Clique em **Enviar**.

O fluxo de trabalho é iniciado. A tarefa aparece no **Tarefas** cartão.

## Solicitar fluxo de trabalho de inicialização {#request-launch-workflow}

Esse fluxo de trabalho permite solicitar um lançamento.

1. Em um projeto simples, clique na divisa para baixo na parte superior direita do **Fluxos de trabalho** mosaico e selecionar **Iniciar fluxo de trabalho**.
1. No assistente do workflow, selecione **Solicitar fluxo de trabalho de inicialização** e clique em **Próxima**.
1. Insira um título para lançamento e forneça o caminho de origem de lançamento. Também é possível adicionar uma descrição e uma data de ativação, se aplicável. Selecione Herdar dados ativos da página de origem ou excluir subpáginas, dependendo de como deseja que o lançamento se comporte.

   ![Solicitar fluxo de trabalho de inicialização](assets/project-request-launch-workflow.png)

1. Clique em **Enviar**.

O fluxo de trabalho é iniciado. O workflow aparece na variável **Fluxos de trabalho** lista.

## Solicitar fluxo de trabalho da página de aterrissagem {#request-landing-page-workflow}

Esse fluxo de trabalho permite solicitar uma landing page.

1. Em um projeto simples, clique na divisa para baixo na parte superior direita do **Fluxos de trabalho** mosaico e selecionar **Iniciar fluxo de trabalho**.
1. No assistente do workflow, selecione **Solicitar página de destino** e clique em **Próxima**.
1. Insira um título para a página de aterrissagem e o caminho principal. Se aplicável, insira uma data de ativação ou escolha um arquivo para a landing page.

   ![Solicitar fluxo de trabalho de página de aterrissagem](assets/project-request-landing-page-workflow.png)

1. Clique em **Enviar**.

O fluxo de trabalho é iniciado. A tarefa aparece no **Tarefas** cartão.

## Solicitar fluxo de trabalho de email {#request-email-workflow}

Esse workflow permite solicitar um email. É o mesmo workflow que aparece no **Emails** bloco.

1. Em um projeto simples, clique na divisa para baixo na parte superior direita do **Fluxos de trabalho** mosaico e selecionar **Iniciar fluxo de trabalho**.
1. No assistente do workflow, selecione **Solicitar email** e clique em **Próxima**.
1. Insira um título de email e os caminhos da campanha e do template. Além disso, você pode fornecer um nome, uma descrição e uma data de ativação.

   ![Solicitar fluxo de trabalho de email](assets/project-request-email-workflow.png)

1. Clique em **Enviar**.

O fluxo de trabalho é iniciado. A tarefa aparece no **Tarefas** cartão.

## Criar (e traduzir) fluxo de trabalho de cópia de idioma para ativos {#create-and-translate-language-copy-workflow-for-assets}

A variável **Criar cópia de idioma** e a variável **Criar e traduzir cópia de idioma** os fluxos de trabalho são abordados detalhadamente no documento [Criação de cópias de idioma para ativos.](/help/assets/translation-projects.md)
