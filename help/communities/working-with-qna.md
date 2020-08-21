---
title: Recurso do fórum de perguntas e respostas
seo-title: Recurso do fórum de perguntas e respostas
description: Adicionar o recurso de fórum QnA a uma página
seo-description: Adicionar o recurso de fórum QnA a uma página
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 9%

---


# Recurso do fórum de perguntas e respostas{#q-a-forum-feature}

## Introdução {#introduction}

O recurso de fórum QnA (perguntas e respostas) fornece uma área para que os membros da comunidade façam e respondam perguntas. Permite que os membros:

* Criar novas perguntas
* Adicionar imagens em linha (com suporte para arrastar e soltar)
* Visualização e perguntas de resposta
* Procurar uma pergunta
* Ajuda a moderar o conteúdo QnA
* Identificar as melhores respostas
* Mover perguntas QnA de uma página para outra

A documentação descreve:

* Adicionar o recurso de fórum QnA a um site AEM.
* Configurações do `QnA`componente.

## Adicionar um fórum de P&amp;R a uma página {#adding-a-q-a-forum-to-a-page}

Para adicionar um `QnA` componente a uma página no modo de autor, use o navegador de componentes para localizá-lo `Communities / QnA` e arrastá-lo para o local em uma página onde o fórum QnA deve aparecer.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/qna-essentials.md#essentials-for-client-side) necessárias forem incluídas, é assim que o `QnA` componente aparece:

![qna-component](assets/qna-component.png)

### Configuração de QnA {#configuring-qna}

Selecione o componente inserido a ser acessado e selecione o `QnA` `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

![qna-config](assets/qna-config.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações** , especifique as configurações para tópicos (perguntas) e respostas (respostas):

* **Permitir miniatura de anexo**

   Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

   Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo de imagem para a miniatura**

   Tamanho mínimo (em bytes) da imagem para gerar miniatura de imagens em linha. O valor padrão é 100000 bytes (100 kb).

* **Tamanho máximo da miniatura**

   Tamanho máximo (em pixels) da imagem em miniatura para imagem em linha. O valor padrão é 800 x 800.

* **Tópicos por página**

   Define o número de perguntas/postagens exibidas por página. O padrão é 10.

* **Moderada**

   Se marcada, a publicação de tópicos e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcada, o fórum é fechado a novas perguntas e comentários. O padrão está desmarcado.

* **Editor de Rich Text**

   Se marcada, os tópicos e os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Permitir marcação**

   Se marcada, permita que os membros adicionem etiquetas à sua postagem (consulte a guia Campo **de** tag). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que os anexos do arquivo sejam adicionados à pergunta ou ao comentário. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para postagens do fórum, que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novas postagens. O padrão está desmarcado.

* **Permitir fixação**

   Se marcada, os tópicos do fórum podem ser fixados na parte superior da lista de tópicos. O padrão está desmarcado.

* **Permitir assinaturas de email**

   Se marcada, permita que os membros sejam notificados de novas postagens por email ([subscrição](/help/communities/subscriptions.md)). Requer que Permitir seguidores seja marcado e o [email seja configurado](/help/communities/email.md). O padrão está desmarcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` for verificada. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` for verificada. Uma lista separada por vírgulas de extensões de arquivos com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que** **todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. O número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

   Se marcada, permita respostas a comentários postados na pergunta. O padrão está desmarcado.

* **Permitir votação**

   Se marcada, inclua o recurso Voto com uma pergunta. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

   Se marcada, permita que os membros excluam os comentários e as perguntas que publicaram. O padrão está desmarcado.

* **Permitir membros privilegiados**

   Se marcada, somente membros privilegiados poderão criar conteúdo.

* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**

   Se ativado, bloqueia o Conteúdo gerado pelo usuário durante a edição no Modo de autor.

* **Mover a resposta selecionada para cima**

   Se marcada, a primeira resposta mostrada é uma resposta selecionada. O padrão está desmarcado.
* **Exibir selos**

   Se marcada, exiba [crachás](/help/communities/implementing-scoring.md) ganhados e atribuídos com a entrada de blog de um membro. O padrão está desmarcado.

* **Ativar conteúdo em destaque**

   se marcada, a ideia pode ser identificada como conteúdo [em](/help/communities/featured.md)destaque. O padrão está desmarcado.

* **Ativar a menção**

   Se ativada, permite que os usuários da comunidade registrados identifiquem outros membros registrados (usando o nome, sobrenome, nome de usuário) e os rotulem usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restrinja o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia Moderação **do** usuário, especifique como os tópicos publicados (perguntas) e as respostas (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

* **Negar respostas**

   Se marcada, os moderadores de membros confiáveis podem negar as respostas publicadas e impedir que elas apareçam no fórum público de perguntas e respostas. O padrão está desmarcado.

* **Fechar/Reabrir tópicos**

   Se marcada, os moderadores de membros confiáveis podem fechar uma pergunta (tópico) para outras edições e respostas e também reabrir uma pergunta. O padrão está desmarcado.

* **Mover tópicos** Se marcada, permita que os moderadores do lado da publicação movam perguntas. O padrão está desmarcado.

* **Sinalizar postagens**

   Se marcada, permita que os membros sinalizem perguntas ou respostas de outras pessoas como inadequadas. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, seu motivo para sinalizar uma pergunta ou resposta como inadequada. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros digitem seu próprio motivo para sinalizar uma pergunta ou resposta como inadequada. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que uma pergunta ou resposta deve ser sinalizada pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

   Insira o número de vezes que uma pergunta ou resposta deve ser sinalizada antes de ser ocultada da visualização pública. Se definido como -1, a pergunta ou resposta sinalizada nunca será ocultada da visualização pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia Campo **de** tag , as tags que podem ser aplicadas, se permitidas na guia **Configurações** , são limitadas de acordo com as namespaces escolhidas.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` estiver marcado na guia **Configurações** . As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace verificadas. A lista do namespace inclui &quot;Tags padrão&quot; (a namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todas as namespaces são permitidas.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como uma sugestão para o membro postando no fórum. Um valor de **-**1 significa sem limites. O padrão é 0.

#### Guia Configurações de classificação {#sort-settings-tab}

Na guia **Classificar configurações** , especifique como os comentários publicados são classificados quando exibidos.

* **Ordenar por**

   Marque todas as seleções de classificação permitidas: `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. O padrão é `Newest, Oldest, Last Updated`.

* **Definir como padrão**

   Puxe para baixo para selecionar uma das opções de classificação marcadas para aparecer como padrão. O padrão é `Newest`.

* **Selecionar as opções de tempo para a classificação do Analytics**

   Solte para selecionar um dos `All, Last 24 Hours, Last 7 Days, Last 30 Days`. O padrão é `All`.

## Experiência com o Visitante do site {#site-visitor-experience}

### Como identificar respostas {#identifying-answers}

Uma resposta pode ser marcada como uma resposta correta ou útil usando o `Select Answer` botão. Quando uma pergunta é marcada como Respondida, outra resposta não pode ser selecionada até que a primeira seja desmarcada usando o `Unmark Chosen Answer` botão.

Depois de selecionada como uma resposta viável, ela pode ser desmarcada usando o `Unmark Chosen Answer` botão.

Depois que uma resposta é selecionada como resposta viável, uma indicação de que a pergunta foi `Answered` exibida ao lado do tópico da pergunta na página principal de QnA.

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar as tarefas de moderação permitidas pela configuração do componente, independentemente de quem criou a pergunta ou resposta.

Eles também podem identificar respostas.

#### Membros {#members}

Quando os visitantes do site estiverem conectados, dependendo da configuração, eles poderão:

* Publique uma nova pergunta.
* Edite ou exclua perguntas que eles criaram.
* Sinalizar perguntas ou respostas de outros membros.
* Identifique as respostas para as perguntas que eles criaram.

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados só podem ler perguntas e respostas publicadas, traduzi-las se houver suporte, mas não podem adicionar perguntas nem respostas, nem sinalizar publicações de outras pessoas.

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [do QnA Essentials](/help/communities/qna-essentials.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.
