---
title: Configuração de desfazer para edição de página
seo-title: Configuring Undo for Page Editing
description: Saiba como configurar o suporte de Desfazer para edição de página no AEM.
seo-description: Learn how to configure Undo support for page editing in AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Configuração de desfazer para edição de página{#configuring-undo-for-page-editing}

O [Serviço OSGi](/help/sites-deploying/configuring-osgi.md)  **Configuração de desfazer do Day CQ WCM** ( `com.day.cq.wcm.undo.UndoConfigService`) expõe várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas.

## Configuração padrão {#default-configuration}

Em uma instalação padrão, as configurações padrão são definidas como propriedades na variável `sling:OsgiConfig`nó:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Este nó contém `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist` para as outras propriedades, os padrões são assumidos.

>[!CAUTION]
>
>Você ***must*** não altere nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo da variável `/libs` O é substituído na próxima vez que você atualizar sua instância (e pode ser substituído quando você aplicar um hotfix ou pacote de recursos).

## Configuração de Desfazer e Refazer {#configuring-undo-and-redo}

Você pode configurar essas propriedades do serviço OSGi para sua própria instância.

>[!NOTE]
>
>Ao trabalhar com AEM, existem vários métodos de gestão das definições de configuração para esses serviços; see [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A seguir são listadas as propriedades exibidas no console da Web, seguido do nome do parâmetro OSGi correspondente, juntamente com uma descrição e o valor padrão (quando apropriado):

* **Ativar**
( 
`cq.wcm.undo.enabled`)

   * **Descrição**: Determina se os autores da página podem desfazer e refazer as alterações.
   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Caminho**
( 
`cq.wcm.undo.path`)

   * **Descrição**: O caminho do repositório para dados binários de desfazer persistentes. Quando os autores alteram dados binários, como imagens, a versão original dos dados é mantida aqui. Quando as alterações nos dados binários são desfeitas, esses dados binários de desfazer são restaurados à página.
   * **Padrão**: `/var/undo`
   * **Tipo**: `String`

   >[!NOTE]
   >
   >Por padrão, somente os administradores podem acessar o `/var/undo` nó . Os autores podem realizar operações de desfazer e refazer no conteúdo binário somente após receber permissões para acessar os dados binários de desfazer.

* **Mínimo. validade**
( 
`cq.wcm.undo.validity`)

   * **Descrição**: O tempo mínimo em que os dados binários de desfazer são armazenados, em horas. Após esse período, os dados binários ficam disponíveis para exclusão, para conservar espaço em disco.
   * **Padrão**: `10`
   * **Tipo**: `Integer`

* **Etapas**
( 
`cq.wcm.undo.steps`)

   * **Descrição**: O número máximo de ações de página que são armazenadas no histórico de desfazer.
   * **Padrão**: `20`
   * **Tipo**: `Integer`

* **Persistência**
( 
`cq.wcm.undo.persistence`)

   * **Descrição**: A classe que persiste no histórico de desfazer. Duas classes de persistência são fornecidas:

      * `CQ.undo.persistence.WindowNamePersistence`: Persiste o histórico usando a propriedade window.name .
      * `CQ.undo.persistence.CookiePersistance`: Persiste o histórico usando cookies.
   * **Padrão**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`


* **Modo de persistência**
( 
`cq.wcm.undo.persistence.mode`)

   * **Descrição**: Determina quando o histórico do comando desfazer é mantido. Selecione essa opção para continuar a desfazer o histórico após cada edição de página. Limpe essa opção para persistir somente quando ocorrer um recarregamento de página (por exemplo, o usuário navega para uma página diferente).

      O histórico de desfazer persistente usa recursos do navegador da Web. Se o navegador dos usuários reagir lentamente às edições de página, tente persistir no histórico de desfazer os recarregamentos de página.

   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Modo de marcador**
( 
`cq.wcm.undo.markermode`)

   * **Descrição**: Especifica a dica visual a ser usada para indicar quais parágrafos são afetados quando ocorre uma ação de desfazer ou refazer. Os seguintes valores são válidos:

      * flash: O indicador de seleção dos parágrafos pisca temporariamente.
      * selecione: O parágrafo é selecionado.
   * **Padrão**: `flash`
   * **Tipo**: `String`


* **Bons componentes**
( 
`cq.wcm.undo.whitelist`)

   * **Descrição**: Uma lista de componentes que você deseja afetar pelos comandos desfazer e refazer. Adicione caminhos de componentes a essa lista quando funcionarem corretamente com desfazer/refazer. Anexe um asterisco (&amp;ast;) para especificar um grupo de componentes:

      * O valor a seguir especifica o componente de texto de base:

         `foundation/components/text`

      * O valor a seguir especifica todos os componentes de base:

         `foundation/components/*`
   * Quando a opção desfazer ou refazer for emitida para um componente que não esteja nessa lista, será exibida uma mensagem indicando que o comando pode não ser confiável.

   * **Padrão**: A propriedade é preenchida com muitos componentes que AEM fornece.
   * **Tipo**: `String[]`


* **Componentes ruins**
( 
`cq.wcm.undo.blacklist`)

   * **Descrição**: Uma lista de componentes e/ou operações de componentes que você não deseja que sejam afetados pelo comando desfazer. Adicione componentes e operações de componentes que não se comportam corretamente com o comando desfazer:

      * Adicione um caminho de componente quando desejar que nenhuma das operações do componente no histórico de desfazer, por exemplo `collab/forum/components/post`
      * Anexe um sinal de dois pontos (:) e uma operação ao caminho quando desejar que a operação específica seja omitida do histórico de desfazer (outras operações funcionam corretamente), por exemplo `collab/forum/components/post:insertParagraph.`

   >[!NOTE]
   >
   >Quando uma operação está nessa lista, ela ainda é adicionada ao histórico de desfazer. Os usuários não podem desfazer operações que existem anteriormente a um **Componente inválido** no histórico de desfazer.

   * Nomes de operação típicos são os seguintes:

      * `insertParagraph`: O componente é adicionado à página.
      * `removeParagraph`: O componente é excluído.
      * `moveParagraph`: O parágrafo é movido para um local diferente.
      * `updateParagraph`: As propriedades do parágrafo são alteradas.
   * **Padrão**: A propriedade é preenchida com várias operações de componente.
   * **Tipo**: `String[]`
