---
title: Recurso de blog
description: Saiba como o recurso de blog permite o fornecimento de informações da comunidade em um formato de registro no diário. As entradas são feitas no ambiente Publish por usuários autorizados.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 0%

---

# Recurso de blog {#blog-feature}

## Introdução {#introduction}

O recurso de blog do AEM Communities foi transformado de uma atividade de criação para uma verdadeira atividade de comunidade, que ocorre no ambiente do Publish.

O recurso de blog permite o fornecimento de informações da comunidade em um formato de registro no diário. Entradas de blog são feitas no ambiente do Publish por membros autorizados (usuários registrados e conectados).

O recurso de blog fornece :

* Criação de artigos e comentários no Publish
* Edição de rich text
* Imagens integradas (com suporte para arrastar e soltar)
* Conteúdo de rede social inserido ([oSuporte incorporado](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modo de rascunho
* Publicação agendada
* Compor em nome (um [membro privilegiado](/help/communities/users.md#privileged-members-group) pode criar conteúdo em nome de um membro da comunidade diferente)
* [Moderação em massa e em contexto](/help/communities/moderate-ugc.md) de artigos e comentários do blog

Esta seção da documentação descreve:

* Adicionar o recurso de blog a um site AEM
* Configurações para componentes de blog

>[!NOTE]
>
>Os componentes `Journal` e `Journal Sidebar` são denominados `Blog` e `Blog Sidebar`.
>
>O recurso de blog encontrado no AEM 6.0 e em versões anteriores foi removido. Ele era baseado em um modelo e só permitia que os autores criassem conteúdo no ambiente de criação.

## Adicionar componentes do blog a uma página {#adding-blog-components-to-a-page}

Se desejar adicionar um blog a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Blog`
* `Communities / Blog Sidebar`

E arraste-os para o lugar em uma página onde o blog deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/blog-developer-basics.md#essentials-for-client-side) são incluídas, o componente `Blog` aparece da seguinte forma:

![adicionar-componente-blog](assets/add-blog-component.png)

### Configuração de blog {#configuring-blog}

Selecione o componente `Blog` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

![Configurações do blog](assets/blog-configure.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações**, especifique os recursos básicos do blog:

* **Permitir miniatura do anexo**

  Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

  Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo da imagem para a miniatura**

  Tamanho mínimo (em bytes) da imagem para gerar a miniatura para imagens integradas. O valor padrão é 100.000 bytes (100 kb).

* **Tamanho Máximo da Miniatura**

  Tamanho máximo (em pixels) da imagem em miniatura para imagem integrada. O valor padrão é 800 x 800.

* **Permitir membros privilegiados**

  Se marcado, somente os membros Privilegiados poderão criar conteúdo.

* **Membros Privilegiados Permitidos**

  Adicione os membros privilegiados com permissão para criar conteúdo.

* **Bloquear Conteúdo Gerado pelo Usuário no Modo de Edição do Autor**

  Se estiver ativado, bloqueia o conteúdo gerado pelo usuário ao editar no Modo Autor.

* **Título do diário**

  O título do blog a ser exibido na página.

>[!NOTE]
>
>O Título do diário é usado para criar automaticamente o URL para o blog.
>
>No máximo 50 caracteres (com 5 caracteres adicionais para exclusividade) são usados do título do diário especificado aqui para criar o URL do blog.

* **Descrição do diário**

  A descrição do blog.

* **Tópicos por página**

  Define o número de entradas/comentários do blog exibidos por página. O padrão é 10.

* **Moderado**

  Se marcados, a postagem de entradas de blog e comentários deve ser aprovada antes de serem exibidos em um site publicado. O padrão é desmarcado.

* **Fechado**

  Se marcado, o blog será fechado para novas entradas e comentários de blog. O padrão está desmarcado.

* **Editor de Rich Text**

  Se marcadas, as entradas de blog e os comentários podem ser inseridos com marcação. O padrão está marcado.

* **Permitir marcação**

  Se marcado, permite que os membros adicionem rótulos de marca às suas publicações (consulte a guia **Campo de marca**). O padrão está desmarcado.

* **Permitir Carregamentos de Arquivos**

  Se marcado, permite que anexos de arquivo sejam adicionados a uma entrada de blog ou comentário. O padrão está desmarcado.

* **Tamanho máx. do arquivo**

  Relevante somente se `Allow File Uploads` estiver marcado. Este campo limita o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

  Relevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os tipos de arquivo não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máx. do arquivo de imagem a ser anexado**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

  Se marcado, permite respostas aos comentários postados na entrada do blog. O padrão está desmarcado.

* **Permitir votação**

  Se marcado, inclui o recurso Votação com uma entrada de blog. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

  Se marcado, permite que os membros excluam os comentários e as entradas de blog que postaram. O padrão está desmarcado.

* **Permitir acompanhamento**

  Se marcado, inclui o seguinte recurso para artigos de blog, o que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novos posts. O padrão está desmarcado.

* **Permitir assinaturas por email**

  Se marcado, permitirá que os membros sejam notificados sobre novas postagens por email ([assinatura](/help/communities/subscriptions.md)). Exige que `Allow Following` seja verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Exibir selos**

  Se marcado, exibe [medalhas](/help/communities/implementing-scoring.md) obtidas e atribuídas com uma entrada de blog do membro. O padrão está desmarcado.

* **Não Obter Respostas na Página de Listagem**

* **Permitir conteúdo em destaque**

  Se marcada, a ideia é identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Habilitar menção**

  Se ativado, permite que os usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e marquem-nos usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas próprias menções.

* **Máximo de menções**

  Restringir o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de Menção da Interface do Usuário**

  Especifique a string do padrão permitido para marcar (@mention) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

#### Guia Moderação de usuário {#user-moderation-tab}

Na guia **Moderação de Usuário**, especifique as configurações de moderação:

* **Negar postagens**

  Se marcados, os moderadores de membros confiáveis têm permissão para negar postagens e impedir que elas apareçam no fórum público. O padrão está desmarcado.

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

Na guia **Campo de marca**, especifique quais marcas poderão ser aplicadas se **Permitir marcação** estiver marcado na guia **Configurações**:

* **Namespaces permitidos**

  Relevante se `Allow Tagging` estiver marcado na guia **Configurações**. As tags que podem ser aplicadas estão limitadas às tags nas categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

  Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. Um valor de -1 significa sem limites. O padrão é 0.

### Configurar a barra lateral do blog {#configuring-blog-sidebar}

Ao clicar duas vezes no componente `Blog Sidebar`, uma caixa de diálogo de edição é aberta.

Na guia **Configurações da Barra Lateral do Diário**, especifique o formato de data para os arquivos mortos e o tipo de entradas a serem exibidas na barra lateral:

![barra lateral de componentes do blog](assets/blog-component-sidebar.png)

* **Formato de data**

  O formato usado para exibir arquivos de entradas de blog. O formato usa espaços reservados seguindo a convenção do Java™.

   * aaaa : ano completo, como &#39;2015&#39;
   * aa : ano curto, como &quot;15&quot;
   * MMMM : mês inteiro, como junho
   * MMM : mês curto, como jun
   * MM : número do mês, como 06

  O padrão é &quot;yyyy MMMMM&quot;, que exibiria, por exemplo, &quot;junho de 2015&quot;

* **Exibir Tipo**

  O Título e o tipo das entradas do blog a serem exibidas na barra lateral. A escolha é entre

   * Autores
   * Categorias
   * Arquivos

* **Caminho do componente de blog**

  *(Opcional)* O local do recurso de blog do qual os artigos de blog devem ser listados. Se deixado em branco, ele usará o componente de resourceType `social/journal/components/hbs/journal` que aparece na mesma página.

   * Por exemplo, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite sugerido**

  O número de artigos de blog a serem exibidos. Um valor de -1 significa sem limite. O padrão é -1.

## Experiência de visitante do site {#site-visitor-experience}

No ambiente de publicação, o recurso de blog exibe o artigo de blog mais recente seguido de artigos de blog mais antigos em ordem decrescente de criação. As barras laterais de blog permitem que os visitantes do site apliquem filtros para limitar a seleção de artigos de blog exibidos.

O artigo do blog é seguido por um link para publicar ou exibir comentários.

Quando um artigo de blog é selecionado, o artigo de blog e os comentários são exibidos (se ativados).

Outras habilidades dependem se o visitante do site é moderador, administrador, membro da comunidade, membro privilegiado ou anônimo.

### Trabalhar com artigos {#working-with-articles}

Ao criar um artigo de blog, existe a opção de fazer o seguinte:

1. Publish imediatamente
1. Publish um rascunho
1. Publish em uma data e hora programadas

Os artigos do blog aparecem na guia apropriada (Publicado, Rascunhos ou Agendado) para membros que podem ser autores em publicações.

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar [tarefas de moderação](/help/communities/moderate-ugc.md) (conforme permitido pela configuração do componente) em todos os artigos e comentários postados em um blog.

![página-inicial-moderador](assets/moderator-homepage.png)

#### Membros {#members}

Quando o usuário conectado é um membro da comunidade ou [membro privilegiado](/help/communities/users.md#privileged-members-group) (dependendo da configuração), ele pode selecionar `New Article` para criar e postar um novo artigo de blog.

Especificamente, eles podem:

* Criar um artigo de blog
* Post um novo artigo de blog em nome de outro membro
* Post um comentário para um artigo de blog
* Editar seu próprio artigo de blog ou comentário
* Excluir seu próprio artigo de blog ou comentário
* Sinalizar artigos ou comentários de outras pessoas

![página-inicial-membro](assets/member-homepage.png)

![criar-blog](assets/create-blog.png)

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados podem apenas ler artigos e comentários de blog publicados, traduzi-los se houver suporte, mas não podem adicionar um artigo ou comentário de blog nem sinalizar artigos ou comentários de outras pessoas.

![visualização-usuário-anônimo](assets/anonymous-user-view.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Blog Essentials](/help/communities/blog-developer-basics.md) para desenvolvedores.

Para obter a moderação de entradas e comentários do blog, consulte [Moderando conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar entradas de blog e comentários, consulte [Marcando Conteúdo Gerado pelo Usuário](/help/communities/tag-ugc.md).

Para tradução de entradas e comentários do blog, consulte [Tradução de Conteúdo Gerado pelo Usuário](/help/communities/translate-ugc.md).
