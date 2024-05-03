---
title: Habilitar logon único em formulários AEM
description: Saiba como habilitar o logon único (SSO) usando cabeçalhos HTTP e SPNEGO.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 89561ed0-d094-4ef7-9bc1-bde11f3c5bc3
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1520'
ht-degree: 0%

---

# Habilitar logon único em formulários AEM{#enabling-single-sign-on-in-aem-forms}

Os formulários AEM fornecem duas maneiras de ativar o logon único (SSO) - cabeçalhos HTTP e SPNEGO.

Quando o SSO é implementado, as páginas de logon do usuário dos formulários AEM não são necessárias e não aparecem se o usuário já estiver autenticado por meio do portal da empresa.

Se os formulários AEM não puderem autenticar um usuário usando um desses métodos, o usuário será redirecionado para uma página de logon.

## Habilitar SSO usando cabeçalhos HTTP {#enable-sso-using-http-headers}

Você pode usar a página Configuração do Portal para habilitar o logon único (SSO) entre aplicativos e qualquer aplicativo que ofereça suporte à transmissão da identidade pelo cabeçalho HTTP. Quando o SSO é implementado, as páginas de logon do usuário dos formulários AEM não são necessárias e não aparecem se o usuário já estiver autenticado por meio do portal da empresa.

Você também pode ativar o SSO usando o SPNEGO. (Consulte [Habilitar SSO usando SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos do portal.
1. Selecione Sim para ativar o SSO. Se você selecionar Não, as configurações restantes na página não estarão disponíveis.
1. Defina as opções restantes na página, conforme necessário, e clique em OK:

   * **Tipo de SSO:** (Obrigatório) Selecione Cabeçalho HTTP para ativar o SSO usando cabeçalhos HTTP.
   * **Cabeçalho HTTP para o identificador do usuário:** (Obrigatório) Nome do cabeçalho cujo valor contém o identificador exclusivo do usuário conectado. O Gerenciamento de usuários usa esse valor para localizar o usuário no banco de dados de Gerenciamento de usuários. O valor obtido desse cabeçalho deve corresponder ao identificador exclusivo do usuário que está sincronizado do diretório LDAP. (Consulte [Configurações do usuário](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **O valor do identificador mapeia para a ID de usuário do usuário em vez do identificador exclusivo do usuário:** Mapeia o valor do identificador exclusivo do usuário para a ID do usuário. Selecione esta opção se o identificador exclusivo do usuário for um valor binário que não pode ser facilmente propagado por cabeçalhos HTTP (por exemplo, objectGUID se você estiver sincronizando usuários do Ative Diretory).
   * **Cabeçalho HTTP para o domínio:** (Não obrigatório) Nome do cabeçalho cujo valor contém o nome de domínio. Use essa configuração somente se nenhum único cabeçalho HTTP identificar exclusivamente o usuário. Use essa configuração para casos em que existem vários domínios e o identificador exclusivo é exclusivo somente em um domínio. Nesse caso, especifique o nome do cabeçalho nessa caixa de texto e especifique o mapeamento de domínio para os vários domínios na caixa Mapeamento de domínio. (Consulte [Edição e conversão de domínios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).)
   * **Mapeamento de domínio:** (Obrigatório) Especifica o mapeamento para vários domínios no formato *valor do cabeçalho=nome do domínio*.

     Por exemplo, considere uma situação em que o cabeçalho HTTP de um domínio é domainName e pode ter valores de domain1, domain2 ou domain3. Nesse caso, use o mapeamento de domínio para mapear os valores de domainName para nomes de domínio do User Management. Cada mapeamento deve estar em uma linha diferente:

     domain1=UMdomain1

     domain2=UMdomain2

     domain3=UMdomain3

### Configurar referenciadores permitidos {#configure-allowed-referers}

Para obter as etapas para configurar referenciadores permitidos, consulte [Configurar referenciadores permitidos](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers).

## Habilitar SSO usando SPNEGO {#enable-sso-using-spnego}

Você pode usar o Mecanismo de Negociação GSSAPI Simples e Protegido (SPNEGO) para habilitar o logon único (SSO) ao usar o Ative Diretory como seu servidor LDAP em um ambiente Windows. Quando o SSO está ativado, as páginas de logon do usuário dos formulários AEM não são necessárias e não são exibidas.

Você também pode ativar o SSO usando cabeçalhos HTTP. (Consulte [Habilitar SSO usando cabeçalhos HTTP](enabling-single-sign-on-aem.md#enable-sso-using-http-headers).)

>[!NOTE]
>
>O AEM Forms no JEE não é compatível com a configuração do SSO usando Kerberos/SPNEGO em vários ambientes de domínio filho.

1. Decida qual domínio usar para habilitar o SSO. O AEM Forms Server e os usuários devem fazer parte do mesmo domínio do Windows ou domínio confiável.
1. No Ative Diretory, crie um usuário que represente o AEM Forms Server. (Consulte [Criar uma conta de usuário](enabling-single-sign-on-aem.md#create-a-user-account).) Se você estiver configurando mais de um domínio para usar o SPNEGO, certifique-se de que as senhas de cada um desses usuários sejam diferentes. Se as senhas não forem diferentes, o SPNEGO SSO não funcionará.
1. Mapeie o nome da entidade de serviço. (Consulte [Mapear um SPN (Nome da Entidade de Serviço)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configure o controlador de domínio. (Consulte [Evitar falhas de verificação de integridade Kerberos](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures).)
1. Adicione ou edite um domínio enterprise conforme descrito em [Adicionar domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains) ou [Edição e conversão de domínios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains). Ao criar ou editar o domínio enterprise, execute estas tarefas:

   * Adicione ou edite um diretório que contenha suas informações do Ative Diretory.
   * Adicione o LDAP como um provedor de autenticação.
   * Adicione o Kerberos como um provedor de autenticação. Forneça as seguintes informações na página Nova ou Editar Autenticação do Kerberos:

      * **Provedor de autenticação:** Kerberos
      * **IP DNS:** O endereço IP DNS do servidor onde os formulários AEM estão sendo executados. Você pode determinar esse endereço IP executando `ipconfig/all` na linha de comando.
      * **Host KDC:** Nome de host ou endereço IP totalmente qualificado do servidor do Ative Diretory usado para autenticação
      * **Usuário de serviço:** O SPN (nome da entidade de serviço) passado para a ferramenta KtPass. No exemplo usado anteriormente, o usuário do serviço é `HTTP/lcserver.um.lc.com`.
      * **Domínio de Serviço:** Nome de domínio do Ative Diretory. No exemplo usado anteriormente, o Nome do domínio é `UM.LC.COM.`
      * **Senha do serviço:** Senha do usuário do serviço. No exemplo usado anteriormente, a senha do serviço é `password`.
      * **Ativar SPNEGO:** Habilita o uso do SPNEGO para logon único (SSO). Selecione esta opção.

1. Defina as configurações do navegador do cliente SPNEGO. (Consulte [Definição das configurações do navegador do cliente SPNEGO](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings).)

### Criar uma conta de usuário {#create-a-user-account}

1. No SPNEGO, registre um serviço como um usuário no Ative Diretory no controlador de domínio para representar formulários AEM. No controlador de domínio, acesse Menu Iniciar > Ferramentas Administrativas > Usuários e Computadores do Ative Diretory. Se Ferramentas administrativas não estiver no menu Iniciar, use o Painel de controle.
1. Clique na pasta Usuários para exibir uma lista de usuários.
1. Clique com o botão direito do mouse na pasta do usuário e selecione Novo > Usuário.
1. Digite o Nome/Sobrenome e o Nome de logon do usuário e clique em Avançar. Por exemplo, defina os seguintes valores:

   * **Nome**: umspnego
   * **Nome de logon do usuário**: spnegodemo

1. Digite uma senha. Por exemplo, defina como *senha*. Certifique-se de que a opção Senha nunca expira esteja selecionada e que nenhuma outra opção esteja selecionada.
1. Clique em Avançar e em Concluir.

### Mapear um SPN (Nome da Entidade de Serviço) {#map-a-service-principal-name-spn}

1. Obtenha o utilitário KtPass. Esse utilitário é usado para mapear um SPN para um REALM. Você pode obter o utilitário KtPass como parte do Pacote de ferramentas ou Kit de recursos do Windows Server. (Consulte [Ferramentas de Suporte do Windows Server 2003 Service Pack 1](https://support.microsoft.com/kb/892777).)
1. Em um prompt de comando, execute `ktpass` usando os seguintes argumentos:

   `ktpass -princ HTTP/`*host* `@`*DOMÍNIO* `-mapuser`*usuário*

   Por exemplo, digite o seguinte texto:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Os valores que você deve fornecer são descritos a seguir:

   **host:** Nome totalmente qualificado do servidor do Forms ou qualquer URL exclusivo. Neste exemplo, ele é definido como lcserver.um.lc.com.

   **REALM:** O realm do Ative Diretory para o controlador de domínio. Neste exemplo, ele é definido como UM.LC.COM. Certifique-se de informar o realm em caracteres maiúsculos. Para determinar o realm do Windows 2003, conclua as seguintes etapas:

   * Clique com o botão direito em Meu computador e selecione Propriedades
   * Clique na guia Nome do computador. O valor Nome do Domínio é o nome do realm.

   **usuário:** O nome de logon da conta de usuário criada na tarefa anterior. Neste exemplo, está definido como spnegodemo.

Se você encontrar este erro:

```shell
DsCrackNames returned 0x2 in the name entry for spnegodemo.
ktpass:failed getting target domain for specified user.
```

tente especificar o usuário como spnegodemo@um.lc.com:

```shell
ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo
```

### Evitar falhas de verificação de integridade Kerberos {#prevent-kerberos-integrity-check-failures}

1. No controlador de domínio, acesse Menu Iniciar > Ferramentas Administrativas > Usuários e Computadores do Ative Diretory. Se Ferramentas administrativas não estiver no menu Iniciar, use o Painel de controle.
1. Clique na pasta Usuários para exibir uma lista de usuários.
1. Clique com o botão direito do mouse na conta de usuário criada em uma tarefa anterior. Neste exemplo, a conta do usuário é `spnegodemo`.
1. Clique em Redefinir senha.
1. Digite e confirme a mesma senha digitada anteriormente. Neste exemplo, está definido como `password`.
1. Desmarque Alterar senha no próximo logon e clique em OK.

### Definição das configurações do navegador do cliente SPNEGO {#configuring-spnego-client-browser-settings}

Para que a autenticação baseada em SPNEGO funcione, o computador cliente deve fazer parte do domínio em que a conta de usuário é criada. Você também deve configurar o navegador do cliente para permitir a autenticação baseada em SPNEGO. Além disso, o site que requer autenticação baseada no SPNEGO deve ser um site confiável.

Se o servidor for acessado usando o nome do computador, como https://lcserver:8080, nenhuma configuração será necessária para o Internet Explorer. Se você inserir um URL que não contenha pontos (&quot;.&quot;), o Internet Explorer tratará o site como um site da intranet local. Se você estiver usando um nome totalmente qualificado para o site, ele deverá ser adicionado como um site confiável.

**Configurar o Internet Explorer 6.x**

1. Vá para Ferramentas > Opções da Internet e clique na guia Segurança.
1. Clique no ícone Intranet local e em Sites.
1. Clique em Avançado e, na caixa Adicionar este site à zona, digite o URL do servidor do Forms. Por exemplo, digite `https://lcserver.um.lc.com`
1. Clique em OK até que todas as caixas de diálogo sejam fechadas.
1. Teste a configuração acessando o URL do servidor do AEM Forms. Por exemplo, na caixa URL do navegador, digite `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurar o Mozilla Firefox**

1. Na caixa URL do navegador, digite `about:config`

   A caixa de diálogo about:config - Mozilla Firefox é exibida.

1. Na caixa Filtro, digite `negotiate`
1. Na lista mostrada, clique em network.negotiation-auth.trusted-uri e digite um dos seguintes comandos conforme apropriado para seu ambiente:

   `.um.lc.com`- Configura o Firefox para permitir SPNEGO para qualquer URL que termine com um.lc.com. Certifique-se de incluir o ponto (&quot;.&quot;) no início.

   `lcserver.um.lc.com` - Configura o Firefox para permitir o SPNEGO somente para seu servidor específico. Não inicie este valor com um ponto (&quot;.&quot;).

1. Teste a configuração acessando o aplicativo. A página de boas-vindas do aplicativo de destino deve ser exibida.
