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
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# Criação e configuração de funções{#creating-and-configuring-roles}

Usando as páginas da Web do Gerenciamento de usuários, é possível associar usuários e grupos a funções que já fazem parte do banco de dados do Gerenciamento de usuários. Também é possível criar, editar e excluir funções.

O Gerenciamento de usuários tem dois tipos de funções:

**Funções mutáveis:** Esse tipo de função pode ser editado e excluído, e as permissões de função podem ser adicionadas e excluídas desses tipos de função. Qualquer função criada é considerada uma função mutável. Você pode adicionar ou remover usuários e grupos atribuídos a funções mutáveis.

**Funções imutáveis:** As funções padrão incluídas no Gerenciamento de usuários são funções imutáveis. Essas funções não podem ser editadas ou excluídas. No entanto, é possível adicionar ou remover usuários e grupos atribuídos a funções imutáveis.

As funções mutáveis e imutáveis também podem ser criadas por meio das APIs de formulários AEM.

## Funções padrão {#default-roles}

As seguintes funções padrão estão incluídas no banco de dados de Gerenciamento de usuários.

**usuário do console de administração:** Pode acessar o console de administração.

**Administrador de aplicativos:** Pode usar todos os recursos do Workbench. Pode usar as páginas Aplicativos e Serviços no console de administração para configurar as propriedades, os pontos de extremidade e a segurança do tempo de execução do serviço.

**Administrador dos AEM forms:** Pode executar todas as tarefas para todos os serviços instalados.

**Administrador de segurança:** Controla as configurações de Gerenciamento de usuários e gerencia usuários e grupos associados a qualquer domínio do Gerenciador de usuários

**Usuário de Serviços:** Pode visualizar e invocar qualquer serviço

**Superadministrador:** Tem acesso a todas as funcionalidades administrativas do sistema, incluindo serviços

**Administrador de Confiança:** Pode gerenciar as configurações de confiança de PKI e as credenciais de PKI gerenciadas a partir da página Gerenciamento de Armazenamento de Confiança no console de administração

### Funções padrão adicionais {#additional-default-roles}

As funções padrão adicionais a seguir podem ser incluídas, dependendo dos componentes de formulários de AEM que você instalou

**Usuário do Aplicativo de Upload de Documento:** É possível carregar documentos usando o Flex Remoting.

**Administrador do Forms:** Pode visualizar e modificar configurações da página Forms no Console de Administração

**Administrador do Contentspace dos formulários AEM:** Pode exibir e modificar configurações da página Serviços de conteúdo (obsoleto) no console de administração

**Usuário do AEM Forms ContentSpace:** Pode fazer logon nas páginas da Web do Contentspace (obsoleto)

**Administrador do Documentum Connector:** Pode visualizar e modificar configurações da página Connector for EMC Documentum no console de administração

**AEM forms FileNet Connector Administrator:** Pode visualizar e modificar configurações da página Conector para IBM FileNet no console de administração

**AEM Forms IBM CM Connector Administrator:** Pode visualizar e modificar configurações da página Conector para IBM Content Manager no console de administração

**Administrador do Rights Management:** Executa todas as tarefas necessárias para todas as configurações do servidor nas páginas do Rights Management relevantes

**Usuário final do Rights Management:** Pode acessar as páginas da Web do usuário final do Rights Management

**Rights Management Convidar Usuário:** Pode convidar usuários

**Rights Management: Gerenciar usuários convidados e locais:** Pode executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas de Rights Management relevantes

**Administrador do Conjunto de Políticas de Rights Management:** Executa todas as tarefas necessárias para todos os conjuntos de políticas nas páginas de Rights Management relevantes

**Rights Management Super Administrador:** Executa todas as tarefas necessárias na página Rights Management

**Administrador do AEM forms Workspace:** Pode exibir e modificar configurações da página Espaço de trabalho no Console de administração

***observação **: O Flex Workspace está obsoleto para a versão AEM formulários.*

**Usuário do Workspace:** Pode fazer logon no aplicativo do usuário final do Workspace

**Administrador de saída:** Pode visualizar e modificar configurações da página Saída no Console de Administração

**Administrador do PDFG:** Pode exibir e modificar configurações da página Gerador de PDF no console de administração

**Usuário do PDFG:** Pode acessar todas as funcionalidades não administrativas do Gerador de PDF

**Aplicação Web de extensões Acrobat Reader DC:** Pode usar o aplicativo web de extensões do Acrobat Reader DC

>[!NOTE]
>
>Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas podem existir fora de um firewall, permitir tarefas de nível administrativo pode representar um risco à segurança. Somente os usuários que têm os privilégios Administrador do AEM forms Workspace ou Usuário do AEM forms Workspace podem acessar as páginas da Web do usuário final do Workspace.

>[!NOTE]
>
>O Flex Workspace está obsoleto para a versão AEM formulários.

## Criar uma função {#create-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Na caixa Nome da função, digite um nome para a função e, opcionalmente, digite uma descrição da função e clique em Avançar.

   >[!NOTE]
   >
   >Ao usar o MySQL, não é possível criar duas funções que tenham o mesmo nome, mas sejam diferentes no uso de caracteres estendidos. Por exemplo, tentar criar uma função chamada abcde quando um âbcdè nomeado já existe resulta em um erro.

1. Clique em Localizar permissões e selecione as permissões para adicionar à função.
1. Clique em OK e depois em Next (Avançar).
1. Atribua essa função a usuários e grupos:

   * Clique em Localizar usuários/grupos.
   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione Nome, Email ou ID de usuário e selecione Usuários, Grupos ou Usuários e Grupos.
   * Selecione o domínio, selecione o número de resultados a serem exibidos e clique em Localizar.
   * Marque as caixas de seleção para os usuários e grupos aos quais atribuir essa função e clique em OK.

1. Para exibir os detalhes do usuário e do grupo, selecione a entidade.
1. Clique em OK e depois em Finish.

## Editar uma função {#edit-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Funções exibe todas as funções no banco de dados do Gerenciamento de Usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Clique na função a ser editada, edite as configurações gerais e clique em Salvar.
1. Para editar permissões de função, clique na guia Permissões e faça o seguinte:

   * Para adicionar novas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões que serão adicionadas, clique em OK e em Salvar.
   * Para excluir uma permissão da função, marque a caixa de seleção da permissão, clique em Excluir e em Salvar.

1. Para gerenciar a quem a função está atribuída, clique na guia Usuários da função e execute estas tarefas:

   * Para atribuir a função a novos usuários e grupos, clique em Localizar usuários/grupos e preencha as informações de pesquisa. Marque a caixa de seleção de cada usuário e grupo ao qual atribuir essa função, clique em OK e em Salvar.
   * Para remover a função, marque a caixa de seleção dos usuários ou grupos, clique em Cancelar atribuição e em Salvar.

## Excluir uma função {#delete-a-role}

É possível excluir qualquer uma das funções criadas, mas não as funções padrão AEM forms incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Funções exibe todas as funções no banco de dados do Gerenciamento de Usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Marque a caixa de seleção da função a ser excluída, clique em Excluir e em OK.

## Atribuir uma função a usuários e grupos {#assign-a-role-to-users-and-groups}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique as informações para restringir a pesquisa e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. Você pode classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Marque as caixas de seleção ao lado dos usuários e grupos para associar a uma função e clique em Atribuir função.
1. Selecione a função a ser atribuída ao usuário ou grupo e clique em OK.

Também é possível atribuir funções usando a página Gerenciamento de funções.

## Determinar quem está atribuído a uma função {#determine-who-is-assigned-to-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Funções exibe todas as funções no banco de dados do Gerenciamento de Usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Na página Detalhes da função , clique na guia Usuários da função . Uma lista de usuários e grupos que estão diretamente associados à função é exibida.

## Alterar permissões de função {#change-role-permissions}

Você pode alterar as permissões de qualquer uma das funções que criou. Não é possível alterar as permissões para as funções padrão do AEM forms incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Funções exibe todas as funções no banco de dados do Gerenciamento de Usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Selecione a função para a qual visualizar permissões e clique na guia Permissões .
1. Para alterar essas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões para adicionar à função, clique em OK e em Salvar.
1. Para excluir uma permissão, selecione-a, clique em Excluir e em Salvar.

### Permissões para formulários AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Adicionar, remover e modificar pontos de extremidade de um serviço

**Logon do Admin Console:** Exibir o console de administração

**Modificação de certificado:** Modifique as configurações de confiança de qualquer certificado no Armazenamento de Confiança

**Leitura do certificado:** Ler qualquer certificado no Armazenamento de Confiança

**Gravação do certificado:** Adicionar um certificado ao Armazenamento de Confiança

**Adição de componente:** Instalar um novo componente no sistema

**Exclusão de componente:** Excluir qualquer componente do sistema

**Leitura do componente:** Leia qualquer componente no sistema

**Administrador do Contentspace:** Permissão para Administrador do Contentspace (obsoleto)

**Logon do console do Contentspace:** Permissão para logon no console do Contentspace (obsoleto)

**Controle de configurações principais:** Gerencie as configurações na página Configurações do sistema principal no Console de administração

**CREATE_VERSION_PERM:** Criar uma nova versão de um serviço

**Modificação de Credencial:** Modifique qualquer credencial de assinatura no Armazenamento de Confiança

**Leitura da Credencial:** Ler qualquer credencial de assinatura no Armazenamento de Confiança

**Gravação de Credencial:** Adicionar uma credencial de assinatura ao Armazenamento de Confiança

**Modificação da CRL:** Modifique qualquer CRL (Lista de Revogação de Certificados) no Armazenamento de Confiança

**Leitura da CRL:** Leia qualquer CRL no Armazenamento de Confiança

**Gravação da CRL:** Adicionar uma CRL ao Armazenamento de Confiança

**Delegar:** Definir uma ACL em um recurso

**DELETE_VERSION_PERM:** Excluir uma versão de um serviço

**Upload de documento:** Fazer upload de documentos em formulários AEM

**Controle de domínio:** Criar, excluir ou modificar configurações de qualquer domínio do Gerenciamento de usuários, incluindo provedores de autenticação e de diretório

**Edição de tipo de evento:** Editar para tipos de evento

**Controle de representação de identidade:** Representar identidade no Gerenciador de usuários

**INVOKE_PERM:** Chamar todas as operações em um serviço

**Controle do Modelo de Dados LCDS:** Ler e implantar modelos de dados no Data Services

**Atualização do License Manager:** Atualizar informações de licença

**MODIFY_CONFIG_PERM:** Modificar a configuração de um serviço

**TERMO** Modificar a versão de um serviço

**PDFGAdminPermission:** Administrador PDFG

**PDFGUserPermission:** Usuário do PDFG

**PERM_DCTM_ADMIN:** Administrador do Documentum Connector

**PERM_FILENET_ADMIN:** Administrador do FileNet Connector

**PERM_FORMS_ADMIN:** Administrador do Forms

**PERM_IBMCM_ADMIN:** Administrador do IBM CM Connector

**PERM_OUTPUT_ADMIN:** Administrador de saída

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Usar o aplicativo web de extensões do Acrobat Reader DC

**PERM_SP_ADMIN:** Gerenciar configurações do SharePoint Connector

**PERM_WORKSPACE_ADMIN:** Gerenciar configurações do Workspace

**PERM_WORKSPACE_USER:** Faça logon no aplicativo do usuário final do Workspace

**Controlo Principal:** Gerencie usuários e grupos para qualquer domínio e gerencie atribuições de função para todos os usuários e grupos em qualquer domínio

**Processar Leitura/Exclusão de Gravação:** Listar e recuperar instâncias de auditoria de workflow

**PROCESS_OWNER_PERM:** Exibir dados de tendências e executar ações administrativas em um serviço criado de um processo

**Lido:** Ler o conteúdo de um recurso

**READ_PERM:** Ler ou visualizar um serviço

**Renovar asserção:** Renovar asserções no Gerenciamento de Usuários

**Representante do Repositório:** Definir uma ACL em um recurso

**Leitura do Repositório:** Ler o conteúdo de um recurso

**Rastreio do Repositório:** Inclua um recurso em uma solicitação de recursos de lista ou leia os metadados de um recurso

**Gravação do Repositório:** Gravar metadados e conteúdo do repositório

**Proprietário da Política de Alteração de Rights Management:** Alterar proprietário da política

**Logon do Console do Usuário Final do Rights Management:** Faça logon na interface do usuário final do Rights Management

**Configuração de gerenciamento de Rights Management:** Gerenciar configuração do servidor

**Rights Management: Gerenciar usuários convidados e locais:** Gerenciar usuários convidados e locais

**Rights Management Manage Conjuntos de Políticas:** Gerenciar todas as políticas e documentos em qualquer conjunto de políticas

**Coordenador de Adição do Conjunto de Políticas do Rights Management:** Adicionar, remover e alterar permissões dos coordenadores de conjuntos de políticas

**Política de Criação do Conjunto de Políticas de Rights Management:** Criar uma nova política para um conjunto de políticas

**Política de Eliminação do Conjunto de Políticas de Rights Management:** Remover uma política de um conjunto de políticas

**Política de Edição do Conjunto de Políticas de Rights Management:** Editar uma política em um conjunto de políticas

**Rights Management Policy Set Manage Document Publisher:** Ao criar conjuntos de políticas, você atribui aos usuários a função de publicador de documentos. O publicador do documento é o usuário que protege o documento com uma política.

**Coordenador de Remoção do Conjunto de Políticas de Rights Management:** Remover um coordenador de conjunto de políticas de um conjunto de políticas

**Documento de Revogação do Conjunto de Políticas de Rights Management:** Revogar acesso a documentos em um conjunto de políticas

**Política do Comutador do Conjunto de Políticas de Rights Management:** Alternar políticas para um documento

**Documento de Cancelamento de Revogação do Conjunto de Políticas de Rights Management:** Cancelar revogação de um documento

**Evento de Exibição do Conjunto de Políticas de Rights Management:** Exibir eventos de política e documento para qualquer política ou documento dentro de um conjunto de políticas

**Rights Management View Server Events:** Pesquisar e exibir todos os eventos de auditoria

**Controle de função:** Criar, excluir e modificar funções no Gerenciamento de usuários

**Serviço Ativar:** Iniciar qualquer serviço, disponibilizando-o para invocação

**Adicionar Serviço:** Implante um novo serviço no registro de serviços. Isso inclui a adição de novos processos e variantes de processos

**Desativação de Serviço:** Pare qualquer serviço no sistema

**Exclusão de Serviço:** Excluir qualquer serviço no sistema, incluindo processos e variantes de processos

**Chamada de serviço:** Chamar qualquer serviço no registro de serviço disponível no tempo de execução

**Modificação de Serviço:** Modifique as propriedades de configuração de qualquer serviço no sistema. Isso inclui bloquear e desbloquear um serviço no IDE e adicionar ou remover pontos de extremidade de um serviço

**Leitura do serviço:** Leia todos os serviços no sistema. Isso inclui todos os processos e variantes de processos

**SERVICE_AGENT_PERM:** Exibir dados e interagir com instâncias de processo de um serviço criado de um processo

**SERVICE_MANAGER_PERM:** Executar balanceamento de carga e outras ações administrativas em um serviço criado de um processo

**START_STOP_PERM:** Iniciar ou parar um serviço

**SUPERVISOR_PERM:** Exibir dados da instância do processo para um serviço criado de um processo

**Traversal:** Inclua um recurso em uma solicitação de recursos de lista ou leia os metadados de um recurso

**Gravar:** Gravar metadados e conteúdo do repositório

**Abrir arquivos no Workbench**

Para visualizar o conteúdo da visualização Recursos no Workbench e abrir arquivos para visualização, um usuário requer as seguintes permissões:

* Leitura do Repositório
* Rastreamento do Repositório
* Chamada de serviço
* Leitura do serviço

## Remover um usuário ou grupo de uma função {#remove-a-user-or-group-from-a-role}

Use a página Gerenciamento de função para remover usuários e grupos de uma função específica. Se o usuário ou grupo herdou a atribuição da função, não será possível remover a função no nível do usuário ou grupo. Remova o usuário ou grupo da árvore de herança ou remova a função do pai.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de Funções exibe todas as funções no banco de dados do Gerenciamento de Usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Na lista de funções, clique no nome da função a ser atualizada e, em seguida, clique na guia Usuários da função . Uma lista de usuários e grupos associados à função é exibida.
1. Marque as caixas de seleção dos usuários e grupos a serem removidos da função e clique em Cancelar atribuição.
1. Clique em Salvar e em OK.
