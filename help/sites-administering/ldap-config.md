---
title: Configuração do LDAP com AEM 6
seo-title: Configuração do LDAP com AEM 6
description: Saiba como configurar o LDAP com AEM.
seo-description: Saiba como configurar o LDAP com AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 0%

---


# Configuração do LDAP com AEM 6 {#configuring-ldap-with-aem}

O LDAP (o diretório **L** Leve **D** A **A** Access **P** Protocolo) é utilizado para aceder aos serviços de diretório centralizados. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuário, pois elas podem ser acessadas por vários aplicativos. Um desses servidores LDAP é o Ative Diretory. O LDAP é frequentemente usado para obter o Single Sign On, que permite que o usuário acesse vários aplicativos depois de fazer logon uma vez.

As contas de usuário podem ser sincronizadas entre o servidor LDAP e o repositório, com os detalhes da conta LDAP sendo salvos no repositório. Isso permite que as contas sejam atribuídas a grupos de repositório para alocar as permissões e os privilégios necessários.

O repositório usa a autenticação LDAP para autenticar esses usuários, com credenciais sendo enviadas ao servidor LDAP para validação, o que é necessário antes de permitir o acesso ao repositório. Para melhorar o desempenho, as credenciais validadas com êxito podem ser armazenadas em cache pelo repositório, com um tempo limite de expiração para garantir que a revalidação ocorra após um período apropriado.

Quando uma conta é removida do servidor LDAP, a validação não é mais concedida e, portanto, o acesso ao repositório é negado. Detalhes das contas LDAP salvas no repositório também podem ser expurgados.

O uso dessas contas é transparente para os usuários, eles não veem diferença entre as contas de usuário e de grupo criadas a partir do LDAP e as criadas exclusivamente no repositório.

No AEM 6, o suporte a LDAP vem com uma nova implementação que requer um tipo de configuração diferente do das versões anteriores.

Todas as configurações LDAP agora estão disponíveis como configurações OSGi. Eles podem ser configurados pelo console de Gerenciamento da Web em:
`https://serveraddress:4502/system/console/configMgr`

Para que o LDAP funcione com AEM, é necessário criar três configurações OSGi:

1. Um provedor de identidade LDAP (IDP).
1. Um Manipulador De Sincronização.
1. Um módulo de logon externo.

>[!NOTE]
>
>Assista [Módulo de logon externo do Oak - Autenticação com LDAP e Além de](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) para aprofundar os módulos de logon externos.
>
>Para ler um exemplo de configuração de Experience Manager com Apache DS, consulte [Configurar o Adobe Experience Manager 6.5 para usar o Apache Diretory Service.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Configuração Do Provedor De Identidade LDAP {#configuring-the-ldap-identity-provider}

O Provedor de identidade LDAP é usado para definir como os usuários são recuperados do servidor LDAP.

Ele pode ser encontrado no console de gerenciamento sob o nome **Apache Jackrabbit Oak LDAP Identity Provider**.

As seguintes opções de configuração estão disponíveis para o provedor de identidade LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do provedor LDAP</strong></td>
   <td>Nome desta configuração de provedor LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nome do host do servidor LDAP</strong><br /> </td>
   <td>Nome do host do servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Porta do servidor LDAP</strong></td>
   <td>Porta do servidor LDAP</td>
  </tr>
  <tr>
   <td><strong>Usar SSL</strong></td>
   <td>Indica se uma conexão SSL (LDAPs) deve ser usada.</td>
  </tr>
  <tr>
   <td><strong>Usar TLS</strong></td>
   <td>Indica se o TLS deve ser iniciado em conexões.</td>
  </tr>
  <tr>
   <td><strong>Desativar verificação de certificado</strong></td>
   <td>Indica se a validação do certificado do servidor deve ser desativada.</td>
  </tr>
  <tr>
   <td><strong>Ligar DN</strong></td>
   <td>DN do usuário para autenticação. Se isso for deixado em branco, um vínculo anônimo será executado.</td>
  </tr>
  <tr>
   <td><strong>Vincular senha</strong></td>
   <td>Senha do usuário para autenticação</td>
  </tr>
  <tr>
   <td><strong>Tempo limite de pesquisa</strong></td>
   <td>Tempo até que a pesquisa atinja o tempo limite</td>
  </tr>
  <tr>
   <td><strong>Máximo de ativos do pool de administração</strong></td>
   <td>O tamanho máximo ativo do pool de conexões administrativas.</td>
  </tr>
  <tr>
   <td><strong>Máximo de ativos do pool de usuários</strong></td>
   <td>O tamanho máximo ativo do pool de conexões do usuário.</td>
  </tr>
  <tr>
   <td><strong>DN base do usuário</strong></td>
   <td>O DN para pesquisas de usuários</td>
  </tr>
  <tr>
   <td><strong>Classes de objetos de usuário</strong></td>
   <td>A lista de classes de objetos que uma entrada de usuário deve conter.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID do usuário</strong></td>
   <td>Nome do atributo que contém a ID do usuário.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra do usuário</strong></td>
   <td>Filtro LDAP extra a ser usado ao pesquisar usuários. O filtro final é formatado da seguinte forma: '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN do usuário</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>DN base do grupo</strong></td>
   <td>O DN de base para pesquisas de grupo.</td>
  </tr>
  <tr>
   <td><strong>Classes de objetos de grupo</strong></td>
   <td>A lista de classes de objetos que uma entrada de grupo deve conter.</td>
  </tr>
  <tr>
   <td><strong>Atributo do nome do grupo</strong></td>
   <td>Nome do atributo que contém o nome do grupo.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra do grupo</strong></td>
   <td>Filtro LDAP extra a ser usado ao procurar grupos. O filtro final está formatado como: '(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN de grupo</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>Atributo do membro do grupo</strong></td>
   <td>Atributo de grupo que contém os membros de um grupo.</td>
  </tr>
 </tbody>
</table>

## Configurando O Manipulador De Sincronização {#configuring-the-synchronization-handler}

O manipulador de sincronização definirá como os usuários e grupos do Provedor de identidades serão sincronizados com o repositório.

Ele está localizado no nome **Apache Jackrabbit Oak Default Sync Handler** no console de gerenciamento.

As seguintes opções de configuração estão disponíveis para o Manipulador de Sincronização:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do manipulador de sincronização</strong></td>
   <td>Nome da configuração de sincronização.</td>
  </tr>
  <tr>
   <td><strong>Tempo de expiração do usuário</strong></td>
   <td>Duração até que um usuário sincronizado expire.</td>
  </tr>
  <tr>
   <td><strong>Associação automática do usuário</strong></td>
   <td>Lista de grupos aos quais um usuário sincronizado é adicionado automaticamente.</td>
  </tr>
  <tr>
   <td><strong>Mapeamento de propriedades do usuário</strong></td>
   <td>Definição de mapeamento de lista de propriedades locais de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do usuário</strong></td>
   <td>O prefixo de caminho usado ao criar novos usuários.</td>
  </tr>
  <tr>
   <td><strong>Expiração da associação do usuário</strong></td>
   <td>Hora após a qual a associação expira.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidade de aninhamento da associação do usuário</strong></td>
   <td>Retorna a profundidade máxima de aninhamento de grupo quando as relações de associação são sincronizadas. Um valor de 0 desativa a pesquisa de associação de grupo. Um valor de 1 só adiciona os grupos diretos de um usuário. Esse valor não tem efeito ao sincronizar grupos individuais somente ao sincronizar um ancestral de associação de usuários.</td>
  </tr>
  <tr>
   <td><strong>Tempo de expiração do grupo</strong></td>
   <td>Duração até que um grupo sincronizado expire.</td>
  </tr>
  <tr>
   <td><strong>Associação automática de grupo</strong></td>
   <td>Lista de grupos aos quais um grupo sincronizado é adicionado automaticamente.</td>
  </tr>
  <tr>
   <td><strong>Mapeamento de propriedades do grupo</strong></td>
   <td>Definição de mapeamento de lista de propriedades locais de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do grupo</strong></td>
   <td>O prefixo de caminho usado ao criar novos grupos.</td>
  </tr>
 </tbody>
</table>

## O módulo de logon externo {#the-external-login-module}

O módulo de logon externo está localizado em **Apache Jackrabbit Oak External Login Module** no console de gerenciamento.

>[!NOTE]
>
>O módulo de logon externo do Apache Jackrabbit Oak implementa as especificações do Java Authentication and Authorization Service (JAAS). Consulte o [Guia oficial de Referência de Segurança do Oracle Java](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obter mais informações.

Seu trabalho é definir qual provedor de identidade e manipulador de sincronização usar, vinculando efetivamente os dois módulos.

As seguintes opções de configuração estão disponíveis:

| **Classificação JAAS** | Especificação da classificação (ou seja, ordem de classificação) desta entrada do módulo de logon. As entradas são classificadas em ordem decrescente (ou seja, as configurações classificadas com valor mais alto vêm primeiro). |
|---|---|
| **Sinalizador de controle JAAS** | Propriedade que especifica se um LoginModule é OBRIGATÓRIO, REQUISITO, SUFICIENTE ou OPTIONAL.Consulte a documentação de configuração do JAAS para obter mais detalhes sobre o significado desses sinalizadores. |
| **Realm JAAS** | O nome do realm (ou nome do aplicativo) com base no qual LoginModule deve ser registrado. Se nenhum nome de realm for fornecido, LoginModule será registrado com um realm padrão, conforme configurado na configuração Felix JAAS. |
| **Nome do provedor de identidade** | Nome do provedor de identidade. |
| **Nome do manipulador de sincronização** | Nome do manipulador de sincronização. |

>[!NOTE]
>
>Se você planeja ter mais de uma configuração LDAP com sua instância AEM, é necessário criar provedores de identidade e manipuladores de sincronização separados para cada configuração.

## Configurar LDAP por SSL {#configure-ldap-over-ssl}

AEM 6 pode ser configurado para autenticação com LDAP por SSL seguindo o procedimento abaixo:

1. Marque as caixas de seleção **Use SSL** ou **Use TLS** ao configurar o [Provedor de identidade LDAP](#configuring-the-ldap-identity-provider).
1. Configure o Manipulador de sincronização e o módulo de logon externo de acordo com sua configuração.
1. Instale os certificados SSL na sua VM Java, se necessário. Isso pode ser feito usando keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Teste a conexão com o servidor LDAP.

### Criando certificados SSL {#creating-ssl-certificates}

Certificados autoassinados podem ser usados ao configurar AEM para autenticação com LDAP via SSL. Abaixo está um exemplo de um procedimento de trabalho para geração de certificados para uso com AEM.

1. Verifique se você tem uma biblioteca SSL instalada e funcionando. Este procedimento usará o OpenSSL como exemplo.

1. Crie um arquivo personalizado de configuração OpenSSL (cnf). Isso pode ser feito copiando o arquivo de configuração padrão **openssl.cnf **e personalizando-o. Em sistemas UNIX, geralmente está localizado em `/usr/lib/ssl/openssl.cnf`

1. Continue criando a chave raiz da CA executando o comando abaixo em um terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Em seguida, crie um novo certificado autoassinado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect o certificado recém-gerado para garantir que tudo esteja na ordem:

   `openssl x509 -noout -text -in root-ca.crt`

1. Verifique se todas as pastas especificadas no arquivo de configuração do certificado (.cnf) existem. Caso contrário, crie-os.
1. Crie uma semente aleatória, executando, por exemplo:

   `openssl rand -out private/.rand 8192`

1. Mova os arquivos .pem criados para os locais configurados no arquivo .cnf.

1. Por fim, adicione o certificado ao armazenamento de chaves Java.

## Ativando o registro de depuração {#enabling-debug-logging}

O registro de depuração pode ser ativado tanto para o provedor de identidade LDAP quanto para o módulo de logon externo, a fim de solucionar problemas de conexão.

Para ativar o registro de depuração, é necessário:

1. Vá para o Console de gerenciamento da Web.
1. Localize &quot;Apache Sling Logging Logger Configuration&quot; e crie dois loggers com as seguintes opções:

* Nível de registro: Depuração
* Arquivo de registro logs/ldap.log
* Padrão de mensagem: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.Jackrabbit.oak.security.authentication.ldap

* Nível de registro: Depuração
* Arquivo de log: logs/external.log
* Padrão de mensagem: {0,date,dd.MM.yyyy HH:mm:ss.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.Jackrabbit.oak.spi.security.authentication.external

## Uma palavra sobre afiliação de grupo {#a-word-on-group-affiliation}

Os usuários sincronizados por meio do LDAP podem fazer parte de grupos diferentes em AEM. Esses grupos podem ser grupos LDAP externos que serão adicionados a AEM como parte do processo de sincronização, mas também podem ser grupos adicionados separadamente e que não fazem parte do esquema de afiliação do grupo LDAP original.

Na maioria dos casos, esses podem ser grupos adicionados por um administrador local de AEM ou por qualquer outro provedor de identidade.

Se um usuário for removido de um grupo no servidor LDAP, a alteração também será refletida no lado AEM após a sincronização. No entanto, todas as outras afiliações de grupo do usuário que não foram adicionadas pelo LDAP permanecerão em vigor.

AEM detecta e lida com a remoção de usuários de grupos externos usando a propriedade `rep:externalId`. Essa propriedade é adicionada automaticamente a qualquer usuário ou grupo sincronizado pelo Manipulador de sincronização e contém informações sobre o provedor de identidade de origem.

Para obter mais informações, consulte a documentação do Apache Oak em [Sincronização de usuários e grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conhecidos {#known-issues}

Se você planeja usar o LDAP sobre SSL, certifique-se de que os certificados que está usando sejam criados sem a opção de comentário do Netscape. Se essa opção estiver ativada, a autenticação falhará com um erro de handshake SSL.

