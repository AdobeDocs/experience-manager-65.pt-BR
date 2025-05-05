---
title: Recurso de fórum
description: Saiba como adicionar e configurar o recurso de fórum que fornece uma área para membros da comunidade conectados criarem, visualizarem, seguirem, pesquisarem ou responderem tópicos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---

# Recurso de fórum{#forum-feature}

## Introdução {#introduction}

O recurso de fórum fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente do Publish para:

* Criar tópicos
* Exibir e responder a tópicos
* Seguir um tópico
* Pesquisar um fórum
* Ajude a moderar o conteúdo do fórum
* Mover tópicos do fórum de uma página para outra

Esta seção da documentação descreve:

* Adicionando o recurso de fórum a um site AEM.
* Definições de configuração para o componente `Forum`.

### Adicionando um fórum a uma página {#adding-a-forum-to-a-page}

Para adicionar um componente `Forum` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Forum`

E arraste-o para o local em uma página onde o fórum deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-forum.md#essentials-for-client-side) são incluídas, é assim que o componente `Forum` aparece:

![componente-fórum](assets/forum-component.png)

### Configurar um fórum {#configuring-a-forum}

Selecione o componente `Forum` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

![configuração-fórum](assets/forum-config.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações**, especifique configurações para tópicos e respostas:

* **Permitir miniatura do anexo**

  Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

  Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo da imagem para a miniatura**
* **Tamanho Máximo da Miniatura**

  Tamanho máximo (em pixels) da imagem em miniatura para imagem integrada. O valor padrão é 800 x 800.

* **Tópicos por página**

  Define o número de tópicos/postagens exibidos por página. O padrão é 10.

* **Moderado**

  Se marcados, a postagem de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

  Se marcado, o fórum será fechado para novos tópicos e comentários. O padrão está desmarcado.

* **Editor de Rich Text**

  Se marcados, os tópicos e comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

  Se marcado, permite que os membros adicionem rótulos de marca às suas publicações (consulte a guia **Campo de marca**). O padrão está desmarcado.

* **Permitir Carregamentos de Arquivos**

  Se marcado, permite que anexos de arquivo sejam adicionados ao tópico ou comentário. O padrão está desmarcado.

* **Permitir acompanhamento**

  Se marcado, inclui o seguinte recurso para postagens no fórum, o que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novas postagens. O padrão está desmarcado.

* **Permitir fixação**

  Se marcados, os tópicos do fórum poderão ser fixados no topo da lista de tópicos. O padrão está desmarcado.

* **Permitir conteúdo em destaque**

  Se marcada, a ideia é identificável como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Permitir assinaturas por email**

  Se marcado, permitirá que os membros sejam notificados sobre novas postagens por email ([assinatura](/help/communities/subscriptions.md)). Exige que `Allow Following` seja verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Tamanho máx. do arquivo**

  Relevante somente se `Allow File Uploads` estiver marcado. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

  Relevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máx. do arquivo de imagem a ser anexado**
Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas encadeadas**

  Se marcado, permite respostas aos comentários publicados no tópico. O padrão está desmarcado.

* **Permitir votação**

  Se marcado, inclui o recurso Votação com um tópico. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

  Se marcado, permite que os membros excluam os comentários e tópicos publicados. O padrão está desmarcado.

* **Mostrar navegações estruturais**

  Se essa opção estiver marcada, mostra navegações estruturais nas páginas de tópico. O padrão está marcado.

* **Exibir selos**

  Se marcado, exibe [medalhas](/help/communities/implementing-scoring.md) obtidas e atribuídas com uma entrada de blog do membro. O padrão está desmarcado.

* **Permitir membros privilegiados**

  Se marcado, somente os membros Privilegiados poderão criar conteúdo.

* **Membros Privilegiados Permitidos**

  Adicione os membros privilegiados com permissão para criar conteúdo.

* **Bloquear Conteúdo Gerado pelo Usuário no Modo de Edição do Autor**

  Se estiver ativado, bloqueia o conteúdo gerado pelo usuário ao editar no Modo Autor.

* **Habilitar menção**

  Se ativado, permite que os usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e marquem-nos usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Máximo de menções**

  Restringir o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de Menção da Interface do Usuário**

  Especifique a string do padrão permitido para marcar (@mention) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Talvez seja necessário marcar `AllowThreaded Replies` e `Allow users to Delete Comments and Topics` para habilitar comentários em um tópico.

#### Guia Moderação de usuário {#user-moderation-tab}

Na guia **Moderação de usuário**, especifique como os tópicos e respostas postados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderando conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

  Se marcados, os moderadores de membros confiáveis têm permissão para negar postagens e impedir que elas apareçam no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir Tópicos**

  Se marcados, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Mover Tópicos**

  Se marcado, permite que os moderadores na publicação movam tópicos. O padrão está marcado.

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

Na guia **Campo de marca**, as marcas que podem ser aplicadas, se permitidas na guia **Configurações**, são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos**

  Relevante se `Allow Tagging` estiver marcado na guia **Configurações**. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

  Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. O padrão é **-**&#x200B;1 (sem limites).

#### Guia Tradução {#translation-tab}

Na guia **Tradução**, se a tradução estiver habilitada para o site da comunidade, a tradução poderá ser definida para traduzir todo o tópico ou as postagens selecionadas.

* **Traduzir tudo**

  Se marcado, o thread do fórum será traduzido para o idioma preferencial do usuário. O padrão está desmarcado.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **Configurações de Classificação**, especifique como os comentários publicados são classificados quando exibidos.

* **Classificar por**

  Verificar todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

  Selecione uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar opções de tempo para a classificação do Analytics**

  Selecione uma das seguintes opções: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

  O padrão é `All`.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Forum Essentials](/help/communities/essentials-forum.md) para desenvolvedores.

Para obter a moderação de tópicos e comentários publicados, consulte [Moderando conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários postados, consulte [Marcação de Conteúdo Gerado pelo Usuário](/help/communities/tag-ugc.md).

Para tradução de tópicos e comentários publicados, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
