---
title: Ações e recursos de fluxos de trabalho de AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE
description: Ações e recursos de fluxos de trabalho de AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 23%

---

# Ações e recursos de fluxos de trabalho de AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Caixa de entrada e espaço de trabalho do AEM {#aem-inbox-and-html-workspace}

Você pode usar AEM Caixa de entrada para executar e monitorar fluxos de trabalho de AEM centrados no Forms no OSGi. Enquanto isso, o HTML Workspace permite executar e monitorar os Workflows do AEM Forms JEE. A tabela a seguir ajuda você a entender várias ações importantes disponíveis AEM Caixa de entrada para fluxos de trabalho de AEM centrados no Forms no OSGi e no HTML Workspace para fluxos de trabalho do AEM Forms JEE.

<table>
 <tbody>
  <tr>
   <td>Ações</td>
   <td>Caixa de entrada AEM</td>
   <td>HTML Workspace</td>
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
   <td>Histórico de tarefas de rastreamento e resumo de tarefas</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Notificações por email</td>
   <td>Compatível<br /> </td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Reatribuição de tarefas</td>
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
   <td>Filas (fila pessoal compartilhada, tarefas de Reivindicação da fila)</td>
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

## Fluxos de trabalho de AEM centrados em formulários nos workflows OSGi e AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Fluxos de trabalho de AEM centrados em formulários em OSGi e fluxos de trabalho JEE da AEM Forms (AEM Forms no JEE Process Management) têm um conjunto diferente de recursos. A tabela a seguir ajuda você a entender recursos importantes disponíveis em Fluxos de trabalho de AEM centrados em formulários no OSGi e no AEM Forms em fluxos de trabalho JEE:

<table>
 <tbody>
  <tr>
   <td>Recursos</td>
   <td>Fluxos de trabalho de AEM centrados em formulários no OSGi<br /> </td>
   <td>Fluxos de trabalho AEM Forms JEE</td>
  </tr>
  <tr>
   <td>Formulários adaptáveis</td>
   <td>Compatível</td>
   <td>Compatível<br /> </td>
  </tr>
  <tr>
   <td>Integração com outras soluções AEM</td>
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
   <td>Definição da prioridade da tarefa</td>
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
   <td>Suportado <sup>[1]</sup></td>
   <td>Suportado <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Gerenciar aplicativos de tarefa e formulário</td>
   <td>Suportado <sup>[2]</sup><br /> </td>
   <td>Suportado <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Serviços de documento</td>
   <td>Suportado <sup>[3]</sup></td>
   <td>Suportado <sup>[3]</sup></td>
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
   <td>Gateways , NO WAIT </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
   <tr>
   <td>Variáveis para armazenar dados </td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>OU E Dividir</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Avatar do usuário</td>
   <td>Compatível</td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Enviar um email ao final do workflow</td>
   <td>Suportado <sup>[7]</sup></td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td>Chamar um serviço da Web a partir de um fluxo de trabalho</td>
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
   <td>Ocultar o botão de salvamento padrão</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Controle granular sobre a seção de detalhes do workflow</td>
   <td>Compatível</td>
   <td>Incompatível</td>
  </tr>
  <tr>
   <td>Serviço de sondagem/agendamento</td>
   <td>Disponível imediatamente</td>
   <td>Implementação personalizada necessária</td>
  </tr>
  <tr>
   <td>Aplicativo adaptável Forms</td>
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
   <td>Controle de documentos</td>
   <td>Compatível</td>
   <td>Compatível </td>
  </tr>
  <tr>
   <td>Executar script</td>
   <td>Suporta ECMAScript</td>
   <td>Suporta snippets de código Java</td>
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
   <td>Categorias de pontos de partida</td>
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
   <td>Exibição do gerenciador</td>
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
   <td>Anexos em nível de tarefa para o aplicativo ou ponto de partida do fluxo de trabalho</td>
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
   <td>E-mail sobre delegação de tarefa e declaração de tarefa</td>
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
   <td>Prioridade da tarefa dinâmica</td>
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

1. Você pode usar Fluxos de trabalho de AEM centrados em formulários no OSGi para assinar um formulário adaptável preenchido. Fluxos de trabalho de AEM centrados em formulários no OSGi são compatíveis com a assinatura de formulário. O [assinatura no formulário](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) experiência não é suportada.

1. É necessário acessar AEM Caixa de entrada para executar e monitorar os fluxos de trabalho centrados em formulário no OSGi da AEM Forms e no HTML Workspace para executar e monitorar os fluxos de trabalho do AEM Forms JEE.
1. Os Serviços de documento nativos da AEM Forms estão disponíveis para fluxos de trabalho de AEM centrados em formulários no OSGi e no AEM Forms em fluxos de trabalho JEE. AEM fluxo de trabalho usa serviços de documento nativos para fluxos de trabalho de AEM centrados em formulários em fluxos de trabalho OSGi e AEM Forms JEE (Gerenciamento de processos).
1. Os fluxos de trabalho JEE do AEM Forms só podem renderizar um formulário adaptável. Ele não suporta renderização de um formulário adaptável como um documento PDF.
1. AEM fluxos de trabalho JEE de formulários não têm uma etapa separada para o Adobe Sign. Você precisa de um formulário adaptável habilitado para Adobe Sign para fluxos de trabalho JEE de formulários AEM. Para obter mais detalhes, consulte [Documentação do Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Você pode usar o [Chamar Serviço de Modelo de Dados de Formulário](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) etapa para invocar um serviço da Web e publicar ou recuperar dados de um aplicativo de terceiros.
1. Você pode usar o [Enviar Email](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar emails.

## Diferenças entre AEM caixa de entrada e os recursos do aplicativo AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Duas das principais maneiras de iniciar um fluxo de trabalho centrado no Forms estão usando [Caixa de entrada AEM](../../forms/using/manage-applications-inbox.md) e aplicativo AEM Forms. Os recursos da Caixa de entrada e do aplicativo AEM Forms AEM, no entanto, são diferentes. A Caixa de entrada de AEM funciona somente com [Fluxos de trabalho centrados na Forms](../../forms/using/aem-forms-workflow.md) enquanto o aplicativo AEM Forms funciona com fluxos de trabalho centrados na Forms e gerenciamento de processos.

A tabela a seguir lista os recursos da Caixa de entrada AEM e do aplicativo AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Ações</strong></p> </td>
   <td><p><strong>Caixa de entrada AEM</strong></p> </td>
   <td><p><strong>Aplicativo AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Início de um aplicativo de formulário</p> </td>
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
   <td><p>Histórico de tarefas de rastreamento e resumo de tarefas</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Incompatível</p> </td>
  </tr>
  <tr>
   <td><p>Adicionar anexos de nível de tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Exibir anexos de nível de tarefa</p> </td>
   <td><p>Compatível</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Adição de anexos de nível de campo</p> </td>
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
