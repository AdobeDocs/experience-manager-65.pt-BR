---
title: Recurso de calendário
seo-title: Recurso de calendário
description: Fornece informações de eventos da comunidade em um formato de calendário
seo-description: Fornece informações de eventos da comunidade em um formato de calendário
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Recurso de calendário{#calendar-feature}

## Introdução {#introduction}

O recurso de calendário oferece suporte ao fornecimento de informações de eventos da comunidade em um formato de calendário para todos os visitantes do site ou somente para visitantes do site que fizeram logon (membros da comunidade), enquanto apenas membros autorizados podem adicionar eventos.

Esta seção da documentação descreve

* adicionar o recurso de calendário a um site do AEM
* configurações para `Calendar`componentes

## Adding a Calendar to a Page {#adding-a-calendar-to-a-page}

Para adicionar um `Calendar` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Calendar`

e arraste-o para o lugar em uma página, como uma posição relativa ao recurso que os usuários devem revisar.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Calendar` componente será exibido.

![chlimage_1-147](assets/chlimage_1-147.png)

### Configurar calendário {#configuring-calendar}

Selecione o `Calendar`componente inserido a ser acessado e selecione o `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-148](assets/chlimage_1-148.png) ![chlimage_1-149](assets/chlimage_1-149.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações **s, especifique se as tags devem ou não ser aplicadas às entradas do calendário.

* **Eventos por página** Define o número de eventos exibidos por página. O padrão é 10.

* **Moderado** Se marcado, a publicação de eventos de calendário e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado** Se marcado, o calendário será fechado para novas entradas e comentários do evento. O padrão está desmarcado.

* **Editor** de Rich Text Se marcado, os eventos do calendário e os comentários podem ser inseridos com marcação. O padrão está marcado.

* **Permitir marcação** Se marcada, permita que os membros adicionem etiquetas aos eventos que publicam (consulte a guia Campo **de** tag ). O padrão está marcado.

* **Permitir uploads** de arquivoSe marcada, permita que os anexos de arquivo sejam adicionados a um evento de calendário ou comentário. O padrão está marcado.

* **Permitir seguidores** Se esta opção estiver marcada, permita que os membros sigam os eventos postados no calendário. O padrão está marcado.

* **Tamanho** de arquivo máximo relevante somente se `Allow File Uploads` estiver marcado. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos** de arquivo permitidosRelevante somente se `Allow File Uploads` estiver marcado. Uma lista separada por vírgulas de extensões de arquivos com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Tamanho** de arquivo de imagem de anexo máximo relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152** **(2 Mb).

* **Tipos** de imagem de capa permitidosUma lista separada por vírgulas de extensões de arquivos de imagem com o separador &quot;ponto&quot;. O padrão é `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respostas encadeadas** Se marcada, permita respostas a comentários postados no evento de calendário. O padrão está marcado.

* **Permitir que os usuários excluam comentários e eventos** Se marcados, permitirá que os membros excluam os comentários e os eventos de calendário que publicaram. O padrão está ** **marcado.

* **Permitir votação** Se marcada, inclua o recurso de votação com um evento de calendário. O padrão está marcado.

* **Mostrar navegações estruturais** Mostrar navegações estruturais na página do evento. O padrão está marcado.

* **Filtro** de intervalo de datasDefine o número de dias adicionados à data atual para calcular o valor &quot;Até&quot; do filtro de página de listagem de eventos do calendário. O número padrão é 30.

* **Permitir conteúdo** em destaque se marcado, a ideia pode ser identificada como conteúdo [em](/help/communities/featured.md)destaque. O padrão está desmarcado.

Na guia **Moderação do usuário **, especifique como os tópicos e as respostas publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

#### Guia Moderação do usuário {#user-moderation-tab}

* **Negar publicações** Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está marcado.

* **Fechar / Reabrir eventos** Se marcados, os moderadores de membros confiáveis podem fechar um evento para outras edições e comentários, e também podem reabrir um evento. O padrão está marcado.

* **Sinalizar publicações** Se marcada, permita que os membros sinalizem os eventos ou comentários de outras pessoas como inadequados. O padrão está marcado**.**

* **Sinalizar lista** de motivos Se marcada, permita que os membros escolham, em uma lista suspensa, o motivo para sinalizar um evento ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo** de sinalização personalizado Se marcado, permita que os membros insiram seu próprio motivo para marcar um evento ou comentário como inapropriado. O padrão está desmarcado**.**

* **Limite** de moderaçãoInsira o número de vezes que um evento ou comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização** Digite o número de vezes que um evento ou comentário deve ser sinalizado antes de ser ocultado da exibição pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia Campo **de** tag , as tags que podem ser aplicadas, se permitidas na guia **Settings **, são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos** Relevante se `Allow Tagging` estiver marcado na guia **Settings **tab. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace verificadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todos os namespaces são permitidos.

* **Limite de sugestão** Insira o número de tags a serem exibidas como uma sugestão para o membro postar no fórum. O padrão é **-**1 (sem limites).

>[!NOTE]
>
>Visite [Administrando tags](/help/sites-administering/tags.md) para saber como adicionar um novo namespace de tag (taxonomia).

#### Guia Tradução {#translation-tab}

Na guia **Tradução **s, se a tradução estiver ativada para o site da comunidade, a tradução pode ser definida para traduzir o thread inteiro (evento e comentários) em vez de postagens específicas.

* **Traduzir tudo** Se marcado, o evento e os comentários serão traduzidos para o idioma preferencial do usuário. O padrão está marcado.

## Experiência do visitante do site {#site-visitor-experience}

No ambiente de publicação, o recurso de calendário exibirá um campo de pesquisa com um intervalo de datas padrão e quaisquer eventos de calendário que se encaixem nesse intervalo.

Quando um evento de calendário é selecionado, os detalhes, a descrição e os comentários do evento de calendário são exibidos.

Outras capacidades dependem de o visitante do site ser um moderador, administrador, membro da comunidade, membro privilegiado ou anônimo.

### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar tarefas [de](/help/communities/moderate-ugc.md) moderação (conforme permitido pela configuração do componente) em todos os eventos de calendário e comentários postados em um evento.

![chlimage_1-150](assets/chlimage_1-150.png)

#### Membros {#members}

Quando o usuário conectado é membro da comunidade ou membro [](/help/communities/users.md#privileged-members-group) privilegiado (dependendo da configuração), ele pode optar por `New Event` criar e publicar um novo evento de calendário.

Especificamente, podem

* criar um novo evento de calendário
* publicar um comentário em um evento de calendário
* editar seu próprio evento de calendário ou comentário
* excluir seus próprios eventos de calendário ou comentários
* sinalizar eventos ou comentários de calendário de outras pessoas

![chlimage_1-151](assets/chlimage_1-151.png) ![chlimage_1-152](assets/chlimage_1-152.png)

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados só podem ler eventos de calendário publicados, traduzi-los se houver suporte, mas não podem adicionar eventos ou comentários nem sinalizar eventos ou comentários de outras pessoas.

![chlimage_1-153](assets/chlimage_1-153.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desenvolvedores.

Para moderação de eventos e comentários do calendário, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar eventos de calendário e comentários, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.

Para obter a tradução de eventos de calendário e comentários, consulte [Traduzindo conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.
