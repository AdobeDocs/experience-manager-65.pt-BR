---
title: Use o modo Layout para redimensionar componentes para formulários adaptáveis
description: Definir a posição dos componentes usando a grade responsiva disponível no modo Layout
feature: Adaptive Forms,Foundation Components
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 1%

---

# Usar o modo Layout para redimensionar componentes {#use-layout-mode-to-resize-components}

O <span class="preview"> Adobe recomenda o uso de [Componentes principais](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=pt-BR) de captura de dados moderna e extensível para [criar um novo Forms Adaptável](/help/forms/using/create-an-adaptive-form-core-components.md) ou [adicionar o Forms Adaptável às páginas do AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Esses componentes representam um avanço significativo na criação do Forms adaptável, garantindo experiências de usuário impressionantes. Este artigo descreve a abordagem mais antiga para criar o Forms adaptável usando componentes de base. </span>

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/resize-using-layout-mode.html?) |
| AEM 6.5 | Este artigo |


A interface de criação do formulário adaptável permite redimensionar componentes usando o modo Layout. Arraste e solte pontos azuis dentro de colunas para definir os pontos inicial e final para posicionar componentes. Os pontos azuis são exibidos depois de tocar no componente na grade responsiva. A grade responsiva consiste em 12 colunas iguais. O sombreamento das cores branco e azul em colunas alternadas diferencia uma coluna da outra.

Você pode usar o modo Layout para redimensionar componentes para todos os tipos de dispositivos, como desktop, tablet, telefone e outros dispositivos menores. O tablet deriva automaticamente a configuração de layout da versão do desktop e os dispositivos menores derivam a configuração de layout do telefone. No entanto, você pode substituir as configurações derivadas automaticamente para definir uma configuração diferente para cada tipo de dispositivo.

## Modo de layout de acesso {#access-layout-mode}

Selecione **Layout** na lista suspensa que aparece na parte superior da interface de criação do formulário adaptável ao lado da opção **Visualizar**. O formulário é exibido no modo Layout.

1. Faça logon na instância de autor do AEM e navegue até **Adobe Experience Manager** > **Forms** > **Forms e Documentos**.
1. Crie um [formulário adaptável](../../forms/using/creating-adaptive-form.md) ou abra um existente.
1. Selecione **Layout** na lista suspensa que aparece na parte superior ao lado da opção **Visualizar**. O formulário é exibido no modo Layout.

   ![Modo de layout](assets/layout_mode_ic_new.png)

## Redimensionar componentes {#resize-components}

1. No modo Layout, selecione o componente a ser redimensionado. Os pontos azuis são exibidos no início e no fim da grade responsiva.
1. Arraste e solte os pontos azuis para definir a posição do componente na grade responsiva.

   ![Redimensionando usando o modo Layout](assets/layout_mode_resize_new_updated1.png)

   A barra de ferramentas exibida ao tocar em componentes consiste nas seguintes opções:

   * **[!UICONTROL Pai]**: selecione o pai de um componente.
   * **[!UICONTROL Reverter layout do ponto de interrupção]**: desfaz todas as alterações de redimensionamento e aplica o layout padrão ao componente.
   * **[!UICONTROL Flutuar para a nova linha]**: desloque o componente para a próxima linha se houver vários componentes dentro da mesma linha.

   Você também pode usar a opção **[!UICONTROL Reverter layout do ponto de interrupção]** ( ![Reverter ponto de interrupção](assets/reverttopreviouslypublishedversion.png)) no nível do painel para desfazer todas as alterações de redimensionamento.

   >[!NOTE]
   >
   >Não é possível redimensionar componentes de coluna de tabela, barra de ferramentas, botão da barra de ferramentas e área de destino usando o modo Layout. Use o modo Estilo para redimensionar esses componentes.

### Exemplo {#example}

**Objetivo:** você deseja inserir um componente de tabela e um componente de imagem e posicioná-los paralelamente uns aos outros em um formulário adaptável.

1. Insira os componentes de tabela e imagem usando o modo Editar no formulário adaptável. O componente de imagem é exibido após o componente de tabela.
1. Alterne para o modo Layout e selecione o componente Tabela. Os pontos azuis para redimensionar a exibição do componente nas colunas 1 e 12.
1. Arraste e solte o ponto azul na coluna 12 para a coluna 6 da grade responsiva.

   ![Definir o ponto final da tabela](assets/layout_mode_end_point_table_new.png)

1. Da mesma forma, selecione o componente de Imagem e arraste e solte o ponto azul na coluna 1 para a coluna 7 da grade responsiva. Os componentes de tabela e imagem são exibidos paralelamente um ao outro.

   ![Tabela e imagem em paralelo no modo Layout](assets/table_image_parallel_new.png)

   Você pode selecionar o componente de Imagem e selecionar a opção **Flutuar para a nova linha**, disponível na barra de ferramentas, para deslocar o componente de Imagem para a próxima linha.

## Redimensionar painéis {#resize-panels-layout-mode}

Execute as seguintes etapas se desejar redimensionar o painel inteiro em vez de componentes individuais:

1. Selecione qualquer um dos componentes no painel que você deseja redimensionar, selecione ![Selecionar pai](assets/select_parent_icon.svg) e selecione a primeira opção na lista suspensa, se o painel for o pai imediato do componente.

   Os pontos azuis são exibidos no início e no fim da grade responsiva.

1. Arraste e solte os pontos azuis para definir a posição do painel na grade responsiva.
Você pode repetir as etapas 1 e 2 e selecionar ![Selecionar pai](assets/float_to_new_line_icon.svg) para deslocar o painel redimensionado para a próxima linha.

## Definir layout de várias colunas para um painel

Execute as seguintes etapas para definir o número de colunas para um painel:

1. No modo **[!UICONTROL Editar]**, selecione o painel, selecione ![Configurar](assets/configure_icon.png) e selecione a opção **[!UICONTROL Responsivo - tudo na página sem navegação]** da lista suspensa **[!UICONTROL Layout do Painel]**.

1. Selecione ![Salvar](assets/save_icon.svg) para salvar as propriedades.

1. No modo **[!UICONTROL Layout]**, selecione qualquer um dos componentes no painel, selecione ![Selecionar pai](assets/select_parent_icon.svg) e selecione o painel.

1. Selecione ![multi-column](assets/multi-column.svg) e selecione o número de colunas na lista suspensa. O número de colunas pode variar de 1 a 12. O painel é dividido em um layout de várias colunas.

![várias colunas no modo de layout](assets/multi-column-layout.png)

## Ativar a nova grade responsiva para layouts responsivos antigos {#enableresponsivegrid}

Ative a nova grade responsiva para formulários criados com o AEM Forms 6.4 ou versão inferior para redimensionar componentes.

>[!NOTE]
>
>Alternar para a nova grade responsiva descarta as propriedades de layout já definidas para componentes usados no formulário.

Execute as seguintes etapas para ativar a nova grade responsiva:

1. Selecione **Layout** na lista suspensa que aparece na parte superior ao lado da opção **Visualizar**. Uma confirmação para ativar o modo Layout é exibida.
1. Selecione **Sim** para habilitar o modo **Layout** para o formulário.

### Incorpore um fragmento antigo em um formulário adaptável com o novo layout responsivo {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

O novo layout responsivo para formulário adaptável permite adicionar um fragmento de formulário adaptável com o layout responsivo antigo ao formulário. No entanto, o novo layout descarta as propriedades de layout já definidas para os componentes usados no fragmento. Você pode alternar para o modo Layout para definir as propriedades de layout dos componentes usados no fragmento.

### Incorporar um fragmento com o novo layout responsivo em um formulário adaptável antigo {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Se você incorporar um fragmento com o novo layout responsivo em um formulário adaptável com um layout responsivo antigo, o sistema solicitará que você ative o modo Layout para o formulário e incorpore novamente o fragmento.

Para habilitar o modo de Layout, selecione **Layout** na lista suspensa que aparece na parte superior ao lado da opção **Visualizar** e selecione **Sim** para confirmar. Selecione o modo **Editar** para reincorporar o fragmento.

## Desativar o modo Layout para formulários com layout responsivo antigo {#disable-layout-mode-for-forms-with-old-responsive-layout}

Você pode desativar o modo Layout para formulários com layout responsivo antigo editando propriedades para o modelo usado no formulário.

Execute as seguintes etapas para desativar o modo Layout:

1. Selecione **[!UICONTROL Ferramentas]** > **[!UICONTROL Geral]** > **[!UICONTROL Modelos]** e abra o modelo usado no formulário no modo **[!UICONTROL Editar]**.
1. Selecione o Contêiner de documentos no painel esquerdo e selecione **[!UICONTROL Política.]**

   ![Desabilitar modo de layout](assets/policy_disable_layout_mode.png)

1. Selecione a guia **[!UICONTROL Configurações de Layout]** e selecione **[!UICONTROL Desabilitar Modo de Layout]**.
1. Selecione ![Salvar alterações](assets/save_icon.png) para salvar as propriedades do modelo.
