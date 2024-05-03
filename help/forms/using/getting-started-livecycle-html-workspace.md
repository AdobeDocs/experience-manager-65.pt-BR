---
title: Introdução ao AEM Forms Workspace
description: Introdução ao uso do espaço de trabalho do LiveCycle AEM Forms para gerenciar seus processos de automação de negócios.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: d2a962b6-16be-4866-a856-5064f81c9610
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 0%

---

# Introdução ao AEM Forms Workspace {#getting-started-with-aem-forms-workspace}

Você pode usar o espaço de trabalho do AEM Forms para executar as seguintes tarefas:

* Iniciar um processo de negócios
* Exibir e agir sobre tarefas atribuídas a você ou a outras listas de tarefas às quais você tem acesso
* Rastrear tarefas que fazem parte dos processos que você iniciou ou em que participou

## Navegação no espaço de trabalho do AEM Forms {#navigating-html-workspace}

Itens diferentes na interface do usuário do AEM Forms Workspace são exibidos dependendo do processo e da tarefa em que você está trabalhando. Você pode ou não ver as guias Resumo, Forms, Detalhes, Histórico, Anexos, Notas ou todos os botões descritos nesta Ajuda o tempo todo.

É possível navegar na interface principal do usuário do AEM Forms Workspace usando um dos seguintes métodos:

* Clique nos itens na barra de navegação superior para acessar a opção Iniciar processo, Lista de tarefas, Preferências, Rastreamento, Ajuda e logout.
* Clique na guia Iniciar processo, Lista de tarefas ou Rastreamento para acessar as três principais áreas de trabalho.
* Nas guias Iniciar processo, Tarefa pendente e Rastreamento, clique nos itens da lista no painel esquerdo para acessar favoritos, categorias de processo, modelos de pesquisa, rascunhos ou tarefas atribuídas. Use a barra de rolagem para ver itens adicionais na lista.
* Todos os botões de ação (Aprovar, Rejeitar, Encaminhar, Consultar, Bloquear e Compartilhar) são exibidos no documento e na Propriedade.
* Clique no ícone Todas as opções na barra de navegação, na parte inferior da página, para encaminhar a tarefa para outro usuário, para compartilhá-la com outro usuário, para consultar a tarefa com outro usuário ou para bloqueá-la.
* Na guia Histórico, selecione uma tarefa para exibir as guias Anexos e Atribuições dessa tarefa.
* Use a tecla tab, as teclas de seta e a barra de espaço para navegar pelo espaço de trabalho do AEM Forms sem usar o mouse.

## Uso do espaço de trabalho do AEM Forms com leitores de tela {#using-html-workspace-with-screen-readers}

O espaço de trabalho do AEM Forms é um aplicativo HTML baseado na web e é compatível com leitores de tela. É possível navegar pela interface do espaço de trabalho do AEM Forms usando o teclado.

Para usar o espaço de trabalho do AEM Forms com um leitor de tela, lembre-se destes pontos:

* O espaço de trabalho do AEM Forms é um aplicativo HTML padrão compatível com qualquer ferramenta de leitor de tela padrão. Não é necessário nenhum script específico para executar uma ferramenta de leitor de tela.
* Toda a navegação no espaço de trabalho do AEM Forms é feita por meio de tags de âncora, que podem ser facilmente acessadas por meio de guias.
* O Forms pode levar alguns segundos para carregar. O leitor de tela não informa de forma audível que o formulário está sendo carregado e que você deve aguardar.

## Navegar pelo espaço de trabalho do AEM Forms usando um teclado {#navigating-html-workspace-using-a-keyboard}

Ao navegar na área de trabalho do AEM Forms usando um teclado, a navegação está em conformidade com as convenções de acessibilidade do HTML. Em determinadas situações, a ordem de tabulação não segue a ordem convencional típica. As seguintes dicas ajudam a navegar na interface:

* Se você tiver problemas ao tabular para fora das barras de ferramentas na parte superior do navegador, pressione Ctrl+Tab para tabular no conteúdo da janela do navegador.
* A Ajuda da área de trabalho do AEM Forms é aberta em uma janela separada do navegador. Depois de exibir a Ajuda, o foco retorna à janela do navegador que contém o espaço de trabalho do AEM Forms. O menu Ajuda permanece focalizado quando o foco retorna.
* Ao abrir um formulário para iniciar um processo ou concluir uma tarefa, o foco permanece com o elemento existente e não é alterado para o formulário. Use tab para mover o foco para o formulário e navegue por ele. A ordem de tabulação no formulário depende do tipo e do design do formulário.

  Para PDF forms, ao passar por tabulação até o final do formulário ou enviá-lo, o foco do cursor salta para a barra de endereço do navegador. Siga os menus novamente (mas não o formulário inteiro) para acessar os botões de ação do formulário, como Salvar como rascunho e Concluído. Se o formulário ainda estiver aberto, você também poderá passar pelos botões e voltar ao formulário.

## Gerenciamento de preferências {#managing-preferences}

Você pode definir as várias preferências do espaço de trabalho do AEM Forms nas seguintes categorias:

**Fora do escritório:** Defina preferências para controlar como as tarefas são atribuídas a outras pessoas enquanto você estiver fora do escritório. Consulte [Definição das preferências de ausência temporária](todo-lists.md#setting-out-of-office-preferences).

**Filas:** Defina preferências para compartilhar sua lista de tarefas com outros usuários ou para solicitar acesso à lista de outro usuário. Consulte [Trabalhar com tarefas de filas de grupo e compartilhadas](todo-lists.md#working-with-tasks-from-group-and-shared-queues).

**Configurações da interface:** Defina as preferências de como você interage com o espaço de trabalho do AEM Forms. Consulte [Definir preferências da interface do usuário](#set-user-interface-preferences).

### Definir preferências da interface do usuário {#set-user-interface-preferences}

Defina as preferências da interface do usuário na guia Preferências > Configurações da interface. As preferências a seguir estão disponíveis.

* **Local de Início:** Especifica a página que aparece ao fazer logon no espaço de trabalho do AEM Forms. As quatro opções disponíveis são Iniciar processo, Tarefa pendente, Rastreamento e Favoritos.
* **Aviso de saída:** Especifica se você será solicitado a confirmar que deseja efetuar logout após clicar em Fazer Logoff.
* **Formato de data:** Especifica o formato de exibição de data usado no espaço de trabalho do AEM Forms.
* **Formato de hora**: especifica o formato de exibição de hora usado no espaço de trabalho do AEM Forms.
* **Notificar eventos de tarefa por e-mail:** Especifica se você receberá notificações por email sobre eventos de tarefas, incluindo atribuições de tarefas, lembretes e prazos finais para tarefas em sua lista de tarefas pendentes e em listas de tarefas pendentes de grupos às quais você pertence.
* **Anexar o Forms no email:** Especifica se uma cópia do formulário é anexada a mensagens de notificação por email. Os anexos são compatíveis somente com formulários PDF e XDP.
* **Salvar rascunho periodicamente:** Especifica se os rascunhos dos formulários são salvos automaticamente periodicamente ou não. Para salvar os rascunhos periodicamente, ative essa opção e defina a duração do salvamento automático de 1 a 30 minutos. Quando o salvamento automático está ativado e um usuário está trabalhando em um rascunho, o rascunho é salvo periodicamente após o número especificado de minutos. O rascunho é salvo automaticamente somente quando há uma alteração no rascunho desde o último salvamento ou salvamento automático. Quando o rascunho é salvo, uma mensagem de alerta é exibida na tela.
