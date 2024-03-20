---
title: Modelos de formulário adaptável
description: Crie modelos de formulário adaptáveis definindo a estrutura básica e o conteúdo do formulário inicial usando o Editor de modelos.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2030'
ht-degree: 1%

---

# Modelos de formulário adaptável{#adaptive-form-templates}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/template-editor.html) |
| AEM 6.5 | Este artigo |



Ao criar um formulário, você adiciona campos e componentes para definir a estrutura do formulário, o conteúdo e as ações no editor. Adicione campos e componentes na `guideRootPanel` do contêiner de formulário. Com o Editor de modelos, você pode criar um modelo que contenha estrutura básica e conteúdo inicial que os autores possam usar para criar formulários.

Por exemplo, você deseja que todos os autores de formulários tenham determinadas caixas de texto, botões de navegação e um botão de envio em um formulário de inscrição. Você pode criar um modelo com os componentes que os autores podem usar para criar um formulário consistente com outros formulários de inscrição. Quando os autores usam o modelo para criar um formulário adaptável, o novo formulário herda a estrutura e os componentes especificados no modelo. O Editor de modelos permite:

* Adicione componentes de cabeçalho e rodapé de um formulário na camada da estrutura.
* Forneça o conteúdo inicial para o formulário.
* Especifique um tema e envie as ações.

## Trabalhar com modelos {#working-with-templates}

É possível acessar o editor de modelos no menu Ferramentas navegando até **Adobe Experience Manager > Ferramentas > Modelos**. Aqui, os modelos são organizados em pastas ativadas para modelos editáveis. O AEM fornece uma pasta global para organizar modelos. No entanto, não está ativado por padrão. Você pode solicitar que o administrador ative a pasta global ou crie uma pasta para modelos. Para obter mais informações sobre como criar pastas, consulte [Pastas de Modelos](/help/sites-developing/page-templates-editable.md).

Depois de optar por abrir uma pasta, você verá um botão Criar que permite criar um modelo para formulários adaptáveis.

### Criação de um modelo {#create-template}

Após criar uma pasta, abra-a e execute as seguintes etapas para criar um template:

1. No console Modelo, selecione **Criar** dentro da pasta que você criou.
1. Na seção Escolher um tipo de modelo, selecione **Modelo de formulário adaptável** e selecione **Próxima**.

1. Na seção Detalhes do Modelo, forneça um Título de Modelo e selecione **Criar**.
Você pode fornecer uma descrição e uma miniatura que poderá ver quando selecionar o modelo criado no momento da criação do formulário.

1. Selecionar **Concluído** para retornar ao console ou selecione **Abertura** para abrir o modelo no editor.

### Interface do editor de modelos {#template-editor-ui}

Ao abrir um modelo para edição, você pode ver os seguintes componentes do Editor de AEM:

* **Barra de ferramentas da página**
Contém as seguintes opções:

   * **Ativar/desativar painel lateral**: permite mostrar ou ocultar a barra lateral.
   * **Informações da página**: permite especificar informações como tempo de publicação/cancelamento de publicação, miniaturas, bibliotecas do lado do cliente, política da página e biblioteca do lado do cliente de design da página.
   * **Emulador**: permite simular e personalizar a aparência para diferentes dispositivos.
   * **Seletor de camada:** Permite alterar a camada.
Você pode escolher **Estrutura** camada ou **Conteúdo inicial** camada. A camada de estrutura permite adicionar e personalizar o cabeçalho e o rodapé. A camada Conteúdo inicial permite personalizar o conteúdo do formulário.

   * **Visualizar:** Permite visualizar a aparência do modelo ao publicá-lo. Você pode usar o Seletor de camada e a Visualização para alternar entre os modos de edição e visualização.

* **Barra lateral:** Fornece os navegadores de Conteúdo, Propriedades, Ativos e Componentes.
* **Barra de ferramentas do componente:** Ao selecionar um componente, você vê uma barra de ferramentas que permite personalizar o componente.
* **Página**: a área onde você adiciona conteúdo para criar o template.

Consulte [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md) para entender o editor da interface para toque.

### Edição de um modelo {#editing-a-template}

Um modelo de formulário adaptável é criado usando duas camadas:

* Estrutura
* Conteúdo inicial

O seletor de camadas está disponível ao lado da opção Visualizar, no canto superior direito da tela.

### Estrutura {#structure}

Ao selecionar a camada de estrutura no Editor de modelo, você pode ver os contêineres de layout acima e abaixo do Contêiner de formulário adaptável. Os autores podem usar esses containers de layout para cabeçalho e rodapé. É possível adicionar, editar ou personalizar o cabeçalho e o rodapé. Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner de formulário adaptável para personalizar o cabeçalho do modelo. Arraste e solte o componente Rodapé do formulário adaptável no contêiner de layout abaixo do Contêiner de formulário adaptável para personalizar o rodapé do modelo.

![Contêiner de layout na camada da estrutura](assets/header-layer-selector.png)

Contêineres de layout na camada da estrutura

**A.** Contêiner de layout do componente de cabeçalho **B.** Contêiner de layout do componente de rodapé

Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner de formulário adaptável. Após adicionar o componente, é possível especificar suas propriedades, que permitem adicionar um logotipo e fornecer seu título.

Da mesma forma, ao arrastar e soltar o componente de rodapé no contêiner de layout abaixo do Contêiner de formulário adaptável, você pode fornecer as informações de direitos autorais e os detalhes da empresa.

![Cabeçalho e rodapé adicionados à camada Estrutura](assets/header-and-footer.png)

Cabeçalho e rodapé adicionados à camada Estrutura

#### Bloquear/desbloquear componentes na camada da estrutura {#locking-unlocking-components-in-the-structure-layer}

Ao editar o modelo com a camada de estrutura selecionada, é possível desbloquear o cabeçalho e o rodapé do modelo. Se um componente estiver desbloqueado no modelo, os autores de formulário poderão editar o componente no formulário adaptável que usa o modelo. Bloquear um componente impede que os autores do formulário o editem no formulário adaptável. A opção Bloquear está disponível na barra de ferramentas do componente.

Por exemplo, você adiciona o componente de cabeçalho no modelo. Ao selecionar o componente, você pode ver uma opção de bloqueio na barra de ferramentas do componente. Normalmente, o cabeçalho inclui o nome da empresa e o logotipo, e você não deseja que os autores de formulários alterem o logotipo e o cabeçalho em um modelo. Em um formulário adaptável criado usando o modelo com o componente de cabeçalho bloqueado, os autores de formulário não podem alterar o logotipo e o nome da empresa.

>[!NOTE]
>
>Não é recomendado bloquear ou desbloquear a imagem ou o logotipo no componente de cabeçalho, individualmente. Você pode desbloquear o componente de cabeçalho.

### Conteúdo inicial {#initial-content}

Quando a opção Conteúdo inicial estiver selecionada, o Contêiner de formulário adaptável do modelo será aberto como um formulário adaptável para edição. Assim como a criação de um formulário adaptável, você pode especificar configurações iniciais, como selecionar um tema e enviar ações.

Os autores de formulários o usam como base para criar um formulário. A estrutura do fluxo de conteúdo é especificada na camada Conteúdo inicial do modelo. Para alternar para a edição do conteúdo inicial do modelo de formulário, antes de Visualizar na barra de ferramentas da página, selecione ![tela suspensa](assets/canvas-drop-down.png) **> Conteúdo inicial**.
![Camada de conteúdo inicial no Editor de modelo](assets/initial-content-layer.png)

Camada de conteúdo inicial no Editor de modelos mostrando o Contêiner de formulário adaptável selecionado para especificar propriedades.

![conteúdo inicial](assets/initial-content-layer-1.png)

Na camada Conteúdo inicial, crie o modelo de formulário adaptável que seus autores usam como base. A criação de um modelo é semelhante à criação de um formulário. As opções disponíveis na Barra lateral são usadas. A barra lateral fornece conteúdo, propriedades, ativos e componentes nos navegadores.

Consulte [Barra lateral](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Ao selecionar Armazenar conteúdo ou Armazenar PDF como a Ação enviar, você obtém uma opção para especificar o Caminho de armazenamento. Se você especificar o caminho no modelo, todos os formulários criados a partir dele terão o mesmo caminho. Você pode especificar o caminho de armazenamento correto ou garantir que os autores do formulário o atualizem para impedir que os dados de cada formulário sejam armazenados no mesmo local.

#### Criação de um modelo de formulário adaptável com guias e painéis  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por exemplo, você deseja criar um modelo com as seguintes guias:

* Informações gerais
* Informações profissionais

Você adicionou um logotipo, forneceu um título e adicionou um rodapé na camada da estrutura. Bloqueie o cabeçalho e o rodapé para impedir que os autores dos formulários o editem quando usarem o modelo para criar formulários.

Altere a camada de Estrutura para Conteúdo inicial e comece a adicionar conteúdo ao formulário. Para criar uma estrutura com guias, adicione um Painel filho no guideRootPanel do contêiner de Formulário adaptável. Para adicionar um painel:

* Você pode adicionar um painel tocando no **+** ao selecionar a variável **Arraste os componentes para cá** opção.

* Você pode arrastar e soltar o componente Painel do navegador de componentes na barra lateral.
* É possível adicionar um painel filho de `guideRootPanel` na barra de ferramentas do componente.

Para criar as guias Informações gerais e Informações profissionais, adicione dois painéis no painel secundário do `guideRootPanel`. Selecione os painéis e selecione ![cmppr](assets/cmppr.png) para abrir as propriedades na barra lateral. Alterar os nomes dos elementos como `general-info` e `professional-info`e títulos como Informações gerais e Informações profissionais, respectivamente. Na barra lateral, selecione conteúdo para abrir o navegador de conteúdo. Na guia Objetos de formulário, selecione `guideRootPanel`. No editor, o guideRootPanel é selecionado. Selecionar ![cmppr](assets/cmppr.png) na barra de ferramentas do componente para abrir suas propriedades. No campo Layout do painel, selecione **Guias na parte superior** e selecione **Concluído**. A estrutura do modelo com guias é aplicada.

#### Adição de conteúdo em guias {#adding-content-in-tabs}

![Adição de campos no modelo de formulário adaptável](assets/template-edit-initial-content.png)

Depois de adicionar painéis e estruturá-los como guias, é possível adicionar campos dentro das guias. Ao selecionar uma guia no editor, você pode ver as **Arraste os componentes para cá** opção. Você pode arrastar e soltar componentes como caixas de texto, itens de lista e botões. Você pode arrastar e soltar componentes do navegador de componentes na barra lateral.

Cada componente tem propriedades que aprimoram a captura e a manipulação de dados. Por exemplo, é possível habilitar a variável **Campo obrigatório** propriedade de um componente. Os autores podem especificar uma mensagem que os clientes veem quando ignoram o preenchimento de um campo obrigatório. Especificar a mensagem em **Mensagem de campo obrigatório** propriedade.

No modelo de exemplo, os campos Name, Phone number e Date of birth são adicionados na guia General Information. Na guia Informações Profissionais, Atualmente empregado, são adicionados os campos Tipo de emprego, Qualificação educacional.

Após adicionar campos, é possível adicionar botões como Enviar e Redefinir.

### Habilitação do modelo {#enabling-the-template}

Ao criar um modelo, ele é adicionado como um rascunho. Habilite o modelo para usá-lo para criar formulários adaptáveis. Para ativar um modelo:

1. Navegue até **Adobe Experience Manager > Ferramentas > Modelos** e abra a pasta na qual você criou o template.

1. O modelo criado está marcado como Rascunho.
1. Selecione o modelo e selecione **Ativar** na barra de ferramentas.
Ao criar um formulário adaptável, você pode ver o modelo listado quando é solicitado a escolher um modelo.

## Importação ou exportação de um template {#importing-or-exporting-a-template}

Um formulário funciona com seu modelo. Ao baixar um formulário adaptável criado usando um modelo personalizado, o modelo não é baixado. Ao importar o formulário em uma instância diferente do AEM Forms, ele é importado sem seu template. Se um formulário for importado, mas seu template não estiver disponível, o formulário não será renderizado. É possível empacotar o modelo personalizado de `/conf` nó em `https://<server>:<port>/crx/packmgr`, e conecte-o à porta na instância do AEM Forms para onde deseja carregar o formulário.

## Criação de um formulário adaptável usando o modelo {#creating-an-adaptive-form-using-the-template}

Depois de criar e ativar um modelo, ele fica disponível no gerenciador de formulários quando você cria um formulário adaptável. Para usar um modelo e criar um formulário adaptável, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).

## Alterar opção de exibição de modelos prontos para uso  {#change-display-option-of-out-of-the-box-templates}

É possível criar modelos personalizados para formulários adaptáveis para definir a estrutura básica e o conteúdo inicial. O AEM Forms também fornece um conjunto de modelos prontos para uso para formulários adaptáveis. Você pode optar por mostrar ou ocultar os modelos.

Execute as seguintes etapas para mostrar e ocultar modelos:

1. Faça logon na instância de autor do AEM Forms e navegue até **Ferramentas** > **Operações** > **Console da Web**.

   >[!NOTE]
   >
   >A URL do console da web do AEM é https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Localize e abra o **Configuração do FormsManager** configurações:

   * Para mostrar ou ocultar o modelo de formulários adaptáveis pronto para uso, marque ou desmarque a opção **Incluir modelos AF e AD prontos para uso** opção.
   * Para mostrar ou ocultar modelos de formulário adaptável prontos para uso que foram adicionados nas versões do AEM 6.0 Forms ou do AEM 6.1 Forms, mas que agora estão obsoletas, marque ou desmarque a opção **Incluir modelos de AF do AEM 6.0** opção. Se essa opção estiver marcada, para ter efeito, ela exigirá a **Incluir modelos AF e AD prontos para uso** a ser habilitada.

1. Clique em **Salvar**. As opções de exibição para os templates prontos para uso são alteradas.

## Recomendações {#recommendations}

* Ao modificar as propriedades do formulário no editor de modelo, não use a propriedade BindReference.
* Caso queira adicionar um ponto de interrupção, crie-o ao criar um modelo de formulário adaptável.
Para obter mais informações sobre pontos de interrupção, consulte [Layout responsivo](/help/sites-authoring/responsive-layout.md).
