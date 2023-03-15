---
title: Gerenciamento dos Fragmentos de conteúdo
description: Saiba como usar o console Assets para gerenciar os Fragmentos de conteúdo AEM, a base do seu conteúdo sem periféricos.
feature: Content Fragments
role: User
exl-id: 25c91a85-06ff-4666-a809-46778a689e25
source-git-commit: 20d46a7c37663dac36e6af9582d569a7f782eab7
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 81%

---

# Gerenciamento dos Fragmentos de conteúdo {#managing-content-fragments}

Saiba como usar o console Assets para gerenciar os Fragmentos de conteúdo AEM, a base do seu conteúdo sem periféricos.

Depois de definir os [Modelos de fragmentos de conteúdo](#creating-a-content-model), você pode usá-los para [criar fragmentos de conteúdo](#creating-a-content-fragment).

O [Editor de fragmentos de conteúdo](#opening-the-fragment-editor) fornece vários [modos](#modes-in-the-content-fragment-editor) para permitir:

* [Editar o conteúdo](#editing-the-content-of-your-fragment) e [gerenciar as variações](#creating-and-managing-variations-within-your-fragment)
* [Anotar em seu fragmento](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Associar conteúdo ao fragmento](#associating-content-with-your-fragment)
* [Configurar os metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Visualizar a árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar a representação JSON](/help/assets/content-fragments/content-fragments-json-preview.md)


>[!NOTE]
>
>Os fragmentos de conteúdo podem ser usados:
>
>* ao criar páginas; consulte [Criação de páginas com fragmentos de conteúdo](/help/sites-authoring/content-fragments.md).
>* para [entrega de conteúdo headless usando fragmentos de conteúdo com GraphQL](/help/assets/content-fragments/content-fragments-graphql.md).


>[!NOTE]
>
>Fragmentos de conteúdo são armazenados como **Ativos**, portanto, são gerenciadas principalmente na variável **Ativos** console.

## Criação de fragmentos de conteúdo {#creating-content-fragments}

### Criação de um modelo de conteúdo {#creating-a-content-model}

Os [modelos de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) podem ser ativados e criados antes da criação de fragmentos de conteúdo com conteúdo estruturado.

### Criação de um fragmento de conteúdo {#creating-a-content-fragment}

O método de criação de um fragmento de conteúdo é:

1. Navegue até a pasta **Ativos** na qual deseja criar o fragmento.
1. Selecione **Criar** e **Fragmento de conteúdo** para abrir o assistente.
1. A primeira etapa do assistente requer que você especifique a base do novo fragmento.

   * [Modelo](/help/assets/content-fragments/content-fragments-models.md) - usado para criar um fragmento que requer conteúdo estruturado; por exemplo, a variável **Aventura** modelo

      * Todos os modelos disponíveis são exibidos.

   Após a seleção, use **Próximo** para continuar.

   ![base do fragmento](assets/cfm-managing-01.png)

1. Na etapa **Propriedades**, especifique:

   * **Básico**

      * **Título**

         O título do fragmento.

         Obrigatório.

      * **Descrição**

      * **Tags**
   * **Avançado**

      * **Nome**

         O nome; será usada para formar o URL.

         Obrigatório; serão derivadas automaticamente do título, mas podem ser atualizadas.


1. Selecione **Criar** para concluir a ação e, em seguida, **Abra** o fragmento para editar ou retorne ao console com **Concluído**.

   >[!NOTE]
   >Em **Lista** do console, você pode atualizar o **Exibir configurações** para ativar o **Modelo de fragmento de conteúdo** coluna.

## Ações para um fragmento de conteúdo no console Ativos {#actions-for-a-content-fragment-assets-console}

No **Ativos** no console, uma variedade de ações está disponível para seus fragmentos de conteúdo:

* Na barra de ferramentas; após a seleção do fragmento, todas as ações apropriadas estarão disponíveis.
* As [ações rápidas](/help/sites-authoring/basic-handling.md#quick-actions); um subconjunto de ações disponível para os cartões de fragmento individuais.

![ações](assets/cfm-managing-02.png)

Selecione o fragmento para exibir a barra de ferramentas com as ações aplicáveis:

* **Download**

   * Salve o fragmento como um arquivo ZIP; você pode definir se deseja incluir Elementos, Variações, Metadados.

* **Criar**
* **Check-out**
* **Propriedades**

   * Permite exibir e/ou editar os metadados do fragmento.

* **Editar**

   * Permite que você [abrir o fragmento para edição de conteúdo](/help/assets/content-fragments/content-fragments-variations.md) juntamente com seus elementos, variações, conteúdo associado e metadados.

* **Gerenciar tags**
* **Para a coleção**
* **Copiar** e **Colar**)
* **Mover**
* **Publicação rápida**
* **Gerenciar publicação**
* **Excluir**

>[!NOTE]
>
>Muitos deles são [ações padrão do Assets](/help/assets/manage-assets.md) e/ou a [AEM aplicativo de desktop](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=pt-BR).

## Abrir o editor de fragmentos {#opening-the-fragment-editor}

Para abrir o fragmento para edição:

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Entre em contato com o administrador do sistema em caso de problemas.

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa das permissões apropriadas. Entre em contato com o administrador do sistema em caso de problemas.

1. Use o **Ativos** para navegar até o local do fragmento de conteúdo.
1. Abra o fragmento para edição, por:

   * Clicar/tocar no link do fragmento ou fragmento (depende da exibição do console).
   * Selecionar o fragmento e **Editar** na barra de ferramentas.

1. O editor de fragmentos será aberto. Faça as alterações necessárias:

   ![editor de fragmento](assets/cfm-managing-03.png)

1. Depois de fazer as alterações, clique em **Salvar**, **Salvar e fechar** ou **Fechar**, conforme necessário.

   >[!NOTE]
   >
   >**Salvar e fechar** está disponível por meio da lista suspensa **Salvar**.

   >[!NOTE]
   >
   >Tanto a opção **Salvar e fechar** quanto **Fechar** fecharão o editor — consulte [Salvar, fechar e versões](#save-close-and-versions) para obter informações completas sobre como as várias opções operam para os fragmentos de conteúdo.

## Modos e ações no Editor de fragmento de conteúdo {#modes-actions-content-fragment-editor}

Há vários modos e ações disponíveis no Editor de fragmento de conteúdo.

### Modos no Editor de fragmento de conteúdo {#modes-in-the-content-fragment-editor}

Navegue pelos vários modos usando os ícones no painel lateral:

* Variações: [Edição de conteúdo](#editing-the-content-of-your-fragment) e [Gerenciamento de variações](#creating-and-managing-variations-within-your-fragment)

* [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
* [Conteúdo associado](#associating-content-with-your-fragment)
* [Metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)
* [Árvore de estrutura](/help/assets/content-fragments/content-fragments-structure-tree.md)
* [Visualizar](/help/assets/content-fragments/content-fragments-json-preview.md)

![modos](assets/cfm-managing-04.png)

### Ações da barra de ferramentas no Editor de fragmento de conteúdo {#toolbar-actions-in-the-content-fragment-editor}

Alguns recursos na barra de ferramentas superior estão disponíveis em vários modos:

![modos](assets/cfm-managing-top-toolbar.png)

* Uma mensagem será exibida quando o fragmento já tiver sido referenciado em uma página de conteúdo. Você pode **Fechar** a mensagem.

* O painel lateral pode ser oculto/exibido usando o ícone **Ativar painel lateral**.

* Abaixo do nome do fragmento, você pode ver o nome do [Modelo de fragmento de conteúdo](/help/assets/content-fragments/content-fragments-models.md) usado para criar o fragmento atual:

   * O nome também é um link que abrirá o editor de modelo.

* Veja o status do fragmento; por exemplo, informações sobre quando ele foi criado, modificado ou publicado.

* **Salvar** fornece acesso à opção **Salvar e fechar**.

* O menu suspenso de três pontos (**...**) fornece acesso a ações adicionais:
   * **Atualizar referências de página**
      * Isso atualiza todas as referências de página.
   * **[Publicação rápida](#publishing-and-referencing-a-fragment)**
   * **[Gerenciar publicação](#publishing-and-referencing-a-fragment)**

<!--
* See the status of the fragment; for example, information about when it was created, modified or published. The status is also color-coded:

  * **New**: grey
  * **Draft**: blue
  * **Published**: green
  * **Modified**: orange
  * **Deactivated**: red
-->

<!--
This updates any page references and ensures that the Dispatcher is flushed as required. 
-->

## Salvar, fechar e versões {#save-close-and-versions}

>[!NOTE]
>
>As versões também podem ser [criadas, comparadas e revertidas a partir da linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

O editor tem várias opções:

* **Salvar** e **Salvar e fechar**

   * **Salvar** salva as alterações mais recentes e permanece no editor.
   * **Salvar e fechar** salva as alterações mais recentes e fecha o editor.

   >[!CAUTION]
   >
   >Para editar um fragmento de conteúdo, você precisa [das permissões apropriadas](/help/sites-developing/customizing-content-fragments.md#asset-permissions). Entre em contato com o administrador do sistema em caso de problemas.

   >[!NOTE]
   >
   >É possível permanecer no editor e fazer uma série de alterações antes de salvar.

   >[!CAUTION]
   >
   >Além de simplesmente salvar suas alterações, as ações também atualizam quaisquer referências e garantem que o Dispatcher seja liberado conforme necessário. Essas alterações podem levar tempo para serem processadas. Devido a isso, pode haver um impacto no desempenho de um sistema grande/complexo/com bastante conteúdo.
   >
   >Lembre-se disso ao usar a opção **Salvar e fechar** e, logo em seguida, entrar novamente no editor de fragmentos para fazer mais alterações e salvá-las.

* **Fechar**

   Fechará o editor sem salvar as alterações mais recentes (ou seja, feitas desde o último **Salvamento**).

Ao editar o fragmento de conteúdo, o AEM cria versões automaticamente para garantir que o conteúdo anterior possa ser restaurado se você cancelar as alterações (usando **Fechar** sem salvar):

1. Quando um fragmento de conteúdo é aberto para edição, o AEM verifica a existência do token baseado em cookie que indica se uma *sessão de edição* existe:

   1. Se o token for encontrado, o fragmento será considerado parte da sessão de edição existente.
   2. Se o token *não* estiver disponível e o usuário iniciar a edição do conteúdo, uma versão será criada e um token para essa nova sessão de edição será enviado ao cliente e salvo em um cookie.

2. Enquanto houver uma seção de edição *ativa*, o conteúdo que está sendo editado será salvo automaticamente a cada 600 segundos (padrão).

   >[!NOTE]
   >
   >O intervalo de salvamento automático pode ser configurado usando o mecanismo `/conf`.
   >
   >Valor padrão, consulte:
   >  `/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se o usuário cancelar a edição, a versão criada no início da sessão de edição será restaurada e o token será removido para encerrar a sessão de edição.
4. Se o usuário escolher **Salvar** as edições, os elementos/variações atualizados serão mantidos e o token será removido para encerrar a sessão de edição.

## Edição do conteúdo do fragmento {#editing-the-content-of-your-fragment}

Após abrir o fragmento, é possível usar a guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) para criar o conteúdo.

## Criação e gerenciamento de variações dentro do fragmento {#creating-and-managing-variations-within-your-fragment}

Depois de criar o conteúdo Principal, é possível criar e gerenciar [Variações](/help/assets/content-fragments/content-fragments-variations.md) desse conteúdo.

## Associar conteúdo ao fragmento {#associating-content-with-your-fragment}

Você também pode [associar conteúdo](/help/assets/content-fragments/content-fragments-assoc-content.md) a um fragmento. Isso fornece uma conexão para que os ativos (por exemplo, imagens) possam ser usados (opcionalmente) com o fragmento quando ele é adicionado a uma página de conteúdo.

## Visualização e edição dos metadados (propriedades) do fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

É possível visualizar e editar as propriedades de um fragmento usando a guia [Metadados](/help/assets/content-fragments/content-fragments-metadata.md).

## Linha de tempo dos fragmentos de conteúdo {#timeline-for-content-fragments}

Além das opções padrão, a [Linha de tempo](/help/assets/manage-assets.md#timeline) fornece informações e ações específicas para fragmentos de conteúdo:

* Visualizar informações sobre versões, comentários e anotações
* Ações para versões

   * **[Reverter para esta versão](#reverting-to-a-version)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **[Comparar com atual](#comparing-fragment-versions)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * Adicionar um **Rótulo** e/ou **Comentário** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **Salvar como versão** (selecione um fragmento existente e, em seguida, a seta para cima na parte inferior da Linha de tempo)

* Ações para anotações

   * **Excluir**

>[!NOTE]
Os comentários são:
* Uma funcionalidade padrão para todos os ativos
* Feitos na Linha de tempo
* Relacionados ao ativo de fragmento
>
As anotações (para fragmentos de conteúdo) são:
* Inseridas no editor de fragmentos
* Específicas de um segmento de texto selecionado no fragmento
>


Por exemplo:

![linha de tempo](assets/cfm-managing-05.png)

## Comparação de versões do fragmento {#comparing-fragment-versions}

A ação **Comparar com atual** fica disponível na [Linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) após selecionar uma versão específica.

Isso abrirá:

* a versão (à esquerda) **Atual** (mais recente)

* a versão selecionada **v&lt;*x.y*>** (à direita)

Elas serão mostradas lado a lado, onde:

* Quaisquer diferenças serão destacadas

   * Texto excluído — vermelho
   * Texto inserido — verde
   * Texto substituído — azul

* O ícone de tela cheia permite abrir uma versão por conta própria e, em seguida, voltar para a visualização paralela
* É possível **Reverter** para a versão específica
* **Concluído** retornará ao console

>[!NOTE]
Não é possível editar o conteúdo do fragmento ao comparar fragmentos.

![comparação](assets/cfm-managing-06.png)

## Reverter para uma versão  {#reverting-to-a-version}

Você pode reverter para uma versão específica do fragmento:

* Diretamente da [Linha de tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Selecione a versão necessária e, em seguida, a ação **Reverter para esta versão**.

* Ao [comparar uma versão com a versão atual](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions), é possível **Reverter** para a versão selecionada.

## Publicar e referenciar um fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
Se o fragmento for baseado em um modelo, é preciso certificar-se de que o [modelo foi publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
Se você publicar um fragmento de conteúdo cujo modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado junto com o fragmento.

Os fragmentos de conteúdo devem ser publicados para uso no ambiente de publicação. Eles podem ser publicados:

* Após a criação; usar [ações disponíveis no console Ativos](#actions-for-a-content-fragment-assets-console).
* No [Editor de fragmento de conteúdo](#toolbar-actions-in-the-content-fragment-editor).
* Quando você [publicar uma página que use o fragmento](/help/sites-authoring/content-fragments.md#publishing); o fragmento será listado nas referências da página.

>[!CAUTION]
Depois que um fragmento tiver sido publicado e/ou referenciado, o AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Excluir um fragmento {#deleting-a-fragment}

Para excluir um fragmento:

1. No console de **Ativos**, navegue até o local do fragmento de conteúdo.
2. Selecione o fragmento.

   >[!NOTE]
   A opção **Excluir** não está disponível como uma ação rápida.

3. Selecione **Excluir** na barra de ferramentas.
4. Confirme a ação **Excluir**.

   >[!CAUTION]
   Se o fragmento já estiver referenciado em uma página, você verá uma mensagem de aviso e será solicitado a confirmar se deseja continuar com uma **Exclusão forçada**. O fragmento, junto com seu componente do fragmento de conteúdo, será excluído de qualquer página de conteúdo.
