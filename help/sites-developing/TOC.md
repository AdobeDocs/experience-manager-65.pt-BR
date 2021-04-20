---
cloud: Experience Cloud
product: adobe experience manager
solution: Experience Manager, Experience Manager Sites
audience: end-user
user-guide-title: Guia do usuário para desenvolvimento no AEM 6.5
breadcrumb-title: Guia de desenvolvimento
user-guide-description: Este guia aborda como criar sua instância no AEM.
feature-set: Experience Manager Sites
feature: Developing
role: Developer
translation-type: tm+mt
source-git-commit: d7b0803385aaa451a1ec7ec280ff51c3e96e36e7
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 16%

---


# Guia do usuário para desenvolvimento no AEM 6.5 {#developing}

+ [Visão geral do Guia do usuário para desenvolvimento](home.md)
+ Introdução para desenvolvedores{#introduction}
   + [Introdução ao desenvolvimento do AEM Sites - Tutorial de WKND](getting-started.md)
   + [AEM Conceitos principais](the-basics.md)
   + [Estrutura da interface de usuário habilitada para toque do AEM](touch-ui-structure.md)
   + [Conceitos da interface de usuário habilitada para toque do AEM](touch-ui-concepts.md)
   + [Desenvolvimento de AEM - Diretrizes e práticas recomendadas](dev-guidelines-bestpractices.md)
   + [Uso de bibliotecas do cliente](clientlibs.md)
   + [Desenvolvimento e diff de página](pagediff.md)
   + [Limitações do editor](editor-limitations.md)
   + [Quadro de proteção do QREF](csrf-protection.md)
   + [Modelagem de Dados - Modelo de David Nuescheler](model-data.md)
   + [Contribuição para AEM](contributing-to-cq.md)
   + [Segurança](security.md)
   + [Materiais de referência](reference-materials.md)
   + [Criar um site com recursos completos (interface clássica)](website.md)
   + [Designs and the Designer (Classic UI)](designer.md)
   + [Migração para a interface de toque](/help/sites-developing/touch-ui-migration.md)
+ Plataforma{#platform}
   + [Folha de características do Sling](sling-cheatsheet.md)
   + [Uso de adaptadores Sling](sling-adapters.md)
   + [Bibliotecas de tags](taglib.md)
   + Modelos{#templates}
      + [Modelos](templates.md)
      + [Modelos de página - Editável  ](page-templates-editable.md)
      + [Modelos de página - Estático](page-templates-static.md)
      + [Modelos de fragmentos do conteúdo](content-fragment-templates.md)
      + [Renderização do modelo adaptável](templates-adaptive-rendering.md)
   + [Uso da Fusão de Recursos do Sling em AEM](sling-resource-merger.md)
   + [Sobreposições](overlays.md)
   + [Convenções de nomenclatura](naming-conventions.md)
   + [Criação de um novo componente de campo da interface do usuário do Granite](granite-ui-component.md)
   + Query Builder{#query-builder}
      + [Implementando um Avaliador de Predicados Personalizados para o Construtor de Consultas](implementing-custom-predicate-evaluator.md)
      + [Referência de predicado do construtor de consultas](querybuilder-predicate-reference.md)
      + [API do Construtor de consulta](querybuilder-api.md)
   + Marcação com tags{#tagging}
      + [Marcação com tags](tags.md)
      + [Estrutura de marcação de AEM](framework.md)
      + [Criação de tags em um aplicativo AEM](building.md)
   + [Personalização de páginas mostradas pelo Manipulador de erros](customizing-errorhandler-pages.md)
   + [Tipos de nó personalizados](custom-nodetypes.md)
   + [Adicionar fontes para renderização de gráficos](adding-fonts.md)
   + [Conexão com Bancos de Dados SQL](jdbc.md)
   + [Exteriorização de URLs](externalizer.md)
   + [Criação e consumo de trabalhos para descarregamento](dev-offloading.md)
   + [Configuração do uso de cookies](cookie-optout.md)
   + [Como acessar programaticamente o JCR AEM](access-jcr.md)
   + [Integração de serviços com o console JMX](jmx-integration.md)
   + [Desenvolvimento do editor em massa](dev-bulk-editor.md)
   + [Desenvolvimento de relatórios](dev-reports.md)
   + eCommerce{#ecommerce}
      + [eCommerce](ecommerce.md)
      + [Desenvolvimento (genérico)](generic.md)
      + [Desenvolvimento com o SAP Commerce Cloud](sap-commerce-cloud.md)
+ Componentes{#components}
   + [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)
   + [Sistema de estilos](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/style-system.html)
   + [Visão geral dos componentes](components.md)
   + [Componentes AEM - Noções básicas](components-basics.md)
   + [Desenvolvimento de componentes de AEM](developing-components.md)
   + [Desenvolvimento de componentes de AEM - Amostras de código](developing-components-samples.md)
   + [Exportador JSON para serviços de conteúdo](json-exporter.md)
   + [Ativando a exportação JSON para um componente](json-exporter-components.md)
   + [Editor de imagem ](image-editor.md)
   + [Tag de decoração](decoration-tag.md)
   + [Usar Ocultar condições](hide-conditions.md)
   + [Configuração de vários editores no local](multiple-inplace-editors.md)
   + [Modo de desenvolvedor](developer-mode.md)
   + [Testar sua interface do usuário](hobbes.md)
   + [Componentes para fragmentos de conteúdo](components-content-fragments.md)
   + [Obter informações de página no formato JSON](pageinfo.md)
   + Internacionalização{#internationalization}
      + [Internacionalizar componentes](i18n.md)
      + [Internacionalizar cadeias de caracteres da interface do usuário](i18n-dev.md)
      + [Usar o tradutor para gerenciar dicionários](i18n-translator.md)
      + [Extraindo strings para tradução](i18n-extract.md)
   + Componentes da interface clássica{#classic-ui-components}
      + [Desenvolvimento de componentes AEM (interface clássica)](developing-components-classic.md)
      + [Uso e extensão de widgets (interface de usuário clássica)](widgets.md)
      + [Uso de xtypes (interface clássica)](xtypes.md)
      + [Desenvolvimento do Forms (interface clássica)](developing-forms.md)
+ Gerenciamento de experiência headless{#headless}
   + [Sem cabeçalho e híbrido com AEM](https://www.adobe.com/content/dam/www/us/en/marketing/experience-manager-sites/headless-content-management-system/pdfs/aem-hybrid-architecture-wp-1-18-19.pdf)
   + [Ativando a exportação JSON para um componente](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/json-exporter-components.html)
   + Aplicativos de página única{#spas}
      + [Introdução SPA e Apresentação](spa-walkthrough.md)
      + [Tutorial WKND do SPA](spa-wknd.md)
      + [Introdução ao SPA no AEM - React](spa-getting-started-react.md)
      + [Introdução ao SPA no AEM - Angular](spa-getting-started-angular.md)
      + [Implementação de um componente de reação para SPA](spa-implementing-react-component.md)
      + [SPA Deep Dives](spa-deep-dives.md)
      + [Visão geral do editor de SPA](spa-overview.md)
      + [Desenvolvimento de SPA para AEM](spa-architecture.md)
      + [SPA Blueprint](spa-blueprint.md)
      + [Componente Página SPA](spa-page-component.md)
      + [Modelo dinâmico para mapeamento de componentes para SPA](spa-dynamic-model-to-component-mapping.md)
      + [Roteamento do Modelo de SPA](spa-routing.md)
      + [Integração do SPA e Adobe Experience Platform Launch](spa-launch.md)
      + [Renderização de SPA e do servidor](spa-ssr.md)
      + [O componente RemotePage](spa-remote-page.md)
      + [Edição de um SPA externo no AEM](spa-edit-external.md)
      + [Componentes compostos em SPA](spa-composite-component.md)
      + [Materiais de referência SPA](spa-reference-materials.md)
   + [API HTTP](https://experienceleague.adobe.com/docs/experience-manager-65/assets/extending/mac-api-assets.html)
   + [Fragmentos de conteúdo](https://experienceleague.adobe.com/docs/experience-manager-65/assets/fragments/content-fragments.html)
   + [Fragmentos de experiência](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/authoring/experience-fragments.html)
   + [Como entender os fragmentos de conteúdo e os serviços de conteúdo no AEM](https://helpx.adobe.com/experience-manager/kt/sites/using/content-fragments-content-services-feature-video-understand.html)
+ Ferramentas de desenvolvimento{#devtools}
   + [Ferramentas de desenvolvimento](dev-tools.md)
   + [Ferramentas de Modernização do AEM](modernization-tools.md)
   + [Editor de caixa de diálogo](dialog-editor.md)
   + [Ferramenta de conversão de caixa de diálogo](dialog-conversion.md)
   + [Desenvolvimento com o CRXDE Lite](developing-with-crxde-lite.md)
   + [Gerenciamento de pacotes usando o Maven](vlt-mavenplugin.md)
   + [Como desenvolver projetos AEM usando o Eclipse](howto-projects-eclipse.md)
   + [Como criar projetos AEM usando o Apache Maven](ht-projects-maven.md)
   + [Como desenvolver projetos AEM usando o IntelliJ IDEA](ht-intellij.md)
   + [Como usar a ferramenta VLT](ht-vlttool.md)
   + [Como usar a ferramenta Servidor proxy](ht-proxy-server.md)
   + [Extensão de colchetes AEM](aem-brackets.md)
   + [Ferramentas de desenvolvedor do AEM para Eclipse](aem-eclipse.md)
   + [Ferramenta AEM Repo](aem-repo-tool.md)
+ Personalização{#personlization}
   + [ContextHub](contexthub.md)
   + [Configuração do Context Hub](ch-configuring.md)
   + [Adicionar o ContextHub às páginas e acessar armazenamentos](ch-adding.md)
   + [Extensão do ContextHub](ch-extend.md)
   + [Exemplos de candidatos à loja do ContextHub](ch-samplestores.md)
   + [Exemplos de tipos de módulo da interface do usuário do ContextHub](ch-samplemodules.md)
   + [Diagnósticos do ContextHub](ch-diagnostics.md)
   + [Desenvolvimento de conteúdo direcionado](target.md)
   + [Referência de API do Javascript do ContextHub](contexthub-api.md)
   + ClientContext{#client-context}
      + [Contexto do cliente em detalhes](client-context.md)
      + [API Javascript de contexto do cliente](ccjsapi.md)
+ Extensão de AEM{#extending-aem}
   + [Personalização da criação de página](customizing-page-authoring-touch.md)
   + [Personalização dos consoles](customizing-consoles-touch.md)
   + [Personalização de exibições das propriedades da página](page-properties-views.md)
   + [Configurar sua página para a edição de itens em massa das propriedades da página](bulk-editing.md)
   + [Personalização e extensão de fragmentos de conteúdo](customizing-content-fragments.md)
   + [Fragmentos de conteúdo configuram componentes para renderização](content-fragments-config-components-rendering.md)
   + [Fragmentos de experiência](experience-fragments.md)
   + Extensão de fluxos de trabalho{#extending-workflows}
      + [Desenvolvimento e extensão de workflows](workflows.md)
      + [Criação de modelos de fluxo de trabalho](workflows-models.md)
      + [Ampliação da funcionalidade do fluxo de trabalho](workflows-customizing-extending.md)
      + [Interação com fluxos de trabalho programaticamente](workflows-program-interaction.md)
      + [Referência da Etapa do fluxo de trabalho](workflows-step-ref.md)
      + [Práticas recomendadas do workflow](workflows-best-practices.md)
      + [Referência do processo de fluxo de trabalho](workflows-process-ref.md)
      + [Variáveis em workflows AEM](/help/sites-developing/using-variables-in-aem-workflows.md)
   + [Extensão do Gerenciador de vários sites](extending-msm.md)
   + Rastreamento e análise{#extending-analytics}
      + [Extensão do rastreamento de eventos](extending-analytics.md)
      + [Adicionar rastreamento do Adobe Analytics aos componentes](extending-analytics-components.md)
      + [Personalização da Adobe Analytics Framework](extending-analytics-framework.md)
      + [Implementação de nomenclatura de página do lado do servidor para o Analytics](extending-analytics-pa-naming.md)
   + Cloud Services{#extending-cloud-services}
      + [Configurações do Cloud Service](extending-cloud-config.md)
      + [Criação de um Cloud Service personalizado](extending-cloud-config-custom-cloud.md)
   + [Criação de extensões personalizadas](extending-campaign-extensions.md)
   + Forms{#extending-forms}
      + [Criação de mapeamentos de formulário personalizados](extending-campaign-form-mapping.md)
      + [Criando modelo de página de AEM personalizado com componentes de formulário Adobe Campaign](extending-campaign-custom-template.md)
      + [Script de análise de solicitação](analyze-request.md)
   + [Integração de serviços com o console JMX](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/jmx-integration.html)
   + [Desenvolvimento do editor em massa](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-bulk-editor.html)
   + Extensão da interface clássica{#extending-classic-ui}
      + [Personalização do console Sites (interface clássica)](customizing-siteadmin.md)
      + [Personalização do console de boas-vindas (interface clássica)](customizing-the-welcome-console.md)
      + [Desenvolvimento de relatórios](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/dev-reports.html)
+ Testes{#testing}
   + [Planejamento](planning.md)
   + [Quais ambientes de teste serão necessários?](test-environments.md)
   + [Definição dos casos de teste](test-cases.md)
   + [Teste - quando e com quem?](when-who.md)
   + [Compilação do plano de teste](test-plan.md)
   + [Rastrear resultados e fornecer feedback](results-and-feedback.md)
   + [Ferramentas de teste e rastreamento](tools.md)
   + [Aceitação e aprovação](acceptance-signoff.md)
   + [A próxima versão..](the-next-release.md)
   + [Listas de verificação](checklists.md)
   + [Dia difícil](tough-day.md)
   + [Testar sua interface do usuário](https://experienceleague.adobe.com/docs/experience-manager-65/developing/components/hobbes.html)
+ Práticas recomendadas    {#bestpractices}
   + [Visão geral das práticas recomendadas](best-practices.md)
   + [Diretrizes de desenvolvimento de AEM e práticas recomendadas](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/dev-guidelines-bestpractices.html)
   + [Práticas recomendadas de desenvolvimento](development-practices.md)
   + [Arquitetura de conteúdo](content-architecture.md)
   + [Arquitetura de software](software-architecture.md)
   + Implementação de referência We.Retail{#we-retail}
      + [Implementação de referência We.Retail](we-retail.md)
      + [Experimentação de fragmentos de conteúdo no We.Retail](we-retail-content-fragments.md)
      + [Como experimentar os Componentes principais no We.Retail](we-retail-core-components.md)
      + [Tentando modelos editáveis no We.Retail](we-retail-editable-templates.md)
      + [Tentando um layout responsivo no We.Retail](we-retail-responsive-layout.md)
      + [Tentar a estrutura do site globalizado no We.Retail](we-retail-globalized-site-structure.md)
      + [Experiência de fragmentos de experiência no We.Retail](we-retail-experience-fragments.md)
   + [Dicas de codificação](coding-tips.md)
   + [armadilhas de código](code-pitfalls.md)
   + [Pacotes OSGI](osgi-bundles.md)
   + [Integração JCR](jcr-integration.md)
   + [Amostras de código](code-samples.md)
   + [Solução de problemas de consultas lentas](troubleshooting-slow-queries.md)
+ Web móvel{#mobileweb}
   + [Web móvel](mobile-web.md)
   + [Criando Filtros de Grupo de Dispositivos](groupfilters.md)
   + [Design responsivo para páginas da Web](responsive.md)
   + [Criação de sites para dispositivos móveis](mobile.md)
   + [Emuladores](emulators.md)
