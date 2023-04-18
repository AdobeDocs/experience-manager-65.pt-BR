---
title: Configuração de componentes padrão no Modo Design
description: Configuração de componentes no modo de design
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 1%

---

# Configuração de componentes padrão no Modo Design{#configuring-components-in-design-mode}

Quando AEM instância é instalada e pronta para uso, uma seleção de componentes é disponibilizada imediatamente no navegador de componentes.

Além disso, vários outros componentes também estão disponíveis. Você pode usar o Modo de design para [ativar/desativar tais componentes](#enable-disable-components). Quando ativado e localizado na página, você pode usar o Modo de design para [configurar os aspectos do design do componente](#configuring-the-design-of-a-component) editando os parâmetros do atributo.

>[!NOTE]
>
>Deve-se ter cuidado ao editar esses componentes. As configurações de design muitas vezes são parte integrante do design de todo o site, por isso só devem ser alteradas por alguém com os privilégios e experiência apropriados, geralmente um administrador ou desenvolvedor. Consulte [Componentes de desenvolvimento](/help/sites-developing/components.md) para obter mais informações.

>[!NOTE]
>
>O modo Design só está disponível para modelos estáticos. Os modelos que são criados com modelos editáveis devem ser editados usando o [editor de modelos](/help/sites-authoring/templates.md).

>[!NOTE]
>
>O modo Design só está disponível para configurações de design armazenadas como conteúdo em ( `/etc`).
>
>A partir do AEM 6.4, é recomendável armazenar designs como dados de configuração no `/apps` para oferecer suporte a cenários de implantação contínua. Designs armazenados em `/apps` não são editáveis no tempo de execução e o modo Design não estará disponível para usuários não administradores nesses modelos.

Isso envolve adicionar ou remover os componentes permitidos no sistema de parágrafo da página. O sistema de parágrafo ( `parsys`) é um componente composto que contém todos os outros componentes de parágrafo. O sistema de parágrafo permite que os autores adicionem componentes de tipos diferentes a uma página, pois contêm todos os outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente.

Por exemplo, o conteúdo de uma página de produto pode conter um sistema de parágrafo com o seguinte:

* Uma imagem do produto (na forma de uma imagem ou de um parágrafo de imagem)
* A descrição do produto (como um parágrafo de texto)
* Uma tabela com dados técnicos (como parágrafo de tabela)
* Um formulário preenchido pelos usuários (como um formulário começa, um elemento de formulário e um parágrafo final de formulário)

>[!NOTE]
>
>Consulte [Componentes de desenvolvimento](/help/sites-developing/components.md) e [Diretrizes para usar modelos e componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obter mais informações sobre `parsys`.

>[!CAUTION]
>
>Editar o design usando o Modo Design conforme descrito neste artigo é a maneira recomendada de definir designs de modelos estáticos
>
>A modificação de designs no CRX DE, por exemplo, não é uma prática recomendada e a aplicação desses designs pode variar do comportamento esperado. Consulte o documento do desenvolvedor [Modelos de página - Estático](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) para obter mais informações.

## Ativar/desativar componentes {#enable-disable-components}

Para ativar ou desativar um componente:

1. Selecione o **Design** modo.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Toque ou clique em um componente. O componente terá uma borda azul quando selecionado.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Clique ou toque no **Pai** ícone .

   ![](do-not-localize/screen_shot_2018-03-22at103204.png)

   Isso selecionará o sistema de parágrafo que contém o componente atual.

1. O **Configurar** ícone para o sistema de parágrafo será mostrado na barra de ação do pai.

   ![](do-not-localize/screen_shot_2018-03-22at103256.png)

   Selecione esta opção para mostrar a caixa de diálogo.

1. Use a caixa de diálogo para definir os componentes disponíveis no navegador de componentes ao editar a página atual.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   A caixa de diálogo tem duas guias:

   * Componentes permitidos
   * Configurações

   **Componentes permitidos**

   No **Componentes permitidos** , você define quais componentes estão disponíveis para o parsys.

   * Os componentes são agrupados por seus grupos de componentes, que podem ser expandidos e recolhidos.
   * Um grupo inteiro pode ser selecionado, marcando o nome do grupo e todos podem ser desmarcados, desmarcando.
   * Um sinal de menos representa pelo menos um, mas não todos os itens em um grupo são selecionados.
   * Uma pesquisa está disponível para filtrar um componente por nome.
   * As contagens listadas à direita do nome do grupo de componentes representam o número total de componentes selecionados nesses grupos, independentemente do filtro.

   A configuração é definida por componente de página. Se as páginas filhas usarem o mesmo modelo e/ou componente de página (normalmente alinhado), a mesma configuração será aplicada ao sistema de parágrafo correspondente.

   >[!NOTE]
   >
   >Os componentes de formulário adaptável são projetados para funcionar dentro do Contêiner de formulário adaptável para aproveitar o ecossistema do Forms. Portanto, esses componentes devem ser usados somente no editor de formulário adaptável e não funcionarão no editor de páginas do Sites.

   **Configurações**

   No **Configurações** é possível definir opções adicionais, como para desenhar uma âncora para cada componente e definir o preenchimento da célula de cada contêiner.

1. Selecionar **Concluído** para salvar sua configuração.

## Configuração do design de um componente {#configuring-the-design-of-a-component}

1. Selecione o **Design** modo.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Toque ou clique em um componente com uma borda azul. Neste exemplo, um componente de imagem herói é selecionado.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Use o **Configurar** para abrir a caixa de diálogo.

   ![](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Na caixa de diálogo de design, é possível configurar o componente de acordo com os parâmetros de design disponíveis.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   A caixa de diálogo tem três guias:

   * Principal
   * Recursos
   * Estilos

   **Propriedades**

   O **Propriedades** permite configurar os parâmetros de design importantes do componente. Por exemplo, para um componente de imagem, você pode definir o tamanho máximo e mínimo da imagem permitida.

   **Recursos**

   O **Recursos** permite ativar ou desativar recursos adicionais do componente. Por exemplo, para um componente de imagem, você pode definir a orientação da imagem, as opções de corte disponíveis e se uma imagem pode ser carregada.

   **Estilos**

   O **Estilos** permite definir as classes e os estilos de CSS a serem usados com o componente.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Use o **Adicionar** para adicionar mais entradas a uma lista de diálogo de várias entradas.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Use o ícone** Excluir **para remover uma entrada de uma lista de diálogo de várias entradas.

   ![](do-not-localize/screen_shot_2018-03-22at103809.png)

   Use o **Mover** ícone para reorganizar a ordem de entradas em uma lista de diálogo de várias entradas.

   ![](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Clique ou toque no **Concluído** para salvar e fechar a caixa de diálogo.
