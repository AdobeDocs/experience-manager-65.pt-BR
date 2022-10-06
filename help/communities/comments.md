---
title: Uso de comentários
seo-title: Using Comments
description: O recurso Comentários permite que visitantes do site que fizeram logon compartilhem suas opiniões e conhecimentos
seo-description: Comments feature lets signed-in site visitors share their opinions and knowledge
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
exl-id: 30baebd9-13c5-4fde-a494-85601abc32a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 6%

---

# Uso de comentários {#using-comments}

## Introdução {#introduction}

O recurso de comentários é usado para permitir que visitantes do site que fizeram logon (membros) compartilhem suas opiniões e conhecimentos sobre o conteúdo do site. Esse recurso geralmente já está presente em outros recursos, mas pode ser adicionado a qualquer site.

O documento descreve:

* Adição de `Comments` para uma página.
* Configurações para o `Comments` componente.

>[!NOTE]
>
>A publicação anônima de um comentário não é suportada. Os visitantes do site devem se registrar (se tornar um membro) e fazer logon para participar.

### Adicionar comentários a uma página {#adding-comments-to-a-page}

Para adicionar uma `Comments` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Comments`

e arraste-a para o local em uma página, como uma posição relativa ao recurso no qual os usuários devem comentar ou simplesmente na parte inferior da página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-comments.md#essentials-for-client-side) são incluídos, é assim que a variável `Comments` componente é exibido.

![componente comentários](assets/comments-component.png)

>[!NOTE]
>
>Somente um `Comments` pode existir em uma página. Esteja ciente de que vários recursos das Comunidades já incluem comentários, como um blog, calendário, fórum, QnA e revisões.

### Configuração de comentários {#configuring-comments}

Selecione o `Comments` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![ícone configurar](assets/configure.png)

![commentssettings](assets/commentssettings.png)

#### Guia Comentários {#comments-tab}

Em **Comentários** , especifique como os comentários são inseridos pelos visitantes.

* **Permitir respostas**

   Se marcada, permite que os membros respondam aos comentários existentes. O padrão está desmarcado.

* **Comentários por página**

   Limita o número de comentários exibidos por página e o número de respostas exibidas. O padrão é 10.

* **Permitir carregamento de arquivos**

   Se marcada, a opção para carregar um arquivo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante somente se Permitir uploads de arquivo estiver marcado. Esse valor limita o tamanho do arquivo carregado. O limite padrão é de 10 MB.

* **Comprimento máximo da mensagem de**

   Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4096 caracteres.

* **Tipos de arquivos permitidos**

   Relevante somente se Permitir uploads de arquivo estiver marcado. Uma lista separada por vírgulas de extensões de nome de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão é nenhum especificado, de modo que todos os tipos de arquivo são permitidos.

* **Editor de rich text**

   Se marcada, os comentários são inseridos com marcação. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, a opção para votar para cima ou para baixo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, permita que os membros sigam os comentários. O padrão está desmarcado.

* **Exibir selos**

   Se marcada, permita que os emblemas ganhados e atribuídos sejam exibidos. O padrão está desmarcado.

#### Guia Moderação do usuário {#user-moderation-tab}

Em **Moderação do usuário** , especifique como os comentários publicados são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Pré-moderação**

   Se marcada, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, o membro que postou o comentário terá a capacidade de excluí-lo. O padrão está desmarcado.

* **Negar comentários**

   Se marcada, permita que os moderadores neguem comentários. O padrão está desmarcado.

* **Fechar/Reabrir comentários**

   Se marcada, permita que os moderadores fechem e reabram comentários. O padrão está desmarcado.

* **Sinalizar comentários**

   Se marcada, permita que os membros sinalizem comentários como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, o motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros insiram seu próprio motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é uma vez (1).

* **Limite de sinalização**

   Insira o número de vezes que um comentário deve ser sinalizado antes de ser oculto da exibição pública. Esse número deve ser maior ou igual a **Limite de moderação**. O padrão é 5.

#### Guia Configurações de classificação {#sort-settings-tab}

Em **Classificar configurações** , especifique como os comentários publicados são classificados quando exibidos.

* **Classificar campo**

   Puxe para baixo para selecionar um dos `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`ou `Most Liked`.

* **Ordem de classificação**

   Puxe para baixo para selecionar um dos `Ascending` ou `Descending`.

### Alterar para um tipo de comentário personalizado {#changing-to-a-custom-comment-type}

Ao alterar o Tipo de recurso do comentário, o sistema de comentários não gera mais uma instância de um comentário usando o padrão, mas uma que foi personalizada (estendida) pelos desenvolvedores.

Depois que os tipos de recursos personalizados forem conhecidos, insira [Modo Design](/help/sites-authoring/default-components-designmode.md) e clique duas vezes em `Comments` para abrir uma caixa de diálogo com uma guia extra.

Em **Tipos de recursos** , especifique o resourceType personalizado para novas instâncias do `Comments or Voting` componentes:

![tipo de recurso](assets/resource-type.png)

* **Tipo de recursos de comentários**

   Navegue até o resourceType de um `comment` componente (comentário único) em /apps. Por exemplo, `/apps/social/commons/components/hbs/comments/comment`

   Esse recurso identifica o resourceType do UGC criado quando um visitante publica um comentário.

* **Tipo de recursos para pesquisa**

   Navegue até o resourceType de um `voting` componente em /apps. Por exemplo, `/apps/social/components/hbs/voting`

   Esse recurso identifica o tipo de recurso do UGC criado quando um visitante posta um voto.

* **Tipo de Recurso do Sistema de Comentários**

   Navegue até o resourceType de um `comments`componente (Sistema de comentários) em /apps. Deixe em branco, a menos que o modelo da página [inclui dinamicamente](/help/communities/scf.md#add-or-include-a-communities-component) o Sistema de comentários no script subjacente em vez de ser adicionado à página como um recurso (nó de comentários). Saiba mais ao ler sobre o [{{include}} auxiliar](/help/communities/handlebars-helpers.md#include).

### Experiência de visitante do site {#site-visitor-experience}

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou o comentário.

#### Membros {#members}

Quando o visitante do site está conectado, dependendo da configuração, ele pode

* Publicar um novo comentário
* Editar seu próprio comentário
* Excluir seus próprios comentários
* Sinalizar comentários de outras pessoas

#### Anônimo {#anonymous}

Os visitantes do site que não estiverem conectados podem ler somente os comentários publicados, traduzi-los se houver suporte, mas não podem adicionar um comentário nem sinalizar os comentários de outras pessoas.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Observações essenciais](/help/communities/essentials-comments.md) página para desenvolvedores.

Para obter a moderação dos comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para obter a tradução de comentários postados, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
