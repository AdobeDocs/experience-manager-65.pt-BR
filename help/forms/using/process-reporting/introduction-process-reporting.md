---
title: Introdução ao Process Reporting
description: Introdução e principais recursos do AEM Forms no JEE Process Reporting
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
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
source-wordcount: '305'
ht-degree: 0%
---
# Introdução ao Process Reporting{#introduction-to-process-reporting}

![relatório-processo](assets/process-reporting.png)

Relatórios de processos é uma ferramenta baseada em navegador usada para criar e exibir relatórios sobre processos e tarefas do AEM Forms.

O Process Reporting fornece um conjunto de relatórios prontos para uso que permitem filtrar, exibir informações sobre processos de longa execução, duração do processo e volume do fluxo de trabalho.

Além disso, o Process Reporting fornece uma interface para executar consultas adhoc e integrar exibições de relatórios personalizadas à interface do usuário do Process Reporting.

Para obter a lista de navegadores compatíveis, consulte [Plataformas compatíveis com AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

O Process Reporting é construído em módulos que:

* Ler dados do processo do Banco de Dados do AEM Forms
* Publicar dados do processo em um repositório incorporado do Process Reporting
* Fornece uma interface de usuário baseada em navegador para exibir relatórios

## Principais recursos {#key-capabilities}

### Relatório sempre ativo {#always-on-reporting}

![gerenciamento de sites](assets/site-management.png)

Visualize a lista de processos de longa execução, gráficos de duração do processo e executar consultas personalizadas usando filtros.

Process Reporting também oferece a opção de exportar o relatório e consultar dados no formato CSV.

### Relatórios Ad Hoc {#adhoc-reports}

![impressão-&amp;-cor](assets/print-and-colour.png)

Use filtros para obter uma visualização específica dos seus dados.

Você pode pesquisar processos ou tarefas por ID, duração, datas de início e término, iniciador do processo e assim por diante.

É possível combinar vários filtros para criar relatórios específicos.

É possível salvar os filtros de relatório para execução em uma data ou hora posterior.

### Histórico de Processos/Tarefas {#process-task-history}

![gerenciamento de arquivos](assets/file-management.png)

Os servidores da AEM Forms executam vários processos em paralelo. Esses processos continuam em transição de um estado para outro. Ao publicar dados do Forms no repositório do Process Reporting em intervalos regulares, o Process Reporting retém as informações de transição sobre os processos em execução no AEM Forms.

### Controle de acesso {#access-control-br}

![sem título](assets/untitled.png)

O Process Reporting fornece acesso baseado em permissão à interface do usuário.

Isso significa que somente os usuários com permissões de relatório têm acesso à interface do usuário do Process Reporting.
