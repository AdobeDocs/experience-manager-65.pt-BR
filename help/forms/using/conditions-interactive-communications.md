---
title: Condições em comunicações interativas
seo-title: Condições em comunicações interativas
description: Criação e edição de fragmentos de condição a serem usados no Interative Communications - condição é um dos quatro tipos de fragmentos de documento usados para criar o Interative Communications. Os outros três são textos, listas e fragmentos de layout.
seo-description: Condições de criação e edição a serem usadas no Interative Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Condições em comunicações interativas{#conditions-in-interactive-communications}

Criação e edição de fragmentos de condição a serem usados no Interative Communications - condição é um dos quatro tipos de fragmentos de documento usados para criar o Interative Communications. Os outros três são textos, listas e fragmentos de layout.

## Visão geral {#overview}

Condição é um fragmento de documento que pode ser incluído em uma Comunicação interativa. Os outros fragmentos de documento são fragmentos de [texto](../../forms/using/texts-interactive-communications.md), lista e layout. As condições permitem definir um ou mais ativos contextuais que são incluídos em uma Comunicação interativa com base nos dados e regras fornecidos.

Exemplos:

* Em um extrato de cartão de crédito, exibir a taxa anual do cartão de crédito e a imagem do cartão de crédito com base no tipo de cartão de crédito do cliente.
* Em um lembrete de vencimento de prêmio de seguro, exibe cálculos de imposto com base nos impostos do estado do cliente.

Os ativos nas condições que são renderizados com base nas regras aplicadas e nos valores passados para a regra. As regras nas condições podem verificar valores nos seguintes tipos de dados:

* Propriedade do modelo de dados de formulário associado
* Quaisquer variáveis que você criar na condição
* Strings
* Números
* expressões matemáticas
* Datas

## Create condition {#createcondition}

1. Selecione **[!UICONTROL Formulários]** > Fragmentos **[!UICONTROL de]** Documento.
1. Selecione **[!UICONTROL Criar]** > **[!UICONTROL Condição]**.
1. Especifique as seguintes informações:

   * **[!UICONTROL Título]**: (Opcional) Insira o título da condição. Os títulos não precisam ser exclusivos e podem ter caracteres especiais e caracteres não ingleses. As condições são referenciadas por seus títulos (quando disponíveis), como em miniaturas e propriedades.
   * **[!UICONTROL Nome]**: O nome exclusivo da condição, em uma pasta. Não podem existir dois fragmentos de documento (texto, condição ou lista) em qualquer estado com o mesmo nome dentro de uma pasta. No campo Nome, é possível digitar somente caracteres, números e hífens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título. Os caracteres especiais, os espaços, os números e os caracteres que não estão em inglês inseridos no campo Título são substituídos por hífens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, é possível editar o valor.

   * **[!UICONTROL Descrição]**: Digite uma descrição do fragmento do documento.
   * **[!UICONTROL Modelo]** de dados de formulário: Como opção, selecione o botão de opção Modelo de dados de formulário para criar a condição com base em um modelo de dados de formulário. Quando o botão de opção Modelo de dados de formulário é selecionado, o campo Modelo **[!UICONTROL de dados de]** formulário é exibido. Procure e selecione um modelo de dados de formulário. Ao criar a condição para uma Comunicação interativa, certifique-se de usar o mesmo modelo de dados que pretende usar na Comunicação interativa. Para obter mais informações sobre o modelo de dados de formulário, consulte Integração [de](../../forms/using/data-integration.md)dados.

   * **[!UICONTROL Tags]**: Como opção, para criar uma tag personalizada, insira o valor no campo de texto e toque em Enter. Quando você salva essa condição, as tags recém-adicionadas são criadas.

1. Toque em **[!UICONTROL Avançar]**.

   A página Criar condição é exibida.

   ![createcondition](assets/createcondition.png)

1. Toque em **[!UICONTROL Adicionar ativos]**.

   A página Selecionar ativos é exibida e exibe os textos, listas, condições e imagens disponíveis para adição na condição.

   >[!NOTE]
   >
   >Somente ativos baseados em nenhum e recém-criados e ativos baseados em FDM (criados usando o mesmo FDM que a condição que está sendo criada) aparecem na página Selecionar ativos.

1. Toque nos ativos apropriados para selecioná-los para incluí-los na condição e, em seguida, toque em **[!UICONTROL Concluído]**.

   A página Criar condição é exibida e lista os ativos adicionados.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Você pode usar as seguintes opções para gerenciar ativos em uma condição:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[Uma]Alteração Rejeitada.**Toque nesse ícone para rejeitar as alterações que você pode ter feito no ativo e na regra na condição.   **[B]Aceitar Alteração.**Toque neste ícone para aceitar as alterações feitas no ativo e na regra na condição.   **[C]Ativo do Duplicado.**Toque nesse ícone para criar uma cópia do ativo junto com a regra aplicada, se houver, na condição. Em seguida, você pode continuar editando a regra e o ativo para o ativo duplicado. A duplicação de um ativo é útil para criar regras semelhantes para exibir ativos alternativos com base em um contexto específico.   **[D]Mostrar Pré-visualização.**Toque nesse ícone para exibir uma pré-visualização do ativo na página Criar\Editar condição.   **Reordenar &#39;server&#39;.** Toque e mantenha pressionado este ícone para arrastar e soltar ativos para reorganizá-los em uma condição.

   Você pode selecionar as seguintes opções para especificar como a condição se comporta no tempo de execução:

   * **Avaliação de múltiplos resultados desativada\Avaliação de vários resultados ativada**: Quando essa opção está ativada (aparece como &quot;Avaliação de múltiplos resultados ativada&quot;), todas as regras são avaliadas e o resultado é a soma de todas as regras verdadeiras. Se essa opção estiver desativada (aparece como &quot;Avaliação de resultados múltiplos desativada&quot;), somente a primeira regra que for encontrada como verdadeira será avaliada e se tornará a saída da condição.

   * **Quebra** de página: Selecione essa opção ( ![quebra](assets/break.png)) para adicionar uma quebra de página entre os ativos das condições. Quando essa opção não está selecionada ( ![nobreak](assets/nobreak.png)), se uma condição estiver transbordando para a próxima página na saída de impressão, toda a condição será deslocada para a próxima página em vez de quebrar a página entre os ativos na condição.

1. Toque em **[!UICONTROL Criar regra]** para adicionar regras para exibir ou ocultar os ativos, conforme necessário. Para usar variáveis nas regras, consulte [criação de variáveis](#variables). Para obter mais informações, consulte [Adicionar regras à condição](#ruleeditor).

   As regras criadas aparecem na coluna REGRA na tela Criar condição.

   ![createconditionscreenrulesadd](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Você pode inserir ativos em sua condição que já tenham regras ou repetições aplicadas.

1. Toque em **[!UICONTROL Salvar]**.

   A condição é criada. Agora, você pode continuar usando a condição como um bloco de construção ao criar uma Comunicação interativa.

   >[!NOTE]
   >
   >Para salvar uma condição nova ou editada, é necessário ter pelo menos uma regra para cada um dos ativos adicionados à condição.

## Editar uma condição {#edit-a-condition}

É possível editar uma condição usando as seguintes etapas. Você também pode optar por editar uma condição em uma Comunicação interativa selecionando Editar fragmento no menu pop-up.

1. Selecione **[!UICONTROL Formulários]** > Fragmentos **[!UICONTROL de]** Documento.
1. Navegue até a condição e selecione-a.
1. Toque em **[!UICONTROL Editar]**.
1. Faça as alterações necessárias na condição. Para obter mais detalhes sobre as informações que podem ser alteradas em uma condição, consulte [Criar condição](#createcondition).
1. Toque em **[!UICONTROL Salvar]** e, em seguida, toque em **[!UICONTROL Fechar]**.

## Criar regras em condição {#ruleeditor}

Usando o editor de regras em uma condição, é possível criar regras para exibir ou ocultar ativos com base em condições **** predefinidas. Essas condições podem ser construídas com base em:

* Strings
* Números
* expressões matemáticas
* Datas
* Propriedades do modelo de dados de formulário associado
* Quaisquer [variáveis](#variables) que você possa ter criado

### Criar regra em condição {#create-rule-in-condition}

1. Ao criar ou editar uma condição, toque no ícone ![ruleeditoricon](assets/ruleeditoricon.png) (Editor de regras) para o ativo relevante.

   A caixa de diálogo Criar regra é exibida. Além da string, do número, da expressão matemática e da data, os seguintes itens também estão disponíveis no Editor de regras para a criação de declarações das regras:

   * Propriedades do modelo de dados de formulário associado
   * Quaisquer [variáveis](#variables) que você tenha criado.
   ![createruledialog](assets/createruledialog.png)

   Selecione a opção apropriada a ser avaliada.

   >[!NOTE]
   >
   >A propriedade Collection não é compatível com a criação de regras para exibir ativos.

1. Selecione o operador apropriado para avaliar a regra, como É igual a, Contém e Start com.
1. Insira a expressão de avaliação, a string, a propriedade do modelo de dados, a variável ou a data.

   ![Regra para mostrar um ativo quando o tipo de política é padrão](assets/ruleincondition.png)

   Regra para mostrar um ativo quando o tipo de política é padrão

   * Ao criar ou editar uma regra, você também pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra/Editar regra. A caixa de diálogo expandida de janela cheia permite criar [variáveis](#variables) para construir regras. Toque em Redimensionar novamente para voltar à caixa de diálogo Criar regra.

   * Você também pode criar várias condições em uma regra.

1. Toque em **[!UICONTROL Concluído]**.

   A regra é aplicada ao ativo.

## Criação e uso de variáveis em uma condição {#variables}

Ao criar ou editar uma regra em uma condição, você pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra\Editar regra. A caixa de diálogo expandida e em janela cheia permite:

* Criar e usar variáveis na regra
* Arrastar e soltar as propriedades e variáveis do modelo de dados de formulário na regra

Toque em Redimensionar novamente para voltar à caixa de diálogo Criar regra\Editar regra.

### Criar variáveis {#create-variables}

1. Ao criar ou editar uma regra em uma condição, você pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra\Editar regra.

   A caixa de diálogo Expandido e em janela cheia é exibida.

   ![expandededitruledialog](assets/expandededitruledialog.png)

1. No painel esquerdo, toque em **[!UICONTROL Variáveis]**.

   O painel Variáveis é exibido.

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. Toque em **[!UICONTROL Criar]**.

   O painel Criar variáveis é exibido.

1. Digite as seguintes informações e toque em **[!UICONTROL Criar]**:

   * **[!UICONTROL Nome]**: Nome da variável.
   * **[!UICONTROL Descrição]**: Opcionalmente, insira uma descrição sobre a variável.
   * **[!UICONTROL Tipo]**: Selecione um tipo de variável: String, Number, Boolean ou Date.
   * **[!UICONTROL Permitir somente]** valores específicos: Para variáveis String e Number, é possível garantir que o agente escolha a partir de um conjunto específico de valores para um espaço reservado na interface do agente. Para especificar o conjunto de valores, selecione essa opção e especifique valores separados por vírgulas que são permitidos no campo **[!UICONTROL Valores]** .

1. Toque em **[!UICONTROL Criar]**.

   A variável é criada e listada no painel Variáveis.

1. Para inserir uma variável na regra, arraste e solte a variável em um espaço reservado para uma opção na regra.
1. Depois de criar uma regra válida, toque em **[!UICONTROL Concluído]**.

   Passe para fazer outras alterações, se necessário, na condição e salvá-la.

