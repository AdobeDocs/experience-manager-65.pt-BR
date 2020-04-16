---
title: Fragmentos de formulário adaptáveis
seo-title: Fragmentos de formulário adaptáveis
description: Formulários adaptáveis fornecem um mecanismo para criar um segmento de formulário, como um painel ou um grupo de campos, como usá-lo em qualquer forma adaptável. Também é possível salvar um painel existente como fragmento.
seo-description: Formulários adaptáveis fornecem um mecanismo para criar um segmento de formulário, como um painel ou um grupo de campos, como usá-lo em qualquer forma adaptável. Também é possível salvar um painel existente como fragmento.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Adaptive form fragments{#adaptive-form-fragments}

Embora cada formulário seja projetado para uma finalidade específica, há alguns segmentos comuns na maioria das formas, como para fornecer detalhes pessoais, como nome e endereço, detalhes familiares, detalhes de renda e assim por diante. Os desenvolvedores de formulários precisam criar esses segmentos comuns sempre que um novo formulário for criado.

Formulários adaptáveis fornecem um mecanismo conveniente para criar segmentos de formulários, como um painel ou um grupo de campos, somente uma vez e reutilizá-los em formulários adaptáveis. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptáveis.

## Criar um fragmento {#create-a-fragment}

É possível criar um fragmento de formulário adaptável do zero ou salvar um painel em um formulário adaptável existente como fragmento.

### Criar fragmento do zero {#create-fragment-from-scratch}

1. Faça logon na instância do autor do AEM Forms em https://[*hostname*]:[*port*]/aem/forms.html.
1. Click **Create > Adaptive Form Fragment**.
1. Especifique o título, o nome, a descrição e as tags do fragmento.

   >[!NOTE]
   >
   >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

1. Clique para abrir a guia Modelo **de** formulário e, no menu suspenso **Selecionar** , selecione um dos seguintes modelos para o fragmento:

   * **Nenhum**: Especifica a criação do fragmento do zero sem usar qualquer modelo de formulário.
   * **Modelo** de formulário: Especifica a criação do fragmento usando um modelo XDP carregado no AEM Forms. Selecione o modelo XDP apropriado como o modelo de formulário para o fragmento.
   ![Criação de um formulário adaptável usando modelo de formulário como modelo](assets/form-template-model.png)

   Os subformulários marcados como fragmentos no modelo de formulário selecionado também são exibidos. É possível selecionar um subformulário para fragmento de formulário adaptável na lista suspensa.

   ![Selecionar subformulários do modelo de formulário especificado](assets/fragment-subform.png)

   Além disso, é possível criar um fragmento de formulário adaptável usando subformulários que não estão marcados como fragmentos no modelo de formulário especificando a expressão SOM para o subformulário na caixa suspensa.

   * **Schema** XML: Especifica a criação do fragmento usando um schema XML carregado no AEM Forms. É possível carregar ou selecionar entre os schemas XML disponíveis como o modelo de formulário para o fragmento.
   ![Criar um fragmento de formulário adaptável com base em um schema XML como modelo](assets/xml-schema-model.png)

   Também é possível criar um fragmento de formulário adaptável selecionando um complexType presente no schema selecionado na caixa suspensa.

   ![Selecione um tipo complexo do modelo de schema XML especificado](assets/complex-type.png)

1. Clique em **Criar** e em **Abrir** para abrir o fragmento, com um modelo padrão, no modo de edição.

No modo de edição, você pode arrastar e soltar qualquer componente de formulário adaptável do sidekick AEM no fragmento. Para obter informações sobre componentes de formulário adaptáveis, consulte [Introdução à criação de formulários](../../forms/using/introduction-forms-authoring.md)adaptáveis.

Além disso, se você selecionou um schema XML ou modelo de formulário XDP como o modelo de formulário para o fragmento, uma nova guia exibindo a hierarquia do modelo de formulário será exibida no localizador de conteúdo. Ela permite arrastar e soltar elementos de modelo de formulário no fragmento. Os elementos de modelo de formulário adicionados são convertidos em componentes de formulário enquanto mantêm as propriedades originais do XDP ou XSD associado.

### Salvar painel como um fragmento {#save-panel-as-a-fragment}

1. Abra um formulário adaptável que contenha o painel que deseja salvar como fragmento de formulário adaptável.
1. Na barra de ferramentas do painel, clique em **[!UICONTROL Salvar como fragmento]**. A caixa de diálogo Salvar como fragmento é aberta.

   >[!NOTE]
   >
   >Se o painel que você está salvando como fragmento contiver o painel filho, o fragmento resultante os incluirá.

1. Na caixa de diálogo Criação de fragmentos, especifique as seguintes informações:

   * **Nome**: Nome do fragmento. O valor padrão é o nome do elemento do painel. É um campo obrigatório.
      >[!NOTE]
      >
      >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

   * **Título**: Título do fragmento. O valor padrão é o título do painel.

   * **Descrição**: Descrição do fragmento.

   * **Tags**: Marca os metadados do fragmento.

   * **Caminho** do Público alvo: Caminho do repositório no qual o fragmento será salvo. Se um caminho não for especificado, um nó com o mesmo nome do fragmento será criado ao lado do nó que contém o formulário adaptável. O fragmento é salvo neste nó.

   * **Modelo** de formulário: Dependendo do modelo de formulário para o formulário adaptável, esse campo exibe o Schema **** XML, o Modelo **de** formulário ou **Nenhum**. É um campo não editável.

   * **Raiz** do modelo de fragmento: Aparece somente em formulários adaptativos baseados em XSD. Especifica a raiz do modelo de fragmento. Você pode escolher **/** ou o tipo complexo XSD no menu suspenso. Observe que é possível reutilizar o fragmento em outro formulário adaptável somente se você selecionar o tipo complexo como a raiz do modelo de fragmento.
Se você escolher **/** como a raiz do modelo de fragmento, a árvore XSD completa da raiz estará visível na guia do modelo de dados de formulário adaptável. Para uma raiz de modelo de fragmento de tipo complexo, somente os descendentes do tipo complexo selecionado ficam visíveis na guia de modelo de dados de formulário adaptável.

   * **Ref** XSD: Aparece somente em formulários adaptativos baseados em XSD. Ele exibe o local do schema XML.

   * **Ref** XDP: Aparece somente em formulários adaptativos baseados em XDP. Ele exibe o local do modelo de formulário XDP.
   ![save-fragment](assets/save-fragment.png)

   Caixa de diálogo Salvar como fragmento

1. Clique em **OK**.

   O painel é salvo no local especificado ou padrão no repositório. No formulário adaptável, o painel é substituído por um instantâneo do fragmento. Como mostrado abaixo, o painel Informações gerais e seus painéis filhos, Informações pessoais e Endereço, são salvos como um fragmento.

   Para editar o fragmento, clique em **[!UICONTROL Editar ativo]** na barra de ferramentas do painel. O fragmento é aberto em uma nova guia ou janela no modo de edição.

   ![Edição de fragmento](assets/edit-fragment.png)

## Trabalhar com fragmentos {#working-with-fragments}

### Configurar aparência do fragmento {#configure-fragment-appearance}

Qualquer fragmento inserido em formulários adaptáveis aparece como uma imagem de espaço reservado. O espaço reservado exibe títulos de até um máximo de dez painéis filhos no fragmento. Você pode configurar o AEM Forms para mostrar o fragmento completo em vez da imagem de espaço reservado.

Execute as seguintes etapas para mostrar fragmentos completos em formulários:

1. Vá para a página de configuração do console da Web do AEM em https:[*host*]:[*port*]/system/console/configMgr.

1. Pesquise e clique em Serviço **** de configuração de formulário adaptável para abri-lo no modo de edição.
1. Desative **[!UICONTROL a caixa de seleção Ativar espaço reservado no lugar do fragmento]** para mostrar fragmentos completos em vez da imagem do espaço reservado.

### Inserir um fragmento em um formulário adaptável {#insert-a-fragment-in-an-adaptive-form}

Os fragmentos de formulário adaptáveis criados aparecem na guia Fragmentos de formulário adaptáveis do localizador de conteúdo do AEM. Para inserir um fragmento de formulário adaptável em um formulário adaptável:

1. Abra o formulário adaptável, no modo de edição, no qual deseja inserir um fragmento de formulário adaptável.
1. Clique em **Assets** ![assets-browser](assets/assets-browser.png) na barra lateral. No navegador de ativos, selecione Fragmentos **de formulário** adaptáveis no menu suspenso.

   Você também pode optar por exibir todos os fragmentos de formulário adaptáveis ou filtrar com base em seu modelo de formulário - Modelo de formulário, Schema XML ou Básico.

1. Arraste e solte um fragmento de formulário adaptável no formulário adaptável.

   >[!NOTE]
   >
   >O fragmento de formulário adaptável não está habilitado para criação a partir do formulário adaptável. Além disso, não é possível usar um fragmento baseado em XSD em um formulário adaptável baseado em JSON e da maneira oposta.

O fragmento de formulário adaptável é inserido por referência no formulário adaptável e é sincronizado com o fragmento de formulário adaptável autônomo. Isso significa que, ao atualizar o fragmento do formulário adaptável, as alterações são refletidas em todos os formulários adaptáveis nos quais o fragmento é usado.

### Incorporar um fragmento em forma adaptável {#embed-a-fragment-in-adaptive-form}

Você pode incorporar um fragmento de formulário adaptável em um formulário adaptável clicando em **Incorporar ativo: &lt;*fragmentName*>** na barra de ferramentas do painel do fragmento adicionado, como mostrado na imagem de exemplo a seguir.

![Incorporar um fragmento de formulário no formulário adaptável](assets/embed-fragment.png)

>[!NOTE]
>
>O fragmento incorporado não está mais vinculado ao fragmento autônomo. É possível editar os componentes no fragmento incorporado a partir do formulário adaptável.

### Uso de fragmentos em fragmentos {#using-fragments-within-fragments}

É possível criar fragmentos de formulário adaptáveis aninhados, o que significa que você pode arrastar e soltar um fragmento em outro fragmento e pode ter uma estrutura de fragmento aninhada.

### Alterar fragmentos {#change-fragments}

É possível substituir ou alterar um fragmento de formulário adaptável por outro fragmento usando a propriedade **Selecionar ativo** de fragmento na caixa de diálogo Editar componente para um painel de fragmento de formulário adaptável.

## Mapeamento automático de fragmentos para vínculo de dados {#auto-mapping-of-fragments-for-data-binding}

Ao criar um fragmento de formulário adaptável usando um modelo de formulário XFA ou um tipo complexo XSD e arrastar e soltar o fragmento em um formulário adaptável, o fragmento XFA ou o tipo complexo XSD é automaticamente substituído pelo fragmento de formulário adaptável correspondente cuja raiz do modelo de fragmento é mapeada para o fragmento XFA ou para o Tipo complexo XSD.

É possível alterar o ativo do fragmento e seus vínculos na caixa de diálogo Editar componente.

>[!NOTE]
>
>Também é possível arrastar e soltar um fragmento de formulário adaptável vinculado da biblioteca do fragmento de formulário adaptável no localizador de conteúdo AEM e fornecer a referência de vínculo correta na caixa de diálogo Editar componente do painel do fragmento de formulário adaptável.

## Gerenciar fragmentos {#manage-fragments}

É possível executar várias operações em fragmentos de formulário adaptáveis usando a interface do usuário do AEM Forms.

1. Ir para `https://[hostname]:'port'/aem/forms.html`.

1. Clique em **Selecionar** na barra de ferramentas da interface do usuário do AEM Forms e selecione um fragmento de formulário adaptável. A barra de ferramentas exibe as seguintes operações que você pode executar no fragmento de formulário adaptável selecionado.

<table>
 <tbody>
  <tr>
   <td><p><strong>Operação</strong></p> </td>
   <td><p><strong>Descrição</strong></p> </td>
  </tr>
  <tr>
   <td><p>Abrir</p> </td>
   <td><p>Abre o fragmento de formulário adaptável selecionado no modo de edição.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Propriedades da exibição</p> </td>
   <td><p>Abre o painel Propriedades. No painel Propriedades, é possível visualização e editar propriedades, gerar uma pré-visualização e carregar uma imagem em miniatura do fragmento selecionado. For more information, see <a href="../../forms/using/manage-form-metadata.md" target="_blank">Managing metadata</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiar</p> </td>
   <td><p>Copia o fragmento selecionado. O botão Colar é exibido na barra de ferramentas.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Faz o download do fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visualizar</p> </td>
   <td><p>Fornece opções para pré-visualização o fragmento como um HTML ou uma pré-visualização personalizada mesclando dados de um arquivo XML com o fragmento. Para obter mais informações, consulte <a href="/help/forms/using/previewing-forms.md" target="_blank">Visualizar um formulário</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Revisão/gerenciamento de Start</p> </td>
   <td><p>Permite iniciar e gerenciar uma revisão do fragmento selecionado. Para obter mais informações, consulte <a href="../../forms/using/create-reviews-forms.md" target="_blank">Criação e gerenciamento de revisões</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Criar dicionário</p> </td>
   <td><p>Gera um dicionário para localizar o fragmento selecionado. Para obter mais informações, consulte <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">Localização de formulários</a>adaptáveis.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar/Desfazer publicação</p> </td>
   <td><p>Publica / despublica o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Excluir</p> </td>
   <td><p>Exclui o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
 </tbody>
</table>

## Localização de formulários adaptáveis contendo fragmentos {#localizing-adaptive-form-containing-fragments}

Para localizar um formulário adaptável que contenha fragmentos de formulário adaptáveis, é necessário localizar o fragmento e o formulário separadamente. A ideia é localizar um fragmento uma vez e reutilizá-lo em vários formulários adaptáveis.

>[!NOTE]
>
>As chaves de localização no fragmento não aparecerão no arquivo XLIFF para um formulário adaptável.

## Pontos principais a serem lembrados ao trabalhar com fragmentos {#key-points-to-remember-when-working-with-fragments}

* Verifique se o nome do fragmento é exclusivo. O fragmento não será criado se houver um fragmento existente com o mesmo nome.
* Em um formulário adaptável baseado em XDP, se você salvar um painel como fragmento que inclui outro fragmento XDP, o fragmento resultante será vinculado automaticamente ao fragmento XDP filho. No caso de um formulário adaptável baseado em XSD, o fragmento resultante será vinculado à raiz do schema.
* Quando você cria um fragmento de formulário adaptável, um nó de fragmento é criado, o que é semelhante ao nó guideContainer para um formulário adaptável, no CRXDe Lite.
* Um fragmento em um formulário adaptável que usa um modelo de dados de formulário diferente não é suportado. Por exemplo, um fragmento baseado em XDP não é suportado em um formulário adaptável baseado em XSD e vice-versa.
* Os fragmentos de formulário adaptáveis estão disponíveis para uso por meio da guia Fragmentos de formulário adaptáveis no localizador de conteúdo AEM.
* Qualquer expressão, script ou estilo em um fragmento de formulário adaptável independente é retido quando inserido por referência ou incorporado em um formulário adaptável.
* Não é possível editar um fragmento de formulário adaptável, que é inserido por referência, de dentro de um formulário adaptável. Para editar, edite o fragmento de formulário adaptável independente ou incorpore o fragmento no formulário adaptável.
* Ao publicar um formulário adaptável, é necessário publicar os fragmentos de formulário adaptável independentes inseridos por referência no formulário adaptável.
* Quando um fragmento de formulário adaptável atualizado é publicado novamente, as alterações são refletidas nas instâncias publicadas do formulário adaptável no qual o fragmento é usado.
* O formulário adaptável que contém o componente Verify não suporta usuários anônimos. Além disso, não é recomendado usar o componente Verify em um fragmento de formulário adaptável.
* (Somente ****Mac) Para garantir que a funcionalidade de fragmentos de formulário funcione perfeitamente em todos os cenários, adicione a seguinte entrada ao arquivo /private/etc/hosts:
   `127.0.0.1 <Host machine>` Máquina **** host: A máquina Apple Mac na qual o AEM Forms é implantado.

## Fragmentos de referência {#reference-fragments}

Os fragmentos de formulário adaptável de referência que podem ser usados para criar o formulário estão disponíveis. For more information, see [Reference Fragments](../../forms/using/reference-adaptive-form-fragments.md).
