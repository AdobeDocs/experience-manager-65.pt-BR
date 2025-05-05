---
title: Experimentar os Componentes principais no We.Retail
description: Saiba como experimentar os Componentes principais no Adobe Experience Manager usando o We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Experimentar os Componentes principais no We.Retail{#trying-out-core-components-in-we-retail}

Os componentes principais são componentes modernos e flexíveis, com fácil extensibilidade e permitindo uma integração simples em seus projetos. Os componentes principais foram criados com base em vários princípios principais de design, como HTL, usabilidade pronta para uso, configurabilidade, controle de versão e extensibilidade. O We.Retail foi criado com base em componentes principais.

## Experimentando {#trying-it-out}

1. Inicie o Adobe Experience Manager (AEM) com o conteúdo de amostra We.Retail e abra o [Console de Componentes](/help/sites-authoring/default-components-console.md).

   **Navegação Global > Ferramentas > Componentes**

1. Ao abrir o painel no console Componentes, você pode filtrar por um grupo de componentes específico. Os componentes principais podem ser encontrados em

   * `.core-wcm`: os componentes principais padrão
   * `.core-wcm-form`: os componentes principais de envio de formulário

   Escolha `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Todos os componentes principais são nomeados como **v1**, refletindo que esta é a primeira versão deste componente principal. As versões regulares serão lançadas a partir de agora, que serão compatíveis com a versão do AEM e permitirão uma atualização fácil para que você possa aproveitar os recursos mais recentes.
1. Clique em **Texto (v1)**.

   Veja se o **Tipo de Recurso** do componente é `/apps/core/wcm/components/text/v1/text`. Os componentes principais são encontrados em `/apps/core/wcm/components` e sua versão é feita por componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clique na guia **Documentação** para ver a documentação do desenvolvedor do componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Retorne ao console Componentes. Filtre o grupo **We.Retail** e selecione o componente **Text**.
1. Veja se o **Tipo de Recurso** aponta para um componente como esperado em `/apps/weretail`, mas o **Supertipo de Recurso** aponta de volta para o componente principal `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Clique na guia **Uso em tempo real** para ver em quais páginas este componente está sendo usado. Clique na primeira página **Obrigado** para editar a página.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Na página Obrigado, selecione o componente de texto e, no menu de edição do componente, clique no ícone Cancelar herança.

   [We.Retail tem uma estrutura de site globalizada](/help/sites-developing/we-retail-globalized-site-structure.md) onde o conteúdo é enviado por push dos mestres de idioma para [live copies por um mecanismo chamado herança](/help/sites-administering/msm.md). Por esse motivo, a herança deve ser cancelada para permitir que um usuário edite o texto manualmente.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme o cancelamento clicando em **Sim**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Quando a herança for cancelada e você selecionar os componentes de texto, muitas outras opções estarão disponíveis. Clique em **Editar**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Agora você pode ver quais opções de edição estão disponíveis para o componente de texto.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. No menu **Informações da página**, selecione **Editar modelo**.
1. No Editor de Modelo da página, clique no ícone **Política** do componente Texto no **Contêiner de Layout** da página.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Os componentes principais permitem que um autor do modelo configure quais Propriedades estão disponíveis para os autores da página. Isso inclui recursos como fontes de colagem permitidas, opções de formatação e estilos de parágrafo disponíveis.

   Essas caixas de diálogo de design estão disponíveis para muitos componentes principais e funcionam lado a lado com o editor de modelo. Depois de ativadas, elas ficam disponíveis para o autor por meio dos editores de componentes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Informações adicionais {#further-information}

Para obter mais informações sobre os componentes principais, consulte o documento de criação [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) para obter uma visão geral dos recursos dos componentes principais, e o documento do desenvolvedor [Desenvolvendo componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=pt-BR) para obter uma visão geral técnica.

Além disso, investigue mais detalhadamente [modelos editáveis](/help/sites-developing/we-retail-editable-templates.md). Consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md) ou o documento do desenvolvedor Página [Modelos - Editáveis](/help/sites-developing/page-templates-editable.md) para obter detalhes completos sobre modelos editáveis.
