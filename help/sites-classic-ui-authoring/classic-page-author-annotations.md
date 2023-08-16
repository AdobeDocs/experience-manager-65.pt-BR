---
title: Anotações ao editar uma página
description: Adicionar conteúdo às páginas do seu site geralmente está sujeito a discussões antes de realmente ser publicado. Para auxiliar nisso, muitos componentes diretamente relacionados ao conteúdo permitem adicionar uma anotação.
page-status-flag: de-activated
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: d60e9601-d15b-4378-a33e-e90961f63195
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 8%

---

# Anotações ao editar uma página{#annotations-when-editing-a-page}

Adicionar conteúdo às páginas do seu site geralmente está sujeito a discussões antes de realmente ser publicado. Para auxiliar nisso, muitos componentes diretamente relacionados ao conteúdo (em vez de, por exemplo, para layout) permitem adicionar uma anotação.

Uma anotação coloca um marcador colorido/nota adesiva na página. A anotação permite a você (ou outros usuários) deixar comentários e/ou perguntas para outros autores/revisores.

>[!NOTE]
>
>A definição de um tipo de componente individual determina se é possível adicionar uma anotação (ou não) nas instâncias desse componente.

>[!NOTE]
>
>As anotações criadas na interface clássica também serão exibidas na interface otimizada para toque. No entanto, os rascunhos são específicos da interface do usuário e são mostrados somente na interface do usuário em que foram criados.

>[!CAUTION]
>
>A exclusão de um recurso (por exemplo, parágrafo) exclui todas as anotações e rascunhos associados a ele, independentemente de sua posição na página como um todo.

>[!NOTE]
>
>Dependendo dos seus requisitos, também é possível desenvolver um fluxo de trabalho para enviar notificações quando anotações são adicionadas, atualizadas ou excluídas.

## Anotações {#annotations}

Dependendo do design do parágrafo, a anotação está disponível como uma opção no menu de contexto (geralmente o botão direito do mouse sobre o parágrafo necessário) ou como um botão na barra de edição de parágrafo.

Em ambos os casos, selecione **Anotar**. Uma anotação colorida com nota adesiva é aplicada ao parágrafo. Você fica imediatamente no modo Editar, o que permite adicionar texto diretamente:

![chlimage_1-137](assets/chlimage_1-137.png)

Você pode mover a anotação para uma nova posição na página. Clique na área da borda superior, mantenha pressionada e arraste simultaneamente a anotação para a nova posição. Pode ser em qualquer lugar da página, embora geralmente seja importante mantê-lo conectado ao parágrafo de alguma forma.

As anotações (incluindo rascunhos relacionados) também são incluídas em qualquer ação de cópia, recorte ou exclusão realizada no parágrafo ao qual estão anexadas. Para ações de cópia ou recorte, a posição da anotação (e rascunhos relacionados) mantém sua posição em relação ao parágrafo de origem.

O tamanho da anotação também pode ser aumentado ou diminuído arrastando o canto inferior direito.

Para fins de rastreamento, a linha de rodapé indica o usuário que criou a anotação e a data. Os autores subsequentes podem editar a mesma anotação (o rodapé é atualizado) ou criar outra anotação para o mesmo parágrafo.

A confirmação é solicitada ao selecionar a exclusão da anotação (a exclusão de uma anotação também exclui os rascunhos anexados a essa anotação).

Os três ícones na parte superior esquerda permitem minimizar a anotação (juntamente com qualquer rascunho relacionado), alterar a cor e adicionar rascunhos.

>[!NOTE]
>
>As anotações só são visíveis no modo Editar do ambiente de criação.
>
>Eles não estão visíveis em um ambiente de publicação, nem nos modos de Visualização ou Design disponíveis em um ambiente de autor.

>[!NOTE]
>
>As anotações não podem ser adicionadas a uma página que foi bloqueada por outro usuário.

## Rascunhos de anotações {#annotation-sketches}

>[!NOTE]
>
>Os rascunhos não estão disponíveis no Internet Explorer, portanto:
>
>* o ícone não é exibido.
>* rascunhos existentes, criados em outro navegador, não serão exibidos.
>

Os rascunhos são um recurso de anotações que permitem criar gráficos de linha simples em qualquer lugar da janela do navegador (parte visível):

![chlimage_1-138](assets/chlimage_1-138.png)

* O cursor se transforma em um fio cruzado quando você está no modo de rascunho. Você pode desenhar várias linhas distintas.
* A linha de rascunho reflete a cor da anotação e pode ser:

   * à mão livre

     o modo padrão; termine soltando o botão do mouse.

   * reta:

     mantenha pressionada `ALT` e clique nos pontos inicial e final; conclua com um clique duplo.

* Depois de sair do modo de rascunho, você pode clicar em uma linha de rascunho para selecioná-lo.
* Mover um rascunho selecionando-o e arrastando-o para a posição desejada.
* Um rascunho sobrepõe o conteúdo. Isso significa que dentro dos quatro cantos do rascunho, não é possível clicar no parágrafo subjacente. Por exemplo, se você precisar editar ou acessar um link. Se isso se tornar um problema (por exemplo, se você tiver um rascunho que cubra uma grande área da página), minimize a anotação apropriada, pois isso também minimizará todos os rascunhos relacionados, dando acesso à área subjacente.
* Para excluir um rascunho individual - selecione o rascunho necessário e pressione a tecla **Excluir** chave (**fn**-**backspace** em um Mac).

* Se você mover ou copiar um parágrafo, todas as anotações relacionadas e seus rascunhos também serão movidos ou copiados; sua posição em relação ao parágrafo permanecerá a mesma.
* Se você excluir uma anotação, todos os rascunhos anexados a essa anotação também serão excluídos.
