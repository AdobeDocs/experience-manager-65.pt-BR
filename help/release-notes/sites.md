---
title: Notas de versão do AEM Sites
description: Notas de versão específicas do Adobe Experience Manager 6.5 Sites.
translation-type: tm+mt
source-git-commit: 8d60e064ab50f24016c049c8d5d0fceb784c99a3
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 71%

---


# Notas de versão do AEM Sites {#aem-sites-release-notes}

Consulte o seguinte para aprimoramentos do AEM Sites 6.5 em detalhes:

## Desenvolvimento de componentes e modelos {#component-amp-template-development}

* Maven Project Archetype 18+ para novos projetos, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype/releases).
* Maven Project Archetype 1.0.6+ de aplicativo de página única para novos projetos, consulte o [Github para obter notas de versão](https://github.com/adobe/aem-spa-project-archetype/releases).
* HTL versão 1.4, consulte o [Github para obter notas de versão](https://github.com/adobe/htl-spec/releases/tag/1.4).

   * operador &quot;in&quot; para strings, arrays e objetos:

      ```html
      ${'a' in 'abc’}
      ${100 in myArray}
      ${'a' in myObject}
      ```

   * Declarações de variáveis com dados definidos automaticamente:
      `<sly data-sly-set.title="${currentPage.title}"/>${title}`

   * Parâmetros de controlo de lista e repetição: begin, step, end:
      `<h2 data-sly-repeat="${currentPage.listChildren @ begin = 1, step=2}">${item.title}</h2>`

   * Identificadores para desvinculação automática de dados:

      ```html
      <div data-sly-unwrap.isUnwrapped="${myCondition || myOtherCondition}">
      text <span data-sly-test="${isUnwrapped}>is unwrapped</code>
      </div>
      ```

   * Suporte para números negativos

* Componentes principais 2.3.2+, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-core-wcm-components/releases).
* Sistema de grade para Contêiner de layout, consulte o [Github](https://github.com/Adobe-Marketing-Cloud/aem-responsivegrid).
* Gerenciador de clientlib: padrão do Google Closure Compiler para a miniificação de clientlibs do JavaScript (o padrão antigo era Yahoo YUI) e o Compilador de Fechamento do Google atualizado para a versão v20190121
* Editor de modelo e políticas

   * Crie e edite modelos para aplicativos de página única que estão usando o JS SDK (também chamado de Editor do SPA)

* We.Retail 4.0 de referência do Site, consulte o [Github para obter notas de versão](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/releases).
* Kit de ferramentas para atualizar sites existentes para aproveitar os recursos mais recentes do editor, consulte [Repositório Github](https://github.com/adobe/aem-modernize-tools)

>[!CAUTION]
>
>AEM inclui a versão 1.12.4 da biblioteca do jQuery para fornecer compatibilidade máxima com o código personalizado existente. As modificações foram feitas pela Adobe para solucionar problemas de segurança conhecidos.

## Administração de site {#site-administration}

* O painel de [Referências](/help/sites-authoring/author-environment-tools.md#references) tem uma nova seção para listar links internos que apontam para a página selecionada. Isso é útil ao planejar usar ou excluir uma página offline, para ver quais páginas precisam ser ajustadas antes de torná-las offline.
* A [exibição em lista](/help/sites-authoring/basic-handling.md#list-view) tem uma nova coluna de fluxo de trabalho que mostra o status quando a página está em um fluxo de trabalho no momento.
* Nas [propriedades de página](/help/sites-authoring/editing-page-properties.md), agora é possível procurar ativos existentes ao atribuir uma Miniatura à página (guia Miniatura).

## Editor de página {#page-editor}

* Permita a edição e composição em contexto de experiências de aplicativo de página única criadas com componentes do lado do cliente de Reação e Angular que estão aproveitando o JS SDK (também chamado de Editor do SPA)
* O Modo de estrutura é mostrado somente se a página tiver uma página de estrutura configurada.

## Fragmentos de conteúdo e editor {#content-fragments-amp-editor}

* Novo painel de [Anotações](/help/assets/content-fragments/content-fragments-variations.md#viewing-editing-deleting-annotations) no Editor de fragmentos de conteúdo para fazer comentários gerais e ver os comentários que fazem no texto (também mostrar no trilho da Linha do tempo)
* Capacidade de definir o tipo de conteúdo padrão de um elemento de texto de várias linhas em um [modelo de Fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) como texto simples, rich text ou markdown
* Adicione [comentários/anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment) selecionando o texto na RTE (exibição em tela inteira)
* [Compare versões](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) de um fragmento de conteúdo lado a lado por meio do painel de Referências
* O Relatório de download de ativos agora mostra fragmentos de conteúdo corretamente
* Adicione o [suporte de fragmento de conteúdo à API HTTP do Assets](/help/assets/assets-api-content-fragments.md) por meio do /api.json. Há APIs para criar, atualizar, ler e excluir os fragmentos de conteúdo.

## Fragmentos de experiência {#experience-fragments}

* Aprimoramento da indexação dos [fragmentos da experiência](/help/sites-authoring/experience-fragments.md), para que seu conteúdo seja encontrado na pesquisa por páginas em que estão sendo usados
* A opção [Exportar para o Target](/help/sites-administering/experience-fragments-target.md) agora permite enviar o Fragmento da experiência como JSON (o padrão é HTML) ou ambos

## Tradução  {#translation}

* Simplifique a criação de projetos de tradução usando os mestres de projeto
* Simplifique a execução de projetos de tradução definindo tarefas de tradução para o status aprovado por padrão
* Permitir atualização de páginas traduzidas com alterações na memória de tradução de terceiros
* Permitir exportar tarefas de tradução no formato JSON
* Atualize a integração do Microsoft Translation para usar a API V3

## Gerenciamento de vários sites (MSM) {#multi-site-management-msm}

* Para configurações de roll-out que usam PushOnModify, melhor manuseio da operação de movimentação de página para evitar o estado inconsistente
* Criar uma nova página dentro da estrutura livecopy agora criará uma página autônoma por padrão
* Use recursos do MSM nos aplicativos de página única que estão usando o JS SDK (também chamado Editor do SPA)

## Lançamentos {#launches}

* Novo fluxo de trabalho de revisão e aprovação para inicializações, e a capacidade de promover apenas as páginas de inicialização aprovadas
* Adição da [opção na interface do usuário para escolher excluir o Launch logo após a etapa de promoção](/help/sites-authoring/launches-promoting.md#promoting-launch-pages)

## Direcionamento e simulação de conteúdo  {#content-targeting-simulation}

* A camada de dados do ContextHub e o mecanismo de regras do cliente do Javascript foram atualizados para usar o jQuery 3 por padrão.

## AEM e Adobe Target {#aem-amp-adobe-target}

>[!CAUTION]
>
>at.js 2.x não é compatível com o AEM no ponto de versão do AEM 6.5. Utilize a versão mais recente do at.js 1.x

* A integração do Adobe Target agora pode usar a API padrão do Target. As versões anteriores do AEM usam a API HTTP Público alvo Classic, que agora está obsoleta.
* A versão 63 do Adobe Target `mbox.js` está incluída. O Adobe recomenda mudar a implementação para `at.js` v1.x.
* `at.js` a versão 1.5.0 agora está incluída. O Adobe recomenda que você use [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para provisionar `at.js` v1.x para o site.

## AEM e Adobe Analytics {#aem-amp-adobe-analytics}

* `s_code.js` H.27.5 está incluído. O Adobe recomenda que você alterne a implementação para `AppMeasurement.js`
* `AppMeasurement.js` v1.8.0 está incluído. O Adobe recomenda usar [Adobe Experience Platform Launch](https://www.adobe.com/experience-platform/launch.html) para provisionar o AppMeasurement.js no site.

## AEM e Comércio {#aem-commerce}

As melhorias na Commerce Integration Framework estão em um ciclo de lançamento mais rápido desde a AEM 6.4. [Saiba mais aqui](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/docs.html).

## Complemento do Communities {#communities-add-on}

Consulte a página [Notas de versão do Communities](../release-notes/communities-release-notes.md)

## Complemento do Screens  {#screens-add-on}

* Uso de inicializações para planejar futuras alterações de conteúdo para conteúdo de sinalização
* Reprodução medida em um canal de sequência
* Crie automaticamente a estrutura do projeto usando um arquivo de origem, por exemplo uma planilha do Excel

Para obter mais detalhes sobre alterações no AEM Screens - consulte as Notas de versão no [Guia do Usuário do AEM Screens](https://docs.adobe.com/content/help/en/experience-manager-screens/user-guide/aem-screens-introduction.html).
