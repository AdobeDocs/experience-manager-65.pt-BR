---
title: Exibindo e Compreendendo Relatórios de Transação
seo-title: Exibindo e Compreendendo Relatórios de Transação
description: Use os relatórios de transação para tomar uma decisão informada sobre o uso do produto e rebalanceamento de investimentos em hardware e software.
seo-description: Use os relatórios de transação para tomar uma decisão informada sobre o uso do produto e rebalanceamento de investimentos em hardware e software.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Exibindo e Compreendendo Relatórios de Transação{#viewing-and-understanding-transaction-reports}

Os relatórios de transação permitem capturar e rastrear o número de formulários enviados, documentos processados e documentos renderizados. O objetivo do rastreamento dessas transações é tomar uma decisão informada sobre o uso do produto e rebalancear os investimentos em hardware e software. Para obter mais informações, consulte Visão geral [dos relatórios de transação do](../../forms/using/transaction-reports-overview.md)AEM Forms.

## Configuração de relatórios de transação {#setting-up-transaction-reports}

O recurso Relatórios de transação está disponível como parte do pacote complementar de formulários AEM. Para obter informações sobre como instalar o pacote complementar em todas as instâncias de autor e publicação, consulte [Instalação e configuração de formulários](/help/forms/using/installing-configuring-aem-forms-osgi.md)AEM. Depois de instalar o pacote complementar de formulários AEM, faça o seguinte:

* Habilitar replicação reversa em todas as instâncias de publicação
* Ativar relatórios de transação
* Fornecer direitos para visualização de um relatório de transação
* (Opcional) Configurar Período de Liberação de Transação e Caixas de Saída [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Os relatórios de transação do AEM Forms não oferecem suporte a topologias que contêm apenas instâncias de publicação.
>* Antes de usar o relatórios de transação, verifique se a replicação reversa está ativada para todas as instâncias de publicação.
>* Os dados de transação são replicados revertidas de uma instância de publicação para somente a instância correspondente do autor ou do processamento. A instância de autor ou processamento não pode replicar mais os dados para outra instância.
>



### Habilitar replicação reversa em todas as instâncias de publicação {#enable-reverse-replication-on-all-the-publish-instances}

Os relatórios de transação usam replicação reversa para consolidar a contagem de transações das instâncias de publicação para as instâncias do autor. Configure a replicação reversa em todas as instâncias de publicação. Para obter instruções detalhadas sobre como configurar a replicação reversa, consulte [replicação](/help/sites-deploying/replication.md).

### Ativar relatórios de transação {#enable-transaction-reports}

Os relatórios de transação estão desativados por padrão. Você pode ativar os relatórios no console da Web do AEM. para ativar os relatórios de transação em um ambiente do AEM Forms, execute as seguintes etapas em todas as instâncias de autor e publicação:

1. Faça logon em uma instância do AEM como administrador. Vá até **Ferramentas** > **Operações** > Console **da Web**.
1. Localize e abra o serviço de Relatórios **de transações do** Forms.
1. Marque a caixa de seleção Registrar transações. Clique em **Salvar**.

   Repita as etapas de 1 a 3 em todas as instâncias de autor e publicação.

### Fornecer direitos para visualização de um relatório de transação {#provide-rights-to-view-a-transaction-report}

Somente os membros do grupo de administradores do fd podem visualização nos relatórios de transação. Para permitir que um usuário visualização relatórios de transação, torne os usuários membros do grupo de administradores de fd. Para obter instruções sobre como tornar um usuário membro de um grupo AEM, consulte Administração [de direitos de acesso, grupo e](/help/sites-administering/user-group-ac-admin.md)usuário.

### (Opcional) Configurar Período de Liberação de Transação e Caixas de Saída {#optional-configure-transaction-flush-period-and-outboxes}

As transações são armazenadas em cache na memória antes de serem armazenadas no repositório. Por padrão, o período de cache (Período de Liberação da Transação) é definido como 60 segundos. Execute as seguintes etapas para alterar o período de cache padrão:

1. Faça logon nas instâncias do autor como um administrador. Vá até **Ferramentas** > **Operações** > Console **da Web**.
1. Localize e abra o serviço Provedor **de Armazenamentos do Repositório de Transações de** Formulários.
1. Especifique o número de segundos no campo Período **de Liberação da** Transação. Clique em **Salvar**.

A replicação reversa copia dados de transação para a caixa de saída padrão das instâncias do autor. Você pode colocar dados de transação em uma caixa de saída personalizada. Execute as seguintes etapas para especificar uma caixa de saída personalizada:

1. Faça logon nas instâncias do autor como um administrador. Vá até **Ferramentas** > **Operações** > Console **da Web**.
1. Localize e abra o serviço Provedor **de Armazenamentos do Repositório de Transações de** Formulários.
1. Especifique o nome da caixa de saída personalizada no campo **Caixas de saída** . Clique em **Salvar**. Uma caixa de saída com o nome especificado é criada em todas as instâncias do autor.

## Exibindo o relatório de transações {#viewing-the-transaction-report}

Você pode visualização relatórios de transação em instâncias de autor ou publicação. O relatório de transação na instância do autor fornece uma soma agregada de todas as transações que ocorrem nas instâncias configuradas de autor e publicação. O relatório de transação na instância de publicação fornece uma contagem de transações que ocorrem somente na instância de publicação subjacente. Execute as seguintes etapas para visualização do relatório:

1. Faça logon no servidor do AEM Forms em `https://[hostname]:'port'`.
1. Navegue até **Ferramentas** > **Formulários**>**Relatório** de Transação de Visualização.

## Compreensão do relatório {#understanding-the-report}

O AEM Forms exibe relatórios de transação desde a data configurada, como mostrado em um relatório resumido abaixo:

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Use as opções **Redefinir a data para hoje** para redefinir os registros de transação. Quando você redefine a data para hoje, todos os registros de transação anteriores são perdidos. Quando você redefine a data em uma instância do autor, a alteração não afeta os relatórios de transação nas instâncias Publicar e, inversamente.
* Use a opção **Mostrar transações de apenas instâncias** de publicação para visualização de todas as transações que ocorreram somente na instância de publicação configurada ou no farm de publicação.
* Use as categorias: Processados **por** Documento, **Documentos renderizados** e **Formulários enviados** para visualização das transações correspondentes. Para o tipo de transações contabilizadas nessas categorias, consulte APIs [de Relatórios de Transação](../../forms/using/transaction-reports-billable-apis.md)Faturável.

## Registros de relatórios de transações de Visualização {#view-transaction-reporting-logs}

O relatórios de transação coloca todas as informações exibidas no relatório e algumas informações adicionais nos registros. As informações fornecidas nos registros são úteis para os usuários avançados. Por exemplo, os registros dividem transações em várias categorias granulares em comparação a três categorias consolidadas exibidas no relatório. Os registros estão em /crx-quickstart/logs/aem-forms-transaction.log.

## Artigos relacionados {#related-articles}

* [Visão geral dos relatórios de transação](../../forms/using/transaction-reports-overview.md)
* [Relatórios de transação APIs faturáveis](../../forms/using/transaction-reports-billable-apis.md)
* [Registrar uma transação para implementações personalizadas](/help/forms/using/record-transaction-custom-implementation.md)

