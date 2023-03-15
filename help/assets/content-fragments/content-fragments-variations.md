---
title: Variações - Criação dos fragmentos de conteúdo
description: Entenda como as variações podem tornar o conteúdo sem interface AEM ainda mais flexível, permitindo que você crie conteúdo para o fragmento e, em seguida, crie variações desse conteúdo de acordo com a finalidade.
feature: Content Fragments
role: User
exl-id: 50982ede-7ccf-45b2-b0dd-a49d23e0f971
source-git-commit: bb5d39277db10fd8d3b436c8d1f40d9d2010adee
workflow-type: tm+mt
source-wordcount: '2426'
ht-degree: 87%

---

# Variações - Criação dos fragmentos de conteúdo{#variations-authoring-fragment-content}

[Variações](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) são um recurso importante de fragmentos de conteúdo AEM, pois permitem criar e editar cópias do conteúdo principal para uso em canais e/ou cenários específicos, tornando a entrega de conteúdo sem cabeçalho ainda mais flexível.

Na guia **Variações**, é possível:

* [Inserir o conteúdo](#authoring-your-content) para o fragmento,
* [Criar e gerenciar variações](#managing-variations) do conteúdo **Principal**,

Executar uma variedade de outras ações, dependendo do tipo de dados que está sendo editado; por exemplo:

* [Inserir ativos visuais no fragmento](#inserting-assets-into-your-fragment) (imagens)

* Selecione entre [Rich text](#rich-text), [Texto sem formatação](#plain-text) e [Markdown](#markdown) para edição

* [Fazer upload de conteúdo](#uploading-content)

* [Visualizar as principais estatísticas](#viewing-key-statistics) (sobre textos multilinha)

* [Resumir texto](#summarizing-text)

* [Sincronizar as variações com o conteúdo Principal](#synchronizing-with-master)

>[!CAUTION]
>
>Depois que um fragmento tiver sido publicado e/ou referenciado, o AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Criação de conteúdo {#authoring-your-content}

Ao abrir o fragmento de conteúdo para edição, a guia **Variações** será aberta por padrão. Aqui é possível criar conteúdo para o Principal ou quaisquer variações que você possua. O fragmento estruturado contém vários campos, de vários tipos de dados, que foram definidos no modelo de conteúdo.

Por exemplo:

![editor de tela cheia](assets/cfm-variations-02.png)

É possível:

* Faça edições no seu conteúdo diretamente no **Variações** Guia; cada tipo de dados fornece opções de edição diferentes, por exemplo:

   * para campos de **Texto multilinha**, também é possível abrir o [editor de tela cheia](#full-screen-editor) para:

      * selecionar o [Formato](#formats)
      * ver mais opções de edição (para formato [Rich text](#rich-text))
      * acessar uma variedade de [ações](#actions)
   * Para campos de **Referência do fragmento**, a opção [Editar fragmento de conteúdo](#fragment-references-edit-content-fragment) pode estar disponível, dependendo da definição do modelo.


* Atribuir **Tags** à variação atual; as tags podem ser adicionadas, atualizadas e removidas

   * As [Tags](/help/sites-authoring/tags.md) são particularmente eficientes ao organizar os fragmentos, pois podem ser usadas para a classificação de conteúdo e taxonomia. As tags podem ser usadas para encontrar conteúdo (por tags) e aplicar operações em massa.

      * As pesquisas por uma tag retornarão o fragmento, com a variação marcada realçada.
      * Tags de variação também podem ser usadas para agrupar variações de um perfil específico da Rede de entrega de conteúdo (CDN) (para armazenamento em cache CDN), em vez de usar o nome da variação.

      Por exemplo, você pode marcar fragmentos relevantes como &quot;lançamento de Natal&quot; para permitir a navegação somente nesses como um subconjunto ou copiá-los para uso com outro lançamento futuro em uma nova pasta.
   >[!NOTE]
   >
   >**Tags** também pode ser adicionado (para a função **Principal** como parte da [Metadados](/help/assets/content-fragments/content-fragments-metadata.md)

* [Criar e gerenciar variações](#managing-variations) do conteúdo **Principal.**

### Editor de tela cheia {#full-screen-editor}

Ao editar um campo de texto multilinha, você pode abrir o editor de tela cheia; toque ou clique no texto e selecione o seguinte ícone de ação:

![ícone do editor de tela cheia](assets/cfm-variations-03.png)

Isso abrirá o editor de texto em tela cheia:

![editor de tela cheia](assets/cfm-variations-fullscreentexteditor.png)

O editor de texto em tela cheia fornece:

* Acesso a várias [ações](#actions)
* Dependendo do [formato](#formats), opções adicionais de formatação ([Rich text](#rich-text))

### Ações {#actions}

As seguintes ações também estão disponíveis (para todos os [formatos](#formats)) quando o editor de tela cheia (ou seja, texto multilinha) estiver aberto:

* Selecionar o [formato](#formats) ([Rich text](#rich-text), [Texto sem formatação](#plain-text) ou [Markdown](#markdown))

* [Fazer upload de conteúdo](#uploading-content)

* [Mostrar estatísticas do texto](#viewing-key-statistics)

* [Sincronizar com o Principal](#synchronizing-with-master) (ao editar uma variação)

* [Resumir texto](#summarizing-text)

### Formatos {#formats}

As opções para editar texto de várias linhas dependem do formato selecionado:

* [Texto formatado](#rich-text)
* [Texto sem formatação](#plain-text)
* [Markdown](#markdown)

O formato pode ser selecionado no editor de tela cheia.

### Rich Text {#rich-text}

A edição de rich text permite formatar:

* Negrito
* Itálico
* Sublinhado
* Alinhamento: esquerda, centro, direita
* Lista com marcadores
* Lista numerada
* Recuo: aumentar, diminuir
* Criar/quebrar hiperlinks
* Colar texto/do Word
* Inserir uma tabela
* Estilo do parágrafo: parágrafo, cabeçalho 1/2/3
* [Inserir ativo](#inserting-assets-into-your-fragment)
* Abrir o editor de tela cheia, onde as seguintes opções de formatação estão disponíveis:
   * Pesquisar
   * Localizar/substituir
   * Verificador ortográfico
   * [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Inserir fragmento de conteúdo](#inserting-content-fragment-into-your-fragment); disponível quando o campo de **Texto de várias linhas** está configurado para **Permitir referência de fragmento**.

As [ações](#actions) também podem ser acessadas pelo editor de tela cheia.

### Texto sem formatação {#plain-text}

O texto sem formatação permite inserir rapidamente conteúdo sem formatação ou markdown. Também é possível abrir o editor de tela cheia para obter mais [ações](#actions).

>[!CAUTION]
>
>Se selecionar **Texto sem formatação**, você poderá perder qualquer formatação, marcação e/ou ativos inseridos no **Rich Text** ou no **Markdown**.

### Markdown {#markdown}

>[!NOTE]
>
>Para obter informações completas, consulte a documentação sobre [Markdown](/help/assets/content-fragments/content-fragments-markdown.md).

Isso permite formatar o texto usando markdown. Você pode definir:

* Cabeçalhos
* Parágrafos e quebras de linha
* Links
* Imagens
* Citações em bloco
* Listas
* Ênfase
* Blocos de código
* Escapes de barra invertida

Você também pode abrir o editor de tela cheia para obter mais [ações](#actions).

>[!CAUTION]
>
>Se você alternar entre **Rich Text** e **Markdown**, poderá ver efeitos inesperados com Cotas de bloqueio e Bloqueios de código, já que esses dois formatos podem ter diferenças na maneira como são tratados.

### Referências do fragmento {#fragment-references}

Se o Modelo do fragmento de conteúdo contiver Referências de fragmento, os autores do fragmento podem ter opções adicionais:

* [Editar fragmento de conteúdo](#fragment-references-edit-content-fragment)
* [Novo fragmento de conteúdo](#fragment-references-new-content-fragment)

![Referências do fragmento](assets/cfm-variations-12.png)

#### Editar fragmento de conteúdo {#fragment-references-edit-content-fragment}

A opção **Editar fragmento do conteúdo** abrirá esse fragmento em uma nova guia de janela.

<!--
The option **Edit Content Fragment** will open that fragment in a new editor tab (within the same browser tab).

Selecting the original tab again (for example, **Little Pony Inc.**), will close this secondary tab (in this case, **Adam Smith**).

![Fragment References](assets/cfm-variations-editreference.png)
-->

#### Novo fragmento de conteúdo {#fragment-references-new-content-fragment}

A opção **Novo fragmento de conteúdo** permitirá criar um fragmento totalmente novo. Para isso, uma variação do assistente de criação de fragmento de conteúdo será aberta no editor.

Será possível criar um novo fragmento ao:

1. Navegar até a pasta desejada e selecioná-la.
1. Selecionar **Próximo**.
1. Especificar propriedades; por exemplo, **Título**.
1. Selecionar **Criar**.
1. Finalmente:
   1. **Concluído** retornará para o fragmento original e referenciará o novo fragmento.
   1. **Abrir** referenciará o novo fragmento e o abrirá para edição em uma nova guia do navegador.

### Visualizar as principais estatísticas {#viewing-key-statistics}

Quando o editor de tela cheia estiver aberto, a ação **Estatísticas de texto** exibirá uma variedade de informações sobre o texto.

Por exemplo:

![statistics](assets/cfm-variations-04.png)

### Fazer upload de conteúdo {#uploading-content}

Para facilitar o processo de criação de fragmentos de conteúdo, é possível fazer o upload de um texto preparado em um editor externo e adicioná-lo diretamente ao fragmento.

### Resumo de texto {#summarizing-text}

O resumo de texto foi criado para ajudar os usuários a reduzir o comprimento do texto para um número predefinido de palavras, mas mantendo os pontos principais e o significado geral.

>[!NOTE]
>
>Em um nível mais técnico, o sistema mantém as frases que julga fornecer a *melhor relação entre densidade e exclusividade das informações* de acordo com algoritmos específicos.

>[!CAUTION]
>
>O fragmento de conteúdo deve ter uma pasta de idioma válida (código ISO) como ancestral; ela serve para determinar o modelo de idioma a ser usado.
>
>Por exemplo, `en/`, como no seguinte caminho:
>
>  `/content/dam/my-brand/en/path-down/my-content-fragment`

>[!CAUTION]
O inglês está disponível pronto para uso.
Outros idiomas estão disponíveis como Pacotes de modelo de idioma no Compartilhamento de pacotes:
* [Francês (fr)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-fr)
* [Alemão (de)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-de)
* [Italiano (it)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-it)
* [Espanhol (es)](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/product/smartcontent-model-es)
>


1. Selecione o **Principal** ou a variação exigida.
1. Abra o editor de tela cheia.

1. Selecione **Resumir texto** na barra de ferramentas.

   ![resumo](assets/cfm-variations-05.png)

1. Especifique o número alvo de palavras e selecione **Iniciar**:
1. O texto original é apresentado lado a lado com o resumo proposto:

   * As frases que serão eliminadas são destacadas em vermelho e tachadas.
   * Clique em qualquer frase destacada para mantê-la no conteúdo resumido.
   * Clique em qualquer frase não destacada para eliminá-la.

1. Selecione **Resumir** para confirmar as alterações.

1. O texto original é apresentado lado a lado com o resumo proposto:

   * As frases que serão eliminadas são destacadas em vermelho e tachadas.
   * Clique em qualquer frase destacada para mantê-la no conteúdo resumido.
   * Clique em qualquer frase não destacada para eliminá-la.
   * As estatísticas do resumo são apresentadas: **Real** e **Alvo**-
   * Você pode **Visualizar** as alterações.

   ![comparação de resumo](assets/cfm-variations-06.png)

### Anotação de um fragmento de conteúdo {#annotating-a-content-fragment}

Para anotar um fragmento:

1. Selecione o **Principal** ou a variação exigida.

1. Abra o editor de tela cheia.

1. O ícone de **Anotar** está disponível na barra de ferramentas superior. Você pode selecionar algum texto, se necessário.

   ![anotar](assets/cfm-variations-07.png)

1. Uma caixa de diálogo será aberta. Aqui é possível inserir sua anotação.

   ![anotar](assets/cfm-variations-07a.png)

1. Selecione **Aplicar** na caixa de diálogo.

   ![anotar](assets/cfm-variations-annotations-apply-icon.png)

   Se a anotação tiver sido aplicada ao texto selecionado, esse texto permanecerá destacado.

   ![anotar](assets/cfm-variations-07b.png)

1. Feche o editor de tela cheia; as anotações permanecem destacadas. Se selecionada, uma caixa de diálogo será aberta para que você possa continuar a editar a anotação.

1. Selecione **Salvar**.

1. Feche o editor de tela cheia; as anotações permanecem destacadas. Se selecionada, uma caixa de diálogo será aberta para que você possa continuar a editar a anotação.

   ![anotar](assets/cfm-variations-07c.png)

### Visualizar, editar e excluir anotações {#viewing-editing-deleting-annotations}

Anotações:

* São indicadas pelo destaque no texto, no modo de tela cheia e no modo normal do editor. Detalhes completos de uma anotação podem ser visualizados, editados e/ou excluídos ao clicar no texto destacado, o que abrirá novamente a caixa de diálogo.

   >[!NOTE]
   Um seletor suspenso é fornecido se várias anotações tiverem sido aplicadas a um texto.

* Quando você exclui o texto inteiro ao qual a anotação foi aplicada, a anotação também é excluída.

* Podem ser listadas e excluídas selecionando a guia **Anotações** no editor do fragmento.

   ![Anotações](assets/cfm-variations-08.png)

* Podem ser visualizadas e excluídas na [Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) do fragmento selecionado.

### Inserir ativos no fragmento {#inserting-assets-into-your-fragment}

Para facilitar o processo de criação de fragmentos de conteúdo, você pode adicionar [Ativos](/help/assets/manage-assets.md) (imagens) diretamente no fragmento.

Eles serão adicionados à sequência de parágrafo do fragmento sem qualquer formatação; a formatação pode ser feita quando o [fragmento for usado/referenciado em uma página](/help/sites-authoring/content-fragments.md).

>[!CAUTION]
Esses ativos não podem ser movidos ou excluídos em uma página de referência. Isso deve ser feito no editor do fragmento.
No entanto, a formatação do ativo (por exemplo, seu tamanho) deve ser feita no [editor de páginas](/help/sites-authoring/content-fragments.md). A representação do ativo no editor de fragmento serve meramente para a criação do fluxo de conteúdo.

>[!NOTE]
Existem vários métodos de adicionar [imagens](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

1. Posicione o cursor na posição que deseja adicionar a imagem.
1. Use o ícone **Inserir ativo** para abrir a caixa de diálogo de pesquisa.

   ![ícone inserir ativo](assets/cfm-variations-09.png)

1. Na caixa de diálogo, é possível:

   * navegar até o ativo necessário no DAM
   * pesquisar o ativo no DAM

   Depois de localizado, selecione o ativo necessário clicando na miniatura.

1. Use **Selecionar** para adicionar o ativo ao sistema de parágrafo do fragmento de conteúdo no local atual.

   >[!CAUTION]
   Se, após adicionar um ativo, você alterar o formato para:
   * **Texto simples:** o ativo será completamente perdido do fragmento.
   * **Marcação**: o ativo não estará visível, mas ainda estará lá ao retornar para **Rich Text**.


### Inserir um fragmento de conteúdo no fragmento {#inserting-content-fragment-into-your-fragment}

Para facilitar o processo de criação de fragmentos de conteúdo, também é possível adicionar outro fragmento de conteúdo ao seu fragmento.

Eles serão adicionados como referência, no local atual no fragmento.

>[!NOTE]
Essa opção está disponível quando o **Texto multilinha** é configurado com a opção **Permitir referência de fragmento**.

>[!CAUTION]
Esses ativos não podem ser movidos ou excluídos em uma página de referência. Isso deve ser feito no editor do fragmento.
No entanto, a formatação do ativo (por exemplo, seu tamanho) deve ser feita no [editor de páginas](/help/sites-authoring/content-fragments.md). A representação do ativo no editor de fragmento serve meramente para a criação do fluxo de conteúdo.

>[!NOTE]
Existem vários métodos de adicionar [imagens](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) ao fragmento e/ou página.

1. Posicione o cursor na posição em que deseja adicionar o fragmento.
1. Use o ícone **Inserir fragmento de conteúdo** para abrir a caixa de diálogo de pesquisa.

   ![ícone Inserir fragmento de conteúdo](assets/cfm-variations-13.png)

1. Na caixa de diálogo, é possível:

   * navegar até o fragmento necessário na pasta de ativos
   * pesquisar o fragmento

   Depois de localizado, selecione o fragmento necessário clicando na miniatura.

1. Use **Selecionar** para adicionar uma referência ao fragmento de conteúdo selecionado no seu fragmento de conteúdo atual (no local atual).

   >[!CAUTION]
   Se, após adicionar uma referência a outro fragmento, você alterar o formato para:
   * **Texto sem formatação:** a referência será completamente removida do fragmento.
   * **Markdown**: a referência permanecerá.


## Gerenciamento de variações {#managing-variations}

### Criar uma variação {#creating-a-variation}

As variações permitem selecionar o conteúdo **Principal** e alterá-lo de acordo com a finalidade (se necessário).

Para criar uma nova variação:

1. Abra o fragmento e verifique se o painel lateral está visível.
1. Selecione **Variações** na barra de ícones, no painel lateral.
1. Selecione **Criar variação**.
1. Uma caixa de diálogo será aberta. Especifique o **Título** e a **Descrição** da nova variação.
1. Selecione **Adicionar**; o fragmento **Mestre** será copiado para a nova variação, que agora está aberta para [edição](#editing-a-variation).

   >[!NOTE]
   Ao criar uma nova variação, é sempre o **Principal** que é copiado, não a variação que está aberta no momento.

   >[!NOTE]
   Ao criar uma nova variação, todas as variáveis **Tags** atualmente atribuído ao **Principal** são copiadas para sua nova variação.

### Editar uma variação {#editing-a-variation}

Você pode fazer alterações no conteúdo de variação após:

* [Criar a variação](#creating-a-variation).
* Abrir um fragmento existente e, em seguida, selecionar a variação necessária no painel lateral.

![editar uma variação](assets/cfm-variations-10.png)

### Renomear uma variação {#renaming-a-variation}

Para renomear uma variação existente:

1. Abra o fragmento e selecione **Variações** no painel lateral.
1. Selecione a variação necessária.
1. Selecione **Renomear** no menu suspenso **Ações**.

1. Digite o novo **Título** e/ou **Descrição** na caixa de diálogo resultante.

1. Confirme a ação **Renomear**.

>[!NOTE]
Isso só afeta o **Título** da variação.

### Excluir uma Variação {#deleting-a-variation}

Para excluir uma variação existente:

1. Abra o fragmento e selecione **Variações** no painel lateral.
1. Selecione a variação necessária.
1. Selecione **Excluir** no menu suspenso de **Ações**.

1. Confirme a ação de **Exclusão** na caixa de diálogo.

>[!NOTE]
Não é possível excluir o **Principal**.

### Sincronização com o Principal {#synchronizing-with-master}

O **Principal** é parte integral de um fragmento de conteúdo e, por definição, contém a cópia principal do conteúdo, enquanto as variações contêm as versões individuais atualizadas e personalizadas desse conteúdo. Quando o Principal é atualizado, é possível que essas alterações também sejam relevantes para as variações e, portanto, precisem ser propagadas para elas.

Ao editar uma variação, você tem acesso à ação para sincronizar o elemento atual da variação com o Principal. Isso permite copiar automaticamente as alterações feitas no Principal para a variação necessária.

>[!CAUTION]
A sincronização só está disponível para copiar alterações *do **Principal**para a variação*.
Somente o elemento atual da variação será sincronizado.
A sincronização só funciona na variável **Texto de várias linhas** tipo de dados.
A transferência de alterações *de uma variação para o **Principal*** não está disponível como uma opção.

<!-- needs new screenshot for synchronize effect -->

1. Abra o fragmento de conteúdo no editor de fragmentos. Certifique-se de que o **Principal** foi editado.

1. Selecione uma variação específica e, em seguida, a ação de sincronização apropriada:

   * no seletor suspenso de **Ações** — **Sincronizar elemento atual com o Principal**

      ![sincronização com o Principal](assets/cfm-variations-11a.png)

   * a barra de ferramentas do editor de tela cheia — **Sincronizar com o Principal**

      ![sincronização com o Principal](assets/cfm-variations-11b.png)

1. O Principal e a variação serão mostrados lado a lado:

   * verde indica conteúdo adicionado (à variação)
   * vermelho indica conteúdo removido (da variação)
   * azul indica texto substituído

   ![sincronização com o Principal](assets/cfm-variations-11c.png)

1. Selecionar **Sincronizar**, a variação será atualizada e exibida.
