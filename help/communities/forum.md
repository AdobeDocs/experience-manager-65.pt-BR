---
title: Recurso de fórum
seo-title: Forum Feature
description: Como adicionar e configurar o recurso de fórum
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

# Recurso de fórum{#forum-feature}

## Introdução {#introduction}

O recurso de fórum fornece uma área para visitantes conectados do site (membros da comunidade) no ambiente de publicação para:

* Criar novos tópicos
* Exibir e responder a tópicos
* Seguir um tópico
* Pesquisar um fórum
* Ajude a moderar o conteúdo do fórum
* Mover tópicos do fórum de uma página para outra

Esta seção da documentação descreve:

* Adicionando o recurso de fórum a um site AEM.
* Definições de configuração para o `Forum` componente.

### Adicionando um fórum a uma página {#adding-a-forum-to-a-page}

Para adicionar um `Forum` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Forum`

e arraste-o para o local em uma página onde o fórum deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-forum.md#essentials-for-client-side) são incluídos, é assim que a variável `Forum` componente aparecerá:

![forum-component](assets/forum-component.png)

### Configurar um fórum {#configuring-a-forum}

Selecione o colocado `Forum` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![forum-config](assets/forum-config.png)

#### Guia Configurações {#settings-tab}

No **Configurações** especifique as configurações para tópicos e respostas:

* **Permitir miniatura de anexo**

   Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

   Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo de imagem para a miniatura**
* **Tamanho máximo da miniatura**

   Tamanho máximo (em pixels) da imagem em miniatura para imagem integrada. O valor padrão é 800 x 800.

* **Tópicos por página**

   Define o número de tópicos/postagens exibidos por página. O padrão é 10.

* **Moderada**

   Se marcados, a postagem de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcado, o fórum será fechado para novos tópicos e comentários. O padrão está desmarcado.

* **Editor de rich text**

   Se marcados, os tópicos e comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

   Se marcados, permitem que os membros adicionem rótulos de tag à sua publicação (consulte **Campo de tag** guia ). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcado, permite que anexos de arquivo sejam adicionados ao tópico ou comentário. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcado, inclui o seguinte recurso para publicações do fórum, o que permite que os membros sejam [notificado](/help/communities/notifications.md) de novos posts. O padrão está desmarcado.

* **Permitir fixação**

   Se marcados, os tópicos do fórum poderão ser fixados no topo da lista de tópicos. O padrão está desmarcado.

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcado, permitir que os membros sejam notificados sobre novas publicações por email ([subscrição](/help/communities/subscriptions.md)). Exige `Allow Following` a ser verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` está marcado. Esse campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` está marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**
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

   Se marcado, exibir ganho e atribuído [medalhas](/help/communities/implementing-scoring.md) com uma entrada de blog do membro. O padrão está desmarcado.

* **Permitir membros privilegiados**

   Se marcado, somente os membros Privilegiados poderão criar conteúdo.

* **Membros privilegiados permitidos**

   Adicione os membros privilegiados com permissão para criar conteúdo.

* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**

   Se estiver ativado, bloqueia o conteúdo gerado pelo usuário ao editar no Modo Autor.

* **Ativar a menção**

   Se ativado, permite que os usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e marquem-nos usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restringir o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string padrão permitida para marcar (@mention) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Pode ser necessário verificar `AllowThreaded Replies` e `Allow users to Delete Comments and Topics` para ativar comentários em um tópico.

#### Guia Moderação de usuário {#user-moderation-tab}

No **Moderação de usuário** especifique como os tópicos publicados e as respostas (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

* **Negar postagens**

   Se marcados, os moderadores de membros confiáveis poderão negar postagens e impedir que a postagem apareça no fórum público. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

   Se marcados, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Mover tópicos**

   Se marcado, permitir que os moderadores de publicação movam tópicos. O padrão está marcado.

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

No **Campo de tag** guia, as tags que podem ser aplicadas, se permitido na guia **Configurações** são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos**

   Relevante se `Allow Tagging` é verificado sob o **Configurações** guia. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. O padrão é **-**1 (sem limites).

#### Guia Tradução {#translation-tab}

No **Tradução** , se a tradução estiver ativada para o site da comunidade, a tradução poderá ser definida para traduzir todo o tópico ou as publicações selecionadas.

* **Converter tudo**

   Se marcado, o thread do fórum será traduzido para o idioma preferencial do usuário. O padrão está desmarcado.

#### Guia Configurações de classificação {#sort-settings-tab}

No **Configurações de classificação** especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Verificar todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Selecione uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Puxe para baixo para selecionar uma das seguintes opções: `All, Last 24 Hours, Last 7 Days, Last 30 Days`.

   O padrão é `All`.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do fórum](/help/communities/essentials-forum.md) página para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação do conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).

Para tradução de tópicos e comentários publicados, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
