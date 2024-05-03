---
title: Ações e recursos de fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE
description: Ações e recursos de fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 20%

---

# Ações e recursos de fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Caixa de entrada do AEM e espaço de trabalho do HTML {#aem-inbox-and-html-workspace}

Você pode usar a Caixa de entrada do AEM para executar e monitorar fluxos de trabalho do AEM centrados no Forms no OSGi. Por outro lado, o HTML Workspace permite executar e monitorar os fluxos de trabalho do AEM Forms JEE. A tabela a seguir ajuda você a entender várias ações importantes disponíveis na Caixa de entrada do AEM para fluxos de trabalho do AEM centrados no Forms no OSGi e no HTML Workspace para fluxos de trabalho do AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Ações</td>
   <td>Caixa de entrada AEM</td>
   <td>Espaço de trabalho do HTML</td>
  </tr>
  <tr>
   <td>Iniciando um processo, tarefa ou aplicativo de formulário<br /> </td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Envio de tarefas</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Atribuir uma tarefa a um grupo</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Enviando para vários roteiros</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Rastreamento do histórico e do resumo das tarefas</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Notificações por email</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Reatribuindo tarefas</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Anexos de nível de campo para formulários adaptáveis</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Exibição de calendário</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Comentários no nível da tarefa</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Filas (fila pessoal compartilhada, tarefas de reclamação da fila)</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Notificação de ausência temporária</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
    <tr>
   <td>Personalização de elementos da interface</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Atribuir uma tarefa a vários usuários</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

## Fluxos de trabalho do AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Os fluxos de trabalho do AEM centrados em formulários no OSGi e os fluxos de trabalho do AEM Forms JEE (AEM Forms no Gerenciamento de processos do JEE) têm um conjunto diferente de recursos. A tabela a seguir ajuda você a entender recursos importantes disponíveis em Workflows do AEM centrados em formulários no OSGi e no AEM Forms em Workflows do JEE:

<table>
 <tbody>
  <tr>
   <td>Recursos</td>
   <td>Workflows do AEM centrados em formulários no OSGi<br /> </td>
   <td>Fluxos de trabalho do AEM Forms JEE</td>
  </tr>
  <tr>
   <td>Adaptive Forms</td>
   <td>Compatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Integração com outras soluções de AEM</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Rabiscar a assinatura</td>
   <td>Compatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Modelos de email personalizados</td>
   <td>Compatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Definindo a prioridade da tarefa</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Tempo limite de uma tarefa após a data de vencimento</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Loops no fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Escolher dinamicamente um destinatário </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Uso de metadados personalizados</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Assinatura eletrônica (Adobe Sign)</td>
   <td>Compatível <sup>[1]</sup></td>
   <td>Compatível <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gerenciar aplicativos de formulários e tarefas</td>
   <td>Compatível <sup>[2]</sup><br /> </td>
   <td>Compatível <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Serviços de documento</td>
   <td>Compatível <sup>[3]</sup></td>
   <td>Compatível <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Renderizar tarefa concluída como formulário adaptável ou documento PDF</td>
   <td>Compatível</td>
   <td>Suportado [4]</td>
  </tr>
  <tr>
   <td>Integração com o Gerenciamento de correspondência</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
   <tr>
   <td>Gateways, SEM ESPERA </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
   <tr>
   <td>Variáveis para armazenar dados </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>OU E dividir</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Avatar do usuário</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Enviar um email ao final do fluxo de trabalho</td>
   <td>Compatível <sup>[7]</sup></td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Chamar um serviço Web a partir de um fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Assinatura digital</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Estágios do fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Formulários adaptáveis somente leitura</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Ocultando o botão de salvamento padrão</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Controle granular da seção de detalhes do fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Serviço de pesquisa/agendamento</td>
   <td>Disponível imediatamente</td>
   <td>É necessária uma implementação personalizada</td>
  </tr>
  <tr>
   <td>Aplicativo Forms adaptável</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço de Assembler</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço PDF Generator</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço do Forms</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço de saída</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Document Assurance</td>
   <td>Compatível</td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Executar script</td>
   <td>Compatível com ECMAScript</td>
   <td>Suporta trechos de código Java</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, PDF forms interativos, Conjunto de formulários</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Relatório de processo</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Assinatura digital</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Categorias de ponto inicial</td>
   <td>Incompatível </td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Aprovação de tarefas em massa </td>
   <td>Incompatível </td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Salvar rascunho com um nome personalizado</td>
   <td>Incompatível </td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Iniciar um processo com dados de processo existentes<br /> </td>
   <td>Incompatível</td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Salvar um ponto de partida como rascunho</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Visualização do gerente</td>
   <td>Incompatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Pesquisar modelos</td>
   <td>Incompatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Integração com aplicativos de terceiros</td>
   <td>Não suportado <sup>[6]</sup></td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Anexos de nível de tarefa para aplicativo de fluxo de trabalho ou ponto inicial</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Email de lembrete</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Alterar título no tempo limite da tarefa</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Enviar email sobre delegação de tarefas e declaração de tarefa</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Delegar entre grupos separados</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Transformação XSLT</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Prioridade de tarefa dinâmica</td>
   <td>Incompatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Título dinâmico</td>
   <td>Incompatível</td>
   <td>Incompatível</td>
  </tr>
    <tr>
   <td>Descrição dinâmica</td>
   <td>Incompatível</td>
   <td>Incompatível</td>
  </tr>
 </tbody>
</table>

1. Você pode usar Workflows do AEM centrados em formulários no OSGi para assinar um formulário adaptável preenchido. Fluxos de trabalho do AEM centrados em formulários no OSGi são compatíveis com a assinatura fora do formulário. A variável [assinatura no formulário](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) experiência não é suportada.

1. Você precisa de acesso à Caixa de entrada do AEM para executar e monitorar fluxos de trabalho centrados em formulários no AEM Forms OSGi e no HTML Workspace para executar e monitorar fluxos de trabalho do AEM Forms JEE.
1. Os serviços de documento nativos da AEM Forms estão disponíveis para fluxos de trabalho AEM centrados em formulário no OSGi e para fluxos de trabalho AEM Forms no JEE. O fluxo de trabalho do AEM usa serviços de documento nativos para fluxos de trabalho do AEM centrados no formulário em fluxos de trabalho OSGi e AEM Forms JEE (Process Management).
1. Os fluxos de trabalho do AEM Forms JEE só podem renderizar um formulário adaptável. Não há suporte para a renderização de um formulário adaptável como um documento PDF.
1. Os fluxos de trabalho do AEM forms JEE não têm uma etapa separada para o Adobe Sign. Você precisa de um formulário adaptável habilitado para o Adobe Sign para AEM formulários JEE Workflows. Para obter mais detalhes, consulte [Documentação do Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Você pode usar o [Invocar serviço de modelo de dados de formulário](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) etapa para chamar um serviço da web e publicar ou recuperar dados de um aplicativo de terceiros.
1. Você pode usar o [Enviar e-mail](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) etapa para enviar emails.

## Diferenças entre a Caixa de entrada do AEM e os recursos do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado no Forms são usar [Caixa de entrada AEM](../../forms/using/manage-applications-inbox.md) e AEM Forms. No entanto, os recursos da Caixa de entrada AEM e do aplicativo AEM Forms são diferentes. A Caixa de entrada AEM funciona somente com [Fluxos de trabalho centrados na Forms](../../forms/using/aem-forms-workflow.md) enquanto o aplicativo AEM Forms funciona com fluxos de trabalho e gerenciamento de processos centrados na Forms.

A tabela a seguir lista os recursos da Caixa de entrada AEM e do aplicativo AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Ações</strong></p> </td>
   <td><p><strong>Caixa de entrada AEM</strong></p> </td>
   <td><p><strong>Aplicativo AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Iniciando um aplicativo de formulário</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Envio de tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Delegar tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Rastreamento do histórico e do resumo das tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Adicionando anexos no nível da tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Exibindo anexos no nível da tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Adição de anexos em nível de campo</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Exibição da exibição de calendário</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Adição de comentários</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
 </tbody>
</table>
