---
title: Gerenciamento dos fragmentos de conteúdo
seo-title: Gerenciamento dos fragmentos de conteúdo
description: Os Fragmentos de conteúdo são armazenados como Ativos, portanto, são gerenciados principalmente no console Ativos.
seo-description: Os Fragmentos de conteúdo são armazenados como Ativos, portanto, são gerenciados principalmente no console Ativos.
uuid: 675e1a6b-2583-488f-bbb4-210daed3e1b0
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: content-fragments
content-type: reference
discoiquuid: 21a18d60-f3fe-4048-9949-8416b5cb4596
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 11%

---


# Gerenciamento dos fragmentos de conteúdo{#managing-content-fragments}

Os Fragmentos de conteúdo são armazenados como **Ativos**, portanto, são gerenciados principalmente no console **Ativos** .

>[!NOTE]
>
>Fragmentos de conteúdo são usados com páginas de criação; consulte Criação [de página com fragmentos](/help/sites-authoring/content-fragments.md)de conteúdo.

## Criação de fragmentos de conteúdo {#creating-content-fragments}

### Criação de um modelo de conteúdo {#creating-a-content-model}

[Os modelos](/help/assets/content-fragments/content-fragments-models.md) de fragmento de conteúdo podem ser ativados e criados antes da criação de fragmentos de conteúdo com conteúdo estruturado.

>[!NOTE]
>
>Consulte [Desenvolvimento de fragmentos](/help/sites-developing/customizing-content-fragments.md) de conteúdo para obter mais informações sobre modelos; usado para fragmentos de conteúdo simples.

### Criação de um fragmento de conteúdo {#creating-a-content-fragment}

O método de criação de um fragmento de conteúdo é (basicamente) o mesmo para fragmentos simples e estruturados:

1. Navegue até a pasta **Ativos** na qual deseja criar o fragmento.
1. Selecione **Criar** e **Fragmento de conteúdo** para abrir o assistente.
1. A primeira etapa do assistente requer que você especifique a base do novo fragmento.

   * Isso pode ser:

      * [Modelo](/help/sites-developing/content-fragment-templates.md) - por exemplo, Fragmento **simples**

      * [Modelo](/help/assets/content-fragments/content-fragments-models.md) - usado para criar um fragmento que requer conteúdo estruturado; por exemplo, o modelo de **aeroporto**
   * Todos os modelos e modelos disponíveis são exibidos.

   Após a seleção, use **Próximo** para continuar.

   ![cfm-6420-15](assets/cfm-6420-15.png)

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

         Obrigatório; serão derivadas automaticamente do título, mas poderão ser atualizadas.


1. Selecione **Criar** para concluir a ação e, em seguida, **Abra** o fragmento para editar ou retorne ao console com **Concluído**.

## Ações para um fragmento de conteúdo {#actions-for-a-content-fragment}

No console **Ativos** , várias ações estão disponíveis para seus fragmentos de conteúdo:

* Na barra de ferramentas; após a seleção do fragmento, todas as ações apropriadas estarão disponíveis.
* Como ações [rápidas](/help/sites-authoring/basic-handling.md#quick-actions); um subconjunto de ações disponível para os cartões de fragmento individuais.

![cfm-6420-17](assets/cfm-6420-17.png)

Selecione o fragmento para revelar a barra de ferramentas com as ações aplicáveis:

* **Download**

   * Salve o fragmento como um arquivo ZIP; você pode definir se deseja incluir Elementos, Variações, Metadados.

* **Criar**
* **Check-out**
* **Propriedades**

   * Permite que você visualização e/ou edite os metadados do fragmento.

* **Editar**

   * Permite [abrir o fragmento para edição de conteúdo](/help/assets/content-fragments/content-fragments-variations.md) junto com seus elementos, variações, conteúdo associado e metadados.

* **Gerenciar tags**
* **Para a coleção**

   * Adicione o fragmento a uma coleção.
   * Isso também pode ser feito ao [associar uma coleção ao fragmento](/help/assets/content-fragments/content-fragments-assoc-content.md#adding-associated-content).

* **Copiar**/**colar**

* **Mover**
* **Publicação rápida**
* **Gerenciar publicação**
* **Excluir**

>[!NOTE]
>
>Muitas dessas ações são [padrão para os Ativos](/help/assets/manage-assets.md) e/ou o aplicativo [para desktop](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html)AEM.

## Abrir o Editor de fragmentos {#opening-the-fragment-editor}

Para abrir o fragmento para edição:

>[!CAUTION]
>
>Para editar um fragmento de conteúdo, você precisa [das permissões](/help/sites-developing/customizing-content-fragments.md#asset-permissions)apropriadas. Entre em contato com o administrador do sistema se tiver problemas.

1. Use o console **Ativos** para navegar até o local do fragmento do conteúdo.
1. Abra o fragmento para edição ao:

   * Clicar/tocar no fragmento ou link do fragmento (isso depende da visualização do console).
   * Selecionando o fragmento, em seguida, **Editar** na barra de ferramentas.

   O editor de fragmentos abrirá:

   ![cfm-6420-18](assets/cfm-6420-18.png)

   >[!NOTE]
   >
   >1. Uma mensagem será exibida quando o fragmento já estiver referenciado em uma página de conteúdo.
   >2. O painel lateral pode ser oculto/exibido usando o ícone **Alternar painel** lateral.


1. Navegue pelos três modos usando os ícones no painel lateral:

   * Variações: [Editar o conteúdo](#editing-the-content-of-your-fragment) e [gerenciar suas variações](#creating-and-managing-variations-within-your-fragment)

   * [Anotações](/help/assets/content-fragments/content-fragments-variations.md#annotating-a-content-fragment)
   * [Conteúdo associado](#associating-content-with-your-fragment)
   * [Metadados](#viewing-and-editing-the-metadata-properties-of-your-fragment)

   ![cfm-10](assets/cfm-10.png)

1. Depois de fazer as alterações, use **Salvar** ou **Cancelar** , conforme necessário.

   >[!NOTE]
   >
   >Tanto **Salvar** quanto **Cancelar** sairão do editor - consulte [Salvar, cancelar e versões](#save-cancel-and-versions) para obter informações completas sobre como ambas as opções operam para fragmentos de conteúdo.

## Salvar, Cancelar e Versões {#save-cancel-and-versions}

>[!NOTE]
>
>As versões também podem ser [criadas, comparadas e revertidas na Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

O editor tem duas opções:

* **Salvar**

   Salva as alterações mais recentes e saia do editor.

   >[!CAUTION]
   >
   >Para editar um fragmento de conteúdo, você precisa [das permissões](/help/sites-developing/customizing-content-fragments.md#asset-permissions)apropriadas. Entre em contato com o administrador do sistema se tiver problemas.

   >[!NOTE]
   >
   >É possível permanecer no editor, fazendo uma série de alterações, antes de selecionar **Salvar**.

   >[!CAUTION]
   >
   >Além de salvar suas alterações, o **Save** também atualiza quaisquer referências e garante que o dispatcher seja liberado conforme necessário. Essas mudanças podem levar tempo para serem processadas. Devido a isso, pode haver um impacto no desempenho em um sistema grande/complexo/com carga intensa.
   >
   >
   >Lembre-se disso ao usar **Salvar** e, em seguida, reinserir rapidamente o editor de fragmentos para fazer e salvar outras alterações.

* **Cancelar**

   Sairá do editor sem salvar as alterações mais recentes.

Ao editar o fragmento do conteúdo, AEM cria automaticamente versões para garantir que o conteúdo anterior possa ser restaurado se você **Cancelar** suas alterações:

1. Quando um fragmento de conteúdo é aberto para edição AEM verifica a existência do token baseado em cookie que indica se existe uma sessão *de* edição:

   1. Se o token for encontrado, o fragmento será considerado parte da sessão de edição existente.
   2. Se o token *não* estiver disponível e o usuário start a edição de conteúdo, uma versão é criada e um token para esta nova sessão de edição é enviado para o cliente, onde é salvo em um cookie.

2. Enquanto há uma sessão de edição *ativa* , o conteúdo que está sendo editado é salvo automaticamente a cada 600 segundos (padrão).

   >[!NOTE]
   >
   >O intervalo de salvamento automático é configurável usando o `/conf` mecanismo.
   >
   >
   >Valor padrão, consulte:
   >
   >
   >`/libs/settings/dam/cfm/jcr:content/autoSaveInterval`

3. Se o usuário selecionar **Cancelar** a edição, a versão criada no start da sessão de edição será restaurada e o token será removido para encerrar a sessão de edição.
4. Se o usuário selecionar para **Salvar** as edições, os elementos/variações atualizados serão mantidos e o token será removido para encerrar a sessão de edição.

## Editar o conteúdo do fragmento {#editing-the-content-of-your-fragment}

Após abrir o fragmento, use a guia [Variações](/help/assets/content-fragments/content-fragments-variations.md) para criar o conteúdo.

## Criação e gerenciamento de variações no fragmento {#creating-and-managing-variations-within-your-fragment}

Depois de criar o conteúdo Principal, você pode criar e gerenciar [variações](/help/assets/content-fragments/content-fragments-variations.md) desse conteúdo.

## Associar conteúdo ao fragmento {#associating-content-with-your-fragment}

Também é possível [associar conteúdo](/help/assets/content-fragments/content-fragments-assoc-content.md) a um fragmento. Isso fornece uma conexão para que os ativos (ou seja, imagens) possam ser usados (opcionalmente) com o fragmento quando ele for adicionado a uma página de conteúdo.

## Visualização e edição dos metadados (propriedades) do fragmento {#viewing-and-editing-the-metadata-properties-of-your-fragment}

É possível visualização e editar as propriedades de um fragmento usando a guia [Metadados](/help/assets/content-fragments/content-fragments-metadata.md) .

## Linha do tempo para fragmentos de conteúdo {#timeline-for-content-fragments}

Além das opções padrão, a [Linha do tempo](/help/assets/manage-assets.md#timeline) fornece informações e ações específicas para fragmentos de conteúdo:

* Informações de visualização sobre versões, comentários e anotações
* Ações para versões

   * **[Reverter para esta versão](#reverting-to-a-version)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **[Comparar com Atual](#comparing-fragment-versions)** (selecione um fragmento existente e, em seguida, uma versão específica)

   * Adicionar um **Rótulo** e/ou **Comentário** (selecione um fragmento existente e, em seguida, uma versão específica)

   * **Salvar como versão** (selecione um fragmento existente e, em seguida, a seta para cima na parte inferior da Linha do tempo)

* Ações para anotações

   * **Excluir**

>[!NOTE]
>
>Os comentários são:
>
>* Funcionalidade padrão para todos os ativos
>* Feito na Linha do tempo
>* Relacionado ao ativo de fragmento

>
>
As anotações (para Fragmentos de conteúdo) são:
>
>* Inserido no editor de fragmentos
>* Específico para um segmento selecionado de texto dentro do fragmento

>



Por exemplo:

![cfm-6420-19-2019](assets/cfm-6420-19-2019.png)

## Comparação de versões de fragmento {#comparing-fragment-versions}

A ação **Comparar com o atual** está disponível na [Linha](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments) do tempo depois que você seleciona uma versão específica.

Isso abrirá:

* a versão **Atual** (mais recente) (à esquerda)

* a versão selecionada **v&lt;*x.y*>** (direita)

Elas serão mostradas lado a lado, onde:

* Quaisquer diferenças são destacadas

   * Texto excluído - vermelho
   * Texto inserido - verde
   * Texto substituído - azul

* O ícone de tela cheia permite que você abra qualquer versão por conta própria; em seguida, alterne de volta para a visualização paralela
* Você pode **Reverter** para a versão específica
* **Concluído** retornará ao console

>[!NOTE]
>
>Não é possível editar o conteúdo do fragmento ao comparar fragmentos.

![cfm-6420-20](assets/cfm-6420-20.png)

## Reverting to a Version  {#reverting-to-a-version}

É possível reverter para uma versão específica do fragmento:

* Diretamente da [Linha do tempo](/help/assets/content-fragments/content-fragments-managing.md#timeline-for-content-fragments).

   Selecione a versão necessária e, em seguida, a ação **Reverter para esta versão** .

* Ao [comparar uma versão com a versão](/help/assets/content-fragments/content-fragments-managing.md#comparing-fragment-versions) atual, é possível **Reverter** para a versão selecionada.

## Publicação e referência de um fragmento {#publishing-and-referencing-a-fragment}

>[!CAUTION]
>
>Se o fragmento for baseado em um modelo, verifique se o [modelo foi publicado](/help/assets/content-fragments/content-fragments-models.md#publishing-a-content-fragment-model).
>
>Se você publicar um fragmento de conteúdo para o qual o modelo ainda não foi publicado, uma lista de seleção indicará isso e o modelo será publicado com o fragmento.

Fragmentos de conteúdo devem ser publicados para uso no ambiente de publicação. Podem ser publicados:

* Após a criação; no console **Ativos** .
* Ao [publicar uma página que usa o fragmento](/help/sites-authoring/content-fragments.md#publishing); o fragmento será listado nas referências de página.

>[!CAUTION]
>
>Depois que um fragmento é publicado e/ou referenciado, AEM exibirá um aviso quando um autor abrir o fragmento para edição novamente. Isso serve para avisar que as alterações no fragmento também afetarão as páginas referenciadas.

## Excluir um fragmento {#deleting-a-fragment}

Para excluir um fragmento:

1. No console **Ativos** , navegue até o local do fragmento de conteúdo.
2. Selecione o fragmento.

   >[!NOTE]
   >
   >The **Delete** action is not available as a quick action.

3. Select **Delete** from the toolbar.
4. Confirme a ação **Excluir** .

   >[!CAUTION]
   >
   >Se o fragmento já estiver referenciado em uma página, você verá uma mensagem de aviso e será solicitado a confirmar se deseja continuar com uma **Exclusão forçada**. O fragmento, junto com seu componente do fragmento de conteúdo, será excluído de qualquer página de conteúdo.

