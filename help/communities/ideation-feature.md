---
title: Recurso de ideação
description: Saiba como adicionar e configurar o recurso de ideação que permite aos membros da comunidade criar, exibir, seguir, votar e comentar ideias compartilhadas com a comunidade.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---

# Recurso de ideação {#ideation-feature}

## Introdução {#introduction}

O recurso de ideação fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente do Publish para:

* Crie ideias para compartilhar com a comunidade.
* Exibir e comentar em ideias.
* Siga uma ideia.
* Vote em uma ideia.

Esta seção da documentação descreve:

* Adicionar o recurso de ideação a um site AEM.
* Configurações do componente de ideação.

### Adicionar uma ideação a uma página {#adding-a-ideation-to-a-page}

Para adicionar um componente `Ideation` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Ideation`

E arraste-a para o lugar em uma página onde a ideia deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/ideation.md#essentials-for-client-side) são incluídas, é assim que o componente `Ideation` aparece:

![ideação](assets/ideation.png)

### Configurar uma ideação {#configuring-an-ideation}

Selecione o componente `Ideation` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

![configurações-ideação](assets/ideation-settings.png)

#### Guia Configurações {#settings-tab}

Na guia **[!UICONTROL Configurações]**, especifique configurações para ideias e comentários:

* **Permitir miniatura do anexo**
* **Tamanho máximo da miniatura do anexo**
* **Tamanho mínimo da imagem para a miniatura**
* **Tamanho Máximo da Miniatura**
* **Permitir membros privilegiados**
* **Membros Privilegiados Permitidos**
* **Bloquear Conteúdo Gerado pelo Usuário no Modo de Edição do Autor**
* **Título da ideação**

* O título de exibição da ideia. O padrão é `Ideation`.
* **Descrição da ideação**

  Uma descrição a ser exibida como um subtítulo para a ideia. O padrão é nenhuma descrição.

* **Tópicos por página**

  Define o número de ideias/postagens exibidas por página. O padrão é 10.

* **Moderado**

  Se marcadas, a postagem de ideias e comentários deve ser aprovada antes que eles possam aparecer em um site de publicação. O padrão está desmarcado.

* **Fechado**

  Se marcado, o fórum de ideação será fechado para novas ideias e comentários. O padrão está desmarcado.

* **Editor de Rich Text**

  Se marcado, as ideias e os comentários poderão ser inseridos com a marcação. O padrão está desmarcado.

* **Permitir marcação**

  Se marcado, permite que os membros adicionem rótulos de marca às suas publicações (consulte a guia **[!UICONTROL Campo de marca]**). O padrão está desmarcado.

* **Permitir Carregamentos de Arquivos**

  Se marcado, permite que anexos de arquivo sejam adicionados à ideia ou ao comentário. O padrão está desmarcado.

* **Tamanho máx. do arquivo**

  Relevante somente se `Allow File Uploads` estiver marcado. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

  Relevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máx. do arquivo de imagem a ser anexado**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

  Se marcada, permite respostas aos comentários publicados na ideia. O padrão está desmarcado.

* **Permitir votação**

  Se marcada, permite a votação dos comentários de uma ideia. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

  Se marcado, permite que os membros excluam os comentários e ideias que publicaram. O padrão está desmarcado.

* **Permitir acompanhamento**

  Se marcado, incluir o seguinte recurso para publicações de ideias, o que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novas publicações. O padrão está desmarcado.

* **Permitir assinaturas por email**

  Se marcado, permitirá que os membros sejam notificados sobre novas postagens por email ([assinatura](/help/communities/subscriptions.md)). Exige que `Allow Following` seja verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Permitir votação**

  Se marcada, permite a votação dos comentários de uma ideia. O padrão está desmarcado.

* **Exibir selos**

  Se marcado, exibe [medalhas](/help/communities/implementing-scoring.md) obtidas e atribuídas com a ideia de um membro. O padrão está desmarcado.

* **Não Obter Respostas na Página de Listagem**

* **Permitir conteúdo em destaque**

  Se marcada, a ideia é identificável como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Habilitar menção**
* **Máximo de menções**
* **Padrão de Menção da Interface do Usuário**

#### Guia Moderação de usuário {#user-moderation-tab}

Na guia **[!UICONTROL Moderação de usuário]**, especifique como as ideias e os comentários publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderando conteúdo gerado por usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

  Se marcados, os moderadores de membros confiáveis podem negar postagens e impedir que elas apareçam no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir Tópicos**

  Se marcados, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Sinalizar postagens**

  Se marcado, permite que os membros marquem tópicos ou comentários de outras pessoas como inadequados. O padrão está desmarcado.

* **Lista de motivos da sinalização**

  Se marcado, permite que os membros escolham, em uma lista suspensa, o motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado do sinalizador**

  Se marcado, permite que os membros insiram seu próprio motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

  Insira o número de vezes que um tópico ou comentário deve ser marcado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de Sinalização**

  Insira o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser ocultado da visualização pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia **[!UICONTROL Campo de marca]**, as marcas que podem ser aplicadas, se permitidas na guia **[!UICONTROL Configurações]**, são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos**

  Relevante se `Allow Tagging` estiver marcado na guia **[!UICONTROL Configurações]**. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

  Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. Um valor de **-1** significa sem limite. O padrão é 0.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **[!UICONTROL Configurações de Classificação]**, especifique como os comentários publicados são classificados quando exibidos.

* **Classificar por**

  Verificar todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

  Selecione uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar opções de tempo para a classificação do Analytics**

  Puxe para baixo para selecionar um de `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

## Experiência de visitante do site {#site-visitor-experience}

### Criando ideia {#creating-idea}

Como em todos os recursos das Comunidades, se você não estiver conectado, um visitante do site poderá somente ler ideias e exibir outras opiniões (por meio de comentários e voto/gosto).

Depois de conectado, um membro pode criar uma ideia.

![criar-nova-ideia](assets/create-new-idea.png)

Antes de enviar a ideia, é possível que o membro salve um rascunho.

Ao selecionar o botão `Save as Draft`, um rascunho é salvo.

![salvar-ideia](assets/save-idea.png)

Ao exibir rascunhos salvos na guia `My Drafts`, selecione `Read More` para entrar novamente no modo de edição:

![editar-ideia](assets/edit-idea.png)

#### Fornecendo feedback {#providing-feedback}

Depois que a ideia for publicada, outros membros poderão entrar, abrir a ideia ( `Read More`) e curtir a ideia, adicionando à contagem de votos e fazer comentários.

![comentários](assets/feedback-idea.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Ideation Essentials](/help/communities/ideation.md) para desenvolvedores.

Para obter a moderação de tópicos e comentários publicados, consulte [Moderando Conteúdo Gerado por Usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários postados, consulte [Marcação de Conteúdo Gerado pelo Usuário](/help/communities/tag-ugc.md).
