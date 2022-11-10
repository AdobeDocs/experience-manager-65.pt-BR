---
title: Visão geral dos componentes
seo-title: Components
description: Os componentes são unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site
seo-description: Components are modular units which realize specific functionality to present your content on your website
uuid: fb39aeb8-8f43-4091-8083-ebfab89e6e63
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 45efff93-2fe5-4313-83a0-0e23a540da93
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 6%

---

# Visão geral dos componentes{#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como esses [usado para criação de página](/help/sites-authoring/default-components-foundation.md).

## O que são Componentes? {#what-exactly-is-a-component}

* Unidades modulares que realizam funcionalidades específicas para apresentar seu conteúdo em seu site.
* Reutilizável.
* Desenvolvido como unidades independentes em uma pasta do repositório.
* Não tem arquivos de configuração ocultos.
* Pode conter outros componentes.
* Pode ser executado em qualquer lugar em qualquer sistema AEM. Eles também podem se limitar a ser executados em componentes específicos.
* Ter uma interface de usuário padronizada.
* Ter um comportamento de edição que possa ser configurado.
* Usar caixas de diálogo que são criadas usando subelementos com base nos componentes da interface do usuário do Granite
* São desenvolvidos usando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html) (recomendado) ou JSP.
* Pode ser desenvolvido para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolva um novo componente na instância local.
* Implante-o no ambiente de teste.
* Implante-o no ambiente de criação ao vivo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seu ambiente de publicação ao vivo, onde eles são usados para renderizar o conteúdo para os visitantes do seu site. Determinados componentes, por exemplo, para Comunidades, também aceitam informações de seus usuários.

Cada componente AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar em *isolamento*, ou seja, dentro de AEM ou de um portal.

## Componentes prontos para uso no AEM {#out-of-the-box-components-within-aem}

AEM vem com uma variedade de [componentes prontos para uso](/help/sites-authoring/default-components.md) que oferecem funcionalidades abrangentes, incluindo:

* Sistema de parágrafos ( `parsys`)
* Página ( `responsivegrid` - interface habilitada para toque somente)
* Texto
* Imagem, acompanhada do texto
* Barra de ferramentas

Os componentes fornecidos e seu uso na variável [Sites We.Retail de exemplo](/help/sites-developing/we-retail.md) fornecido ilustra como implementar e usar componentes. Os componentes são fornecidos com todo o código-fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Componentes principais e componentes básicos {#core-components-and-foundation-components}

Há dois conjuntos de componentes de AEM fornecidos pelo Adobe disponíveis:

* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Componentes fundamentais](/help/sites-authoring/default-components-foundation.md)

**Componentes principais** foram introduzidos com o AEM 6.3 e oferecem funcionalidade de criação flexível e repleta de recursos. O [Site de referência We.Retail](/help/sites-developing/we-retail.md) ilustra como os componentes principais podem ser usados e representam as práticas recomendadas atuais do desenvolvimento de componentes.

**Componentes básicos** estão disponíveis com AEM para várias versões e estão disponíveis prontamente em uma instalação padrão do AEM. Embora ainda sejam compatíveis, a maioria foi substituída, não são mais aprimoradas e se baseiam em tecnologias herdadas.

>[!NOTE]
>
>[Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) representam as práticas recomendadas atuais para design e desenvolvimento de componentes e servem como implementações de referência.
>
>[Ferramentas de Modernização AEM](modernization-tools.md) pode ajudar na migração para os Componentes principais.

### Visualizando componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis na sua instância do AEM, use o [Console de componentes](/help/sites-authoring/default-components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. Em **[!UICONTROL CRXDE Lite]**, selecione **[!UICONTROL Ferramentas]** na barra de ferramentas, em seguida **[!UICONTROL Query]**, que abre o **[!UICONTROL Query]** guia .

1. No **[!UICONTROL Query]** guia , selecione `XPath` as **[!UICONTROL Tipo]**.

1. No **[!UICONTROL Query]** campo de entrada, digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes são listados.

## Recursos adicionais {#further-reading}

As páginas a seguir fornecem informações mais detalhadas sobre o desenvolvimento desses — e de outros — componentes:

* [Componentes AEM - Noções básicas](/help/sites-developing/components-basics.md)
* [Desenvolvimento de componentes de AEM](/help/sites-developing/developing-components.md)
* [Desenvolvimento de componentes de AEM - Amostras de código](/help/sites-developing/developing-components-samples.md)
* [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desenvolvedor](/help/sites-developing/developer-mode.md)
* [Testar sua interface do usuário](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)
* [Obter informações de página no formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalizar componentes](/help/sites-developing/i18n.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
* [Uso de condições de ocultação](/help/sites-developing/hide-conditions.md)
* Interface do usuário clássica

   * [Componentes AEM (interface clássica)](/help/sites-developing/developing-components-classic.md)
   * [Uso e extensão de widgets (interface de usuário clássica)](/help/sites-developing/widgets.md)
   * [Uso de xtypes (interface clássica)](/help/sites-developing/xtypes.md)
   * [Desenvolvimento do Forms (interface clássica)](/help/sites-developing/developing-forms.md)
