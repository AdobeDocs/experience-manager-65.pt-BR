---
title: Recurso de blog
seo-title: Blog Feature
description: Informações da comunidade em um formato de diário
seo-description: Community information in a journaling format
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
source-git-commit: fe731e1a8866fbdd1f982d67d6ff29cbf7f0cd7c
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 7%

---

# Recurso de blog {#blog-feature}

## Introdução {#introduction}

O recurso de blog do AEM Communities foi transformado de uma atividade de criação para uma verdadeira atividade da comunidade, que ocorre no ambiente de publicação.

O recurso de blog permite o fornecimento de informações da comunidade em um formato de registro no diário. Entradas de blog são feitas no ambiente de publicação por membros autorizados (usuários registrados e conectados).

O recurso de blog fornece :

* Criação do lado da publicação de artigos e comentários do blog
* Edição de rich text
* Imagens integradas (com suporte para arrastar e soltar)
* Conteúdo de rede social incorporado ([Suporte incorporado](/help/communities/blog-developer-basics.md#allowing-rich-media))
* Modo de rascunho
* Publicação agendada
* Compor em nome de (uma [membro privilegiado](/help/communities/users.md#privileged-members-group) pode criar conteúdo em nome de um membro da comunidade diferente)
* [Moderação em massa e no contexto](/help/communities/moderate-ugc.md) de artigos e comentários do blog

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

e arraste-os para o local em uma página onde o blog deve aparecer.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/blog-developer-basics.md#essentials-for-client-side) são incluídos, é assim que a variável `Blog` componente aparecerá:

![add-blog-component](assets/add-blog-component.png)

### Configuração de blog {#configuring-blog}

Selecione o colocado `Blog` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

![Configurações do blog](assets/blog-configure.png)

#### Guia Configurações {#settings-tab}

No **Configurações** especifique os recursos básicos do blog:

* **Permitir miniatura de anexo**

  Se marcada, uma miniatura da imagem anexada é criada.

* **Tamanho máximo da miniatura do anexo**

  Tamanho máximo (em pixels) da imagem em miniatura do anexo. O valor padrão é 800 x 800.

* **Tamanho mínimo de imagem para a miniatura**

  Tamanho mínimo (em bytes) da imagem para gerar a miniatura para imagens integradas. O valor padrão é 100000 bytes (100kb).

* **Tamanho máximo da miniatura**

  Tamanho máximo (em pixels) da imagem em miniatura para imagem integrada. O valor padrão é 800 x 800.

* **Permitir membros privilegiados**

  Se marcado, somente os membros Privilegiados poderão criar conteúdo.

* **Membros privilegiados permitidos**

  Adicione os membros privilegiados com permissão para criar conteúdo.

* **Bloquear conteúdo gerado pelo usuário no modo Edição do autor**

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

* **Moderada**

  Se marcado, a postagem de entradas de blog e comentários deve ser aprovada antes de serem exibidos em um site publicado. O padrão é desmarcado.

* **Fechado**

  Se marcado, o blog será fechado para novas entradas e comentários de blog. O padrão está desmarcado.

* **Editor de rich text**

  Se marcadas, as entradas de blog e os comentários podem ser inseridos com marcação. O padrão está marcado.

* **Permitir marcação**

  Se marcados, permitem que os membros adicionem rótulos de tag à sua publicação (consulte **Campo de tag** guia ). O padrão está desmarcado.

* **Permitir carregamento de arquivos**

  Se marcado, permite que anexos de arquivo sejam adicionados a uma entrada de blog ou comentário. O padrão está desmarcado.

* **Tamanho máximo do arquivo**

  Relevante apenas se `Allow File Uploads` está marcado. Esse campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

  Relevante apenas se `Allow File Uploads` está marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

  Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152 (2 Mb).

* **Permitir respostas**

  Se marcado, permite respostas aos comentários postados na entrada do blog. O padrão está desmarcado.

* **Permitir votação**

  Se marcado, inclui o recurso Votação com uma entrada de blog. O padrão está desmarcado.

* **Permitir que usuários excluam comentários e tópicos**

  Se marcados, permitem que os membros excluam os comentários e as entradas de blog postados. O padrão está desmarcado.

* **Permitir monitoramento**

  Se marcado, inclui o seguinte recurso para artigos de blog, que permite que membros sejam [notificado](/help/communities/notifications.md) de novos posts. O padrão está desmarcado.

* **Permitir assinaturas de email**

  Se marcado, permitir que os membros sejam notificados sobre novas publicações por email ([subscrição](/help/communities/subscriptions.md)). Exige `Allow Following` a ser verificado e [email configurado](/help/communities/email.md). O padrão está desmarcado.

* **Exibir selos**

  Se marcado, exibir ganho e atribuído [medalhas](/help/communities/implementing-scoring.md) com uma entrada de blog do membro. O padrão está desmarcado.

* **Não receber respostas na página de listagem**

* **Ativar conteúdo em destaque**

  Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

* **Ativar a menção**

  Se ativado, permite que os usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e marquem-nos usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

  Restringir o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

  Especifique a string do padrão permitido para marcar (@mention) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

#### Guia Moderação de usuário {#user-moderation-tab}

No **Moderação de usuário** especifique as configurações de moderação:

* **Negar postagens**

  Se marcados, os moderadores de membros confiáveis poderão negar postagens e impedir que a postagem apareça no fórum público. O padrão está desmarcado.

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

No **Campo de tag** especifique as tags que poderão ser aplicadas se **Permitir marcação** é verificar no **Configurações** Guia:

* **Namespaces permitidos**

  Relevante se `Allow Tagging` é verificado sob o **Configurações** guia. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

  Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. Um valor de -1 significa sem limites. O padrão é 0.

### Configurar a barra lateral do blog {#configuring-blog-sidebar}

Ao clicar duas vezes no ícone `Blog Sidebar` componente, uma caixa de diálogo de edição é aberta.

No **Configurações da barra lateral do diário** especifique o formato de data para os arquivos e o tipo de entradas a serem exibidas na barra lateral:

![barra lateral de componentes do blog](assets/blog-component-sidebar.png)

* **Formato de data**

  O formato usado para exibir arquivos de entradas de blog. O formato usa espaços reservados seguindo a convenção do Java.

   * aaaa : ano completo, como &#39;2015&#39;
   * aa : ano curto, como &quot;15&quot;
   * MMMM : mês inteiro, como junho
   * MMM : mês curto, como jun
   * MM : número do mês, como 06

  O padrão é &quot;yyyy MMMMM&quot;, que exibiria, por exemplo, &quot;junho de 2015&quot;

* **Visualizar tipo**

  O Título e o tipo das entradas do blog a serem exibidas na barra lateral. A escolha é entre

   * Autores
   * Categorias
   * Arquivos

* **Caminho do componente Blopg**

  *(Opcional)* A localização do recurso de blog do qual os artigos de blog devem ser listados. Se deixado em branco, usará o componente de resourceType `social/journal/components/hbs/journal` que aparece na mesma página.

   * Por exemplo, `/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **Limite sugerido**

  O número de artigos de blog a serem exibidos. Um valor de -1 significa sem limite. O padrão é -1.

## Experiência de visitante do site {#site-visitor-experience}

No ambiente de publicação, o recurso de blog exibirá o artigo de blog mais recente seguido de artigos de blog mais antigos em ordem decrescente de criação. As barras laterais de blog permitem que os visitantes do site apliquem filtros para limitar a seleção de artigos de blog exibidos.

O artigo do blog é seguido por um link para publicar ou exibir comentários.

Quando um artigo de blog é selecionado, o artigo de blog e os comentários são exibidos (se ativados).

Outras habilidades dependem se o visitante do site é moderador, administrador, membro da comunidade, membro privilegiado ou anônimo.

### Trabalhar com artigos {#working-with-articles}

Ao criar um novo artigo de blog, há a opção de:

1. Publicar imediatamente
1. Publicar um rascunho
1. Publicar em uma data e hora programadas

Os artigos do blog serão exibidos na guia apropriada (Publicado, Rascunhos ou Agendado) para os membros que podem ser autores em publicações.

#### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar [tarefas de moderação](/help/communities/moderate-ugc.md) (conforme permitido pela configuração do componente ) em todos os artigos e comentários de blog publicados em um blog.

![moderator-homepage](assets/moderator-homepage.png)

#### Membros {#members}

Quando o usuário conectado é um membro da comunidade ou [membro privilegiado](/help/communities/users.md#privileged-members-group) (dependendo da configuração), é possível selecionar `New Article` para criar e publicar um novo artigo de blog.

Especificamente, eles podem:

* Criar um novo artigo de blog
* Publicar um novo artigo de blog em nome de outro membro
* Publicar um comentário em um artigo do blog
* Editar seu próprio artigo de blog ou comentário
* Excluir seu próprio artigo de blog ou comentário
* Sinalizar artigos ou comentários de outras pessoas

![member-homepage](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados podem apenas ler artigos e comentários de blog publicados, traduzi-los se houver suporte, mas não podem adicionar um artigo ou comentário de blog nem sinalizar artigos ou comentários de outras pessoas.

![anonymous-user-view](assets/anonymous-user-view.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do blog](/help/communities/blog-developer-basics.md) página para desenvolvedores.

Para moderação de entradas e comentários do blog, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar entradas de blog e comentários, consulte [Marcação do conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).

Para tradução de entradas e comentários do blog, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
