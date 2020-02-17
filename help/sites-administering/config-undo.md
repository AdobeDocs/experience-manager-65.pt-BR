---
title: Configuração do comando Desfazer para edição de página
seo-title: Configuração do comando Desfazer para edição de página
description: Saiba como configurar o suporte de Desfazer para edição de página no AEM.
seo-description: Saiba como configurar o suporte de Desfazer para edição de página no AEM.
uuid: e5a49587-a2a6-41d5-b449-f7a8f7e4cee6
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 3cc7efc5-bcb2-41c9-b78b-308f6b7a298e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuração do comando Desfazer para edição de página{#configuring-undo-for-page-editing}

A Configuração [de Desfazer do CQ WCM do serviço](/help/sites-deploying/configuring-osgi.md) OSGi **Day CQ (** `com.day.cq.wcm.undo.UndoConfigService`) expõe várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas.

## Configuração padrão {#default-configuration}

Em uma instalação padrão, as configurações padrão são definidas como propriedades no `sling:OsgiConfig`nó:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Esse nó contém `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist` propriedades, para as outras propriedades os padrões são assumidos.

>[!CAUTION]
>
>Você não ***deve*** alterar nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo do é substituído na próxima vez que você atualizar sua instância (e pode muito bem ser substituído quando você aplicar uma correção ou um pacote de recursos). `/libs`

## Configuração de Desfazer e Refazer {#configuring-undo-and-redo}

Você pode configurar essas propriedades do serviço OSGi para sua própria instância.

>[!NOTE]
>
>When working with AEM there are several methods of managing the configuration settings for such services; see [Configuring OSGi](/help/sites-deploying/configuring-osgi.md) for more details and the recommended practices.

A seguir, são mostradas as propriedades como exibidas no console da Web, seguidas do nome do parâmetro OSGi correspondente, juntamente com uma descrição e o valor padrão (se for o caso):

* **Enable**( `cq.wcm.undo.enabled`)

   * **Descrição**: Determina se os autores de página podem desfazer e refazer alterações.
   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Caminho**
( `cq.wcm.undo.path`)

   * **Descrição**: O caminho do repositório para dados binários de desfazer persistentes. Quando os autores alteram dados binários, como imagens, a versão original dos dados é mantida aqui. Quando as alterações nos dados binários são desfeitas, esses dados binários desfeitos são restaurados para a página.
   * **Padrão**: `/var/undo`
   * **Tipo**: `String`
   >[!NOTE]
   >
   >Por padrão, somente os administradores podem acessar o `/var/undo` nó. Os autores podem realizar operações de desfazer e refazer no conteúdo binário somente depois de terem permissão para acessar os dados binários de desfazer.

* **Mínimo. valid**( `cq.wcm.undo.validity`)

   * **Descrição**: A quantidade mínima de tempo que os dados binários de desfazer são armazenados, em horas. Após esse período, os dados binários estão disponíveis para exclusão, para conservar espaço em disco.
   * **Padrão**: `10`
   * **Tipo**: `Integer`

* **Etapas**( `cq.wcm.undo.steps`)

   * **Descrição**: O número máximo de ações de página armazenadas no histórico de desfazer.
   * **Padrão**: `20`
   * **Tipo**: `Integer`

* **Persistência**( `cq.wcm.undo.persistence`)

   * **Descrição**: A classe que persiste no histórico de desfazer. Duas classes de persistência são fornecidas:

      * `CQ.undo.persistence.WindowNamePersistence`: Persiste no histórico usando a propriedade window.name.
      * `CQ.undo.persistence.CookiePersistance`: Persiste no histórico usando cookies.
   * **Padrão**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`


* **Modo** de persistência( `cq.wcm.undo.persistence.mode`)

   * **Descrição**: Determina quando o histórico de desfazer é persistente. Selecione essa opção para persistir no histórico de desfazer após cada edição de página. Desmarque essa opção para persistir somente quando ocorrer um recarregamento de página (por exemplo, o usuário navega para uma página diferente).

      O histórico de desfazer persistente usa recursos do navegador da Web. Se o navegador dos usuários reagir lentamente às edições da página, tente persistir no histórico de desfazer quando a página for recarregada.

   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Modo** marcador( `cq.wcm.undo.markermode`)

   * **Descrição**: Especifica a dica visual a ser usada para indicar quais parágrafos são afetados quando ocorre um comando desfazer ou refazer. Os seguintes valores são válidos:

      * flash: O indicador de seleção dos parágrafos pisca temporariamente.
      * selecione: O parágrafo é selecionado.
   * **Padrão**: `flash`
   * **Tipo**: `String`


* **Bons componentes**( `cq.wcm.undo.whitelist`)

   * **Descrição**: Uma lista de componentes que você deseja que sejam afetados pelos comandos desfazer e refazer. Adicione caminhos de componentes a essa lista quando eles funcionarem corretamente com desfazer/refazer. Anexar um asterisco (&amp;ast;) para especificar um grupo de componentes:

      * O valor a seguir especifica o componente de texto da base:

         `foundation/components/text`

      * O valor a seguir especifica todos os componentes de fundação:

         `foundation/components/*`
   * Quando desfazer ou refazer for emitido para um componente que não está nessa lista, uma mensagem será exibida indicando que o comando pode não ser confiável.

   * **Padrão**: A propriedade é preenchida com muitos componentes fornecidos pelo AEM.
   * **Tipo**: `String[]`


* **Componentes** defeituosos( `cq.wcm.undo.blacklist`)

   * **Descrição**: Uma lista de componentes e/ou operações de componentes que você não deseja que sejam afetados pelo comando desfazer. Adicione componentes e operações de componentes que não se comportam corretamente com o comando desfazer:

      * Adicione um caminho de componente quando desejar que nenhuma das operações do componente ocorra no histórico de desfazer, por exemplo `collab/forum/components/post`
      * Anexar dois pontos (:) e uma operação ao caminho quando desejar que essa operação específica seja omitida do histórico de desfazer (outras operações funcionam corretamente), por exemplo `collab/forum/components/post:insertParagraph.`
   >[!NOTE]
   >
   >Quando uma operação está nessa lista, ela ainda é adicionada ao histórico de desfazer. Os usuários não podem desfazer operações que existem antes de uma operação Componente **** inválido no histórico de desfazer.

   * Os nomes típicos das operações são os seguintes:

      * `insertParagraph`: O componente é adicionado à página.
      * `removeParagraph`: O componente é excluído.
      * `moveParagraph`: O parágrafo é movido para um local diferente.
      * `updateParagraph`: As propriedades do parágrafo são alteradas.
   * **Padrão**: A propriedade é preenchida com várias operações de componente.
   * **Tipo**: `String[]`




