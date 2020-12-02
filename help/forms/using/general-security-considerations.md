---
title: Considerações gerais de segurança para AEM Forms no JEE
seo-title: Considerações gerais de segurança para AEM Forms no JEE
description: Saiba como se preparar para endurecer seu AEM Forms no ambiente JEE.
seo-description: Saiba como se preparar para endurecer seu AEM Forms no ambiente JEE.
uuid: 4d098731-fc8f-41d7-98b5-5c2e31211614
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 64bc6018-2828-4634-9275-48f1d411452b
docset: aem65
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 1%

---


# Considerações gerais de segurança para AEM Forms em JEE{#general-security-considerations-for-aem-forms-on-jee}

Este artigo fornece informações introdutórias que ajudam você a se preparar para endurecer seu ambiente AEM Forms. Ele inclui informações de pré-requisito sobre a AEM Forms em JEE, sistema operacional, servidor de aplicativos e segurança de banco de dados. Revise essas informações antes de continuar a bloquear seu ambiente.

## Informações de segurança específicas do fornecedor {#vendor-specific-security-information}

Esta seção contém informações relacionadas à segurança sobre sistemas operacionais, servidores de aplicativos e bancos de dados que estão incorporados à sua solução AEM Forms em JEE.

Use os links desta seção para encontrar informações de segurança específicas do fornecedor para seu sistema operacional, banco de dados e servidor de aplicativos.

### Informações de segurança do sistema operacional {#operating-system-security-information}

Ao proteger seu sistema operacional, considere cuidadosamente a implementação das medidas descritas pelo fornecedor do sistema operacional, incluindo o seguinte:

* Definição e controle de usuários, funções e privilégios
* Registros de monitoramento e trilhas de auditoria
* Remoção de serviços e aplicativos desnecessários
* Backup de arquivos

Para obter informações sobre segurança sobre sistemas operacionais compatíveis com a AEM Forms em JEE, consulte os recursos na tabela:

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
   <td><p><a href="https://www.ibm.com/support/knowledgecenter/ssw_aix_72/com.ibm.aix.security/security-kickoff.htm" target="_blank">Benefícios de segurança do IBM AIX</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft Windows Server® 2016 </p> </td>
   <td><p><a href="https://cloudblogs.microsoft.com/windowsserver/2017/08/22/now-available-windows-server-2016-security-guide/">Guia de Segurança do Windows Server 2016</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Linux® AP ou ES</p> </td>
   <td><p><a href="https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/pdf/security_guide/Red_Hat_Enterprise_Linux-7-Security_Guide-en-US.pdf" target="_blank">Red Hat Enterprise Linux Security Guide</a></p> </td>
  </tr>
  <tr>
   <td><p>Sun Solaris 11</p> </td>
   <td><p><a href="https://docs.oracle.com/cd/E53394_01/html/E54807/index.html" target="_blank">Diretrizes de segurança e proteção</a></p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Atualização 3</td>
   <td><a href="https://docs.oracle.com/cd/E52668_01/E54670/E54670.pdf" target="_blank">Guia de segurança para a versão 7</a><br /> </td>
  </tr>
  <tr>
   <td>CentOS 7<sup> </sup></td>
   <td><a href="https://wiki.centos.org/HowTos/OS_Protection" target="_blank">Documentação de proteção</a></td>
  </tr>
 </tbody>
</table>

### Informações de segurança do servidor de aplicativos {#application-server-security-information}

Ao proteger o servidor de aplicativos, considere cuidadosamente a implementação das medidas descritas pelo fornecedor do servidor, incluindo:

* Uso de nome de usuário de administrador não óbvio
* Desativação de serviços desnecessários
* Proteção do gerenciador de console
* Ativação de cookies seguros
* Fechando portas desnecessárias
* Limitação de clientes por endereços IP ou domínios
* Uso do Java™ Security Manager para restringir de forma programática privilégios

Para obter informações de segurança sobre servidores de aplicativos compatíveis com a AEM Forms em JEE, consulte os recursos nesta tabela.

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
   <td><p>Procure por Understanding WebLogic Security em <a href="https://download.oracle.com/docs/">https://download.oracle.com/docs/</a>.</p> </td>
  </tr>
  <tr>
   <td><p>IBM WebSphere®</p> </td>
   <td><p><a href="https://www.ibm.com/developerworks/websphere/zones/was/security/" target="_blank">Proteção dos aplicativos e seus ambientes</a></p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® JBoss®</p> </td>
   <td><p><a href="https://docs.jboss.org/author/display/AS7/Security+subsystem+configuration">Configuração do subsistema de segurança</a></p> </td>
  </tr>
 </tbody>
</table>

### Informações de segurança do banco de dados {#database-security-information}

Ao proteger seu banco de dados, considere implementar as medidas descritas pelo fornecedor do banco de dados, incluindo:

* Restrição de operações com controles de acesso (ACLs)
* Uso de portas não padrão
* Ocultar o banco de dados por trás de um firewall
* Criptografar dados confidenciais antes de gravá-los no banco de dados (consulte a documentação do fabricante do banco de dados)

Para obter informações de segurança sobre bancos de dados compatíveis com a AEM Forms em JEE, consulte os recursos nesta tabela.

<table>
 <thead>
  <tr>
   <th><p>Banco de dados</p> </th>
   <th><p>Recurso de segurança</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>IBM DB2® 11.1</p> </td>
   <td><p><a href="https://www-01.ibm.com/software/data/db2/library/">Biblioteca da família de produtos DB2</a></p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td>Pesquise na Web por "SQL Server 2016: Segurança"</td>
  </tr>
  <tr>
   <td><p>MySQL 5</p> </td>
   <td><p><a href="https://dev.mysql.com/doc/refman/5.0/en/security.html">Problemas gerais de segurança do MySQL 5.0</a></p> <p><a href="https://dev.mysql.com/doc/refman/5.1/en/security.html">Problemas gerais de segurança do MySQL 5.1</a></p> </td>
  </tr>
  <tr>
   <td><p>Oracle® 12c</p> </td>
   <td><p>Consulte o capítulo Segurança na <a href="https://docs.oracle.com/database/121/TDPSG/GUID-6E2F4E53-5D87-4FCD-9C9C-6792217D7014.htm#TDPSG94426" target="_blank">documentação do Oracle 12g</a></p> </td>
  </tr>
 </tbody>
</table>

Esta tabela descreve as portas padrão que precisam ser abertas durante o processo de configuração do AEM Forms no JEE. Se estiver se conectando por https, ajuste as informações da porta e os endereços IP de acordo. Para obter mais informações sobre a configuração de portas, consulte o documento *Instalação e Implantação do AEM Forms no JEE* para seu servidor de aplicativos.

<table>
 <thead>
  <tr>
   <th><p>Produto ou serviço</p> </th>
   <th><p>Número da porta</p> </th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>JBoss</p> </td>
   <td><p>8080</p> </td>
  </tr>
  <tr>
   <td><p>WebLogic</p> </td>
   <td><p>7001</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>Servidor gerenciado WebLogic</p> </td>
   <td><p>Definido pelo administrador durante a configuração</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>WebSphere</p> </td>
   <td><p>9060, se o Global Security estiver ativado, o valor padrão da porta SSL será 9043.</p> <p>9080</p> </td>
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
   <td>&gt;<p>DB2</p> </td>
   <td><p>50000</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>SQL Server</p> </td>
   <td><p>1433</p> </td>
  </tr>
  <tr>
   <td>&gt;<p>LDAP</p> </td>
   <td><p>A porta na qual o servidor LDAP está sendo executado. Normalmente, a porta padrão é 389. No entanto, se você selecionar a opção SSL, a porta padrão é normalmente 636. Confirme com o administrador LDAP qual porta especificar.</p> </td>
  </tr>
 </tbody>
</table>

### Configurando JBoss para usar uma porta HTTP não padrão {#configuring-jboss-to-use-a-non-default-http-port}

O JBoss Application Server usa 8080 como a porta HTTP padrão. O JBoss também tem portas pré-configuradas 8180, 8280 e 8380, que são comentadas no arquivo jEFP-service.xml. Se você tiver um aplicativo em seu computador que já usa essa porta, altere a porta que a AEM Forms no JEE usa seguindo estas etapas:

1. Abra o seguinte arquivo para edição:

   Instalação do Single Server: [Raiz JBoss]/standalone/configuration/standalone.xml

   Instalações de cluster: [Raiz JBoss]/domain/configuration/domain.xml

1. Altere o valor do atributo **port** na tag **&lt;socket-binding>** para um número de porta personalizado. Por exemplo, o seguinte usa a porta 8090:

   &lt;socket-binding name=&quot;http&quot; port=&quot;8090&quot; />

1. Salve e feche o arquivo.
1. Reinicie o servidor de aplicativos JBoss.

## Considerações de segurança do AEM Forms em JEE {#aem-forms-on-jee-security-considerations}

Esta seção descreve alguns AEM Forms sobre problemas de segurança específicos de JEE que você deve conhecer.

### Credenciais de email não criptografadas no banco de dados {#email-credentials-not-encrypted-in-database}

As credenciais de email armazenadas pelos aplicativos não são criptografadas antes de serem armazenadas no AEM Forms no banco de dados JEE. Quando você configura um terminal de serviço para usar email, qualquer informação de senha usada como parte dessa configuração de terminal não é criptografada quando é armazenada no banco de dados.

### Conteúdo sensível para o Rights Management no banco de dados {#sensitive-content-for-rights-management-in-the-database}

A AEM Forms em JEE usa o banco de dados AEM Forms em JEE para armazenar informações confidenciais sobre chaves de documento e outro material criptográfico usado para documentos de política. Proteger o banco de dados contra invasão ajuda a proteger essas informações confidenciais.

### Senha em forma de texto transparente {#password-in-clear-text-format-in-adobe-ds-xml}

O servidor de aplicativos usado para executar o AEM Forms no JEE requer sua própria configuração para acesso ao banco de dados por meio de uma fonte de dados configurada no servidor de aplicativos. Certifique-se de que o servidor de aplicativos não exponha a senha do banco de dados em texto nítido em seu arquivo de configuração da fonte de dados.

O arquivo lc_[database].xml não deve conter senha em formato de texto claro. Consulte o fornecedor do servidor de aplicativos sobre como criptografar essas senhas para o servidor de aplicativos.

>[!NOTE]
>
>O instalador chave-na-mão JBoss do AEM Forms em JEE criptografa a senha do banco de dados.

O IBM WebSphere Application Server e o Oracle WebLogic Server podem criptografar senhas de fontes de dados por padrão. No entanto, confirme com a documentação do servidor de aplicativos para garantir que isso esteja acontecendo.

### Proteger a chave privada armazenada no Repositório de Confiança {#protecting-the-private-key-stored-in-trust-store}

As chaves privadas ou credenciais importadas no Repositório de Confiança são armazenadas no AEM Forms no banco de dados JEE. Tome as precauções apropriadas para proteger o banco de dados e restringir o acesso somente a administradores designados.
