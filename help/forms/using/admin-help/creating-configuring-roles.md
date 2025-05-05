---
title: Criação e configuração de funções
description: Saiba como associar usuários e grupos a funções que já fazem parte do banco de dados de Gerenciamento de usuários. Também é possível criar, editar e excluir funções.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '2495'
ht-degree: 0%

---

# Criação e configuração de funções{#creating-and-configuring-roles}

Usando as páginas da Web de Gerenciamento de usuários, você pode associar usuários e grupos a funções que já fazem parte do banco de dados de Gerenciamento de usuários. Também é possível criar, editar e excluir funções.

O Gerenciamento de usuários tem dois tipos de funções:

**Funções mutáveis:** esse tipo de função pode ser editado e excluído, e permissões de função podem ser adicionadas e excluídas desses tipos de função. Qualquer função criada é considerada uma função mutável. Você pode adicionar ou remover usuários e grupos atribuídos a funções mutáveis.

**Funções imutáveis:** as funções padrão incluídas no Gerenciamento de Usuários são funções imutáveis. Essas funções não podem ser editadas ou excluídas. No entanto, você pode adicionar ou remover usuários e grupos atribuídos a funções imutáveis.

As funções mutáveis e imutáveis também podem ser criadas por meio das APIs de formulários AEM.

## Funções padrão {#default-roles}

As funções padrão a seguir estão incluídas no banco de dados de Gerenciamento de usuários.

**Usuário do console de administração:** Pode acessar o console de administração.

**Administrador do Aplicativo:** Pode usar todos os recursos do Workbench. Você pode usar as páginas Aplicativos e Serviços no console de administração para configurar propriedades, pontos de extremidade e segurança do tempo de execução do serviço.

**Administrador de formulários AEM:** pode executar todas as tarefas para todos os serviços instalados.

**Administrador de Segurança:** controla as configurações de Gerenciamento de Usuários e gerencia usuários e grupos associados a qualquer domínio do Gerenciador de Usuários

**Usuário de Serviços:** Pode exibir e invocar qualquer serviço

**Superadministrador:** tem acesso a todas as funcionalidades administrativas do sistema, incluindo serviços

**Administrador de Confiança:** pode gerenciar as configurações de confiança PKI e as credenciais PKI gerenciadas na página Gerenciamento de Repositório de Confiança no console de administração

### Funções padrão adicionais {#additional-default-roles}

As seguintes funções padrão adicionais podem ser incluídas, dependendo dos componentes de formulários AEM instalados por você

**Usuário do Aplicativo de Carregamento de Documentos:** Pode carregar documentos usando o Flex Remoting.

**Administrador do Forms:** pode exibir e modificar configurações na página Forms no Console de Administração

**Administrador do Contentspace do Forms AEM:** pode exibir e modificar configurações da página Serviços de Conteúdo (obsoleto) no console de administração

**Usuário do Contentspace dos formulários AEM:** Pode fazer logon nas páginas da Web do Contentspace (Obsoleto)

**Administrador do Documentum Connector:** pode visualizar e modificar configurações a partir da página Connector for EMC Documentum no console de administração

**Administrador do Conector FileNet dos formulários AEM:** pode exibir e modificar configurações do Conector para IBM FileNet na página de console de administração

**Administrador do IBM CM Connector do AEM Forms:** pode exibir e modificar configurações no Conector da página Gerenciador de conteúdo do IBM no console de administração

**Administrador de Rights Management:** Executa todas as tarefas necessárias para todas as configurações de servidor nas páginas de Rights Management relevantes

**Usuário final do Rights Management:** pode acessar páginas da Web do usuário final do Rights Management

**Rights Management Convidar Usuário:** Pode convidar usuários

Rights Management **Gerenciar Usuários Convidados e Locais:** Pode executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas de Rights Management relevantes

**Administrador de Conjunto de Políticas de Rights Management:** Executa todas as tarefas necessárias para todos os conjuntos de políticas nas páginas de Rights Management relevantes

**Superadministrador de Rights Management:** Executa todas as tarefas necessárias da página de Rights Management

**Administrador do AEM Forms Workspace:** pode exibir e modificar configurações na página Workspace no Console de Administração

***observação &#x200B;**: o Flex Workspace foi descontinuado para a versão de formulários AEM.*

**Usuário do Workspace:** pode fazer logon no aplicativo de usuário final do Workspace

**Administrador de Saída:** pode exibir e modificar configurações na página Saída do Console de Administração

**Administrador do PDFG:** pode exibir e modificar configurações na página PDF Generator no console de administração

**Usuário PDFG:** pode acessar todas as funcionalidades não administrativas do PDF Generator

**Aplicativo Web de extensões do Acrobat Reader DC:** Pode usar o aplicativo Web de extensões do Acrobat Reader DC

>[!NOTE]
>
>Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas podem existir fora de um firewall, a permissão de tarefas no nível da administração pode representar um risco de segurança. Somente os usuários que têm os privilégios de Administrador do Workspace para formulários AEM ou de Usuário do Workspace para formulários AEM podem acessar as páginas da Web do usuário final do Workspace.

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

## Criar uma função {#create-a-role}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Na caixa Nome da função, digite um nome para a função e, opcionalmente, digite uma descrição da função e, em seguida, clique em Avançar.

   >[!NOTE]
   >
   >Ao usar o MySQL, você não pode criar duas funções que tenham o mesmo nome, mas sejam diferentes no uso de caracteres estendidos. Por exemplo, tentar criar uma função chamada abcde quando uma chamada âbcdè já existe resulta em um erro.

1. Clique em Localizar permissões e selecione as permissões a serem adicionadas à função.
1. Clique em OK e depois em Next.
1. Atribuir esta função a usuários e grupos:

   * Clique em Localizar usuários/grupos.
   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione Nome, Email ou ID de usuário e, em seguida, selecione Usuários, Grupos ou Usuários e Grupos.
   * Selecione o domínio, selecione o número de resultados a serem exibidos e clique em Find.
   * Marque as caixas de seleção dos usuários e grupos aos quais atribuir esta função e clique em OK.

1. Para exibir detalhes do usuário e do grupo, selecione a entidade.
1. Clique em OK e em Finish.

## Editar uma função {#edit-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Atribuições exibe todas as atribuições no banco de dados de Gerenciamento de Usuários. Se a lista de atribuições for grande, use a área Localizar na parte superior da página para procurar um nome de atribuição específico.

1. Clique na função para editar, editar as configurações gerais e clique em Salvar.
1. Para editar permissões de função, clique na guia Permissões e execute estas tarefas:

   * Para adicionar novas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões a serem adicionadas, clique em OK e, em seguida, clique em Salvar.
   * Para excluir uma permissão da função, marque a caixa de seleção da permissão, clique em Excluir e, em seguida, clique em Salvar.

1. Para gerenciar a quem a função é atribuída, clique na guia Usuários da função e execute estas tarefas:

   * Para atribuir a função a novos usuários e grupos, clique em Localizar usuários/grupos e preencha as informações de pesquisa. Marque a caixa de seleção para cada usuário e grupo ao qual atribuir esta função, clique em OK e em Salvar.
   * Para remover a função, marque a caixa de seleção dos usuários ou grupo, clique em Cancelar atribuição e em Salvar.

## Excluir uma função {#delete-a-role}

É possível excluir qualquer uma das funções que você criou, mas não as funções de formulários AEM padrão incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Atribuições exibe todas as atribuições no banco de dados de Gerenciamento de Usuários. Se a lista de atribuições for grande, use a área Localizar na parte superior da página para procurar um nome de atribuição específico.

1. Marque a caixa de seleção da função a ser excluída, clique em Excluir e, em seguida, em OK.

## Atribuir uma função a usuários e grupos {#assign-a-role-to-users-and-groups}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique informações para restringir a pesquisa e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Marque as caixas de seleção ao lado dos usuários e grupos a serem associados a uma função e clique em Atribuir função.
1. Selecione a função a ser atribuída ao usuário ou grupo e clique em OK.

Você também pode atribuir funções usando a página Gerenciamento de funções.

## Determinar quem está atribuído a uma função {#determine-who-is-assigned-to-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Atribuições exibe todas as atribuições no banco de dados de Gerenciamento de Usuários. Se a lista de atribuições for grande, use a área Localizar na parte superior da página para procurar um nome de atribuição específico.

1. Na página Detalhes da função, clique na guia Usuários da função. Uma lista de usuários e grupos que estão diretamente associados à função é exibida.

## Alterar permissões de função {#change-role-permissions}

É possível alterar as permissões de qualquer uma das funções criadas. Não é possível alterar as permissões para as funções de formulários AEM padrão incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Atribuições exibe todas as atribuições no banco de dados de Gerenciamento de Usuários. Se a lista de atribuições for grande, use a área Localizar na parte superior da página para procurar um nome de atribuição específico.

1. Selecione a função para a qual exibir permissões e clique na guia Permissões.
1. Para alterar essas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões a serem adicionadas à função, clique em OK e, em seguida, clique em Salvar.
1. Para excluir uma permissão, selecione-a, clique em Excluir e em Salvar.

### Permissões de formulários AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Adicionar, remover e modificar pontos de extremidade para um serviço

**Logon de Admin Console:** Exibir o console de administração

**Modificação de Certificado:** Modifique as configurações de confiança de qualquer certificado no Repositório de Confiança

**Leitura de Certificado:** Leia qualquer certificado no Repositório Confiável

**Gravação de Certificado:** Adicione um certificado ao Repositório Confiável

**Adição de Componente:** Instale um novo componente no sistema

**Exclusão de Componente:** Exclua qualquer componente do sistema

**Leitura de Componente:** Leia qualquer componente no sistema

**Administrador do Contentspace:** Permissão para Administrador do Contentspace (Obsoleto)

**Logon do Console Contentspace:** Permissão para Logon do Console Contentspace (Obsoleto)

**Controle das Configurações Principais:** Gerencie as configurações na página Configurações Principais do Sistema no Console de Administração

**CREATE_VERSION_PERM:** criar uma versão de um serviço

**Modificação de Credencial:** Modifique qualquer credencial de assinatura no Repositório de Confiança

**Leitura de Credencial:** Leia qualquer credencial de assinatura no Repositório de Confiança

**Gravação de Credencial:** Adicione uma credencial de assinatura ao Repositório de Confiança

**Modificação de CRL:** Modifique qualquer CRL (Lista de Revogação de Certificado) no Repositório de Confiança

**Leitura da CRL:** Leia qualquer CRL no Armazenamento de Confiança

**Gravação de CRL:** Adicione uma CRL ao Repositório de Confiança

**Delegar:** Defina uma ACL em um recurso

**DELETE_VERSION_PERM:** Excluir uma versão de um serviço

**Carregamento de Documentos:** Carregar documentos em formulários AEM

**Controle de Domínio:** crie, exclua ou modifique configurações para qualquer domínio de Gerenciamento de Usuários, incluindo seus provedores de autenticação e diretório

**Editar Tipo de Evento:** Editar tipos de evento

**Controle de Representação de Identidade:** Representar identidade no Gerenciador de Usuários

**INVOKE_PERM:** Chame todas as operações em um serviço

**Controle de Modelo de Dados LCDS:** Ler e implantar modelos de dados no Data Services

**Atualização do License Manager:** Atualizar informações de licença

**MODIFY_CONFIG_PERM:** Modificar a configuração de um serviço

**TERM** Modificar a versão de um serviço

**PDFGAdminPermission:** administrador PDFG

**PDFGUserPermission:** usuário PDFG

**PERM_DCTM_ADMIN:** administrador do Documentum Connector

**PERM_FILENET_ADMIN:** administrador do FileNet Connector

**PERM_FORMS_ADMIN:** administrador do Forms

**PERM_IBMCM_ADMIN:** Administrador do IBM CM Connector

**PERM_OUTPUT_ADMIN:** Administrador de saída

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Use o aplicativo Web de extensões do Acrobat Reader DC

**PERM_SP_ADMIN:** Gerenciar configurações do Conector do SharePoint

**PERM_WORKSPACE_ADMIN:** Gerenciar configurações do Workspace

**PERM_WORKSPACE_USER:** Faça logon no aplicativo de usuário final do Workspace

**Controle da Entidade de Segurança:** Gerencie usuários e grupos para qualquer domínio e gerencie atribuições de função para todos os usuários e grupos em qualquer domínio

**Leitura/Exclusão da Gravação do Processo:** Listar e recuperar instâncias de auditoria do fluxo de trabalho

**PROCESS_OWNER_PERM:** Exiba dados de tendência e execute ações administrativas em um serviço criado a partir de um processo

**Leitura:** Ler o conteúdo de um recurso

**READ_PERM:** Ler ou exibir um serviço

**Renovar asserção:** Renovar asserções no Gerenciamento de Usuários

**Delegado do repositório:** Defina uma ACL em um recurso

**Leitura do Repositório:** Ler o conteúdo de um recurso

**Travessia de Repositório:** Inclua um recurso em uma solicitação de recursos de lista ou leia os metadados de um recurso

**Gravação do Repositório:** Gravar metadados e conteúdo do repositório

**Proprietário da Política de Alteração de Rights Management:** Proprietário da política de alteração

**Logon do Console do Usuário Final do Rights Management:** Logon na Interface do Usuário Final do Rights Management

**Configuração de Gerenciamento de Rights Management:** Gerenciar configuração do servidor

Rights Management **Gerenciar Usuários Convidados e Locais:** Gerenciar usuários convidados e locais

**Gerenciar Conjuntos de Políticas do Rights Management:** Gerenciar todas as políticas e documentos em qualquer conjunto de políticas

**Adicionar coordenador do conjunto de políticas do Rights Management:** Adicionar, remover e alterar permissões para coordenadores do conjunto de políticas

**Criar política de conjunto de políticas do Rights Management:** Criar uma política para um conjunto de políticas

**Política de Exclusão do Conjunto de Políticas Rights Management:** Remova uma política de um conjunto de políticas

**Editar Política de Conjunto de Políticas Rights Management:** Editar uma política em um conjunto de políticas

**Conjunto de Políticas do Rights Management Gerenciar Editor de Documentos:** Ao criar conjuntos de políticas, atribua aos usuários a função de editor de documentos. O editor do documento é o usuário que protege o documento com uma política.

**Coordenador de Remoção do Conjunto de Políticas do Rights Management:** Remova um coordenador de conjunto de políticas de um conjunto de políticas

**Revogar documento de conjunto de políticas do Rights Management:** Revogar acesso a documentos em um conjunto de políticas

**Política de Rights Management Defina a Política de Alternância:** políticas de alternância para um documento

**Documento de Cancelamento de Revogação de Definição de Política de Rights Management:** Cancele a Revogação de um documento

**Evento de Exibição do Conjunto de Políticas do Rights Management:** Exiba eventos de política e documento para qualquer política ou documento em um conjunto de políticas

**Eventos de Servidor de Exibição do Rights Management:** Pesquise e exiba todos os eventos de auditoria

**Controle de Função:** Criar, excluir e modificar funções no Gerenciamento de Usuários

**Ativação de Serviço:** Inicie qualquer serviço, disponibilizando-o para invocação

**Adição de Serviço:** Implante um novo serviço no Registro de serviço. Isso inclui a adição de novos processos e variantes de processos

**Desativação de Serviço:** Para qualquer serviço no sistema

**Exclusão de Serviço:** Exclua qualquer serviço no sistema, incluindo processos e variantes de processos

**Chamada de Serviço:** Chame qualquer serviço no Registro de serviço disponível em tempo de execução

**Modificação de Serviço:** Modifique as propriedades de configuração de qualquer serviço no sistema. Isso inclui bloquear e desbloquear um serviço no IDE e adicionar ou remover pontos finais de um serviço

**Leitura de Serviço:** Leia todos os serviços no sistema. Isso inclui todos os processos e variantes de processos

**SERVICE_AGENT_PERM:** Exiba dados e interaja com instâncias do processo para um serviço criado a partir de um processo

**SERVICE_MANAGER_PERM:** Execute o balanceamento de carga e outras ações administrativas em um serviço criado a partir de um processo

**START_STOP_PERM:** Iniciar ou parar um serviço

**SUPERVISOR_PERM:** Exibir dados de instância de processo para um serviço criado a partir de um processo

**Percorrer:** Incluir um recurso em uma solicitação de recursos de lista ou ler os metadados de um recurso

**Gravar:** Gravar metadados e conteúdo do repositório

**Abrindo arquivos no Workbench**

Para exibir o conteúdo da visualização Recursos no Workbench e abrir arquivos para visualização, um usuário precisa das seguintes permissões:

* Leitura do repositório
* Percurso do repositório
* Chamada de serviço
* Leitura do serviço

## Remover um usuário ou grupo de uma função {#remove-a-user-or-group-from-a-role}

Use a página Gerenciamento de Atribuições para remover usuários e grupos de uma atribuição específica. Se o usuário ou grupo tiver herdado a atribuição de função, não será possível remover a função no nível do usuário ou grupo. Remova o usuário ou grupo da árvore de herança ou remova a função do pai.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Atribuições exibe todas as atribuições no banco de dados de Gerenciamento de Usuários. Se a lista de atribuições for grande, use a área Localizar na parte superior da página para procurar um nome de atribuição específico.

1. Na lista de funções, clique no nome da função a ser atualizada e, em seguida, clique na guia Usuários da função. Uma lista de usuários e grupos associados à função é exibida.
1. Marque as caixas de seleção dos usuários e grupos a serem removidos da função e clique em Cancelar atribuição.
1. Clique em Salvar e em OK.
