---
title: Como experimentar os Componentes principais no We.Retail
seo-title: Trying out Core Components in We.Retail
description: Como experimentar os Componentes principais no We.Retail
seo-description: null
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
exl-id: b5f2be67-c93c-4dbc-acc0-3edd8f1a282f
source-git-commit: b886844dc80482ae4aae5fc7ce09e466efecc3bd
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 1%

---

# Como experimentar os Componentes principais no We.Retail{#trying-out-core-components-in-we-retail}

Os componentes principais são componentes modernos e flexíveis, com fácil extensibilidade e permitindo uma integração simples em seus projetos. Os componentes principais foram criados em torno de vários princípios importantes de design, como HTL, usabilidade pronta para uso, configurabilidade, controle de versão e extensibilidade. O We.Retail foi criado em componentes principais.

## Tentando {#trying-it-out}

1. Inicie o AEM com o conteúdo de amostra We.Retail e abra o [Console de componentes](/help/sites-authoring/default-components-console.md).

   **Navegação global -> Ferramentas -> Componentes**

1. Ao abrir o painel no console Componentes, é possível filtrar por um grupo de componentes específico. Os componentes principais podem ser encontrados em

   * `.core-wcm`: Os componentes principais padrão
   * `.core-wcm-form`: Os componentes principais de envio do formulário

   Choose `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Observe que todos os componentes principais são nomeados **v1**, refletindo que esta é a primeira versão desse componente principal. As versões regulares serão lançadas a partir de agora, o que será compatível com a versão do AEM e permitirá uma atualização fácil para que você possa aproveitar os recursos mais recentes.
1. Clique em **Texto (v1)**.

   Veja que a variável **Tipo de recurso** do componente é `/apps/core/wcm/components/text/v1/text`. Os componentes principais são encontrados em `/apps/core/wcm/components` e são controle de versão por componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clique no botão **Documentação** para ver a documentação do desenvolvedor do componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Retorne ao Console de componentes. Filtro para o grupo **We.Retail** e selecione o **Texto** componente.
1. Veja que a variável **Tipo de recurso** aponta para um componente conforme esperado em `/apps/weretail` mas o **Supertipo de Recurso** aponta para o componente principal `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Clique no botão **Uso em tempo real** para ver em quais páginas esse componente está sendo usado no momento. Clique no primeiro **Obrigado** para editar a página.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Na página Obrigado, selecione o componente de texto e, no menu de edição do componente, clique no ícone Cancelar herança .

   [We.Retail tem uma estrutura de site globalizada](/help/sites-developing/we-retail-globalized-site-structure.md) onde o conteúdo é enviado dos mestres de linguagem para [live copies por meio de um mecanismo chamado herança](/help/sites-administering/msm.md). Por esse motivo, a herança deve ser cancelada para permitir que um usuário edite texto manualmente.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme o cancelamento clicando em **Sim**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Depois que a herança é cancelada e você seleciona os componentes de texto, muitas outras opções estão disponíveis. Clique em** Editar**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Agora é possível ver quais opções de edição estão disponíveis para o componente de texto.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. No **Informações da página** selecionar menu **Editar modelo**.
1. No Editor de modelo da página, clique no **Política** ícone do componente de Texto na **Contêiner de layout** da página.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Os componentes principais permitem que um autor de modelo configure quais propriedades estão disponíveis para os autores da página. Isso inclui recursos como fontes de colagem permitidas, opções de formatação, estilos de parágrafo disponíveis, etc.

   Essas caixas de diálogo de design estão disponíveis para muitos componentes principais e funcionam lado a lado com o editor de modelo. Uma vez ativadas, elas ficam disponíveis para o autor por meio dos editores de componente.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Informações adicionais {#further-information}

Para obter mais informações sobre os componentes principais, consulte o documento de criação [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) para obter uma visão geral dos recursos dos componentes principais e o documento do desenvolvedor [Desenvolvimento dos componentes principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obter uma visão geral técnica.

Além disso, você pode querer investigar mais detalhadamente [modelos editáveis](/help/sites-developing/we-retail-editable-templates.md). Consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md) ou a página do documento do desenvolvedor [Modelos - Editáveis](/help/sites-developing/page-templates-editable.md) para obter detalhes completos sobre modelos editáveis.
