---
title: Recurso de calendário
seo-title: Recurso de calendário
description: Fornece informações de evento da comunidade em um formato de calendário
seo-description: Fornece informações de evento da comunidade em um formato de calendário
uuid: 262f6afa-d8aa-4815-8440-a8ed5668c76d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 70fa0b9c-cb98-45c4-9c94-bef4a9f3741e
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 7%

---


# Recurso de calendário {#calendar-feature}

## Introdução {#introduction}

O recurso de calendário oferece suporte ao fornecimento de informações de evento da comunidade em um formato de calendário para todos os visitantes do site ou somente para visitantes do site conectados (membros da comunidade), enquanto somente os membros autorizados podem adicionar eventos.

Esta seção da documentação descreve

* Adicionar o recurso de calendário a um site AEM
* Configurações para `Calendar` componentes

## Adding a Calendar to a Page {#adding-a-calendar-to-a-page}

Para adicionar um `Calendar` componente a uma página no modo de autor, use o navegador de componentes para localizar

* `Communities / Calendar`

e arraste-o para o lugar em uma página, como uma posição relativa ao recurso que os usuários devem revisar.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/calendar-basics-for-developers.md#essentials-for-client-side) necessárias forem incluídas, será assim que o `Calendar` componente será exibido.

![componente de calendário](assets/calendar-component.png)

### Configuração do calendário {#configuring-calendar}

Selecione o componente inserido a ser acessado e selecione o `Calendar` `Configure` ícone que abre a caixa de diálogo de edição.

![configure](assets/configure-new.png)

![configure-calendário](assets/configure-calendar1.png)

#### Guia Configurações {#settings-tab}

Na guia **Configurações** , especifique se as tags devem ou não ser aplicadas às entradas do calendário.

* **Eventos por página**

   Define o número de eventos exibidos por página. O padrão é 10.

* **Moderada**

   Se marcada, a publicação de eventos de calendário e comentários deve ser aprovada antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Fechado**

   Se marcada, o calendário é fechado às novas entradas e comentários do evento. O padrão está desmarcado.

* **Editor de Rich Text**

   Se marcada, eventos de calendário e comentários podem ser inseridos com marcação. O padrão está marcado.

* **Permitir marcação**

   Se marcada, permita que os membros adicionem etiquetas às eventos que publicaram (consulte a guia Campo **** de etiqueta). O padrão está marcado.

* **Permitir carregamento de arquivos**

   Se marcada, permita que os anexos de arquivo sejam adicionados a um evento de calendário ou comentário. O padrão está marcado.

* **Permitir monitoramento**

   Se marcada, permita que os membros sigam eventos postados no calendário. O padrão está marcado.

* **Tamanho máximo do arquivo**

   Relevante apenas se `Allow File Uploads` for verificada. Este campo limitará o tamanho (em bytes) de um arquivo carregado. O padrão é 104857600 (10 Mb).

* **Tipos de arquivos permitidos**

   Relevante apenas se `Allow File Uploads` for verificada. Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, o upload dos não especificados não será permitido. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Tamanho máximo do arquivo de imagem a ser anexado**

   Relevante somente se a opção Permitir uploads de arquivo estiver marcada. Número máximo de bytes que um arquivo de imagem carregado pode ter. O padrão é 2097152** **(2 Mb).

* **Tipos de imagem de capa permitidos**

   Uma lista separada por vírgulas de extensões de arquivos de imagem com o separador &quot;ponto&quot;. O padrão é `.jpg,.jpeg,.png,.gif,.bmp`.

* **Permitir respostas encadeadas**

   Se marcada, permita respostas a comentários postados no evento do calendário. O padrão está marcado.

* **Permitir que usuários excluam comentários e eventos**

   Se marcada, permita que os membros excluam os comentários e eventos de calendário publicados. O padrão está ** **marcado.

* **Permitir votação**

   Se marcada, inclua o recurso Voto com um evento de calendário. O padrão está marcado.

* **Mostrar navegações estruturais**

   Mostrar navegações estruturais na página do evento. O padrão está marcado.

* **Filtro do intervalo de datas**

   Define o número de dias adicionados à data atual para calcular o valor &quot;Até&quot; do filtro da página de listagem de eventos do calendário. O número padrão é 30.

* **Ativar conteúdo em destaque**

   Se marcada, a ideia pode ser identificada como conteúdo [em](/help/communities/featured.md)destaque. O padrão está desmarcado.

Na guia Moderação **do** usuário, especifique como os tópicos e as respostas publicados (conteúdo gerado pelo usuário) são gerenciados. Para obter mais informações, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

#### Guia Moderação do usuário {#user-moderation-tab}

* **Negar postagens**

   Se marcada, os moderadores de membros confiáveis poderão negar publicações e impedir que a publicação apareça no fórum público. O padrão está marcado.

* **Fechar / Reabrir eventos**

   Se marcada, os moderadores de membros confiáveis podem fechar um evento para outras edições e comentários, e também podem reabrir um evento. O padrão está marcado.

* **Sinalizar postagens**

   Se marcada, permita que os membros sinalizem eventos ou comentários de outras pessoas como inadequados. O padrão está marcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os membros escolham, em uma lista suspensa, seu motivo para sinalizar um evento ou comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os membros insiram seu próprio motivo para sinalizar um evento ou comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um evento ou comentário deve ser sinalizado pelos membros antes que os moderadores sejam notificados. O padrão é 1 (uma vez).

* **Limite de sinalização**

   Insira o número de vezes que um evento ou comentário deve ser sinalizado antes de ser ocultado da visualização pública. Se definido como -1, o tópico ou comentário sinalizado nunca será ocultado da visualização pública. Caso contrário, esse número deve ser maior ou igual ao Limite de moderação. O padrão é 5.

#### Guia Campo de tag {#tag-field-tab}

Na guia Campo **de** tag , as tags que podem ser aplicadas, se permitidas na guia **Configurações** , são limitadas de acordo com as namespaces escolhidas.

* **Espaços de nomes permitidos**

   Relevante se `Allow Tagging` estiver marcado na guia **Configurações** . As marcas que podem ser aplicadas são limitadas às da categoria verificada. A lista do namespace inclui &quot;Tags padrão&quot; (a namespace padrão) e &quot;Incluir todas as tags&quot;. O padrão não está marcado, o que significa que todas as namespaces são permitidas.

* **Limite sugerido**

   Insira o número de tags a serem exibidas como uma sugestão para o membro postando no fórum. O padrão é **-**1 (sem limites).

>[!NOTE]
>
>Visite [Administrando tags](/help/sites-administering/tags.md) para saber como adicionar uma nova namespace de tag (taxonomia).

#### Guia Tradução {#translation-tab}

Na guia **Tradução** , se a tradução estiver ativada para o site da comunidade, a tradução pode ser definida para traduzir o thread inteiro (evento e comentários) em vez de postagens específicas.

* **Converter tudo**

   Se marcada, o evento e os comentários são traduzidos para o idioma preferencial do usuário. O padrão está marcado.

## Experiência com o Visitante do site {#site-visitor-experience}

No ambiente de publicação, o recurso de calendário exibirá um campo de pesquisa com um intervalo de datas padrão e qualquer evento de calendário que se enquadre nesse intervalo.

Quando um evento de calendário é selecionado, os detalhes, a descrição e os comentários do evento do calendário são exibidos.

Outras capacidades dependem de o visitante do site ser um moderador, administrador, membro da comunidade, membro privilegiado ou anônimo.

### Moderadores e administradores {#moderators-and-administrators}

Quando o usuário conectado tem privilégios de moderador ou administrador, ele pode executar tarefas [de](/help/communities/moderate-ugc.md) moderação (conforme permitido pela configuração do componente) em todos os eventos de calendário e comentários postados em um evento.

![moderadores-visualização](assets/moderators-view.png)

#### Membros {#members}

Quando o usuário conectado é membro da comunidade ou membro [](/help/communities/users.md#privileged-members-group) privilegiado (dependendo da configuração), ele pode optar por `New Event` criar e publicar um novo evento de calendário.

Concretamente, podem:

* Criar um novo evento de calendário
* Publicar um comentário em um evento de calendário
* Editar seu próprio evento de calendário ou comentário
* Excluir seus próprios eventos de calendário ou comentários
* Sinalizar eventos ou comentários do calendário de outras pessoas

![create-evento](assets/configure-calendar2.png)

![evento-post](assets/configure-calendar3.png)

#### Anônimo {#anonymous}

Os visitantes do site que não estão conectados só podem ler eventos do calendário publicados, traduzi-los se houver suporte, mas não podem adicionar eventos ou comentários nem sinalizar eventos ou comentários de outras pessoas.

![anonimato-usuário-visualização](assets/anonymous-user-view1.png)

## Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [Calendar Essentials](/help/communities/calendar-basics-for-developers.md) para desenvolvedores.

Para moderação de eventos de calendário e comentários, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar eventos de calendário e comentários, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.

Para obter a tradução de eventos de calendário e comentários, consulte [Traduzindo conteúdo](/help/communities/translate-ugc.md)gerado pelo usuário.
