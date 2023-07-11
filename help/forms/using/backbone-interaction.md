---
title: Interação backbone
seo-title: Backbone interaction
description: Informações conceituais sobre o uso de modelos de JavaScript do Backbone no espaço de trabalho do AEM Forms.
seo-description: Conceptual information about use of Backbone JavaScript models in AEM Forms workspace.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
exl-id: 8fd9770b-6ec4-4b09-b6b2-47a5e5d40f79
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# Interação backbone{#backbone-interaction}

O Backbone é uma biblioteca que ajuda a criar e a seguir a arquitetura MVC em aplicações Web. A ideia básica do Backbone é organizar sua interface em visualizações lógicas, apoiadas por modelos, cada um dos quais pode ser atualizado independentemente quando o modelo muda, sem precisar redesenhar a página. Para obter mais informações sobre o Backbone, consulte [https://backbonejs.org](https://backbonejs.org/).

Alguns conceitos principais são os seguintes:

**Modelo de backbone** Contém dados e a maior parte da lógica relacionada a esses dados.

**Modo de exibição de backbone** Usado para representar o estado do modelo correspondente. Uma exibição de backbone se comporta realmente como um controlador, ouvindo eventos da interface do usuário como cliques do usuário ou eventos de modelo (como dados alterados) e modifica a interface do usuário conforme apropriado.

**modelo HTML** Um modelo de invólucro que tem espaços reservados preenchidos pelo modelo.

**Workspace do AEM Forms** Contém vários componentes individuais. Cada componente:

* Representa um único elemento da interface de usuário lógico.
* Pode ser uma coleção de componentes semelhantes.
* Composto pelo modelo Backbone, visualização Backbone e modelo HTML.
* Contém referência a um serviço.
* Contém referência aos utilitários necessários.

Quando um componente é inicializado, os seguintes objetos são criados:

* Uma nova instância do modelo de Backbone para o componente é criada. Serviço inserido no modelo.
* Uma nova instância da exibição de Backbone é criada.
* Instância do modelo correspondente, modelo de HTML e Utilitários são inseridos na visualização.

Na visualização Backbone, há um mapa de eventos que mapeia os vários eventos que podem surgir devido às interações da interface do usuário com um manipulador correspondente. Este mapeamento é iniciado assim que um componente é inicializado.

Quando uma exibição é inicializada, ela chama seu modelo correspondente para buscar dados do servidor. Quando todos os dados exigidos por uma visualização estão disponíveis, a visualização renderiza os dados no formato especificado pelo modelo de HTML. Várias exibições podem compartilhar o mesmo modelo para comunicação.

![Exibição de backbone de formulários AEM](do-not-localize/aem_forms_workflow.png)

Um exemplo:

1. O usuário clica em um modelo de tarefa na lista de tarefas.
1. A exibição Tarefa escuta o clique e chama a função de renderização no modelo de tarefa.
1. O modelo de tarefa chama o serviço, que é um ponto comum para toda a comunicação com o servidor do AEM Forms.
1. A classe de serviço chama o ponto de extremidade REST do AEM Forms para o método de renderização via ajax.
1. O retorno de chamada bem-sucedido desta invocação do Ajax é definido no template de tarefa.
1. O modelo de tarefa gera um evento de backbone quando uma notificação de chamada de renderização é concluída.
1. Outra exibição, exibição de detalhes da tarefa, escuta esse evento do modelo de tarefa.
1. A exibição de detalhes da tarefa altera o modelo de detalhes da tarefa para exibir a tarefa renderizada (formulário, detalhes, anexos, observações e assim por diante) ao usuário.
