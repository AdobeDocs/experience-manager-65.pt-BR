---
title: Recurso do fórum
seo-title: Recurso do fórum
description: Como adicionar e configurar o recurso do fórum
seo-description: Como adicionar e configurar o recurso do fórum
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 871c42ee000eb250c1c6159d9a0c752e8ed4d7b8
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 10%

---


# Recurso do fórum{#forum-feature}

## Introdução {#introduction}

O recurso de fórum fornece uma área para visitantes de site conectados (membros da comunidade) no ambiente de publicação para:

* Criar novos tópicos
* Visualização e resposta aos tópicos
* Siga um tópico
* Pesquisar em um fórum
* Ajudar a moderar o conteúdo do fórum
* Mover tópicos do fórum de uma página para outra

Esta seção da documentação descreve:

* Adicionar o recurso do fórum a um site AEM.
* Configurações do componente `Forum`.

### Adicionar um fórum a uma página {#adding-a-forum-to-a-page}

Para adicionar um componente `Forum` a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Forum`

e arraste-o para o lugar em uma página onde o fórum deve aparecer.

Para obter as informações necessárias, visite [Informações básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-forum.md#essentials-for-client-side) forem incluídas, o componente `Forum` aparecerá desta forma:

![componente do fórum](assets/forum-component.png)

### Configuração de um fórum {#configuring-a-forum}

Selecione o componente `Forum` inserido para acessar e selecione o ícone `Configure` que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações**, especifique as configurações para tópicos e respostas:

* **Permitir miniatura de anexo**

   Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

   Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo da imagem para miniatura**
* **Tamanho máximo da miniatura**

   Tamanho máximo (em pixels) da imagem em miniatura para imagem em linha. O valor padrão é 800 x 800.

* **Tópicos por página**

   Define o número de tópicos/postagens exibidos por página. O padrão é 10.

* **Moderada**

   Se marcada, a publicação de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcada, o fórum é fechado a novos tópicos e comentários. O padrão está desmarcado.

* **Editor de Rich Text**

   Se marcada, os tópicos e os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

   Se marcada, permita que os membros adicionem etiquetas à sua postagem (consulte a guia **Campo de tag**). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que os anexos do arquivo sejam adicionados ao tópico ou ao comentário. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para postagens do fórum, que permite que os membros sejam [notificados](/help/communities/notifications.md) de novas postagens. O padrão está desmarcado.

* **Permitir fixação**

   Se marcada, os tópicos do fórum podem ser fixados na parte superior da lista de tópicos. O padrão está desmarcado.

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcada, permita que os membros sejam notificados de novas postagens por email ([subscrição](/help/communities/subscriptions.md)). Exige que `Allow Following` seja verificado e [e-mail configurado](/help/communities/email.md). O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante somente se `Allow File Uploads` estiver marcado. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Tamanho máx. do arquivo de imagem anexadaRelevante somente se Permitir uploads de arquivo estiver marcado.**
Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas encadeadas**

   Se marcada, permita respostas para comentários postados no tópico. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, inclua o recurso Voto com um tópico. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

   Se marcada, permita que os membros excluam os comentários e tópicos publicados. O padrão está desmarcado.

* **Mostrar navegações estruturais**

   Se marcada, mostrar navegações estruturais em páginas de tópicos. O padrão está marcado.

* **Exibir selos**

   Se marcada, exiba os [emblemas](/help/communities/implementing-scoring.md) obtidos e atribuídos com a entrada de blog de um membro. O padrão está desmarcado.

* **Permitir membros privilegiados**

   Se marcada, somente membros privilegiados poderão criar conteúdo.

* **Membros privilegiados permitidos**

   Adicione os membros com privilégios permitidos para criar conteúdo.

* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**

   Se ativado, bloqueia o Conteúdo gerado pelo usuário durante a edição no Modo de autor.

* **Ativar a menção**

   Se ativada, permite que os usuários da comunidade registrados identifiquem outros membros registrados (usando o nome, sobrenome, nome de usuário) e os rotulem usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restrinja o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Pode ser necessário marcar `AllowThreaded Replies` e `Allow users to Delete Comments and Topics` para ativar os comentários em um tópico.

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia **Moderação do usuário**, especifique como os tópicos e as respostas publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

   Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

   Se marcada, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Mover tópicos**

   Se marcada, permita que os moderadores do lado da publicação movam tópicos. O padrão está marcado.

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

Na guia **Campo de tag**, as tags que podem ser aplicadas, se permitidas na guia **Settings**, são limitadas de acordo com as namespaces escolhidas.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` estiver marcado na guia **Settings**. As marcas que podem ser aplicadas são limitadas às da categoria verificada. A lista do namespace inclui &quot;Tags padrão&quot; (a namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todas as namespaces são permitidas.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como uma sugestão para o membro postando no fórum. O padrão é **-**1 (sem limites).

#### Guia Tradução {#translation-tab}

Na guia **Tradução**, se a tradução estiver ativada para o site da comunidade, a tradução poderá ser definida para traduzir o tópico inteiro ou as publicações selecionadas.

* **Converter tudo**

   Se marcada, o thread do fórum é traduzido para o idioma preferencial do usuário. O padrão está desmarcado.

#### guia Configurações de classificação {#sort-settings-tab}

Na guia **Classificar configurações**, especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Marque todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Puxe para baixo para selecionar uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Puxe para baixo para selecionar uma das seguintes opções: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   O padrão é `All`.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Fórum Essentials](/help/communities/essentials-forum.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).

Para obter a tradução de tópicos e comentários postados, consulte [Traduzindo conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
