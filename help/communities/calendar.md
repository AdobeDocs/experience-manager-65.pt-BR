---
title: Recurso de calendário
seo-title: Calendar Feature
description: Fornece informações sobre o evento da comunidade em um formato de calendário
seo-description: Provides community event information in a calendar format
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
exl-id: c9b34b00-525d-4ca3-bd18-11bb7ce66787
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 7%

---

# Recurso de calendário {#calendar-feature}

## Introdução {#introduction}

O recurso de calendário oferece informações sobre o evento da comunidade em um formato de calendário para todos os visitantes do site ou apenas para visitantes conectados do site (membros da comunidade), enquanto somente membros autorizados podem adicionar eventos.

Esta seção da documentação descreve

* Adicionar o recurso de calendário a um site AEM
* Definições de configuração para `Calendar` componentes

## Adicionar um calendário a uma página {#adding-a-calendar-to-a-page}

Para adicionar um `Calendar` para uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Calendar`

e arraste-o para o local em uma página, como uma posição relativa ao recurso para que os usuários analisem.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) são incluídos, é assim que a variável `Calendar` será exibido.

![calendar-component](assets/calendar-component.png)

### Configurar calendário {#configuring-calendar}

Selecione o colocado `Calendar` para acessar e selecionar a variável `Configure` ícone que abre a caixa de diálogo de edição.

![configurar](assets/configure-new.png)

![configure-calendar](assets/configure-calendar1.png)

#### Guia Configurações {#settings-tab}

No **Configurações** especifique se permite ou não a aplicação de tags às entradas do calendário.

* **Eventos por página**

   Define o número de eventos exibidos por página. O padrão é 10.

* **Moderada**

   Se marcados, a postagem de eventos de calendário e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcado, o calendário será fechado para novas entradas de evento e comentários. O padrão está desmarcado.

* **Editor de rich text**

   Se marcados, os eventos de calendário e os comentários podem ser inseridos com marcação. O padrão está marcado.

* **Permitir marcação**

   Se marcado, permite que os membros adicionem rótulos de tag aos eventos publicados (consulte **Campo de tag** guia ). O padrão está marcado.

* **Permitir carregamento de arquivos**

   Se marcado, permite que anexos de arquivo sejam adicionados a um evento de calendário ou comentário. O padrão está marcado.

* **Permitir monitoramento**

   Se marcado, permite que os membros sigam os eventos publicados no calendário. O padrão está marcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` está marcado. Esse campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` está marcado. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não poderão ser carregados. O padrão é nenhum especificado, de modo que todos os tipos de arquivos são permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

   Relevante somente se Permitir uploads de arquivo estiver marcado. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152** ** (2 Mb).

* **Tipos de imagem de capa permitidos**

   Uma lista separada por vírgulas de extensões de arquivos de imagem com o separador &quot;ponto&quot;. O padrão é `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respostas encadeadas**

   Se marcado, permite respostas aos comentários postados no evento de calendário. O padrão está marcado.

* **Permitir que usuários excluam comentários e eventos**

   Se marcados, permitem que os membros excluam os comentários e eventos de calendário publicados. O padrão é** **marcado.

* **Permitir votação**

   Se marcado, inclui o recurso Votação com um evento de calendário. O padrão está marcado.

* **Mostrar navegações estruturais**

   Mostrar navegações estruturais na página do evento. O padrão está marcado.

* **Filtro do intervalo de datas**

   Define o número de dias adicionados à data atual para calcular o valor &quot;Para&quot; do filtro de página da listagem de eventos do calendário. O número padrão é 30.

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como [conteúdo em destaque](/help/communities/featured.md). O padrão está desmarcado.

No **Moderação de usuário** especifique como os tópicos publicados e as respostas (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

#### Guia Moderação de usuário {#user-moderation-tab}

* **Negar postagens**

   Se marcados, os moderadores de membros confiáveis poderão negar postagens e impedir que a postagem apareça no fórum público. O padrão está marcado.

* **Fechar / Reabrir eventos**

   Se marcados, os moderadores de membros confiáveis podem fechar um evento para outras edições e comentários, e também podem reabrir um evento. O padrão está marcado.

* **Sinalizar postagens**

   Se marcado, permite que os membros sinalizem eventos ou comentários de outras pessoas como inadequados. O padrão está marcado.

* **Sinalizar lista de motivo**

   Se marcado, permitirá que os membros escolham, em uma lista suspensa, o motivo para sinalizar um evento ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcado, permite que os membros insiram seu próprio motivo para sinalizar um evento ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um evento ou comentário deve ser marcado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

   Insira o número de vezes que um evento ou comentário deve ser sinalizado antes de ser ocultado da visualização pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da exibição pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

No **Campo de tag** guia, as tags que podem ser aplicadas, se permitido na guia **Configurações** são limitadas de acordo com os namespaces escolhidos.

* **Namespaces permitidos**

   Relevante se `Allow Tagging` é verificado sob o **Configurações** guia. As tags que podem ser aplicadas são limitadas àquelas dentro das categorias de namespace marcadas. A lista de namespaces inclui &quot;Tags padrão&quot; (o namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão é nenhum marcado, o que significa que todos os namespaces são permitidos.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como sugestão para a publicação do membro no fórum. O padrão é **-**1 (sem limites).

>[!NOTE]
>
>Visita [Administração de tags](/help/sites-administering/tags.md) para saber como adicionar um novo namespace de tag (taxonomia).

#### Guia Tradução {#translation-tab}

No **Tradução** se a tradução estiver ativada para o site da comunidade, a tradução pode ser definida para traduzir toda a thread (evento e comentários) em vez de publicações específicas.

* **Converter tudo**

   Se marcados, o evento e os comentários serão traduzidos para o idioma preferencial do usuário. O padrão está marcado.

## Experiência de visitante do site {#site-visitor-experience}

No ambiente de publicação, o recurso de calendário exibirá um campo de pesquisa com um intervalo de datas padrão e quaisquer eventos de calendário que estejam dentro desse intervalo.

Quando um evento de calendário é selecionado, os detalhes, a descrição e os comentários do evento de calendário são exibidos.

Outras habilidades dependem se o visitante do site é moderador, administrador, membro da comunidade, membro privilegiado ou anônimo.

### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar [tarefas de moderação](/help/communities/moderate-ugc.md) (conforme permitido pela configuração do componente) em todos os eventos de calendário e comentários publicados em um evento.

![visualização de moderadores](assets/moderators-view.png)

#### Membros {#members}

Quando o usuário conectado é um membro da comunidade ou [membro privilegiado](/help/communities/users.md#privileged-members-group) (dependendo da configuração), é possível selecionar `New Event` para criar e publicar um novo evento de calendário.

Especificamente, eles podem:

* Criar um novo evento de calendário
* Publicar um comentário em um evento de calendário
* Editar seu próprio evento de calendário ou comentário
* Excluir seu próprio evento de calendário ou comentário
* Sinalizar eventos ou comentários do calendário de outras pessoas

![create-event](assets/configure-calendar2.png)

![event-post](assets/configure-calendar3.png)

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados podem ler apenas os eventos de calendário publicados e traduzi-los, se houver suporte, mas não podem adicionar um evento ou comentário, nem sinalizar eventos ou comentários de outras pessoas.

![anonymous-user-view](assets/anonymous-user-view1.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos do calendário](/help/communities/calendar-basics-for-developers.md) página para desenvolvedores.

Para moderação de eventos e comentários do calendário, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar eventos e comentários do calendário, consulte [Marcação do conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).

Para tradução de eventos e comentários do calendário, consulte [Tradução de conteúdo gerado pelo usuário](/help/communities/translate-ugc.md).
