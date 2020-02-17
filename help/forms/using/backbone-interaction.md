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
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# Interação da coluna vertebral{#backbone-interaction}

Backbone é uma biblioteca que ajuda a criar e seguir a arquitetura MVC em aplicativos da Web. A ideia básica do Backbone é organizar sua interface em exibições lógicas, apoiadas por modelos, que podem ser atualizados independentemente quando o modelo é alterado, sem precisar redesenhar a página. Para obter mais informações sobre Backbone, consulte [https://backbonejs.org](https://backbonejs.org/).

Alguns conceitos-chave são os seguintes:

**Modelo** Backbone Contém dados e a maior parte da lógica relacionada a esses dados.

**Exibição** de backbone usada para representar o estado do modelo correspondente. Uma visualização de backbone na verdade se comporta como um controlador, ouvindo eventos de interface do usuário, como cliques do usuário, ou eventos de modelo (como dados alterados), e modifica a interface do usuário conforme apropriado.

**Modelo** HTML Um modelo de invólucro que tem espaços reservados preenchidos pelo modelo.

**A área de trabalho** do AEM Forms contém vários componentes individuais. Cada componente:

* Representa um único elemento lógico da interface do usuário.
* Pode ser uma coleção de componentes semelhantes.
* Composto por modelo Backbone, visualização Backbone e modelo HTML.
* Contém referência a um serviço.
* Contém referência aos utilitários necessários.

Quando um componente é inicializado, os seguintes objetos são criados:

* Uma nova instância do modelo Backbone para o componente é criada. O serviço é inserido no modelo.
* Uma nova instância da exibição Backbone é criada.
* A instância do modelo correspondente, modelo HTML e Utilitários são inseridos na exibição.

Na exibição Backbone, há um mapa de eventos que mapeia os vários eventos que podem surgir devido às interações da interface do usuário com um manipulador correspondente. Esse mapeamento é iniciado assim que um componente é inicializado.

Quando uma exibição é inicializada, a exibição chama seu modelo correspondente para buscar dados do servidor. Quando todos os dados exigidos por uma exibição estiverem disponíveis, a exibição renderizará os dados no formato especificado pelo modelo HTML. Várias exibições podem compartilhar o mesmo modelo para comunicação.

![](do-not-localize/aem_forms_workflow.png)

Um exemplo:

1. O usuário clica em um modelo de tarefa na lista de tarefas.
1. A exibição de tarefa escuta o clique e chama a função de renderização no modelo de tarefa.
1. Posteriormente, o modelo de tarefa chama o serviço, que é um ponto comum para todas as comunicações com o servidor de formulários AEM.
1. A classe de serviço chama o terminal REST do AEM Forms para método de renderização via ajax.
1. O retorno de sucesso para esta invocação Ajax é definido no modelo de tarefa.
1. O modelo de tarefa gera um evento de backbone como uma notificação de conclusão da chamada de renderização.
1. Outra exibição, a exibição de detalhes da tarefa escuta esse evento do modelo de tarefa.
1. A exibição de detalhes da tarefa altera o modelo de detalhes da tarefa para exibir a tarefa renderizada (formulário, detalhes, anexos, observações e assim por diante) para o usuário.

[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)
