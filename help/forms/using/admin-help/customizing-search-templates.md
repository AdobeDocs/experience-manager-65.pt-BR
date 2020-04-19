---
title: Personalização de modelos de pesquisa
seo-title: Personalização de modelos de pesquisa
description: Você pode criar modelos de pesquisa a serem usados no Workspace para pesquisar instâncias de processos nas páginas de Tarefas e Rastreamento. Também é possível editar ou excluir modelos de pesquisa existentes.
seo-description: Você pode criar modelos de pesquisa a serem usados no Workspace para pesquisar instâncias de processos nas páginas de Tarefas e Rastreamento. Também é possível editar ou excluir modelos de pesquisa existentes.
uuid: 2043ba8a-07f0-4054-af3c-f3a14c2183ab
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_workspace
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6e4b4dfa-3af5-4c21-a2a1-b90ef02d8514
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Personalização de modelos de pesquisa {#customizing-search-templates}

Você pode criar modelos de pesquisa a serem usados no Workspace para pesquisar instâncias de processos nas páginas de Tarefas e Rastreamento. Também é possível editar ou excluir modelos de pesquisa existentes.

Ao criar ou editar um modelo de pesquisa, você pode especificar o layout e a ordem de classificação dos resultados da pesquisa. No entanto, os usuários podem modificar essas configurações no Workspace depois que os resultados da pesquisa forem exibidos.

Você pode criar quantos modelos de pesquisa forem necessários.

>[!NOTE]
>
>Ao salvar um modelo de pesquisa, você deve dar a ele um nome exclusivo. Caso contrário, um modelo existente pode ser substituído sem uma mensagem de aviso.

## Criar um modelo de pesquisa simples {#create-a-simple-search-template}

1. No console de administração, clique em Serviços > Área de trabalho > Pesquisar modelos.
1. Na guia Identificação, na caixa Descrição do modelo de pesquisa, forneça a finalidade do modelo.
1. (Opcional) Clique na guia Critérios e especifique os critérios de pesquisa para o modelo.
1. Clique na guia Salvar, digite um nome exclusivo para o modelo e clique em Salvar.

## Criar ou editar um modelo de pesquisa {#create-or-edit-a-search-template}

1. No console de administração, clique em Serviços > Área de trabalho > Pesquisar modelos.
1. (Opcional) Se você estiver editando um modelo existente ou usando um modelo existente como a base para um novo modelo, selecione o modelo na lista Pesquisar nome do modelo.
1. Na caixa Descrição do modelo de pesquisa, forneça a finalidade do modelo.
1. (Opcional) Na caixa Instruções do usuário, forneça quaisquer instruções que possam ajudar a usar o modelo. Essas instruções são exibidas no Workspace quando um usuário seleciona o modelo de pesquisa.
1. Clique na guia Critérios. Aqui você define um ou mais critérios de pesquisa. Para adicionar um critério de pesquisa:

   * Na parte superior da guia Critérios, selecione um Elemento de processo ou Elemento de Tarefa.

      **Dica**: *Se você tiver selecionado o elemento Nome do processo anteriormente e tiver especificado um processo, quaisquer Variáveis de processo definidas nesse processo também estarão disponíveis para seleção.*

      **Dica**: *Se você selecionar o elemento Visível da Tarefa, os usuários poderão remover tarefas concluídas dos resultados da pesquisa.*

      Os campos de critérios de pesquisa do elemento selecionado aparecem na parte inferior da guia Critérios.

   * Para cada Elemento de processo, Elemento de Tarefa e Variável de processo selecionados, preencha os campos de pesquisa correspondentes na parte inferior da guia Critérios:

      * Selecione um operador relacional (como &quot;ser igual a&quot;) na lista fornecida e especifique o valor do operando na caixa ao lado.
      * (Opcional) Para permitir que os usuários alterem o valor do operando no Workspace, selecione Permitir que o usuário altere o operando.
      * (Opcional) Para permitir que os usuários alterem o operador relacional, selecione Permitir que o usuário selecione outro operador relacional. Na lista exibida, selecione os operadores que estarão disponíveis para o usuário.
      **Dica**: *Se você selecionou Nome do processo como o elemento, poderá clicar no ícone ao lado do campo operando para exibir uma lista na qual é possível selecionar um processo que está sendo executado no servidor de formulários. Após selecionar um processo, quaisquer variáveis de processo definidas nesse processo estarão disponíveis para seleção em Variáveis de processo na seção superior da guia Critérios.*

      **Dica**: *Você pode excluir um elemento do modelo de pesquisa clicando no ícone Excluir ao lado dos critérios de pesquisa do elemento.*


1. (Opcional) Para que cada cabeçalho de coluna seja exibido nos resultados da pesquisa, clique na guia Layout e execute as seguintes etapas:

   * Selecione um elemento de processo ou tarefa e clique na seta para a direita para movê-lo para a lista Colunas para Relatório.
   * Na lista Colunas a serem relatadas, selecione o processo ou elemento de tarefa e clique na Seta para cima ou Seta para baixo para movê-la para o seu lugar na ordem da coluna. Os cabeçalhos de coluna nos resultados da pesquisa serão exibidos na ordem em que estão listados aqui.
   * (Opcional) Para alterar o nome do elemento para o cabeçalho da coluna, selecione o elemento na lista Colunas para Relatório e forneça o novo nome.
   >[!NOTE]
   >
   >O layout especificado no modelo de pesquisa substitui as preferências do usuário especificadas para os cabeçalhos de coluna no Workspace.

1. (Opcional) Para que cada coluna classifique os resultados da pesquisa, clique na guia Classificar e execute as seguintes etapas:

   * Selecione um elemento de processo ou tarefa e clique na seta para a direita para movê-lo para a lista Ordem de classificação.
   * Na lista Ordem de classificação, selecione o processo ou elemento de tarefa e clique na Seta para cima ou Seta para baixo para movê-lo para seu lugar na ordem de classificação. As colunas nos resultados da pesquisa serão classificadas com base na ordem em que estão listadas aqui.
   * (Opcional) Para classificar uma coluna em ordem decrescente, marque a caixa de seleção ao lado do nome do elemento. Se a caixa de seleção não estiver selecionada, a coluna será classificada em ordem crescente.

1. Clique na guia Salvar.
1. (Opcional) Se estiver criando um novo modelo de pesquisa, atribua a ele um nome exclusivo. Se você não especificar um nome exclusivo, poderá substituir um modelo existente.
1. Clique no botão Salvar.

## Excluir um modelo de pesquisa {#delete-a-search-template}

1. Na guia Identificação, selecione um nome na lista Nome do modelo de pesquisa.
1. Clique em Excluir este modelo e em OK.

