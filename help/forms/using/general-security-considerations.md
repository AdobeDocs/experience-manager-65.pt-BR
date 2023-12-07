---
title: Considerações gerais de segurança para o AEM Forms no JEE
description: Saiba como se preparar para fortalecer seu AEM Forms no ambiente JEE.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
docset: aem65
role: Admin
exl-id: 3f150dd5-f486-4f16-9de9-035cde53b034
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 1%

---

# Considerações gerais de segurança para o AEM Forms no JEE{#general-security-considerations-for-aem-forms-on-jee}

Este artigo fornece informações introdutórias que ajudam você a se preparar para fortalecer seu ambiente do AEM Forms. Inclui informações de pré-requisitos sobre o AEM Forms no JEE, sistema operacional, servidor de aplicativos e segurança de banco de dados. Examine essas informações antes de continuar a bloquear o ambiente.

## Informações de segurança específicas do fornecedor {#vendor-specific-security-information}

Esta seção contém informações relacionadas à segurança sobre sistemas operacionais, servidores de aplicativos e bancos de dados incorporados à sua solução AEM Forms no JEE.

Use os links desta seção para localizar informações de segurança específicas do fornecedor para seu sistema operacional, banco de dados e servidor de aplicativos.

### Informações de segurança do sistema operacional {#operating-system-security-information}

Ao proteger seu sistema operacional, considere cuidadosamente a implementação das medidas descritas pelo fornecedor do sistema operacional, incluindo as seguintes:

* Definindo e controlando usuários, atribuições e privilégios
* Monitorar logs e trilhas de auditoria
* Remoção de serviços e aplicativos desnecessários
* Fazendo backup de arquivos

Para obter informações de segurança sobre sistemas operacionais compatíveis com o AEM Forms no JEE, consulte os recursos na tabela:

<table>
 <thead>
  <tr>
   <th><p>Sistema Operacional</p> </th>
   <th><p>Recurso de segurança</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® AIX® 7.2</p> </td>
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Benefícios da segurança no IBM® AIX®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guia de Segurança do Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP ou ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Guia de segurança do Red Hat® Enterprise Linux®</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris™ 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Diretrizes de segurança e proteção</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Atualização 3</td>
   <td><a href="https://docs.oracle.com/en/operating-systems/oracle-linux/7/security/" target="_blank">Guia de segurança da versão 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentação de proteção</a></td>
  </tr>
 </tbody>
</table>

### Informações de segurança do servidor de aplicativos {#application-server-security-information}

Ao proteger o servidor de aplicativos, considere cuidadosamente a implementação das medidas descritas pelo fornecedor do servidor, incluindo as seguintes:

* Uso de nome de usuário de administrador não óbvio
* Desabilitar serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechando portas desnecessárias
* Limitação de clientes por endereços IP ou domínios
* Utilização do Gerenciador de segurança Java™ para restringir privilégios de forma programática

Para obter informações de segurança sobre servidores de aplicações compatíveis com o AEM Forms no JEE, consulte os recursos nesta tabela.

<table>
 <thead>
  <tr>
   <th><p>Servidor de aplicativos</p> </th>
   <th><p>Recurso de segurança</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Oracle WebLogic®</p> </td>
   <td><p>Procure por Noções Básicas sobre a Segurança do WebLogic em <a href="https://docs.oracle.com/">https://docs.oracle.com/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM® WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Protegendo aplicativos e seus ambientes</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security%20subsystem%20configuration.html">Configuração do subsistema de segurança</a></p> </td>
  </tr>
 </tbody>
</table>

### Informações de segurança do banco de dados {#database-security-information}

Ao proteger seu banco de dados, considere implementar as medidas descritas pelo fornecedor do banco de dados, incluindo as seguintes:

* Restringindo operações com listas de controle de acesso (ACLs)
* Uso de portas não padrão
* Ocultando o banco de dados por trás de um firewall
* Criptografar dados confidenciais antes de gravá-los no banco de dados (consulte a documentação do fabricante do banco de dados)

Para obter informações de segurança sobre bancos de dados compatíveis com o AEM Forms no JEE, consulte os recursos nesta tabela.

<table>
 <thead>
  <tr>
   <th><p>Banco de dados</p> </th>
   <th><p>Recurso de segurança</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM® DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Biblioteca da família de produtos DB2®</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2016</p> </td>
   <td>Pesquise na Web por "SQL Server 2016: Segurança"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemas gerais de segurança do MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemas gerais de segurança do MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>Consulte o capítulo Segurança no <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">Documentação do Oracle 12g</a></p> </td>
  </tr>
 </tbody>
</table>

Esta tabela descreve as portas padrão que devem ser abertas durante o processo de configuração do AEM Forms no JEE. Se estiver se conectando via https, ajuste as informações da porta e os endereços IP de acordo. Para obter mais informações sobre a configuração de portas, consulte *Instalação e implantação do AEM Forms no JEE* para o seu servidor de aplicativos.

<table>
 <thead>
  <tr>
   <th><p>Produto ou serviço</p> </th>
   <th><p>Número da porta</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss®</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Servidor Gerenciado WebLogic</p> </td>
   <td><p>Definido pelo administrador durante a configuração</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere®</p> </td>
   <td><p>9060, se a Segurança global estiver ativada, o valor padrão da porta SSL será 9043.</p> <p>9080</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Servidor BAM</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SOAP</p> </td>
   <td><p>8880</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>MySQL</p> </td>
   <td><p>3306</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Oracle</p> </td>
   <td><p>1521</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>DB2®</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>A porta em que o servidor LDAP está sendo executado. Normalmente, a porta padrão é 389. No entanto, se você selecionar a opção SSL, a porta padrão normalmente é a 636. Confirme com o administrador LDAP que porta especificar.</p> </td>
  </tr>
 </tbody>
</table>

### Configuração do JBoss® para usar uma porta HTTP não padrão {#configuring-jboss-to-use-a-non-default-http-port}

O JBoss® Application Server usa 8080 como a porta HTTP padrão. O JBoss® também tem as portas pré-configuradas 8180, 8280 e 8380, que são comentadas no arquivo jboss-service.xml. Se você tiver um aplicativo em seu computador que já use essa porta, altere a porta que o AEM Forms no JEE usa seguindo estas etapas:

1. Abra o seguinte arquivo para edição:

   Instalação em um único servidor: [Raiz JBoss®]/standalone/configuration/standalone.xml

   Instalações do cluster: [Raiz JBoss®]/domain/configuration/domain.xml

1. Altere o valor de **porta** atributo no **&lt;socket-binding>** para um número de porta personalizado. Por exemplo, o seguinte usa a porta 8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot;/>

1. Salvar e fechar o arquivo.
1. Reinicie o servidor de aplicativos JBoss®.

## Considerações de segurança do AEM Forms no JEE {#aem-forms-on-jee-security-considerations}

Esta seção descreve algumas AEM Forms sobre problemas de segurança específicos do JEE que você deve saber.

### Credenciais de email não criptografadas no banco de dados {#email-credentials-not-encrypted-in-database}

As credenciais de email armazenadas pelas aplicações não são criptografadas antes de serem armazenadas no banco de dados do AEM Forms no JEE. Quando você configura um endpoint de serviço para usar email, as informações de senha usadas como parte dessa configuração de endpoint não são criptografadas quando armazenadas no banco de dados.

### Conteúdo confidencial para o Rights Management no banco de dados {#sensitive-content-for-rights-management-in-the-database}

O AEM Forms no JEE usa o banco de dados AEM Forms no JEE para armazenar informações confidenciais da chave do documento e outros materiais criptográficos usados para documentos de política. Proteger o banco de dados contra invasões ajuda a proteger essas informações confidenciais.

### Senha em formato de texto não criptografado {#password-in-clear-text-format-in-adobe-ds-xml}

O servidor de aplicativos usado para executar o AEM Forms no JEE requer sua própria configuração para acessar o banco de dados por meio de uma fonte de dados configurada no servidor de aplicativos. Certifique-se de que o servidor de aplicativos não exponha a senha do banco de dados em texto não criptografado no arquivo de configuração da origem de dados.

O lc_[banco de dados]O arquivo .xml não deve conter senha em formato de texto não criptografado. Consulte o fornecedor do servidor de aplicativos para saber como criptografar essas senhas para ele.

>[!NOTE]
>
>O instalador turnkey do AEM Forms no JEE JBoss® criptografa a senha do banco de dados.

O IBM® WebSphere® Application Server e o Oracle WebLogic Server podem criptografar senhas de origens de dados por padrão. No entanto, você deve confirmar com a documentação do servidor de aplicativos para garantir que isso esteja acontecendo.

### Protegendo a chave privada armazenada no Armazenamento de Confiança {#protecting-the-private-key-stored-in-trust-store}

As chaves privadas ou credenciais importadas no Trust Store são armazenadas no AEM Forms no banco de dados JEE. Para proteger o banco de dados e restringir o acesso somente aos administradores designados, tome as precauções adequadas.
