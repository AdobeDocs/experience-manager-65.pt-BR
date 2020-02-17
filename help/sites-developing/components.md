---
title: Visão geral dos componentes
seo-title: Componentes
description: Os componentes são unidades modulares que obtêm funcionalidade específica para apresentar seu conteúdo em seu site
seo-description: Os componentes são unidades modulares que obtêm funcionalidade específica para apresentar seu conteúdo em seu site
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
translation-type: tm+mt
source-git-commit: 5597fb39500ac1f85d03263bfa1e5239d35d2a2c

---


# Visão geral dos componentes{#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para a criação](/help/sites-authoring/default-components-foundation.md)de páginas.

## O que são os componentes? {#what-exactly-is-a-component}

* Unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site.
* Reutilizável.
* Desenvolvido como unidades independentes em uma pasta do repositório.
* Não tem arquivos de configuração ocultos.
* Pode conter outros componentes.
* Pode ser executado em qualquer lugar em qualquer sistema AEM. Eles também podem ser limitados a serem executados em componentes específicos.
* Tenha uma interface de usuário padronizada.
* Ter comportamento de edição que possa ser configurado.
* Usar caixas de diálogo que são criadas usando subelementos com base em componentes da interface do usuário do Granite
* São desenvolvidos usando [HTL](https://docs.adobe.com/content/help/en/experience-manager-htl/using/overview.html) (recomendado) ou JSP.
* Pode ser desenvolvido para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolva um novo componente na sua instância local.
* Implante-o no ambiente de teste.
* Implante-o em seu ambiente de criação ao vivo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seu ambiente de publicação ao vivo, onde eles são usados para renderizar conteúdo para visitantes do seu site. Determinados componentes, por exemplo para Comunidades, também aceitam informações de seus usuários.

Cada componente AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar *isoladamente*, ou seja, no AEM ou em um portal.

## Componentes prontos para uso no AEM {#out-of-the-box-components-within-aem}

AEM comes with a variety of [out-of-the-box components](/help/sites-authoring/default-components.md) that provide comprehensive functionality including:

* Sistema de parágrafos ( `parsys`)
* Página (somente `responsivegrid` - interface habilitada para toque)
* Texto
* Imagem, com o texto que a acompanha
* Barra de ferramentas

Os componentes fornecidos e seu uso nos sites [We.Retail de](/help/sites-developing/we-retail.md) amostra fornecidos ilustram como implementar e usar componentes. Os componentes são fornecidos com todo o código fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Componentes principais e componentes básicos {#core-components-and-foundation-components}

Há dois conjuntos de componentes AEM fornecidos pela Adobe disponíveis:

* [Componentes principais](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Componentes fundamentais](/help/sites-authoring/default-components-foundation.md)

**Os componentes** principais foram introduzidos com o AEM 6.3 e oferecem funcionalidade de criação flexível e repleta de recursos. O site [de referência](/help/sites-developing/we-retail.md) We.Retail ilustra como os componentes principais podem ser usados e representa as práticas recomendadas atuais do desenvolvimento de componentes.

**Os componentes** básicos foram disponibilizados com o AEM para muitas versões e estão disponíveis prontamente em uma instalação padrão do AEM. Embora ainda seja suportado, a maioria foi substituída, não é mais aprimorada e se baseia em tecnologias herdadas.

>[!NOTE]
>
>[Os Componentes](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principais representam as práticas recomendadas atuais para o design e desenvolvimento de componentes e servem como implementações de referência.
>
>[As Ferramentas](modernization-tools.md) de modernização do AEM podem ajudar na migração para os Componentes principais.

### Exibindo componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis em sua instância do AEM, use o console [](/help/sites-authoring/default-components-console.md)Componentes.

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. No **[!UICONTROL CRXDE Lite]**, selecione **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, **[!UICONTROL Consulta]**, que abre a guia **[!UICONTROL Consulta]** .

1. Na guia **[!UICONTROL Consulta]** , selecione `XPath` como **[!UICONTROL Tipo]**.

1. No campo de entrada **[!UICONTROL Consulta]** , digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes são listados.

## Recursos adicionais {#further-reading}

As páginas a seguir fornecem informações mais detalhadas sobre o desenvolvimento desses componentes e de outros componentes:

* [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md)
* [Desenvolvimento de componentes do AEM](/help/sites-developing/developing-components.md)
* [Desenvolvimento de componentes do AEM - exemplos de código](/help/sites-developing/developing-components-samples.md)
* [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desenvolvedor](/help/sites-developing/developer-mode.md)
* [Teste da interface do usuário](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)
* [Obter informações da página no formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalizando componentes](/help/sites-developing/i18n.md)
* [Componentes principais](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Como usar Ocultar condições](/help/sites-developing/hide-conditions.md)
* Interface do usuário clássica

   * [Componentes do AEM (interface clássica)](/help/sites-developing/developing-components-classic.md)
   * [Uso e extensão de widgets (interface clássica)](/help/sites-developing/widgets.md)
   * [Uso de xtypes (interface clássica)](/help/sites-developing/xtypes.md)
   * [Desenvolvimento de formulários (Interface clássica)](/help/sites-developing/developing-forms.md)

