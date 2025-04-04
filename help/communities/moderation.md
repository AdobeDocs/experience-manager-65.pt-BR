---
title: Console de moderação
description: Saiba como administradores e moderadores da comunidade podem usar o console Moderação para acessar todos os UGC para os quais têm permissão de moderação.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 2%

---

# Console de moderação {#moderation-console}

No AEM Communities, a [moderação de conteúdo da comunidade](/help/communities/moderate-ugc.md) em massa é possível nos ambientes do Autor e do Publish, por administradores e moderadores da comunidade (membros confiáveis da comunidade atribuídos como moderadores).

Os administradores e os moderadores da comunidade também podem executar a [moderação no contexto](/help/communities/in-context.md) no ambiente do Publish.

Um recurso de todos os [sites de comunidade](/help/communities/sites-console.md) é um item de menu `Administration` disponível para usuários que entram com privilégios administrativos. O link `Administration` fornece acesso ao console Moderação.

No console Moderação, os administradores e moderadores da comunidade têm acesso a todo o conteúdo gerado pelo usuário (UGC) para o qual têm permissão de moderação. Se permitido moderar vários sites, é possível exibir publicações em todos os sites ou filtrar por sites de comunidades selecionados.

Para obter informações mais detalhadas, visite [Gerenciando usuários e grupos de usuários](/help/communities/users.md).

O console Moderação é compatível com:

* Execução de tarefas de moderação em massa.
* Pesquisando UGC.
* Exibição de detalhes de UGC.
* Exibição dos detalhes do autor de UGC.

Somente quando conectado como administrador ou como membro com ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)` é possível executar tarefas de moderação.

## Acesso ao ambiente do Publish {#publish-environment-access}

O acesso ao console Moderação a partir de um site da comunidade publicado é feito por meio de um link Administração que aparece quando um moderador da comunidade está conectado.

![publishweretail](assets/publishweretail.png)

Ao selecionar o link Administração, o console Moderação é exibido:

![publicação-console-moderação](assets/moderation-console-publish.png)

## Acesso ao ambiente do autor {#author-environment-access}

No ambiente de criação, para acessar o console Moderação

* Na navegação global, selecione **[!UICONTROL Comunidades]** > **[!UICONTROL Moderação]**.

Somente quando conectado como administrador ou como membro com [permissões de moderador](/help/communities/in-context.md#identifyingtrustedmembers) é possível executar tarefas de moderação. O único conteúdo da comunidade exibido é aquele que o membro conectado tem permissão para moderar.

>[!NOTE]
>
>O UGC do ambiente do Publish só estará visível no Autor se o SRP escolhido implementar um armazenamento comum. Por exemplo, por padrão, o armazenamento é JSRP, que não é um armazenamento comum para Autor e Publish. Consulte [Armazenamento do conteúdo da comunidade](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Interface do console da moderação {#moderation-console-ui}

Separando o painel de navegação esquerdo (que aparece no autor, mas não no Publish), a interface do usuário de moderação tem as seguintes áreas principais:

* **[Barra de navegação superior](#top-navigation-bar)**
* **[Barra de ferramentas](#toolbar)**
* **[Área de conteúdo](#content-area)**

### Barra de navegação superior {#top-navigation-bar}

A barra de navegação superior é constante para todos os consoles. Para obter mais informações, consulte [Manuseio básico](/help/sites-authoring/basic-handling.md).

### Barra de ferramentas {#toolbar}

A barra de ferramentas, localizada abaixo da barra de navegação superior, fornece a seguinte opção de alternância no lado esquerdo:

* [Trilho do filtro](/help/communities/moderation.md#filterrail)
abre um painel que permite a escolha de propriedades nas quais filtrar o conteúdo.

A barra de ferramentas, localizada abaixo da barra de navegação superior, fornece a seguinte opção de alternância no lado esquerdo:

![alternaralternaçãoalternância](assets/toggleswitch.png)

[Trilho do filtro](/help/communities/moderation.md#filterrail)
abre um painel ao selecionar Pesquisar, o que permite uma escolha de propriedades nas quais filtrar o conteúdo.

![filterrail](assets/filterrail.png)

### Área de conteúdo {#content-area}

A área de conteúdo contém informações para o UGC publicado:

* UGC publicado
* Nome do membro
* Avatar do membro
* Localização da publicação
* Quando foi publicado
* Número de respostas à postagem
* [Sentimento](/help/communities/moderate-ugc.md#sentiment) associado à publicação
* Se aprovada, uma marca de seleção é exibida
* Se houver um anexo, um clipe de papel será exibido

>[!NOTE]
> 
>A área de conteúdo apresenta uma *rolagem infinita*, o que significa que ela permite continuar a rolagem até que você tenha atingido o fim do conteúdo. A barra de ferramentas permanece em uma posição fixa e visível acima da área de conteúdo, mesmo ao rolar a tela.

### Trilho do filtro {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

O ícone do painel lateral abre o painel de filtros. O painel de filtros, que aparece à esquerda da área de conteúdo, fornece filtros diferentes, cada um com um efeito imediato no UGC referenciado que aparece na área de conteúdo.

Os filtros em cada categoria estão **OR** juntos, e os filtros em categorias diferentes estão **AND** juntos.

Por exemplo, se você marcar **Pergunta** e **Resposta**, verá um conteúdo que é uma **Pergunta** *ou* uma **Resposta**.

No entanto, se você marcar **Pergunta** e **Pendente**, verá apenas conteúdo que é uma **Pergunta** e que está **Pendente**.

>[!NOTE]
>
>Os moderadores da comunidade podem marcar os filtros predefinidos na interface do usuário do console de moderação. À medida que esses filtros são anexados ao final do URL (como parâmetros de sequência de consulta), os moderadores podem voltar posteriormente aos filtros marcados e também compartilhar esses links.

![ícone de pesquisa](assets/searchicon.png)

Quando o painel de filtros está aberto, o ícone Pesquisar alterna para o painel lateral fechado. No entanto, para fechar o painel de filtros e exibir somente o conteúdo gerado pelo usuário, clique no ícone Pesquisar e selecione a opção Somente conteúdo.

#### Caminho do conteúdo {#content-path}

Caminho de conteúdo limita o UGC de referência exibido para as publicações colocadas no repositório de conteúdo especificado.

![caminho-conteúdo](assets/content-path.png)

#### Pesquisa de texto {#text-search}

A pesquisa de texto limita o UGC referenciado exibido às publicações nas quais contém o texto inserido.

![pesquisa-texto](assets/text-search.png)

#### Site {#site}

O site limita o UGC referenciado exibido para publicações nos sites da comunidade selecionados. Se nenhum site for marcado, todas as referências ao UGC serão exibidas.

![painel-site](assets/site-panel.png)

>[!NOTE]
>
>Quando o console de moderação em massa é acessado por um administrador, todas as referências ao UGC são mostradas, incluindo sites não criados com o [assistente de criação de sites](/help/communities/sites-console.md), como as Geometrixx.
>
>Quando o console de moderação em massa é acessado no Publish por um membro confiável da comunidade, somente as referências ao UGC criado para sites da comunidade que o membro está autorizado a moderar são mostradas. Além disso, pode ser filtrado com o filtro Site.

#### Tipo de conteúdo {#content-type}

Tipo de conteúdo limita o UGC referenciado exibido às publicações do tipo de recurso selecionado. Um ou mais dos seguintes tipos podem ser selecionados. Todos os tipos são mostrados se nenhum estiver selecionado.

* **Comentário**
* **Tópico do fórum**
* **Resposta do fórum**
* **Pergunta de QnA**
* **Resposta QnA**
* **Artigo do blog**
* **Comentário no Blog**
* **Evento de calendário**
* **Comentário do calendário**
* **Pasta da Biblioteca de Arquivos**
* **Documento da biblioteca de arquivos**
* **Ideia**
* **Comentário sobre a ideação**

![tipos-conteúdo](assets/content-types.png)

#### Tipos de conteúdo adicionais {#additional-content-types}

Para adicionar recursos adicionais aos quais filtrar:

* Faça logon na instância do autor como administrador.
* Abra o [Console da Web](https://localhost:4502/system/console/configMgr).
* Localizar `AEM Communities Moderation Dashboard Filters`.
* Selecione a configuração para poder abrir no modo de edição.
* Insira o ResourceType de um componente no qual filtrar:

   * Por exemplo, para filtrar os componentes de Votação incluídos, informe:

     `Voting=social/tally/components/hbs/voting`

  ![tipo de conteúdo adicional](assets/additional-contenttype.png)

* Selecione Salvar.
* Atualize o console Comunidades - Moderação.

O resultado é um novo filtro selecionável para `Voting` no grupo de filtros `Content Type`.

Quando esse filtro é selecionado, o conteúdo do painel mostra o UGC que corresponde a qualquer um dos Tipos de recursos inseridos.

#### Status {#status}

Status limita o UGC referenciado exibido a publicações do status selecionado, que pode ser um ou mais de Pendente, Aprovado, Negado ou Fechado e Rascunho ou Agendado para Artigos do Blog e Respondido ou Não Respondido para Perguntas QnA. Se nenhum for selecionado, todos serão exibidos.

>[!NOTE]
>
>Se apenas o status Não respondido for selecionado, o moderador verá todo o conteúdo (para todos os tipos de conteúdo) exceto as perguntas respondidas. É assim porque a propriedade responsável pela Pergunta Respondida não existe se não houver perguntas não respondidas e outro conteúdo, como tópico de fórum, artigo de blog ou comentários.

![status](assets/statuses.png)

#### Sinalização {#flagging}

A sinalização limita o UGC referenciado exibido às publicações sinalizadas ou ocultas.

Depois que um conteúdo é sinalizado, ele permanece sinalizado até que você remova o sinalizador desse conteúdo único selecionando o botão **Sinalizar** novamente. Não há níveis de sinalização, como importante ou de acompanhamento.

![sinalizando](assets/flagging.png)

#### Membros {#members}

Membros limita o UGC referenciado exibido para o UGC publicado pelo nome do membro inserido.

![membros](assets/members.png)

#### Publicado nos últimos {#posted-in-the-last}

Publicado em Os últimos limita o UGC referenciado exibido nas publicações feitas na última hora, dia, semana, mês ou ano.

![postado-último](assets/posted-last.png)

#### Sentimento {#sentiment}

[Sentimento](/help/communities/moderate-ugc.md#sentiment) limita o UGC referenciado exibido a postagens com um valor de sentimento positivo, negativo ou neutro.

![sentimento](assets/sentiment.png)

## Filtros personalizados {#custom-filters}

Além dos filtros prontos para uso no [Trilho do filtro](/help/communities/moderation.md#ootbfilters), filtros personalizados adicionais sobre metadados podem ser adicionados à interface de moderação. Os desenvolvedores podem usar o código de amostra no GitHub para estender os filtros existentes da interface de moderação.

![filtro-tag-personalizado](assets/custom-tag-filter.png)

O [projeto de amostra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) no GitHub implementa o filtro Tag para filtrar a lista de UGC com base no fato de as marcas específicas serem aplicadas ao conteúdo gerado pelo usuário. Você pode seguir o código de amostra e criar filtros análogos para outros campos de metadados UGC semelhantes.

Para instalar a amostra do filtro Tags:

1. Abra o Gerenciador de Pacotes na instância do Autor AEM (`https://[aem-author]:4502/crx/packmgr/index.jsp`) e na instância do AEM Publish (`https://[aem-publish]:4503/crx/packmgr/index.jsp`).
1. Compile o pacote `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` do código GitHub, instale e habilite o mesmo.
1. Abra o console de pacotes na instância de Autor do AEM ( `https://[aem-author]:4502/system/console/bundles`) e na instância de AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Compile o pacote (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) do GitHub, instale e habilite o mesmo.
1. Vá para o nó **/apps/social/moderation/facets** na instância do Autor do AEM (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) e do AEM Publish (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`).
1. Adicione um usuário técnico **communities-utility-reader** com `jcr:read` permissões.

Para expor os filtros personalizados nos sites da Comunidade existentes:

1. Editar `Clientlibs` da página de moderação existente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Adicionar nova categoria `cq.social.hbs.moderation.v2.`

1. Ir para `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Definir para o novo componente `sling:resourceType = social/moderation/v2/filters.`

1. Acesse `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Defina para o novo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Ações de moderação {#moderation-actions}

[As ações de moderação](/help/communities/moderate-ugc.md#moderation-actions) podem ser executadas em uma ou mais seleções feitas na área de conteúdo ou ao exibir detalhes do conteúdo.

Para moderar as postagens em massa, na área de conteúdo, clique no ícone Selecionar (![seletor](assets/selecticon.png)) em uma postagem, que aparece ao passar o mouse sobre ela (área de trabalho) ou pressionando e segurando um dedo na postagem (celular). Ao fazer isso, você entra no modo de seleção múltipla e agora pode selecionar as publicações subsequentes para serem moderadas em massa, basta clicar nelas. Use os botões exibidos na barra de ferramentas para executar ações de moderação nas publicações selecionadas. Todas as ações solicitam confirmação.

Para moderar uma única publicação na área de conteúdo, passe o mouse sobre ela (na área de trabalho) ou pressione e mantenha pressionado um dedo na publicação (dispositivos móveis), de modo que os botões apareçam na publicação. Ao operar em um único detalhe de conteúdo, somente uma ação de exclusão solicita confirmação.

### Moderação de várias postagens {#moderating-multiple-posts}

Entre no modo de seleção em massa clicando no ícone `Select` em uma publicação:

![ícone de seleção](assets/select-icon.png)

Para sair do modo de seleção em massa, selecione o ícone Cancelar (x) na barra de ferramentas:

As ações de moderação que podem ser executadas em várias publicações são:

* Negar 
* Excluir
* Fechar/reabrir as postagens

Os ícones que permitem essas ações só aparecem na barra de ferramentas quando várias publicações são selecionadas.

![bulkmoderador](assets/bulkmoderate.png)

### Moderação de uma única publicação {#moderating-a-single-post}

No modo de seleção única, é possível:

* Exiba os detalhes do usuário selecionando o nome dele.
* Visualize a publicação no contexto, selecionando o link para a publicação.
* [Responder](#reply)
* [Permitir](#allow)
* [Negar ](#deny)
* [Excluir](#delete)
* [Fechar](#close)
* Exibir [Histórico de moderação](#moderation-history)
* [Exibir Detalhes](#viewdetails)

Presente na exibição de cartão acima dos ícones de ação de moderação está o texto da publicação e abaixo estão os dados que indicam:

* Se tiver respostas e, em caso afirmativo, precedido do número de respostas
* Se tiver sido sinalizado
* Se tiver sido aprovado
* Quando o UGC foi publicado

![singleselectmode](assets/singleselectmode.png)

#### Responder {#reply}

![responder](assets/reply.png)

Ao trabalhar com uma única publicação, um ícone Responder será exibido se o tipo de UGC der suporte a respostas e estiver configurado para permitir respostas.

#### Permitir {#allow}

![permitir](assets/allow.png)

Ao trabalhar com uma única publicação, o ícone Permitir é exibido quando a publicação é sinalizada ou negada. Se sinalizado, selecionar Permitir apaga todos os sinalizadores.

#### Negar  {#deny}

![negar](assets/deny.png)

A ação de moderação **Negar** só está disponível para conteúdo moderado e não aparece em conteúdo não moderado, exceto no modo de seleção múltipla.

O conteúdo que não é moderado é sempre aprovado.

O conteúdo moderado entra inicialmente em um estado Pendente e pode ser modificado posteriormente para aprovação ou negação.

O conteúdo que deixa o estado pendente nunca pode retornar a um estado pendente. O conteúdo marcado como aprovado ou negado pode ser alterado para um estado diferente a qualquer momento.

#### Excluir {#delete}

![excluir](assets/delete.png)

Na seleção única ou no modo em massa, é possível selecionar itens e excluí-los. A ação de exclusão resulta em uma caixa de diálogo de confirmação. Depois de excluídos, esses itens desaparecem imediatamente da área de conteúdo. **Depois que o UGC é excluído, ele é removido permanentemente do repositório e não pode ser recuperado posteriormente**.

#### Fechar {#close}

![fechar](assets/close.png)

Ao trabalhar com uma única publicação, um ícone Fechar será exibido se o tipo de UGC suportar a capacidade de evitar outras publicações para esse recurso.

#### Histórico de moderação {#moderation-history}

![moderação](assets/moderation.png)

Ao trabalhar com uma única publicação, um ícone de Histórico de moderação é exibido ao passar o mouse sobre ele. Selecionar o ícone exibe um painel contendo um histórico de ações executadas em relação à publicação UGC.

Para retornar à exibição da área de conteúdo de várias publicações UGC, selecione o X no canto superior direito do painel de detalhes da exibição.

Por exemplo:

![histórico-moderação](assets/moderation-history.png)

#### Exibir detalhe {#view-detail}

![exibir](assets/view.png)

Ao trabalhar com uma única publicação, para ver mais detalhes, abra o UGC no modo de detalhes.

Para fazer isso, passe o mouse sobre a publicação para exibir o ícone `View Detail` e selecione-o para exibir um painel contendo mais detalhes da publicação.

Para retornar à exibição da área de conteúdo de várias publicações UGC, selecione o X no canto superior direito do painel de detalhes da exibição.

Por exemplo:

![visualização1](assets/view1.png)
