---
title: Ecrã inicial
seo-title: Ecrã inicial
description: Descrição dos componentes da tela inicial do aplicativo AEM Forms
seo-description: Descrição dos componentes da tela inicial do aplicativo AEM Forms
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# Tela inicial{#home-screen}

Ao fazer logon no aplicativo AEM Forms, você é redirecionado para a tela inicial.

## Tela inicial padrão {#default-home-screen}

Por padrão, a tela Início exibe todos os formulários, incluindo pontos de partida e tarefas (se o servidor conectado estiver habilitado para o AEM Forms Workflow), juntamente com as miniaturas associadas. É possível especificar as miniaturas no servidor AEM Forms.

A figura a seguir é anotada com chamadas para os componentes essenciais na tela inicial padrão.

![Tela inicial do aplicativo Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Botão** Menu: Toque no  **** botão Menu para navegar até Tarefa, Forms, Caixa de saída e Configurações. Se seu aplicativo AEM Forms estiver conectado a um servidor AEM Forms JEE, você poderá ver a opção Tarefa. A opção Tarefas também armazena os rascunhos criados a partir do tarefa em um processo. Para servidores AEM Forms OSGi, a opção Tarefa está oculta. A caixa de saída armazena os formulários e rascunhos salvos antes de sincronizar com o servidor. Todos os formulários e rascunhos salvos na caixa de saída são carregados no servidor AEM Forms quando o aplicativo é [sincronizado com o servidor](../../forms/using/sync-app.md). Para obter informações sobre Configurações, consulte [Atualizar Configurações Gerais](../../forms/using/update-general-settings.md).
1. **Tarefa ou formulário**: Toque na tarefa ou formulário listado com o qual você deseja trabalhar.
1. **Reticências** horizontais: Indica que as ações estão disponíveis para o formulário. Tocar nas reticências exibe as ações e a descrição fornecidas pelo autor. A opção **Excluir rascunho** e **Concluir** fica visível quando você toca nas reticências.
1. **Ícone** Atualizar: Toque no ícone de atualização para sincronizar seu aplicativo com o servidor AEM Forms.

### Personalização da tela inicial {#customizing-the-home-screen}

![Configurações gerais](assets/gen-settings.png)

Você pode alterar a tela inicial padrão do aplicativo a partir das **[Configurações gerais](../../forms/using/update-general-settings.md)** do aplicativo, ou da guia **Preferência** no espaço de trabalho HTML.

A alteração feita na configuração da tela inicial no aplicativo afeta a tela inicial do usuário registrado no dispositivo móvel atual.

No entanto, a alteração feita na área de trabalho HTML afeta todos os usuários do aplicativo AEM Forms conectados ao servidor AEM Forms.
