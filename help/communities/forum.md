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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Recurso do fórum{#forum-feature}

## Introdução {#introduction}

O recurso de fórum fornece uma área para visitantes do site conectados (membros da comunidade) no ambiente de publicação para:

* criar novos tópicos
* exibir e responder tópicos
* seguir um tópico
* pesquisar um fórum
* ajudar a moderar o conteúdo do fórum
* mover tópicos do fórum de uma página para outra

Esta seção da documentação descreve

* adicionar o recurso do fórum a um site do AEM
* configurações do `Forum`componente

### Adding a Forum to a Page {#adding-a-forum-to-a-page}

Para adicionar um `Forum` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Forum`

e arraste-o para o lugar em uma página onde o fórum deve aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do cliente](/help/communities/essentials-forum.md#essentials-for-client-side) necessárias forem incluídas, o `Forum`componente aparecerá desta forma:

![chlimage_1-104](assets/chlimage_1-104.png)

### Configuração de um fórum {#configuring-a-forum}

Selecione o componente inserido a ser acessado e selecione o `Forum` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### Guia Configurações {#settings-tab}

Na **guia **Configurações **, especifique as configurações para tópicos e respostas:

* **Permitir miniatura de anexo**Se marcada, uma miniatura da imagem anexada é criada.
* **Tamanho** máximo da miniatura de anexação (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo da imagem para miniatura**
* **Tamanho** máximo da miniatura (em pixels) da imagem em miniatura para imagem em linha. O valor padrão é 800 x 800.

* **Tópicos por página**Define o número de tópicos/postagens exibidos por página. O padrão é 10.
* **Moderado** Se marcado, a publicação de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado** Se marcado, o fórum é fechado para novos tópicos e comentários. O padrão está desmarcado.

* **Editor** de Rich Text Se marcado, os tópicos e os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação** Se marcada, permita que os membros adicionem etiquetas à sua publicação (consulte a guia Campo **de** tag ). O padrão está desmarcado.

* **Permitir uploads** de arquivoSe marcada, permita que os anexos de arquivo sejam adicionados ao tópico ou ao comentário. O padrão está desmarcado.

* **Permitir seguidores** Se marcada, inclua o seguinte recurso para postagens do fórum, que permite que os membros sejam [notificados](/help/communities/notifications.md) de novas postagens. O padrão está desmarcado.

* **Permitir fixação** Se marcada, os tópicos do fórum podem ser fixados na parte superior da lista de tópicos. O padrão está desmarcado.

* **Permitir conteúdo** em destaque se marcado, a ideia pode ser identificada como conteúdo [em](/help/communities/featured.md)destaque. O padrão está desmarcado.

* **Permitir assinaturas** por email Se marcada, permitir que os membros sejam notificados de novas publicações por email ([assinatura](/help/communities/subscriptions.md)). Requer `Allow Following` a verificação e configuração [de](/help/communities/email.md)email. O padrão está desmarcado.

* **Tamanho** de arquivo máximo relevante somente se `Allow File Uploads` estiver marcado. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos** de arquivo permitidosRelevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivos com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que** **todos os tipos de arquivos são permitidos.

* **Tamanho** de arquivo de imagem de anexo máximo relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152** **(2 Mb).

* **Permitir respostas encadeadas** Se marcada, permita respostas a comentários postados no tópico. O padrão está desmarcado.

* **Permitir votação** Se marcada, inclua o recurso Votação com um tópico. O padrão está desmarcado.

* **Permitir que os usuários excluam comentários e tópicos** Se marcados, permita que os membros excluam os comentários e tópicos publicados. O padrão está desmarcado.

* **Mostrar navegações estruturais** Se marcada, mostrar navegações estruturais nas páginas de tópicos. O padrão está marcado.

* **Exibir emblemas** Se marcada, exibe [emblemas ganhados e atribuídos](/help/communities/implementing-scoring.md) com a entrada de blog de um membro. O padrão está desmarcado.

* **Permitir membros** privilegiados Se marcada, somente membros privilegiados poderão criar conteúdo.

* **Membros com privilégios permitidos**Adicione os membros com privilégios permitidos para criar conteúdo.
* **Bloquear conteúdo gerado pelo usuário no modo** de edição do autor Se ativado, bloqueia o conteúdo gerado pelo usuário durante a edição no modo de autor.

* **Ativar menção** Se ativada, permite que usuários da comunidade registrados identifiquem outros membros registrados (usando o nome, sobrenome, nome de usuário) e os rotulem usando a sintaxe @user-name comum. Os usuários marcados recebem notificações sobre suas menções.

* **Menções máximas** Restringe o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão** de menção da interface do usuárioEspecifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>Pode ser necessário verificar tanto `AllowThreaded Replies` quanto `Allow users to Delete Comments and Topics` para permitir comentários sobre um tópico.

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia **Moderação do usuário **, especifique como os tópicos e as respostas publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

* **Negar publicações** Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está desmarcado.

* **Fechar / Reabrir tópicos** Se marcados, os moderadores de membros confiáveis podem fechar um tópico para outras edições e comentários, e também podem reabrir um tópico. O padrão está desmarcado.

* **Mover tópicos** Se marcada, permita que os moderadores do lado da publicação movam tópicos. O padrão está marcado.

* **Sinalizar publicações** Se marcada, permita que os membros sinalizem os tópicos ou comentários de outras pessoas como inadequados. O padrão está desmarcado.

* **Sinalizar lista** de motivos Se marcada, permita que os membros escolham, em uma lista suspensa, o motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo** do sinalizador personalizado Se marcado, permita que os membros insiram seu próprio motivo para sinalizar um tópico ou comentário como inapropriado. O padrão está desmarcado.

* **Limite** de moderaçãoInsira o número de vezes que um tópico ou comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização** Digite o número de vezes que um tópico ou comentário deve ser sinalizado antes de ser ocultado da exibição pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia Campo **de** tag , as tags que podem ser aplicadas, se permitidas na guia **Settings **, são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos** Relevante se `Allow Tagging` estiver marcado na guia **Settings **tab. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace verificadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todos os namespaces são permitidos.

* **Limite de sugestão** Insira o número de tags a serem exibidas como uma sugestão para o membro postar no fórum. O padrão é **-**1 (sem limites).

#### Guia Tradução {#translation-tab}

Na guia **Tradução **s, se a tradução estiver ativada para o site da comunidade, a tradução pode ser definida para traduzir o tópico inteiro ou as publicações selecionadas.

* **Traduzir tudo** Se marcado, o thread do fórum será traduzido para o idioma preferido do usuário. O padrão está desmarcado.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **Configurações de classificação **s, especifique como os comentários publicados são classificados quando exibidos.

* **Classificar por** Marque todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Defina como Padrão** Puxe para baixo para selecionar uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecione Opções de tempo para** puxar para baixo a classificação do Analytics para selecionar uma das opções `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Fórum Essentials](/help/communities/essentials-forum.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.

Para obter a tradução de tópicos e comentários publicados, consulte [Traduzindo conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.
