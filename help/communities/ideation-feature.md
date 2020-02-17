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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Recurso Ideação{#ideation-feature}

## Introdução {#introduction}

O recurso de ideação fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente de publicação para:

* criar ideias para compartilhar com a comunidade
* exibir e comentar ideias
* seguir uma ideia
* votação de uma ideia

Esta seção da documentação descreve

* adicionar o recurso de ideação a um site do AEM
* configurações do componente Ideação

### Adding a Ideation to a Page {#adding-a-ideation-to-a-page}

Para adicionar um `Ideation` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Ideation`

e arraste-a para o lugar em uma página onde a ideia deve aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do cliente](/help/communities/ideation.md#essentials-for-client-side) necessárias forem incluídas, o `Ideation`componente aparecerá desta forma:

![chlimage_1-71](assets/chlimage_1-71.png)

### Configuração de uma ideia {#configuring-an-ideation}

Selecione o componente inserido a ser acessado e selecione o `Ideation` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-72](assets/chlimage_1-72.png) ![ideation-settings](assets/ideation-settings.png)

#### Guia Configurações {#settings-tab}

Em **Configurações **guia, especifique as configurações para ideias e comentários:

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

   Se marcada, permita que os membros adicionem etiquetas à sua postagem (consulte a guia Campo **de** tag). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que os anexos de arquivo sejam adicionados à ideia ou ao comentário. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` for verificada. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` for verificada. Uma lista separada por vírgulas de extensões de arquivos com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que** **todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152** **(2 Mb).

* **Permitir respostas**

   Se marcada, permita respostas a comentários postados na ideia. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, permita votar os comentários de uma ideia. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

   Se marcada, permita que os membros excluam os comentários e ideias publicados. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para publicações de ideias, que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novas publicações. O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcada, permita que os membros sejam notificados de novas postagens por email ([assinatura](/help/communities/subscriptions.md)). Requer `Allow Following` a verificação e configuração [de](/help/communities/email.md)email. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, permita votar os comentários de uma ideia. O padrão está desmarcado.

* **Exibir selos**

   Se marcada, exiba [crachás](/help/communities/implementing-scoring.md) ganhados e atribuídos com a ideia de um membro. O padrão está desmarcado.

* **Não obter respostas na página de listagem**

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como conteúdo [em](/help/communities/featured.md)destaque. O padrão está desmarcado.

* **Ativar a menção**
* **Quantidade máxima de menções**
* **Padrão de menção da interface do usuário**

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia **Moderação do usuário **, especifique como as ideias e os comentários publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

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

   Insira o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser ocultado da exibição pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia Campo **de** tag , as tags que podem ser aplicadas, se permitidas na guia **Settings **, são limitadas de acordo com os namespaces escolhidos.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` estiver marcado na guia **Configurações** . As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace verificadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como uma sugestão para o membro postando no fórum. Um valor de **-**1 significa sem limite. O padrão é 0.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **Configurações de classificação **s, especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Marque todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Puxe para baixo para selecionar uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Puxe para baixo para selecionar um dos `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

## Experiência do visitante do site {#site-visitor-experience}

### Criando ideia {#creating-idea}

Como acontece com todos os recursos das Comunidades, se não estiverem conectados, um visitante do site só poderá ler ideias e exibir opiniões de outras pessoas (por meio de comentários e votação/curtir).

Depois de conectado, um membro pode criar uma nova ideia.

![chlimage_1-73](assets/chlimage_1-73.png)

Antes de enviar a ideia, é possível que o membro salve um rascunho.

Ao selecionar o `Save as Draft` botão, um rascunho é salvo.

![chlimage_1-74](assets/chlimage_1-74.png)

Ao exibir rascunhos salvos na `My Drafts` guia, selecione `Read More` para entrar novamente no modo de edição:

![chlimage_1-75](assets/chlimage_1-75.png)

#### Fornecer feedback {#providing-feedback}

Uma vez publicada a ideia, outros membros podem fazer logon, abrir a ideia ( `Read More`) e gostar da ideia, adicionando ao número de votos e fazendo comentários.

![chlimage_1-76](assets/chlimage_1-76.png)

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Ideation Essentials](/help/communities/ideation.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.
