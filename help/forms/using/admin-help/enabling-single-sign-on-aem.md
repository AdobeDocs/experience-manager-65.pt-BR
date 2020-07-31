---
title: Habilitar logon único em formulários AEM
seo-title: Habilitar logon único em formulários AEM
description: Saiba como ativar o logon único (SSO) usando cabeçalhos HTTP e SPNEGO.
seo-description: Saiba como ativar o logon único (SSO) usando cabeçalhos HTTP e SPNEGO.
uuid: 2bc08b4f-dcbe-4a16-9025-32fc14605e13
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ee54d9d4-190d-4665-925a-9740ac65fbd5
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 0%

---


# Habilitar logon único em formulários AEM{#enabling-single-sign-on-in-aem-forms}

AEM formulários fornece duas maneiras de habilitar o logon único (SSO) - cabeçalhos HTTP e SPNEGO.

Quando o SSO for implementado, as páginas de logon do usuário dos formulários AEM não serão obrigatórias e não aparecerão se o usuário já estiver autenticado por meio de seu portal de empresa.

Se AEM formulários não puderem autenticar um usuário usando um desses métodos, o usuário será redirecionado para uma página de logon.

## Habilitar SSO usando cabeçalhos HTTP {#enable-sso-using-http-headers}

Você pode usar a página Configuração do portal para ativar o logon único (SSO) entre aplicativos e qualquer aplicativo que suporte a transmissão da identidade pelo cabeçalho HTTP. Quando o SSO for implementado, as páginas de logon do usuário dos formulários AEM não serão obrigatórias e não aparecerão se o usuário já estiver autenticado por meio de seu portal de empresa.

Você também pode ativar o SSO usando o SPNEGO. (Consulte [Ativar SSO usando o SPNEGO](enabling-single-sign-on-aem.md#enable-sso-using-spnego).)

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos do portal.
1. Selecione Sim para ativar o SSO. Se você selecionar Não, as configurações restantes na página não estarão disponíveis.
1. Defina as opções restantes na página, conforme necessário, e clique em OK:

   * **Tipo SSO:** (Obrigatório) Selecione Cabeçalho HTTP para ativar o SSO usando cabeçalhos HTTP.
   * **Cabeçalho HTTP para o identificador do usuário:** (Obrigatório) Nome do cabeçalho cujo valor contém o identificador exclusivo do usuário conectado. O Gerenciamento de usuários usa esse valor para localizar o usuário no banco de dados de Gerenciamento de usuários. O valor obtido a partir desse cabeçalho deve corresponder ao identificador exclusivo do usuário que está sincronizado a partir do diretório LDAP. (Consulte Configurações [do usuário](/help/forms/using/admin-help/adding-configuring-users.md#user-settings).)
   * **O valor do identificador mapeia para a ID de usuário do usuário em vez do identificador exclusivo do usuário:** Mapeia o valor identificador exclusivo do usuário para a ID do usuário. Selecione essa opção se o identificador exclusivo do usuário for um valor binário que não pode ser facilmente propagado pelos cabeçalhos HTTP (por exemplo, objectGUID se você estiver sincronizando usuários do Ative Diretory).
   * **Cabeçalho HTTP para o domínio:** (Não obrigatório) Nome do cabeçalho cujo valor contém o nome do domínio. Use essa configuração somente se nenhum cabeçalho HTTP único identificar o usuário. Use essa configuração para casos em que existem vários domínios e o identificador exclusivo é exclusivo somente em um domínio. Nesse caso, especifique o nome do cabeçalho nessa caixa de texto e especifique o mapeamento de domínio para os vários domínios na caixa de mapeamento Domínio. (Consulte [Edição e conversão de domínios](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)existentes.)
   * **Mapeamento de domínio:** (Obrigatório) Especifica o mapeamento para vários domínios no formato *header value=domain name*.

      Por exemplo, considere uma situação em que o cabeçalho HTTP de um domínio seja domainName e ele possa ter valores de domain1, domain2 ou domain3. Nesse caso, use o mapeamento de domínio para mapear os valores de domainName para nomes de domínio do Gerenciamento de usuários. Cada mapeamento deve estar em uma linha diferente:

      domain1=UMdomain1

      domain2=UMdomain2

      domain3=UMdomain3

### Configurar referenciadores permitidos {#configure-allowed-referers}

Para obter as etapas de configuração de referenciadores permitidos, consulte [Configurar referenciadores](/help/forms/using/admin-help/preventing-csrf-attacks.md#configure-allowed-referers)permitidos.

## Habilitar SSO usando SPNEGO {#enable-sso-using-spnego}

Você pode usar o Mecanismo de Negociação GSSAPI Simples e Protegido (SPNEGO) para ativar o logon único (SSO) ao usar o Ative Diretory como seu servidor LDAP em um ambiente do Windows. Quando o SSO estiver ativado, as páginas de logon de usuário dos formulários AEM não são obrigatórias e não são exibidas.

Você também pode ativar o SSO usando cabeçalhos HTTP. (Consulte [Ativar SSO usando cabeçalhos](enabling-single-sign-on-aem.md#enable-sso-using-http-headers)HTTP.)

>[!NOTE]
>
>AEM Forms no JEE não suportam a configuração de SSO usando Kerberos/SPNEGO em vários ambientes de domínio filho.

1. Decida qual domínio usar para ativar o SSO. O servidor de formulários AEM e os usuários devem fazer parte do mesmo domínio do Windows ou domínio confiável.
1. No Ative Diretory, crie um usuário que represente o servidor de formulários AEM. (Consulte [Criar uma conta](enabling-single-sign-on-aem.md#create-a-user-account)de usuário.) Se você estiver configurando mais de um domínio para usar o SPNEGO, verifique se as senhas de cada um desses usuários são diferentes. Se as senhas não forem diferentes, o SSO SPNEGO não funcionará.
1. Mapeie o nome do principal do serviço. (Consulte [Mapear um Nome Principal de Serviço (SPN)](enabling-single-sign-on-aem.md#map-a-service-principal-name-spn).)
1. Configure o controlador de domínio. (Consulte [Evitar falhas](enabling-single-sign-on-aem.md#prevent-kerberos-integrity-check-failures)de verificação de integridade do Kerberos.)
1. Adicione ou edite um domínio corporativo conforme descrito em [Adicionar domínios](/help/forms/using/admin-help/adding-domains.md#adding-domains) ou [Editar e converter domínios](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains)existentes. Ao criar ou editar o domínio corporativo, execute estas tarefas:

   * Adicione ou edite um diretório que contenha suas informações do Ative Diretory.
   * Adicione LDAP como um provedor de autenticação.
   * Adicione Kerberos como um provedor de autenticação. Forneça as seguintes informações na página Nova Autenticação ou Editar Autenticação para Kerberos:

      * **Provedor de autenticação:** Kerberos
      * **IP DNS:** O endereço IP DNS do servidor no qual os formulários AEM estão sendo executados. Você pode determinar esse endereço IP executando `ipconfig/all` na linha de comando.
      * **Host KDC:** Nome do host totalmente qualificado ou endereço IP do servidor Ative Diretory usado para autenticação
      * **Usuário do serviço:** O nome do principal de serviço (SPN) passado para a ferramenta KtPass. No exemplo usado anteriormente, o usuário do serviço é `HTTP/lcserver.um.lc.com`.
      * **Realm de serviço:** Nome de domínio do Ative Diretory. No exemplo usado anteriormente, o nome de Domínio é `UM.LC.COM.`
      * **Senha do serviço:** Senha do usuário do serviço. No exemplo usado anteriormente, a senha do serviço é `password`.
      * **Ativar SPNEGO:** Permite o uso de SPNEGO para logon único (SSO). Selecione essa opção.

1. Defina as configurações do navegador do cliente SPNEGO. (Consulte [Configuração das configurações](enabling-single-sign-on-aem.md#configuring-spnego-client-browser-settings)do navegador cliente SPNEGO.)

### Criar uma conta de usuário {#create-a-user-account}

1. No SPNEGO, registre um serviço como um usuário no Ative Diretory no controlador de domínio para representar formulários AEM. No controlador de domínio, vá para Menu Start > Ferramentas administrativas > Usuários e computadores do Ative Diretory. Se Ferramentas administrativas não estiver no menu Start, use o Painel de controle do Campaign.
1. Clique na pasta Usuários para exibir uma lista de usuários.
1. Clique com o botão direito do mouse na pasta do usuário e selecione Novo > Usuário.
1. Digite o Nome/Sobrenome e o Nome de login do usuário e clique em Avançar. Por exemplo, defina os seguintes valores:

   * **Nome**: umspnego
   * **Nome** de logon do usuário: spnegodemo

1. Digite uma senha. Por exemplo, defina-a como *senha*. Verifique se a opção Senha nunca expira está selecionada e se nenhuma outra opção está selecionada.
1. Clique em Avançar e em Concluir.

### Mapear um Nome Principal de Serviço (SPN) {#map-a-service-principal-name-spn}

1. Obtenha o utilitário KtPass. Este utilitário é usado para mapear um SPN para um REALM. Você pode obter o utilitário KtPass como parte do pacote de ferramentas do Windows Server ou do Kit de recursos. (Consulte Ferramentas [de suporte do](https://support.microsoft.com/kb/892777)Windows Server 2003 Service Pack 1.)
1. Em um prompt de comando, execute `ktpass` usando os seguintes argumentos:

   `ktpass -princ HTTP/`*host *`@`*REALM* `-mapuser`*user *

   Por exemplo, digite o seguinte texto:

   `ktpass -princ HTTP/lcserver.um.lc.com@UM.LC.COM -mapuser spnegodemo`

   Os valores que devem ser fornecidos são descritos a seguir:

   **host:** Nome totalmente qualificado do servidor de formulários ou qualquer URL exclusivo. Neste exemplo, ele é definido como lcserver.um.lc.com.

   **REALM:** O realm do Ative Diretory para o controlador de domínio. Neste exemplo, ele é definido como UM.LC.COM. Certifique-se de inserir o realm em caracteres em maiúsculas. Para determinar o realm do Windows 2003, conclua as seguintes etapas:

   * Clique com o botão direito do mouse em Meu computador e selecione Propriedades
   * Clique na guia Nome do computador. O valor Nome de domínio é o nome do realm.

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

### Evitar falhas na verificação de integridade do Kerberos {#prevent-kerberos-integrity-check-failures}

1. No controlador de domínio, vá para Menu Start > Ferramentas administrativas > Usuários e computadores do Ative Diretory. Se Ferramentas administrativas não estiver no menu Start, use o Painel de controle do Campaign.
1. Clique na pasta Usuários para exibir uma lista de usuários.
1. Clique com o botão direito do mouse na conta de usuário criada em uma tarefa anterior. Neste exemplo, a conta de usuário é `spnegodemo`.
1. Clique em Redefinir senha.
1. Digite e confirme a mesma senha que você digitou anteriormente. Neste exemplo, está definido como `password`.
1. Desmarque Alterar senha no próximo logon e clique em OK.

### Configuração do navegador cliente SPNEGO {#configuring-spnego-client-browser-settings}

Para que a autenticação baseada em SPNEGO funcione, o computador cliente deve fazer parte do domínio no qual a conta de usuário é criada. Você também deve configurar o navegador cliente para permitir a autenticação com base em SPNEGO. Além disso, o site que requer autenticação com base em SPNEGO deve ser um site confiável.

Se o servidor for acessado usando o nome do computador, como https://lcserver:8080, nenhuma configuração é necessária para o Internet Explorer. Se você digitar um URL que não contenha nenhum ponto (&quot;.&quot;), o Internet Explorer tratará o site como um site da intranet local. Se você estiver usando um nome totalmente qualificado para o site, o site deverá ser adicionado como um site confiável.

**Configurar o Internet Explorer 6.x**

1. Vá até Ferramentas > Opções da Internet e clique na guia Segurança.
1. Clique no ícone Intranet local e, em seguida, clique em Sites.
1. Clique em Avançado e, na caixa Adicionar este site à região, digite o URL do servidor de formulários. For example, type `https://lcserver.um.lc.com`
1. Clique em OK até que todas as caixas de diálogo sejam fechadas.
1. Teste a configuração acessando o URL do servidor de formulários AEM. Por exemplo, na caixa URL do navegador, digite `https://lcserver.um.lc.com:8080/um/login?um_no_redirect=true`

**Configurar o Mozilla Firefox**

1. Na caixa URL do navegador, digite `about:config`

   A caixa de diálogo about:config - Mozilla Firefox é exibida.

1. Na caixa Filtro, digite `negotiate`
1. Na lista mostrada, clique em network.exchange-auth.trusted-uri e digite um dos seguintes comandos, conforme apropriado para o seu ambiente:

   `.um.lc.com`- Configura o Firefox para permitir o SPNEGO para qualquer URL que termine com um.lc.com. Certifique-se de incluir o ponto (&quot;.&quot;) no começo.

   `lcserver.um.lc.com` - Configura o Firefox para permitir o SPNEGO somente para seu servidor específico. Não start esse valor com um ponto (&quot;.&quot;).

1. Teste a configuração acessando o aplicativo. A página de boas-vindas do aplicativo de público alvo deve ser exibida.

