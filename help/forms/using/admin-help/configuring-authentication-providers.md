---
title: Configuração de provedores de autenticação
seo-title: Configuring authentication providers
description: Adicione, edite ou exclua provedores de autenticação, altere as configurações de autenticação e leia sobre o provisionamento just-in-time dos usuários.
seo-description: Add, edit, or delete authentication providers, change authentication settings, and read about just-in-time provisioning of users.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
exl-id: d72a3977-1423-49e0-899b-234bb76be378
source-git-commit: 1cdd15800548362ccdd9e70847d9df8ce93ee06e
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 0%

---

# Configuração de provedores de autenticação {#configuring-authentication-providers}

Os domínios híbridos exigem pelo menos um provedor de autenticação e os domínios corporativos exigem pelo menos um provedor de autenticação ou provedor de diretório.

Se você habilitar o SSO usando o SPNEGO, adicione um provedor de autenticação Kerberos com o SPNEGO habilitado e um provedor LDAP como backup. Essa configuração permite a autenticação do usuário com um ID de usuário e senha se o SPNEGO não estiver funcionando. (Consulte [Ativar SSO usando SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Adicionar um provedor de autenticação {#add-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em um domínio existente na lista. Se estiver adicionando autenticação para um novo domínio, consulte [Adicionar um domínio corporativo](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) ou [Adicionar um domínio híbrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação , selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa.
1. Forneça quaisquer informações adicionais necessárias na página. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. (Opcional) Clique em Testar para testar a configuração.
1. Clique em OK e em OK novamente.

## Editar um provedor de autenticação existente {#edit-an-existing-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Na página exibida, selecione o provedor de autenticação apropriado na lista e faça as alterações necessárias. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. Clique em OK.

## Excluir um provedor de autenticação {#delete-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Marque as caixas de seleção dos provedores de autenticação a serem excluídos e clique em Excluir.
1. Clique em OK na página de confirmação que aparece e clique em OK novamente.

## Configurações de autenticação {#authentication-settings}

As configurações a seguir estão disponíveis, dependendo do tipo de domínio e do tipo de autenticação escolhido.

### Configurações LDAP {#ldap-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação LDAP, poderá optar por usar o servidor LDAP especificado na configuração do diretório ou escolher um servidor LDAP diferente para ser usado na autenticação. Se você escolher um servidor diferente, seus usuários deverão existir em ambos os servidores LDAP.

Para usar o servidor LDAP especificado na configuração de diretório, selecione LDAP como o provedor de autenticação e clique em OK.

Para usar um servidor LDAP diferente para executar autenticação, selecione LDAP como o provedor de autenticação e marque a caixa de seleção Autenticação LDAP personalizada. As configurações a seguir são exibidas.

**Servidor:**  (Obrigatório) Nome de domínio totalmente qualificado (FQDN) do servidor de diretório. Por exemplo, para um computador chamado x na rede example.com, o FQDN é x.example.com. Um endereço IP pode ser usado no lugar do nome do servidor FQDN.

**Porta:** (Obrigatório) A porta que o servidor de diretório usa. Normalmente, 389 ou 636 se o protocolo SSL for usado para enviar informações de autenticação pela rede.

**SSL:** (Obrigatório) Especifica se o servidor de diretório usa SSL ao enviar dados pela rede. O padrão é Não. Quando definido como Sim, o certificado do servidor LDAP correspondente deve ser confiável pelo JRE (Java™ runtime environment) do servidor de aplicativos.

**Vínculo**  (Obrigatório) Especifica como acessar o diretório.

**Anônimo:** não é necessário nenhum nome de usuário ou senha.

**Usuário:** a autenticação é necessária. Na caixa Nome, especifique o nome do registro do usuário que pode acessar o diretório. É melhor inserir o DN (nome distinto completo) da conta de usuário, como cn=Jane Doe, ou=user, dc=can, dc=com. Na caixa Senha, especifique a senha associada. Essas configurações são necessárias quando você seleciona Usuário como a opção Vínculo.

**Recuperar DNs de Base:**  (Não obrigatório) Recupera os DNs de Base e os exibe na lista suspensa. Essa configuração é útil quando você tem vários DNs de base e precisa selecionar um valor.

**DN de base:** (Obrigatório) usado como ponto de partida para sincronizar usuários e grupos da hierarquia LDAP. É melhor especificar um DN básico no nível mais baixo da hierarquia que abrange todos os usuários e grupos que precisam ser sincronizados para serviços. Não inclua o DN do usuário nessa configuração. Para sincronizar um usuário específico, use a configuração Filtro de pesquisa .

**Preencha a página com:**  (Não obrigatório) Quando selecionada, preenche os atributos nas páginas de configurações de Usuário e Grupo com os valores LDAP padrão correspondentes.

**Filtro de pesquisa:** (Obrigatório) o filtro de pesquisa a ser usado para localizar o registro associado ao usuário. Consulte Sintaxe de filtro de pesquisa.

### Configurações de Kerberos {#kerberos-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação Kerberos, as configurações a seguir estarão disponíveis.

**DNS IP:** O endereço IP DNS do servidor em que AEM formulários está em execução. No Windows, você pode determinar esse endereço IP executando ipconfig /all na linha de comando.

**Host KDC:** nome de host totalmente qualificado ou endereço IP do servidor Ative Diretory usado para autenticação.

**Usuário do Serviço:** Se estiver usando o Ative Diretory 2003, esse valor será o mapeamento criado para o principal de serviço no formulário  `HTTP/<server name>`. Se estiver usando o Ative Diretory 2008, esse valor será a ID de logon da entidade de serviço. Por exemplo, suponha que a entidade de serviço seja chamada de um spnego, a ID de usuário é spnegodemo e o mapeamento é HTTP/example.yourcompany.com. Com o Ative Diretory 2003, você define Usuário do Serviço como HTTP/example.yourcompany.com. Com o Ative Diretory 2008, você define Usuário de Serviço como spnegodemo. (Consulte Ativar SSO usando SPNEGO.)

**Realm de Serviço:** Nome de domínio do Ative Diretory

**Senha do serviço:** Senha do usuário do serviço

**Habilitar SPNEGO:** Habilita o uso de SPNEGO para logon único (SSO). (Consulte Ativar SSO usando SPNEGO.)

### Configurações SAML {#saml-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação SAML, as configurações a seguir estarão disponíveis. Para obter informações sobre configurações SAML adicionais, consulte [Definir configurações do provedor de serviço SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selecione um arquivo de metadados do provedor de identidade SAML a ser importado:** Clique em Procurar para selecionar um arquivo de metadados do provedor de identidade SAML gerado pelo IDP e clique em Importar. Detalhes do IDP são exibidos.

**Título:** alias para o URL denotado pela EntityID. O título também é exibido na página de logon para usuários empresariais e locais.

**O Provedor de Identidade Suporta Autenticação Básica do Cliente:** A Autenticação Básica do Cliente é usada quando o IDP usa um perfil SAML Artifact Resolution. Nesse perfil, o Gerenciamento de usuários se conecta a um serviço da Web em execução no IDP para recuperar a asserção de SAML real. O IDP pode exigir autenticação. Se o IDP exigir autenticação, selecione essa opção e especifique um nome de usuário e senha nas caixas fornecidas.

**Propriedades personalizadas:** permite especificar propriedades adicionais. As propriedades adicionais são pares name=value separados por novas linhas.

As seguintes propriedades personalizadas são necessárias se a vinculação de artefato for usada.

* Adicione a seguinte propriedade personalizada para especificar um nome de usuário que represente o Provedor de Serviços de Formulários AEM, que será usada para autenticar no serviço de Resolução de Artefatos do IDP.
   `saml.idp.resolve.username=<username>`

* Adicione a seguinte propriedade personalizada para especificar a senha para o usuário especificado em `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Adicione a seguinte propriedade personalizada para permitir que o provedor de serviços ignore a validação do certificado enquanto estabelece a conexão com o serviço de Resolução de Artefatos por SSL.
   `saml.idp.resolve.ignorecert=true`

### Configurações personalizadas {#custom-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar Autenticação personalizada, selecione o nome do provedor de autenticação personalizado.

## Provisionamento just-in-time de usuários {#just-in-time-provisioning-of-users}

O provisionamento just-in-time cria um usuário no banco de dados do Gerenciamento de usuários automaticamente depois que o usuário é autenticado com êxito por meio de um provedor de autenticação. As funções e os grupos relevantes também são atribuídos dinamicamente ao novo usuário. Você pode ativar o provisionamento just-in-time para domínios corporativos e híbridos.

Este procedimento descreve como a autenticação tradicional funciona em formulários AEM:

1. Quando um usuário tenta fazer logon em AEM formulários, o Gerenciamento de usuários transmite suas credenciais sequencialmente para todos os provedores de autenticação disponíveis. (As credenciais de logon incluem combinação de nome de usuário/senha, tíquete Kerberos, assinatura PKCS7 e assim por diante.)
1. O provedor de autenticação valida as credenciais.
1. O provedor de autenticação verifica se o usuário existe no banco de dados do Gerenciamento de usuários. Os seguintes status são possíveis:

   **** ExisteSe o usuário estiver atual e desbloqueado, o Gerenciamento de usuários retornará a autenticação bem-sucedida. No entanto, se o usuário não for atual ou estiver bloqueado, o Gerenciamento de usuários retornará a falha de autenticação.

   **Não** existe. O Gerenciamento de Usuário retorna a falha de autenticação.

   **** InvalidUser Management retorna a falha de autenticação.

1. O resultado retornado pelo provedor de autenticação é avaliado. Se o provedor de autenticação retornar a autenticação bem-sucedido, o usuário poderá fazer logon. Caso contrário, o Gerenciamento de usuários verificará o próximo provedor de autenticação (etapas 2 a 3).
1. A falha de autenticação é retornada se nenhum provedor de autenticação disponível validar as credenciais do usuário.

Quando o provisionamento just-in-time é ativado, novos usuários são criados dinamicamente no Gerenciamento de usuários se um dos provedores de autenticação validar suas credenciais. (Após a etapa 3 do procedimento acima.)

Sem provisionamento just-in-time, quando um usuário é autenticado com êxito, mas não é encontrado no banco de dados do Gerenciamento de usuários, a autenticação falha. O provisionamento just-in-time adiciona uma etapa no procedimento de autenticação para criar o usuário e atribuir funções e grupos ao usuário.

### Habilitar provisionamento just-in-time para um domínio {#enable-just-in-time-provisioning-for-a-domain}

1. Escreva um contêiner de serviço que implemente as interfaces IdentityCreator e AssignmentProvider. (Consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Implante o contêiner de serviço no servidor de formulários.
1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

   Selecione um domínio existente ou clique em Novo domínio empresarial.

1. Para criar um domínio, clique em Novo domínio empresarial ou Novo domínio híbrido. Para editar um domínio existente, clique no nome do domínio.
1. Selecione Ativar apenas no provisionamento de tempo.

   ***observação **: Se a caixa de seleção Ativar provisionamento just in time estiver ausente, clique em Início > Configurações > Gerenciamento de usuário > Configuração > Atributos avançados do sistema e clique em Recarregar.*

1. Adicionar provedores de autenticação. Ao adicionar provedores de autenticação, na tela Nova Autenticação, selecione um Criador de Identidade e Provedor de Atribuição registrado. (Consulte [Configuração de provedores de autenticação](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salve o domínio.
