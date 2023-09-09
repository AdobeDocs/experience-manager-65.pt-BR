---
title: Fragmentos de formulário adaptável
seo-title: Adaptive form fragments
description: Formulários adaptáveis fornecem um mecanismo para criar um segmento de formulário, como um painel ou um grupo de campos, como usá-lo em qualquer formulário adaptável. Também é possível salvar um painel existente como fragmento.
seo-description: Adaptive forms provides a mechanism to create a form segment, such as a panel or a group of fields, as use it in any adaptive form. You can also save an existing panel as fragment.
uuid: bb4830b5-82a0-4026-9dae-542daed10e6f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 1a32eb24-db3b-4fad-b1c7-6326b5af4e5e
docset: aem65
feature: Adaptive Forms
exl-id: 2f276e9d-b3c1-48f7-a94a-bdf7eb15a031
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2111'
ht-degree: 1%

---

# Fragmentos de formulário adaptável{#adaptive-form-fragments}

<span class="preview"> O Adobe recomenda o uso da captura de dados moderna e extensível [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) para [criação de um novo Forms adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adição de Forms adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

Embora cada formulário seja projetado para um propósito específico, há alguns segmentos comuns na maioria dos formulários, como o de fornecer detalhes pessoais, como nome e endereço, detalhes da família, detalhes de renda etc. Os desenvolvedores de formulários são necessários para criar esses segmentos comuns sempre que um novo formulário for criado.

Formulários adaptáveis fornecem um mecanismo conveniente para criar segmentos de formulários, como um painel ou um grupo de campos, somente uma vez e reutilizá-los em formulários adaptáveis. Esses segmentos reutilizáveis e independentes são chamados de fragmentos de formulário adaptáveis.

## Criar um fragmento {#create-a-fragment}

É possível criar um fragmento de formulário adaptável do zero ou salvar um painel em um formulário adaptável existente como fragmento.

### Criar fragmento do zero {#create-fragment-from-scratch}

1. Faça logon no instância de autor do AEM Forms em https://[*hostname*]:[*porta*]/aem/forms.html.
1. Clique **Criar > fragmento** de formulário adaptável.
1. Especifique título, nome, descrição e tags para o fragmento.

   >[!NOTE]
   >
   >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

1. Clique para abrir a **Modelo de formulário** e na guia **Selecionar de** selecione um dos seguintes modelos para o fragmento:

   * **Nenhum**: especifica criar o fragmento do zero sem usar nenhum modelo de formulário.
   * **Modelo de** formulário: especifica a criação do fragmento usando um modelo XDP carregado para AEM Forms. Selecione o modelo XDP apropriado como o modelo de formulário para o fragmento.

   ![Criação de um formulário adaptável usando modelo de formulário como modelo](assets/form-template-model.png)

   Os subformulários marcados como fragmentos no modelo de formulário selecionado também são exibidos. Você pode selecionar um subformulário para fragmento de formulário adaptável na lista suspensa.

   ![Selecionar subformulários do modelo de formulário especificado](assets/fragment-subform.png)

   Além disso, você pode criar um fragmento de formulário adaptável usando subformulários que não estão marcados como fragmentos no modelo de formulário especificando a expressão SOM para o subformulário na caixa suspensa.

   * **Esquema XML**: Especifica como criar o fragmento usando um esquema XML carregado no AEM Forms. Você pode fazer upload ou selecionar dentre os esquemas XML disponíveis como o modelo de formulário do fragmento.

   ![Criar um fragmento de formulário adaptável com base em um esquema XML como modelo](assets/xml-schema-model.png)

   Você também pode criar um fragmento de formulário adaptável selecionando um complexType presente no esquema selecionado na caixa suspensa.

   ![Selecione um tipo complexo no modelo de esquema XML especificado](assets/complex-type.png)

1. Clique em **Criar** e clique em **Abertura** para abrir o fragmento, com um modelo padrão, no modo de edição.

No modo de edição, você pode arrastar e soltar qualquer componente de formulário adaptável do sidekick do AEM no fragmento. Para obter informações sobre componentes de formulários adaptáveis, consulte [Introdução à criação de formulários adaptáveis](../../forms/using/introduction-forms-authoring.md).

Além disso, se você selecionou um esquema XML ou modelo de formulário XDP como o modelo de formulário do fragmento, uma nova guia que exibe a hierarquia do modelo de formulário aparece no localizador de conteúdo. Ela permite arrastar e soltar elementos do modelo de formulário no fragmento. Os elementos de modelo de formulário adicionados são convertidos em componentes de formulário, ao mesmo tempo em que retêm as propriedades originais do XDP ou XSD associado.

### Salvar painel como um fragmento {#save-panel-as-a-fragment}

1. Abra um formulário adaptável que contenha o painel que você deseja salvar como fragmento de formulário adaptável.
1. Na barra de ferramentas do painel, clique em **[!UICONTROL Salvar como fragmento]**. A caixa de diálogo Salvar como fragmento é aberta.

   >[!NOTE]
   >
   >Se o painel que você está salvando como fragmento contiver painel secundário, o fragmento resultante os incluirá.

1. Na caixa de diálogo Criação de fragmento, especifique as seguintes informações:

   * **Nome**: Nome do fragmento. O valor padrão é o nome do elemento do painel. É um campo obrigatório.
     >[!NOTE]
     >
     >Certifique-se de especificar um nome exclusivo para o fragmento. Se já existir outro fragmento com o mesmo nome, o fragmento não será criado.

   * **Título**: Título do fragmento. O valor padrão é o título do painel.

   * **Descrição**: Descrição do fragmento.

   * **Tags**: marca os metadados do fragmento.

   * **Caminho de destino**: Caminho do repositório onde o fragmento será salvo. Se você não especificar um caminho, um nó com o mesmo nome do fragmento será criado ao lado do nó que contém o formulário adaptável. O fragmento é salvo neste nó.

   * **Modelo de formulário**: Dependendo do modelo de formulário para o formulário adaptável, esse campo exibe a variável **Esquema XML**, **Modelo de formulário** ou **Nenhum**. É um campo não editável.

   * **Raiz do modelo de fragmento**: aparece somente em formulários adaptáveis baseados em XSD. Especifica a raiz do modelo de fragmento. Você pode escolher **/** ou o tipo complexo XSD no menu suspenso. Observe que você só poderá reutilizar o fragmento em outro formulário adaptável se selecionar o tipo complexo como a raiz do modelo de fragmento.
Se você escolher **/** como a raiz do modelo de fragmento, a árvore XSD completa da raiz fica visível na guia modelo de dados de formulário adaptável. Para uma raiz de modelo de fragmento de tipo complexo, somente os descendentes do tipo complexo selecionado ficam visíveis na guia modelo de dados de formulário adaptável.

   * **XSD Ref**: aparece somente em formulários adaptáveis baseados em XSD. Ela exibe a localização do esquema XML.

   * **XDP Ref**: aparece somente em formulários adaptáveis baseados em XDP. Ela exibe o local do modelo de formulário XDP.

   ![save-fragment](assets/save-fragment.png)

   Caixa de diálogo Salvar como fragmento

1. Clique em **OK**.

   O painel é salvo no local especificado ou padrão no repositório. No formulário adaptável, o painel é substituído por um instantâneo do fragmento. Como mostrado abaixo, o painel Informações gerais e seus painéis secundários, Informações pessoais e Endereço, são salvos como um fragmento.

   Para editar o fragmento, clique em **[!UICONTROL Editar ativo]** na barra de ferramentas do painel. O fragmento é aberto em uma nova guia ou janela no modo de edição.

   ![Edição de fragmento](assets/edit-fragment.png)

## Trabalho com fragmentos {#working-with-fragments}

### Configurar a aparência do fragmento {#configure-fragment-appearance}

Qualquer fragmento inserido em formulários adaptáveis é exibido como uma imagem de espaço reservado. O espaço reservado exibe títulos de até dez painéis secundários no fragmento. Você pode configurar o AEM Forms para mostrar o fragmento completo em vez da imagem de espaço reservado.

Execute as seguintes etapas para mostrar fragmentos completos em formulários:

1. Vá para a página de configuração do console da Web do AEM em https:[*host*]:[*porta*]/system/console/configMgr

1. Pesquisar e clicar **[!UICONTROL Configuração do canal da Web do formulário adaptável e da comunicação interativa]** para abri-lo no modo de edição.
1. Desative **[!UICONTROL Ativar Espaço reservado no lugar da caixa de seleção Fragmento]** para mostrar fragmentos completos em vez da imagem de espaço reservado.

### Inserir um fragmento em um formulário adaptável {#insert-a-fragment-in-an-adaptive-form}

Os fragmentos de formulários adaptáveis criados aparecem nos Fragmentos de formulário adaptável guia do localizador AEM conteúdo. Para inserir um fragmento de formulário adaptável em um formulário adaptável:

1. Abra o formulário adaptável, no modo de edição, no qual deseja inserir um fragmento de formulário adaptável.
1. Clique em **Assets** ![assets-browser](assets/assets-browser.png) na barra lateral. No navegador de ativos, selecione **Fragmentos do formulário adaptável** no menu suspenso.

   Também é possível optar por exibir todos os fragmentos de formulário adaptável ou filtrar com base em seu modelo de formulário - Modelo de formulário, Esquema XML ou Básico.

1. Arraste e solte um fragmento de formulário adaptável no formulário adaptável.

   >[!NOTE]
   >
   >O fragmento de formulário adaptável não é habilitado para criação a partir do formulário adaptável. Além disso, não é possível usar um fragmento baseado em XSD em um formulário adaptável baseado em JSON e da maneira oposta.

O fragmento de formulário adaptável é inserido por referência no formulário adaptável e é sincronizado com o fragmento de formulário adaptável independente. Significa que ao atualizar o fragmento de formulário adaptável, as alterações refletem em todos os formulários adaptáveis nos quais o fragmento é usado.

### Incorporar um fragmento no formulário adaptável {#embed-a-fragment-in-adaptive-form}

Você pode optar por incorporar um fragmento de formulário adaptável em um formulário adaptável clicando em **Incorporar ativo: &lt;*fragmentName*>** na barra de ferramentas do painel do fragmento adicionado, conforme mostrado no exemplo de imagem a seguir.

![Incorporar um fragmento de formulário no formulário adaptável](assets/embed-fragment.png)

>[!NOTE]
>
>O fragmento incorporado não está mais vinculado ao fragmento independente. Você pode editar os componentes no fragmento incorporado a partir do formulário adaptável.

### Uso de fragmentos dentro de fragmentos {#using-fragments-within-fragments}

É possível criar fragmentos de formulário adaptáveis aninhados, o que significa que você pode arrastar e soltar um fragmento em outro fragmento e pode ter uma estrutura de fragmento aninhada.

### Alterar fragmentos {#change-fragments}

É possível substituir ou alterar um fragmento de formulário adaptável por outro fragmento usando o **Selecionar ativo do fragmento** na caixa de diálogo Editar componente para um painel de fragmento de formulário adaptável.

## Mapeamento automático de fragmentos para associação de dados {#auto-mapping-of-fragments-for-data-binding}

Ao criar um fragmento de formulário adaptável usando um modelo de formulário XFA ou tipo complexo XSD e arrastar e soltar o fragmento em um formulário adaptável, o fragmento XFA ou o tipo complexo XSD é substituído automaticamente pelo fragmento de formulário adaptável correspondente cuja raiz do modelo de fragmento é mapeada para o fragmento XFA ou o Tipo complexo XSD.

É possível alterar o ativo do fragmento e suas associações na caixa de diálogo Editar componente.

>[!NOTE]
>
>Você também pode arrastar e soltar um fragmento de formulário adaptável vinculado da biblioteca de fragmentos de formulário adaptável no localizador de conteúdo do AEM e fornecer a referência de vinculação correta na caixa de diálogo Editar componente do painel de fragmentos de formulário adaptável.

## Gerenciar fragmentos {#manage-fragments}

É possível executar várias operações em fragmentos de formulário adaptáveis usando a interface do usuário do AEM Forms.

1. Acesse `https://[hostname]:'port'/aem/forms.html`.

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
   <td><p>Abre o painel Propriedades. No painel Propriedades, é possível visualizar e editar propriedades, gerar uma visualização e fazer upload de uma imagem em miniatura para o fragmento selecionado. Para obter mais informações, consulte <a href="../../forms/using/manage-form-metadata.md" target="_blank">Gerenciamento de metadados</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Copiar</p> </td>
   <td><p>Copia o fragmento selecionado. O botão Colar aparece na barra de ferramentas.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Download</p> </td>
   <td><p>Baixa o fragmento selecionado.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Visualização</p> </td>
   <td><p>Fornece opções para visualizar o fragmento como um HTML ou uma visualização personalizada mesclando dados de um arquivo XML com o fragmento. Para obter mais informações, consulte <a href="/help/forms/using/previewing-forms.md" target="_blank">Pré-visualização de um formulário</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Iniciar revisão/Gerenciar revisão</p> </td>
   <td><p>Permite iniciar e gerenciar uma revisão do fragmento selecionado. Para obter mais informações, consulte <a href="../../forms/using/create-reviews-forms.md" target="_blank">Criar e gerenciar revisões</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Criar dicionário</p> </td>
   <td><p>Gera um dicionário para localizar o fragmento selecionado. Para obter mais informações, consulte <a href="/help/forms/using/lazy-loading-adaptive-forms.md" target="_blank">Localização de formulários adaptáveis</a>.<br /> <br /> </p> </td>
  </tr>
  <tr>
   <td><p>Publicar/Desfazer a publicação</p> </td>
   <td><p>Publica/cancela a publicação do fragmento selecionado.<br /> <br /> </p> </td>
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

* Certifique-se de que o nome do fragmento seja exclusivo. O fragmento não é criado se houver um fragmento existente com o mesmo nome.
* Em um formulário adaptável baseado em XDP, se você salvar um painel como fragmento que inclui outro fragmento XDP, o fragmento resultante será vinculado automaticamente ao fragmento XDP secundário. No caso de um formulário adaptável baseado em XSD, o fragmento resultante será vinculado à raiz do esquema.
* Ao criar um fragmento de formulário adaptável, um nó de fragmento é criado, o que é semelhante ao nó guideContainer de um formulário adaptável, no CRXDe Lite.
* Um fragmento em um formulário adaptável que usa um modelo de dados de formulário diferente não é compatível. Por exemplo, um fragmento baseado em XDP não é suportado em um formulário adaptável baseado em XSD e vice-versa.
* Fragmentos de formulários adaptáveis estão disponíveis para uso por meio dos Fragmentos de formulário adaptável guia em AEM conteúdo localizador.
* Qualquer expressão, script ou estilo em um fragmento de formulário adaptável independente é retido quando é inserido por referência ou incorporado em um formulário adaptável.
* Não é possível editar um fragmento de formulário adaptável, que é inserido por referência, de dentro de um formulário adaptável. Para editar, edite o fragmento de formulário adaptável independente ou incorpore o fragmento no formulário adaptável.
* Ao publicar um formulário adaptável, você precisa publicar os fragmentos de formulário adaptáveis independentes inseridos por referência no formulário adaptável.
* Ao republicar um fragmento de formulário adaptável atualizado, as alterações são refletidas nas instâncias publicadas do formulário adaptável no qual o fragmento é usado.
* O formulário adaptável contendo o componente Verificar não é compatível com usuários anônimos. Além disso, não é repromendado para usar o componente Verificar em um fragmento de formulário adaptável.
* (**Somente** Mac) Para garantir que os fragmentos de formulário funcionalidade funciona perfeitamente em todos os cenários, adicione a seguinte entrada ao arquivo /private/etc/hosts:
  `127.0.0.1 <Host machine>`**Máquina de host**: a máquina Apple Mac na qual o AEM Forms é implantado.

## Fragmentos de referência {#reference-fragments}

Os fragmentos de formulário adaptáveis de referência que você pode usar para criar seu formulário estão disponíveis. Para obter mais informações, consulte [Fragmentos de referência](../../forms/using/reference-adaptive-form-fragments.md).
