---
title: Recurso de ideação
description: Saiba como adicionar e configurar o recurso de ideação que permite aos membros da comunidade criar, exibir, seguir, votar e comentar ideias compartilhadas com a comunidade.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: e130bab4-524d-4413-ba8b-53d0ed9e8623
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 10%

---

# Recurso de ideação {#ideation-feature}

## Introdução {#introduction}

O recurso de ideação fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente de Publicação para:

* Crie ideias para compartilhar com a comunidade.
* Exibir e comentar em ideias.
* Siga uma ideia.
* Vote em uma ideia.

Esta seção da documentação descreve:

* Adicionar o recurso de ideação a um site AEM.
* Configurações do componente de ideação.

### Adicionar uma ideação a uma página {#adding-a-ideation-to-a-page}

Para adicionar um `Ideation` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Ideation`

E arraste-a para o lugar em uma página onde a ideia deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/ideation.md#essentials-for-client-side) são incluídos, é assim que a variável `Ideation` é exibido:

![ideação](assets/ideation.png)

### Configurar uma ideação {#configuring-an-ideation}

Selecione o colocado `Ideation` para que você possa acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Guia Configurações {#settings-tab}

No **[!UICONTROL Configurações]** especifique as configurações para ideias e comentários:

* **Permitir miniatura de anexo**
* **Tamanho máximo da miniatura do anexo**
* **Tamanho mínimo de imagem para a miniatura**
* **Tamanho máximo da miniatura**
* **Permitir membros privilegiados**
* **Membros privilegiados permitidos**
* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**
* **Título da ideação**

* O título de exibição da ideia. O padrão é `Ideation`.
* **Descrição da ideação**

  Uma descrição a ser exibida como um subtítulo para a ideia. O padrão é nenhuma descrição.

* **Tópicos por página**

  Define o número de ideias/postagens exibidas por página. O padrão é 10.

* **Moderada**

  Se marcadas, a postagem de ideias e comentários deve ser aprovada antes que eles possam aparecer em um site de publicação. O padrão está desmarcado.

* **Fechado**

  Se marcado, o fórum de ideação será fechado para novas ideias e comentários. O padrão está desmarcado.

* **Editor de rich text**

  Se marcado, as ideias e os comentários poderão ser inseridos com a marcação. O padrão está desmarcado.

* **Permitir marcação**

  Se marcados, permitem que os membros adicionem rótulos de tag às suas publicações (consulte **[!UICONTROL Campo de tag]** guia ). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

  Se marcado, permite que anexos de arquivo sejam adicionados à ideia ou ao comentário. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

  Relevante apenas se `Allow File Uploads` está marcado. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

  Relevante apenas se `Allow File Uploads` está marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

  Se marcada, permite respostas aos comentários publicados na ideia. O padrão está desmarcado.

* **Permitir votação**

  Se marcada, permite a votação dos comentários de uma ideia. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

  Se marcado, permite que os membros excluam os comentários e ideias que publicaram. O padrão está desmarcado.

* **Permitir monitoramento**

  Se marcado, incluir o seguinte recurso para publicações de ideia, o que permite que os membros sejam [notificado](/help/communities/notifications.md) de novos posts. O padrão está desmarcado.

* **Permitir assinaturas de email**

  Se marcado, permitir que os membros sejam notificados sobre novas publicações por email ([subscrição](/help/communities/subscriptions.md)). Exige `Allow Following` a ser verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Permitir votação**

  Se marcada, permite a votação dos comentários de uma ideia. O padrão está desmarcado.

* **Exibir selos**

  Se marcado, exibir ganho e atribuído [medalhas](/help/communities/implementing-scoring.md) com a ideia de um membro. O padrão está desmarcado.

* **Não receber respostas na página de listagem**

* **Ativar conteúdo em destaque**

  Se marcada, a ideia é identificável como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Habilitar a menção**
* **Quantidade máxima de menções**
* **Padrão de menção da interface do usuário**

#### Guia Moderação de usuário {#user-moderation-tab}

No **[!UICONTROL Moderação de usuário]** especifique como as ideias e os comentários publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

  Se marcados, os moderadores de membros confiáveis podem negar postagens e impedir que elas apareçam no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

  Se marcados, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Sinalizar postagens**

  Se marcado, permite que os membros marquem tópicos ou comentários de outras pessoas como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

  Se marcado, permite que os membros escolham, em uma lista suspensa, o motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

  Se marcado, permite que os membros insiram seu próprio motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

  Insira o número de vezes que um tópico ou comentário deve ser marcado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

  Insira o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser ocultado da visualização pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

No **[!UICONTROL Campo de tag]** guia, as tags que podem ser aplicadas, se permitido na guia **[!UICONTROL Configurações]** são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos**

  Relevante se `Allow Tagging` é verificado sob o **[!UICONTROL Configurações]** guia. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

  Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. Um valor de **-1** significa sem limite. O padrão é 0.

#### Guia Configurações de classificação {#sort-settings-tab}

No **[!UICONTROL Configurações de classificação]** especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

  Verificar todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

  Selecione uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

  Selecione um dos `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

## Experiência de visitante do site {#site-visitor-experience}

### Criando ideia {#creating-idea}

Como em todos os recursos das Comunidades, se você não estiver conectado, um visitante do site poderá somente ler ideias e exibir outras opiniões (por meio de comentários e voto/gosto).

Depois de conectado, um membro pode criar uma ideia.

![create-new-idea](assets/create-new-idea.png)

Antes de enviar a ideia, é possível que o membro salve um rascunho.

Ao selecionar a variável `Save as Draft` , um rascunho será salvo.

![save-idea](assets/save-idea.png)

Ao visualizar rascunhos salvos na `My Drafts` selecione `Read More` para entrar novamente no modo de edição:

![edit-idea](assets/edit-idea.png)

#### Fornecendo feedback {#providing-feedback}

Depois que a ideia for publicada, outros membros poderão fazer logon e abrir a ideia ( `Read More`) e curtir a ideia, somando assim à contagem de votos, e fazer comentários.

![feedback](assets/feedback-idea.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos da ideação](/help/communities/ideation.md) página para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação do conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).
