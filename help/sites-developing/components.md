---
title: Componentes Visão geral
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
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 8%

---


# Visão geral dos componentes{#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para criação de página](/help/sites-authoring/default-components-foundation.md).

## O que são os componentes? {#what-exactly-is-a-component}

* Unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site.
* Reutilizável.
* Desenvolvido como unidades independentes em uma pasta do repositório.
* Não tem arquivos de configuração ocultos.
* Pode conter outros componentes.
* Pode ser executado em qualquer lugar dentro de qualquer sistema AEM. Eles também podem ser limitados a serem executados em componentes específicos.
* Tenha uma interface de usuário padronizada.
* Ter comportamento de edição que possa ser configurado.
* Usar caixas de diálogo que são criadas usando subelementos com base em componentes da interface do usuário do Granite
* São desenvolvidos usando [HTL](https://docs.adobe.com/content/help/pt-BR/experience-manager-htl/using/overview.html) (recomendado) ou JSP.
* Pode ser desenvolvido para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolva um novo componente na sua instância local.
* Implante-o no ambiente de teste.
* Implante-o em seu ambiente de criação ao vivo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seus ambientes de publicação ao vivo, onde eles são usados para renderizar o conteúdo de visitantes em seu site. Determinados componentes, por exemplo para Comunidades, também aceitam informações de seus usuários.

Cada componente AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar em *isolar*, ou seja, em AEM ou em um portal.

## Componentes prontos para uso em AEM {#out-of-the-box-components-within-aem}

AEM vem com uma variedade de [componentes prontos para uso](/help/sites-authoring/default-components.md) que fornecem funcionalidade abrangente, incluindo:

* Sistema de parágrafos ( `parsys`)
* Página ( `responsivegrid` - somente interface habilitada para toque)
* Texto
* Imagem, acompanhado do texto
* Barra de ferramentas

Os componentes fornecidos e seu uso nos [sites We.Retail](/help/sites-developing/we-retail.md) de amostra fornecidos ilustram como implementar e usar componentes. Os componentes são fornecidos com todo o código fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Componentes principais e componentes básicos {#core-components-and-foundation-components}

Há dois conjuntos de componentes de AEM fornecidos pelo Adobe disponíveis:

* [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html)
* [Componentes fundamentais](/help/sites-authoring/default-components-foundation.md)

**Os componentes principais** foram introduzidos com AEM 6.3 e funcionalidade de criação flexível e repleta de recursos para ofertas. O [site de referência We.Retail](/help/sites-developing/we-retail.md) ilustra como os componentes principais podem ser usados e representa as práticas recomendadas atuais do desenvolvimento de componentes.

**Os** componentes básicos foram disponibilizados com AEM para muitas versões e estão disponíveis prontamente em uma instalação AEM padrão. Embora ainda seja suportado, a maioria foi substituída, não é mais aprimorada e se baseia em tecnologias herdadas.

>[!NOTE]
>
>[Os ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) componentes principais representam as práticas recomendadas atuais para o design e desenvolvimento de componentes e servem como implementações de referência.
>
>[AEM ](modernization-tools.md) Ferramentas de modernização ajudam na migração para os Componentes principais.

### Exibindo Componentes Disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis em sua instância AEM, use o [console Componentes](/help/sites-authoring/default-components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. Em **[!UICONTROL CRXDE Lite]**, selecione **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, **[!UICONTROL Query]**, que abre a guia **[!UICONTROL Query]**.

1. Na guia **[!UICONTROL Query]**, selecione `XPath` como **[!UICONTROL Tipo]**.

1. No campo de entrada **[!UICONTROL Query]**, digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Execute]** e os componentes serão listados.

## Recursos adicionais {#further-reading}

As páginas a seguir fornecem informações mais detalhadas sobre o desenvolvimento desses componentes e de outros componentes:

* [Componentes AEM - Noções básicas](/help/sites-developing/components-basics.md)
* [Desenvolvimento de componentes AEM](/help/sites-developing/developing-components.md)
* [Desenvolvimento de componentes AEM - exemplos de código](/help/sites-developing/developing-components-samples.md)
* [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desenvolvedor](/help/sites-developing/developer-mode.md)
* [Testando sua interface de usuário](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)
* [Obter informações da página no formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalização de componentes](/help/sites-developing/i18n.md)
* [Componentes principais](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html)
* [Como usar Ocultar condições](/help/sites-developing/hide-conditions.md)
* Interface do usuário clássica

   * [Componentes AEM (IU clássica)](/help/sites-developing/developing-components-classic.md)
   * [Uso e extensão de widgets (interface clássica)](/help/sites-developing/widgets.md)
   * [Uso de xtypes (interface clássica)](/help/sites-developing/xtypes.md)
   * [Desenvolvimento do Forms (interface clássica)](/help/sites-developing/developing-forms.md)

