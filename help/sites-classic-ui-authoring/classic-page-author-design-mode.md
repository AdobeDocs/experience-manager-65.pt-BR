---
title: Configuração dos componentes no Modo de design
seo-title: Configuring Components in Design Mode
description: Quando a instância do AEM é instalada prontamente, uma seleção de componentes é disponibilizada imediatamente no sidekick. Além destes, outros componentes também estarão disponíveis. Você pode usar o Modo de design para Ativar/Desativar tais componentes.
seo-description: When AEM instance is installed out-of-the-box, a selection of components are immediately available in the sidekick. In addition to these, various other components are also available. You can use Design mode to Enable/disable such components.
uuid: 2cd5dad0-2f9c-4f34-aae8-1638d1445eb3
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 10466b49-f8bd-4c2c-8106-b0c7ba054989
docset: aem65
exl-id: cb2d2d0d-feb4-4b89-8325-80f735816904
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 92%

---

# Configuração dos componentes no Modo de design{#configuring-components-in-design-mode}

Quando a instância do AEM é instalada prontamente, uma seleção de componentes é disponibilizada imediatamente no sidekick.

Além destes, outros componentes também estarão disponíveis. Você pode usar o Modo de design para [Ativar/Desativar tais componentes](#enabledisablecomponentsusingdesignmode). Quando ativado e localizado em sua página, você poderá usar o Modo de design para [configurar os aspectos de design do componente](#configuringcomponentsusingdesignmode) através da edição dos parâmetros do atributo.

>[!NOTE]
>
>Alguns cuidados devem ser tomados ao editar esses componentes. As configurações de design muitas vezes são uma parte integrante do design de todo o site, por isso só devem ser alteradas por alguém com os privilégios adequados (e experiência), normalmente um administrador ou desenvolvedor. Consulte [Desenvolvimento de componentes](/help/sites-developing/components.md) para obter mais informações.

Na verdade, isso envolve adicionar ou remover os componentes permitidos no sistema de parágrafo da página. O sistema de parágrafo (`parsys`) é um componente composto que contém todos os outros componentes de parágrafo. O sistema de parágrafo permite aos autores adicionar componentes de diferentes tipos em uma página, pois contêm todos os outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente.

Por exemplo, o conteúdo de uma página de produto pode conter um sistema de parágrafo com o seguinte:

* Uma imagem do produto (na forma de uma imagem ou de um parágrafo de imagem e texto)
* A descrição do produto (como um parágrafo de texto)
* Uma tabela com os dados técnicos (como um parágrafo de tabela)
* Um formulário para os usuários preencherem (como formas de começar, formas de elemento e formas de parágrafo final)

>[!NOTE]
>
>Consulte [Desenvolvimento de componentes](/help/sites-developing/components.md#paragraphsystem) e [diretrizes para o uso de modelos e componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obter mais informações sobre o `parsys`.

## Desativar/Ativar componentes {#enable-disable-components}

No modo de Design, o sidekick é minimizado e você tem a possibilidade de configurar os componentes acessíveis para a criação:

1. Para entrar no modo de Design, abra uma página de edição e use o ícone Sidekick:

   ![](do-not-localize/chlimage_1.png)

1. Clique em **Editar** sobre o sistema de parágrafo (**Concepção do par**).

   ![screen_shot_2012-02-08at102726am](assets/screen_shot_2012-02-08at102726am.png)

1. Uma caixa de diálogo será aberta, listando os grupos de componentes que são mostrados no Sidekick, juntamente com os componentes individuais que eles contêm.

   Selecione conforme necessário para adicionar, ou remover, os componentes que estarão disponíveis no sidekick.

   ![screen_shot_2012-02-08at103407am](assets/screen_shot_2012-02-08at103407am.png)

1. O Sidekick é minimizado no modo Design. Ao clicar na seta, você pode maximizar o Sidekick e retornar ao modo Editar:

   ![](do-not-localize/sidekick-collapsed.png)

## Configuração do design de um componente {#configuring-the-design-of-a-component}

No modo Design, também é possível configurar os atributos para os componentes individuais. Cada componente tem seus próprios parâmetros, o exemplo a seguir mostra o componente de **Imagem**:

1. Para entrar no modo de Design, abra uma página de edição e use o ícone Sidekick:

   ![](do-not-localize/chlimage_1-1.png)

1. É possível configurar o design dos componentes.

   Por exemplo, se você clicar em **Editar** no componente Imagem (**Design da imagem**) você pode configurar os parâmetros específicos do componente:

   ![chlimage_1-5](assets/chlimage_1-5.png)

1. Clique em **OK** para salvar suas alterações.

1. O Sidekick é minimizado no modo Design. Ao clicar na seta, você pode maximizar o Sidekick e retornar ao modo Editar:

   ![](do-not-localize/sidekick-collapsed-1.png)
