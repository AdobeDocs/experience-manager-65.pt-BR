---
title: Introdução ao AEM Forms workspace
seo-title: Getting started with AEM Forms workspace
description: Como começar a usar a área de trabalho do LiveCycle AEM Forms para gerenciar os processos de automação de negócios.
seo-description: How to get started with using the LiveCycle AEM Forms workspace to manage your business automation processes.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Introdução ao AEM Forms workspace {#getting-started-with-aem-forms-workspace}

Você pode usar o espaço de trabalho do AEM Forms para executar as seguintes tarefas:

* Iniciar um processo de negócios
* Exibir e agir de acordo com as tarefas atribuídas a você ou a outras listas de tarefas às quais você tem acesso
* Rastrear tarefas que fazem parte dos processos em que você iniciou ou participou

## Navegação no espaço de trabalho do AEM Forms {#navigating-html-workspace}

Itens diferentes na interface do usuário do espaço de trabalho do AEM Forms são exibidos dependendo do processo e da tarefa em que você está trabalhando. Você pode ou não ver as guias Resumo, Forms, Detalhes, Histórico, Anexos ou Notas ou todos os botões descritos nesta Ajuda o tempo todo.

Você pode navegar pela interface do usuário principal do espaço de trabalho do AEM Forms usando qualquer um dos métodos a seguir:

* Clique nos itens na barra de navegação superior para acessar a opção Iniciar processo, lista de itens a fazer, Preferências, Rastreamento, Ajuda e logout.
* Clique na guia Iniciar processo, Desfazer ou Rastreamento para acessar as três principais áreas de trabalho.
* Nas guias Iniciar processo, Desfazer e Rastreamento, clique nos itens na lista no painel à esquerda para acessar os favoritos, categorias de processo, modelos de pesquisa, rascunhos ou tarefas atribuídas. Use a barra de rolagem para ver itens adicionais na lista.
* Todos os botões de ação - Aprovar, Rejeitar, Encaminhar, Consultar, Bloquear e Compartilhar - são exibidos em ambos, o documento e a Propriedade.
* Clique no ícone Todas as opções na barra de navegação, na parte inferior da página, para encaminhar a tarefa para outro usuário, para compartilhar a tarefa com outro usuário, para consultar a tarefa com outro usuário ou para bloquear a tarefa.
* Na guia History , selecione uma tarefa para exibir as guias Attachments and Assignments para essa tarefa.
* Use a tecla tab, as teclas de seta e a barra de espaço para navegar pelo espaço de trabalho do AEM Forms sem usar o mouse.

## Uso da área de trabalho do AEM Forms com leitores de tela {#using-html-workspace-with-screen-readers}

O AEM Forms workspace é um aplicativo HTML baseado na web e é compatível com leitores de tela. Você pode navegar pela interface do espaço de trabalho do AEM Forms usando o teclado.

Para usar a espaço de trabalho do AEM Forms com um leitor de tela, lembre-se dos seguintes pontos:

* O AEM Forms workspace é um aplicativo HTML padrão que está em conformidade com qualquer ferramenta de leitor de tela padrão. Você não precisa de nenhum script específico para executar uma ferramenta de leitor de tela.
* Toda a navegação no espaço de trabalho do AEM Forms é por meio de tags de âncora, que podem ser acessadas facilmente por meio de guias.
* O Forms pode levar alguns segundos para carregar. O leitor de tela não informa à toa que o formulário está sendo carregado e que você deve aguardar.

## Navegação pelo espaço de trabalho do AEM Forms usando um teclado {#navigating-html-workspace-using-a-keyboard}

Quando você navega no espaço de trabalho do AEM Forms usando um teclado, a navegação está em conformidade com as convenções de acessibilidade do HTML. Em determinadas situações, a ordem de tabulação não segue a ordem convencional típica. As dicas a seguir ajudam a navegar na interface:

* Se tiver problemas ao sair das barras de ferramentas na parte superior do navegador, pressione Ctrl+Tab para acessar o conteúdo da janela do navegador.
* A Ajuda do espaço de trabalho do AEM Forms é aberta em uma janela separada do navegador. Após visualizar a Ajuda, o foco volta para a janela do navegador que contém o espaço de trabalho do AEM Forms. O menu Ajuda permanece focado quando o foco volta.
* Ao abrir um formulário para iniciar um processo ou concluir uma tarefa, o foco permanece com o elemento existente e não é alterado para o formulário. Use a guia para mover o foco para o formulário e navegar por ele. A ordem de tabulação por meio do formulário depende do tipo e do design do formulário.

   Para PDF forms, quando você navega até o final do formulário ou envia o formulário, o foco do cursor salta para a barra de endereços do navegador. É necessário percorrer os menus novamente (mas não o formulário inteiro) para acessar os botões de ação do formulário, como Salvar como rascunho e Concluído. Se o formulário ainda estiver aberto, também é possível tabular depois dos botões e retornar ao formulário.

## Gerenciamento de preferências {#managing-preferences}

Você pode definir as várias preferências do espaço de trabalho do AEM Forms nas seguintes categorias:

**Fora do Escritório:** Defina as preferências para controlar como as tarefas são atribuídas a outras pessoas enquanto você estiver fora do escritório. Consulte [Configuração de preferências fora do escritório](todo-lists.md#setting-out-of-office-preferences).

**Filas:** Defina as preferências para compartilhar sua lista de itens a fazer com outros usuários ou para solicitar acesso a outra lista de usuários. Consulte [Trabalhar com tarefas de grupos e filas compartilhadas](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Configurações da interface do usuário:** Defina as preferências de como você interage com o espaço de trabalho do AEM Forms. Consulte [Definir preferências da interface do usuário](#set-user-interface-preferences).

### Definir preferências da interface do usuário {#set-user-interface-preferences}

Defina as preferências da interface do usuário na guia Preferências > Configurações da interface do usuário . As preferências a seguir estão disponíveis.

* **Localização inicial:** Especifica a página que é exibida quando você faz logon no AEM Forms workspace. As quatro opções disponíveis são Iniciar processo, Fazer, Rastreamento e Favoritos.
* **Aviso de Logout:** Especifica se você é solicitado a confirmar que deseja fazer logoff depois de clicar em Fazer logoff.
* **Formato de data:** Especifica o formato de exibição de data usado na área de trabalho do AEM Forms.
* **Formato de hora**: Especifica o formato de exibição de tempo usado na área de trabalho do AEM Forms.
* **Notificar eventos de tarefa por email:** Especifica se você recebe notificações por email para eventos de tarefa, incluindo atribuições de tarefa, lembretes e prazos para tarefas em sua lista de Tarefas Pendentes e em listas de Tarefas Pendentes às quais você pertence.
* **Anexar o Forms no Email:** Especifica se uma cópia do formulário está anexada a mensagens de notificação por email. Anexos são suportados apenas para formulários PDF e XDP.
* **Salvar rascunho periodicamente:** Especifica se os rascunhos do formulário são salvos automaticamente periodicamente ou não. Para salvar seus rascunhos periodicamente, ative essa opção e defina a duração do salvamento automático de 1 a 30 minutos. Quando o salvamento automático é ativado e um usuário está trabalhando em um rascunho, o rascunho é salvo periodicamente após o número especificado de minutos. O rascunho é salvo automaticamente somente quando há uma alteração no rascunho desde a última gravação ou salvamento automático. Quando o rascunho for salvo, uma mensagem de alerta será exibida na tela.
