---
title: Configuração de componentes padrão no modo de design
description: Configuração de componentes no modo de design
uuid: b9c9792d-4398-446d-8767-44d4e7ce9a2e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 8ae6817a-16d3-4740-b67a-498e75adf350
exl-id: 5e232886-75c1-4f0f-b359-4739ae035fd3
source-git-commit: cae9890cd61d6d894f34c7299e2e15ee70e14ac9
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 1%

---

# Configuração de componentes padrão no modo de design{#configuring-components-in-design-mode}

Quando a instância do AEM é instalada imediatamente, uma seleção de componentes é disponibilizada imediatamente no navegador de componentes.

Além desses, vários outros componentes também estão disponíveis. Você pode usar o modo Design para [ativar/desativar esses componentes](#enable-disable-components). Quando ativado e localizado na sua página, você pode usar o modo Design para [configurar aspectos do design do componente](#configuring-the-design-of-a-component) editando os parâmetros de atributo.

>[!NOTE]
>
>Tenha cuidado ao editar esses componentes. As configurações de design são geralmente parte integrante do design de todo o site, portanto, elas só devem ser alteradas por alguém com os privilégios e a experiência apropriados, geralmente um administrador ou um desenvolvedor. Consulte [Desenvolvendo componentes](/help/sites-developing/components.md) para obter mais informações.

>[!NOTE]
>
>O modo Design está disponível somente para modelos estáticos. Os modelos criados com os modelos editáveis devem ser editados usando o [editor de modelo](/help/sites-authoring/templates.md).

>[!NOTE]
>
>O modo de design só está disponível para configurações de design armazenadas como conteúdo em ( `/etc`).
>
>A partir do AEM 6.4, é recomendável armazenar designs como dados de configuração em `/apps` para suportar cenários de implantação contínua. Designs armazenados em `/apps` não são editáveis em tempo de execução e o modo Design não estará disponível para usuários não administradores desses modelos.

Isso envolve adicionar ou remover os componentes permitidos no sistema de parágrafo da página. O sistema de parágrafos ( `parsys`) é um componente composto que contém todos os outros componentes de parágrafo. O sistema de parágrafo permite que os autores adicionem componentes de diferentes tipos a uma página, pois ela contém todos os outros componentes de parágrafo. Cada tipo de parágrafo é representado como um componente.

Por exemplo, o conteúdo de uma página de produto pode conter um sistema de parágrafo que contenha o seguinte:

* Uma imagem do produto (no formato de uma imagem ou de um parágrafo de imagem de texto)
* A descrição do produto (como um parágrafo de texto)
* Uma tabela com dados técnicos (como um parágrafo de tabela)
* Um formulário que os usuários preenchem (no início dos formulários, elemento de formulários e parágrafo final dos formulários)

>[!NOTE]
>
>Consulte [Desenvolvendo componentes](/help/sites-developing/components.md) e [Diretrizes para o uso de modelos e componentes](/help/sites-developing/dev-guidelines-bestpractices.md#guidelines-for-using-templates-and-components) para obter mais informações sobre `parsys`.

>[!CAUTION]
>
>A edição do design usando o Modo de design conforme descrito neste artigo é a maneira recomendada de definir designs de modelos estáticos
>
>A modificação de designs no CRX DE, por exemplo, não é a prática recomendada e a aplicação de tais designs pode variar do comportamento esperado. Consulte o documento do desenvolvedor [Modelos de página - Estáticos](/help/sites-developing/page-templates-static.md#how-template-designs-are-applied) para obter mais informações.

## Ativar/desativar componentes {#enable-disable-components}

Para ativar ou desativar um componente:

1. Selecione o **Design** modo.

   ![screen_shot_2018-03-22at103113](assets/screen_shot_2018-03-22at103113.png)

1. Toque ou clique em um componente. O componente terá uma borda azul quando selecionado.

   ![screen_shot_2018-03-22at103204](assets/screen_shot_2018-03-22at103204.png)

1. Clique ou toque no **Pai** ícone.

   ![Pai](do-not-localize/screen_shot_2018-03-22at103204.png)

   Isso selecionará o sistema de parágrafo que contém o componente atual.

1. A variável **Configurar** O ícone do sistema de parágrafo será mostrado na barra de ação do pai.

   ![Configurar](do-not-localize/screen_shot_2018-03-22at103256.png)

   Selecione esta opção para mostrar a caixa de diálogo.

1. Use a caixa de diálogo para definir os componentes disponíveis no navegador de componentes ao editar a página atual.

   ![screen_shot_2018-03-22at103329](assets/screen_shot_2018-03-22at103329.png)

   A caixa de diálogo tem duas guias:

   * Componentes permitidos
   * Configurações

   **Componentes permitidos**

   No **Componentes permitidos** você define quais componentes estão disponíveis para o parsys.

   * Os componentes são agrupados por seus grupos de componentes, que podem ser expandidos e recolhidos.
   * Um grupo inteiro pode ser selecionado, marcando o nome do grupo, e todos podem ser desmarcados ao desmarcar.
   * Um sinal de menos representa pelo menos um, mas não todos os itens em um grupo são selecionados.
   * Há uma pesquisa disponível para filtrar um componente por nome.
   * As contagens listadas à direita do nome do grupo de componentes representam o número total de componentes selecionados nesses grupos, independentemente do filtro.

   Você define a configuração por componente de página. Se as páginas secundárias usarem o mesmo modelo e/ou componente de página (geralmente alinhado), a mesma configuração será aplicada ao sistema de parágrafo correspondente.

   >[!NOTE]
   >
   >Os componentes do formulário adaptável são projetados para funcionar dentro do Contêiner de formulário adaptável para aproveitar o ecossistema do Forms. Portanto, esses componentes devem ser usados somente no editor de formulário adaptável e não funcionarão no editor de páginas do Sites.

   **Configurações**

   No **Configurações** guia é possível definir opções adicionais, como desenhar uma âncora para cada componente e definir o preenchimento da célula de cada contêiner.

1. Selecionar **Concluído** para salvar sua configuração.

## Configuração do design de um componente {#configuring-the-design-of-a-component}

1. Selecione o **Design** modo.

   ![screen_shot_2018-03-22at103113-1](assets/screen_shot_2018-03-22at103113-1.png)

1. Toque ou clique em um componente com uma borda azul. Neste exemplo, um componente de imagem herói é selecionado.

   ![screen_shot_2018-03-22at103434](assets/screen_shot_2018-03-22at103434.png)

1. Use o **Configurar** ícone para abrir o diálogo.

   ![Ícone Configurar](do-not-localize/screen_shot_2018-03-22at103256-1.png)

   Na caixa de diálogo de design, é possível configurar o componente de acordo com os parâmetros de design disponíveis.

   ![screen_shot_2018-03-22at103530](assets/screen_shot_2018-03-22at103530.png)

   A caixa de diálogo tem três guias:

   * Principal
   * Recursos
   * Estilos

   **Propriedades**

   A variável **Propriedades** permite configurar os parâmetros de design importantes do componente. Por exemplo, para um componente de imagem, é possível definir o tamanho máximo e mínimo da imagem permitida.

   **Recursos**

   A variável **Recursos** permite ativar ou desativar recursos adicionais do componente. Por exemplo, para um componente de imagem, é possível definir a orientação da imagem, as opções de corte disponíveis e se uma imagem pode ser carregada.

   **Estilos**

   A variável **Estilos** permite definir as classes e os estilos CSS a serem usados com o componente.

   ![screen_shot_2018-03-22at103741](assets/screen_shot_2018-03-22at103741.png)

   Use o **Adicionar** botão para adicionar entradas adicionais a uma lista de caixas de diálogo de várias entradas.

   ![chlimage_1-94](assets/chlimage_1-94.png)

   Use o **Excluir** ícone para remover uma entrada de uma lista de caixas de diálogo de várias entradas.

   ![Excluir](do-not-localize/screen_shot_2018-03-22at103809.png)

   Use o **Mover** ícone para reorganizar a ordem das entradas em uma lista de caixas de diálogo de várias entradas.

   ![Mover](do-not-localize/screen_shot_2018-03-22at103816.png)

1. Clique ou toque no **Concluído** ícone para salvar e fechar o diálogo.
