---
title: Condições em comunicações interativas
seo-title: Conditions in Interactive Communications
description: Criação e edição de fragmentos de condição a serem usados em Comunicações interativas - a condição é um dos quatro tipos de fragmentos de documento usados para criar Comunicações interativas. Os outros três são textos, listas e fragmentos de layout.
seo-description: Creating and editing conditions to be used in Interactive Communications
uuid: c98f02d5-1769-46dd-ab35-6e8145a24939
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fe59d260-d392-4d6f-bb7e-2f2a1d701f51
docset: aem65
feature: Interactive Communication
exl-id: 0c0dc6a2-b889-4516-8e08-1e9d31be2cce
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 0%

---

# Condições em comunicações interativas{#conditions-in-interactive-communications}

Criação e edição de fragmentos de condição a serem usados em Comunicações interativas - a condição é um dos quatro tipos de fragmentos de documento usados para criar Comunicações interativas. Os outros três são textos, listas e fragmentos de layout.

## Visão geral {#overview}

Condição é um fragmento de documento que pode ser incluído em uma Comunicação interativa. Os outros fragmentos do documento são [texto](../../forms/using/texts-interactive-communications.md), lista e fragmento de layout. As condições permitem definir um ou mais ativos contextuais que são incluídos em uma Comunicação interativa com base nos dados e regras fornecidos.

Exemplos:

* Em um demonstrativo de cartão de crédito, exiba a taxa anual do cartão de crédito e a imagem do cartão de crédito com base no tipo de cartão de crédito do cliente.
* Em um lembrete de prêmio de seguro devido, exiba cálculos de imposto com base nos impostos estaduais do cliente.

Os ativos nas condições que são renderizados com base nas regras aplicadas e os valores passados para a regra. As regras nas condições podem verificar valores nos seguintes tipos de dados:

* Propriedade do modelo de dados de formulário associado
* Quaisquer variáveis criadas na condição
* Cadeias de caracteres
* Números
* Expressões matemáticas
* Datas

## Criar condição {#createcondition}

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.
1. Selecionar **[!UICONTROL Criar]** > **[!UICONTROL Condição]**.
1. Especifique as seguintes informações:

   * **[!UICONTROL Título]**: (Opcional) Insira o título da condição. Os títulos não precisam ser exclusivos e podem ter caracteres especiais e caracteres que não estejam em inglês. As condições são mencionadas por seus títulos (quando disponíveis), como em miniaturas e propriedades.
   * **[!UICONTROL Nome]**: o nome exclusivo da condição, em uma pasta. Não podem existir dois fragmentos de documento (texto, condição ou lista) em nenhum estado com o mesmo nome em uma pasta. No campo Nome, você pode inserir apenas caracteres, números e hifens do idioma inglês. O campo Nome é preenchido automaticamente com base no campo Título. Os caracteres especiais, espaços, números e caracteres que não estão em inglês inseridos no campo Título são substituídos por hifens no campo Nome. Embora o valor no campo Título seja copiado automaticamente para o Nome, você pode editar o valor.

   * **[!UICONTROL Descrição]**: digite uma descrição do fragmento do documento.
   * **[!UICONTROL Modelo de dados do formulário]**: como opção, selecione o botão de opção Modelo de dados de formulário para criar a condição com base em um modelo de dados de formulário. Ao selecionar o botão de opção Modelo de dados de formulário, **[!UICONTROL Modelo de dados do formulário]** é exibido. Procure e selecione um modelo de dados de formulário. Ao criar uma condição para uma Comunicação interativa, certifique-se de usar o mesmo modelo de dados que pretende usar na Comunicação interativa. Para obter mais informações sobre o modelo de dados de formulário, consulte [Integração de dados](../../forms/using/data-integration.md).

   * **[!UICONTROL Tags]**: Opcionalmente, para criar uma tag personalizada, insira o valor no campo de texto e toque em Inserir. Ao salvar essa condição, as tags recém-adicionadas são criadas.

1. Toque **[!UICONTROL Próxima]**.

   Criar Condição é exibida.

   ![createcondition](assets/createcondition.png)

1. Toque **[!UICONTROL Adicionar ativos]**.

   A página Selecionar ativos é exibida e exibe os textos, as listas, as condições e as imagens disponíveis para adição na condição.

   >[!NOTE]
   >
   >Somente ativos baseados em nenhum, recém-criados e ativos baseados em FDM (criados usando o mesmo FDM da condição que está sendo criada) são exibidos na página Selecionar ativos.

1. Toque nos ativos apropriados para selecioná-los para inclusão na condição e toque em **[!UICONTROL Concluído]**.

   Criar condição é exibida e lista os ativos adicionados.

   ![createconditionassetsadd](assets/createconditionassetsadd.png)

   Você pode usar as seguintes opções para gerenciar ativos em uma condição:

   ![createconditionscreenassetsaddedannotated](assets/createconditionscreenassetsaddedannotated.png)

   **[A] Rejeitar alteração.** Toque nesse ícone para rejeitar as alterações que você pode ter feito no ativo e na regra na condição.
   **[B] Aceite a alteração.** Toque nesse ícone para aceitar as alterações feitas no ativo e na regra na condição.
   **[C] Ativo duplicado.** Toque nesse ícone para criar uma cópia do ativo junto com a regra aplicada, se houver, na condição. Em seguida, você pode continuar editando a regra e o ativo para o ativo duplicado. Duplicar um ativo é útil para criar regras semelhantes para exibir ativos alternativos com base em um contexto específico.
   **[D] Mostrar visualização.** Toque nesse ícone para exibir uma visualização do ativo na página Criar\Editar condição.
   **Reordenação de &#39;servidor&#39;.** Toque e segure esse ícone para arrastar e soltar ativos e reorganizá-los em uma condição.

   Você pode selecionar as seguintes opções para especificar como a condição se comporta no tempo de execução:

   * **Múltiplos resultados da avaliação desativado\Múltiplos resultados da avaliação ativado**: quando essa opção está ativada (aparece como &quot;Avaliação de vários resultados ativada&quot;), todas as regras são avaliadas e o resultado é a soma de todas as regras verdadeiras. Se essa opção estiver desativada (exibida como &quot;Avaliação de vários resultados desativada&quot;), somente a primeira regra que for considerada verdadeira será avaliada e se tornará a saída da condição.

   * **Quebra de página**: selecione esta opção ( ![interrupção](assets/break.png)) para adicionar uma quebra de página entre os ativos das condições. Quando esta opção não está selecionada ( ![nobreak](assets/nobreak.png)), se uma condição estiver transbordando para a próxima página na saída de impressão, a condição inteira será deslocada para a próxima página em vez de quebrar na página entre os ativos na condição.

1. Toque **[!UICONTROL Criar regra]** para adicionar regras para exibir ou ocultar os ativos, conforme necessário. Para usar variáveis nas regras, consulte [criação de variáveis](#variables). Para obter mais informações, consulte [Adicionar regras à condição](#ruleeditor).

   As regras criadas são exibidas na coluna REGRA na tela Criar condição.

   ![createconditionscreenrulesaded](assets/createconditionscreenrulesadded.png)

   >[!NOTE]
   >
   >Você pode inserir ativos na sua condição que já têm regras ou repetição aplicadas.

1. Toque **[!UICONTROL Salvar]**.

   A condição é criada. Agora é possível continuar usando a condição como um bloco de construção ao criar uma Comunicação interativa.

   >[!NOTE]
   >
   >Para salvar uma condição nova ou editada, você deve ter pelo menos uma regra para cada um dos ativos adicionados na condição.

## Editar uma condição {#edit-a-condition}

Você pode editar uma condição usando as etapas a seguir. Você também pode optar por editar uma condição em uma Comunicação interativa selecionando Editar fragmento no menu pop-up.

1. Selecionar **[!UICONTROL Forms]** > **[!UICONTROL Fragmentos do documento]**.
1. Navegue até a condição e selecione-a.
1. Toque **[!UICONTROL Editar]**.
1. Faça as alterações necessárias na condição. Para obter mais detalhes sobre as informações que você pode alterar em uma condição, consulte [Criar condição](#createcondition).
1. Toque **[!UICONTROL Salvar]** e toque em **[!UICONTROL Fechar]**.

## Criar regras na condição {#ruleeditor}

Ao usar o editor de regras em uma condição, é possível criar regras para exibir ou ocultar ativos com base em **condições predefinidas**. Essas condições podem ser construídas com base em:

* Cadeias de caracteres
* Números
* Expressões matemáticas
* Datas
* Propriedades do modelo de dados de formulário associado
* Qualquer [variáveis](#variables) que você pode ter criado

### Criar regra na condição {#create-rule-in-condition}

1. Ao criar ou editar uma condição, toque em ![ruleeditoricon](assets/ruleeditoricon.png) (Editor de regras) ícone do ativo relevante.

   A caixa de diálogo Criar regra é exibida. Além de sequência, número, expressão matemática e data, os itens a seguir também estão disponíveis no Editor de regras para criar instruções das regras:

   * Propriedades do modelo de dados de formulário associado
   * Qualquer [variáveis](#variables) que você pode ter criado.

   ![createruledialog](assets/createruledialog.png)

   Selecione a opção apropriada a ser avaliada.

   >[!NOTE]
   >
   >A propriedade de coleção não tem suporte para criar regras para exibir ativos.

1. Selecione o operador apropriado para avaliar a regra, como É igual a, Contém e Começa com.
1. Insira a expressão de avaliação, string, propriedade do modelo de dados, variável ou data.

   ![Regra para mostrar um ativo quando o tipo de política é padrão](assets/ruleincondition.png)

   Regra para mostrar um ativo quando o tipo de política é padrão

   * Ao criar ou editar uma regra, você também pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra/Editar regra. A caixa de diálogo expandida em janela inteira permite criar [variáveis](#variables) para criar regras. Toque em Redimensionar novamente para voltar à caixa de diálogo Criar regra.

   * Você também pode criar várias condições em uma regra.

1. Toque **[!UICONTROL Concluído]**.

   A regra é aplicada ao ativo.

## Criação e uso de variáveis em uma condição {#variables}

Ao criar ou editar uma regra em uma condição, você pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra\Editar regra. A caixa de diálogo expandida em janela cheia permite:

* Criar e usar variáveis na regra
* Arraste e solte propriedades e variáveis do modelo de dados de formulário na regra

Toque novamente em Redimensionar para voltar à caixa de diálogo Criar regra\Editar regra.

### Criar variáveis {#create-variables}

1. Ao criar ou editar uma regra em uma condição, você pode tocar em ![icon_resize](assets/icon_resize.png) (Redimensionar) para expandir a caixa de diálogo Criar regra\Editar regra.

   A caixa de diálogo Expandido, janela inteira é exibida.

   ![expandeditruledialog](assets/expandededitruledialog.png)

1. No painel esquerdo, toque em **[!UICONTROL Variáveis]**.

   O painel Variáveis é exibido.

   ![expandeditrulevariables](assets/expandededitrulevariables.png)

1. Toque **[!UICONTROL Criar]**.

   Criar variáveis é exibido.

1. Insira as seguintes informações e toque em **[!UICONTROL Criar]**:

   * **[!UICONTROL Nome]**: Nome da variável.
   * **[!UICONTROL Descrição]**: Opcionalmente, insira uma descrição sobre a variável.
   * **[!UICONTROL Tipo]**: selecione um tipo da variável: String, Number, Boolean ou Date.
   * **[!UICONTROL Permitir Somente Valores Específicos]**: para variáveis de string e número, você pode garantir que o agente escolha entre um conjunto específico de valores para um espaço reservado na interface do usuário do agente. Para especificar o conjunto de valores, selecione essa opção e especifique valores separados por vírgula que sejam permitidos na **[!UICONTROL Valores]** campo.

1. Toque **[!UICONTROL Criar]**.

   A variável é criada e listada no painel Variáveis.

1. Para inserir uma variável na regra, arraste e solte a variável em um espaço reservado para obter uma opção na regra.
1. Depois de criar uma regra válida, toque em **[!UICONTROL Concluído]**.

   Continue fazendo mais alterações, se necessário, na condição e salvando-a.
