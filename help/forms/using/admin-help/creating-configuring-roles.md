---
title: Criação e configuração de funções
seo-title: Creating and configuring roles
description: Saiba como associar usuários e grupos a funções que já fazem parte do banco de dados de Gerenciamento de usuários. Também é possível criar, editar e excluir funções.
seo-description: Learn how to associate users and groups with roles that are already part of the User Management database. You can also create, edit, and delete roles.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
exl-id: b447e545-f73e-4fde-a001-86e0e1cf4a12
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 0%

---

# Criação e configuração de funções{#creating-and-configuring-roles}

Usando as páginas da Web de Gerenciamento de usuários, você pode associar usuários e grupos a funções que já fazem parte do banco de dados de Gerenciamento de usuários. Também é possível criar, editar e excluir funções.

O Gerenciamento de usuários tem dois tipos de funções:

**Funções mutáveis:** Esse tipo de função pode ser editado e excluído, e permissões de função podem ser adicionadas e excluídas desses tipos de função. Qualquer função criada é considerada uma função mutável. Você pode adicionar ou remover usuários e grupos atribuídos a funções mutáveis.

**Funções imutáveis:** As funções padrão incluídas no Gerenciamento de usuários são funções imutáveis. Essas funções não podem ser editadas ou excluídas. No entanto, você pode adicionar ou remover usuários e grupos atribuídos a funções imutáveis.

As funções mutáveis e imutáveis também podem ser criadas por meio das APIs de formulários AEM.

## Funções padrão {#default-roles}

As funções padrão a seguir estão incluídas no banco de dados de Gerenciamento de usuários.

**Admin Console Usuário:** Pode acessar o console de administração.

**Administrador do aplicativo:** Pode usar todos os recursos do Workbench. Você pode usar as páginas Aplicativos e Serviços no console de administração para configurar propriedades, pontos de extremidade e segurança do tempo de execução do serviço.

**Administrador do AEM Forms:** Pode executar todas as tarefas de todos os serviços instalados.

**Administrador de segurança:** Controla as configurações de Gerenciamento de usuários e gerencia usuários e grupos associados a qualquer domínio do Gerenciador de usuários

**Usuário de serviços:** Pode exibir e chamar qualquer serviço

**Superadministrador:** Tem acesso a todas as funcionalidades administrativas do sistema, incluindo serviços

**Administrador de Confiança:** É possível gerenciar as configurações de confiança de PKI e as credenciais de PKI gerenciadas na página Gerenciamento de Armazenamento Confiável no console de administração

### Funções padrão adicionais {#additional-default-roles}

As seguintes funções padrão adicionais podem ser incluídas, dependendo dos componentes de formulários AEM instalados por você

**Usuário do aplicativo de carregamento de documento:** Pode carregar documentos usando o Flex Remoting.

**Administrador do Forms:** Pode exibir e modificar configurações na página Forms no Console de administração

**Administrador do Contentspace do AEM Forms:** Pode exibir e modificar configurações na página Serviços de conteúdo (obsoleto) no console de administração

**AEM forma Contentspace Usuário:** Pode fazer logon nas páginas da Web Contentspace (Obsoleto)

**Administrador do Documentum Connector:** Pode exibir e modificar configurações na página Connector for EMC Documentum no console de administração

**Administrador do Conector FileNet dos formulários AEM:** Pode exibir e modificar configurações na página Connector for IBM FileNet no console de administração

**O AEM forma o Administrador do IBM CM Connector:** Pode exibir e modificar configurações no Conector da página Gerenciador de conteúdo do IBM no console de administração

**Administrador de Rights Management:** Executa todas as tarefas necessárias para todas as configurações de servidor nas páginas de Rights Management relevantes

**Usuário final do Rights Management:** Pode acessar páginas da Web do usuário final do Rights Management

**Rights Management Convidar Usuário:** Pode convidar usuários

**Rights Management Gerenciar usuários convidados e locais:** Pode executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas de Rights Management relevantes

**Administrador de Definição de Política Rights Management:** Executa todas as tarefas necessárias para todos os conjuntos de políticas nas páginas de Rights Management relevantes

**Superadministrador de Rights Management:** Executa todas as tarefas necessárias da página de Rights Management

**Administrador do AEM Forms Workspace:** Pode exibir e modificar configurações na página Espaço de trabalho no Console de administração

***observação **: o Flex Workspace está obsoleto para a versão de formulários AEM.*

**Usuário do Workspace:** Pode fazer logon no aplicativo do usuário final do Workspace

**Administrador de saída:** Pode exibir e modificar configurações na página Saída no Console de administração

**Administrador PDFG:** Pode exibir e modificar configurações na página PDF Generator no console de administração

**Usuário PDFG:** Pode acessar todas as funcionalidades não administrativas do PDF Generator

**Aplicativo Web de extensões do Acrobat Reader DC:** Pode usar o aplicativo web de extensões do Acrobat Reader DC

>[!NOTE]
>
>Usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas podem existir fora de um firewall, a permissão de tarefas no nível da administração pode representar um risco de segurança. Somente os usuários que têm os privilégios de Administrador do AEM Forms Workspace ou Usuário do AEM Forms Workspace podem acessar as páginas da Web do usuário final do Workspace.

>[!NOTE]
>
>O espaço de trabalho do Flex está obsoleto para a versão do AEM forms.

## Criar uma função {#create-a-role}

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

**ADD_REMOVE_ENDPOINT_PERM:** Adicionar, remover e modificar endpoints de um serviço

**Login do Admin Console:** Exibir o console de administração

**Modificação do certificado:** Modifique as configurações de confiança de qualquer certificado no Armazenamento de Confiança

**Leitura do certificado:** Ler qualquer certificado no Armazenamento de Confiança

**Gravação do certificado:** Adicionar um certificado ao armazenamento de confiança

**Adição de componente:** Instalar um novo componente no sistema

**Exclusão de componente:** Excluir qualquer componente no sistema

**Leitura do componente:** Leia todos os componentes do sistema

**Administrador do Contentspace:** Permissão para administrador do Contentspace (obsoleto)

**Logon no console Contentspace:** Permissão para logon do console Contentspace (obsoleto)

**Controle de configurações principais:** Gerencie as configurações na página Configurações principais do sistema no Console de administração

**CREATE_VERSION_PERM:** Criar uma nova versão de um serviço

**Modificação de credencial:** Modificar qualquer credencial de assinatura no Armazenamento de Confiança

**Leitura de credencial:** Ler qualquer credencial de assinatura no Armazenamento de Confiança

**Gravação de credencial:** Adicionar uma credencial de assinatura ao Armazenamento de Confiança

**Modificação da CRL:** Modificar qualquer CRL (Lista de Revogação de Certificado) no Armazenamento de Confiança

**Leitura da CRL:** Ler qualquer CRL no Armazenamento de Confiança

**Gravação da CRL:** Adicionar uma CRL ao Armazenamento de Confiança

**Delegar:** Definir uma ACL em um recurso

**DELETE_VERSION_PERM:** Excluir uma versão de um serviço

**Carregamento de documento:** Carregar documentos em formulários AEM

**Controle de domínio:** Criar, excluir ou modificar configurações para qualquer domínio de Gerenciamento de usuários, incluindo seus provedores de autenticação e diretório

**Editar tipo de evento:** Editar em tipos de evento

**Controle de Representação de Identidade:** Representar identidade no Gerenciador de usuários

**INVOKE_PERM:** Executar todas as operações em um serviço

**Controle do modelo de dados LCDS:** Ler e implantar modelos de dados no Data Services

**Atualização do License Manager:** Atualizar informações de licença

**MODIFY_CONFIG_PERM:** Modificar a configuração de um serviço

**TERMO** Modificar a versão de um serviço

**PDFGAdminPermission:** Administrador PDFG

**PDFGUserPermission:** Usuário PDFG

**PERM_DCTM_ADMIN:** Administrador do Documentum Connector

**PERM_FILENET_ADMIN:** Administrador do FileNet Connector

**PERM_FORMS_ADMIN:** administrador do Forms

**PERM_IBMCM_ADMIN:** Administrador do IBM CM Connector

**PERM_OUTPUT_ADMIN:** Administrador de saída

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Usar o aplicativo web de extensões do Acrobat Reader DC

**PERM_SP_ADMIN:** Gerenciar configurações do SharePoint Connector

**PERM_WORKSPACE_ADMIN:** Gerenciar configurações do Workspace

**PERM_WORKSPACE_USER:** Faça logon no aplicativo do usuário final do Workspace

**Controle principal:** Gerencie usuários e grupos para qualquer domínio e gerencie atribuições de funções para todos os usuários e grupos em qualquer domínio

**Leitura/exclusão de gravação de processo:** Listar e recuperar instâncias de auditoria de fluxo de trabalho

**PROCESS_OWNER_PERM:** Exibir dados de tendência e executar ações administrativas em um serviço criado a partir de um processo

**Lido:** Ler o conteúdo de um recurso

**READ_PERM:** Ler ou exibir um serviço

**Renovar asserção:** Renovar asserções no Gerenciamento de usuários

**Delegado do repositório:** Definir uma ACL em um recurso

**Leitura do repositório:** Ler o conteúdo de um recurso

**Percurso do repositório:** Incluir um recurso em uma solicitação de recursos de lista ou ler os metadados de um recurso

**Gravação no repositório:** Gravar metadados e conteúdo do repositório

**Proprietário da Política de Alteração de Rights Management:** Alterar proprietário da política

**Logon no console do usuário final do Rights Management:** Fazer logon na interface do usuário final do Rights Management

**Configuração do gerenciador de Rights Management:** Gerenciar configuração do servidor

**Rights Management Gerenciar usuários convidados e locais:** Gerenciar usuários convidados e locais

**Rights Management Gerenciar Conjuntos de Políticas:** Gerenciar todas as políticas e documentos em qualquer conjunto de políticas

**Coordenador de Adição do Conjunto de Políticas do Rights Management:** Adicionar, remover e alterar permissões para coordenadores de definições de políticas

**Política Rights Management Definir Criar Política:** Criar uma nova política para um conjunto de políticas

**Política Rights Management Definir Política de Exclusão:** Remover uma política de um conjunto de políticas

**Política Rights Management Definir Editar Política:** Editar uma política em um conjunto de políticas

**Política Rights Management Defina Gerenciar Editor de Documentos:** Ao criar conjuntos de políticas, você atribui aos usuários a função de editor de documentos. O editor do documento é o usuário que protege o documento com uma política.

**Coordenador de Remoção do Conjunto de Políticas Rights Management:** Remover um coordenador de conjunto de políticas de um conjunto de políticas

**Documento de Revogação de Definição de Política Rights Management:** Revogar acesso a documentos em um conjunto de políticas

**Política Rights Management Definir Política de Comutação:** Alternar políticas para um documento

**Documento Não Revogado de Definição de Política Rights Management:** Cancelar revogação de um documento

**Evento de Exibição de Definição de Política Rights Management:** Exibir eventos de política e documento para qualquer política ou documento em um conjunto de políticas

**Eventos do Servidor de Exibição do Rights Management:** Pesquisar e exibir todos os eventos de auditoria

**Controle de função:** Criar, excluir e modificar funções no Gerenciamento de usuários

**Ativação do serviço:** Iniciar qualquer serviço, disponibilizando-o para invocação

**Adição de serviço:** Implante um novo serviço no Registro do serviço. Isso inclui a adição de novos processos e variantes de processos

**Desativação do serviço:** Interromper qualquer serviço no sistema

**Exclusão de serviço:** Excluir qualquer serviço no sistema, incluindo processos e variantes de processos

**Chamada de serviço:** Invocar qualquer serviço no registro de serviço disponível no tempo de execução

**Modificação do serviço:** Modifique as propriedades de configuração de qualquer serviço no sistema. Isso inclui bloquear e desbloquear um serviço no IDE e adicionar ou remover pontos finais de um serviço

**Leitura do serviço:** Leia todos os serviços no sistema. Isso inclui todos os processos e variantes de processos

**SERVICE_AGENT_PERM:** Exibir dados e interagir com instâncias de processo para um serviço criado a partir de um processo

**SERVICE_MANAGER_PERM:** Executar balanceamento de carga e outras ações administrativas em um serviço criado a partir de um processo

**START_STOP_PERM:** Iniciar ou parar um serviço

**SUPERVISOR_PERM:** Exibir dados da instância do processo para um serviço criado a partir de um processo

**Percorrer:** Incluir um recurso em uma solicitação de recursos de lista ou ler os metadados de um recurso

**Gravar:** Gravar metadados e conteúdo do repositório

**Abrir arquivos no Workbench**

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
