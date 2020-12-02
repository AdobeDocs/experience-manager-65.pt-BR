---
title: Recurso Ideação
seo-title: Recurso Ideação
description: Adicionar e configurar o recurso Ideação
seo-description: Adicionar e configurar o recurso Ideação
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
translation-type: tm+mt
source-git-commit: f62fb1eb760ddd7baee9ba5a631ff4b921e2d08b
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 10%

---


# Recurso Ideação {#ideation-feature}

## Introdução {#introduction}

O recurso de ideação fornece uma área para visitantes de site conectados (membros da comunidade) no ambiente de publicação para:

* Crie ideias para compartilhar com a comunidade.
* Visualização e comentário sobre ideias.
* Siga uma ideia.
* Votem em uma ideia.

Esta seção da documentação descreve:

* Adicionar o recurso de ideação a um site AEM.
* Configurações do componente Ideação.

### Adicionar uma ideia a uma página {#adding-a-ideation-to-a-page}

Para adicionar um componente `Ideation` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Ideation`

e arraste-a para o lugar em uma página onde a ideia deve aparecer.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/ideation.md#essentials-for-client-side) forem incluídas, o componente `Ideation` aparecerá desta forma:

![ideação](assets/ideation.png)

### Configurando uma Ideia {#configuring-an-ideation}

Selecione o componente `Ideation` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### Guia Configurações {#settings-tab}

Na guia **[!UICONTROL Settings]**, especifique as configurações para ideias e comentários:

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

   Uma descrição para exibir como um subtítulo para a ideia. O padrão não é descrição.

* **Tópicos por página**

   Define o número de ideias/postagens exibidas por página. O padrão é 10.

* **Moderada**

   Se marcada, a postagem de ideias e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcada, o fórum de ideação está fechado a novas ideias e comentários. O padrão está desmarcado.

* **Editor de Rich Text**

   Se marcada, ideias e comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

   Se marcada, permita que os membros adicionem etiquetas à sua postagem (consulte a guia **[!UICONTROL Campo de tag]**). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que os anexos de arquivo sejam adicionados à ideia ou ao comentário. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante somente se `Allow File Uploads` estiver marcado. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

   Se marcada, permita respostas a comentários postados na ideia. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, permita votar os comentários de uma ideia. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

   Se marcada, permita que os membros excluam os comentários e ideias que publicaram. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para publicações de ideias, que permite que os membros sejam [notificados](/help/communities/notifications.md) de novas publicações. O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcada, permita que os membros sejam notificados de novas postagens por email ([subscrição](/help/communities/subscriptions.md)). Exige que `Allow Following` seja verificado e [e-mail configurado](/help/communities/email.md). O padrão está desmarcado.

* **Permitir votação**

   Se marcada, permita votar os comentários de uma ideia. O padrão está desmarcado.

* **Exibir selos**

   Se marcada, exiba os [emblemas](/help/communities/implementing-scoring.md) obtidos e atribuídos com a ideia de um membro. O padrão está desmarcado.

* **Não obter respostas na página de listagem**

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Ativar a menção**
* **Quantidade máxima de menções**
* **Padrão de menção da interface do usuário**

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia **[!UICONTROL Moderação do usuário]**, especifique como as ideias e os comentários publicados (conteúdo gerado pelo usuário) serão gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

   Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

   Se marcada, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Sinalizar postagens**

   Se marcada, permita que os membros sinalizem os tópicos ou comentários de outras pessoas como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, seu motivo para marcar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros insiram seu próprio motivo para marcar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um tópico ou comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

   Insira o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser ocultado da visualização pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da visualização pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia **[!UICONTROL Campo de tag]**, as tags que podem ser aplicadas, se permitidas na guia **[!UICONTROL Settings]**, são limitadas de acordo com as namespaces escolhidas.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` estiver marcado na guia **[!UICONTROL Settings]**. As marcas que podem ser aplicadas são limitadas às da categoria verificada. A lista do namespace inclui &quot;Tags padrão&quot; (a namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todas as namespaces são permitidas.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como uma sugestão para o membro postando no fórum. Um valor de **-1** significa que não há limite. O padrão é 0.

#### guia Configurações de classificação {#sort-settings-tab}

Na guia **[!UICONTROL Classificar configurações]**, especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Marque todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Puxe para baixo para selecionar uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Puxe para baixo para selecionar `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

## Experiência de Visitante do site {#site-visitor-experience}

### Criando Ideia {#creating-idea}

Como acontece com todos os recursos das Comunidades, se não estiverem conectados, um visitante do site só poderá ler ideias e visualização opiniões de outras pessoas (através de comentários e votação/curtir).

Depois de conectado, um membro pode criar uma nova ideia.

![create-new-idea](assets/create-new-idea.png)

Antes de enviar a ideia, é possível que o membro salve um rascunho.

Ao selecionar o botão `Save as Draft`, um rascunho é salvo.

![ideia salvadora](assets/save-idea.png)

Ao exibir rascunhos salvos na guia `My Drafts`, selecione `Read More` para entrar novamente no modo de edição:

![ideia de edição](assets/edit-idea.png)

#### Fornecer feedback {#providing-feedback}

Assim que a ideia for publicada, outros membros poderão fazer logon, abrir a ideia ( `Read More`) e curtir a ideia, adicionando à contagem de votos e fazendo comentários.

![feedback](assets/feedback-idea.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Ideation Essentials](/help/communities/ideation.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).
