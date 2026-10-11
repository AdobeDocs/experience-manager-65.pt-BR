---
title: Rastreamento de processos
description: Como rastrear seus processos pesquisando por eles e visualizando seus detalhes.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 381a46c6-c73c-476a-a1a0-20d921069c37
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%
---
# Rastreamento de processos {#tracking-processes}

Na página Rastreamento, é possível pesquisar processos ativos ou concluídos nos quais você iniciou ou participou e exibir os detalhes do processo. Os detalhes do processo mostram as tarefas, atribuições e formulários que faziam parte do processo. Você também pode iniciar novos processos usando dados de formulário de um processo iniciado anteriormente.

## Pesquisar processos e tarefas {#search-for-processes-and-tasks}

Você pode pesquisar instâncias de processos e tarefas associadas com base em nomes de processos ou usando modelos de pesquisa definidos pelo administrador do espaço de trabalho do AEM Forms.

Você pode definir quais colunas aparecem nos resultados da pesquisa.

>[!NOTE]
>
>Os resultados da pesquisa não incluem tarefas que apareceram em um grupo ou lista compartilhada à qual você tem acesso, a menos que você realmente tenha participado das tarefas. Os resultados não incluem instâncias de processos concluídas que o administrador removeu.

### Pesquisar por nome de processo {#search-by-process-name}

1. Na página Rastreamento, no painel esquerdo, selecione um nome de processo. Todas as instâncias desse processo nas quais você iniciou ou concluiu uma tarefa são exibidas no painel principal.
1. Clique em uma instância do processo para exibir mais informações sobre ela.

### Procurar uma tarefa usando um modelo de pesquisa {#search-for-a-task-using-a-search-template}

1. Na página Acompanhamento, na lista à esquerda, selecione **Pesquisar Modelos** e selecione um modelo de pesquisa.
1. Se o modelo der suporte a parâmetros de pesquisa, Para restringir os parâmetros de pesquisa, preencha os campos do modelo e clique em **Pesquisar**. Exibe uma lista de todas as tarefas das quais você participou, que correspondem aos critérios de pesquisa.

## Exibir detalhes do processo {#view-process-details}

Na página de Rastreamento, é possível selecionar um processo e visualizar seus detalhes. Você pode pesquisar os processos com base em vários parâmetros para exibir os detalhes da tarefa. Você também pode visualizar a guia Status para processos que têm vários usuários recebendo tarefas em paralelo, onde as ferramentas para revisar documentos estão habilitadas.

**Status:** o status das tarefas em um processo é exibido na coluna &#39;Ação Selecionada&#39; quando você clica em uma tarefa. No entanto, o status do processo não está disponível.

1. Selecione a instância do processo na lista de resultados da pesquisa para exibir detalhes das tarefas que fazem parte da instância do processo.
1. Para exibir mais informações sobre uma tarefa, execute uma ou mais destas ações:

   * Para exibir notas e anexos de uma tarefa, clique na guia Anexos.
   * Para exibir os detalhes de atribuição da tarefa, clique na guia Atribuição.
   * Para exibir o formulário associado, clique no botão de formulário.
