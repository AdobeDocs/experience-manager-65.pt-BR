---
title: Recurso Biblioteca de arquivos
seo-title: Recurso Biblioteca de arquivos
description: O recurso Biblioteca de arquivos permite que visitantes do site com logon façam upload, gerenciem e baixem arquivos
seo-description: O recurso Biblioteca de arquivos permite que visitantes do site com logon façam upload, gerenciem e baixem arquivos
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# Recurso Biblioteca de arquivos{#file-library-feature}

## Introdução {#introduction}

O recurso de biblioteca de arquivos fornece um local para visitantes do site com logon (membros da comunidade) carregarem, gerenciarem e baixarem arquivos no site da comunidade.

Esta seção da documentação descreve:

* Adicionar o recurso da biblioteca de arquivos a um site do AEM.
* Configurações do `File Library` componente.

### Adicionar uma biblioteca de arquivos a uma página {#adding-a-file-library-to-a-page}

Para adicionar um `File Library` componente a uma página no modo de autor, localize o componente

* `Communities / File Library`

e arraste-o para o lugar em uma página.

Para obter as informações necessárias, visite Noções básicas sobre componentes [das comunidades](/help/communities/basics.md).

Quando as bibliotecas [do lado do cliente](/help/communities/essentials-file-library.md#essentials-for-client-side) necessárias forem incluídas, o `File Library` componente será exibido desta forma:

![chlimage_1-145](assets/chlimage_1-145.png)

### Configuração da biblioteca de arquivos {#configuring-file-library}

Selecione o componente inserido a ser acessado e selecione o `File Library` `Configure` ícone que abre a caixa de diálogo de edição.

![chlimage_1-146](assets/chlimage_1-146.png) ![forum-config-1](assets/forum-config-1.png)

#### Guia Comentários {#comments-tab}

Na guia **Comentários** , especifique se e como os comentários dos arquivos carregados serão exibidos:

* **Permitir comentários em arquivos**

   Se marcada, permita comentários em arquivos carregados. O padrão está desmarcado.

* **Comentários por página**

   Limita o número de comentários exibidos por página, bem como o número de respostas exibidas. O padrão é **10**.

* **Tamanho máximo do arquivo**

   Esse valor limitará o tamanho do arquivo carregado. O limite padrão é 104857600 (10 Mb).

* **Comprimento máximo da mensagem de**

   Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4096 caracteres.

* **Tipos de arquivos permitidos**

   Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo: .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão não é especificado de modo que todos os tipos de arquivos sejam permitidos.

* **Editor de Rich Text**

   Se marcada, os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, os usuários podem excluir seus próprios comentários. O padrão está marcado.

* **Permitir marcação**

   Se marcada, a capacidade de adicionar uma tag ao arquivo será ativada. O padrão está desmarcado.

* **Espaços de nomes permitidos**

   Se a opção Permitir marcação estiver marcada, as tags disponíveis serão limitadas às namespaces verificadas. Se nenhum estiver marcado, então todos são permitidos. O padrão é todas as namespaces.

* **Limite sugerido**

   Se a opção Permitir marcação estiver marcada, essa configuração limitará o número de tags sugeridas a serem exibidas. Se definido como -1, não há limite. O padrão é -1.

* **Permitir votação**

   Se marcada, a capacidade de votar em um arquivo será ativada. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para artigos de blog, que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novas publicações. O padrão está desmarcado.

* **Ativar a menção**

   Se ativada, permite que os usuários da comunidade registrados identifiquem outros membros registrados (usando o nome, sobrenome, nome de usuário) e os rotulem usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restrinja o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo, ~{{familyName}}{{specifiedName}}.

* **Permitir respostas encadeadas**

   Se marcada, permita respostas para comentários postados. O padrão está desmarcado.

#### Guia Moderação do usuário {#user-moderation-tab}

Na guia Moderação **do** usuário, configure a moderação de comentários, se forem permitidos comentários:

* **Pré-moderação**

   Se marcada, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, o visitante que postou o comentário terá a capacidade de excluí-lo. O padrão está marcado.

* **Negar comentários**

   Se marcada, permita que os moderadores de membros confiáveis neguem comentários. O padrão está desmarcado.

* **Fechar/Reabrir comentários**

   Se marcada, permita que os moderadores de membros confiáveis fechem e reabram comentários. O padrão está desmarcado.

* **Sinalizar comentários**

   Se marcada, permita que os visitantes sinalizem comentários como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os visitantes escolham, em uma lista suspensa, seu motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os visitantes insiram seu próprio motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um comentário deve ser sinalizado por visitantes antes que os moderadores sejam notificados. O padrão é uma vez (**1**).

* **Limite de sinalização**

   Insira o número de vezes que um comentário deve ser sinalizado antes de ser ocultado da visualização pública. Esse número deve ser maior ou igual ao Limite de **moderação**. O padrão é 5.

### Guia Configurações de classificação {#sort-settings-tab}

Ordenar por

Definir como padrão

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [File Library Essentials](/help/communities/essentials-file-library.md) para desenvolvedores.

Para moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo](/help/communities/moderate-ugc.md)gerado pelo usuário.

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo](/help/communities/tag-ugc.md)gerado pelo usuário.
