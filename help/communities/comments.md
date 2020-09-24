---
title: Uso de comentários
seo-title: Uso de comentários
description: Os recursos de comentários permitem que visitantes do site conectados compartilhem suas opiniões e conhecimentos
seo-description: Os recursos de comentários permitem que visitantes do site conectados compartilhem suas opiniões e conhecimentos
uuid: 40acd962-846c-483c-b789-aab3a7d2b31b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 216cfb3e-777e-4773-afba-749debdca000
docset: aem65
translation-type: tm+mt
source-git-commit: 6be0aa7c3f6b21ad26221289a6cca2b4615ed3f4
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 6%

---


# Uso de comentários {#using-comments}

## Introdução {#introduction}

O recurso comments é usado para permitir que visitantes do site conectados (membros) compartilhem suas opiniões e conhecimentos sobre o conteúdo do site. Esse recurso geralmente já está presente em outros recursos, mas pode ser adicionado a qualquer site.

O documento descreve:

* Adicionando `Comments` a uma página.
* Configurações do `Comments` componente.

>[!NOTE]
>
>Não há suporte para a publicação anônima de um comentário. Os visitantes do site devem se registrar (tornar-se um membro) e fazer logon para participar.


### Adicionar comentários a uma página {#adding-comments-to-a-page}

Para adicionar um `Comments` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Comments`

e arraste-o para o lugar em uma página, como uma posição relativa ao recurso no qual os usuários podem comentar ou simplesmente na parte inferior da página.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do cliente](/help/communities/essentials-comments.md#essentials-for-client-side) necessárias são incluídas, é assim que o `Comments` componente aparece.

![comments-component](assets/comments-component.png)

>[!NOTE]
>
>Somente um `Comments` componente pode existir em uma página. Esteja ciente de que vários recursos das Comunidades já incluem comentários, como um blog, calendário, fórum, QnA e revisões.


### Configuração de comentários {#configuring-comments}

Selecione o componente inserido a ser acessado e selecione o `Comments` `Configure` ícone que abre a caixa de diálogo de edição.

![ícone configurar](assets/configure.png)

![commentssettings](assets/commentssettings.png)

#### Guia Comentários {#comments-tab}

Na guia **Comentários** , especifique como os comentários são inseridos pelos visitantes.

* **Permitir respostas**

   Se marcada, permite que os membros respondam aos comentários existentes. O padrão está desmarcado.

* **Comentários por página**

   Limita o número de comentários exibidos por página e o número de respostas exibidas. O padrão é 10.

* **Permitir carregamento de arquivos**

   Se marcada, a opção para carregar um arquivo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. Esse valor limita o tamanho do arquivo carregado. O limite padrão é 10 MB.

* **Comprimento máximo da mensagem de**

   Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4096 caracteres.

* **Tipos de arquivos permitidos**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. Uma lista separada por vírgulas de extensões de nome de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Editor de Rich Text**

   Se marcada, os comentários são inseridos com marcação. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, a opção para votar para cima ou para baixo é apresentada com a caixa de entrada de texto. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, permita que os membros sigam os comentários. O padrão está desmarcado.

* **Exibir selos**

   Se marcada, permita que os crachás ganhados e premiados sejam exibidos. O padrão está desmarcado.

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia Moderação **do** usuário, especifique como os comentários publicados serão gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

* **Pré-moderação**

   Se marcada, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, o membro que postou o comentário terá a capacidade de excluí-lo. O padrão está desmarcado.

* **Negar comentários**

   Se marcada, permita que os moderadores neguem comentários. O padrão está desmarcado.

* **Fechar/Reabrir comentários**

   Se marcada, permita que os moderadores fechem e reabram os comentários. O padrão está desmarcado.

* **Sinalizar comentários**

   Se marcada, permita que os membros sinalizem comentários como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, seu motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros digitem seu próprio motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é uma vez (1).

* **Limite de sinalização**

   Insira o número de vezes que um comentário deve ser sinalizado antes de ser ocultado da visualização pública. Esse número deve ser maior ou igual ao Limite de **moderação**. O padrão é 5.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **Classificar configurações** , especifique como os comentários publicados são classificados quando exibidos.

* **Classificar campo**

   Puxe para baixo para selecionar um dos `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed`ou `Most Liked`.

* **Ordem de classificação**

   Puxe para baixo para selecionar um de `Ascending` ou `Descending`.

### Alteração para um tipo de comentário personalizado {#changing-to-a-custom-comment-type}

Ao alterar o Tipo de recurso de comentário, o sistema de comentários não gera mais uma instância de um comentário usando o padrão, mas uma que foi personalizada (estendida) pelos desenvolvedores.

Depois que os tipos de recursos personalizados forem conhecidos, entre no Modo [de](/help/sites-authoring/default-components-designmode.md) design e clique no duplo no componente inserido `Comments` para abrir uma caixa de diálogo com uma guia extra.

Na guia Tipos **de** recursos, especifique o resourceType personalizado para novas instâncias dos `Comments or Voting` componentes:

![tipo de recurso](assets/resource-type.png)

* **Tipo de recursos de comentários**

   Navegue até resourceType de um `comment` componente estendido (comentário único) em /apps. Por exemplo, `/apps/social/commons/components/hbs/comments/comment`

   Esse recurso identifica o resourceType do UGC criado quando um visitante postou um comentário.

* **Tipo de recursos para pesquisa**

   Navegue até resourceType de um componente estendido em /apps. `voting` Por exemplo, `/apps/social/components/hbs/voting`

   Esse recurso identifica o tipo de recurso do UGC criado quando um visitante posta um voto.

* **Tipo de recurso do sistema de comentários**

   Navegue até resourceType de um `comments`componente estendido (Sistema de comentários) em /apps. Deixe em branco, a menos que o modelo de página inclua [](/help/communities/scf.md#add-or-include-a-communities-component) dinamicamente o Sistema de comentários no script subjacente em vez de ser adicionado à página como um recurso (nó de comentários). Saiba mais lendo sobre o auxiliar [](/help/communities/handlebars-helpers.md#include){{include}}.

### Experiência com o Visitante do site {#site-visitor-experience}

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou o comentário.

#### Membros {#members}

Quando o visitante do site estiver conectado, dependendo da configuração, eles poderão

* Publicar um novo comentário
* Editar seus próprios comentários
* Excluir seus próprios comentários
* Sinalizar comentários de outras pessoas

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados só podem ler comentários publicados, traduzi-los se houver suporte, mas não podem adicionar comentários nem sinalizar comentários de outras pessoas.

### Informações adicionais {#additional-information}

Para obter mais informações, consulte a página [Comments Essentials (Essenciais](/help/communities/essentials-comments.md) de comentários) para desenvolvedores.

Para moderação de comentários publicados, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para obter a tradução de comentários publicados, consulte [Traduzindo conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.
