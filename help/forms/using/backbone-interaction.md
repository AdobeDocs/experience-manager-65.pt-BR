---
title: Interação da coluna vertebral
seo-title: Interação da coluna vertebral
description: Informações conceituais sobre o uso de modelos JavaScript Backbone na área de trabalho do AEM Forms.
seo-description: Informações conceituais sobre o uso de modelos JavaScript Backbone na área de trabalho do AEM Forms.
uuid: 040f42cb-3b76-4657-ba05-9e52647efb12
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 538591fe-29e4-40c4-a045-06095cc0c6b8
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Interação da coluna vertebral{#backbone-interaction}

Backbone é uma biblioteca que ajuda a criar e seguir a arquitetura MVC em aplicativos da Web. A ideia básica do Backbone é organizar sua interface em visualizações lógicas, apoiadas por modelos, cada um dos quais pode ser atualizado independentemente quando o modelo é alterado, sem precisar redesenhar a página. Para obter mais informações sobre o Backbone, consulte [https://backbonejs.org](https://backbonejs.org/).

Alguns conceitos-chave são os seguintes:

**Modelo** Backbone Contém dados e a maior parte da lógica relacionada a esses dados.

**visualização** Backbone Usada para representar o estado do modelo correspondente. Uma visualização de backbone na verdade se comporta como um controlador, ouvindo eventos de interface do usuário como cliques do usuário ou eventos de modelo (como dados alterados) e modifica a interface do usuário conforme apropriado.

**Modelo** HTML Um modelo de invólucro que tem espaços reservados preenchidos pelo modelo.

**Área de trabalho** do AEM Forms Contém vários componentes individuais. Cada componente:

* Representa um único elemento lógico da interface do usuário.
* Pode ser uma coleção de componentes semelhantes.
* Composto por modelo Backbone, visualização Backbone e modelo HTML.
* Contém referência a um serviço.
* Contém referência aos utilitários necessários.

Quando um componente é inicializado, os seguintes objetos são criados:

* Uma nova instância do modelo Backbone para o componente é criada. O serviço é inserido no modelo.
* Uma nova instância da visualização Backbone é criada.
* A instância do modelo correspondente, modelo HTML e Utilitários são inseridos na visualização.

Na visualização de backbone, há um mapa de eventos que mapeia os vários eventos que podem surgir devido às interações da interface do usuário com um manipulador correspondente. Esse mapeamento é iniciado assim que um componente é inicializado.

Quando uma visualização é inicializada, a visualização chama seu modelo correspondente para buscar dados do servidor. Quando todos os dados exigidos por uma visualização estiverem disponíveis, a visualização renderizará os dados no formato especificado pelo modelo HTML. Várias visualizações podem compartilhar o mesmo modelo para comunicação.

![](do-not-localize/aem_forms_workflow.png)

Um exemplo:

1. O usuário clica em um modelo de tarefa na lista de tarefa.
1. A visualização de Tarefa escuta o clique e chama a função de renderização no modelo de tarefa.
1. Posteriormente, o modelo de Tarefa chama o serviço, que é um ponto comum para todas as comunicações com o servidor de formulários AEM.
1. A classe de serviço chama o terminal REST do AEM Forms para método de renderização via ajax.
1. O retorno de sucesso para esta invocação Ajax é definido no modelo de tarefa.
1. O modelo de Tarefa gera um evento de backbone como uma notificação de conclusão da chamada de renderização.
1. Outra visualização, a visualização de detalhes da tarefa escuta esse evento do modelo de tarefa.
1. A visualização de detalhes da Tarefa altera o modelo de detalhes da tarefa para exibir a tarefa renderizada (formulário, detalhes, anexos, observações e assim por diante) para o usuário.
