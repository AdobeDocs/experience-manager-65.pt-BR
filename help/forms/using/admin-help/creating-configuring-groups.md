---
title: Criação e configuração de grupos
seo-title: Creating and configuring groups
description: Saiba como criar grupos manual ou dinamicamente, editar um grupo, visualizar detalhes sobre um grupo ou excluir um grupo.
seo-description: Learn how to create groups manually or dynamically, edit a group, view details about a group, or delete a group.
uuid: 8532d72b-270a-4fcf-b7a5-56fca979a5fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2058b501-65ce-4ad3-8e1b-b2eab896f70f
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Criação e configuração de grupos{#creating-and-configuring-groups}

Criar grupos de usuários permite atribuir funções ao grupo em vez de a usuários individuais.

Dois tipos diferentes de grupos estão disponíveis. Você pode criar um grupo manualmente e adicionar usuários e outros grupos a ele. Você também pode criar grupos dinâmicos que incluem automaticamente todos os usuários que atendem a um conjunto específico de regras.

Os usuários podem experimentar um tempo de resposta mais lento se pertencerem a muitos grupos (por exemplo, 500 ou mais) ou se os grupos estiverem profundamente aninhados (por exemplo, 30 níveis). Se você estiver enfrentando esse problema, é possível configurar AEM formulários para buscar previamente informações de determinados domínios. (Consulte [Configurar formulários AEM para buscar previamente informações de domínio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Criar um grupo manualmente {#create-a-group-manually}

Ao criar um grupo manualmente, é possível adicionar usuários e outros grupos a ele e atribuir funções ao grupo. Também é possível associar o grupo a um grupo pai.

Se você estiver usando os Serviços de conteúdo (obsoleto), poderá selecionar a opção Selecionar essa opção para encaminhar usuários e grupos para os principais provedores de armazenamento externo registrado na página Gerenciamento de domínio para encaminhar as informações para quaisquer novos usuários ou grupos criados nos Serviços de conteúdo (obsoleto).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos e, em seguida, clique em Novo grupo.
1. Complete a seção Configurações gerais e clique em Avançar. Nome canônico e Nome de grupo são atributos obrigatórios.

   O Canonical Name é um identificador exclusivo do grupo. Cada grupo e usuário em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Sistema gerado para permitir que o Gerenciamento de usuários atribua um valor exclusivo, ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome canônico.

   Evite usar caracteres sublinhados (_) em nomes canônicos, por exemplo, `sample_group`. Quando você pesquisa por grupos com base em seu nome canônico, aqueles que contêm caracteres sublinhados não são retornados.

1. Para adicionar usuários e grupos a este novo grupo, clique em Localizar Usuários/Grupos e faça o seguinte:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista Em, selecione Usuários, Grupos ou Usuários e Grupos.
   * Na lista Uso, selecione Nome, Email ou ID de usuário.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos usuários e grupos a serem adicionados a esse novo grupo e clique em OK.

1. Clique em Avançar.
1. Para adicionar este novo grupo a outros grupos existentes, clique em Localizar Grupos e execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos grupos aos quais o novo grupo pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo, clique em Localizar Funções, marque as caixas de seleção de cada função a ser atribuída ao grupo e clique em OK. Os usuários do grupo herdam funções atribuídas no nível do grupo.
1. Clique em Concluir.

## Criar um grupo dinâmico {#create-a-dynamic-group}

Em um grupo dinâmico, você não seleciona individualmente os usuários que pertencem ao grupo. Em vez disso, você especifica um conjunto de regras e todos os usuários que atendem a essas regras são automaticamente adicionados ao grupo dinâmico.

Use uma destas duas maneiras para criar grupos dinâmicos:

* Ative a criação automática de grupos dinâmicos com base em domínios de email, como @adobe.com. Quando você habilita esse recurso, o Gerenciamento de usuários cria um grupo dinâmico para cada domínio de email exclusivo no banco de dados de formulários AEM. Use uma expressão cron para especificar a frequência com que o Gerenciamento de usuários pesquisa o banco de dados de formulários AEM para novos domínios de email. Esses grupos dinâmicos são adicionados ao domínio local DefaultDom e são nomeados como &quot;Todos os usuários com um *`[email domain]`* ID de email.&quot;
* Crie um grupo dinâmico com base em critérios especificados, incluindo o domínio de email do usuário, a descrição, o nome canônico e o nome de domínio. Para pertencer ao grupo dinâmico, o usuário deve atender a todos os critérios especificados. Para configurar uma condição &quot;ou&quot;, crie dois grupos dinâmicos separados e adicione-os a um grupo local. Por exemplo, use essa abordagem para criar um grupo de usuários que pertençam ao domínio de email @adobe.com ou cujo nome canônico contenha ou=adobe.com. No entanto, os utilizadores não têm necessariamente de cumprir ambas as condições.

Um grupo dinâmico contém somente usuários. Ele não pode conter outros grupos. No entanto, um grupo dinâmico pode pertencer a um grupo pai.

### Criar grupos dinâmicos automaticamente com base em domínios de email {#automatically-create-dynamic-groups-based-on-email-domains}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Criação automática de grupo dinâmico, marque a caixa de seleção .
1. Especifique quando o Gerenciador de usuários verifica novos domínios de email. Esse tempo deve ser após o tempo de sincronização do domínio, pois a criação de grupos dinâmicos é lógica somente se a sincronização do domínio estiver concluída.

   * Para ativar a sincronização automática diariamente, digite a hora no formato de 24 horas na caixa Ocorrências diárias em . Ao salvar suas configurações, esse valor é convertido em uma expressão cron, exibida na caixa abaixo.
   * Para agendar a sincronização em um dia específico da semana ou mês, ou em um mês específico, selecione digite a expressão cron apropriada na caixa . O valor padrão é `0 00 4 ? * *`(o que significa verificar às 4 horas todos os dias).

      O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

1. Clique em Salvar.

### Criar um grupo dinâmico com base em critérios especificados {#create-a-dynamic-group-based-on-specified-criteria}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Clique em Novo grupo dinâmico.
1. Complete a seção Configurações gerais . Nome do grupo é um atributo obrigatório. Você pode atribuir o grupo a qualquer domínio configurado.
1. Em Critérios do grupo dinâmico, especifique um ou mais atributos usados para preencher o grupo dinâmico.

   >[!NOTE]
   >
   >Os atributos Email, Description e Canonical Name fazem distinção entre maiúsculas e minúsculas ao usar o operador Igual. Eles não fazem distinção entre maiúsculas e minúsculas com os operadores Começa com, Termina com ou Contém .

   **Email:** O domínio de email do usuário, como `@adobe.com`.

   **Descrição:** Descrição do usuário, como &quot;Cientista da computação&quot;

   **Nome Canônico:** O nome canônico do usuário, como `ou=adobe.com`

   **Nome do domínio:** O nome do domínio ao qual o usuário pertence, como `DefaultDom`. O atributo Nome de domínio faz distinção entre maiúsculas e minúsculas ao usar o operador Contém . Não diferencia maiúsculas de minúsculas com os operadores Starts With, End With ou Equals .

1. Clique em Testar. Uma página de teste exibe os 200 primeiros usuários que atendem aos critérios definidos. Clique em Fechar.
1. Se o teste retornou os resultados esperados, clique em Avançar. Caso contrário, edite os critérios do grupo dinâmico e teste novamente.
1. Para adicionar o grupo dinâmico a um grupo pai, clique em Localizar grupos e execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, marque as caixas de seleção dos grupos aos quais o grupo dinâmico pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo dinâmico, clique em Localizar Funções, marque as caixas de seleção de cada função a ser atribuída ao grupo e clique em OK. Os usuários do grupo herdam funções atribuídas no nível do grupo.
1. Clique em Concluir.

## Exibir detalhes sobre um grupo {#view-details-about-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista Em, selecione Grupo e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do grupo para exibir detalhes. A página Detalhes do grupo é exibida.
1. Para exibir membros diretos do grupo, clique em Principais Secundários.

## Editar um grupo {#edit-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Para localizar o grupo a ser editado, faça o seguinte:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista Uso, selecione Nome ou Email.
   * Na lista Em, selecione Grupos.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Localizar.
   * Nos resultados da pesquisa, clique no nome do grupo a ser editado.

1. Na guia Details , edite as configurações gerais e clique em Save .
1. Para editar os grupos associados, clique na guia Grupos principais e execute estas tarefas:

   * Para localizar grupos para adicionar à associação, clique em Localizar Grupos e preencha as informações de pesquisa.
   * Para adicionar grupos, marque a caixa de seleção dos grupos a serem adicionados, clique em OK e em Salvar.
   * Para excluir um grupo associado, marque a caixa de seleção do grupo a ser excluído, clique em Excluir, em OK e em Salvar.

1. Para editar os usuários e grupos no grupo, clique na guia Principais Filho e faça o seguinte:

   * Para localizar usuários e grupos a serem adicionados, clique em Localizar usuários/grupos e preencha as informações de pesquisa.
   * Para adicionar um usuário ou grupo, marque a caixa de seleção do usuário ou grupo, clique em OK e em Salvar.
   * Para excluir um usuário ou grupo, marque a caixa de seleção do usuário ou grupo, clique em Excluir, clique em OK e em Salvar.

1. Para editar atribuições de função, clique na guia Atribuições de função e faça o seguinte:

   * Para localizar funções a serem atribuídas ao grupo, clique em Localizar Funções.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em OK e em Salvar.
   * Para cancelar a atribuição de uma função, marque a caixa de seleção da função, clique em Cancelar atribuição e em Salvar.

## Excluir um grupo {#delete-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista Localizar, selecione Grupos e clique em Localizar.
1. Marque a caixa de seleção do grupo a ser excluído, clique em Excluir e em OK.
