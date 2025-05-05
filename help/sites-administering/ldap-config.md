---
title: Configuração do LDAP com AEM 6
description: Saiba como usar e configurar serviços LDAP com AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: 2ebca4fb-20f7-499c-96a0-4018eaeddc1a
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---

# Configuração do LDAP com AEM 6 {#configuring-ldap-with-aem}

O LDAP (o protocolo **L** ightweight **D** diretory **A** ccess **P** a) é usado para acessar serviços de diretório centralizados. Isso ajuda a reduzir o esforço necessário para gerenciar contas de usuários, pois elas podem ser acessadas por vários aplicativos. Um desses servidores LDAP é o Ative Diretory. O LDAP geralmente é usado para obter o Logon único, que permite que um usuário acesse vários aplicativos depois de fazer logon uma vez.

As contas de usuário podem ser sincronizadas entre o servidor LDAP e o repositório, com os detalhes da conta LDAP salvos no repositório. Essa funcionalidade permite que as contas sejam atribuídas a grupos de repositórios para alocar as permissões e os privilégios necessários.

O repositório usa autenticação LDAP para autenticar esses usuários, com credenciais sendo passadas ao servidor LDAP para validação, o que é necessário antes de permitir o acesso ao repositório. Para melhorar o desempenho, as credenciais validadas com êxito podem ser armazenadas em cache pelo repositório, com um tempo limite de expiração para garantir que a revalidação ocorra após um período apropriado.

Quando uma conta é removida do servidor LDAP, a validação não é mais concedida e o acesso ao repositório é negado. Os detalhes das contas LDAP salvas no repositório também podem ser removidos.

O uso dessas contas é transparente para os usuários. Ou seja, eles não veem diferença entre contas de usuários e de grupos criadas com base no LDAP e contas criadas exclusivamente no repositório.

No AEM 6, o suporte LDAP vem com uma nova implementação que requer um tipo de configuração diferente do que com versões anteriores.

Todas as configurações LDAP agora estão disponíveis como configurações OSGi. Eles podem ser configurados por meio do console de Gerenciamento da Web em:
`https://serveraddress:4502/system/console/configMgr`

Para que o LDAP funcione com AEM, você deve criar três configurações OSGi:

1. Um Provedor de Identidade LDAP (IDP).
1. Um Manipulador de sincronização.
1. Um Módulo De Logon Externo.

>[!NOTE]
>
>Assista ao [Módulo de Logon Externo do Oak - Autenticação com LDAP e posterior](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-oak-external-login-module-authenticating-with-ldap-and-beyond.html) para aprofundar Módulos de Logon Externos.
>
>Para ler um exemplo de configuração do Experience Manager com o Apache DS, consulte [Configurando o Adobe Experience Manager 6.5 para usar o Apache Diretory Service.](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager/configuring-adobe-experience-manager-6-to-use-apache-directory/m-p/183805)

## Configuração do provedor de identidade LDAP {#configuring-the-ldap-identity-provider}

O Provedor de Identidade LDAP é usado para definir como os usuários são recuperados do servidor LDAP.

Ele pode ser encontrado no console de gerenciamento sob o nome **Apache Jackrabbit Oak LDAP Identity Provider**.

As seguintes opções de configuração estão disponíveis para o Provedor de Identidade LDAP:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do provedor LDAP</strong></td>
   <td>Nome desta configuração do provedor LDAP.</td>
  </tr>
  <tr>
   <td><strong>Nome do Host do Servidor LDAP</strong><br /> </td>
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
   <td>Indica se a validação do certificado do servidor deve ser desabilitada.</td>
  </tr>
  <tr>
   <td><strong>Vincular DN</strong></td>
   <td>DN do usuário para autenticação. Se esse campo ficar vazio, uma associação anônima será executada.</td>
  </tr>
  <tr>
   <td><strong>Senha de associação</strong></td>
   <td>Senha do usuário para autenticação</td>
  </tr>
  <tr>
   <td><strong>Tempo limite de pesquisa</strong></td>
   <td>Tempo até que uma pesquisa expire</td>
  </tr>
  <tr>
   <td><strong>Máximo de pool de administradores ativo</strong></td>
   <td>O tamanho máximo ativo do pool de conexões do administrador.</td>
  </tr>
  <tr>
   <td><strong>Máximo de usuários ativos no pool</strong></td>
   <td>O tamanho máximo ativo do pool de conexão do usuário.</td>
  </tr>
  <tr>
   <td><strong>DN base do usuário</strong></td>
   <td>O DN para pesquisas de usuário</td>
  </tr>
  <tr>
   <td><strong>Classes de objeto do usuário</strong></td>
   <td>A lista de classes de objetos que uma entrada de usuário deve conter.</td>
  </tr>
  <tr>
   <td><strong>Atributo de ID de usuário</strong></td>
   <td>Nome do atributo que contém a ID do usuário.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra do usuário</strong></td>
   <td>Filtro LDAP adicional a ser usado ao pesquisar por usuários. O filtro final é formatado como: '(&amp;(&lt;idAttr&gt;=&lt;userId&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)' (user.extraFilter)</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN do usuário</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>DN de base do grupo</strong></td>
   <td>O DN base para pesquisas de grupo.</td>
  </tr>
  <tr>
   <td><strong>Agrupar classes de objeto</strong></td>
   <td>A lista de classes de objetos que uma entrada de grupo deve conter.</td>
  </tr>
  <tr>
   <td><strong>Atributo do nome do grupo</strong></td>
   <td>Nome do atributo que contém o nome do grupo.</td>
  </tr>
  <tr>
   <td><strong>Filtro extra do grupo</strong></td>
   <td>Filtro LDAP adicional a ser usado ao pesquisar por grupos. O filtro final é formatado como: '(&amp;(&lt;nameAttr&gt;=&lt;groupName&gt;)(objectclass=&lt;objectclass&gt;)&lt;extraFilter&gt;)'</td>
  </tr>
  <tr>
   <td><strong>Caminhos de DN de grupo</strong></td>
   <td>Controla se o DN deve ser usado para calcular uma parte do caminho intermediário.</td>
  </tr>
  <tr>
   <td><strong>Atributo do membro do grupo</strong></td>
   <td>Atributo de grupo que contém um ou mais membros de um grupo.</td>
  </tr>
 </tbody>
</table>

## Configuração Do Manipulador De Sincronização {#configuring-the-synchronization-handler}

O manipulador de sincronização define como os usuários e grupos do Provedor de identidade são sincronizados com o repositório.

Está localizado no nome **Apache Jackrabbit Oak Default Sync Handler** do console de gerenciamento.

As seguintes opções de configurações estão disponíveis para o Manipulador de sincronização:

<table>
 <tbody>
  <tr>
   <td><strong>Nome do Manipulador de Sincronização</strong></td>
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
   <td>Definição de mapeamento de lista de propriedades locais a partir de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do usuário</strong></td>
   <td>O prefixo de caminho usado ao criar usuários.</td>
  </tr>
  <tr>
   <td><strong>Expiração de associação de usuário</strong></td>
   <td>Tempo após o qual a associação expira.<br /> </td>
  </tr>
  <tr>
   <td><strong>Profundidade de aninhamento de associação de usuário</strong></td>
   <td>Retorna a profundidade máxima do aninhamento de grupos quando as relações de associação são sincronizadas. Um valor 0 desativa efetivamente a pesquisa de associação de grupo. Um valor igual a 1 adiciona apenas os grupos diretos de um usuário. Este valor não tem efeito ao sincronizar grupos individuais somente ao sincronizar uma ancestralidade de associação de usuários.</td>
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
   <td><strong>Mapeamento de propriedade de grupo</strong></td>
   <td>Definição de mapeamento de lista de propriedades locais a partir de propriedades externas.</td>
  </tr>
  <tr>
   <td><strong>Prefixo do caminho do grupo</strong></td>
   <td>O prefixo de caminho usado ao criar grupos.</td>
  </tr>
 </tbody>
</table>

## O módulo de login externo {#the-external-login-module}

O módulo de logon externo está localizado no **Módulo de Logon Externo do Apache Jackrabbit Oak** no console de gerenciamento.

>[!NOTE]
>
>O módulo de logon externo do Apache Jackrabbit Oak implementa as especificações do Java™ Authentication and Authorization Servi (JAAS). Consulte o [Guia oficial de Referência de Segurança do Oracle Java™](https://docs.oracle.com/javase/8/docs/technotes/guides/security/jaas/JAASRefGuide.html) para obter mais informações.

Seu trabalho é definir qual Provedor de identidade e Manipulador de sincronização usar, vinculando efetivamente os dois módulos.

As seguintes opções de configuração estão disponíveis:

| **Classificação no JAAS** | Especificando a classificação (ou seja, a ordem de classificação) dessa entrada do módulo de logon. As entradas são classificadas em ordem decrescente (ou seja, as configurações com classificação de valor mais alto vêm primeiro). |
|---|---|
| **Sinalizador de Controle JAAS** | Propriedade que especifica se um LoginModule é REQUIRED, REQUISITE, SUFFICIENT ou OPTIONAL. Consulte a documentação de configuração do JAAS para obter mais detalhes sobre o significado desses sinalizadores. |
| **Território JAAS** | O nome do realm (ou nome da aplicação) no qual o LoginModule é registrado. Se nenhum nome de realm for fornecido, o LoginModule será registrado com um realm default conforme configurado na configuração do Felix JAAS. |
| **Nome do Provedor de Identidade** | Nome do provedor de identidade. |
| **Nome do Manipulador de Sincronização** | Nome do manipulador de sincronização. |

>[!NOTE]
>
>Se você planeja ter mais de uma configuração LDAP com sua instância AEM, provedores de identidade e manipuladores de sincronização separados devem ser criados para cada configuração.

## Configurar LDAP sobre SSL {#configure-ldap-over-ssl}

O AEM 6 pode ser configurado para autenticação com LDAP sobre SSL seguindo o procedimento abaixo:

1. Marque as caixas de seleção **Usar SSL** ou **Usar TLS** ao configurar o [Provedor de Identidade LDAP](#configuring-the-ldap-identity-provider).
1. Configure o Manipulador de sincronização e o módulo de Logon externo de acordo com sua configuração.
1. Instale os certificados SSL em sua VM Java™, se necessário. Esta instalação pode ser feita usando a ferramenta de chave:

   `keytool -import -alias localCA -file <certificate location> -keystore <keystore location>`

1. Teste a conexão com o servidor LDAP.

### Criação de certificados SSL {#creating-ssl-certificates}

Certificados autoassinados podem ser usados ao configurar o AEM para autenticação com LDAP via SSL. Veja abaixo um exemplo de um procedimento funcional para geração de certificados para uso com AEM.

1. Verifique se você tem uma biblioteca SSL instalada e em funcionamento. Este procedimento usa OpenSSL como exemplo.

1. Crie um arquivo de configuração OpenSSL (cnf) personalizado. Essa configuração pode ser feita copiando o arquivo de configuração padrão **openssl.cnf** e personalizando-o. Em sistemas UNIX®, está em `/usr/lib/ssl/openssl.cnf`

1. Prossiga para a criação da chave raiz da CA executando o comando abaixo em um terminal:

   ```
   openssl genpkey -algorithm [public key algorithm] -out certificatefile.key -pkeyopt [public key algorithm option]
   ```

1. Em seguida, crie um certificado autoassinado:

   `openssl req -new -x509 -days [number of days for certification] -key certificatefile.key -out root-ca.crt -config CA/openssl.cnf`

1. Para verificar se tudo está em ordem, inspecione o certificado recém-gerado:

   `openssl x509 -noout -text -in root-ca.crt`

1. Verifique se todas as pastas especificadas no arquivo de configuração de certificado (.cnf) existem. Caso contrário, crie-as.
1. Crie uma seed aleatória, executando, por exemplo:

   `openssl rand -out private/.rand 8192`

1. Mova os arquivos .pem criados para os locais configurados no arquivo .cnf.

1. Por fim, adicione o certificado ao Java™ keystore.

## Ativando o log de depuração {#enabling-debug-logging}

O log de depuração pode ser ativado para o Provedor de Identidade LDAP e o Módulo de Login Externo para solucionar problemas de conexão.

Para ativar o log de depuração, faça o seguinte:

1. Vá até o Console de Gerenciamento da Web.
1. Localize &quot;Configuração do logger de log do Apache Sling&quot; e crie dois loggers com as seguintes opções:

* Nível de registro: depuração
* Arquivo de log logs/ldap.log
* Padrão de Mensagem: &lbrace;0,date,`dd.MM.yyyy` `HH:mm:ss.SSS` &ast;{4}&ast; {2} {3} {5}
* Agente de log: org.apache.jackrabbit.oak.security.authentication.ldap

* Nível de registro: depuração
* Arquivo de log: logs/external.log
* Padrão de Mensagem: &lbrace;0,date,`dd.MM.yyyy` `HH:mm:ss.SSS` &ast;{4}&ast; {2} {3} {5}
* Agente de log: org.apache.jackrabbit.oak.spi.security.authentication.external

## Uma Palavra sobre Afiliação de Grupos {#a-word-on-group-affiliation}

Os usuários sincronizados por meio do LDAP podem fazer parte de diferentes grupos no AEM. Esses grupos podem ser grupos LDAP externos que são adicionados ao AEM como parte do processo de sincronização. No entanto, eles também podem ser grupos adicionados separadamente e que não fazem parte do esquema original de afiliação de grupo LDAP.

Normalmente, esses grupos são adicionados por um administrador local do AEM ou por qualquer outro provedor de identidade.

Se um usuário for removido de um grupo no servidor LDAP, a alteração será refletida no lado AEM na sincronização. No entanto, todas as outras afiliações de grupo do usuário que não foram adicionadas pelo LDAP permanecem em vigor.

O AEM detecta e lida com a limpeza de usuários de grupos externos usando a propriedade `rep:externalId`. Esta propriedade é adicionada automaticamente a qualquer usuário ou grupo que seja sincronizado pelo Manipulador de sincronização e contenha informações sobre o provedor de identidade de origem.

Consulte a documentação do Apache Oak em [Sincronização de usuários e grupos](https://jackrabbit.apache.org/oak/docs/security/authentication/usersync.html).

## Problemas conhecidos {#known-issues}

Se você planeja usar LDAP sobre SSL, verifique se os certificados que você está usando são criados sem a opção de comentário do Netscape. Se essa opção estiver ativada, a autenticação falhará com um erro de handshake SSL.
