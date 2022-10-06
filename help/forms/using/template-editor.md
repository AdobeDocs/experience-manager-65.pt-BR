---
title: Modelos de formulário adaptável
seo-title: Adaptive Form Templates
description: Crie modelos de formulário adaptáveis definindo a estrutura básica e o conteúdo do formulário inicial usando o Editor de modelos.
seo-description: Create adaptive form templates by defining the basic structure and initial form content using the Template Editor.
uuid: 317ca3ab-f809-49a7-a063-9d0c17a35fe4
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b21a48ba-eccd-4bb5-9b92-3039026ddf2a
docset: aem65
feature: Adaptive Forms
exl-id: d7287ee7-fb4e-4d47-b37e-0a9260344070
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 0%

---

# Modelos de formulário adaptável{#adaptive-form-templates}

Ao criar um formulário, você adiciona campos e componentes para definir a estrutura, o conteúdo e as ações do formulário no editor. Você adiciona campos e componentes na `guideRootPanel` do contêiner de formulário. Com o Editor de modelo, é possível criar um modelo que contenha a estrutura básica e o conteúdo inicial que os autores podem usar para criar formulários.

Por exemplo, você deseja que todos os autores de formulários tenham determinadas caixas de texto, botões de navegação e um botão Enviar em um formulário de inscrição. É possível criar um modelo com os componentes que os autores podem usar para criar um formulário consistente com outros formulários de inscrição. Quando os autores usam o modelo para criar um formulário adaptável, o novo formulário herda a estrutura e os componentes especificados no modelo. O Editor de modelos permite:

* Adicione componentes de cabeçalho e rodapé de um formulário na camada de estrutura.
* Forneça o conteúdo inicial do formulário.
* Especifique um tema, envie ações.

## Trabalhar com modelos {#working-with-templates}

Você pode acessar o editor de modelos no menu Ferramentas navegando até **Adobe Experience Manager > Ferramentas > Modelos**. Aqui, os modelos são organizados em pastas habilitadas para modelos editáveis. AEM fornece uma pasta global para organizar templates. No entanto, não está ativado por padrão. Você pode solicitar ao Administrador que ative a pasta global ou crie uma nova pasta para modelos. Para obter mais informações sobre como criar pastas, consulte [Pastas de modelo](/help/sites-developing/page-templates-editable.md).

Depois de tocar em para abrir uma pasta, você encontrará um botão Criar que permite criar um novo modelo para formulários adaptáveis.

### Criação de um modelo {#create-template}

Depois de criar uma pasta, abra-a e execute as seguintes etapas para criar um template:

1. No console Modelo , toque em **Criar** na pasta que você criou.
1. Na seção Selecionar um tipo de modelo , selecione **Modelo de formulário adaptável** e tocar **Próximo**.

1. Na seção Detalhes do modelo , forneça um Título de modelo e toque em **Criar**.
Você pode fornecer uma descrição e uma miniatura que podem ser exibidas quando é possível selecionar o modelo criado no momento da criação do formulário.

1. Toque **Concluído** para retornar ao console ou toque em **Abrir** para abrir o template no editor.

### Interface do usuário do editor de modelos {#template-editor-ui}

Ao abrir um modelo para edição, você pode ver os seguintes componentes do Editor de AEM:

* **Barra de ferramentas da página**
Contém as seguintes opções:

   * **Alternar painel lateral**: Permite mostrar ou ocultar a barra lateral.
   * **Informações da página**: Permite que você especifique informações como o tempo de publicação/cancelamento de publicação, miniaturas, bibliotecas do lado do cliente, política de página e biblioteca do lado do cliente de design de página.
   * **Emulador**: Permite simular e personalizar a busca de dispositivos diferentes.
   * **Seletor de camada:** Permite alterar a camada.
Você pode escolher **Estrutura** camada ou **Conteúdo inicial** camada. A camada Estrutura permite adicionar e personalizar o cabeçalho e o rodapé. A camada Conteúdo inicial permite personalizar o conteúdo do formulário.

   * **Visualizar:** Permite que você visualize a aparência do modelo ao publicá-lo. Você pode usar o Seletor de camada e a Visualização para alternar os modos de edição e visualização.

* **Barra lateral:** Fornece os navegadores de Conteúdo, Propriedades, Ativos e Componentes.
* **Barra de ferramentas do componente:** Ao selecionar um componente, você verá uma barra de ferramentas que permite personalizar o componente.
* **Página**: A área onde você adiciona conteúdo para criar o modelo.

Consulte [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md) para entender o editor da interface de toque.

### Edição de um modelo {#editing-a-template}

Um modelo de formulário adaptável é criado usando duas camadas:

* Estrutura
* Conteúdo inicial

O seletor de camada está disponível ao lado da opção Visualização no canto superior direito da tela.

### Estrutura {#structure}

Ao selecionar a camada de estrutura no Editor de modelo, é possível ver os contêineres de layout acima e abaixo do Contêiner de formulário adaptável. Os autores podem usar esses contêineres de layout para cabeçalho e rodapé. Você pode adicionar, editar ou personalizar o cabeçalho e o rodapé. Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner do formulário adaptável para personalizar o cabeçalho do modelo. Arraste e solte o componente Rodapé do formulário adaptável no contêiner de layout abaixo do Contêiner de formulário adaptável para personalizar o rodapé do modelo.

![Contêiner de layout na camada de estrutura](assets/header-layer-selector.png)

Contêineres de layout na camada de estrutura

**A.** Contêiner de layout para o componente Cabeçalho **B.** Contêiner de layout para o componente Rodapé

Arraste e solte o componente Cabeçalho do formulário adaptável no contêiner de layout acima do Contêiner do formulário adaptável. Após adicionar o componente, é possível especificar suas propriedades que permitem adicionar um logotipo e fornecer seu título.

Da mesma forma, ao arrastar e soltar o componente de rodapé no contêiner de layout abaixo do Contêiner de formulário adaptável, é possível fornecer as informações de direitos autorais e os detalhes da empresa.

![Cabeçalho e rodapé adicionados na camada Estrutura](assets/header-and-footer.png)

Cabeçalho e rodapé adicionados na camada Estrutura

#### Bloquear/desbloquear componentes na camada de estrutura {#locking-unlocking-components-in-the-structure-layer}

Ao editar o modelo com a camada de estrutura selecionada, é possível desbloquear o cabeçalho e o rodapé do modelo. Se um componente estiver desbloqueado no modelo, os autores de formulário poderão editar o componente no formulário adaptável que usa o modelo. Bloquear um componente impede que os autores de formulários o editem no formulário adaptável. A opção Bloquear está disponível na barra de ferramentas do componente.

Por exemplo, você adiciona o componente de cabeçalho no modelo. Ao selecionar o componente, você pode ver uma opção de bloqueio na barra de ferramentas do componente. Normalmente, o cabeçalho inclui o nome e o logotipo da empresa e você não deseja que os autores de formulários alterem o logotipo e o cabeçalho em um modelo. Em um formulário adaptável criado usando o modelo com o componente de cabeçalho bloqueado, os autores de formulário não podem alterar o logotipo e o nome da empresa.

>[!NOTE]
>
>Bloquear ou desbloquear imagem ou logotipo no componente de cabeçalho, individualmente, não é recomendado. Você pode desbloquear o componente de cabeçalho.

### Conteúdo inicial {#initial-content}

Quando a opção Conteúdo inicial é selecionada, o Contêiner de formulário adaptável do modelo é aberto como um formulário adaptável para edição. Assim como a criação de um formulário adaptável, você pode especificar as configurações iniciais, como selecionar um tema e enviar ações.

Os autores de formulários o usam como base para criar um formulário. A estrutura do fluxo de conteúdo é especificada na camada Conteúdo inicial do modelo. Para alternar para a edição do conteúdo inicial do modelo de formulário, antes de Visualizar na barra de ferramentas da página, toque em ![lista suspensa de tela](assets/canvas-drop-down.png) **> Conteúdo inicial**.
![Camada Conteúdo inicial no Editor de modelos](assets/initial-content-layer.png)

Camada Conteúdo inicial no Editor de modelo mostrando o Contêiner de formulário adaptável selecionado para especificar propriedades.

![conteúdo inicial](assets/initial-content-layer-1.png)

Na camada Conteúdo inicial , é possível criar o modelo de formulário adaptável usado pelos autores como base. A criação de um modelo é semelhante à criação de um formulário. Você usa as opções disponíveis na Barra lateral. A barra lateral fornece navegadores de conteúdo, propriedades, ativos e componentes.

Consulte [Barra lateral](../../forms/using/introduction-forms-authoring.md#sidebar).

>[!NOTE]
>
>Ao selecionar Armazenar conteúdo ou Armazenar PDF como a Ação de envio, você obtém uma opção para especificar o Caminho de armazenamento. Se você especificar o caminho no modelo, todos os formulários criados a partir dele terão o mesmo caminho. Você pode especificar o caminho de armazenamento correto ou garantir que os autores de formulários o atualizem para impedir que os dados de cada formulário sejam armazenados no mesmo local.

#### Criação de um modelo de formulário adaptável com guias e painéis  {#creating-an-adaptive-form-template-with-tabs-and-panels-nbsp}

Por exemplo, você deseja criar um modelo com as seguintes guias:

* Informações gerais
* Informações profissionais

Você adicionou um logotipo, forneceu um título e adicionou um rodapé na camada da estrutura. Bloqueie o cabeçalho e o rodapé para impedir que os autores de formulários os editem quando usam o modelo para criar formulários.

Altere a camada de Estrutura para Conteúdo inicial e comece a adicionar conteúdo ao formulário. Para criar uma estrutura com guias, adicione um Painel filho no guia Painel raiz do contêiner de Formulário adaptável. Para adicionar um painel:

* Você pode adicionar um painel tocando no botão **+** ao selecionar o botão **Arraste componentes aqui** opção.

* Você pode arrastar e soltar o componente do painel do navegador de componentes na barra lateral.
* Você pode adicionar o painel filho da `guideRootPanel` na barra de ferramentas do componente.

Para criar as guias Informações gerais e Informações profissionais , adicione dois painéis no painel filho da `guideRootPanel`. Selecione os painéis e toque em ![cmppr](assets/cmppr.png) para abrir as propriedades na barra lateral. Altere os nomes dos elementos como `general-info` e `professional-info`e títulos como Informações gerais e Informações profissionais, respectivamente. Na barra lateral, toque em conteúdo para abrir o navegador de conteúdo. Na guia Objetos de formulário , selecione `guideRootPanel`. No editor, o guideRootPanel é selecionado. Toque ![cmppr](assets/cmppr.png) na barra de ferramentas do componente para abrir suas propriedades. No campo Layout do painel , selecione **Guias em cima** e tocar **Concluído**. A estrutura do modelo com guias é aplicada.

#### Adição de conteúdo em guias {#adding-content-in-tabs}

![Adição de campos no modelo de formulário adaptável](assets/template-edit-initial-content.png)

Depois de adicionar painéis e estruturá-los como guias, é possível adicionar campos dentro das guias. Ao selecionar uma guia no editor, é possível ver a variável **Arraste componentes aqui** opção. Você pode arrastar e soltar componentes como caixas de texto, itens de lista e botões. Você pode arrastar e soltar componentes do navegador de componentes na barra lateral.

Cada componente tem propriedades que aprimoram a captura e a manipulação de dados. Por exemplo, é possível ativar a variável **Campo obrigatório** de um componente. Seus autores podem especificar uma mensagem que seus clientes veem ao ignorar o preenchimento de um campo obrigatório. Especifique a mensagem em **Mensagem de campo necessária** propriedade.

No modelo de exemplo, os campos Nome, Número de telefone e Data de nascimento são adicionados na guia Informações gerais . Na guia Informações profissionais , são adicionados o tipo de emprego atualmente empregado, os campos de qualificação educacional .

Depois de adicionar campos, é possível adicionar botões, como Enviar e Redefinir.

### Ativação do template {#enabling-the-template}

Ao criar um modelo, ele é adicionado como rascunho. Ative o modelo para usá-lo na criação de formulários adaptáveis. Para ativar um template:

1. Navegar para **Adobe Experience Manager > Ferramentas > Modelos** e abra a pasta na qual você criou o template.

1. O modelo criado é marcado como Rascunho.
1. Selecione o modelo e toque em **Habilitar** na barra de ferramentas.
Ao criar um formulário adaptável, você pode ver o modelo listado quando for solicitado a escolher um modelo.

## Importação ou exportação de um template {#importing-or-exporting-a-template}

Um formulário funciona com seu modelo. Quando você baixa um formulário adaptável criado usando um modelo personalizado, o modelo não é baixado. Ao importar o formulário em uma instância diferente do AEM Forms, ele é importado sem o modelo. Se um formulário for importado, mas seu modelo não estiver disponível, o formulário não será renderizado. Você pode empacotar o modelo personalizado de `/conf` nó no `https://<server>:<port>/crx/packmgr`e a porta na instância do AEM Forms onde deseja fazer upload do formulário.

## Criação de um formulário adaptável usando o modelo {#creating-an-adaptive-form-using-the-template}

Depois de criar e ativar um modelo, ele fica disponível no Gerenciador de formulários quando você cria um formulário adaptável. Para usar um modelo e criar um formulário adaptável, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).

## Alterar a opção de exibição dos modelos predefinidos  {#change-display-option-of-out-of-the-box-templates}

Você pode criar modelos personalizados para formulários adaptáveis para definir a estrutura básica e o conteúdo inicial. O AEM Forms também fornece um conjunto de modelos prontos para uso para formulários adaptáveis. Você pode optar por mostrar ou ocultar os modelos.

Execute as seguintes etapas para mostrar e ocultar modelos:

1. Faça logon na instância do autor do AEM Forms e navegue até **Ferramentas** > **Operações** > **Console da Web**.

   >[!NOTE]
   >
   >O URL AEM console da Web é https://&#39;[server]:[porta]&#39;/system/console/configMgr

1. Localize e abra o **Configuração do FormsManager** configurações:

   * Para mostrar ou ocultar modelos de formulários adaptáveis prontos para uso, marque ou desmarque a opção **Incluir modelos AF e AD prontos para uso** opção.
   * Para mostrar ou ocultar modelos de formulário adaptáveis prontos para uso que foram adicionados nas versões AEM 6.0 Forms ou AEM 6.1 Forms, mas agora estão obsoletas, marque ou desmarque a opção **Incluir modelos AEM 6.0 AF** opção. Se essa opção estiver marcada, para entrar em vigor, ela exigirá que a variável **Incluir modelos AF e AD prontos para uso** configuração a ser ativada.

1. Clique em **Salvar**. As opções de exibição para os templates prontos para uso são alteradas.

## Recomendações {#recommendations}

* Ao modificar as propriedades do formulário no editor de modelo, não use a propriedade BindReference.
* Se quiser adicionar um ponto de interrupção, crie-o ao criar um modelo de formulário adaptável.
Para obter mais informações sobre pontos de interrupção, consulte [Layout responsivo](/help/sites-authoring/responsive-layout.md).
