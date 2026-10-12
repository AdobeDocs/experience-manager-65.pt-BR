---
title: 'Banco de dados Microsoft SQL Server: ajuste da configuração'
description: Saiba como ajustar a configuração do banco de dados do Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%
---
# Banco de dados Microsoft SQL Server: ajuste da configuração {#microsoft-sql-server-database-fine-tuning-the-configuration}

Você deve alterar as configurações padrão ao usar o Microsoft SQL Server. Clique com o botão direito do mouse no servidor local do Oracle Enterprise Manager para acessar a caixa de diálogo de propriedades.

## Configurações de memória {#memory-settings}

Altere a alocação mínima de memória para o maior número possível. Se o banco de dados estiver sendo executado em um computador separado, use toda a memória. As configurações padrão não alocam memória de forma agressiva, o que dificulta o desempenho em quase qualquer banco de dados. Você deve ser mais agressivo na alocação de memória em máquinas de produção.

## Configurações do processador {#processor-settings}

Modifique as configurações do processador e, o mais importante, marque a caixa de seleção Aumentar a prioridade do SQL Server no Windows para que o servidor use o máximo possível de ciclos. A configuração Usar fibras NT é menos importante, mas convém selecioná-la também.

## Configurações do banco de dados {#database-settings}

Alterar as configurações do banco de dados. A configuração mais importante é Intervalo de Recuperação, que especifica o tempo máximo de espera pela recuperação após uma falha. A configuração padrão é de um minuto. Usar um valor maior, de 5 a 15 minutos, melhora o desempenho porque dá ao servidor mais tempo para gravar as alterações do log do banco de dados de volta nos arquivos do banco de dados.

>[!NOTE]
>
>Essa configuração não compromete o comportamento transacional porque altera somente o comprimento da repetição do arquivo de log que deve ser feita na inicialização.

Defina o tamanho Alocado de Espaço para o log e o arquivo de dados como muito maior que o banco de dados inicial. Considere quanto o banco de dados pode crescer ao longo de um ano. Idealmente, os arquivos de log e de dados são alocados em uma extensão contígua para que os dados não acabem fragmentados em todo o disco.
