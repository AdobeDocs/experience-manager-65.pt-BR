---
title: Trabalhar com fluxos de trabalho de projeto
seo-title: Trabalhar com fluxos de trabalho de projeto
description: Há uma variedade de fluxos de trabalho de projeto disponíveis para uso imediato.
seo-description: Há uma variedade de fluxos de trabalho de projeto disponíveis para uso imediato.
uuid: 376922ca-e09e-4ac8-88c8-23dac2b49dbe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 9d2bf30c-5190-4924-82cd-bcdfde24eb39
translation-type: tm+mt
source-git-commit: 0033dfac2540f56b3903c19f6ca19677af050db3
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 85%

---


# Trabalhar com fluxos de trabalho de projeto{#working-with-project-workflows}

Os fluxos de trabalho de projeto disponíveis para uso imediato incluem os seguintes:

* **Fluxo de trabalho**  de aprovação de projeto - Esse fluxo de trabalho permite que você atribua conteúdo a um usuário, revise e aprove.
* **Solicitar lançamento**  - um fluxo de trabalho que solicita uma inicialização.
* **Solicitar Landing page**  - esse fluxo de trabalho solicita uma landing page.
* **Solicitar email** - Fluxo de trabalho para solicitar um email.
* **Sessão fotográfica do produto e Sessão fotográfica do produto (Comércio)** - Mapeia ativos com produtos
* **Criar e traduzir cópia DAM e Criar cópia de idioma DAM** - Cria binários, metadados e tags traduzidos para ativos e pastas.

Dependendo de qual modelo de projeto você selecionar, certos fluxos de trabalho estarão disponíveis:

|  | **Projeto simples** | **Projeto de mídia** | **Projeto de sessão fotográfica do produto** | **Projeto de tradução** |
|---|:-:|:-:|:-:|:-:|
| Solicitar cópia |  | x |  |  |
| Sessão fotográfica do produto |  | x | x |  |
| Foto do produto (Comércio) |  |  | x |  |
| Aprovação do projeto | x |  |  |  |
| Solicitar lançamento | x |  |  |  |
| Solicitar página de aterrissagem | x |  |  |  |
| Solicitar email | x |  |  |  |
| DAM Criar Cópia de Idioma;ast; |  |  |  | x |
| DAM Criar e Traduzir Cópia de Idioma;ast; |  |  |  | x |

>[!NOTE]
>
>&amp;ast; Esses workflows não são iniciados a partir do bloco **Workflow** em Projetos. Consulte [Criação de cópias de idioma para ativos.](/help/sites-administering/tc-manage.md)

As etapas para iniciar e concluir fluxos de trabalho são as mesmas, independentemente do fluxo de trabalho escolhido. Apenas as etapas mudam.

Você inicia um fluxo de trabalho diretamente em Projetos (exceto para Criar cópia de idioma DAM ou Criação e tradução DAM da cópia de idioma). Informações sobre quaisquer tarefas pendentes em um projeto são listadas no bloco **Tarefas**. Notificações de tarefas que precisam ser concluídas aparecem ao lado do ícone de usuário.

Para obter mais informações sobre como trabalhar com fluxos de trabalho no AEM, consulte o seguinte:

* [Participar de fluxos de trabalho](/help/sites-authoring/workflows-participating.md)
* [Aplicação de fluxos de trabalho a páginas](/help/sites-authoring/workflows-applying.md)
* [Configuração de fluxos de trabalho](/help/sites-administering/workflows.md)

Esta seção descreve os fluxos de trabalho disponíveis para Projetos.

## Fluxo de trabalho Solicitar cópia {#request-copy-workflow}

Esse fluxo de trabalho permite solicitar um manuscrito de um usuário e depois aprová-lo. Para iniciar o fluxo de trabalho Solicitar cópia:

1. No projeto Mídia, selecione o sinal **+** no bloco **Fluxos de trabalho** e selecione **Solicitar fluxo de trabalho de cópia**.
1. Insira um título de manuscrito e um breve resumo do que você está solicitando. Se aplicável, insira uma contagem de palavras de destino, uma prioridade de tarefa e uma data de vencimento.

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa é exibida no bloco **Tarefas**.

   ![chlimage_1-322](assets/chlimage_1-322.png)

## Fluxo de trabalho Sessão fotográfica do produto {#product-photo-shoot-workflow}

Os fluxos de trabalho Sessão fotográfica do produto (comércio e sem comércio) são abordados em detalhes em [Projeto criativo](/help/sites-authoring/managing-product-information.md).

## Fluxo de trabalho para aprovação do projeto  {#project-approval-workflow}

No fluxo de trabalho Aprovação de projeto, você atribui conteúdo a um usuário e depois revisa e aprova esse conteúdo.

1. No projeto Simples, selecione o sinal **`+`** no bloco **Workflows** e selecione **Fluxo de Trabalho de Aprovação de Projeto**.
1. Insira um título e selecione a quem ele deve ser atribuído na lista Equipe. Se aplicável, insira uma descrição, um caminho de conteúdo, uma prioridade de tarefa e uma data de vencimento.

   ![chlimage_1-323](assets/chlimage_1-323.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa é exibida no bloco **Tarefas**.

   ![chlimage_1-324](assets/chlimage_1-324.png)

## Fluxo de trabalho Solicitar lançamento {#request-launch-workflow}

Esse fluxo de trabalho permite solicitar um lançamento.

1. No projeto Simples, selecione o sinal **+** no bloco **Fluxos de trabalho** e selecione **Solicitar fluxo de trabalho de inicialização**.
1. Insira um título para o lançamento e forneça o caminho da origem de lançamento. Você também pode adicionar uma descrição e uma data de colocação ao vivo, se aplicável. Selecione Herdar dados online de página fonte ou Excluir subpáginas, dependendo de como você deseja que o lançamento se comporte.

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. O fluxo de trabalho é exibido na lista **Workflows** (clique em elipses **...** no bloco **Workflows** para acessar esta lista).

## Fluxo de trabalho Solicitar página de aterrissagem {#request-landing-page-workflow}

Esse fluxo de trabalho permite solicitar uma página de aterrissagem.

1. Em seu projeto Simples, selecione o sinal de **+** no bloco **Fluxos de trabalho** e selecione Fluxo de trabalho Solicitar página de aterrissagem.
1. Insira um título para sua página de destino e o caminho pai. Se aplicável, insira uma data de colocação ao vivo ou escolha um arquivo para sua página de aterrissagem.

   ![chlimage_1-326](assets/chlimage_1-326.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa é exibida no bloco **Tarefas**.

## Fluxo de trabalho Solicitar email  {#request-email-workflow}

Esse fluxo de trabalho permite solicitar um email. É o mesmo fluxo de trabalho que aparece no bloco **Emails**.

1. Em seu projeto de Mídia ou Simples, selecione o sinal de **+** no bloco **Fluxos de trabalho** e selecione **Fluxo de trabalho Solicitar email**.
1. Insira um título de email, bem como os caminhos da campanha e do modelo. Além disso, você pode fornecer um nome, uma descrição e uma data de colocação ao vivo.

   ![chlimage_1-327](assets/chlimage_1-327.png)

1. Clique em **Criar**. O fluxo de trabalho é iniciado. A tarefa é exibida no bloco **Tarefas**.

   ![chlimage_1-328](assets/chlimage_1-328.png)

## Criar (e Traduzir) fluxo de trabalho de cópia de idioma para ativos {#create-and-translate-language-copy-workflow-for-assets}

Os fluxos de trabalho **Criar cópia de idioma** e **Criar e traduzir da cópia de idioma** são discutidos detalhadamente em [Criar cópias de idioma para ativos.](/help/assets/translation-projects.md)
