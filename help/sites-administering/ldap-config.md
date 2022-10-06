---
title: Configuração do LDAP com AEM 6
seo-title: Configuring LDAP with AEM 6
description: Saiba como configurar o LDAP com AEM.
seo-description: Learn how to configure LDAP with AEM.
uuid: 0007def4-86f0-401d-aa37-c8d49d5acea1
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 5faf6ee5-9242-48f4-87a8-ada887a3be1e
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 0%

---

# Configuração do LDAP com AEM 6 {#configuring-ldap-with-aem}

LDAP (o **L** leve **D** Diretório **A** acesso **P** rotocol) é usado para acessar serviços de diretório centralizados. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuário, pois elas podem ser acessadas por vários aplicativos. Um desses servidores LDAP é o Ative Diretory. O LDAP é frequentemente usado para alcançar o Logon único , o que permite que um usuário acesse vários aplicativos após fazer logon uma vez.

As contas de usuário podem ser sincronizadas entre o servidor LDAP e o repositório, com os detalhes da conta LDAP sendo salvos no repositório. Isso permite que as contas sejam atribuídas a grupos de repositório para alocar as permissões e privilégios necessários.

O repositório usa a autenticação LDAP para autenticar esses usuários, com credenciais sendo passadas ao servidor LDAP para validação, o que é necessário antes de permitir o acesso ao repositório. Para melhorar o desempenho, as credenciais validadas com êxito podem ser armazenadas em cache pelo repositório, com um tempo limite de expiração para garantir que a revalidação ocorra após um período apropriado.

Quando uma conta é removida do servidor LDAP, a validação não é mais concedida e, portanto, o acesso ao repositório é negado. Detalhes de contas LDAP que são salvas no repositório também podem ser removidos.

O uso dessas contas é transparente para os usuários, eles não veem diferença entre as contas de usuário e grupo criadas a partir do LDAP e as criadas exclusivamente no repositório.

No AEM 6, o suporte LDAP vem com uma nova implementação que requer um tipo de configuração diferente das versões anteriores.

Todas as configurações LDAP agora estão disponíveis como configurações OSGi. Eles podem ser configurados por meio do console de Gerenciamento da Web em:
`https://serveraddress:4502/system/console/configMgr`

Para que o LDAP funcione com o AEM, é necessário criar três configurações OSGi:

1. Um provedor de identidade LDAP (IDP).
1. Um Manipulador De Sincronização.
1. Um Módulo De Logon Externo.

>[!NOTE]
>
>Observar [Módulo de logon externo do Oak - Autenticação com LDAP e Além](https://docs.adobe.com/content/ddc/en/gems/oak-s-external-login-module---authenticating-with-ldap-and-beyon.html#) para aprofundar os Módulos de logon externo.
>
>Para ler um exemplo de configuração do Experience Manager com Apache DS, consulte [Configurando o Adobe Experience Manager 6.5 para usar o Apache Diretory Service.](https://helpx.adobe.com/experience-manager/using/configuring-aem64-apache-directory-service.html)

## Configuração Do Provedor De Identidade LDAP {#configuring-the-ldap-identity-provider}

O Provedor de identidade LDAP é usado para definir como os usuários são recuperados do servidor LDAP.

Ele pode ser encontrado no console de gerenciamento sob o **Provedor de identidade LDAP do Apache Jackrabbit Oak** nome.

As seguintes opções de configuração estão disponíveis para o Provedor de identidade LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do provedor LDAP</strong></td>
   <td>Nome dessa configuração do provedor LDAP.</td>
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
   <td>Indica se o TLS deve ser iniciado nas conexões.</td>
  </tr>
  <tr>
   <td><strong>Desativar verificação de certificado</strong></td>
   <td>Indica se a validação do certificado do servidor deve ser desativada.</td>
  </tr>
  <tr>
   <td><strong>DN de Ligação</strong></td>
   <td>DN do usuário para autenticação. Se isso for deixado em branco, um vínculo anônimo será executado.</td>
  </tr>
  <tr>
   <td><strong>Senha de Ligação</strong></td>
   <td>Senha do usuário para autenticação</td>
  </tr>
  <tr>
   <td><strong>Tempo limite da pesquisa</strong></td>
   <td>Tempo até que a pesquisa atinja o tempo limite</td>
  </tr>
  <tr>
   <td><strong>Máximo de pool de administradores ativo</strong></td>
   <td>O tamanho ativo máximo do pool de conexão do administrador.</td>
  </tr>
  <tr>
   <td><strong>Máximo de pool de usuários ativo</strong></td>
   <td>O tamanho ativo máximo do pool de conexões do usuário.</td>
  </tr>
  <tr>
   <td><strong>DN de base do usuário</strong></td>
   <td>O DN para pesquisas de usuários</td>
  </tr>
  <tr>
   <td><strong>Classes de objetos do usuário</strong></td>
   <td>A lista de classes de objetos que uma entrada de usuário deve conter.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID do usuário</strong></td>
   <td>Nome do atributo que contém a ID do usuário.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra do usuário</strong></td>
   <td>Filtro LDAP extra a ser usado ao pesquisar usuários. O filtro final é formatado da seguinte maneira: '(&amp;(&lt;idattr&gt;=&lt;userid&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN do usuário</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>DN de base de grupo</strong></td>
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
   <td>Filtro LDAP extra a ser usado ao pesquisar por grupos. O filtro final é formatado como: '(&amp;(&lt;nameattr&gt;=&lt;groupname&gt;)(objectclass=&lt;objectclass&gt;)&lt;extrafilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN do Grupo</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>Atributo do membro do grupo</strong></td>
   <td>Atributo de grupo que contém os membros de um grupo.</td>
  </tr>
 </tbody>
</table>

## Configurar O Manipulador De Sincronização {#configuring-the-synchronization-handler}

O manipulador de sincronização definirá como os usuários e grupos do Provedor de identidade serão sincronizados com o repositório.

Está localizado sob a variável **Manipulador de sincronização padrão do Apache Jackrabbit Oak** no console de gerenciamento.

As seguintes opções de configurações estão disponíveis para o Manipulador de Sincronização:

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
   <td><strong>Associação automática de usuário</strong></td>
   <td>Lista de grupos aos quais um usuário sincronizado é adicionado automaticamente.</td>
  </tr>
  <tr>
   <td><strong>Mapeamento de propriedade do usuário</strong></td>
   <td>Definição de mapeamento de lista de propriedades locais de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do usuário</strong></td>
   <td>O prefixo de caminho usado ao criar novos usuários.</td>
  </tr>
  <tr>
   <td><strong>Expiração de associação de usuário</strong></td>
   <td>Hora após a qual a associação expira.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidade de aninhamento da associação do usuário</strong></td>
   <td>Retorna a profundidade máxima do aninhamento de grupo quando as relações de associação são sincronizadas. Um valor de 0 desativa efetivamente a pesquisa de associação de grupo. Um valor de 1 adiciona apenas os grupos diretos de um usuário. Esse valor não tem efeito ao sincronizar grupos individuais somente ao sincronizar um ancestral de associação de usuários.</td>
  </tr>
  <tr>
   <td><strong>Tempo de Expiração do Grupo</strong></td>
   <td>Duração até que um grupo sincronizado expire.</td>
  </tr>
  <tr>
   <td><strong>Associação automática de grupo</strong></td>
   <td>Lista de grupos aos quais um grupo sincronizado é adicionado automaticamente.</td>
  </tr>
  <tr>
   <td><strong>Mapeamento de propriedade do grupo</strong></td>
   <td>Definição de mapeamento de lista de propriedades locais de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do grupo</strong></td>
   <td>O prefixo de caminho usado ao criar novos grupos.</td>
  </tr>
 </tbody>
</table>

## O módulo de logon externo {#the-external-login-module}

O módulo de logon externo está localizado na guia **Módulo de logon externo Apache Jackrabbit Oak** no console de gerenciamento.

>[!NOTE]
>
>O módulo de logon externo do Apache Jackrabbit Oak implementa as especificações do Java Authentication and Authorization Service (JAAS). Consulte a [Guia oficial de referência de segurança do Java Oracle](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obter mais informações.

Seu trabalho é definir qual Provedor de identidade e Manipulador de sincronização usar, vinculando efetivamente os dois módulos.

As seguintes opções de configuração estão disponíveis:

| **Classificação JAAS** | Especificação da classificação (ou seja, ordem de classificação) dessa entrada do módulo de logon. As entradas são classificadas em uma ordem decrescente (ou seja, as configurações de classificação de valor mais alto vêm primeiro). |
|---|---|
| **Sinalizador de Controle JAAS** | Propriedade especificando se um LoginModule é OBRIGATÓRIO, REQUISITO, SUFICIENTE ou OPCIONAL.Consulte a documentação de configuração do JAAS para obter mais detalhes sobre o significado desses sinalizadores. |
| **Território JAAS** | O nome do realm (ou nome do aplicativo) com base no qual o LoginModule será registrado. Se nenhum nome de realm for fornecido, o LoginModule será registrado com um realm padrão como configurado na configuração do Felix JAAS. |
| **Nome do provedor de identidade** | Nome do provedor de identidade. |
| **Nome do manipulador de sincronização** | Nome do manipulador de sincronização. |

>[!NOTE]
>
>Se você planeja ter mais de uma configuração LDAP com sua instância de AEM, é necessário criar provedores de identidade e manipuladores de sincronização separados para cada configuração.

## Configurar LDAP por SSL {#configure-ldap-over-ssl}

AEM 6 pode ser configurado para autenticação com LDAP por SSL seguindo o procedimento abaixo:

1. Verifique a **Usar SSL** ou **Usar TLS** caixas de seleção ao configurar o [Provedor de identidade LDAP](#configuring-the-ldap-identity-provider).
1. Configure o Manipulador de sincronização e o módulo de Logon externo de acordo com sua configuração.
1. Instale os certificados SSL em sua VM Java, se necessário. Isso pode ser feito usando keytool:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Teste a conexão com o servidor LDAP.

### Criação de certificados SSL {#creating-ssl-certificates}

Certificados autoassinados podem ser usados ao configurar AEM para autenticação com LDAP via SSL. Veja abaixo um exemplo de um procedimento de trabalho para gerar certificados para uso com o AEM.

1. Certifique-se de ter uma biblioteca SSL instalada e funcionando. Este procedimento usará o OpenSSL como exemplo.

1. Crie um arquivo de configuração (cnf) OpenSSL personalizado. Isso pode ser feito copiando o arquivo de configuração padrão **openssl.cnf **e personalizando-o. Em sistemas UNIX, geralmente está localizado em `/usr/lib/ssl/openssl.cnf`

1. Continue criando a chave raiz da CA executando o comando abaixo em um terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Em seguida, crie um novo certificado autoassinado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Inspect o certificado recém-gerado para garantir que tudo esteja em ordem:

   `openssl x509 -noout -text -in root-ca.crt`

1. Verifique se todas as pastas especificadas no arquivo de configuração de certificado (.cnf) existem. Caso contrário, crie-os.
1. Crie uma seed aleatória, executando, por exemplo:

   `openssl rand -out private/.rand 8192`

1. Mova os arquivos .pem criados para os locais configurados no arquivo .cnf .

1. Por fim, adicione o certificado ao keystore Java.

## Ativação do log de depuração {#enabling-debug-logging}

O registro de depuração pode ser ativado tanto para o Provedor de identidade LDAP quanto para o Módulo de logon externo para solucionar problemas de conexão.

Para ativar o log de depuração, é necessário:

1. Vá para o Console de Gerenciamento da Web.
1. Localize &quot;Configuração do Apache Sling Logging Logger&quot; e crie dois loggers com as seguintes opções:

* Nível de registro: Depurar
* Arquivo de log logs/ldap.log
* Padrão da mensagem: {0,data,dd.MM.yyyy HH:mm:s.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.security.authentication.ldap

* Nível de registro: Depurar
* Arquivo de log: logs/external.log
* Padrão da mensagem: {0,data,dd.MM.yyyy HH:mm:s.SSS} &amp;ast;{4}&amp;ast; {2} {3} {5}
* Logger: org.apache.jackrabbit.oak.spi.security.authentication.external

## Uma palavra sobre afiliação de grupo {#a-word-on-group-affiliation}

Os usuários sincronizados por meio do LDAP podem fazer parte de grupos diferentes no AEM. Esses grupos podem ser grupos LDAP externos que serão adicionados a AEM como parte do processo de sincronização, mas também podem ser grupos que são adicionados separadamente e não fazem parte do esquema de afiliação do grupo LDAP original.

Na maioria dos casos, esses podem ser grupos adicionados por um administrador de AEM local ou por qualquer outro provedor de identidade.

Se um usuário for removido de um grupo no servidor LDAP, a alteração também será refletida no lado AEM após a sincronização. No entanto, todas as outras afiliações de grupo do usuário que não foram adicionadas pelo LDAP permanecerão em vigor.

O AEM detecta e lida com a limpeza de usuários de grupos externos ao usar o `rep:externalId` propriedade. Essa propriedade é adicionada automaticamente a qualquer usuário ou grupo sincronizado pelo Manipulador de Sincronização e contém informações sobre o provedor de identidade de origem.

Para obter mais informações, consulte a documentação do Apache Oak em [Sincronização de usuários e grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conhecidos {#known-issues}

Se você planeja usar o LDAP sobre SSL, certifique-se de que os certificados que está usando sejam criados sem a opção de comentário do Netscape. Se essa opção estiver habilitada, a autenticação falhará com um erro de handshake SSL.
