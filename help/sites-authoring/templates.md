---
title: 'Criação de modelos de páginas  '
seo-title: 'Criação de modelos de páginas  '
description: O modelo define a estrutura da página resultante e, com o editor de modelo, criar e manter modelos não é mais uma tarefa apenas do desenvolvedor
seo-description: O modelo define a estrutura da página resultante e, com o editor de modelo, criar e manter modelos não é mais uma tarefa apenas do desenvolvedor
uuid: e14cd298-289f-43f0-aacb-314ed5d56c12
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: b53348ca-fc50-4e7d-953d-b4c03a5025bb
docset: aem65
translation-type: tm+mt
source-git-commit: e3f1c932a5937e8a115e2849935b8f5ea5c2613d
workflow-type: tm+mt
source-wordcount: '4833'
ht-degree: 96%

---


# Criação de modelos de páginas  {#creating-page-templates}

Ao criar uma página, você deve selecionar um modelo, que será usado como a base de criação da nova página. O modelo define a estrutura da página resultante, qualquer conteúdo inicial e os componentes que podem ser usados.

Com o **Editor de modelos**, criar e manter modelos não é mais uma tarefa somente para desenvolvedores. Um tipo de usuário avançado, chamado de **autor de modelo**, também pode ser envolvido. Os desenvolvedores ainda são necessários para configurar o ambiente, criar bibliotecas de clientes e criar os componentes a serem usados, mas uma vez que essas noções básicas estejam em vigor, o **autor do modelo** terá a flexibilidade de criar e configurar modelos sem um projeto de desenvolvimento.

O **console Modelos** permite que os autores do modelo:

* Criem um novo modelo ou copiem um modelo existente.
* Gerenciem o ciclo de vida do modelo.

O **Editor de modelo** permite que os autores do modelo:

* Adicionem componentes ao modelo e os posicionem em uma grade responsiva.
* Pré-configurar os componentes.
* Definam quais componentes podem ser editados nas páginas criadas com o modelo.

Este documento explica como um **autor de modelo** pode usar o console e o editor de modelo para criar e gerenciar modelos editáveis.

Para obter informações detalhadas sobre como os modelos editáveis funcionam a um nível técnico, consulte o documento do desenvolvedor [Modelos de página - Editáveis](/help/sites-developing/page-templates-editable.md) para obter mais informações.

>[!NOTE]
>
>O **Editor de modelos** não oferece suporte para direcionamento diretamente no nível do modelo. As páginas criadas com base em um modelo editável podem ser direcionadas, mas os modelos em si não podem.

>[!CAUTION]
>
>As páginas e modelos criados com o **Console de Modelos** não devem ser usados com a interface clássica, e esse uso não é suportado.

## Antes de começar {#before-you-start}

>[!NOTE]
>
>Um administrador precisa configurar uma pasta de modelo no **Navegador de configurações** e aplicar permissões apropriadas antes que um autor de modelo possa criar um modelo nessa pasta.

É importante considerar os pontos a seguir antes de começar:

* Criar um novo modelo requer colaboração. Por esse motivo, a [Função](#roles) é indicada para cada tarefa.

* Dependendo de como sua instância for configurada, pode ser útil estar ciente de que o AEM agora oferece [dois tipos básicos de modelo](/help/sites-authoring/templates.md#editable-and-static-templates). Isso não afetará como você [usa um modelo para criar uma página](#using-a-template-to-create-a-page), mas afeta o tipo de modelo que você pode criar e como uma página se relaciona com o seu modelo.

### Funções {#roles}

A criação de um novo modelo usando o **Console de modelos** e o **Editor de modelos** exige a colaboração entre as seguintes funções:

* **Admin**:

   * Cria uma nova pasta de modelos requer direitos de `admin`.

   * Tais tarefas também podem ser realizadas por um desenvolvedor

* **Desenvolvedor**:

   * Concentra-se em detalhes técnicos/internos
   * Precisa de experiência com o ambiente de desenvolvimento.
   * Fornece ao autor do modelo as informações necessárias. 

* **Autor do modelo**:

   * Esse é um autor específico, membro do grupo `template-authors`

      * Isso atribui os privilégios e permissões necessários. 
   * Pode configurar o uso dos componentes e outros detalhes de alto nível, que requer:

      * Algum conhecimento técnico

         * Por exemplo, uso de padrões ao definir caminhos.
      * Informações técnicas do desenvolvedor.



Devido à natureza de algumas tarefas, como a criação de uma pasta, um ambiente de desenvolvimento é necessário, e isso requer conhecimento/experiência.

As tarefas detalhadas neste documento estão listadas com a função responsável por levá-las.

### Modelos editáveis e estáticos {#editable-and-static-templates}

O AEM agora oferece dois tipos básicos de modelos:

* [Modelos editáveis](/help/sites-authoring/templates.md#creatingandmanagingnewtemplates)

   * Podem ser [criados](#creatinganewtemplate) e [editados](#editingatemplate) pelos autores de modelo usando o console e o editor de **Modelo**. O console **Modelo** é acessível na seção **Geral** do console **Ferramentas**.

   * Depois que a nova página for criada, uma conexão dinâmica será mantida entre a página e o modelo. Isso significa que as alterações à estrutura e/ou ao conteúdo do modelo serão refletidas em todas as páginas criadas com esse modelo. As alterações ao conteúdo desbloqueado (isto é inicial) não serão refletidas.
   * Use as políticas de conteúdo, que você pode definir no editor do modelo, para continuar com as propriedades de design. O modo Design no editor de páginas não é mais usado para modelos editáveis.

* Modelos estáticos

   * Os modelos estáticos foram disponibilizados para várias versões do AEM.
   * Eles são [fornecidos por seus desenvolvedores](/help/sites-developing/page-templates-static.md) e, portanto, não podem ser criados ou editados por autores.
   * Eles são copiados para criar a nova página, mas nenhuma conexão dinâmica existe após essa ação (embora o nome do modelo seja registrado para a informações).
   * Use o [modo Design](/help/sites-authoring/default-components-designmode.md) para continuar com as propriedades de design.
   * Como a edição de modelos estáticos é a tarefa exclusiva de um desenvolvedor, consulte o documento do desenvolvedor [Modelos de página - Estático](/help/sites-developing/page-templates-static.md) para obter mais informações.

Por definição, o console de modelo e o editor de modelo permitem apenas a criação e edição de modelos editáveis. Portanto, este documento foca exclusivamente nos modelos editáveis.

### Usar um modelo para criar uma página  {#using-a-template-to-create-a-page}

Ao usar um modelo para [criar uma nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page), não há diferenças visíveis e nenhuma indicação entre os modelos estáticos e editáveis. Para o autor da página, o processo é transparente.

## Criação e gerenciamento de modelos {#creating-and-managing-templates}

Ao criar um novo modelo editável:

* Use o console **Modelo**. Disponível na seção **Geral** do console **Ferramentas**.

   * Ou diretamente em: [https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf](https://localhost:4502/libs/wcm/core/content/sites/templates.html/conf)

* É possível [criar uma pasta para os modelos](#creating-a-template-folder-admin) se necessário
* [Criar um novo modelo](#creatinganewtemplateauthor), inicialmente vazio   [](#templatedefinitions)

* [Definir propriedades adicionais](#definingtemplatepropertiesauthor) para o modelo, se necessário
* [Editar o modelo](#editingtemplates) para definir:

   * [Estrutura](#editingatemplatestructureauthor) - conteúdo predefinido que não pode ser alterado nas páginas criadas com o modelo.
   * [Conteúdo inicial](#editing-a-template-initial-content-author) - conteúdo predefinido que pode ser alterado nas páginas criadas com o modelo.
   * [Layout](#editingatemplatelayoutauthor) - para um intervalo de dispositivos.
   * [Estilos](/help/sites-authoring/style-system.md) - defina os estilos a serem usados com o modelo e seus componentes.

* [Ativar modelo](#enablingatemplateauthor) para uso ao criar uma página
* [Ativar modelo](#allowing-a-template-author) para a página ou a ramificação obrigatória do seu site
* [Publicar o modelo](#publishingatemplateauthor) para torná-lo disponível no ambiente de publicação

>[!NOTE]
>
>Os **Modelos permitidos** geralmente são predefinidos quando seu site for inicialmente configurado.

>[!CAUTION]
>
>Nunca insira qualquer informação que precise ser [internacionalizada](/help/sites-developing/i18n.md) em um modelo.

### Criação de uma pasta de modelo - Administrador {#creating-a-template-folder-admin}

Uma pasta de modelo deve ser criada para que o projeto mantenha seus modelos específicos de projetos. Trata-se de uma tarefa de administrador e está descrita no documento [Modelos de página - Editáveis](/help/sites-developing/page-templates-editable.md#template-folders).

### Criação de um novo modelo - Autor do modelo {#creating-a-new-template-template-author}

1. Abra o **console Modelos** (em **Ferramentas ->** **Geral**) para navegar até a pasta necessária.

   >[!NOTE]
   >
   >Em uma instância padrão do AEM, a pasta **global** já existe no console modelo. Isso mantém modelos padrão e atua como um fallback se nenhuma política e/ou tipo de modelo for localizado na pasta atual.
   >
   >
   >É uma prática recomendada usar uma [pasta de modelo criada para o seu projeto](/help/sites-developing/page-templates-editable.md#template-folders).

1. Selecione **Criar**, em seguida **Criar modelo** para abrir o assistente.

1. Escolha um **Tipo de modelo**, em seguida selecione **Avançar**.

   >[!NOTE]
   >
   >Os tipos de modelo são layouts predefinidos e podem ser considerados modelos de um modelo. Eles são predefinidos pelos desenvolvedores ou pelo administrador do sistema. Encontre mais informações podem ser encontradas no documento do desenvolvedor [Modelos de página - Editáveis](/help/sites-developing/page-templates-editable.md#template-type).

1. Preencha os **detalhes do modelo**:

   * **Nome do modelo**
   * **Descrição**

1. Selecione **Criar**. Uma confirmação será exibida, selecione **Abrir**[](#editingatemplate) para começar a editar o modelo ou **Concluído** para retornar ao console do modelo.

   >[!NOTE]
   >
   >Quando um modelo novo for criado, ele será marcado como **Rascunho** no console. Isso indica que ainda não está disponível para uso por autores da página.

### Definir propriedades do modelo - Autor do modelo    {#defining-template-properties-template-author}

Um modelo pode ter as seguintes propriedades:

* Imagem

   * A imagem a ser usada como uma [miniatura do modelo](/help/sites-authoring/templates.md#template-thumbnail-image) para auxiliar na seleção, como o assistente Criar página.

      * Pode ser enviado por upload
      * Pode ser gerado com base no conteúdo do modelo

* Título

   * Um título usado para identificar o modelo, como no assistente **Criar página**.

* Descrição

   * Uma descrição opcional para fornecer mais informações sobre o modelo e seu uso, que pode ser visualizada, por exemplo, no assistente **Criar página**.

Para exibir e/ou editar as propriedades:

1. No **console Modelos**, selecione o modelo.
1. Selecione **Propriedades da exibição** na barra de ferramentas ou nas opções rápidas para abrir a caixa de diálogo.
1. Agora você pode exibir ou editar as propriedades do modelo.

>[!NOTE]
>
>O status de um modelo (rascunho, ativado ou desativado) é exibido no console.

#### Imagem em miniatura do modelo {#template-thumbnail-image}

Para definir a miniatura do modelo:

1. Edite as propriedades do modelo.
1. Escolha se deseja fazer upload de uma miniatura ou gerá-la a partir do conteúdo do modelo.

   * Se desejar fazer upload de uma miniatura, clique ou toque em **Fazer upload da imagem**
   * Se desejar fazer o upload de uma miniatura, clique ou toque em **Gerar visualização**

1. Para ambos os métodos será exibida uma visualização de miniatura.

   Se não for satisfatório, clique ou toque em **Limpar** para fazer o upload de outra imagem ou para gerar a miniatura novamente.

1. Quando estiver satisfeito com a miniatura, clique ou toque em **Salvar e fechar**.

### Ativar e permitir um modelo - Autor do modelo    {#enabling-and-allowing-a-template-template-author}

Para poder usar um modelo ao criar uma página é necessário:

* [Ativar o modelo](#enablingatemplate) para disponibilizá-lo para o uso na criação de páginas.
* [Permitir o modelo](#allowingatemplate) para especificar as ramificações de conteúdo nas quais o modelo pode ser usado.

#### Habilitar um modelo - Autor do modelo {#enabling-a-template-template-author}

Um modelo pode ser habilitado ou desabilitado para torná-lo disponível ou indisponível no assistente **Criar página**.

>[!CAUTION]
>
>Uma vez que um modelo estiver habilitado um aviso será exibido quando um autor de modelo começar a atualizar o modelo. Este aviso tem o objetivo de informar o usuário de que o modelo pode ser referenciado, de modo que todas as alterações podem afetar as páginas que fazem referência a ele.

1. No **console Modelos**, selecione o modelo.
1. Selecione **Habilitar** ou **Desabilitar** da barra de ferramentas e depois na caixa de diálogo de confirmação.
1. Agora é possível usar o modelo ao [criar uma nova página](/help/sites-authoring/managing-pages.md#creating-a-new-page), embora você provavelmente queira [editar o modelo](#editingatemplate) de acordo com seus requisitos.

>[!NOTE]
>
>O status de um modelo (rascunho, ativado ou desativado) é exibido no console.

#### Ativar um modelo - Autor {#allowing-a-template-author}

Um modelo pode ser disponibilizado ou indisponibilizado para determinadas ramificações de página.

1. Abra as [Propriedades da página](/help/sites-authoring/editing-page-properties.md) da página raiz da ramificação onde deseja que o modelo fique disponível.

1. Abra a guia **Avançado**.

1. Em **Configurações do modelo** use **Adicionar campo** para especificar os caminhos aos seus modelos.

   O caminho pode ser explícito ou usar padrões. Por exemplo:

   `/conf/<your-folder>/settings/wcm/templates/.*`

   A ordem dos caminhos é irrelevante, todos os caminhos serão digitalizados e os modelos recuperados.

   >[!NOTE]
   >
   >Se a lista **Modelos permitidos** de for deixada em branco, a árvore será crescente até que um valor/lista seja encontrado.
   >
   >
   >Consulte [Disponibilidade do modelo](/help/sites-developing/templates.md#template-availability) - os princípios para os modelos permitidos permanecem os mesmos.

1. Clique em **Salvar** para salvar as alterações nas propriedades da página.

>[!NOTE]
>
>Geralmente os modelos permitidos são predefinidos para todo o site quando configurado.

### Publicar um modelo - Autor do modelo {#publishing-a-template-template-author}

À medida que o modelo for referenciado quando a página for renderizada, o modelo totalmente configurado precisará ser publicado, para estar disponível no ambiente de publicação.

1. No **console Modelos**, selecione o modelo.
1. Selecione **Publicar** na barra de ferramentas para abrir o assistente.
1. Selecione as **Políticas do conteúdo** para ser publicado em tandem.

1. Selecione **Publicar** na barra de ferramentas para concluir a ação.

## Editar modelos - Autores do modelo    {#editing-templates-template-authors}

Ao criar ou editar um modelo há vários aspectos que podem ser definidos. A edição modelos é semelhante à criação de página.

Os seguintes aspectos de um modelo podem ser editados:

* [Estrutura](#editingatemplatestructure)

   Os componentes adicionados aqui não podem ser movidos/removido das páginas resultantes pelos autores da página. Se desejar que os autores da página possam adicionar e remover os componentes para páginas resultantes, é necessário adicionar um sistema de parágrafos ao modelo.

   Quando os componentes estiverem bloqueados, você pode adicionar conteúdo, o qual não poderá ser editado pelos autores da página. É possível desbloquear componentes para permitir que você defina o [conteúdo inicial](#editingatemplateinitialcontent).

   >[!NOTE]
   >
   >No modo de estrutura, nenhum componente pai de um componente desbloqueado pode ser movido, recortado ou ser excluído.

* [Conteúdo inicial](#editingatemplateinitialcontent)

   Quando um componente tiver sido desbloqueado, é possível definir o conteúdo inicial que será copiado para páginas resultantes, criado a partir do modelo. Esses componentes desbloqueados podem ser editados nas páginas resultantes.

   >[!NOTE]
   >
   >No modo de **conteúdo inicial**, bem como nas páginas resultantes, todos os componentes desbloqueados que tenham um pai acessível (isto é, componentes dentro de um contêiner de layout) podem ser excluídos.

* [Layout](#editingatemplatelayout)

   Aqui é possível predefinir o layout do modelo para os formatos de dispositivo necessários. O modo **Layout** de criação do modelo tem a mesma funcionalidade que o modo [**Layout** da criação de página](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode).

* [Políticas da página](#editingatemplatepagepolicies)

   Nas políticas de página, é possível conectar políticas de página predefinidas à página. Essas políticas da página definem as várias configurações de design.

* [Estilos](/help/sites-authoring/style-system.md)

   O sistema de estilos permite ao autor do modelo definir classes de estilo na política de conteúdo de um componente para que autores de conteúdo possam selecioná-las ao editarem o componente em uma página. Esses estilos podem ser variações visuais alternativas de um componente, tornando-o mais flexível.

   Consulte a [documentação do Style System](/help/sites-authoring/style-system.md) para obter mais informações.

O seletor de **Modo** na barra de ferramentas permite selecionar e editar o aspecto apropriado do modelo:

* [Estrutura](#editingatemplatestructure)
* [Conteúdo inicial](#editingatemplateinitialcontent)
* [Layout](#editingatemplatelayout)

![chlimage_1-135](assets/chlimage_1-133.png)

Já a opção **Política de página** no menu **Informações de página** permite [selecionar as políticas de página necessárias](#editingatemplatepagepolicies):

![screen_shot_2018-03-23at120604](assets/screen_shot_2018-03-23at120604.png)

>[!CAUTION]
>
>Se um autor começar a editar um modelo que já foi habilitado, ativado um aviso será exibido. Este aviso tem o objetivo de informar o usuário de que o modelo pode ser referenciado, de modo que todas as alterações podem afetar as páginas que fazem referência a ele.

### Editar um modelo - Estrutura - Autor do modelo {#editing-a-template-structure-template-author}

No modo **Estrutura** você define os componentes e o conteúdo para o modelo, a política do modelo e seus componentes.

* Os componentes definidos na estrutura do modelo não podem ser movidos em uma página resultante ou excluídos de qualquer página resultante.
* Se desejar que os autores da página possam adicionar e remover componentes, adicione um sistema de parágrafo ao modelo.
* Os componentes podem ser desbloqueados e bloqueados novamente para permitir que você defina o [conteúdo inicial](#editingatemplateinitialcontent).

* As políticas de design dos componentes e página são definidas.

![screen_shot_2018-03-23at120819](assets/screen_shot_2018-03-23at120819.png)

No modo **Estrutura** do editor de modelo:

* **Adicione componentes**

   Há vários mecanismos para adicionar componentes ao modelo:

   * No navegador **Componentes** no painel lateral.
   * Ao usar a opção **Inserir componente** (ícone **+**), disponível na barra de ferramentas dos componentes já no modelo ou na caixa **Arrastar componentes até aqui**.

   * Ao arrastar um ativo (no navegador de **Ativos** no painel lateral) diretamente no modelo para gerar o componente adequado no local.

   Uma vez adicionado, cada componente é marcado com:

   * Uma borda
   * Um marcador para mostrar o tipo de componente
   * Um marcador para mostrar quando o componente for desbloqueado

   >[!NOTE]
   >
   >Ao adicionar um componente de **Título** pronto ao modelo, ele conterá **estrutura** de texto padrão.
   >
   >
   >Se alterar e adicionar seu próprio texto, esse texto atualizado será usado quando uma página for criada a partir do modelo.
   >
   >
   >Se deixar o texto padrão (estrutura) como está, o título será padrão para o nome da página subsequente.

   >[!NOTE]
   >
   >Embora não seja idêntico, adicionar componentes e ativos a um modelo tem muitas coisa em comum com as ações semelhantes ao [criar a página](/help/sites-authoring/editing-content.md).

* **Ações do componente**

   Execute ações nos componentes em uma vez que tiverem sido adicionadas ao modelo. Cada instância individual tem uma barra de ferramentas que permite acessar as ações disponíveis. A barra de ferramentas depende do tipo de componente.

   ![screen_shot_2018-03-23at120909](assets/screen_shot_2018-03-23at120909.png)

   Além disso, ela pode ser dependente das ações executadas como quando uma política foi associada ao componente, o ícone de configuração de design é disponibilizado.

* **Editar e configurar**

   Com essas duas ações você pode adicionar conteúdo aos seus componentes.

* **Borda para indicar estrutura**

   Ao trabalhar no modo **estrutura**, uma borda laranja indica que o componente selecionado no momento. Uma linha pontilhada também indica o componente pai.

   Por exemplo, no instantâneo abaixo do componente **Texto** é selecionado, dentro de um **contêiner de layout** (responsivegrid).

   ![chlimage_1-134](assets/chlimage_1-134.png)

* **Política e propriedades (geral)**

   As políticas do conteúdo (ou design) definem as propriedades do design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Crie uma política de conteúdo ou selecione uma existente para um componente. Isso permite que definir os detalhes do design.

   ![chlimage_1-135](assets/chlimage_1-135.png) ![chlimage_1-136](assets/chlimage_1-136.png)

   A janela de configuração é dividida em dois.

   * Do lado esquerdo da caixa de diálogo, em **Política**, você tem a capacidade de selecionar uma política existente.
   * Do lado direito da caixa de diálogo, em **Propriedades**, você pode definir as propriedades específicas ao tipo de componente.

   As propriedades disponíveis dependem do componente selecionado. Por exemplo, para um componente de texto, as propriedades definem as opções de copiar e colar, de formatação e o estilo de parágrafo, entre outras.

   ***Política***

   As políticas do conteúdo (ou design) definem as propriedades do design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Em **Política** é possível selecionar uma política existente para aplicar ao componente por meio da lista suspensa.

   ![chlimage_1-137](assets/chlimage_1-137.png)

   Uma nova política pode ser adicionada ao selecionar o botão adicionar ao lado da lista suspensa **Selecionar política**. Um novo título deve ser especificado no campo **Título da política**.

   ![chlimage_1-138](assets/chlimage_1-138.png)

   A política existente selecionada na lista suspensa **Selecionar política** pode ser copiada como uma nova política usando o botão copiar ao lado do menu suspenso. Um novo título deve ser especificado no campo **Título da política**. Por padrão, a política copiada será denominada **Cópia de X**, onde X é o título da política copiada.

   ![chlimage_1-139](assets/chlimage_1-139.png)

   É opcional uma descrição da política no campo **Descrição da política**.

   Na seção **Outros modelos que também utilizam a política selecionada**, você pode ver qual modelo utiliza a política selecionada na lista suspensa **Selecionar política**.

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >Se vários componentes do mesmo tipo forem adicionados como conteúdo inicial, a mesma política se aplica a todos os componentes. Isso reflete a mesma restrição no [**Modo Design** dos modelos estáticos](/help/sites-authoring/default-components-designmode.md).

   ***Propriedades***

   No cabeçalho **Propriedades** você pode definir as configurações do componente. O cabeçalho tem duas guias:

   * Principal
   * Recursos

   *Principal*

   Na guia **Principal**, são definidas as configurações mais importantes do componente.

   Por exemplo, para um componente de imagem, as larguras permitidas podem ser definidas junto com a ativação do carregamento lento.

   Se uma configuração permitir várias configurações, clique ou toque no botão **Adicionar** para adicionar outra configuração.

   ![chlimage_1-141](assets/chlimage_1-141.png)

   Para remover uma configuração, clique ou toque no botão **Excluir** localizado à direita da configuração.

   Para remover uma configuração, clique ou toque no botão** Excluir**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

   *Recursos*

   A guia **Recursos** permite habilitar ou desabilitar recursos adicionais do componente.

   Por exemplo, para um componente de imagem, é possível definir as proporções de corte, orientações de imagem permitidas e se os uploads estão permitidos.

   ![chlimage_1-143](assets/chlimage_1-143.png)

   >[!CAUTION]
   >
   >Observe que no AEM, as proporções de corte estão definidas como **altura/largura**. Isso difere da definição convencional de largura/altura e é feita por motivos de compatibilidade legal. Os usuários da criação de página não estarão cientes de qualquer diferença desde que você defina o **Nome** claramente, uma vez que este é exibido na interface do usuário.

   >[!NOTE]
   >
   >[](/help/sites-administering/rich-text-editor.md#main-pars-header-206036638)As políticas de conteúdo para componentes que implementam o editor de rich text só podem ser definidas para opções disponibilizadas pelo RTE pelas configurações da interface do usuário. [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638) [](/help/sites-administering/rich-text-editor.md#main-pars_header_206036638)

* **Política e propriedades (contêiner de layout)**

   As configurações de política e propriedades de um contêiner de layout são semelhantes ao uso geral, mas com algumas diferenças.

   >[!NOTE]
   >
   >Configurar uma política é obrigatório para componentes do contêiner porque isso permite definir os componentes que estarão disponíveis no contêiner.

   A janela de configuração é dividida em dois, como na janela de uso geral.

   ***Política***

   As políticas do conteúdo (ou design) definem as propriedades do design de um componente. Por exemplo, os componentes disponíveis ou as dimensões mínimas/máximas. Eles são aplicáveis ao modelo (e às páginas criadas com o modelo).

   Em **Política** é possível selecionar uma política existente para aplicar ao componente por meio da lista suspensa. Isso funciona exatamente da mesma forma que a janela de uso geral.

   ***Propriedades***

   No cabeçalho **Propriedades** você pode escolher quais componentes estarão disponíveis para o contêiner de layout e definir suas configurações. O cabeçalho tem três guias:

   * Componentes permitidos
   * Componentes padrão
   * Configurações receptivas

   *Componentes permitidos*

   Na guia **Componentes permitidos**, você define quais componentes estão disponíveis para o contêiner de layout.

   * Os componentes são agrupados por seus grupos de componentes, que podem ser expandidos e recolhidos.
   * Para selecionar um grupo inteiro, marque o nome do grupo. Para cancelar a seleção, desmarque.
   * Um sinal de menos indica que pelo menos um, mas não todos os itens em um grupo foram selecionados.
   * Uma pesquisa está disponível para filtrar um componente pelo nome.
   * As pontuações listadas à direita do nome do grupo de componentes representa o número total de componentes selecionados nesses grupos independentemente do filtro.

   ![chlimage_1-144](assets/chlimage_1-144.png)

   *Componentes padrão*

   Na guia **Componentes padrão**, você define quais componentes são associados automaticamente a determinados tipos de mídia, de modo que, quando um autor arrastar um ativo do navegador do ativo, o AEM saiba com que componente associá-lo. Observe que apenas os componentes com zonas para soltar estão disponíveis para essa configuração.

   Clique ou toque em **Adicionar mapeamento** para adicionar um componente totalmente novo e o tipo de mapeamento MIME.

   Selecione um componente na lista e clique ou toque em **Adicionar tipo** para adicionar outro tipo MIME a um componente já mapeado. Clique no ícone **Excluir** para remover a um tipo MIME.

   ![chlimage_1-145](assets/chlimage_1-145.png)

   *Configurações receptivas*

   Na guia **Configurações responsivas**, é possível configurar o número de colunas na grade resultante do contêiner de layout.

* **Desbloquear/bloquear componentes**

   Você bloqueia/desbloqueia componentes para definir se o conteúdo estará disponível para a modificação no modo **Conteúdo inicial**.

   Quando um componente é desbloqueado:

   * Um indicador de cadeado aberto é exibido na borda.
   * A barra de ferramentas do componente será ajustada adequadamente.
   * Todo o conteúdo já inserido não será mais mostrado no modo **estrutura**.

      * O conteúdo já inserido é considerado conteúdo inicial e é visível apenas no modo **Conteúdo inicial**.
   * Os pais do componente desbloqueado não podem ser movidos, recortados ou excluídos.

   ![chlimage_1-146](assets/chlimage_1-146.png)

   Isso inclui desbloquear componentes de contêiner para que outros componentes possam ser adicionados, no modo **Conteúdo inicial** ou nas páginas resultantes. Se você já tiver adicionado componentes/conteúdo ao contêiner antes de desbloqueá-lo, eles não serão mais exibidos quando estiverem no modo **Estrutura**, mas serão exibidos no modo **Conteúdo inicial**. No **modo Estrutura**, apenas o componente do contêiner será mostrado com sua lista de **Componentes permitidos**.

   ![chlimage_1-147](assets/chlimage_1-147.png)

   Para economizar espaço, o contêiner de layout não é expandido para acomodar a lista de componentes permitidos. Em vez disso, o contêiner se torna uma lista rolável.

   Os componentes configuráveis são mostrados com um ícone de **Política**, que pode ser tocado ou clicado para editar a política e as propriedades desse componente.

   ![chlimage_1-148](assets/chlimage_1-148.png)

* **Relação com páginas existentes**

   Se a estrutura for atualizada depois de criar as páginas baseadas no modelo, então essas páginas refletirão as alterações no modelo. Um aviso é exibido na barra de ferramentas para lembrá-lo desse fato, junto com caixas de diálogo de confirmação.

   ![chlimage_1-149](assets/chlimage_1-149.png)

### Editar um modelo - Conteúdo inicial - Criação {#editing-a-template-initial-content-author}

O modo **Conteúdo inicial** é usado para o conteúdo definido que aparecerá quando uma página for inicialmente criada com base no modelo. O conteúdo inicial pode ser editado por autores da página.

Embora todo o conteúdo criado no modo **Estrutura** seja visível no **Conteúdo inicial**, somente os componentes que foram desbloqueados podem ser selecionados e editados.

>[!NOTE]
>
>O modo **Conteúdo inicial** pode ser visto como um modo de edição para páginas criadas com esse modelo. Sendo assim, as políticas não estão definidas no modo **Conteúdo inicial**, mas no modo [**Estrutura**](/help/sites-authoring/templates.md#editing-a-template-structure-template-author).

* Os componentes desbloqueados disponíveis para edição são marcados. Quando selecionados, apresentam uma borda azul:

   ![chlimage_1-150](assets/chlimage_1-150.png)

* Os componentes desbloqueados têm uma barra de ferramentas, permitindo editar e configurar o conteúdo:

   ![chlimage_1-151](assets/chlimage_1-151.png)

* Se um componente do contêiner foi desbloqueado (no modo **estrutura**), você pode adicionar novos componentes ao contêiner (no modo **Conteúdo inicial**). Os componentes adicionados no modo **Conteúdo inicial** podem ser movidos para ou excluído das páginas resultantes.

   Você pode adicionar o componente utilizando a área **Arraste componentes até aqui** ou a opção **Inserir novo componente** na barra de ferramentas do contêiner apropriado.

   ![chlimage_1-152](assets/chlimage_1-152.png) ![chlimage_1-153](assets/chlimage_1-153.png)

* Se o conteúdo inicial do modelo for atualizado depois que as páginas forem criadas com base no modelo, então essas páginas não serão afetadas por alterações no conteúdo inicial no modelo.

>[!NOTE]
>
>O conteúdo inicial destina-se a preparar componentes e o layout de página que servem como ponto de partida para a criação do conteúdo. Não se destina a ser o conteúdo real que permaneceria intacto. Por esse motivo, o conteúdo inicial não pode ser traduzido.
>
>Se você precisar incluir texto traduzível no modelo, como em cabeçalhos ou rodapés, poderá usar os recursos de [localização dos componentes principais](https://docs.adobe.com/content/help/br/experience-manager-core-components/using/get-started/localization.html).

### Editar um modelo - Layout - Autor do modelo {#editing-a-template-layout-template-author}

É possível definir o layout do modelo para um intervalo de dispositivos. O [Layout responsivo](/help/sites-authoring/responsive-layout.md) para modelos funciona como na criação de página.

>[!NOTE]
>
>As modificações no layout serão refletidas no modo **Conteúdo inicial**, mas nenhuma alteração será vista no modo **Estrutura**.

![chlimage_1-154](assets/chlimage_1-154.png)

### Editar um modelo - Design da página - Autor/desenvolvedor do modelo {#editing-a-template-page-design-template-author-developer}

O design da página, incluindo as bibliotecas do lado do cliente e as políticas de página necessárias, é mantido na opção **Design da página** do menu **Informações da página**.

Para acessar a caixa de diálogo **Design da página**:

1. No **Editor de modelos**, selecione **Informações da página** na barra de ferramentas e, em seguida, **Design da página** para abrir a caixa de diálogo.
1. A caixa de diálogo **Design da página** é aberta e dividida em duas seções:

   * A metade esquerda define as [políticas da página](/help/sites-authoring/templates.md#page-policies)
   * A metade direita define as [propriedades da página](/help/sites-authoring/templates.md#page-properties)

   ![chlimage_1-155](assets/chlimage_1-155.png)

#### Políticas da página {#page-policies}

É possível aplicar uma política de conteúdo ao modelo ou às páginas resultantes. Isso define a política de conteúdo do sistema de parágrafo principal na página.

![chlimage_1-156](assets/chlimage_1-156.png)

* É possível selecionar uma política existente para a página na lista suspensa **Selecionar política**.

   ![chlimage_1-157](assets/chlimage_1-157.png)

   Uma nova política pode ser adicionada ao selecionar o botão adicionar ao lado da lista suspensa **Selecionar política**. Um novo título deve ser especificado no campo **Título da política**.

   ![chlimage_1-158](assets/chlimage_1-158.png)

   A política existente selecionada na lista suspensa **Selecionar política** pode ser copiada como uma nova política usando o botão copiar ao lado do menu suspenso. Um novo título deve ser especificado no campo **Título da política**. Por padrão, a política copiada será denominada **Cópia de X**, onde X é o título da política copiada.

   ![chlimage_1-159](assets/chlimage_1-159.png)

* Defina um título para a política no campo **Título da política**. É necessário que a política tenha um título para que possa ser facilmente selecionada na lista suspensa **Selecionar política**.

   ![chlimage_1-160](assets/chlimage_1-160.png)

* É opcional uma descrição da política no campo **Descrição da política**.
* Na seção **Outros modelos que também utilizam a política selecionada**, você pode ver qual modelo utiliza a política selecionada na lista suspensa **Selecionar política**.

   ![chlimage_1-161](assets/chlimage_1-161.png)

#### Propriedades da página {#page-properties}

Usando as propriedades de página, é possível definir as bibliotecas do lado do cliente necessárias usando a caixa de diálogo **Design da página**. Essas bibliotecas do lado do cliente incluem folhas de estilo e o javascript a serem carregados com o modelo e as páginas criadas com esse modelo.

![chlimage_1-162](assets/chlimage_1-162.png)

* Especifique as bibliotecas do lado do cliente que deseja aplicar às páginas criadas com esse modelo. Digitando o nome de uma biblioteca no campo de texto da seção **Bibliotecas do lado do cliente**.

   ![chlimage_1-163](assets/chlimage_1-163.png)

* Se as várias bibliotecas forem necessárias, clique no botão Adicionar para adicionar um campo de texto extra para o nome da biblioteca.

   ![chlimage_1-164](assets/chlimage_1-164.png)

   Adicione quantos campos de texto forem necessário para suas bibliotecas do lado do cliente.

   ![chlimage_1-165](assets/chlimage_1-165.png)

* Defina a posição relativa das bibliotecas conforme necessário, ao arrastar os campos usando a alça de arrastar.

   ![chlimage_1-166](assets/chlimage_1-166.png)

>[!NOTE]
>
>Como o autor do modelo pode especificar a política de página no modelo, ele precisará obter detalhes das bibliotecas do lado do cliente apropriadas do desenvolvedor.

### Editar um modelo - Propriedades iniciais da página - Criação {#editing-a-template-initial-page-properties-author}

Usando a opção **Propriedades da página inicial**, é possível definir as [propriedades de página](/help/sites-authoring/editing-page-properties.md) iniciais a ser usadas ao criar páginas resultantes.

1. No editor de modelo, selecione **Informações da página** na barra de ferramentas, em seguida **Propriedades da página inicial** para abrir a caixa de diálogo.

1. Na caixa de diálogo, é possível definir as propriedades que deseja aplicar às páginas criadas com esse modelo.

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Confirme suas definições em **Concluído**.

## Práticas recomendadas    {#best-practices}

Ao criar modelos você deve considerar:

1. O impacto das modificações no modelo depois que as páginas foram criadas a partir desse modelo.

   Veja uma lista das diferentes operações possíveis nos modelos e como elas afetam as páginas criadas a partir delas:

   * Alterações na estrutura:

      * São aplicadas imediatamente às páginas resultantes.
      * É necessária a publicação do modelo alterado para que os visitantes vejam as alterações.
   * Alterações nas políticas de conteúdo e configurações de design:

      * São aplicadas imediatamente às páginas resultantes.
      * É necessária a publicação das alterações para que os visitantes vejam as alterações.
   * Alterações no conteúdo inicial:

      * Aplicam-se somente às páginas criadas após as alterações no modelo.
   * As alterações no layout dependem de se o componente modificado for parte:

      * Apenas da estrutura - aplicada instantaneamente
      * Contém conteúdo inicial - somente nas páginas criadas após a alteração

   Tome cuidado especial ao:

   * Bloquear ou desbloquear componentes em modelos permitidos.
   * Isso pode ter efeitos colaterais, uma vez que as páginas já existentes podem estar usando o modelo. Geralmente:

      * Desbloquear componentes (que foram bloqueados) ficará ausente nas páginas existentes.
      * Bloquear componentes (que eram editáveis) ocultará esse conteúdo nas páginas.

   >[!NOTE]
   >
   >O AEM dá avisos explícitos ao alterar o status de bloqueio de componentes nos modelos que não são mais rascunhos.

1. [Criar suas próprias pastas](#creatingatemplatefolderdeveloper) para os modelos específicos de site.
1. [Publicar os modelos](#publishingatemplateauthor) a partir do console **Modelos**.
