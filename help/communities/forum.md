---
title: Recurso do fórum
seo-title: Forum Feature
description: Como adicionar e configurar o recurso do fórum
seo-description: How to add and configure the forum feature
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
exl-id: 2b1a4917-9db6-436a-a5fd-c102fe41fb9d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1216'
ht-degree: 10%

---

# Recurso do fórum{#forum-feature}

## Introdução {#introduction}

O recurso de fórum fornece uma área para visitantes do site com logon (membros da comunidade) no ambiente de publicação para:

* Criar novos tópicos
* Exibir e responder aos tópicos
* Siga um tópico
* Pesquisar um fórum
* Ajude a moderar o conteúdo do fórum
* Mover tópicos do fórum de uma página para outra

Esta seção da documentação descreve:

* Adicionando o recurso do fórum a um site AEM.
* Configurações para o `Forum` componente.

### Adicionar um fórum a uma página {#adding-a-forum-to-a-page}

Para adicionar uma `Forum` para uma página no modo autor, use o navegador de componentes para localizar

* `Communities / Forum`

e arraste-o para o local em uma página onde o fórum deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-forum.md#essentials-for-client-side) são incluídos, é assim que a variável `Forum` componente será exibido:

![componente do fórum](assets/forum-component.png)

### Configurar um fórum {#configuring-a-forum}

Selecione o `Forum` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Guia Configurações {#settings-tab}

Em **Configurações** , especifique as configurações dos tópicos e respostas:

* **Permitir miniatura de anexo**

   Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

   Tamanho máximo (em pixels) da imagem de miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo da imagem para miniatura**
* **Tamanho máximo da miniatura**

   Tamanho máximo (em pixels) da imagem em miniatura para imagem em linha. O valor padrão é 800 x 800.

* **Tópicos por página**

   Define o número de tópicos/postagens exibidos por página. O padrão é 10.

* **Moderada**

   Se marcada, a publicação de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcada, o fórum é fechado para novos tópicos e comentários. O padrão está desmarcado.

* **Editor de rich text**

   Se marcada, tópicos e comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

   Se marcada, permitir que membros adicionem rótulos de tag à publicação (consulte **Campo de tag** ). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que anexos de arquivo sejam adicionados ao tópico ou comentário. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para publicações do fórum, que permite que os membros sejam [notificado](/help/communities/notifications.md) de novos posts. O padrão está desmarcado.

* **Permitir fixação**

   Se marcada, os tópicos do fórum podem ser fixados ao topo da lista de tópicos. O padrão está desmarcado.

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcada, permita que os membros sejam notificados sobre novas postagens por email ([assinatura](/help/communities/subscriptions.md)). Exige `Allow Following` a verificar e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` está marcada. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` está marcada. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo : .jpg, .jpeg, .png, .doc, .docx, .pdf. Se qualquer tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivo são permitidos.

* **Tamanho máximo do arquivo de imagem anexada**
Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas encadeadas**

   Se marcada, permita respostas para comentários publicados no tópico. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, inclua o recurso Votação com um tópico. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

   Se marcada, permita que os membros excluam os comentários e tópicos publicados. O padrão está desmarcado.

* **Mostrar navegações estruturais**

   Se marcada, mostrar navegação estrutural nas páginas de tópicos. O padrão está marcado.

* **Exibir selos**

   Se marcada, exibir ganhado e atribuído [emblemas](/help/communities/implementing-scoring.md) com a entrada de um membro no blog. O padrão está desmarcado.

* **Permitir membros privilegiados**

   Se marcada, somente os membros com privilégios poderão criar conteúdo.

* **Membros privilegiados permitidos**

   Adicione os membros privilegiados com permissão para criar conteúdo.

* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**

   Se estiver ativado, bloqueia o Conteúdo gerado pelo usuário durante a edição no Modo de autor.

* **Ativar a menção**

   Se estiver habilitado, o permite que usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e os marque usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restrinja o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Pode ser necessário verificar ambos `AllowThreaded Replies` e `Allow users to Delete Comments and Topics` para permitir comentários em um tópico.

#### Guia Moderação do usuário {#user-moderation-tab}

Em **Moderação do usuário** , especifique como os tópicos e as respostas publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

   Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

   Se marcada, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Mover tópicos**

   Se marcada, permita que moderadores do lado da publicação movam tópicos. O padrão está marcado.

* **Sinalizar postagens**

   Se marcada, permita que os membros sinalizem os tópicos ou comentários de outras pessoas como inapropriado. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, o motivo para marcar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros insiram seu próprio motivo para marcar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um tópico ou comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

   Insira o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser oculto da exibição pública. Se definido como -1, o tópico ou comentário sinalizado nunca será oculto da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Em **Campo de tag** , as tags que podem ser aplicadas, se permitidas sob a variável **Configurações** , são limitadas de acordo com os namespaces escolhidos.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` é verificada sob o **Configurações** guia . As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace verificadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como sugestão para o membro postando no fórum. O padrão é **-**1 (sem limites).

#### Guia Tradução {#translation-tab}

Em **Tradução** , se a tradução estiver ativada para o site da comunidade, a tradução poderá ser definida para traduzir o tópico inteiro ou as publicações selecionadas.

* **Converter tudo**

   Se marcada, o thread do fórum é traduzido para o idioma preferencial do usuário. O padrão está desmarcado.

#### Guia Configurações de classificação {#sort-settings-tab}

Em **Classificar configurações** , especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Marque todas as seleções de classificação permitidas : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Puxe para baixo para selecionar uma das opções de classificação marcadas que serão exibidas como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Puxe para baixo para selecionar uma das seguintes opções: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   O padrão é `All`.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do fórum](/help/communities/essentials-forum.md) página para desenvolvedores.

Para obter moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).

Para obter a tradução de tópicos e comentários publicados, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
