---
title: Exibição e Noções Básicas dos Relatórios de Transação
seo-title: Viewing and Understanding Transaction Reports
description: Use os relatórios de transações para tomar uma decisão informada sobre o uso do produto e reequilibrar os investimentos em hardware e software.
seo-description: Use transaction reports to make an informed decision about the product usage and rebalancing investments in hardware and software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '858'
ht-degree: 0%

---

# Exibição e Noções Básicas dos Relatórios de Transação{#viewing-and-understanding-transaction-reports}

Relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo por trás do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e reequilibrar os investimentos em hardware e software. Para obter mais informações, consulte [Visão Geral dos Relatórios de Transação do AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configuração de relatórios de transações  {#setting-up-transaction-reports}

O recurso Relatórios de transação está disponível como parte do pacote complementar dos formulários AEM. Para obter informações sobre como instalar o pacote complementar em todas as instâncias do autor e de publicação, consulte [Instalação e configuração de formulários AEM](/help/forms/using/installing-configuring-aem-forms-osgi.md). Depois de instalar o pacote complementar do AEM Forms, faça o seguinte:

* Habilitar replicação reversa em todas as instâncias de publicação
* Ativar relatórios de transações
* Fornecer direitos para visualizar um relatório de transações
* (Opcional) Configurar Período de Liberação da Transação e Caixas de Saída [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Os relatórios de transação do AEM Forms não suportam topologias que contêm apenas instâncias de publicação.
>* Antes de usar o relatório de transações, verifique se a replicação reversa está ativada para todas as instâncias de publicação.
>* Os dados da transação são revertidos e replicados de uma instância de publicação para somente o autor ou instância de processamento correspondente. A instância de autoria ou processamento não pode replicar dados para outra instância.
>

### Habilitar replicação reversa em todas as instâncias de publicação {#enable-reverse-replication-on-all-the-publish-instances}

Os relatórios de transação usam replicação reversa para consolidar a contagem de transações de instâncias de publicação para instâncias de autoria. Configure a replicação inversa em todas as instâncias de publicação. Para obter instruções detalhadas sobre como configurar a replicação reversa, consulte [replicação](/help/sites-deploying/replication.md).

### Ativar relatórios de transações {#enable-transaction-reports}

Os relatórios de transação estão desativados por padrão. Você pode ativar os relatórios no Console da Web do AEM. para Ativar relatórios de transações em um ambiente do AEM Forms, execute as seguintes etapas em todas as instâncias do autor e de publicação:

1. Faça logon em uma instância do AEM como administrador. Ir para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o **Relatórios de transação do Forms** serviço.
1. Marque a caixa de seleção Registrar Transações. Clique em **Salvar**.

   Repita as etapas 1 a 3 em todas as instâncias de autor e publicação.

### Fornecer direitos para visualizar um relatório de transações {#provide-rights-to-view-a-transaction-report}

Somente os membros do grupo fd-administrator podem exibir relatórios de transações. Para permitir que um usuário visualize relatórios de transações, torne os usuários membros do grupo fd-administrator. Para obter instruções sobre como tornar um usuário membro de um grupo AEM, consulte [Administração de direitos de usuário, grupo e acesso](/help/sites-administering/user-group-ac-admin.md).

### (Opcional) Configurar Período de Liberação da Transação e Caixas de Saída {#optional-configure-transaction-flush-period-and-outboxes}

As transações são armazenadas em cache na memória antes de serem armazenadas no repositório. O processo é seguido para garantir que não haja gravações frequentes no repositório. Por padrão, o período de cache (Período de liberação da transação) é definido como 60 segundos. Você pode alterar o período padrão para adequá-lo ao seu ambiente. Execute as seguintes etapas para alterar o período de armazenamento em cache default:

1. Faça logon nas instâncias de criação como administrador. Ir para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o **Provedor de Armazenamento do Repositório de Transações da Forms** serviço.
1. Especifique o número de segundos na variável **Período de Liberação da Transação** campo. Clique em **Salvar**.

A replicação reversa copia os dados da transação para a caixa de saída padrão das instâncias do autor. Você pode colocar os dados da transação em uma caixa de saída personalizada. Execute as seguintes etapas para especificar uma caixa de saída personalizada:

1. Faça logon nas instâncias de criação como administrador. Ir para **Ferramentas** > **Operações** > **Console da Web**.
1. Localize e abra o **Provedor de Armazenamento do Repositório de Transações da Forms** serviço.
1. Especifique o nome da caixa de saída personalizada que **Caixas de saída** campo. Clique em **Salvar**. Uma caixa de saída com o nome especificado é criada em todas as instâncias do autor.

## Exibição do relatório de transações {#viewing-the-transaction-report}

Você pode exibir relatórios de transações nas instâncias de autor ou publicação. O relatório de transações na instância do autor fornece uma soma agregada de todas as transações que ocorrem nas instâncias do autor e de publicação configuradas. O relatório de transações na instância de publicação fornece uma contagem de transações que ocorrem somente na instância de publicação subjacente. Execute as seguintes etapas para exibir o relatório:

1. Faça logon no servidor do AEM Forms em `https://[hostname]:'port'`.
1. Navegue até **Ferramentas** > **Forms**>**Exibir Relatório de Transações**.

## Noções básicas do relatório {#understanding-the-report}

O AEM Forms exibe relatórios de transações desde a data configurada, conforme mostrado abaixo em um relatório resumido:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Use o **Redefinir a data como hoje** opções para redefinir registros de transação. Ao redefinir a data como hoje, todos os registros de transações anteriores são perdidos. Ao redefinir a data em uma instância de autor, a alteração não afeta os relatórios de transações nas instâncias Publicar e vice-versa.
* Use o **Mostrar transações somente de Instâncias de publicação** para exibir todas as transações que ocorreram somente na instância de publicação configurada ou no farm de publicação.
* Use as categorias: **Documento processado**, **Documentos renderizados**, e **Forms enviado** para exibir transações correspondentes. Para o tipo de transações contabilizadas nessas categorias, consulte [APIs de relatórios de transações faturáveis](../../forms/using/transaction-reports-billable-apis.md).

## Exibir logs de relatórios de transações {#view-transaction-reporting-logs}

O relatório de transações coloca todas as informações exibidas no relatório e algumas informações adicionais nos logs. As informações fornecidas nos logs são úteis para os usuários avançados. Por exemplo, os registros dividem as transações em várias categorias granulares em comparação às três categorias consolidadas exibidas no relatório. Os logs estão disponíveis no `error.log` arquivo no `/crx-repository/logs/` diretório. Os logs estarão disponíveis mesmo que você não ative os relatórios de transação do Console da Web do AEM.

## Artigos relacionados {#related-articles}

* [Visão Geral dos Relatórios de Transação](../../forms/using/transaction-reports-overview.md)
* [APIs de relatórios de transação faturáveis](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)
