---
title: Ações e recursos de Workflows AEM centrados em forma em workflows OSGi e AEM Forms JEE
description: Ações e recursos de Workflows AEM centrados em forma em workflows OSGi e AEM Forms JEE
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: d5d30e16d2561c020a82cdda847a9dd9b48acd3b
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 21%

---


# Ações e recursos de Workflows AEM centrados em forma em workflows OSGi e AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Caixa de entrada do AEM e área de trabalho HTML {#aem-inbox-and-html-workspace}

Você pode usar a Caixa de entrada do AEM para executar e monitorar Workflows AEM centrados em formulários no OSGi. Enquanto isso, o HTML Workspace permite que você execute e monitore Workflows JEE do AEM Forms. A tabela a seguir ajuda você a entender várias ações importantes disponíveis na Caixa de entrada do AEM para Workflows AEM centrados em formulários no OSGi e na Área de trabalho HTML para Workflows JEE AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Ações</td>
   <td>Caixa de entrada AEM</td>
   <td>Espaço de trabalho HTML</td>
  </tr>
  <tr>
   <td>Iniciar um processo, tarefa ou aplicativo de formulário<br /> </td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Enviando tarefas</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Atribuição de uma tarefa a um grupo</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Envio para várias rotas</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Rastreamento do histórico de tarefas e do resumo de tarefas</td>
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
   <td>visualização do calendário</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Comentários de nível de Tarefa</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Filas (fila pessoal compartilhada, tarefas de solicitação da fila)</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Notificação fora do escritório</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
    <tr>
   <td>Personalização de elementos da interface do usuário</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Atribuição de uma tarefa a vários usuários</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
 </tbody>
</table>

## Workflows AEM centrados em formulários em Workflows OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Workflows AEM centrados em forma no OSGi e Workflows JEE (AEM Forms no JEE Process Management) têm um conjunto diferente de recursos. A tabela a seguir ajuda você a entender os recursos importantes disponíveis em Workflows AEM centrados em forma no OSGi e AEM Forms em Workflows JEE:

<table>
 <tbody>
  <tr>
   <td>Recursos</td>
   <td>Workflows AEM centrados em forma no OSGi<br /> </td>
   <td>Workflows JEE AEM Forms</td>
  </tr>
  <tr>
   <td>Formulários adaptáveis</td>
   <td>Compatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Integração com outras soluções do AEM</td>
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
   <td>Definindo prioridade de tarefa</td>
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
   <td>Escolhendo dinamicamente um destinatário </td>
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
   <td>Supported <sup>[1]</sup></td>
   <td>Supported <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gerenciar aplicativos de tarefa e formulário</td>
   <td>Supported <sup>[2]</sup><br /> </td>
   <td>Supported <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Serviços de documentação</td>
   <td>Supported <sup>[3]</sup></td>
   <td>Supported <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Renderizar tarefa concluída como formulário adaptável ou documento PDF</td>
   <td>Compatível</td>
   <td>Compatível [4]</td>
  </tr>
  <tr>
   <td>Integração com o Gerenciamento de correspondência</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Botão de redefinição</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Etapas do fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Formulários adaptáveis somente leitura</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Ocultar o botão de gravação padrão</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Controle granular sobre a seção de detalhes do fluxo de trabalho</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Serviço de pesquisa/agendamento</td>
   <td>Disponível para utilização imediata</td>
   <td>Implementação personalizada necessária</td>
  </tr>
  <tr>
   <td>Aplicativo de formulários adaptativos</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço de Assembler</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Serviço do Gerador de PDF</td>
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
   <td>Garantia de Documento</td>
   <td>Compatível</td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Executar script</td>
   <td>Suporta ECMAScript</td>
   <td>Suporta códigos Java</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>  
  <tr>
   <td>Formulários HTML5, PDF forms interativos, Conjunto de formulários</td>
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
   <td>categorias de ponto de partida</td>
   <td>Incompatível </td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Aprovação de tarefa em massa </td>
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
   <td>Avatar do usuário</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>visualização do gerente</td>
   <td>Incompatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Modelos de pesquisa</td>
   <td>Incompatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Integração com aplicativos de terceiros</td>
   <td>Not Supported <sup>[6]</sup></td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Anexos em nível de Tarefa para o aplicativo de fluxo de trabalho ou ponto de inicialização</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Email do lembrete</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Alterar título no tempo limite da tarefa</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>E-mail sobre delegação de tarefas e declaração de tarefas</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Enviar um email ao final do fluxo de trabalho</td>
   <td>Supported <sup>[7]</sup></td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Delegar entre grupos de disjunção</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Chamar um serviço da Web de um fluxo de trabalho</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Transformação XSLT</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Gateways , SEM ESPERA </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
   <tr>
   <td>Variáveis para armazenar dados </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>OU, E dividir</td>
   <td>Incompatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Prioridade da tarefa dinâmica</td>
   <td>Incompatível</td>
   <td>Incompatível</td>
  </tr>
 </tbody>
</table>

1. Você pode usar Workflows AEM centrados em forma no OSGi para assinar um formulário adaptativo preenchido. Workflows AEM centrados em forma no OSGi são compatíveis com a assinatura de formulário. Não há suporte para a experiência de assinatura [](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) no formulário.

1. É necessário acessar a Caixa de entrada do AEM para executar e monitorar workflows centrados em forma nos AEM Forms OSGi e HTML Workspace para executar e monitorar AEM Forms JEE.
1. Os Serviços de Documento de AEM Forms nativos estão disponíveis para Workflows AEM centrados em forma no OSGi e AEM Forms em Workflows JEE. O AEM Workflow usa serviços de documento nativos para Workflows AEM centrados em forma em Workflows OSGi e AEM Forms JEE (Process Management).
1. Workflows JEE AEM Forms só podem renderizar um formulário adaptável. Ele não suporta a renderização de um formulário adaptável como um documento PDF.
1. Os Workflows JEE de formulários AEM não têm uma etapa separada para o Adobe Sign. Você precisa de um formulário adaptável habilitado para o Adobe Sign para Workflows JEE de formulários AEM. Para obter mais detalhes, consulte a documentação [do](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Adobe Sign.
1. Você pode usar a etapa [Invocar serviço](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) de modelo de dados de formulário para chamar um serviço da Web e postar ou recuperar dados de um aplicativo de terceiros.
1. Você pode usar a etapa [Enviar email](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar emails.

## Diferenças entre os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado no Forms são usar o aplicativo [AEM Inbox](../../forms/using/manage-applications-inbox.md) e o aplicativo AEM Forms. Os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms, no entanto, são diferentes. A Caixa de entrada do AEM funciona somente com workflows [centrados no](../../forms/using/aem-forms-workflow.md) Forms, enquanto o aplicativo AEM Forms funciona com workflows centrados no Forms e também com gerenciamento de processos.

A tabela a seguir lista os recursos da Caixa de entrada do AEM e do aplicativo AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Ações</strong></p> </td>
   <td><p><strong>Caixa de entrada AEM</strong></p> </td>
   <td><p><strong>Aplicativo AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Iniciar um aplicativo de formulário</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Enviando tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Delegando tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Rastreamento do histórico de tarefas e do resumo de tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Adicionar anexos de nível de tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Exibição de anexos de nível de tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Adicionar anexos de nível de campo</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Exibição da visualização do calendário</p> </td>
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

