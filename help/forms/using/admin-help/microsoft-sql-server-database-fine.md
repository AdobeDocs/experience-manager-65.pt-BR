---
title: '"Banco de dados do Microsoft SQL Server: Ajuste da configuração"'
seo-title: '"Banco de dados do Microsoft SQL Server: Ajuste da configuração"'
description: Saiba como ajustar a configuração do banco de dados do Microsoft SQL Server.
seo-description: Saiba como ajustar a configuração do banco de dados do Microsoft SQL Server.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Banco de dados do Microsoft SQL Server: Ajuste da configuração {#microsoft-sql-server-database-fine-tuning-the-configuration}

Você deve alterar as configurações padrão ao usar o Microsoft SQL Server. Clique com o botão direito do mouse no servidor local no Oracle Enterprise Manager para acessar a caixa de diálogo de propriedades.

## Configurações de memória {#memory-settings}

Altere a alocação mínima de memória para o maior número possível. Se o banco de dados estiver sendo executado em um computador separado, use toda a memória. As configurações padrão não alocam memória de forma agressiva, o que dificulta o desempenho em quase qualquer banco de dados. Você deveria ser mais agressivo em alocar memória em máquinas de produção.

## Configurações do processador {#processor-settings}

Modifique as configurações do processador e, mais importante, marque a caixa de seleção Aumentar prioridade do SQL Server no Windows para que o servidor use o maior número possível de ciclos. A configuração Usar fibras NT é menos importante, mas talvez você também queira selecioná-la.

## Configurações do banco de dados {#database-settings}

Altere as configurações do banco de dados. A configuração mais importante é o Intervalo de recuperação, que especifica a quantidade máxima de tempo de espera para a recuperação após uma falha. A configuração padrão é de um minuto. Usar um valor maior, de 5 a 15 minutos, melhora o desempenho, pois dá ao servidor mais tempo para gravar alterações do log do banco de dados de volta nos arquivos do banco de dados.

>[!NOTE]
>
>Essa configuração não compromete o comportamento transacional, pois altera apenas o comprimento da reprodução do arquivo de log que deve ser feita na inicialização.

Defina o tamanho Espaço alocado para o log e o arquivo de dados como muito maior que o banco de dados inicial. Considere o quanto o banco de dados pode crescer ao longo de um ano. O ideal é que os arquivos de log e de dados sejam alocados em uma extensão contígua para que os dados não acabem fragmentados em todo o disco.
