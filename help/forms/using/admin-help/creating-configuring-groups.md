---
title: Criação e configuração de grupos
description: Saiba como criar grupos manual ou dinamicamente, editar um grupo, exibir detalhes sobre um grupo ou excluir um grupo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 72edd8d1-8573-4942-8ced-1a100af58d78
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 872e2de411f51b5f0b26a2ff47cb49f01313d39f
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Criação e configuração de grupos{#creating-and-configuring-groups}

A criação de grupos de usuários permite atribuir funções ao grupo em vez de a usuários individuais.

Dois tipos diferentes de grupos estão disponíveis. Você pode criar um grupo manualmente e adicionar usuários e outros grupos a ele. Você também pode criar grupos dinâmicos que incluam automaticamente todos os usuários que atendam a um conjunto específico de regras.

Os usuários podem enfrentar um tempo de resposta mais lento se pertencerem a muitos grupos (por exemplo, 500 ou mais) ou se os grupos estiverem aninhados profundamente (por exemplo, 30 níveis). Se você estiver com esse problema, poderá configurar formulários AEM para pré-buscar informações de determinados domínios. (Consulte [Configurar formulários AEM para buscar previamente informações de domínio](/help/forms/using/admin-help/configure-aem-forms-prefetch-domain.md#configure-aem-forms-to-prefetch-domain-information).)

## Criar um grupo manualmente {#create-a-group-manually}

Ao criar um grupo manualmente, você pode adicionar usuários e outros grupos a ele e atribuir funções ao grupo. Você também pode associar o grupo a um grupo principal.

Se você estiver usando o Content Services (Obsoleto), poderá selecionar a opção Selecionar esta opção para enviar usuários e grupos para provedores de armazenamento principal externos registrados na página Gerenciamento de domínio para enviar as informações para quaisquer novos usuários ou grupos criados no Content Services (Obsoleto).

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos e, em seguida, clique em Novo grupo.
1. Complete a seção Configurações gerais e clique em Avançar. O Nome canônico e o Nome do grupo são atributos obrigatórios.

   O Nome canônico é um identificador exclusivo do grupo. Cada grupo e usuário em um domínio deve ter um nome canônico exclusivo. Marque a caixa de seleção Gerado pelo Sistema para permitir que o Gerenciamento de Usuários atribua um valor exclusivo ou desmarque a caixa de seleção e especifique um valor personalizado para o Nome Canônico.

   Evite usar caracteres de sublinhado (_) em nomes canônicos, por exemplo, `sample_group`. Quando você pesquisa por grupos com base em seus nomes canônicos, os que contêm caracteres sublinhados não são retornados.

1. Para adicionar usuários e grupos a esse novo grupo, clique em Localizar usuários/grupos e execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista Em, selecione Usuários, Grupos ou Usuários e Grupos.
   * Na lista Usando, selecione Nome, Email ou ID de usuário.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Find.
   * Nos resultados da pesquisa, marque as caixas de seleção dos usuários e grupos a serem adicionados a este novo grupo e clique em OK.

1. Clique em Avançar.
1. Para adicionar este novo grupo a outros grupos existentes, clique em Localizar grupos e execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Find.
   * Nos resultados da pesquisa, marque as caixas de seleção dos grupos aos quais o novo grupo pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo, clique em Localizar Funções, marque as caixas de seleção para cada função a ser atribuída ao grupo e clique em OK. Os usuários no grupo herdam funções atribuídas no nível do grupo.
1. Clique em Finish.

## Criar um grupo dinâmico {#create-a-dynamic-group}

Em um grupo dinâmico, você não seleciona individualmente os usuários que pertencem ao grupo. Em vez disso, você especifica um conjunto de regras e todos os usuários que atendem a essas regras são automaticamente adicionados ao grupo dinâmico.

Use uma destas duas maneiras para criar grupos dinâmicos:

* Ative a criação automática de grupos dinâmicos com base em domínios de email, como @adobe.com. Quando você habilita esse recurso, o Gerenciamento de usuários cria um grupo dinâmico para cada domínio de email exclusivo no banco de dados de formulários AEM. Use uma expressão cron para especificar a frequência com que o Gerenciamento de usuários pesquisa novos domínios de email no banco de dados de formulários AEM. Esses grupos dinâmicos são adicionados ao domínio local DefaultDom e são nomeados como &quot;Todos os usuários com um *`[email domain]`* ID do e-mail.&quot;
* Crie um grupo dinâmico com base em critérios especificados, incluindo o domínio de email, a descrição, o nome canônico e o nome de domínio do usuário. Para pertencer ao grupo dinâmico, um usuário deve atender a todos os critérios especificados. Para configurar uma condição &quot;ou&quot;, crie dois grupos dinâmicos separados e adicione-os a um grupo local. Por exemplo, use essa abordagem para criar um grupo de usuários que pertencem ao domínio de email @adobe.com ou cujo nome canônico contém ou=adobe.com. No entanto, os usuários não precisam necessariamente atender a ambas as condições.

Um grupo dinâmico contém apenas usuários. Ela não pode conter outros grupos. No entanto, um grupo dinâmico pode pertencer a um grupo principal.

### Criar automaticamente grupos dinâmicos com base em domínios de email {#automatically-create-dynamic-groups-based-on-email-domains}

1. Clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Criação automática de grupo dinâmico, marque a caixa de seleção.
1. Especifique quando o Gerenciador de usuários verificará se há novos domínios de email. Esse horário deve ser posterior ao horário de sincronização do domínio, pois a criação de grupos dinâmicos é lógica somente se a sincronização do domínio for concluída.

   * Para habilitar a sincronização automática diariamente, digite a hora no formato de 24 horas na caixa Ocorre diariamente em. Quando você salva as configurações, esse valor é convertido em uma expressão cron, que é exibida na caixa abaixo.
   * Para agendar a sincronização em um dia específico da semana ou mês, ou em um mês específico, selecione digite a expressão cron apropriada na caixa. O valor padrão é `0 00 4 ? * *`(o que significa verificar às 4 da manhã todos os dias).

     O uso da expressão cron é baseado no sistema de agendamento de tarefas de código aberto Quartz, versão 1.4.0.

1. Clique em Salvar.

### Criar um grupo dinâmico com base em critérios especificados {#create-a-dynamic-group-based-on-specified-criteria}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Clique em Novo grupo dinâmico.
1. Complete a seção Configurações gerais. Nome do Grupo é um atributo obrigatório. Você pode atribuir o grupo a qualquer domínio configurado.
1. Em Critérios do grupo dinâmico, especifique um ou mais atributos usados para preencher o grupo dinâmico.

   >[!NOTE]
   >
   >Os atributos Email, Description e Canonical Name fazem distinção entre maiúsculas e minúsculas ao usar o operador Equals. Eles não fazem distinção entre maiúsculas e minúsculas com os operadores Começa com, Termina com ou Contém.

   **Email:** Domínio de email do usuário, como `@adobe.com`.

   **Descrição:** Descrição do usuário, como &quot;Cientista de computação&quot;

   **Nome canônico:** Nome canônico do usuário, como `ou=adobe.com`

   **Nome do domínio:** O nome do domínio ao qual o usuário pertence, como `DefaultDom`. O atributo Nome de domínio diferencia maiúsculas de minúsculas ao usar o operador Contém. Não diferencia maiúsculas de minúsculas com os operadores Começa com, Termina com ou É igual a.

1. Clique em Test (Testar). Uma página de Teste exibe os primeiros 200 usuários que atendem aos critérios definidos. Clique em Fechar.
1. Se o teste retornou os resultados esperados, clique em Next. Caso contrário, edite os critérios do grupo dinâmico e teste novamente.
1. Para adicionar o grupo dinâmico a um grupo pai, clique em Localizar grupos e execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Find.
   * Nos resultados da pesquisa, marque as caixas de seleção para os grupos aos quais o grupo dinâmico pertence e clique em OK.

1. Clique em Avançar.
1. Para atribuir funções ao grupo dinâmico, clique em Localizar funções, marque as caixas de seleção para cada função a ser atribuída ao grupo e clique em OK. Os usuários no grupo herdam funções atribuídas no nível do grupo.
1. Clique em Finish.

## Exibir detalhes sobre um grupo {#view-details-about-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista Em, selecione Grupo e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Clique no nome do grupo para exibir detalhes sobre. A página Detalhes do grupo é exibida.
1. Para exibir membros diretos do grupo, clique em Principais Filhos.

## Editar um grupo {#edit-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Para localizar o grupo a ser editado, execute estas tarefas:

   * Na caixa Localizar, digite os critérios de pesquisa.
   * Na lista Utilizando, selecione Nome ou Email.
   * Na lista Em, selecione Grupos.
   * Selecione o domínio, selecione o número de itens a serem exibidos e clique em Find.
   * Nos resultados da pesquisa, clique no nome do grupo a ser editado.

1. Na guia Detalhes, edite as configurações gerais e clique em Salvar.
1. Para editar os grupos associados, clique na guia Grupos Pai e execute estas tarefas:

   * Para localizar grupos a serem adicionados à associação, clique em Localizar Grupos e preencha as informações de pesquisa.
   * Para adicionar grupos, marque a caixa de seleção dos grupos a serem adicionados, clique em OK e em Salvar.
   * Para excluir um grupo associado, marque a caixa de seleção do grupo a ser excluído, clique em Excluir, clique em OK e, em seguida, clique em Salvar.

1. Para editar os usuários e grupos no grupo, clique na guia Principais Filhos e execute estas tarefas:

   * Para localizar usuários e grupos a serem adicionados, clique em Localizar usuários/grupos e preencha as informações de pesquisa.
   * Para adicionar um usuário ou grupo, marque a caixa de seleção referente ao usuário ou grupo, clique em OK e, em seguida, em Salvar.
   * Para excluir um usuário ou grupo, marque a caixa de seleção referente ao usuário ou grupo, clique em Excluir, clique em OK e, em seguida, clique em Salvar.

1. Para editar atribuições de função, clique na guia Atribuições de função e execute estas tarefas:

   * Para localizar funções a serem atribuídas ao grupo, clique em Localizar Funções.
   * Para adicionar uma função, marque a caixa de seleção da função, clique em OK e, em seguida, clique em Salvar.
   * Para desatribuir uma função, marque a caixa de seleção da função, clique em Desatribuir e, em seguida, clique em Salvar.

## Excluir um grupo {#delete-a-group}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Na lista Localizar, selecione Grupos e clique em Localizar.
1. Marque a caixa de seleção do grupo a ser excluído, clique em Excluir e em OK.
