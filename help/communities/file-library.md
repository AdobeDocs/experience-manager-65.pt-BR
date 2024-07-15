---
title: Recurso Biblioteca de Arquivos
description: O recurso Biblioteca de arquivos permite que visitantes do site conectados façam upload, gerenciem e baixem arquivos.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 05cfaab5-a12d-475f-9095-a9fb13571d0a
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 1%

---

# Recurso Biblioteca de Arquivos{#file-library-feature}

## Introdução {#introduction}

O recurso de biblioteca de arquivos fornece um local para visitantes conectados do site (membros da comunidade) fazerem upload, gerenciarem e baixarem arquivos no site da comunidade.

Esta seção da documentação descreve:

* Adicionando o recurso de biblioteca de arquivos a um site AEM.
* Definições de configuração para o componente `File Library`.

### Adicionar uma biblioteca de arquivos a uma página {#adding-a-file-library-to-a-page}

Para adicionar um componente `File Library` a uma página no modo de autor, localize o componente:

* `Communities / File Library`

E arraste-o para o local em uma página.

Para obter as informações necessárias, visite [Noções básicas sobre componentes das comunidades](/help/communities/basics.md).

Quando as [bibliotecas obrigatórias do lado do cliente](/help/communities/essentials-file-library.md#essentials-for-client-side) são incluídas, é assim que o componente `File Library` aparece:

![biblioteca-de-arquivos1](assets/file-library1.png)

### Configuração da biblioteca de arquivos {#configuring-file-library}

Selecione o componente `File Library` inserido para que você possa acessar e selecionar o ícone `Configure` que abre a caixa de diálogo de edição.

![configurar-novo](assets/configure-new.png)

![biblioteca-de-arquivos2](assets/file-library2.png)

#### Guia Comentários {#comments-tab}

Na guia **Comentários**, especifique se e como os comentários dos arquivos carregados serão exibidos:

* **Permitir comentários nos arquivos**

  Se marcado, permite comentários nos arquivos carregados. O padrão está desmarcado.

* **Comentários por página**

  Limita o número de comentários exibidos por página e o número de respostas exibidas. O padrão é **10**.

* **Tamanho máx. do arquivo**

  Esse valor limita o tamanho do arquivo carregado. O limite padrão é 104857600 (10 MB).

* **Comprimento Máximo da Mensagem**

  Número máximo de caracteres que podem ser inseridos na caixa de texto. O padrão é 4.096 caracteres.

* **Tipos de arquivos permitidos**

  Uma lista separada por vírgulas de extensões de arquivo com o separador &quot;ponto&quot;. Por exemplo, .jpg, .jpeg, .png, .doc, .docx, .pdf. Se algum tipo de arquivo for especificado, os tipos de arquivo não especificados não serão permitidos. O padrão não é especificado, de modo que todos os tipos de arquivos sejam permitidos.

* **Editor de Rich Text**

  Se marcados, os comentários podem ser inseridos com marcação. O padrão está desmarcado.

* **Excluir comentários**

  Se marcado, os usuários poderão excluir seus próprios comentários. O padrão está marcado.

* **Permitir marcação**

  Se essa opção estiver marcada, a capacidade de adicionar uma tag ao arquivo será ativada. O padrão está desmarcado.

* **Namespaces permitidos**

  Se Permitir marcação estiver marcado, as tags disponíveis serão limitadas aos namespaces marcados. Se nenhum namespace for marcado, todos serão permitidos. O padrão é todos os namespaces.

* **Limite sugerido**

  Se Permitir marcação estiver marcada, essa configuração limita o número de tags sugeridas para exibição. Se definido como -1, não há limite. O padrão é -1.

* **Permitir votação**

  Se marcado, a capacidade de votar em um arquivo será ativada. O padrão está desmarcado.

* **Permitir acompanhamento**

  Se marcado, inclui o seguinte recurso para artigos de blog, o que permite que os membros sejam [notificados](/help/communities/notifications.md) sobre novos posts. O padrão está desmarcado.

* **Habilitar menção**

  Se ativado, permite que os usuários registrados da comunidade identifiquem outros membros registrados (usando nome, sobrenome, nome de usuário) e marquem-nos usando a sintaxe comum @user-name. Os usuários marcados recebem notificações sobre suas menções.

* **Máximo de menções**

  Restringir o número máximo de menções permitidas em uma publicação. O padrão é 10.

* **Padrão de Menção da Interface do Usuário**

  Especifique a cadeia de caracteres do padrão permitido para marcar (@mention) o usuário registrado em uma publicação. Por exemplo, `~{{familyName}}{{givenName}}`.

* **Permitir respostas encadeadas**

  Se marcado, permite respostas aos comentários postados. O padrão está desmarcado.

#### Guia Moderação de usuário {#user-moderation-tab}

Na guia **Moderação de Usuário**, configure a moderação de comentários, se comentários forem permitidos:

* **Pré-moderação**

  Se marcados, os comentários devem ser aprovados antes de serem exibidos em um site de publicação. O padrão está desmarcado.

* **Excluir comentários**

  Se marcado, o visitante que postou o comentário poderá excluí-lo, se desejado. O padrão está marcado.

* **Negar comentários**

  Se marcado, permitir que os moderadores de membros confiáveis neguem comentários. O padrão está desmarcado.

* **Fechar/Reabrir Comentários**

  Se essa opção estiver marcada, permitir que os moderadores de membros confiáveis fechem e reabram comentários. O padrão está desmarcado.

* **Sinalizar comentários**

  Se marcado, permite que os visitantes sinalizem comentários como inadequados. O padrão está desmarcado.

* **Lista de motivos da sinalização**

  Se marcado, permite que os visitantes escolham, em uma lista suspensa, o motivo para sinalizar um comentário como inapropriado. O padrão está desmarcado.

* **Motivo personalizado do sinalizador**

  Se marcado, permite que os visitantes insiram seu próprio motivo para sinalizar um comentário como inapropriado. O padrão está desmarcado.

* **Limite de moderação**

  Insira o número de vezes que um comentário deve ser marcado pelos visitantes antes que os moderadores sejam notificados. O padrão é uma vez (**1**).

* **Limite de Sinalização**

  Insira o número de vezes que um comentário deve ser sinalizado antes de ser ocultado da visualização pública. Este número deve ser maior ou igual ao **Limite de moderação**. O padrão é 5.

### Guia Configurações de classificação {#sort-settings-tab}

Classificar por

Definir como padrão

### Informações adicionais {#additional-information}

Mais informações podem ser encontradas na página [File Library Essentials](/help/communities/essentials-file-library.md) para desenvolvedores.

Para obter a moderação de tópicos e comentários publicados, consulte [Moderando conteúdo gerado pelo usuário](/help/communities/moderate-ugc.md).

Para marcar tópicos e comentários postados, consulte [Marcação de Conteúdo Gerado pelo Usuário](/help/communities/tag-ugc.md).
