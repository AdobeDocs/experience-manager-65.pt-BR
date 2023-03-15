---
title: Recurso da biblioteca de arquivos
seo-title: File Library Feature
description: O recurso Biblioteca de arquivos permite que visitantes do site que fizeram logon façam upload, gerenciem e baixem arquivos
seo-description: The File Library feature lets signed-in site visitors upload, manage, and download files
uuid: e78a90bd-f1d3-44f8-98eb-1498a55e8217
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: ea2b23af-49c3-409b-a041-43c42d846f21
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 9%

---

# Recurso da biblioteca de arquivos{#file-library-feature}

## Introdução {#introduction}

O recurso biblioteca de arquivos fornece um local para visitantes do site com logon (membros da comunidade) fazerem upload, gerenciamento e download de arquivos no site da comunidade.

Esta seção da documentação descreve:

* Adicionar o recurso da biblioteca de arquivos a um site AEM.
* Configurações para o `File Library` componente.

### Adicionar uma biblioteca de arquivos a uma página {#adding-a-file-library-to-a-page}

Para adicionar uma `File Library` para uma página no modo de criação, localize o componente:

* `Communities / File Library`

e arraste-a para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes do Communities](/help/communities/basics.md).

Quando a variável [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-file-library.md#essentials-for-client-side) são incluídos, é assim que a variável `File Library` componente será exibido:

![file-library1](assets/file-library1.png)

### Configuração da biblioteca de arquivos {#configuring-file-library}

Selecione o `File Library` para acessar e selecionar o `Configure` ícone que abre a caixa de diálogo de edição.

![configure-new](assets/configure-new.png)

![file-library2](assets/file-library2.png)

#### Guia Comentários {#comments-tab}

Em **Comentários** , especifique se e como os comentários dos arquivos carregados são exibidos:

* **Permitir comentários em arquivos**

   Se marcada, permita comentários em arquivos carregados. O padrão está desmarcado.

* **Comentários por página**

   Limita o número de comentários exibidos por página, bem como o número de respostas exibidas. O padrão é **10º**.

* **Tamanho máximo do arquivo**

   Esse valor limitará o tamanho do arquivo carregado. O limite padrão é 104857600 (10 Mb).

* **Comprimento máximo da mensagem de**

   Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4096 caracteres.

* **Tipos de arquivos permitidos**

   Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo : .jpg, .jpeg, .png, .doc, .docx, .pdf. Se qualquer tipo de arquivo for especificado, os não especificados não serão permitidos. O padrão não é especificado de modo que todos os tipos de arquivo sejam permitidos.

* **Editor de rich text**

   Se marcada, os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, os usuários poderão excluir seus próprios comentários. O padrão está marcado.

* **Permitir marcação**

   Se marcada, a capacidade de adicionar uma tag ao arquivo será ativada. O padrão está desmarcado.

* **Espaços de nomes permitidos**

   Se a opção Permitir marcação estiver marcada, as tags disponíveis serão limitadas aos namespaces marcados. Se nenhum estiver marcado, então todos são permitidos. O padrão é todos os namespaces.

* **Limite sugerido**

   Se a opção Permitir marcação estiver marcada, essa configuração limitará o número de tags sugeridas a serem exibidas. Se definido como -1, não há limite. O padrão é -1.

* **Permitir votação**

   Se marcada, a capacidade de votar em um arquivo será ativada. O padrão está desmarcado.

* **Permitir monitoramento**

   Se marcada, inclua o seguinte recurso para artigos do blog, que permite que os membros sejam [notificado](/help/communities/notifications.md) de novos posts. O padrão está desmarcado.

* **Ativar a menção**

   Se estiver habilitado, o permite que usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e os marque usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Quantidade máxima de menções**

   Restrinja o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de menção da interface do usuário**

   Especifique a string de padrão permitida para marcar (@menção) o usuário registrado em uma publicação. Por exemplo ~{{familyName}}{{givenName}}.

* **Permitir respostas encadeadas**

   Se marcada, permita respostas para comentários postados. O padrão está desmarcado.

#### Guia Moderação do usuário {#user-moderation-tab}

Em **Moderação do usuário** , configure a moderação de comentários, se os comentários forem permitidos:

* **Pré-moderação**

   Se marcada, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

   Se marcada, o visitante que postou o comentário tem a capacidade de excluí-lo. O padrão está marcado.

* **Negar comentários**

   Se marcada, permita que os moderadores de membros confiáveis neguem comentários. O padrão está desmarcado.

* **Fechar/Reabrir comentários**

   Se marcada, permita que os moderadores de membros confiáveis fechem e reabram comentários. O padrão está desmarcado.

* **Sinalizar comentários**

   Se marcada, permita que os visitantes sinalizem comentários como inadequados. O padrão está desmarcado.

* **Sinalizar lista de motivo**

   Se marcada, permita que os visitantes escolham, em uma lista suspensa, o motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado de sinalização**

   Se marcada, permita que os visitantes insiram seu próprio motivo para marcar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

   Insira o número de vezes que um comentário deve ser sinalizado por visitantes antes de os moderadores serem notificados. O padrão é uma vez (**1**).

* **Limite de sinalização**

   Insira o número de vezes que um comentário deve ser sinalizado antes de ser oculto da exibição pública. Esse número deve ser maior ou igual a **Limite de moderação**. O padrão é 5.

### Guia Configurações de classificação {#sort-settings-tab}

Ordenar por

Definir como padrão

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas no [Fundamentos da biblioteca de arquivos](/help/communities/essentials-file-library.md) página para desenvolvedores.

Para obter moderação de tópicos e comentários publicados, consulte [Moderação de conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários publicados, consulte [Marcação de conteúdo gerado pelo usuário](/help/communities/tag-ugc.md).
