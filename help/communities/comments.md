---
title: Uso de comentários
description: O recurso Comentários permite que visitantes do site conectados compartilhem suas opiniões e conhecimentos
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Uso de comentários {#using-comments}

## Introdução {#introduction}

O recurso comentários é usado para permitir que visitantes do site (membros) conectados compartilhem suas opiniões e conhecimentos sobre o conteúdo do site. Esse recurso geralmente já está presente em outros recursos, mas pode ser adicionado a qualquer site.

O documento descreve:

* Adicionando `Comments` para uma página.
* Definições de configuração para o `Comments` componente.

>[!NOTE]
>
>Não há suporte para postagem anônima de um comentário. Os visitantes do site devem se registrar (tornar-se membros) e fazer logon para participar.

### Adicionar comentários a uma página {#adding-comments-to-a-page}

Para adicionar um `Comments` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Comments`

e arraste-o para o local em uma página, como uma posição relativa ao recurso para que os usuários comentem ou simplesmente na parte inferior da página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-comments.md#essentials-for-client-side) são incluídos, é assim que a variável `Comments` é exibido.

![comentários-componente](assets/comments-component.png)

>[!NOTE]
>
>Somente um `Comments` pode existir em uma página. Observe que vários recursos das Comunidades já incluem comentários, como um blog, calendário, fórum, QnA e avaliações.

### Configuração de comentários {#configuring-comments}

Selecione o colocado `Comments` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![ícone de configuração](assets/configure.png)

![commentssettings](assets/commentssettings.png)

#### Guia Comentários {#comments-tab}

No **Comentários** especifique como os comentários são inseridos pelos visitantes.

* **Permitir respostas**

  Quando marcado, permite que os membros respondam aos comentários existentes. O padrão está desmarcado.

* **Comentários por página**

  Limita o número de comentários exibidos por página e o número de respostas exibidas. O padrão é 10.

* **Permitir carregamentos de arquivo**

  Se marcada, a opção para carregar um arquivo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Esse valor limita o tamanho do arquivo carregado. O limite padrão é de 10 MB.

* **Comprimento máximo da mensagem**

  Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4.096 caracteres.

* **Tipos de arquivo permitidos**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Uma lista separada por vírgulas de extensões de nome de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Editor de Rich Text**

  Se marcado, os comentários serão inseridos com marcação. O padrão está desmarcado.

* **Permitir votação**

  Se marcada, a opção para votar para cima ou para baixo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Permitir acompanhamento**

  Se marcado, permitir que os membros sigam os comentários. O padrão está desmarcado.

* **Exibir selos**

  Se marcado, permite que medalhas ganhas e concedidas sejam exibidas. O padrão está desmarcado.

#### Guia Moderação de usuário {#user-moderation-tab}

No **Moderação de usuário** especifique como os comentários publicados são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Pré-moderação**

  Se marcados, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

  Se marcado, o membro que postou o comentário recebe a capacidade de excluí-lo. O padrão está desmarcado.

* **Negar comentários**

  Se marcado, permite que os moderadores neguem comentários. O padrão está desmarcado.

* **Fechar / Reabrir comentários**

  Se marcado, permite que os moderadores fechem e reabram os comentários. O padrão está desmarcado.

* **Sinalizar comentários**

  Se marcado, permite que os membros sinalizem comentários como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

  Se marcado, permite que os membros escolham, em uma lista suspensa, o motivo para sinalizar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

  Se marcado, permite que os membros insiram seu próprio motivo para sinalizar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

  Insira o número de vezes que um comentário deve ser marcado pelos membros antes que os moderadores sejam notificados. O padrão é uma vez (1).

* **Limite de sinalização**

  Insira o número de vezes que um comentário deve ser sinalizado antes de ser ocultado da visualização pública. Esse número deve ser maior ou igual ao **Limite de moderação**. O padrão é 5.

#### Guia Configurações de classificação {#sort-settings-tab}

No **Configurações de classificação** especifique como os comentários publicados são classificados quando exibidos.

* **Classificar campo**

  Selecione um dos `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`ou `Most Liked`.

* **Ordem de classificação**

  Selecione um dos `Ascending` ou `Descending`.

### Alterar para um tipo de comentário personalizado {#changing-to-a-custom-comment-type}

Ao alterar o Tipo de recurso de comentário, o sistema de comentário não gera mais uma instância de um comentário usando o padrão, mas sim uma que foi personalizada (estendida) pelos desenvolvedores.

Depois que os tipos de recursos personalizados forem conhecidos, insira [Modo Design](/help/sites-authoring/default-components-designmode.md) e clique duas vezes no local `Comments` para abrir uma caixa de diálogo com uma guia extra.

No **Tipos de recursos** especifique o resourceType personalizado para novas instâncias do `Comments or Voting` componentes:

![tipo de recurso](assets/resource-type.png)

* **Tipo de recurso de comentário**

  Navegue até o resourceType de uma extensão `comment` componente (comentário único) em /apps. Por exemplo, `/apps/social/commons/components/hbs/comments/comment`

  Esse recurso identifica o resourceType do UGC criado quando um visitante publica um comentário.

* **Tipo de recursos para pesquisa**

  Navegue até o resourceType de uma extensão `voting` componente em /apps. Por exemplo, `/apps/social/components/hbs/voting`

  Esse recurso identifica o tipo de recurso do UGC criado quando um visitante publica um voto.

* **Tipo de recursos de comentários do sistema**

  Navegue até o resourceType de uma extensão `comments`componente (Sistema de comentários) em /apps. Deixe em branco, a menos que o modelo de página [inclui dinamicamente](/help/communities/scf.md#add-or-include-a-communities-component) o Sistema de comentários no script subjacente, em vez de ser adicionado à página como um recurso (nó comentários). Saiba mais lendo sobre o [`{{include}}` auxiliar](/help/communities/handlebars-helpers.md#include).

### Experiência de visitante do site {#site-visitor-experience}

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou o comentário.

#### Membros {#members}

Quando o visitante do site está conectado, dependendo da configuração, ele pode

* Postar um novo comentário
* Editar seu próprio comentário
* Excluir seu próprio comentário
* Sinalizar comentários de outras pessoas

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados podem ler somente os comentários publicados, traduzi-los se houver suporte, mas não podem adicionar um comentário nem sinalizar comentários de outras pessoas.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos de comentários](/help/communities/essentials-comments.md) página para desenvolvedores.

Para moderação dos comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para tradução de comentários publicados, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
