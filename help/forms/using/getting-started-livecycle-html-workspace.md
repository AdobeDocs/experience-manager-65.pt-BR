---
title: Introdução à área de trabalho do AEM Forms
seo-title: Introdução à área de trabalho do AEM Forms
description: Como começar a usar a área de trabalho do LiveCycle AEM Forms para gerenciar seus processos de automação de negócios.
seo-description: Como começar a usar a área de trabalho do LiveCycle AEM Forms para gerenciar seus processos de automação de negócios.
uuid: 35ca1a51-92c3-40d8-8de3-604be8704752
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fa6e0246-6bd2-4ffb-b54c-15eda605f213
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Introdução à área de trabalho do AEM Forms {#getting-started-with-aem-forms-workspace}

Você pode usar a área de trabalho do AEM Forms para executar as seguintes tarefas:

* Start de um processo de negócios
* Visualização e agir de acordo com tarefas atribuídas a você ou a outras listas de tarefas que você tenha acesso a
* Rastrear tarefas que fazem parte dos processos em que você começou ou participou

## Navegação na área de trabalho do AEM Forms {#navigating-html-workspace}

Diferentes itens na interface do usuário da área de trabalho do AEM Forms são exibidos dependendo do processo e da tarefa em que você está trabalhando. Você pode ou não ver as guias Resumo, Formulários, Detalhes, Histórico, Anexos ou Anotações, ou todos os botões descritos nesta Ajuda o tempo todo.

Você pode navegar pela interface principal do usuário da área de trabalho do AEM Forms usando qualquer um dos seguintes métodos:

* Clique nos itens na barra de navegação superior para acessar as opções Processo de Start, lista para fazer, Preferências, Rastreamento, Ajuda e logout.
* Clique na guia Processo de Start, Desfazer ou Rastreamento para acessar as três principais áreas de trabalho.
* Nas guias Processo de Start, Desfazer e Rastreamento, clique nos itens na lista no painel esquerdo para acessar os favoritos, processar categorias, modelos de pesquisa, rascunhos ou tarefas atribuídas. Use a barra de rolagem para ver itens adicionais na lista.
* Todos os botões de ação - Aprovar, Rejeitar, Encaminhar, Consultar, Bloquear e Compartilhar - são exibidos em ambos, o documento e a Propriedade.
* Clique no ícone Todas as opções na barra de navegação, na parte inferior da página, para encaminhar a tarefa para outro usuário, para compartilhar a tarefa com outro usuário, para consultar a tarefa com outro usuário ou para bloquear a tarefa.
* Na guia Histórico, selecione uma tarefa para exibir as guias Anexos e Atribuições para essa tarefa.
* Use a tecla tab, as teclas de seta e a barra de espaço para navegar pela área de trabalho do AEM Forms sem usar o mouse.

## Uso da área de trabalho do AEM Forms com leitores de tela {#using-html-workspace-with-screen-readers}

A área de trabalho do AEM Forms é um aplicativo HTML baseado na Web e é compatível com leitores de tela. É possível navegar pela interface do espaço de trabalho do AEM Forms usando o teclado.

Para usar a área de trabalho do AEM Forms com um leitor de tela, lembre-se dos seguintes pontos:

* A área de trabalho do AEM Forms é um aplicativo HTML padrão que está em conformidade com qualquer ferramenta padrão de leitor de tela. Não é necessário nenhum script específico para executar uma ferramenta de leitor de tela.
* Toda a navegação na área de trabalho do AEM Forms é feita por meio de tags de âncora, que podem ser facilmente acessadas por meio de guias.
* Os formulários podem levar alguns segundos para serem carregados. O leitor de tela não informa de forma audível que o formulário está sendo carregado e que você deve aguardar.

## Navegar no espaço de trabalho do AEM Forms usando um teclado {#navigating-html-workspace-using-a-keyboard}

Quando você navega na área de trabalho do AEM Forms usando um teclado, a navegação está em conformidade com as convenções de acessibilidade HTML. Em determinadas situações, a ordem de tabulação não segue a ordem convencional típica. As dicas a seguir ajudam a navegar na interface:

* Se tiver problemas ao sair das barras de ferramentas na parte superior do navegador, pressione Ctrl+Tab para acessar o conteúdo da janela do navegador.
* A Ajuda da área de trabalho do AEM Forms é aberta em uma janela separada do navegador. Depois de visualização na Ajuda, o foco retorna à janela do navegador que contém a área de trabalho do AEM Forms. O menu Ajuda permanece focado quando o foco retorna.
* Ao abrir um formulário para start de um processo ou concluir uma tarefa, o foco permanece com o elemento existente e não é alterado para o formulário. Use a guia para mover o foco para o formulário e navegar por ele. A ordem de tabulação no formulário depende do tipo e do design do formulário.

   Para formulários PDF, quando você navega até o final do formulário ou envia o formulário, o foco do cursor vai para a barra Endereço do navegador. É necessário percorrer os menus novamente (mas não o formulário inteiro) para acessar os botões de ação do formulário, como Salvar como rascunho e Concluído. Se o formulário ainda estiver aberto, você também poderá percorrer os botões e voltar ao formulário.

## Gerenciamento de preferências {#managing-preferences}

Você pode definir as várias preferências de espaço de trabalho do AEM Forms nas seguintes categorias:

**Fora do escritório:** Defina as preferências para controlar como as tarefas são atribuídas a outras pessoas enquanto você estiver fora do escritório. Consulte [Configuração de preferências](/help/forms/using/todo-lists.md#main-pars-heading-22)fora do escritório.

**Filas:** Defina preferências para compartilhar sua lista de tarefas com outros usuários ou para solicitar acesso à lista de outro usuário. Consulte [Trabalhar com tarefas de filas](/help/forms/using/todo-lists.md#main-pars-heading-19)de grupo e compartilhadas.

**Configurações da interface do usuário:** Defina as preferências para como você interage com a área de trabalho do AEM Forms. Consulte [Definir preferências](/help/forms/using/getting-started-livecycle-html-workspace.md#main-pars-heading-5)da interface do usuário.

### Definir preferências da interface do usuário {#set-user-interface-preferences}

Defina as preferências da interface do usuário na guia Preferências > Configurações da interface do usuário. As preferências a seguir estão disponíveis.

* **Localização do Start:** Especifica a página que aparece quando você faz logon na área de trabalho do AEM Forms. As quatro opções disponíveis são Processo de Start, Fazer, Rastreamento e Favoritos.
* **Aviso de logout:** Especifica se você será solicitado a confirmar que deseja fazer logout depois de clicar em Logout.
* **Formato de data:** Especifica o formato de exibição de data usado na área de trabalho do AEM Forms.
* **Formato** de hora: Especifica o formato de exibição de tempo usado na área de trabalho do AEM Forms.
* **Notificar Eventos de Tarefa por email:** Especifica se você recebe notificações por e-mail para eventos de tarefa, incluindo atribuições de tarefa, lembretes e prazos para tarefas na lista de Tarefas Pendentes e nas listas de Tarefas Pendentes a que pertence.
* **Anexar formulários no email:** Especifica se uma cópia do formulário está anexada às mensagens de notificação por email. Anexos são suportados apenas para formulários PDF e XDP.
* **Salve o rascunho periodicamente:** Especifica se os rascunhos de formulário são salvos automaticamente periodicamente ou não. Para salvar seus rascunhos periodicamente, ative essa opção e defina a duração do salvamento automático de 1 a 30 minutos. Quando o salvamento automático é ativado e um usuário está trabalhando em um rascunho, o rascunho é salvo periodicamente após o número especificado de minutos. O rascunho é salvo automaticamente somente quando há uma alteração no rascunho desde a última gravação ou salvamento automático. Quando o rascunho for salvo, uma mensagem de alerta será exibida na tela.
