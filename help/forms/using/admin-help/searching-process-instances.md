---
title: Procurando instâncias de processo
seo-title: Procurando instâncias de processo
description: Use a página Pesquisa de Processo para informar critérios de pesquisa para localizar uma instância de processo.
seo-description: Use a página Pesquisa de Processo para informar critérios de pesquisa para localizar uma instância de processo.
uuid: 4a9c5b05-add5-4278-9c6f-d1928b6860d2
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 88b634bb-8f6c-4830-ad01-821668609615
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Procurando instâncias de processo{#searching-for-process-instances}

Use a página Pesquisa de Processo para informar critérios de pesquisa para localizar uma instância de processo. Você pode acessar a página Pesquisa de processos na página de fluxo de trabalho de formulários ou clicando em Pesquisar na página Instância de processos.

Você pode informar critérios básicos para realizar uma pesquisa geral, atributos específicos para realizar uma pesquisa detalhada ou uma combinação de critérios básicos e atributos específicos para executar uma pesquisa combinada.

## Executar uma pesquisa geral {#perform-a-general-search}

Uma pesquisa geral por um processo é mais apropriada se você souber a ID do processo da instância do processo, se estiver procurando por um grupo de instâncias do processo relacionadas ou se apenas algumas instâncias do processo estiverem em execução.

Informe os critérios básicos para realizar uma pesquisa geral. Se você inserir vários critérios, a pesquisa será realizada com uma condição E implícita.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processos.
1. Na página Pesquisa de processos, em Pesquisa geral, forneça os seguintes critérios:

   * **ID do processo:** o número inteiro positivo que identifica cada instância exclusiva do processo.
   * **Status do processo:** selecione um status na lista.
   * **Aplicativo:** selecione um aplicativo da lista. Somente aplicativos implantados são exibidos.
   * **Nome do processo - Versão:** selecione um nome de processo no menu. Somente os processos implantados são exibidos.

1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

## Execute uma pesquisa detalhada para um processo {#perform-a-detailed-search-for-a-process}

Você pode inserir atributos específicos para realizar uma pesquisa detalhada. Uma pesquisa detalhada é mais apropriada se você tiver muitas instâncias de processo em execução e precisar restringir as localizações possíveis por determinados critérios.

1. No console de administração, clique em Serviços > Fluxo de trabalho do Forms > Pesquisa de processos.
1. Na página Pesquisa de Processo, em Pesquisa Detalhada, especifique seu primeiro conjunto de critérios:

   * Na lista Atributo, selecione um atributo.
   * Na lista Filtro, selecione um operador.
   * Na caixa Valor, digite um valor apropriado para o atributo selecionado.

1. Para adicionar outra linha, selecione Mais Filtros. Outro conjunto de listas de Atributo, Filtro e Valor é exibido, bem como uma lista de Condição.
1. Em Condição, selecione E ou OU. Repita as etapas de 1 a 3 conforme necessário para restringir ainda mais sua pesquisa.
1. Para adicionar ou remover linhas, clique em Mais Filtros ou Menos Filtros. Você pode ter de uma a quatro linhas.
1. Clique em Pesquisar. A página Instância do processo é exibida, listando as instâncias encontradas.

[Sobre os status da instância do processo](/help/forms/using/admin-help/processes.md#about-process-instance-statuses)

## Execute uma pesquisa combinada para um processo {#perform-a-combined-search-for-a-process}

Para criar uma pesquisa com base em uma pesquisa geral e em uma pesquisa detalhada, com um E implícito entre as áreas, informe os critérios de pesquisa nas áreas Pesquisa Geral e Pesquisa Detalhada na página Pesquisa do Processo.

Se a pesquisa for muito estreita, nenhuma instância será encontrada.
