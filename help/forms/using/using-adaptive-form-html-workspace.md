---
title: Uso de um formulário adaptável na área de trabalho HTML
seo-title: Uso de um formulário adaptável na área de trabalho HTML
description: Uso de um formulário adaptável na área de trabalho HTML
seo-description: Uso de um formulário adaptável na área de trabalho HTML
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
translation-type: tm+mt
source-git-commit: 8e724af4d69cb859537dd088119aaca652ea3931
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# Uso de um formulário adaptável na área de trabalho HTML{#using-an-adaptive-form-in-html-workspace}

O AEM Forms em JEE fornece a capacidade de usar um formulário adaptável na área de trabalho HTML.

Como é possível selecionar um XDP durante o design do Processo, a capacidade de navegar de um formulário adaptável existente AEM repositório foi adicionada. O recurso oferece ao designer de Processo a capacidade de configurar um formulário adaptável no Ponto de partida e na Tarefa.

## Experiência de design de processo {#process-design-experience}

Execute o seguinte procedimento para habilitar formulários adaptáveis a serem usados no design de processo:

* Em Atribuir ponto de Tarefa e Start, é possível navegar até um ativo de formulário adaptável no repositório CRX ao atribuir um ativo de formulário a uma tarefa.
* Na folha de propriedades Atribuir Tarefa/Ponto de Start do Workbench, é possível ocultar a barra de ferramentas de nível superior/global de um formulário adaptável.
* Você pode usar novos perfis de ação para renderizar e enviar ações em formulários adaptáveis.

### Exportação e importação de aplicativos de LiveCycle {#livecycle-application-export-and-import}

Como os formulários adaptáveis estão no repositório AEM, a exportação do aplicativo LiveCycle contém apenas as referências para formulários adaptáveis usados. Por conseguinte, a exportação e importação de aplicativos LiveCycle é um processo em duas etapas. O aplicativo LiveCycle inclui definições de processo e assim por diante. Um pacote separado contendo formulários adaptáveis é exportado como um arquivo ZIP da AEM. Durante a importação, o aplicativo LiveCycle é importado por meio do Workbench e os formulários adaptáveis são importados por meio do AEM.

## Experiência do usuário em formulários adaptáveis no espaço de trabalho HTML {#user-experience-of-adaptive-form-in-html-workspace}

O HTML Workspace fornece alguns controles adaptáveis específicos ao formulário, além de controles que estão disponíveis para formulários móveis. Um usuário pode adicionar anexos, salvar, assinar, enviar e navegar pelos formulários adaptáveis no Espaço de trabalho HTML quando o usuário abrir uma Tarefa ou um Ponto de Start. Veja a seguir as especificações:

1. Para anexar arquivos, use anexos de Tarefa, como aconteceu no Mobile Forms. Qualquer botão do tipo Anexo de arquivo do formulário adaptável está oculto.

1. Para salvar um formulário adaptável, clique em **Salvar**, como acontecia no Mobile Forms. Qualquer botão Salvar tipo de formulário adaptativo está oculto.

1. Para enviar um formulário adaptável, use o botão **Enviar** ou as ações de rota disponíveis, como era o caso no Mobile Forms. Qualquer botão de tipo Enviar do formulário adaptável está oculto.

1. **Visibilidade** da barra de ferramentas global do formulário adaptável: Se o designer de processos ocultar a barra de ferramentas global/de nível superior, a barra de ferramentas e os botões não aparecerão nos formulários adaptáveis.

1. **Controles de navegação da área de trabalho para Forms** adaptável: Os botões Próximo/Anterior estão disponíveis junto com os botões Salvar, Enviar e Ação de Rota para um formulário adaptável na área de trabalho HTML. Clique nos botões Próximo/Anterior para navegar pelos painéis de formulários adaptáveis na área de trabalho HTML. Os botões Próximo/Anterior fornecem navegação profunda, semelhante aos controles de navegação na visualização Móvel dos formulários adaptáveis.

1. **Serviços de eSign e Componente de resumo do formulário** adaptável: O componente Resumo não está operacional no espaço de trabalho HTML. Em outras palavras, se um formulário adaptável tiver um componente Resumo, ele não estará visível no espaço de trabalho. Em vez de Enviar automaticamente no componente Assinar, o usuário da área de trabalho clica na ação Enviar ou em uma rota na área de trabalho HTML. Depois que um documento é assinado, ele fica visível como um documento assinado plano. Clique em **Enviar** ou em uma ação de rota para fechar/concluir a tarefa ou o Ponto de Start.\
   O documento assinado é coletado do servidor de serviços eSign e o arquivo xml de dados é encaminhado para a próxima etapa do processo.

## Etapas para usar formulários adaptáveis no design de processo {#steps-to-use-adaptive-forms-in-process-design}

1. Abra o Adobe Experience Manager Forms Workbench.

1. Vá para **Arquivo > Novo > Aplicativo** ou use o aplicativo existente para criar um aplicativo.

   ![Criar novo aplicativo](assets/create_new_appl.png)

   Criar novo aplicativo

1. Crie um processo ou use um processo existente no aplicativo.

   ![Criar novo processo](assets/create_new_process.png)

   Criar novo processo

1. Crie um ponto de Start ou atribua Tarefa e clique duplo nele.
1. Na seção **[!UICONTROL Apresentação e dados]**, selecione **[!UICONTROL usar um ativo CRX]** e clique nas elipses antes do ativo.

   ![Usar um ativo CRX](assets/use_crx_asset.png)

   Usar um ativo CRX

1. Selecione o formulário adaptável criado por meio da interface do usuário Gerenciar ativos e clique em **[!UICONTROL OK]**.

   ![Selecione um formulário adaptável](assets/selecting_form.png)

   Selecione um formulário adaptável

   >[!NOTE]
   >
   >Para obter detalhes sobre como criar um formulário adaptável, consulte [Criar um formulário adaptável](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Para obter detalhes sobre como criar um processo, consulte [Criar e gerenciar processos](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).

