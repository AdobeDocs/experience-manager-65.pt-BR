---
title: Configuração de provedores de autenticação
description: Adicione, edite ou exclua provedores de autenticação, altere configurações de autenticação e leia sobre o provisionamento just-in-time de usuários.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d72a3977-1423-49e0-899b-234bb76be378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1580'
ht-degree: 0%

---

# Configuração de provedores de autenticação {#configuring-authentication-providers}

Os domínios híbridos exigem pelo menos um provedor de autenticação, e os domínios enterprise exigem pelo menos um provedor de autenticação ou provedor de diretório.

Se você habilitar o SSO usando o SPNEGO, adicione um provedor de autenticação Kerberos com o SPNEGO habilitado e um provedor LDAP como backup. Essa configuração permite a autenticação do usuário com uma ID de usuário e senha se o SPNEGO não estiver funcionando. (Consulte [Habilitar SSO usando SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Adicionar um provedor de autenticação {#add-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em um domínio existente na lista. Se você estiver adicionando autenticação para um novo domínio, consulte [Adicionar um domínio corporativo](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) ou [Adicionar um domínio híbrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação, selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa.
1. Forneça todas as informações adicionais necessárias na página. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. (Opcional) Clique em Testar para testar a configuração.
1. Clique em OK e em OK novamente.

## Editar um provedor de autenticação existente {#edit-an-existing-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Na página exibida, selecione o provedor de autenticação apropriado na lista e faça as alterações necessárias. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. Clique em OK.

## Excluir um provedor de autenticação {#delete-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Marque as caixas de seleção dos provedores de autenticação a serem excluídos e clique em Excluir.
1. Clique em OK na página de confirmação exibida e clique em OK novamente.

## Configurações de autenticação {#authentication-settings}

As configurações a seguir estão disponíveis, dependendo do tipo de domínio e do tipo de autenticação que você escolheu.

### Configurações LDAP {#ldap-settings}

Se você estiver configurando a autenticação para um domínio enterprise ou híbrido e selecionar a autenticação LDAP, poderá optar por usar o servidor LDAP especificado na configuração do diretório ou escolher outro servidor LDAP para usar na autenticação. Se você escolher um servidor diferente, seus usuários deverão existir em ambos os servidores LDAP.

Para usar o servidor LDAP especificado na sua configuração de diretório, selecione LDAP como o provedor de autenticação e clique em OK.

Para usar um servidor LDAP diferente para fazer autenticação, selecione LDAP como provedor de autenticação e marque a caixa de seleção Autenticação LDAP Personalizada. As seguintes definições de configuração são exibidas.

**Servidor:** (Obrigatório) FQDN (nome de domínio totalmente qualificado) do servidor de diretório. Por exemplo, para um computador chamado x na rede example.com, o FQDN é x.example.com. Um endereço IP pode ser usado no lugar do nome do servidor FQDN.

**Porta:** (obrigatória) a porta usada pelo servidor de diretório. Normalmente 389 ou 636 se o protocolo SSL for usado para enviar informações de autenticação pela rede.

**SSL:** (Obrigatório) Especifica se o servidor de diretório usa SSL ao enviar dados pela rede. O padrão é Não. Quando definido como Sim, o certificado do servidor LDAP correspondente deve ser confiável pelo Java™ runtime environment (JRE) do servidor de aplicativos.

**Associação** (Obrigatório) Especifica como acessar o diretório.

**Anônimo:** nenhum nome de usuário ou senha é necessário.

**Usuário:** A autenticação é necessária. Na caixa Nome, especifique o nome do registro do usuário que pode acessar o diretório. É melhor inserir o nome distinto completo (DN) da conta de usuário, como cn=Jane Doe, ou=user, dc=can, dc=com. Na caixa Senha, especifique a senha associada. Essas configurações são necessárias ao selecionar Usuário como a opção de Vinculação.

**Recuperar DNs de Base:** (Não obrigatório) Recupera os DNs de base e os exibe na lista suspensa. Essa configuração é útil quando você tem vários DNs de base e precisa selecionar um valor.

**DN Base:** (Obrigatório) Usado como ponto de partida para sincronizar usuários e grupos da hierarquia LDAP. É melhor especificar um DN base no nível mais baixo da hierarquia que abranja todos os usuários e grupos que precisam ser sincronizados para serviços. Não inclua o DN do usuário nessa configuração. Para sincronizar um usuário específico, use a configuração Filtro de pesquisa.

**Preencher página com:** (Não obrigatório) Quando selecionado, preenche os atributos nas páginas de configurações Usuário e Grupo com os valores LDAP padrão correspondentes.

**Filtro de Pesquisa:** (Obrigatório) O filtro de pesquisa a ser usado para localizar o registro associado ao usuário. Consulte Sintaxe do filtro de pesquisa.

### Configurações Kerberos {#kerberos-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação Kerberos, as seguintes configurações estarão disponíveis.

**IP do DNS:** O endereço IP do DNS do servidor onde os formulários AEM estão em execução. No Windows, você pode determinar esse endereço IP executando ipconfig /all na linha de comando.

**Host KDC:** Nome de host ou endereço IP totalmente qualificado do servidor do Ative Diretory usado para autenticação.

**Usuário de Serviço:** Se você estiver usando o Ative Diretory 2003, esse valor será o mapeamento criado para a entidade de serviço no formulário `HTTP/<server name>`. Se você estiver usando o Ative Diretory 2008, esse valor será a ID de logon da entidade de serviço. Por exemplo, suponha que a entidade de serviço seja chamada de um spnego, a ID do usuário seja spnegodemo e o mapeamento seja HTTP/example.yourcompany.com. Com o Ative Diretory 2003, você definiu o Usuário de Serviço como HTTP/example.yourcompany.com. Com o Ative Diretory 2008, você definiu Service User para spnegodemo. (Consulte Habilitar SSO usando SPNEGO.)

**Realm de Serviço:** Nome de domínio do Ative Diretory

**Senha do serviço:** Senha do usuário do serviço

**Habilitar SPNEGO:** Habilita o uso do SPNEGO para logon único (SSO). (Consulte Habilitar SSO usando SPNEGO.)

### Configurações de SAML {#saml-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação SAML, as seguintes configurações estarão disponíveis. Para obter informações sobre configurações SAML adicionais, consulte [Definir configurações do provedor de serviços SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selecione um Metadado de Provedor de Identidade SAML
arquivo a ser importado:** Clique em Procurar para selecionar um arquivo de metadados do provedor de identidade SAML gerado pelo IDP e clique em Importar. Os detalhes do IDP são exibidos.

**Título:** Alias da URL denotada pela EntityID. O título também é exibido na página de logon para usuários corporativos e locais.

O **Provedor de Identidade dá suporte à Autenticação Básica do Cliente:** a Autenticação Básica do Cliente é usada quando o IDP usa um perfil de Resolução de Artefato SAML. Neste perfil, o Gerenciamento de usuários se conecta novamente a um serviço Web em execução no IDP para recuperar a asserção SAML real. O IDP pode exigir autenticação. Se o IDP exigir autenticação, selecione essa opção e especifique um nome de usuário e uma senha nas caixas fornecidas.

**Propriedades Personalizadas:** Permite que você especifique propriedades adicionais. As propriedades adicionais são pares nome=valor separados por novas linhas.

As seguintes propriedades personalizadas são necessárias se a associação de artefato for usada.

* Adicione a seguinte propriedade personalizada para especificar um nome de usuário que representa o Provedor de serviços de formulários AEM, usado para autenticar no serviço de Resolução de artefatos IDP.
  `saml.idp.resolve.username=<username>`

* Adicione a seguinte propriedade personalizada para especificar a senha do usuário especificado em `saml.idp.resolve.username`.
  `saml.idp.resolve.password=<password>`

* Adicione a seguinte propriedade personalizada para permitir que o provedor de serviços ignore a validação do certificado ao estabelecer a conexão com o serviço de Resolução de Artefatos por SSL.
  `saml.idp.resolve.ignorecert=true`

### Configurações personalizadas {#custom-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar Autenticação personalizada, selecione o nome do provedor de autenticação personalizado.

## Provisionamento just-in-time de usuários {#just-in-time-provisioning-of-users}

O provisionamento just-in-time cria automaticamente um usuário no banco de dados de Gerenciamento de usuários depois que o usuário é autenticado com êxito por meio de um provedor de autenticação. As funções e os grupos relevantes também são atribuídos dinamicamente ao novo usuário. Você pode ativar o provisionamento just-in-time para domínios corporativos e híbridos.

Este procedimento descreve como a autenticação tradicional funciona em formulários AEM:

1. Quando um usuário tenta fazer logon em formulários AEM, o Gerenciamento de usuários passa suas credenciais sequencialmente para todos os provedores de autenticação disponíveis. (As credenciais de logon incluem combinação de nome de usuário/senha, tíquete Kerberos, assinatura PKCS7 e assim por diante.)
1. O provedor de autenticação valida as credenciais.
1. O provedor de autenticação verifica se o usuário existe no banco de dados de Gerenciamento de usuários. Os seguintes status são possíveis:

   **Existe** Se o usuário estiver atualizado e desbloqueado, o Gerenciamento de Usuários retornará uma autenticação com êxito. No entanto, se o usuário não for atual ou estiver bloqueado, o Gerenciamento de usuários retornará uma falha de autenticação.

   **Não existe** O Gerenciamento de Usuários retorna uma falha de autenticação.

   **Inválido** O Gerenciamento de Usuários retorna uma falha de autenticação.

1. O resultado retornado pelo provedor de autenticação é avaliado. Se o provedor de autenticação retornou êxito de autenticação, o usuário tem permissão para fazer logon. Caso contrário, o Gerenciamento de usuários verificará com o próximo provedor de autenticação (etapas 2-3).
1. A falha de autenticação será retornada se nenhum provedor de autenticação disponível validar as credenciais do usuário.

Quando o provisionamento just-in-time está ativado, novos usuários são criados dinamicamente no Gerenciamento de usuários se um dos provedores de autenticação validar suas credenciais. (Após a etapa 3 do procedimento acima.)

Sem o provisionamento just-in-time, quando um usuário é autenticado com êxito, mas não é encontrado no banco de dados de Gerenciamento de usuários, a autenticação falha. O provisionamento just-in-time adiciona uma etapa no procedimento de autenticação para criar o usuário e atribuir funções e grupos ao usuário.

### Habilitar provisionamento just-in-time para um domínio {#enable-just-in-time-provisioning-for-a-domain}

1. Grave um contêiner de serviço que implemente as interfaces IdentityCreator e AssignmentProvider. (Consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Implante o contêiner de serviço no Forms Server.
1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.

   Selecione um domínio existente ou clique em Novo Domínio Enterprise.

1. Para criar um domínio, clique em Novo domínio corporativo ou Novo domínio híbrido. Para editar um domínio existente, clique no nome do domínio.
1. Selecione Ativar provisionamento just-in-time.

   ***observação **: se a caixa de seleção Habilitar Provisionamento Just In Time estiver ausente, clique em Início > Configurações > Gerenciamento de Usuários> Configuração > Atributos Avançados do Sistema e clique em Recarregar.*

1. Adicionar provedores de autenticação. Ao adicionar provedores de autenticação, na tela Nova autenticação, selecione um Criador de identidade e um Provedor de atribuição registrados. (Consulte [Configuração de provedores de autenticação](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salve o domínio.
