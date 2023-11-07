---
title: Pesquisando instâncias de processo
seo-title: Searching for process instances
description: Utilize a página Pesquisa de Processo para informar critérios de pesquisa para localizar uma instância de processo.
seo-description: Use the Process Search page to enter search criteria for finding a process instance.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
exl-id: 35f9acbf-7a82-43b1-9e17-9be4de666212
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Pesquisando instâncias de processo{#searching-for-process-instances}

Utilize a página Pesquisa de Processo para informar critérios de pesquisa para localizar uma instância de processo. Você pode acessar a página Pesquisa de Processo na página de fluxo de trabalho de formulários ou clicando em Pesquisar na página Instância de Processo.

Você pode informar critérios básicos para executar uma pesquisa geral, atributos específicos para executar uma pesquisa detalhada ou uma combinação de critérios básicos e atributos específicos para executar uma pesquisa combinada.

## Realizar uma pesquisa geral {#perform-a-general-search}

Uma pesquisa geral de um processo é mais apropriada se você souber a ID do processo da instância do processo, se estiver procurando um grupo de instâncias de processo relacionadas ou se apenas algumas instâncias de processo estiverem em execução.

Informe os critérios básicos para executar uma pesquisa geral. Se você informar vários critérios, a pesquisa será executada com uma condição AND implícita.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processo.
1. Na página Pesquisa do processo, em Pesquisa geral, forneça os seguintes critérios:

   * **ID do processo:** O número inteiro positivo que identifica cada instância de processo exclusiva.
   * **Status do processo:** Selecione um status na lista.
   * **Aplicativo:** Selecione um aplicativo na lista. Somente os aplicativos implantados são exibidos.
   * **Nome do processo - Versão:** Selecione um nome de processo no menu. Somente os processos implantados são exibidos.

1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

## Executar uma pesquisa detalhada para um processo {#perform-a-detailed-search-for-a-process}

Você pode informar atributos específicos para executar uma pesquisa detalhada. Uma pesquisa detalhada é mais apropriada se você tiver muitas instâncias de processo em execução e precisar restringir as possíveis localizações por determinados critérios.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processo.
1. Na página Pesquisa do processo, em Pesquisa detalhada, especifique seu primeiro conjunto de critérios:

   * Na lista Atributo, selecione um atributo.
   * Na lista Filtro, selecione um operador.
   * Na caixa Valor, digite um valor apropriado para o atributo selecionado.

1. Para adicionar outra linha, selecione Mais filtros. É exibido outro conjunto de listas de Atributo, Filtro e Valor e uma lista de Condições.
1. Em Condição, selecione AND ou OR. Repita as etapas de 1 a 3, conforme necessário, para restringir ainda mais sua pesquisa.
1. Para adicionar ou remover linhas, clique em Mais filtros ou Menos filtros. Você pode ter de uma a quatro linhas.
1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

[Sobre status de instância de processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Executar uma pesquisa combinada para um processo {#perform-a-combined-search-for-a-process}

Para criar uma pesquisa com base em uma pesquisa geral e em uma pesquisa detalhada, com um AND implícito entre as áreas, informe seus critérios de pesquisa nas áreas Pesquisa Geral e Pesquisa Detalhada na página Pesquisa do Processo.

Se a pesquisa for muito estreita, nenhuma instância será encontrada.
