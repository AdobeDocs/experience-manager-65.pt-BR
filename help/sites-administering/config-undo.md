---
title: Configuração de Desfazer para Edição de Página
description: Saiba como configurar o suporte a Desfazer para edição de página no AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: 2cf3ac3f-ee17-480d-a32a-c57631502693
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 0%

---

# Configuração de Desfazer para Edição de Página{#configuring-undo-for-page-editing}

A variável [Serviço OSGi](/help/sites-deploying/configuring-osgi.md)  **Configuração de desfazer WCM CQ do dia** ( `com.day.cq.wcm.undo.UndoConfigService`) expõe várias propriedades que controlam o comportamento dos comandos desfazer e refazer para editar páginas.

## Configuração padrão {#default-configuration}

Em uma instalação padrão, as configurações padrão são definidas como propriedades no `sling:OsgiConfig`nó:

`/libs/wcm/core/config.author/com.day.cq.wcm.undo.UndoConfig`

Este nó contém `cq.wcm.undo.whitelist` e `cq.wcm.undo.blacklist` propriedades, para as outras propriedades, os padrões são usados.

>[!CAUTION]
>
>Você ***deve*** não alterar nada no `/libs` caminho.
>
>Isso ocorre porque o conteúdo de `/libs` é substituído na próxima vez que você atualizar sua instância (e pode ser substituído ao aplicar um hotfix ou pacote de recursos).

## Configurando Desfazer e Refazer {#configuring-undo-and-redo}

Você pode configurar essas propriedades de serviço do OSGi para sua própria instância.

>[!NOTE]
>
>Ao trabalhar com AEM, há vários métodos de gerenciamento das definições de configuração desses serviços; consulte [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) para obter mais detalhes e as práticas recomendadas.

A seguir estão as propriedades conforme exibidas no console da Web, seguidas pelo nome do parâmetro OSGi correspondente, juntamente com uma descrição e o valor padrão (quando apropriado):

* **Ativar**
( `cq.wcm.undo.enabled`)

   * **Descrição**: determina se os autores de página podem desfazer e refazer alterações.
   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Caminho**
( `cq.wcm.undo.path`)

   * **Descrição**: o caminho do repositório para a persistência de dados binários de desfazer. Quando os autores alteram dados binários, como imagens, a versão original dos dados é mantida aqui. Quando as alterações nos dados binários são desfeitas, esses dados binários são restaurados na página.
   * **Padrão**: `/var/undo`
   * **Tipo**: `String`

  >[!NOTE]
  >
  >Por padrão, somente os administradores podem acessar a variável `/var/undo` nó. Os autores podem executar operações de desfazer e refazer em conteúdo binário somente após receberem permissões para acessar os dados de desfazer binários.

* **Versão mín. validade**
( `cq.wcm.undo.validity`)

   * **Descrição**: A quantidade mínima de tempo em que os dados binários do undo são armazenados, em horas. Após esse período, os dados binários ficam disponíveis para exclusão, a fim de conservar o espaço em disco.
   * **Padrão**: `10`
   * **Tipo**: `Integer`

* **Etapas**
( `cq.wcm.undo.steps`)

   * **Descrição**: o número máximo de ações de página armazenadas no histórico do undo.
   * **Padrão**: `20`
   * **Tipo**: `Integer`

* **Persistência**
( `cq.wcm.undo.persistence`)

   * **Descrição**: a classe que persiste no histórico do undo. Duas classes de persistência são fornecidas:

      * `CQ.undo.persistence.WindowNamePersistence`: persiste o histórico usando a propriedade window.name.
      * `CQ.undo.persistence.CookiePersistance`: persiste o histórico usando cookies.

   * **Padrão**: `CQ.undo.persistence.WindowNamePersistence`
   * **Tipo**: `String`

* **Modo de persistência**
( `cq.wcm.undo.persistence.mode`)

   * **Descrição**: determina quando o histórico da ação desfazer é mantido. Selecione esta opção para manter o histórico de desfazer após cada edição de página. Desmarque essa opção para persistir somente quando ocorrer um recarregamento de página (por exemplo, o usuário navega para uma página diferente).

     A persistência do histórico de desfazer usa os recursos do navegador da Web. Se o navegador dos usuários reagir lentamente às edições da página, tente persistir no histórico de desfazer nos recarregamentos da página.

   * **Padrão**: `Selected`
   * **Tipo**: `Boolean`

* **Modo de marcador**
( `cq.wcm.undo.markermode`)

   * **Descrição**: Especifica a sinalização visual a ser usada para indicar quais parágrafos são afetados quando ocorre uma ação desfazer ou refazer. Os seguintes valores são válidos:

      * flash: O indicador de seleção dos parágrafos pisca temporariamente.
      * select: O parágrafo é selecionado.

   * **Padrão**: `flash`
   * **Tipo**: `String`

* **Bons componentes**
( `cq.wcm.undo.whitelist`)

   * **Descrição**: uma lista de componentes que você deseja que sejam afetados pelos comandos desfazer e refazer. Adicionar caminhos de componentes a esta lista quando eles funcionarem corretamente com undo/redo. Anexe um asterisco (&amp;ast;) para especificar um grupo de componentes:

      * O valor a seguir especifica o componente de texto de base:

        `foundation/components/text`

      * O valor a seguir especifica todos os componentes de base:

        `foundation/components/*`

   * Quando undo ou redo é emitido para um componente que não está nessa lista, uma mensagem é exibida indicando que o comando pode não ser confiável.

   * **Padrão**: a propriedade é preenchida com muitos componentes que o AEM fornece.
   * **Tipo**: `String[]`

* **Componentes inválidos**
( `cq.wcm.undo.blacklist`)

   * **Descrição**: uma lista de componentes e/ou operações de componentes que você não deseja que sejam afetados pelo comando desfazer. Adicione componentes e operações de componentes que não se comportam corretamente com o comando desfazer:

      * Adicione um caminho de componente quando não quiser nenhuma das operações do componente no histórico Desfazer, por exemplo, `collab/forum/components/post`
      * Anexe dois pontos (:) e uma operação ao caminho quando quiser que essa operação específica seja omitida do histórico de desfazer (outras operações funcionam corretamente), por exemplo, `collab/forum/components/post:insertParagraph.`

  >[!NOTE]
  >
  >Quando uma operação está nessa lista, ela ainda é adicionada ao histórico desfazer. Os usuários não podem desfazer operações que existem antes de um **Componente incorreto** operação no histórico de desfazer.

   * Os nomes de operação típicos são os seguintes:

      * `insertParagraph`: o componente é adicionado à página.
      * `removeParagraph`: o componente é excluído.
      * `moveParagraph`: O parágrafo é movido para um local diferente.
      * `updateParagraph`: as propriedades do parágrafo são alteradas.

   * **Padrão**: a propriedade é preenchida com várias operações de componente.
   * **Tipo**: `String[]`
