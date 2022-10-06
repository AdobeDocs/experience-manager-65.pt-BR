---
title: Uso de um formulário adaptável no HTML Workspace
seo-title: Using an adaptive form in HTML Workspace
description: Uso de um formulário adaptável no HTML Workspace
seo-description: Using an adaptive form in HTML Workspace
uuid: 473d5daf-a3ed-449f-9136-585755b59922
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 2b6875cd-2ee7-4aa8-90c7-d33583dc2f0e
docset: aem65
exl-id: 15b9ae98-059f-4bf7-bfdd-9cfeb8eb30a4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Uso de um formulário adaptável no HTML Workspace{#using-an-adaptive-form-in-html-workspace}

O AEM Forms no JEE fornece a capacidade de usar um formulário adaptável no HTML Workspace.

Como é possível selecionar um XDP durante o design do processo, a capacidade de navegar de um formulário adaptável existente AEM repositório foi adicionada. O recurso fornece ao designer de processos a capacidade de configurar um formulário adaptável no Ponto de partida e na Tarefa.

## Experiência de design de processo {#process-design-experience}

Execute o seguinte procedimento para habilitar formulários adaptáveis a serem usados no design do processo:

* Em Atribuir tarefa e ponto de início, é possível navegar até um ativo de formulário adaptável no repositório CRX ao atribuir um ativo de formulário a uma tarefa.
* Na folha de propriedades Atribuir Tarefa/Ponto de Início da Bancada, é possível ocultar a barra de ferramentas de nível superior/global de um formulário adaptável.
* Você pode usar novos perfis de Ação para processar e enviar ações em formulários adaptáveis.

### Exportação e importação de aplicativos LiveCycle {#livecycle-application-export-and-import}

Como os formulários adaptáveis estão no repositório AEM, a exportação do aplicativo LiveCycle contém apenas as referências para os formulários adaptáveis usados. Portanto, a exportação e a importação de aplicativos LiveCycle é um processo em duas etapas. O aplicativo LiveCycle inclui definições de processo e assim por diante. Um pacote separado contendo formulários adaptáveis é exportado como um arquivo ZIP do AEM. Ao importar, o aplicativo LiveCycle é importado por meio do Workbench e os formulários adaptáveis são importados por meio do AEM.

## Experiência do usuário de formulário adaptável no HTML Workspace {#user-experience-of-adaptive-form-in-html-workspace}

O HTML Workspace fornece alguns controles adaptáveis específicos do formulário, além dos controles que estão disponíveis para formulários móveis. Um usuário pode adicionar anexos, salvar, assinar, enviar e navegar pelos formulários adaptáveis no HTML Workspace quando o usuário abre uma Tarefa ou um Ponto de Início. Estas são as especificações:

1. Para anexar arquivos, use anexos de Tarefa, como era o caso no Mobile Forms. Qualquer botão do tipo File Attachment do formulário adaptável está oculto.

1. Para salvar um formulário adaptável, clique em **Salvar**, como foi o caso no Mobile Forms. Qualquer botão de tipo Salvar do formulário adaptável está oculto.

1. Para enviar um formulário adaptável, use o **Enviar** ações de botão ou rota disponíveis, como era o caso no Mobile Forms. Qualquer botão de tipo Enviar do formulário adaptável está oculto.

1. **Visibilidade da barra de ferramentas global do formulário adaptável**: Se o designer de processos ocultar a barra de ferramentas global/de nível superior, a barra de ferramentas e os botões não aparecerão em formulários adaptáveis.

1. **Controles de navegação do Workspace para Adaptive Forms**: Os botões Next/Previous estão disponíveis junto com os botões Save, Submit e Route Action para um formulário adaptável no HTML Workspace. Clique nos botões Avançar/Anterior para navegar pelos painéis de formulários adaptáveis no HTML Workspace. Os botões Próximo/Anterior fornecem navegação profunda, de modo semelhante aos controles de navegação na visualização Móvel dos formulários adaptáveis.

1. **Serviços de eSign e Componente de resumo do formulário adaptável**: O componente Resumo não é operacional no HTML Workspace. Em outras palavras, se um formulário adaptável tiver um componente de Resumo, ele não estará visível no espaço de trabalho. Em vez de Enviar automaticamente no componente Assinar , o usuário do espaço de trabalho clica na ação Enviar ou em uma rota no HTML Workspace. Depois que um documento é assinado, ele é visível como um documento assinado simples. Clique em **Enviar** ou uma ação de rota para fechar/concluir a tarefa ou o Ponto de Início.\
   O documento assinado é coletado do servidor de serviços de assinatura eletrônica e o arquivo xml de dados é encaminhado para a próxima etapa do processo.

## Etapas para usar formulários adaptáveis no design do processo {#steps-to-use-adaptive-forms-in-process-design}

1. Abra o Adobe Experience Manager Forms Workbench.

1. Ir para **Arquivo > Novo > Aplicativo** ou use o aplicativo existente para criar um aplicativo.

   ![Criar novo aplicativo](assets/create_new_appl.png)

   Criar novo aplicativo

1. Crie um processo ou use um processo existente no aplicativo.

   ![Criar novo processo](assets/create_new_process.png)

   Criar novo processo

1. Crie um Ponto de Início ou Atribua Tarefa e clique duas vezes nele.
1. Em **[!UICONTROL Apresentação e dados]** seção , selecione **[!UICONTROL usar um ativo CRX]** e clique nas reticências antes do ativo.

   ![Usar um ativo CRX](assets/use_crx_asset.png)

   Usar um ativo CRX

1. Selecione o formulário adaptável criado por meio da interface do usuário Gerenciar ativos e clique em **[!UICONTROL OK]**.

   ![Selecione um formulário adaptável](assets/selecting_form.png)

   Selecione um formulário adaptável

   >[!NOTE]
   >
   >Para obter detalhes sobre como criar um formulário adaptável, consulte [Criação de um formulário adaptável](../../forms/using/creating-adaptive-form.md).
   >
   >
   >Para obter detalhes sobre como criar um processo, consulte [Criação e gerenciamento de processos](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/WS92d06802c76abadb-1cc35bda128261a20dd-7ff7.2.html).
