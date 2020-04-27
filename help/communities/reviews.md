---
title: Usando o Resumo de Revisões e Revisões (Exibição)
seo-title: Usando o Resumo de Revisões e Revisões (Exibição)
description: Adicionar os componentes Resumo de revisões e revisões a uma página
seo-description: Adicionar os componentes Resumo de revisões e revisões a uma página
uuid: bd1ccee7-b26b-4a27-b1ea-89609f5080af
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: bf4e7809-8def-4647-aaa6-3ac36865511f
translation-type: tm+mt
source-git-commit: 62f2a11491e427a13cecae75c225ed41a44783cd

---


# Usando o Resumo de Revisões e Revisões (Exibição) {#using-reviews-and-reviews-summary-display}

O `Reviews` componente é um composto de componentes [Comentários](comments.md) e [Classificação](rating.md) prontos para uso.

O `Reviews Summary (Display)` componente fornece um resumo de uma instância ativa ou fechada de um `Reviews` componente para exibição em outro lugar do site.

>[!NOTE]
>
>Não há suporte para a publicação anônima de uma revisão. Os visitantes do site devem se registrar (tornar-se um membro) e fazer logon para participar. O visitante conectado pode atualizar sua revisão a qualquer momento.


## Adding a Review to a Page {#adding-a-review-to-a-page}

Para adicionar um `Reviews` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / Reviews` e arrastá-lo para o local em uma página, como uma posição relativa ao recurso que os usuários devem revisar.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](reviews-basics.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Reviews`componente será exibido.

![chlimage_1-340](assets/chlimage_1-340.png)

## Configuração de revisões {#configuring-reviews}

Selecione o componente inserido a ser acessado e selecione o `Reviews` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-341](assets/chlimage_1-341.png)

Na guia Classificações **** permitidas, especifique a lista completa de classificações a serem exibidas aos membros. A primeira notação deve ser global/geral, dado que é a notação que fornece a notação média para o `Review Summary (Display)` componente. As próximas duas classificações na configuração padrão devem receber um título diferente de &quot;Subrating 1&quot; ou &quot;Subrating 2&quot;.

![chlimage_1-342](assets/chlimage_1-342.png)

* **[!UICONTROL Classificações permitidas]**

   Uma lista de classificações da qual um membro pode escolher.

   Use a seta para cima, a seta para baixo e os botões para excluir para modificar as seleções visíveis.

   Clique em **[!UICONTROL Adicionar item]** para adicionar outra opção de classificação.

Na guia Classificações **** obrigatórias, digite novamente os itens da lista de Classificações **** permitidas que precisam ser classificados. Se um item for especificado apenas na guia Classificações permitidas, ele poderá ficar desmarcado quando submetido pelo membro.

No site, as classificações necessárias são marcadas com um asterisco. Se um item for obrigatório e não estiver marcado, uma mensagem será exibida para o membro e o envio será negado até que todas as classificações necessárias sejam marcadas.

![chlimage_1-343](assets/chlimage_1-343.png)

* **[!UICONTROL Classificações necessárias]**

   Um subconjunto de classificações permitidas, indicando quais classificações são necessárias.

   Use a seta para cima, a seta para baixo e os botões para excluir para modificar as seleções visíveis.

   Clique em **[!UICONTROL Adicionar item]** para adicionar outra opção de resposta.

>[!NOTE]
>
>Se um item for inserido na guia Classificações **** obrigatórias que não esteja especificada na guia Classificações **** permitidas, então ele não será incluído nos itens para classificar.


Na guia **[!UICONTROL Revisões]** , especifique como as revisões serão tratadas.

![chlimage_1-344](assets/chlimage_1-344.png)

* **[!UICONTROL Permitir respostas]**

   Se marcada, permita respostas a revisões. O padrão está desmarcado.

* **[!UICONTROL Fechado]**

   Se marcada, a revisão é fechada para novas revisões e respostas. O padrão está desmarcado.

* **[!UICONTROL Permitir carregamento de arquivos]**

   Se marcada, permita que os anexos de arquivo sejam carregados para a revisão. O padrão está desmarcado.

* **Tamanho máximo do arquivo **

   Relevante somente se a opção **[!UICONTROL Permitir uploads]** de arquivo estiver marcada. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 10 MB.

* **[!UICONTROL Comprimento máximo da mensagem de]**

   Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4096 caracteres.

* **[!UICONTROL Tipos de arquivos permitidos]**

   Relevante somente se a opção **[!UICONTROL Permitir uploads]** de arquivo estiver marcada. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **[!UICONTROL Editor de Rich Text]**

   Se marcada, as publicações podem ser inseridas com marcação. O padrão está desmarcado.

* **[!UICONTROL Permitir votação]**

   Se marcada, inclua o recurso Voto para um tópico. O padrão está desmarcado.

Na guia Moderação **[!UICONTROL do]** usuário, especifique como as revisões publicadas serão gerenciadas. Para obter mais informações, consulte [Moderação de conteúdo](moderate-ugc.md)gerado pelo usuário.

![chlimage_1-345](assets/chlimage_1-345.png)

* **[!UICONTROL Pré-moderação]**

   Se marcadas, as revisões devem ser aprovadas antes de serem exibidas em um site de publicação. O padrão está desmarcado.

* **[!UICONTROL Excluir análises]**

   Se marcada, o membro que postou a revisão terá a capacidade de excluí-la. O padrão está desmarcado.

* **[!UICONTROL Negar análises]**

   Se marcada, permita que os moderadores neguem revisões. O padrão está desmarcado.

* **[!UICONTROL Fechar/reabrir análises]**

   Se marcada, permita que os moderadores fechem e reabram as revisões. O padrão está desmarcado.

* **[!UICONTROL Sinalizar análises]**

   Se marcada, permita que os membros sinalizem revisões como inadequadas. O padrão está desmarcado.

* **[!UICONTROL Sinalizar lista de motivo]**

   Se marcada, permita que os membros escolham, em uma lista suspensa, seu motivo para marcar uma revisão como inadequada. O padrão está desmarcado.

* **[!UICONTROL Motivo personalizado de sinalização]**

   Se marcada, permita que os membros insiram seu próprio motivo para marcar uma revisão como inadequada. O padrão está desmarcado.

* **[!UICONTROL Limite de moderação]**

   Insira o número de vezes que uma revisão deve ser sinalizada pelos membros antes que os moderadores sejam notificados. O padrão é uma vez (1).

* **[!UICONTROL Limite de sinalização]**

   Insira o número de vezes que uma revisão deve ser sinalizada antes de ser ocultada da visualização pública. Esse número deve ser maior ou igual ao Limite de **[!UICONTROL moderação]**. O padrão é 5.

### Adicionar um resumo de revisão (exibição) a uma página {#adding-a-review-summary-display-to-a-page}

Para adicionar um `Reviews Summary (Display)` componente a uma página no modo de autor, localize o componente

* `Communities / Reviews Summary (Display)`

e arraste-o para o lugar em uma página onde um resumo de uma revisão ativa ou fechada deve ser exibido.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](basics.md).

Quando as bibliotecas [do lado do cliente](reviews-basics.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Reviews Summary (Display)`componente será exibido.

![chlimage_1-346](assets/chlimage_1-346.png)

>[!NOTE]
>
>A &quot;Média&quot; reflete os votos do primeiro item listado nas guias Classificações Permitidas da revisão que está sendo resumida.


### Configuração do Resumo das Revisões (Exibição) {#configuring-reviews-summary-display}

Selecione o componente inserido a ser acessado e selecione o `Reviews Summary (Display)` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-347](assets/chlimage_1-347.png)

Na guia **[!UICONTROL Revisar resumo]**

![chlimage_1-348](assets/chlimage_1-348.png)

* `Review Path`

   digite ou navegue até a instância colocada do `reviews`componente para resumir, por exemplo, se adicionada à Página da Web do site de envolvimento do [Geometrixx,](getting-started.md) o caminho seria:

   `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

   Se marcada, inclua a exibição de um gráfico de barras indicando quantos de cada classificação de estrela existem nas revisões que estão sendo resumidas. O padrão está desmarcado.

### Alteração para um tipo de revisão personalizada {#changing-to-a-custom-review-type}

O componente Revisões usa o Sistema de comentários.

Ao alterar o Tipo de recurso de comentário, o sistema de comentários não gerará mais uma instância de um comentário usando o padrão, mas uma que foi personalizada (estendida) pelos desenvolvedores.

Depois que os tipos de recursos personalizados forem conhecidos, digite Modo [de](../../help/sites-authoring/default-components-designmode.md) design e clique no duplo no componente colocado `Comments` para abrir uma caixa de diálogo com uma guia adicional.

Na guia Tipos **[!UICONTROL de]** recursos, especifique o resourceType personalizado para novas instâncias dos `Comments or Voting`componentes:

![chlimage_1-349](assets/chlimage_1-349.png)

* **[!UICONTROL Tipo de recursos de comentários]**

   Navegue até resourceType de um `comment`componente estendido (comentário único) em /apps. Por exemplo, `/apps/social/commons/components/hbs/comments/comment`.

   Esse recurso identificará o resourceType do UGC criado quando um visitante postar um comentário.

* **[!UICONTROL Tipo de recursos para pesquisa]**

   Navegue até resourceType de um `voting`componente estendido em /apps. Por exemplo, `/apps/social/components/hbs/voting`.

   Esse recurso identificará o tipo de recurso do UGC criado quando um visitante postar um voto.

* **[!UICONTROL Tipo de recurso do sistema de comentários]**

   Navegue até resourceType de um `comments`componente estendido (Sistema de comentários) em /apps. Deixe em branco, a menos que o modelo de página inclua [](scf.md#add-or-include-a-communities-component) dinamicamente o Sistema de comentários no script subjacente em vez de ser adicionado à página como um recurso (nó de comentários). Saiba mais lendo sobre o auxiliar [](handlebars-helpers.md#include){{include}}.

## Experiência com o Visitante do site {#site-visitor-experience}

### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou a revisão.

### Membros {#members}

Quando o visitante do site estiver conectado, dependendo da configuração, eles poderão

* Publicar uma nova revisão.
* Edite sua própria revisão.
* Exclua sua própria revisão.
* Sinalize os comentários de revisão de outras pessoas.

Somente uma classificação por membro é permitida. O membro pode alterar a sua notação a qualquer momento.

### Anônimo {#anonymous}

Os visitantes do site que não estão conectados só podem ler revisões publicadas, traduzi-las se suportadas, mas não podem adicionar uma classificação ou uma revisão, nem sinalizar comentários de revisão de outras pessoas.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Revisar essenciais](reviews-basics.md) para desenvolvedores.

Para moderação de comentários publicados, consulte [Moderação de conteúdo](moderate-ugc.md)gerado pelo usuário.

Para obter a tradução de comentários publicados, consulte [Traduzindo conteúdo](translate-ugc.md)gerado pelo usuário.
