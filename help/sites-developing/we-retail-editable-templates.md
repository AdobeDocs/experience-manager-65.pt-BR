---
title: Experimentar modelos editáveis no We.Retail
seo-title: Trying out Editable Templates in We.Retail
description: Saiba como experimentar Modelos editáveis no Adobe Experience Manager usando o We.Retail.
seo-description: null
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 9%

---

# Experimentar modelos editáveis no We.Retail{#trying-out-editable-templates-in-we-retail}

Com os modelos editáveis, criar e manter modelos não é mais uma tarefa somente para desenvolvedores. Um tipo de usuário avançado, chamado de autor de modelo, agora pode criar modelos. Os desenvolvedores ainda são necessários para configurar o ambiente, criar bibliotecas de clientes e criar os componentes a serem usados, mas uma vez que essas noções básicas estejam em vigor, o autor do modelo terá a flexibilidade de criar e configurar modelos sem um projeto de desenvolvimento.

Todas as páginas no We.Retail são baseadas em modelos editáveis, permitindo que não desenvolvedores adaptem e personalizem os modelos.

## Experimentando {#trying-it-out}

1. Edite a página Equipamento da ramificação de idioma principal.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Observe que o seletor de modo não oferece mais um modo Design. Todas as páginas para We.Retail são baseadas em modelos editáveis e, para alterar o design dos modelos editáveis, elas devem ser editadas no editor de modelos.
1. No **Informações da página** menu selecionar **Editar modelo**.
1. Agora você está editando o modelo da Página principal.

   O modo de estrutura da página permite modificar a estrutura do modelo. Isso inclui, por exemplo, os componentes permitidos no contêiner de layout.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configure as políticas para o Contêiner de layout para definir quais componentes são permitidos no contêiner.

   As políticas são equivalentes às configurações de design.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Na caixa de diálogo de design do contêiner de layout, é possível

   * Selecione uma política existente ou crie uma nova política para o container
   * Selecionar quais componentes são permitidos no contêiner
   * Definir os componentes padrão a serem colocados quando um ativo é arrastado para o contêiner

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. De volta ao editor de modelo, é possível editar a política do componente de texto no contêiner de layout.

   Isso permite:

   * Selecione uma política existente ou crie uma nova política para o container
   * Defina os recursos disponíveis para o autor da página ao usar esse componente, como

      * Fontes de colagem permitidas
      * Opções de formatação
      * Estilos de parágrafo permitidos
      * Caracteres especiais permitidos

   Muitos componentes baseados nos componentes principais permitem a configuração de opções no nível do componente por meio dos modelos editáveis, eliminando a necessidade de personalização pelos desenvolvedores.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. De volta ao editor de modelo, você pode usar o seletor de modo para alterar para **Conteúdo inicial** para definir qual conteúdo é necessário na página.

   **Layout** O modo pode ser usado como está em uma página normal para definir o layout do modelo.

## Mais informações {#more-information}

Para obter mais informações, consulte o documento de criação [Criação de modelos de página](/help/sites-authoring/templates.md) ou a página do documento do desenvolvedor [Modelos - Editáveis](/help/sites-developing/page-templates-editable.md) para obter detalhes técnicos completos sobre modelos editáveis.

Você também pode querer investigar [componentes principais](/help/sites-developing/we-retail-core-components.md). Consulte o documento de criação [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=pt-BR) para obter uma visão geral dos recursos dos componentes principais e o documento do desenvolvedor [Desenvolvimento dos Componentes principais](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) para obter uma visão geral técnica.
