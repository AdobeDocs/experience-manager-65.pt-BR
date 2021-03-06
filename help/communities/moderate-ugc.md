---
title: Moderação de conteúdo da comunidade
seo-title: Moderating Community Content
description: Conceitos e ações de moderação
seo-description: Moderation concepts and actions
uuid: 5c991d3a-0037-4d78-8f91-bb62e44441fa
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6866d209-5789-4ef9-bc3c-d644d4fb4b1c
docset: aem65
role: Admin
exl-id: 22276580-e6bc-41c5-9ac3-e8f291f676b7
source-git-commit: 812b9f3af3ad04343e648a8d07d53f8442978b82
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 2%

---

# Moderação de conteúdo da comunidade {#moderating-community-content}

## Visão geral {#overview}

O conteúdo da comunidade, também conhecido como conteúdo gerado pelo usuário (UGC), é criado quando um membro (visitante conectado do site) publica conteúdo de um site da comunidade publicado por meio da interação com um dos seguintes componentes da comunidade :

* [Blog](/help/communities/blog-feature.md): membros postam um artigo ou comentário no blog.
* [Calendário](/help/communities/calendar.md): os membros postam um evento ou comentário do calendário.
* [Comentários](/help/communities/comments.md): os membros postam um comentário ou respondem a um comentário.

* [Fórum](/help/communities/forum.md): os membros postam um novo tópico ou respondem a um tópico.
* [Ideação](/help/communities/ideation-feature.md): os membros postam uma ideia ou comentário.
* [QnA](/help/communities/working-with-qna.md): membros criam uma pergunta ou respondem uma pergunta.
* [Resenhas](/help/communities/reviews.md): os membros postam um comentário ao classificar um item.

A moderação do UGC é útil para reconhecer contribuições positivas, bem como limitar as negativas (como spam e linguagem abusiva). O UGC pode ser moderado de vários ambientes:

* [Armazenamento de conteúdo comunitário](working-with-srp.md)

* [Console de moderação em massa](moderation.md)

   O console Moderação é acessível aos administradores e [moderadores da comunidade](/help/communities/users.md) no ambiente público, bem como pelos administradores no ambiente do autor. Isso é possível quando o conteúdo da comunidade é armazenado em um [loja comum](/help/communities/working-with-srp.md).

* [Moderação no contexto](in-context.md)

   A moderação no ambiente de publicação pode ser executada pelos administradores e moderadores da comunidade diretamente na página em que o conteúdo foi publicado.

## Ações de moderação {#moderation-actions}

As ações que podem ser executadas no conteúdo publicado (UGC) variam de acordo com a identidade do usuário e o ambiente. A tabela abaixo usa a seguinte terminologia para descrever as várias funções de acordo com a identidade do usuário :

* `Admin`

   Um usuário que é membro de [administradores da comunidade](users.md) grupo.

* `Moderator`

   Um membro de um [moderadores da comunidade](users.md#publishenvironmentusersandgroups) grupo (tem [permissões de moderador](in-context.md#moderatorpermissions)).

* `Creator`

   O usuário que postou o conteúdo.

* `Member`

   Um usuário conectado sem permissões especiais.

* `Visitor`

   Um usuário anônimo.

<table>
 <tbody>
  <tr>
   <td> </td>
   <td><strong>Admin</strong></td>
   <td><strong>Moderador</strong></td>
   <td><strong>Criador</strong></td>
   <td><strong>Membro</strong></td>
   <td><strong>Visitante</strong></td>
   <td><strong>Evento<br /> Disparado</strong></td>
   <td><strong>Remodado</strong></td>
  </tr>
  <tr>
   <td><strong>Editar/<br /> Excluir</strong></td>
   <td>X</td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Recortar</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Negar </strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Fechar/<br /> Reabrir</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X<br /> </td>
  </tr>
  <tr>
   <td><strong>Sinalizador/<br /> Cancelar sinalização</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
   <td>X</td>
   <td> </td>
  </tr>
  <tr>
   <td><strong>Permitir</strong></td>
   <td>X</td>
   <td>X</td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td>X</td>
   <td>X</td>
  </tr>
 </tbody>
</table>

### Editar / Excluir {#edit-delete}

Depois que uma publicação é feita, ela pode ser editada ou excluída pelo criador, administrador ou moderador da comunidade.

Quando o UGC é excluído, ele é removido do repositório e pode não ser recuperado.

### Recortar {#cut}

Um administrador ou moderador de comunidade pode mover um ou mais tópicos do fórum ou perguntas de QnA de um local para outro. Isso inclui de um site da comunidade a outro site da comunidade, desde que o mesmo membro tenha privilégios de moderação em ambos os sites.

Ao selecionar a ação Cortar, o conteúdo é copiado para uma área de transferência. Várias publicações podem ser copiadas e movidas como um grupo para o novo local.

![cutugc](assets/cutugc.png)

![putbackugc](assets/putbackugc.png)

No outro local, quando o conteúdo está presente na área de transferência, um botão Colar fica visível ao lado da Nova publicação com um número identificando o número de publicações que serão coladas. O botão Colar inclui uma opção para limpar a área de transferência em vez de colar.

![pasteugc](assets/pasteugc.png)

![pasteugc1](assets/pasteugc1.png)

### Negar  {#deny}

Um moderador pode impedir que o UGC permaneça visível no site publicado. Para administradores e moderadores da comunidade, a publicação ainda está disponível e é anotada como spam.

### Fechar / Reabrir {#close-reopen}

A ação Fechar opera em todo o thread de conversa (um tópico de fórum ou o comentário inicial) e inclui todas as postagens ou respostas subsequentes.

Quando fechado, não apenas não são possíveis mais respostas, como também não são permitidas ações de moderação.

Para executar qualquer operação, o tópico ou comentário deve ser Reaberto.

A ação Fechar/Reabrir pode ser executada pelos administradores ou moderadores da comunidade.

### Sinalizar / Dessinalizar {#flag-unflag}

Sinalizar é um meio para qualquer membro conectado, exceto pelo criador do conteúdo, para indicar que há um problema com o conteúdo de uma publicação. Depois de sinalizado, um ícone de cancelamento de sinalizador será exibido, permitindo que o mesmo membro desmarque o conteúdo.

A moderação no contexto pode ser configurada para permitir que os membros selecionem um motivo ao marcar uma publicação. A lista de motivos de sinalizador selecionáveis pode ser configurada, incluindo se um motivo personalizado pode ou não ser inserido. O motivo do sinalizador é salvo com o UGC, mas o motivo não aciona nenhuma ação específica. Somente o número de sinalizadores aciona uma notificação. O conteúdo sinalizado é anotado como tal, para que os moderadores possam agir com base nele.

O sistema rastreia todos os sinalizadores, que foram sinalizados, e o motivo do sinalizador e envia um evento quando o limite foi atingido. Se o UGC for Permitido por um moderador da comunidade, esses sinalizadores serão arquivados. Depois de permitir e arquivar, se houver sinalizadores subsequentes, eles serão arquivados como se não houvesse sinalizadores anteriores.

### Permitir {#allow}

A ação Permitir é uma opção para UGC que foi Sinalizado, Negado ou não foi aprovado em um sistema pré-moderado. A ação Permitir limpará qualquer status sinalizado ou negado/spam presente e arquivará quaisquer dados sinalizados.

## Conceitos comuns de moderação {#common-moderation-concepts}

### Premoderation {#premoderation}

Quando o UGC é pré-moderado, a publicação não será exibida no site publicado até ser aprovada por uma ação de moderação. Durante a criação de um [site da comunidade](/help/communities/sites-console.md), marcando a caixa [O conteúdo é pré-implantado](sites-console.md#moderation) habilitará a pré-moderação para todo o site. Depois que os componentes são colocados em uma página, os componentes que oferecem suporte à moderação podem ser configurados para pré-moderação usando uma configuração na caixa de diálogo de edição:

* [Comentários](comments.md) e [revisões](reviews.md)
em **[!UICONTROL Moderação do usuário]** > **[!UICONTROL Pré-moderação]**.

* [Fórum](/help/communities/forum.md), [ideação](/help/communities/ideation-feature.md), [QnA](/help/communities/working-with-qna.md)e [calendário](/help/communities/calendar.md)
em **[!UICONTROL Configurações]** > **[!UICONTROL Moderado]**.

### Detecção de spam {#spam-detection}

A detecção de spam é uma funcionalidade de moderação automática, que filtra partes indesejadas do conteúdo gerado pelo usuário, marcando-as como spam. Depois de habilitado, ele identifica se o conteúdo gerado pelo usuário é spam ou não com base em uma coleção pré-configurada de palavras de spam. As palavras de spam padrão são fornecidas em

`/libs/settings/community/sites/moderation/spamdetector-conf/profiles/spam_words.txt`.

No entanto, para personalizar ou estender as palavras de spam padrão, crie um conjunto de palavras no diretório /apps seguindo a estrutura das palavras de spam padrão por meio de [sobreposição](/help/communities/overlay-comments.md).

Uma postagem gerada pelo usuário (em todos os tipos de conteúdo, por exemplo, blogs, fóruns e comentários) contendo palavras spam é marcada com o texto &quot;Essa postagem foi classificada como spam&quot; acima da postagem.

O moderador pode ver essa publicação e marcar a mesma para permitir ou negar a exibição no site. As ações de moderação nessas publicações podem ser executadas no contexto ou por meio da interface do usuário de moderação em massa.

![spam](assets/spamdetection.png)

Para ativar o mecanismo de detecção de spam, siga estas etapas:

1. Abrir [Console da Web](https://localhost:4502/system/console/configMgr), indo para `/system/console/configMgr`.

1. Localizar **Moderação automática do AEM Communities** e edite-a.
1. Adicione o **[!UICONTROL SpamProcess]** entrada.

![spamprocess](assets/spamprocess.png)

>[!NOTE]
>
>A detecção de spam só é implementada para o idioma inglês.

### Sentimento {#sentiment}

O sentimento é calculado com base no número de palavras-chave positivas e negativas ([palavras de ordem](#configuringwatchwords)) presente em uma publicação (UGC).

A análise de sentimento usa um conjunto de regras pré-configuradas e calcula o sentimento do UGC. As regras padrão estão localizadas em: `/libs/cq/workflow/components/workflow/social/sentiments/rules.`

O valor gerado pelas regras é de 1 (todas negativas, nenhuma palavra positiva) a 10 (todas positivas, nenhuma negativa). Um valor de sentimento de 5 é um sentimento neutro e é o padrão.

As regras definidas no componente /libs são:

* Regra 1: defina o valor como 1 se não houver palavras positivas e pelo menos uma palavra negativa.
* Regra 2: defina o valor como 10 se não houver palavras negativas e pelo menos uma palavra positiva.
* Regra 3: defina o valor como 3 se houver mais palavras negativas do que palavras positivas.
* Regra 4: defina o valor como 8 se houver mais palavras positivas do que palavras negativas.

Para substituir ou adicionar regras, crie um conjunto de regras no diretório /apps seguindo a estrutura das regras padrão. Edite a configuração de sentimento para identificar o local das regras.

Depois de analisado, o sentimento é armazenado com o UGC.

No [console de moderação em massa](/help/communities/moderation.md), é possível filtrar e exibir o UGC com base no fato do sentimento ser negativo, neutro ou positivo.

#### Palavras de vigia {#watchwords}

AEM comunidades fornece um *analisador de palavra de ordem* como etapa no processo de avaliação [sentimento](#sentiment). A contribuição para o valor do sentimento fornecido pelas palavras de ordem é devido a uma comparação de palavras de observação negativas e positivas usadas no conteúdo publicado, bem como de palavras proibidas.

#### Configurar o sentimento e as palavras de observação {#configure-sentiment-and-watchwords}

A lista de palavras de observação positivas e negativas pode ser personalizada como podem ser as regras de sentimento.

A lista padrão de palavras de ordem pode ser inserida como propriedades de um nó no repositório, semelhante ao padrão ou substituindo o padrão configurando o serviço OSGi `sentimentprocess.name` com a lista de palavras.

O **sentimentprocess.name** também pode ser modificado para fazer referência à localização de um conjunto personalizado de regras de sentimento.

Para configurar o sentimento e as palavras de observação:

* Faça logon na instância do autor como administrador.
* Abrir [Console da Web](https://localhost:4502/system/console/configMgr).
* Localizar `sentimentprocess.name`.
* Selecione a configuração a ser aberta no modo de edição.

![sentimentprocess](assets/sentimentprocess.png)

* **Palavras de observação positivas**

   Uma lista de palavras separada por vírgulas que contribui para um sentimento positivo que substitui os padrões. O padrão é uma lista vazia.

* **Palavras de inspeção negativas**

   Uma lista de palavras separada por vírgulas que contribui para um sentimento negativo que substitui os padrões. O padrão é uma lista vazia.

* **Caminho explícito para o nó de palavras de observação**

   O local do repositório de um nó que contém o padrão `positive` e `negative` propriedades que especificam palavras de observação padrão. O padrão é `/libs/settings/community/watchwords/default`.

* **Regras de sentimentos**

   O local do repositório das regras para calcular o sentimento com base em palavras de observação positivas e negativas. O padrão é `/libs/cq/workflow/components/workflow/social/sentiments/rules` (no entanto, não há mais nenhum workflow envolvido).

A seguir, um exemplo de uma entrada personalizada para palavras de observação padrão, quando `Explicit Path to Watchwords Node` está definida como `/libs/settings/community/watchwords/default`.

![crxde](assets/crxde.png)

### Permissões do moderador {#moderator-permissions}

As seguintes permissões, quando atribuídas ao mesmo recurso, são coletivamente chamadas de `moderator permissions`:

* `Read`
* `Modify`
* `Create`
* `Delete`
* `Replicate`
