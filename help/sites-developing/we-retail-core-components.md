---
title: Experimente os componentes principais no We.Retail
seo-title: Experimente os componentes principais no We.Retail
description: 'null'
seo-description: nulo
uuid: 8d1cea0b-99d9-49b2-b275-41f14864b1ff
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: af3cd818-61cf-4da1-bfb5-87540911ddd5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---


# Experimente os componentes principais em We.Retail{#trying-out-core-components-in-we-retail}

Os componentes principais são componentes modernos e flexíveis, com fácil extensibilidade e que permitem uma integração simples em seus projetos. Os componentes principais foram criados com base em vários princípios principais de design, como HTL, usabilidade imediata, configuração, controle de versão e extensibilidade. We.Retail foi construído com base em componentes principais.

## Tentando sair {#trying-it-out}

1. Start AEM com o conteúdo de amostra We.Retail e abra o [console Componentes](/help/sites-authoring/default-components-console.md).

   **Navegação global -> Ferramentas -> Componentes**

1. Ao abrir o painel no console Componentes, você pode filtrar por um grupo específico de componentes. Os componentes principais podem ser encontrados em

   * `.core-wcm`: Os componentes principais padrão
   * `.core-wcm-form`: Os componentes principais de envio do formulário

   Choose `.core-wcm`.

   ![chlimage_1-162](assets/chlimage_1-162.png)

1. Observe que todos os componentes principais são nomeados como **v1**, refletindo que esta é a primeira versão desse componente principal. Versões regulares serão lançadas a partir de agora, o que será compatível com a versão e permitirá uma atualização fácil, para que você possa aproveitar os recursos mais recentes.
1. Clique em **Texto (v1)**.

   Verifique se **Tipo de Recurso** do componente é `/apps/core/wcm/components/text/v1/text`. Os componentes principais são encontrados em `/apps/core/wcm/components` e têm controle de versão por componente.

   ![chlimage_1-163](assets/chlimage_1-163.png)

1. Clique na guia **Documentação** para ver a documentação do desenvolvedor do componente.

   ![chlimage_1-164](assets/chlimage_1-164.png)

1. Retorne ao console Componentes. Filtre pelo grupo **We.Retail** e selecione o componente **Text**.
1. Verifique se **Tipo de Recurso** aponta para um componente conforme esperado em `/apps/weretail`, mas o **Supertipo de Recurso** aponta de volta para o componente principal `/apps/core/wcm/components/text/v1/text`.

   ![chlimage_1-165](assets/chlimage_1-165.png)

1. Clique na guia **Uso ao vivo** para ver em quais páginas esse componente está sendo usado no momento. Clique na primeira página **Obrigado** para editar a página.

   ![chlimage_1-166](assets/chlimage_1-166.png)

1. Na página Obrigado, selecione o componente de texto e, no menu de edição do componente, clique no ícone Cancelar herança.

   [We.Retail tem uma estrutura de site globalizada ](/help/sites-developing/we-retail-globalized-site-structure.md) onde o conteúdo é enviado de mestres de linguagem para cópias  [ao vivo por meio de um mecanismo chamado herança](/help/sites-administering/msm.md). Por esse motivo, a herança deve ser cancelada para permitir que um usuário edite texto manualmente.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme o cancelamento clicando em **Yes**.

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Após a herança ser cancelada e você selecionar os componentes de texto, muitas outras opções estarão disponíveis. Clique em** Editar**.

   ![chlimage_1-169](assets/chlimage_1-169.png)

1. Agora você pode ver quais opções de edição estão disponíveis para o componente de texto.

   ![chlimage_1-170](assets/chlimage_1-170.png)

1. No menu **Informações da página**, selecione **Editar modelo**.
1. No Editor de modelos da página, clique no ícone **Política** do componente Texto no **Container de layout** da página.

   ![chlimage_1-171](assets/chlimage_1-171.png)

1. Os componentes principais permitem que um autor de modelo configure quais Propriedades estão disponíveis para os autores da página. Isso inclui recursos como fontes de colagem permitidas, opções de formatação, estilos de parágrafo disponíveis etc.

   Essas caixas de diálogo de design estão disponíveis para muitos componentes principais e funcionam lado a lado com o editor de modelo. Depois de ativados, eles ficam disponíveis para o autor por meio dos editores de componentes.

   ![chlimage_1-172](assets/chlimage_1-172.png)

## Informações adicionais {#further-information}

Para obter mais informações sobre os componentes principais, consulte o documento de criação [Componentes principais](https://docs.adobe.com/content/help/pt-BR/experience-manager-core-components/using/introduction.html) para obter uma visão geral dos recursos dos componentes principais e do documento de desenvolvedor [Desenvolvimento dos componentes principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obter uma visão geral técnica.

Além disso, talvez você queira investigar mais sobre [modelos editáveis](/help/sites-developing/we-retail-editable-templates.md). Consulte o documento de criação [Criando Modelos de Página](/help/sites-authoring/templates.md) ou a Página de documentos do desenvolvedor [Modelos - Editável](/help/sites-developing/page-templates-editable.md) para obter detalhes completos sobre modelos editáveis.
