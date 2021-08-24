---
title: Exibindo e Noções Gerais de Relatórios de Transações
seo-title: Exibindo e Noções Gerais de Relatórios de Transações
description: Use os relatórios de transação para tomar uma decisão informada sobre o uso do produto e o rebalanceamento de investimentos em hardware e software.
seo-description: Use os relatórios de transação para tomar uma decisão informada sobre o uso do produto e o rebalanceamento de investimentos em hardware e software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 75e1697c301dca3a649833a45caa1753fdc81514
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Exibindo e Noções Gerais de Relatórios de Transações{#viewing-and-understanding-transaction-reports}

Relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e reequilibrar os investimentos em hardware e software. Para obter mais informações, consulte [Visão geral dos relatórios de transação do AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configuração de relatórios de transações  {#setting-up-transaction-reports}

O recurso Relatórios de transação está disponível como parte do pacote complementar de formulários AEM. Para obter informações sobre como instalar o pacote complementar em todas as instâncias de autor e publicação, consulte [Instalar e configurar formulários AEM](/help/forms/using/installing-configuring-aem-forms-osgi.md). Depois de ter o pacote complementar de formulários AEM instalado, faça o seguinte:

* Habilitar replicação reversa em todas as instâncias de publicação
* Ativar relatórios de transações
* Fornecer direitos para exibir um relatório de transação
* (Opcional) Configurar Período de Liberação de Transação e Caixas de Saída [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Os relatórios de transação do AEM Forms não são compatíveis com topologias que contêm apenas instâncias de publicação.
>* Antes de usar o relatório de transações, verifique se a replicação reversa está habilitada para todas as instâncias de publicação.
>* Os dados de transação são replicados reversivamente de uma instância de publicação para apenas a instância de autor ou processamento correspondente. A instância de processamento ou autor não pode replicar mais os dados para outra instância.

>



### Habilitar replicação reversa em todas as instâncias de publicação {#enable-reverse-replication-on-all-the-publish-instances}

Os relatórios de transação usam replicação reversa para consolidar a contagem de transações das instâncias de publicação para as instâncias de autor. Configure a replicação inversa em todas as instâncias de publicação. Para obter instruções detalhadas sobre como configurar a replicação inversa, consulte [replication](/help/sites-deploying/replication.md).

### Ativar relatórios de transações {#enable-transaction-reports}

Os relatórios de transação são desativados por padrão. Você pode ativar os relatórios AEM Console da Web. para ativar os relatórios de transação em um ambiente AEM Forms, execute as seguintes etapas em todas as instâncias de criação e publicação:

1. Faça logon em uma instância AEM como administrador. Vá para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o serviço **Forms Transaction Reporting**.
1. Marque a caixa de seleção Registrar Transações. Clique em **Salvar**.

   Repita as etapas 1 a 3 em todas as instâncias de autor e publicação.

### Fornecer direitos para exibir um relatório de transação {#provide-rights-to-view-a-transaction-report}

Somente os membros do grupo fd-administrators podem exibir os relatórios de transação. Para permitir que um usuário exiba relatórios de transação, torne os usuários membros do grupo fd-administrators . Para obter instruções sobre como tornar um usuário membro de um grupo de AEM, consulte [Administração de Usuário, Grupo e Direitos de Acesso](/help/sites-administering/user-group-ac-admin.md).

### (Opcional) Configurar Período de Liberação de Transação e Caixas de Saída {#optional-configure-transaction-flush-period-and-outboxes}

As transações são armazenadas em cache na memória antes de serem armazenadas no repositório. O processo é seguido para garantir que não haja gravações frequentes no repositório. Por padrão, o período de armazenamento em cache (Período de Liberação da Transação) é definido como 60 segundos. Você pode alterar o período padrão para se adequar ao seu ambiente. Execute as seguintes etapas para alterar o período padrão de armazenamento em cache:

1. Faça logon nas instâncias de criação como administrador. Vá para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o serviço **Forms Transaction Repository Storage Provider**.
1. Especifique o número de segundos no campo **Período de Liberação da Transação**. Clique em **Salvar**.

A replicação inversa copia os dados da transação para a caixa de saída padrão das instâncias do autor. Você pode colocar os dados da transação em uma caixa de saída personalizada. Execute as seguintes etapas para especificar uma caixa de saída personalizada:

1. Faça logon nas instâncias de criação como administrador. Vá para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o serviço **Forms Transaction Repository Storage Provider**.
1. Especifique o nome da caixa de saída personalizada no campo **Caixas de saída**. Clique em **Salvar**. Uma caixa de saída com o nome especificado é criada em todas as instâncias do autor.

## Exibição do relatório de transações {#viewing-the-transaction-report}

Você pode exibir relatórios de transação em instâncias de criação ou publicação. O relatório de transação na instância de autor fornece uma soma agregada de todas as transações que ocorrem nas instâncias de autor e publicação configuradas. O relatório de transação na instância de publicação fornece uma contagem de transações que ocorrem apenas na instância de publicação subjacente. Execute as seguintes etapas para visualizar o relatório:

1. Faça logon no servidor do AEM Forms em `https://[hostname]:'port'`.
1. Navegue até **Ferramentas** > **Forms****Exibir Relatório de Transação**.

## Noções básicas sobre o relatório {#understanding-the-report}

O AEM Forms exibe relatórios de transação desde a data configurada, conforme mostrado em um relatório resumido abaixo:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Use as opções **Reset the date to today** para redefinir os registros de transação. Quando você redefine a data para hoje, todos os registros de transação anteriores são perdidos. Quando você redefine a data em uma instância do autor, a alteração não afeta os relatórios de transação nas instâncias de Publicação e, inversamente.
* Use o **Show transactions of only Publish instances** para exibir todas as transações que ocorreram somente na instância de publicação configurada ou no farm de publicação.
* Use as categorias: **Documento processado**, **Documentos renderizados** e **Forms enviado** para exibir as transações correspondentes. Para o tipo de transações contabilizadas nessas categorias, consulte [APIs de Relatórios de Transações Faturáveis](../../forms/using/transaction-reports-billable-apis.md).

## Exibir logs de relatórios de transações {#view-transaction-reporting-logs}

O relatório de transações coloca todas as informações exibidas no relatório e algumas informações adicionais nos logs. As informações fornecidas nos logs são úteis para os usuários avançados. Por exemplo, os logs dividem as transações em várias categorias granulares em comparação às três categorias consolidadas exibidas no relatório. Os logs estão disponíveis no arquivo `error.log` no diretório `/crx-repository/logs/`. Os logs estão disponíveis mesmo se você não habilitar os relatórios de transação AEM Console da Web.

## Artigos relacionados {#related-articles}

* [Visão geral dos relatórios de transação](../../forms/using/transaction-reports-overview.md)
* [APIs faturáveis dos relatórios de transação](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
