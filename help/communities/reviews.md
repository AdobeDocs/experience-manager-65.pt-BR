---
title: Uso do Resumo de análises e análises (exibir)
description: Saiba como adicionar os componentes de Resumo das revisões e análises a uma página.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 170414a6-c40b-4ad2-9294-7c2266850c3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---

# Uso do Resumo de análises e análises (exibir) {#using-reviews-and-reviews-summary-display}

O componente `Reviews` é composto de [Comentários](comments.md) e [Classificação](rating.md) componentes prontos para uso.

O componente `Reviews Summary (Display)` fornece um resumo de uma instância ativa ou fechada de um componente `Reviews` para exibição em outro lugar no site.

>[!NOTE]
>
>Não há suporte para postagem anônima de uma revisão. Os visitantes do site devem se registrar (tornar-se membros) e fazer logon para participar. O visitante conectado pode atualizar sua revisão a qualquer momento.

## Adicionando uma Revisão a uma Página {#adding-a-review-to-a-page}

Para adicionar um componente `Reviews` a uma página no modo de autor, use o navegador de componentes para localizar `Communities / Reviews` e arrastá-lo para o local em uma página, como uma posição relativa ao recurso para os usuários revisarem.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](reviews-basics.md#essentials-for-client-side) são incluídas, é assim que o componente `Reviews` aparece.

![criar-revisão](assets/create-review.png)

## Configurar análises {#configuring-reviews}

Selecione o componente `Reviews` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

Na guia **[!UICONTROL Classificações permitidas]**, especifique a lista completa de classificações a serem exibidas para os membros. A primeira classificação deve ser geral/geral, pois é a classificação que fornece a classificação média para o componente `Review Summary (Display)`. As próximas duas classificações na configuração padrão devem receber um título diferente, diferente de &quot;Subclassificação 1&quot; ou &quot;Subclassificação 2&quot;.

![classificação-permitida](assets/configure-review1.png)

* **[!UICONTROL Classificações permitidas]**

  Uma lista de classificações que um membro pode escolher.

  Use os botões seta para cima, seta para baixo e excluir para modificar as seleções visíveis.

  Clique em **[!UICONTROL Adicionar Item]** para adicionar outra opção de classificação.

Na guia **[!UICONTROL Classificações necessárias]**, insira novamente os itens da lista de **[!UICONTROL Classificações permitidas]** que são necessários para classificação. Se um item for especificado somente na guia Classificações Permitidas, ele poderá ser deixado desmarcado quando for enviado pelo membro.

No site, as classificações necessárias são marcadas com um asterisco. Se um item for obrigatório e deixado desmarcado, uma mensagem será exibida para o membro e o envio será negado até que todas as classificações necessárias sejam marcadas.

![classificação-necessária](assets/configure-review2.png)

* **[!UICONTROL Classificações necessárias]**

  Um subconjunto de classificações permitidas, indicando quais classificações são necessárias.

  Use os botões seta para cima, seta para baixo e excluir para modificar as seleções visíveis.

  Clique em **[!UICONTROL Adicionar Item]** para adicionar outra opção de resposta.

>[!NOTE]
>
>Se um item for inserido na guia **[!UICONTROL Classificações Necessárias]** não especificada na guia **[!UICONTROL Classificações Permitidas]**, ele não será incluído nos itens a serem classificados.

Na guia **[!UICONTROL Revisões]**, especifique como as revisões são tratadas.

![avaliações](assets/configure-review3.png)

* **[!UICONTROL Permitir respostas]**

  Se marcado, permitir respostas para revisões. O padrão está desmarcado.

* **[!UICONTROL Fechado]**

  Se marcada, a revisão será fechada para novas revisões e respostas. O padrão está desmarcado.

* **[!UICONTROL Permitir Carregamentos de Arquivos]**

  Se marcado, permite que os anexos de arquivo sejam carregados para revisão. O padrão está desmarcado.

* **Tamanho máx. do arquivo**

  Relevante somente se **[!UICONTROL Permitir carregamentos de arquivos]** estiver marcado. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 10 MB.

* **[!UICONTROL Comprimento Máximo da Mensagem]**

  Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4.096 caracteres.

* **[!UICONTROL Tipos de arquivos permitidos]**

  Relevante somente se **[!UICONTROL Permitir carregamentos de arquivos]** estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **[!UICONTROL Editor de Rich Text]**

  Se marcados, os posts podem ser inseridos com marcação. O padrão está desmarcado.

* **[!UICONTROL Permitir votação]**

  Se marcado, inclui o recurso Votação de um tópico. O padrão está desmarcado.

Na guia **[!UICONTROL Moderação de usuário]**, especifique como os comentários publicados são gerenciados. Para obter mais informações, consulte [Moderando conteúdo gerado por usuário](moderate-ugc.md).

![moderação-usuário](assets/configure-review4.png)

* **[!UICONTROL Pré-moderação]**

  Se marcadas, as revisões devem ser aprovadas antes de serem exibidas em um site de publicação. O padrão está desmarcado.

* **[!UICONTROL Excluir análises]**

  Se marcado, o membro que postou a revisão poderá excluí-lo. O padrão está desmarcado.

* **[!UICONTROL Negar análises]**

  Se marcado, permitir que os moderadores neguem comentários. O padrão está desmarcado.

* **[!UICONTROL Fechar/Reabrir análises]**

  Se marcado, permite que os moderadores fechem e reabram os comentários. O padrão está desmarcado.

* **[!UICONTROL Sinalizar análises]**

  Se marcado, permite que os membros sinalizem revisões como inapropriadas. O padrão está desmarcado.

* **[!UICONTROL Lista de motivos da sinalização]**

  Se marcado, permitirá que os membros escolham, em uma lista suspensa, seu motivo para sinalizar uma revisão como inapropriado. O padrão está desmarcado.

* **[!UICONTROL Motivo personalizado do sinalizador]**

  Se marcado, permite que os membros insiram seu próprio motivo para sinalizar uma revisão como inapropriada. O padrão está desmarcado.

* **[!UICONTROL Limite de moderação]**

  Insira o número de vezes que uma revisão deve ser marcada por membros antes que os moderadores sejam notificados. O padrão é uma vez (1).

* **[!UICONTROL Limite de Sinalização]**

  Insira o número de vezes que uma revisão deve ser sinalizada antes de ser ocultada da visualização pública. Este número deve ser maior ou igual ao **[!UICONTROL Limite de moderação]**. O padrão é 5.

### Adicionar um resumo de revisão (exibir) a uma página {#adding-a-review-summary-display-to-a-page}

Para adicionar um componente `Reviews Summary (Display)` a uma página no modo de autor, localize o componente

* `Communities / Reviews Summary (Display)`

E arraste-o para o local em uma página onde um resumo de uma revisão ativa ou fechada deve ser exibido.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](reviews-basics.md#essentials-for-client-side) são incluídas, é assim que o `Reviews Summary (Display)`componente é exibido.

![resumo da revisão](assets/configure-review5.png)

>[!NOTE]
>
>A &quot;Média&quot; reflete os votos para o primeiro item listado nas guias de Classificações permitidas da revisão que está sendo resumida.

### Resumo das análises de configuração (exibir) {#configuring-reviews-summary-display}

Selecione o componente `Reviews Summary (Display)` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

Na guia **[!UICONTROL Resumo da Revisão]**

![resumo da revisão](assets/configure-review6.png)

* `Review Path`

  Insira ou navegue até a instância colocada do componente `reviews` para que você possa resumir. Por exemplo, se adicionado à Página da Web do [site do Geometrixx](getting-started.md), o caminho será:

  `/content/sites/engage/en/page/jcr:content/content/primary/reviews`

* `Include histogram`

  Se marcado, incluirá a exibição de um gráfico de barras indicando quantas classificações de estrelas há nas revisões sendo resumidas. O padrão está desmarcado.

### Alterar para um tipo de revisão personalizada {#changing-to-a-custom-review-type}

O componente de Revisões usa o Sistema de comentários.

Ao alterar o Tipo de recurso de comentário, o sistema de comentário não gera mais uma instância de um comentário usando o padrão, mas sim uma que foi personalizada (estendida) pelos desenvolvedores.

Quando os tipos de recursos personalizados forem conhecidos, entre no [Modo de Design](../../help/sites-authoring/default-components-designmode.md) e clique duas vezes no componente `Comments` inserido para abrir uma caixa de diálogo com uma guia adicional.

Na guia **[!UICONTROL Tipos de Recursos]**, especifique o resourceType personalizado para novas instâncias dos componentes `Comments or Voting`:

![comentários-votação](assets/configure-review7.png)

* **[!UICONTROL Tipo de recurso de comentário]**

  Navegue até o resourceType de um componente `comment` estendido (comentário único) em /apps. Por exemplo, `/apps/social/commons/components/hbs/comments/comment`.

  Esse recurso identifica o resourceType do UGC criado quando um visitante publica um comentário.

* **[!UICONTROL Tipo de recursos de votação]**

  Navegue até o resourceType de um componente `voting` estendido em /apps. Por exemplo, `/apps/social/components/hbs/voting`.

  Esse recurso identifica o tipo de recurso do UGC criado quando um visitante publica um voto.

* **[!UICONTROL Tipo de recursos de comentários do sistema]**

  Navegue até o resourceType de um componente `comments` estendido (Sistema de comentários) em /apps. Deixe em branco a menos que o modelo de página [inclua dinamicamente](scf.md#add-or-include-a-communities-component) o Sistema de comentários no script subjacente em vez de ser adicionado à página como um recurso (nó de comentários). Saiba mais lendo sobre o [`{{include}}` auxiliar](handlebars-helpers.md#include).

## Experiência de visitante do site {#site-visitor-experience}

### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou a revisão.

### Membros {#members}

Quando o visitante do site está conectado, dependendo da configuração, ele pode:

* Post uma nova revisão
* Editar sua própria revisão
* Excluir sua própria revisão
* Sinalizar comentários de outras pessoas

Só é permitida uma classificação por membro. O membro pode alterar a sua classificação a qualquer momento.

### Anônimo {#anonymous}

Os visitantes do site que não estão conectados podem ler somente os comentários publicados, traduzi-los se houver suporte, mas não podem adicionar uma classificação ou uma revisão, nem sinalizar os comentários de revisão de outras pessoas.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Review Essentials](reviews-basics.md) para desenvolvedores.

Para obter a moderação dos comentários publicados, consulte [Moderando Conteúdo Gerado por Usuário](moderate-ugc.md).

Para tradução de comentários publicados, consulte [Tradução de Conteúdo Gerado pelo Usuário](translate-ugc.md).
