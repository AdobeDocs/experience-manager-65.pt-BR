---
title: Visão geral dos componentes
description: Os componentes são unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 9e30c969-2692-4380-943a-b022ee900ce8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 44%

---

# Visão geral dos componentes{#components-overview}

Esta página fornece uma visão geral dos componentes do Adobe Experience Manager (AEM), como os [usados para criação de página](/help/sites-authoring/default-components-foundation.md).

## O que são componentes? {#what-exactly-is-a-component}

* Unidades modulares que realizam funcionalidades específicas para apresentar conteúdo em seu site.
* Reutilizáveis.
* Desenvolvidos como unidades independentes em uma pasta do repositório.
* Não contêm arquivos de configuração ocultos.
* Podem conter outros componentes.
* Pode ser executado em qualquer lugar dentro de qualquer sistema AEM. Eles também podem ser limitados para execução em componentes específicos.
* Têm uma interface de usuário padronizada.
* Têm um comportamento de edição que pode ser configurado.
* Use caixas de diálogo que são criadas usando subelementos com base nos componentes da interface do Granite
* São desenvolvidos usando [HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/content/overview.html?lang=pt-BR) (recomendado) ou JSP.
* Podem ser desenvolvidos para criar componentes personalizados que estendem a funcionalidade padrão.

Como os componentes são modulares, você pode:

* Desenvolver um novo componente na instância local.
* Implantá-los no ambiente de teste.
* Implantá-los no ambiente de criação ativo, onde eles permitem que autores e/ou administradores adicionem e configurem conteúdo.
* Implante-o em seu(s) ambiente(s) de publicação ativo(s), onde eles são usados para renderizar conteúdo para os visitantes do seu site. Determinados componentes, por exemplo, para Comunidades, também aceitam a entrada dos usuários.

Cada componente do AEM:

* É um tipo de recurso.
* É uma coleção de scripts que executa completamente uma função específica.
* Pode funcionar em *isolamento*, significando em AEM ou em um portal.

## Componentes prontos para uso dentro do AEM {#out-of-the-box-components-within-aem}

O AEM vem com uma variedade de [componentes prontos para uso](/help/sites-authoring/default-components.md) que fornecem funcionalidade abrangente, incluindo:

* Sistema de parágrafos ( `parsys`)
* Página ( `responsivegrid` - somente interface habilitada para toque)
* Texto
* Imagem, com texto de acompanhamento
* Barra de ferramentas

Os componentes fornecidos e seu uso nos [sites de amostra do We.Retail](/help/sites-developing/we-retail.md) fornecidos ilustram como implementar e usar componentes. Os componentes são fornecidos com todos os códigos-fonte e podem ser usados como estão ou como pontos de partida para componentes modificados ou estendidos.

### Componentes principais e Componentes de base {#core-components-and-foundation-components}

Há dois conjuntos de componentes AEM fornecidos pelo Adobe disponíveis:

* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Componentes de fundação](/help/sites-authoring/default-components-foundation.md)

Os **Componentes principais** foram introduzidos com o AEM 6.3 e oferecem funcionalidade de criação flexível e repleta de recursos. O [site de referência We.Retail](/help/sites-developing/we-retail.md) ilustra como os componentes principais podem ser usados e representa as práticas recomendadas atuais de desenvolvimento de componentes.

Os **Componentes de base** estão disponíveis com AEM para muitas versões e estão prontos para uso em uma instalação padrão do AEM. Embora ainda seja compatível, a maioria foi descontinuada, não está mais aprimorada e é baseada em tecnologias herdadas.

>[!NOTE]
>
>Os [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) representam as práticas recomendadas atuais para design e desenvolvimento de componentes e servem como implementações de referência.
>
>As [Ferramentas de modernização do AEM](modernization-tools.md) podem ajudar na migração para os Componentes principais.

### Visualização de componentes disponíveis {#viewing-available-components}

Para obter uma visão geral de todos os componentes disponíveis na instância do AEM, use o [Console de Componentes](/help/sites-authoring/default-components-console.md).

Como alternativa, você também pode usar o CRXDE Lite para obter uma lista de todos os componentes disponíveis no repositório.

1. No **[!UICONTROL CRXDE Lite]**, clique em **[!UICONTROL Ferramentas]** na barra de ferramentas e, em seguida, em **[!UICONTROL Consulta]** para abrir a guia **[!UICONTROL Consulta]**.

1. Na guia **[!UICONTROL Consulta]**, selecione `XPath` como **[!UICONTROL Tipo]**.

1. No campo de entrada **[!UICONTROL Consulta]**, digite a seguinte string:

   `//element(*, cq:Component)`

1. Clique em **[!UICONTROL Executar]** e os componentes serão listados.

## Recursos adicionais {#further-reading}

As páginas a seguir fornecem informações mais detalhadas sobre o desenvolvimento desses e de outros componentes:

* [Componentes do AEM - Noções básicas](/help/sites-developing/components-basics.md)
* [Desenvolvimento de componentes do AEM](/help/sites-developing/developing-components.md)
* [Desenvolvimento de componentes do AEM - Amostras de código](/help/sites-developing/developing-components-samples.md)
* [Configuração de vários editores no local](/help/sites-developing/multiple-inplace-editors.md)
* [Modo de desenvolvedor](/help/sites-developing/developer-mode.md)
* [Teste da interface do usuário](/help/sites-developing/hobbes.md)
* [Componentes para fragmentos de conteúdo](/help/sites-developing/components-content-fragments.md)
* [Obtendo informações de página no formato JSON](/help/sites-developing/pageinfo.md)
* [Internacionalizar componentes](/help/sites-developing/i18n.md)
* [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR)
* [Uso de condições de ocultação](/help/sites-developing/hide-conditions.md)
* IU Clássica

   * [Componentes do AEM (Interface clássica)](/help/sites-developing/developing-components-classic.md)
   * [Uso e extensão de widgets (interface de usuário clássica)](/help/sites-developing/widgets.md)
   * [Uso do xtypes (Interface clássica)](/help/sites-developing/xtypes.md)
   * [Desenvolvimento do Forms (interface clássica)](/help/sites-developing/developing-forms.md)
