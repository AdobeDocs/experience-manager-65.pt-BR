---
title: Criação e configuração de funções
seo-title: Criação e configuração de funções
description: Saiba como associar usuários e grupos a funções que já fazem parte do banco de dados Gerenciamento de usuários. Também é possível criar, editar e excluir funções.
seo-description: Saiba como associar usuários e grupos a funções que já fazem parte do banco de dados Gerenciamento de usuários. Também é possível criar, editar e excluir funções.
uuid: e8e4331d-48e1-4fa9-8f44-f885f4ab1a54
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_organizing_users
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 737fb4d1-adef-47e1-9a0d-8cddd13132cb
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '2556'
ht-degree: 0%

---


# Criação e configuração de funções{#creating-and-configuring-roles}

Usando as páginas da Web Gerenciamento de usuários, você pode associar usuários e grupos a funções que já fazem parte do banco de dados Gerenciamento de usuários. Também é possível criar, editar e excluir funções.

O Gerenciamento de usuários tem dois tipos de funções:

**Funções mutáveis:** Esse tipo de função pode ser editado e excluído, e permissões de função podem ser adicionadas e excluídas desses tipos de função. Qualquer função criada é considerada uma função mutável. Você pode adicionar ou remover usuários e grupos atribuídos a funções mutáveis.

**Funções imutáveis:** as funções padrão incluídas no Gerenciamento de usuários são funções imutáveis. Essas funções não podem ser editadas ou excluídas. No entanto, você pode adicionar ou remover usuários e grupos atribuídos a funções imutáveis.

As funções mutáveis e imutáveis também podem ser criadas por meio das APIs de formulários AEM.

## Funções padrão {#default-roles}

As seguintes funções padrão estão incluídas no banco de dados Gerenciamento de usuários.

**usuário do console de administração:** pode acessar o console de administração.

**Administrador de aplicativos:** pode usar todos os recursos do Workbench. Pode usar as páginas Aplicativos e Serviços no console de administração para configurar as propriedades, os pontos de extremidade e a segurança do tempo de execução do serviço.

**Administrador de formulários AEM:** pode executar todas as tarefas para todos os serviços instalados.

**Administrador de segurança:** controla as configurações de Gerenciamento de usuários e gerencia usuários e grupos associados a qualquer domínio do Gerenciador de usuários

**Usuário de serviços:** pode visualização e invocar qualquer serviço

**Superadministrador:** tem acesso a todas as funcionalidades administrativas do sistema, incluindo serviços

**Administrador de confiança:** pode gerenciar as configurações de confiança de PKI e as credenciais de PKI gerenciadas na página Gerenciamento de armazenamento de confiança no console de administração

### Funções padrão adicionais {#additional-default-roles}

As funções padrão adicionais a seguir podem ser incluídas, dependendo dos componentes de formulários AEM instalados

**Usuário do aplicativo de upload do documento:** pode carregar documentos usando o Flex Remoting.

**Administrador do Forms:** pode visualização e modificar configurações da página do Forms no Console de administração

**AEM formulários Administrador de Contentspace:** Pode visualização e modificar configurações da página Serviços de conteúdo (obsoleto) no console de administração

**Usuário do Contentspace de formulários AEM:** pode fazer logon nas páginas da Web do Contentspace (obsoleto)

**Administrador do Documentum Connector:** pode visualização e modificar configurações da página Connector for EMC Documentum no console de administração

**AEM formulários FileNet Connector Administrator:** Pode visualização e modificar configurações da página Connector for IBM FileNet no console de administração

**AEM formulários do IBM CM Connector Administrator:** pode visualização e modificar configurações da página Connector for IBM Content Manager no console de administração

**Administrador de Rights Management:** Executa todas as tarefas necessárias para todas as configurações de servidor nas páginas Rights Management relevantes

**Usuário final do Rights Management:** pode acessar páginas da Web de usuários finais do Rights Management

**Rights Management Convidar usuário:** Pode convidar usuários

**Rights Management para gerenciar usuários convidados e locais:** pode executar tarefas necessárias para gerenciar todos os usuários convidados e locais nas páginas Rights Management relevantes

**Administrador de conjunto de políticas de Rights Management:** Executa todas as tarefas necessárias para todos os conjuntos de políticas nas páginas Rights Management relevantes

**Super Administrador do Rights Management:** Executa todas as tarefas necessárias na página Rights Management

**AEM formulários Administrador do Workspace:** pode visualização e modificar configurações da página do Workspace no Console de Administração

***observação **: O Flex Workspace está obsoleto para AEM versão de formulários.*

**Usuário do Workspace:** pode fazer logon no aplicativo de usuário final do Workspace

**Administrador de saída:** pode visualização e modificar configurações da página Saída no Console de administração

**Administrador do PDFG:** pode visualização e modificar configurações da página Gerador de PDF no console de administração

**Usuário do PDFG:** pode acessar todas as funcionalidades não administrativas do Gerador de PDF

**aplicação web de extensões do Acrobat Reader DC:** Pode usar o aplicativo da Web de extensões do Acrobat Reader DC

>[!NOTE]
>
>Os usuários com determinados tipos de privilégios de administrador não podem acessar as páginas da Web do usuário final do Workspace por motivos de segurança. Como essas páginas podem existir fora de um firewall, permitir tarefas de nível administrativo pode representar um risco à segurança. Somente os usuários que tiverem os formulários AEM Administrador do Espaço de trabalho ou AEM privilégios de Usuário do Espaço de trabalho poderão acessar as páginas da Web do usuário final do Espaço de trabalho.

>[!NOTE]
>
>O Flex Workspace está obsoleto para AEM versão de formulários.

## Criar uma função {#create-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nova função.
1. Na caixa Nome da função, digite um nome para a função e, opcionalmente, digite uma descrição da função e clique em Avançar.

   >[!NOTE]
   >
   >Ao usar o MySQL, não é possível criar duas funções que tenham o mesmo nome, mas que sejam diferentes no uso de caracteres estendidos. Por exemplo, tentar criar uma função chamada abcde quando um nome âbcdè já existe resulta em um erro.

1. Clique em Localizar permissões e selecione as permissões para adicionar à função.
1. Clique em OK e em Avançar.
1. Atribua esta função a usuários e grupos:

   * Clique em Localizar usuários/grupos.
   * Na caixa Localizar, digite os critérios de pesquisa.
   * Selecione Nome, Email ou ID de usuário e, em seguida, selecione Usuários, Grupos ou Usuários e grupos.
   * Selecione o domínio, selecione o número de resultados a serem exibidos e clique em Localizar.
   * Marque as caixas de seleção para os usuários e grupos aos quais atribuir essa função e clique em OK.

1. Para visualização de detalhes de usuários e grupos, selecione a entidade.
1. Clique em OK e em Concluir.

## Editar uma função {#edit-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de funções exibe todas as funções no banco de dados Gerenciamento de usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Clique na função para editar, editar as configurações gerais e clique em Salvar.
1. Para editar permissões de função, clique na guia Permissões e faça as seguintes tarefas:

   * Para adicionar novas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões a serem adicionadas, clique em OK e em Salvar.
   * Para excluir uma permissão da função, marque a caixa de seleção da permissão, clique em Excluir e em Salvar.

1. Para gerenciar a função atribuída, clique na guia Usuários da função e faça as seguintes tarefas:

   * Para atribuir a função a novos usuários e grupos, clique em Localizar usuários/grupos e preencha as informações de pesquisa. Marque a caixa de seleção de cada usuário e grupo ao qual atribuir essa função, clique em OK e em Salvar.
   * Para remover a função, marque a caixa de seleção dos usuários ou do grupo, clique em Cancelar atribuição e em Salvar.

## Excluir uma função {#delete-a-role}

É possível excluir qualquer uma das funções que você criou, mas não as funções padrão de formulários AEM que estão incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de funções exibe todas as funções no banco de dados Gerenciamento de usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Marque a caixa de seleção da função a ser excluída, clique em Excluir e, em seguida, clique em OK.

## Atribuir uma função a usuários e grupos {#assign-a-role-to-users-and-groups}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Usuários e grupos.
1. Especifique as informações para restringir a pesquisa e clique em Localizar. Os resultados da pesquisa são listados na parte inferior da página. É possível classificar a lista clicando em qualquer um dos cabeçalhos da coluna.
1. Marque as caixas de seleção ao lado dos usuários e grupos a serem associados a uma função e clique em Atribuir função.
1. Selecione a função a ser atribuída ao usuário ou grupo e clique em OK.

Você também pode atribuir funções usando a página Gerenciamento de funções.

## Determinar quem está atribuído a uma função {#determine-who-is-assigned-to-a-role}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de funções exibe todas as funções no banco de dados Gerenciamento de usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Na página Detalhes da função, clique na guia Usuários da função. Uma lista de usuários e grupos que estão diretamente associados à função é exibida.

## Alterar permissões de função {#change-role-permissions}

É possível alterar as permissões de qualquer uma das funções que você criou. Não é possível alterar as permissões para as funções padrão de formulários AEM que estão incluídas no produto.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de funções exibe todas as funções no banco de dados Gerenciamento de usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Selecione a função para a qual deseja visualização as permissões e clique na guia Permissões.
1. Para alterar essas permissões, clique em Localizar permissões, marque as caixas de seleção das permissões a serem adicionadas à função, clique em OK e em Salvar.
1. Para excluir uma permissão, selecione-a, clique em Excluir e em Salvar.

### Permissões para formulários AEM {#aem-forms-permissions}

**ADD_REMOVE_ENDPOINT_PERM:** Adicionar, remover e modificar pontos de extremidade de um serviço

**Login no Admin Console:** Visualização no console de administração

**Modificação do Certificado:** Modifique as configurações de confiança de qualquer certificado no Repositório de Confiança

**Leitura do certificado:** Ler qualquer certificado no Repositório de confiança

**Gravação de certificado:** adicione um certificado ao armazenamento de confiança

**Adição de componente:** instale um novo componente no sistema

**Exclusão de componente:** exclua qualquer componente no sistema

**Leitura do componente:** Ler qualquer componente no sistema

**Administrador do Contentspace:** Permissão para Administrador do Contentspace (Obsoleto)

**Logon do console do Contentspace:** Permissão para o Contentspace (Obsoleto) Login do console

**Controle de configurações principais:** gerencie as configurações na página Configurações principais do sistema no Console de administração

**CREATE_VERSION_PERM:** Criar uma nova versão de um serviço

**Modificação da Credencial:** Modifique qualquer credencial de assinatura no Armazenamento de Confiança

**Leitura de credencial:** Ler qualquer credencial de assinatura no Repositório de confiança

**Gravação de credencial:** adicione uma credencial de assinatura ao armazenamento de confiança

**Modificação da CRL:** modifique qualquer CRL (Lista de Revogação de Certificado) no Repositório de Confiança

**Leitura da CRL:** Ler qualquer CRL no Repositório de Confiança

**Gravação de CRL:** adicione uma CRL ao armazenamento de confiança

**Delegar:** Definir uma ACL em um recurso

**DELETE_VERSION_PERM:** Excluir uma versão de um serviço

**Upload de documento:** Carregar documentos em formulários AEM

**Controle de Domínio:** Criar, excluir ou modificar configurações para qualquer domínio de Gerenciamento de Usuário, incluindo sua autenticação e provedores de diretório

**Edição de tipo de evento:** Editar em tipos de evento

**Controle de representação de identidade:** Representar identidade no Gerenciador de usuários

**INVOKE_PERM:** Chamar todas as operações em um serviço

**Controle de Modelo de Dados LCDS:** Ler e implantar modelos de dados no Data Services

**Atualização do License Manager:** Atualizar informações da licença

**MODIFY_CONFIG_PERM:** Modificar a configuração de um serviço

**** TERMOodificar a versão de um serviço

**PDFGAdminPermission:administrador** PDFG

**PDFGUserPermission:usuário** PDFG

**PERM_DCTM_ADMIN:administrador do** Documentum Connector

**PERM_FILENET_ADMIN:administrador do** FileNet Connector

**PERM_FORMS_ADMIN:administrador** Forms

**PERM_IBMCM_ADMIN:administrador do** IBM CM Connector

**PERM_OUTPUT_ADMIN:administrador** de saída

**PERM_READER_EXTENSIONS_WEB_APPLICATION:** Use o aplicativo da Web de extensões Acrobat Reader DC

**PERM_SP_ADMIN:** Gerenciar configurações do SharePoint Connector

**PERM_WORKSPACE_ADMIN:** Gerenciar configurações da Workspace

**PERM_WORKSPACE_USER:** Faça logon no aplicativo de usuário final da Workspace

**Controle principal:** gerencie usuários e grupos para qualquer domínio e gerencie atribuições de função para todos os usuários e grupos em qualquer domínio

**Processar leitura/exclusão da gravação:** Lista e recuperação de instâncias de auditoria do fluxo de trabalho

**PROCESS_OWNER_PERM:dados de tendências de** Visualização e executar ações administrativas em um serviço criado a partir de um processo

**Ler:** Ler o conteúdo de um recurso

**READ_PERM:** Ler ou visualização um serviço

**Renovar asserção:** Renovar asserções no Gerenciamento de usuários

**Representante do repositório:** definir uma ACL em um recurso

**Leitura do repositório:** Leia o conteúdo de um recurso

**Trajeto do repositório:** inclua um recurso em uma solicitação de recursos de lista ou leia os metadados de um recurso

**Gravação do repositório:** Gravar metadados e conteúdo do repositório

**Proprietário da Política de Alteração de Rights Management:** Alterar proprietário da política

**Logon no console do usuário final do Rights Management:** faça logon na interface do usuário final do Rights Management

**Configuração do Rights Management Manage:** Gerenciar configuração do servidor

**Rights Management: Gerenciar usuários convidados e locais:** Gerenciar usuários convidados e locais

**Rights Management Manage Policy Sets:** gerencie todas as políticas e documentos em qualquer conjunto de políticas

**Coordenador Adicionar conjunto de políticas de Rights Management:** Adicionar, remover e alterar permissões dos coordenadores de definição de políticas

**Política de Rights Management: Criar Política:** Criar uma nova política para um conjunto de políticas

**Política de Rights Management: política de exclusão de conjunto de políticas:** remover uma política de um conjunto de políticas

**Política de Rights Management Definir Política Editar Política:** Editar uma política em um conjunto de políticas

**Rights Management Policy Set Manage Documento Publisher:** ao criar conjuntos de políticas, você atribui aos usuários a função de editor de documentos. O editor do documento é o usuário que protege o documento com uma política.

**Rights Management Policy Set Remover Coordenador:** Remover um coordenador de conjunto de políticas de um conjunto de políticas

**Rights Management Policy Set Revoke Documento:** Revogar acesso a documentos em um conjunto de políticas

**Política de troca de conjunto de políticas de Rights Management:políticas de** troca de um documento

**Rights Management Policy Set Cancelar revogação de Documento:** Cancelar revogação de um documento

**evento de Visualização de Conjunto de Políticas de Rights Management:política de** Visualização e eventos de documento para qualquer política ou documento em um conjunto de políticas

**eventos de servidor de Visualização de Rights Management:** pesquisar e visualização todos os eventos de auditoria

**Controle de função:** Criar, excluir e modificar funções no Gerenciamento de usuários

**Ativação do serviço:** Start qualquer serviço, disponibilizando-o para invocação

**Adição de serviço:** Implantar um novo serviço no registro de serviço. Isso inclui a adição de novos processos e variantes de processos

**Desativação do serviço:** pare qualquer serviço no sistema

**Exclusão de serviço:** exclua qualquer serviço no sistema, incluindo processos e variantes de processo

**Chamada de serviço:** Chame qualquer serviço no registro de serviço disponível em tempo de execução

**Modificação do serviço:** modifique as propriedades de configuração de qualquer serviço no sistema. Isso inclui bloquear e desbloquear um serviço no IDE e adicionar ou remover pontos de extremidade de um serviço

**Leitura do serviço:** leia todos os serviços no sistema. Isso inclui todos os processos e variantes de processos

**SERVICE_AGENT_PERM:dados de** Visualização e interagir com instâncias de processo para um serviço criado a partir de um processo

**SERVICE_MANAGER_PERM:** Executar balanceamento de carga e outras ações administrativas em um serviço criado a partir de um processo

**START_STOP_PERM:** Start ou parar um serviço

**SUPERVISOR_PERM:dados de instância do processo de** Visualização para um serviço criado a partir de um processo

**Traversal:** inclua um recurso em uma solicitação de recursos de lista ou leia os metadados de um recurso

**Gravação:** Gravar metadados e conteúdo do repositório

**Abrir arquivos no Workbench**

Para visualização do conteúdo da visualização Recursos no Workbench e abrir arquivos para visualização, um usuário requer as seguintes permissões:

* Leitura do repositório
* Trajeto do repositório
* Chamada de serviço
* Leitura do serviço

## Remover um usuário ou grupo de uma função {#remove-a-user-or-group-from-a-role}

Use a página Gerenciamento de funções para remover usuários e grupos de uma função específica. Se o usuário ou grupo herdou a atribuição da função, não será possível remover a função no nível do usuário ou grupo. Remova o usuário ou grupo da árvore de herança ou remova a função do pai.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de funções e, em seguida, clique em Nome da função.

   Por padrão, a página Gerenciamento de funções exibe todas as funções no banco de dados Gerenciamento de usuários. Se a lista de funções for grande, use a área Localizar na parte superior da página para procurar um nome de função específico.

1. Na lista de funções, clique no nome da função a ser atualizada e clique na guia Usuários da função. Uma lista de usuários e grupos associados à função é exibida.
1. Marque as caixas de seleção para os usuários e grupos a serem removidos da função e clique em Cancelar atribuição.
1. Clique em Salvar e em OK.

