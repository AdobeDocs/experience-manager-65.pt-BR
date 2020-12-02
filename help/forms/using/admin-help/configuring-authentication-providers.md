---
title: Configurar provedores de autenticação
seo-title: Configurar provedores de autenticação
description: Adicione, edite ou exclua provedores de autenticação, altere as configurações de autenticação e leia sobre o provisionamento just-in-time dos usuários.
seo-description: Adicione, edite ou exclua provedores de autenticação, altere as configurações de autenticação e leia sobre o provisionamento just-in-time dos usuários.
uuid: 90e7690b-1ce0-4604-b58f-6dca4f2372cf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 31dd8db3-ddac-429e-82f8-8c5dc4ffc186
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# Configurando provedores de autenticação {#configuring-authentication-providers}

Domínios híbridos exigem pelo menos um provedor de autenticação e domínios corporativos exigem pelo menos um provedor de autenticação ou provedor de diretório.

Se você ativar o SSO usando o SPNEGO, adicione um provedor de autenticação Kerberos com o SPNEGO ativado e um provedor LDAP como backup. Essa configuração permite a autenticação do usuário com uma ID de usuário e senha se o SPNEGO não estiver funcionando. (Consulte [Habilitar SSO usando SPNEGO](/help/forms/using/admin-help/enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

## Adicionar um provedor de autenticação {#add-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em um domínio existente na lista. Se você estiver adicionando autenticação para um novo domínio, consulte [Adicionar um domínio corporativo](/help/forms/using/admin-help/adding-domains.md#add-an-enterprise-domain) ou [Adicionar um domínio híbrido](/help/forms/using/admin-help/adding-domains.md#add-a-hybrid-domain).
1. Clique em Adicionar autenticação e, na lista Provedor de autenticação, selecione um provedor, dependendo do mecanismo de autenticação que sua organização usa.
1. Forneça quaisquer informações adicionais necessárias na página. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. (Opcional) Clique em Testar para testar a configuração.
1. Clique em OK e em OK novamente.

## Editar um provedor de autenticação existente {#edit-an-existing-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Na página que é exibida, selecione o provedor de autenticação apropriado na lista e faça as alterações necessárias. (Consulte [Configurações de autenticação](configuring-authentication-providers.md#authentication-settings).)
1. Clique em OK.

## Excluir um provedor de autenticação {#delete-an-authentication-provider}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique no domínio apropriado na lista.
1. Marque as caixas de seleção dos provedores de autenticação a serem excluídos e clique em Excluir.
1. Clique em OK na página de confirmação que é exibida e clique em OK novamente.

## Configurações de autenticação {#authentication-settings}

As configurações a seguir estão disponíveis, dependendo do tipo de domínio e do tipo de autenticação escolhido.

### Configurações LDAP {#ldap-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação LDAP, poderá optar por usar o servidor LDAP especificado na configuração do diretório ou escolher um servidor LDAP diferente para usar na autenticação. Se você escolher um servidor diferente, seus usuários deverão existir em ambos os servidores LDAP.

Para usar o servidor LDAP especificado na configuração do diretório, selecione LDAP como provedor de autenticação e clique em OK.

Para usar um servidor LDAP diferente para realizar a autenticação, selecione LDAP como provedor de autenticação e marque a caixa de seleção Autenticação LDAP personalizada. As seguintes configurações são exibidas.

**Servidor:** (obrigatório) Nome de domínio totalmente qualificado (FQDN) do servidor de diretório. Por exemplo, para um computador chamado x na rede corp.example.com, o FQDN é x.corp.example.com. Um endereço IP pode ser usado no lugar do nome do servidor FQDN.

**Porta:** (Obrigatória) A porta que o servidor de diretório usa. Normalmente, 389 ou 636 se o protocolo SSL for usado para enviar informações de autenticação pela rede.

**SSL:** (Obrigatório) Especifica se o servidor de diretório usa SSL ao enviar dados pela rede. O padrão é Não. Quando definido como Sim, o certificado do servidor LDAP correspondente deve ser confiável pelo JRE (Java™ Runtime ambiente) do servidor de aplicativos.

**Vínculo**  (Obrigatório) Especifica como acessar o diretório.

**Anônimo:** nenhum nome de usuário ou senha é necessário.

**Usuário:** autenticação é necessária. Na caixa Nome, especifique o nome do registro do usuário que pode acessar o diretório. É melhor inserir o nome distinto (DN) completo da conta de usuário, como cn=Jane Doe, ou=user, dc=can, dc=com. Na caixa Senha, especifique a senha associada. Essas configurações são necessárias quando você seleciona Usuário como a opção Vínculo.

**Recuperar DNs de Base:** (Não obrigatório) Recupera os DNs de base e os exibe na lista suspensa. Essa configuração é útil quando você tem vários DNs de base e precisa selecionar um valor.

**DN base:**  (obrigatório) usado como ponto de partida para sincronizar usuários e grupos da hierarquia LDAP. É melhor especificar um DN básico no nível mais baixo da hierarquia que abrange todos os usuários e grupos que precisam ser sincronizados para serviços. Não inclua o DN do usuário nesta configuração. Para sincronizar um usuário específico, use a configuração Filtro de pesquisa.

**Preencha a página com:** (Não obrigatório) Quando selecionada, preenche os atributos nas páginas de configurações de Usuário e Grupo com os valores LDAP padrão correspondentes.

**Filtro de pesquisa:**  (obrigatório) O filtro de pesquisa a ser usado para localizar o registro associado ao usuário. Consulte Sintaxe do filtro de pesquisa.

### Configurações Kerberos {#kerberos-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação Kerberos, as seguintes configurações estarão disponíveis.

**DNS IP:** o endereço IP DNS do servidor no qual os formulários AEM estão em execução. No Windows, você pode determinar esse endereço IP executando ipconfig /all na linha de comando.

**Host KDC: nome de host** totalmente qualificado ou endereço IP do servidor Ative Diretory usado para autenticação.

**Usuário do serviço:** se você estiver usando o Ative Diretory 2003, esse valor será o mapeamento criado para o principal do serviço no formulário  `HTTP/<server name>`. Se você estiver usando o Ative Diretory 2008, esse valor será a ID de logon do principal do serviço. Por exemplo, suponha que o principal do serviço seja chamado de um spnego, a ID do usuário seja spnegodemo e o mapeamento seja HTTP/example.corp.suaempresa.com. Com o Ative Diretory 2003, você define Usuário do Serviço como HTTP/example.corp.suaempresa.com. Com o Ative Diretory 2008, você define Usuário do Serviço como spnegodemo. (Consulte Habilitar SSO usando SPNEGO.)

**Realm de serviço:nome** de domínio do Ative Diretory

**Senha do serviço:senha do usuário** do serviço

**Habilitar SPNEGO:** Habilita o uso de SPNEGO para logon único (SSO). (Consulte Habilitar SSO usando SPNEGO.)

### Configurações SAML {#saml-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar a autenticação SAML, as seguintes configurações estarão disponíveis. Para obter informações sobre configurações SAML adicionais, consulte [Definir configurações do provedor de serviço SAML](/help/forms/using/admin-help/configure-saml-service-provider-settings.md#configure-saml-service-provider-settings).

**Selecione um arquivo de metadados do provedor de identidade SAML a ser importado:** Clique em Procurar para selecionar um arquivo de metadados do provedor de identidade SAML gerado do seu IDP e clique em Importar. Detalhes do IDP são exibidos.

**Título:** alias do URL denotado pela EntityID. O título também é exibido na página de logon para usuários corporativos e locais.

**O Provedor de identidade oferece suporte à autenticação básica do cliente: a autenticação básica do** cliente é usada quando o IDP usa um perfil SAML de resolução de artefato. Neste perfil, o Gerenciamento de usuários se conecta de volta a um serviço da Web em execução no IDP para recuperar a asserção SAML real. O IDP pode exigir autenticação. Se o IDP exigir autenticação, selecione essa opção e especifique um nome de usuário e senha nas caixas fornecidas.

**Propriedades personalizadas:** permite especificar propriedades adicionais. As propriedades adicionais são pares name=value separados por novas linhas.

As seguintes propriedades personalizadas são necessárias se a vinculação de artefato for usada.

* Adicione a seguinte propriedade personalizada para especificar um nome de usuário que representa o Provedor de serviço de formulários AEM, que será usado para autenticação no serviço de Resolução de artefatos IDP.
   `saml.idp.resolve.username=<username>`

* Adicione a seguinte propriedade personalizada para especificar a senha para o usuário especificado em `saml.idp.resolve.username`.
   `saml.idp.resolve.password=<password>`

* Adicione a seguinte propriedade personalizada para permitir que o provedor de serviço ignore a validação do certificado ao estabelecer a conexão com o serviço de Resolução de artefato por SSL.
   `saml.idp.resolve.ignorecert=true`

### Configurações personalizadas {#custom-settings}

Se você estiver configurando a autenticação para um domínio corporativo ou híbrido e selecionar Autenticação personalizada, selecione o nome do provedor de autenticação personalizada.

## Provisionamento just-in-time de usuários {#just-in-time-provisioning-of-users}

O provisionamento just-in-time cria automaticamente um usuário no banco de dados Gerenciamento de usuários depois que ele é autenticado com êxito por meio de um provedor de autenticação. As funções e grupos relevantes também são atribuídos dinamicamente ao novo usuário. Você pode ativar o provisionamento just-in-time para domínios corporativos e híbridos.

Este procedimento descreve como a autenticação tradicional funciona em formulários AEM:

1. Quando um usuário tenta fazer logon em formulários AEM, o Gerenciamento de usuários transmite suas credenciais sequencialmente a todos os provedores de autenticação disponíveis. (As credenciais de logon incluem combinação de nome de usuário/senha, ticket Kerberos, assinatura PKCS7 e assim por diante.)
1. O provedor de autenticação valida as credenciais.
1. O provedor de autenticação verifica se o usuário existe no banco de dados Gerenciamento de usuários. Os seguintes status são possíveis:

   **** ExisteSe o usuário estiver atual e desbloqueado, o Gerenciamento de usuários retornará a autenticação bem-sucedida. No entanto, se o usuário não estiver atualizado ou estiver bloqueado, o Gerenciamento de usuários retornará uma falha de autenticação.

   **Não** existeO Gerenciamento de usuários retorna a falha de autenticação.

   **O Gerenciamento de** Usuário Inválido retorna a falha de autenticação.

1. O resultado retornado pelo provedor de autenticação é avaliado. Se o provedor de autenticação retornar a autenticação bem-sucedida, o usuário poderá fazer logon. Caso contrário, o Gerenciamento de usuários verifica o próximo provedor de autenticação (etapas 2-3).
1. A falha de autenticação será retornada se nenhum provedor de autenticação disponível validar as credenciais do usuário.

Quando o provisionamento just-in-time é ativado, novos usuários são criados dinamicamente no Gerenciamento de usuários se um dos provedores de autenticação validar suas credenciais. (Após a etapa 3 do procedimento acima.)

Sem provisionamento just-in-time, quando um usuário é autenticado com êxito, mas não é encontrado no banco de dados Gerenciamento de usuários, a autenticação falha. O provisionamento just-in-time adiciona uma etapa no procedimento de autenticação para criar o usuário e atribuir funções e grupos ao usuário.

### Habilitar provisionamento just-in-time para um domínio {#enable-just-in-time-provisioning-for-a-domain}

1. Escreva um container de serviço que implemente as interfaces IdentityCreator e AssignmentProvider. (Consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63).)
1. Implante o container de serviço no servidor de formulários.
1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.

   Selecione um domínio existente ou clique em Novo domínio corporativo.

1. Para criar um domínio, clique em Novo domínio corporativo ou Novo domínio híbrido. Para editar um domínio existente, clique no nome do domínio.
1. Selecione Ativar apenas no provisionamento de tempo.

   ***observação **: Se a caixa de seleção Ativar apenas no provisionamento de tempo estiver ausente, clique em Início > Configurações > Gerenciamento do usuário > Configuração > Atributos avançados do sistema e clique em Recarregar.*

1. Adicione provedores de autenticação. Ao adicionar provedores de autenticação, na tela Nova autenticação, selecione um Criador de identidade e Provedor de atribuição registrados. (Consulte [Configuração de provedores de autenticação](configuring-authentication-providers.md#configuring-authentication-providers).)
1. Salve o domínio.

