---
title: Pesquisar instâncias de processo
seo-title: Searching for process instances
description: Use a página Pesquisa de Processo para inserir critérios de pesquisa para localizar uma instância de processo.
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Pesquisar instâncias de processo{#searching-for-process-instances}

Use a página Pesquisa de Processo para inserir critérios de pesquisa para localizar uma instância de processo. Você pode acessar a página Pesquisa de processo na página do fluxo de trabalho de formulários ou clicando em Pesquisar na página Instância do processo .

Você pode inserir critérios básicos para realizar uma pesquisa geral, atributos específicos para realizar uma pesquisa detalhada ou uma combinação de critérios básicos e atributos específicos para realizar uma pesquisa combinada.

## Realizar uma pesquisa geral {#perform-a-general-search}

Uma pesquisa geral por um processo é mais apropriada se você souber a ID do processo da instância do processo, se estiver procurando um grupo de instâncias do processo relacionadas ou se apenas algumas instâncias do processo estiverem em execução.

Insira critérios básicos para executar uma pesquisa geral. Se você inserir vários critérios, a pesquisa será executada com uma condição E implícita.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processos.
1. Na página Pesquisa de processo , em Pesquisa geral, forneça os seguintes critérios:

   * **ID do processo:** O número inteiro positivo que identifica cada instância de processo exclusiva.
   * **Status do processo:** Selecione um status na lista.
   * **Aplicativo:** Selecione um aplicativo na lista. Somente as aplicações implantadas são mostradas.
   * **Nome do processo - Versão:** Selecione um nome de processo no menu. Somente os processos implantados são mostrados.

1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

## Realizar uma pesquisa detalhada de um processo {#perform-a-detailed-search-for-a-process}

Você pode inserir atributos específicos para realizar uma pesquisa detalhada. Uma pesquisa detalhada é mais apropriada se você tiver muitas instâncias de processo em execução e precisar restringir os possíveis achados por determinados critérios.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processos.
1. Na página Pesquisa de processo , em Pesquisa detalhada, especifique seu primeiro conjunto de critérios:

   * Na lista Atributo, selecione um atributo.
   * Na lista Filtro , selecione um operador.
   * Na caixa Valor, digite um valor apropriado para o atributo selecionado.

1. Para adicionar outra linha, selecione Mais filtros. Outro conjunto de listas de Atributo, Filtro e Valor é exibido, bem como uma lista de Condições.
1. Em Condição, selecione E ou OU. Repita as etapas 1 a 3 conforme necessário para limitar ainda mais sua pesquisa.
1. Para adicionar ou remover linhas, clique em Mais filtros ou Menos filtros. É possível ter de uma a quatro linhas.
1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

[Sobre status da instância do processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Executar uma pesquisa combinada para um processo {#perform-a-combined-search-for-a-process}

Para criar uma pesquisa com base em uma pesquisa geral e em uma pesquisa detalhada, com um E implícito entre as áreas, insira os critérios de pesquisa nas áreas Pesquisa geral e Pesquisa detalhada na página Pesquisa de processo .

Se a pesquisa for muito estreita, nenhuma instância será encontrada.
