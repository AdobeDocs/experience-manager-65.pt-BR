---
title: Tela inicial
seo-title: Home screen
description: Descrição dos componentes da tela inicial do aplicativo AEM Forms
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Tela inicial{#home-screen}

Ao fazer logon no aplicativo AEM Forms, você é redirecionado para a tela inicial.

## Tela inicial padrão {#default-home-screen}

Por padrão, a tela inicial exibe todos os formulários, incluindo os pontos de partida e as tarefas (se o servidor conectado estiver habilitado para o AEM Forms Workflow), juntamente com as miniaturas associadas. Você pode especificar as miniaturas no servidor do AEM Forms.

A figura a seguir é anotada com chamadas para os componentes essenciais na tela inicial padrão.

![Tela inicial do aplicativo Forms](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **Botão Menu**: Toque no **Menu** para navegar até Tarefas, Forms, Caixa de saída e Configurações. Se o aplicativo AEM Forms estiver conectado a um servidor JEE AEM Forms, você poderá ver a opção Tarefas . A opção Tarefas também armazena os rascunhos criados a partir de tarefas em um processo. Para servidores OSGi da AEM Forms, a opção Tarefas está oculta. A caixa de saída armazena os formulários e rascunhos salvos antes de sincronizar com o servidor. Todos os formulários e rascunhos salvos na Caixa de saída são carregados no servidor do AEM Forms quando o aplicativo é [sincronizado com o servidor](../../forms/using/sync-app.md). Para obter informações sobre Configurações, consulte [Atualizar configurações gerais](../../forms/using/update-general-settings.md).
1. **Tarefa ou formulário**: Toque na tarefa ou formulário listado com o qual deseja trabalhar.
1. **Reticências Horizontais**: Indica que as ações estão disponíveis para o formulário. Tocar no elipse exibe as ações e a descrição fornecidas pelo autor. O **Excluir rascunho** e **Concluído** é visível ao tocar nas reticências.
1. **Ícone Atualizar**: Toque no ícone de atualização para sincronizar o aplicativo com o servidor do AEM Forms.

### Personalização da tela inicial {#customizing-the-home-screen}

![Configurações gerais](assets/gen-settings.png)

Você pode alterar a tela inicial padrão do aplicativo na **[Configurações gerais](../../forms/using/update-general-settings.md)** do aplicativo ou do **Preferência** no HTML Workspace.

A alteração feita na configuração da tela inicial no aplicativo afeta a tela inicial do usuário atual registrado no dispositivo móvel atual.

No entanto, a alteração feita no HTML Workspace afeta todos os usuários de aplicativos do AEM Forms conectados ao servidor do AEM Forms.
