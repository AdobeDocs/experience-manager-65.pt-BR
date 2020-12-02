---
title: Criação e configuração de grupos
seo-title: Criação e configuração de grupos
description: Saiba como criar grupos de forma manual ou dinâmica, editar um grupo, detalhes de visualização sobre um grupo ou excluir um grupo.
seo-description: Saiba como criar grupos de forma manual ou dinâmica, editar um grupo, detalhes de visualização sobre um grupo ou excluir um grupo.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
translation-type: tm+mt
source-git-commit: d3719a9ce2fbb066f99445475af8e1f1e7476f4e
workflow-type: tm+mt
source-wordcount: '1593'
ht-degree: 0%

---


# Criação e configuração de grupos{#creating-and-configuring-groups}

Criar grupos de usuários permite que você atribua funções ao grupo em vez de a usuários individuais.

Dois tipos diferentes de grupos estão disponíveis. Você pode criar manualmente um grupo e adicionar usuários e outros grupos a ele. Você também pode criar grupos dinâmicos que incluem automaticamente todos os usuários que atendem a um conjunto de regras especificado.

Os usuários podem experimentar um tempo de resposta mais lento se pertencerem a muitos grupos (por exemplo, 500 ou mais) ou se os grupos estiverem profundamente aninhados (por exemplo, 30 níveis). Se você estiver enfrentando esse problema, é possível configurar formulários AEM para obter previamente informações de determinados domínios. (Consulte [Configurar formulários AEM para pré-buscar informações de domínio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Criar um grupo manualmente {#create-a-group-manually}

Ao criar manualmente um grupo, você pode adicionar usuários e outros grupos a ele e atribuir funções ao grupo. Você também pode associar o grupo a um grupo pai.

Se você estiver usando o Content Services (obsoleto), poderá selecionar a opção Selecionar esta opção para encaminhar usuários e grupos para provedores de Armazenamentos principais externos registrados na página Gerenciamento de domínio para encaminhar as informações para quaisquer novos usuários ou grupos criados no Content Services (obsoleto).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos e clique em Novo grupo.
1. Complete a seção Configurações gerais e clique em Avançar. Nome canônico e Nome do grupo são atributos obrigatórios.

   O Nome Canônico é um identificador exclusivo do grupo. Cada grupo e usuário em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Gerado pelo sistema para permitir que o Gerenciamento de usuários atribua um valor exclusivo ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome canônico.

   Evite usar caracteres sublinhados (_) em nomes canônicos, por exemplo, `sample_group`. Quando você pesquisa grupos com base em seu nome canônico, os que contêm caracteres sublinhados não são retornados.

1. Para adicionar usuários e grupos a esse novo grupo, clique em Localizar usuários/grupos e faça as seguintes tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista In, selecione Usuários, grupos ou Usuários e grupos.
   * Na lista Usando, selecione Nome, Email ou ID de usuário.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos usuários e grupos a serem adicionados a esse novo grupo e clique em OK.

1. Clique em Avançar.
1. Para adicionar esse novo grupo a outros grupos existentes, clique em Localizar grupos e faça as seguintes tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos grupos aos quais o novo grupo pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo, clique em Localizar funções, marque as caixas de seleção de cada função a ser atribuída ao grupo e clique em OK. Os usuários do grupo herdam funções atribuídas no nível do grupo.
1. Clique em Concluir.

## Criar um grupo dinâmico {#create-a-dynamic-group}

Em um grupo dinâmico, você não seleciona individualmente os usuários que pertencem ao grupo. Em vez disso, você especifica um conjunto de regras e todos os usuários que atendem a essas regras são adicionados automaticamente ao grupo dinâmico.

Use uma destas duas maneiras para criar grupos dinâmicos:

* Ative a criação automática de grupos dinâmicos com base em domínios de email, como @adobe.com. Quando você ativa esse recurso, o Gerenciamento de usuários cria um grupo dinâmico para cada domínio de email exclusivo no banco de dados de formulários AEM. Use uma expressão cron para especificar com que frequência o Gerenciamento de usuários pesquisa o banco de dados de formulários AEM para novos domínios de email. Esses grupos dinâmicos são adicionados ao domínio local DefaultDom e são nomeados como &quot;Todos os usuários com uma ID de email *`[email domain]`*&quot;.
* Crie um grupo dinâmico com base em critérios especificados, incluindo o domínio de email do usuário, a descrição, o nome canônico e o nome do domínio. Para pertencer ao grupo dinâmico, um usuário deve atender a todos os critérios especificados. Para configurar uma condição &quot;ou&quot;, crie dois grupos dinâmicos separados e adicione-os a um grupo local. Por exemplo, use essa abordagem para criar um grupo de usuários que pertençam ao domínio de email @adobe.com ou cujo nome canônico contenha ou=adobe.com. No entanto, os utilizadores não têm necessariamente de satisfazer ambas as condições.

Um grupo dinâmico contém apenas usuários. Não pode conter outros grupos. No entanto, um grupo dinâmico pode pertencer a um grupo pai.

### Criar grupos dinâmicos automaticamente com base em domínios de email {#automatically-create-dynamic-groups-based-on-email-domains}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Configurar atributos avançados do sistema.
1. Em Criação automática de grupo dinâmico, marque a caixa de seleção.
1. Especifique quando o Gerenciador de usuários verifica novos domínios de email. Esse tempo deve ser após o tempo de sincronização do domínio, pois a criação de grupos dinâmicos é lógica somente se a sincronização do domínio estiver concluída.

   * Para ativar a sincronização automática diariamente, digite o horário no formato de 24 horas na caixa Ocorre diariamente em. Quando você salva suas configurações, esse valor é convertido em uma expressão cron, exibida na caixa abaixo.
   * Para programar a sincronização em um dia específico da semana ou mês, ou em um mês específico, selecione digite a expressão de cron apropriada na caixa. O valor padrão é `0 00 4 ? * *` (o que significa verificar em 4 A.M. todos os dias).

      O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

1. Clique em Salvar.

### Criar um grupo dinâmico com base em critérios especificados {#create-a-dynamic-group-based-on-specified-criteria}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Clique em Novo grupo dinâmico.
1. Complete a seção Configurações gerais. Nome do grupo é um atributo obrigatório. Você pode atribuir o grupo a qualquer domínio configurado.
1. Em Critérios de grupo dinâmico, especifique um ou mais atributos usados para preencher o grupo dinâmico.

   >[!NOTE]
   >
   >Os atributos Email, Description e Canonical Name fazem distinção entre maiúsculas e minúsculas ao usar o operador Equals. Eles não fazem distinção entre maiúsculas e minúsculas com os operadores Start Com, Termina com ou Contém.

   **Email: domínio de email do** usuário, como  `@adobe.com`.

   **Descrição:descrição** do usuário, como &quot;Cientista da computação&quot;

   **Nome canônico:nome canônico do** usuário, como  `ou=adobe.com`

   **Nome do domínio:** o nome do domínio ao qual o usuário pertence, como  `DefaultDom`. O atributo Nome de domínio faz distinção entre maiúsculas e minúsculas ao usar o operador Contém. Não diferencia maiúsculas de minúsculas com os operadores Start Com, Termina com ou Igual.

1. Clique em Testar. Uma página de teste exibe os primeiros 200 usuários que atendem aos critérios definidos. Clique em Fechar.
1. Se o teste retornou os resultados esperados, clique em Avançar. Caso contrário, edite os critérios de grupo dinâmico e teste novamente.
1. Para adicionar o grupo dinâmico a um grupo pai, clique em Localizar grupos e faça as seguintes tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos grupos aos quais o grupo dinâmico pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo dinâmico, clique em Localizar funções, marque as caixas de seleção de cada função a ser atribuída ao grupo e clique em OK. Os usuários do grupo herdam funções atribuídas no nível do grupo.
1. Clique em Concluir.

## Detalhes da visualização sobre um grupo {#view-details-about-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista In, selecione Grupo e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. É possível classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do grupo para exibir detalhes sobre o. A página Detalhes do grupo é exibida.
1. Para visualização de membros diretos do grupo, clique em Principais filhos.

## Editar um grupo {#edit-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Para localizar o grupo a ser editado, faça as seguintes tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista Using (Uso), selecione Name (Nome) ou Email.
   * Na lista In, selecione Grupos.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, clique no nome do grupo a ser editado.

1. Na guia Detalhes, edite as configurações gerais e clique em Salvar.
1. Para editar os grupos associados, clique na guia Grupos pai e faça as seguintes tarefas:

   * Para localizar grupos a serem adicionados à associação, clique em Localizar grupos e preencha as informações de pesquisa.
   * Para adicionar grupos, marque a caixa de seleção dos grupos a serem adicionados, clique em OK e em Salvar.
   * Para excluir um grupo associado, marque a caixa de seleção do grupo a ser excluído, clique em Excluir, clique em OK e em Salvar.

1. Para editar os usuários e grupos no grupo, clique na guia Principais filhos e faça as seguintes tarefas:

   * Para localizar usuários e grupos a serem adicionados, clique em Localizar usuários/grupos e preencha as informações de pesquisa.
   * Para adicionar um usuário ou grupo, marque a caixa de seleção do usuário ou grupo, clique em OK e em Salvar.
   * Para excluir um usuário ou grupo, marque a caixa de seleção do usuário ou grupo, clique em Excluir, clique em OK e em Salvar.

1. Para editar atribuições de função, clique na guia Atribuições de função e faça as seguintes tarefas:

   * Para localizar funções a serem atribuídas ao grupo, clique em Localizar Funções.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em OK e em Salvar.
   * Para cancelar a atribuição de uma função, marque a caixa de seleção da função, clique em Cancelar atribuição e clique em Salvar.

## Excluir um grupo {#delete-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista Localizar, selecione Grupos e clique em Localizar.
1. Marque a caixa de seleção do grupo a ser excluído, clique em Excluir e, em seguida, clique em OK.

