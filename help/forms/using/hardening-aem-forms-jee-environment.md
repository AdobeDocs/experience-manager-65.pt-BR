---
title: Fortalecimento do AEM Forms no ambiente JEE
description: Conheça uma variedade de configurações de fortalecimento de segurança para melhorar a segurança do AEM Forms no JEE executado em uma intranet corporativa.
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
role: Admin,User
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
solution: Experience Manager, Experience Manager Forms
feature: Document Security,Adaptive Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '7608'
ht-degree: 1%

---

# Fortalecimento do AEM Forms no ambiente JEE {#hardening-your-aem-forms-on-jee-environment}

Conheça uma variedade de configurações de fortalecimento de segurança para melhorar a segurança do AEM Forms no JEE executado em uma intranet corporativa.

O artigo descreve recomendações e práticas recomendadas para proteger servidores que executam o AEM Forms no JEE. Este não é um documento abrangente de fortalecimento do host para o seu sistema operacional e servidores de aplicativos. Em vez disso, este artigo descreve uma variedade de configurações que fortalecem a segurança que você deve implementar para melhorar a segurança do AEM Forms no JEE que está sendo executado em uma intranet corporativa. No entanto, para garantir que o AEM Forms nos servidores de aplicativos JEE permaneça seguro, você também deve implementar procedimentos de monitoramento de segurança, detecção e resposta.

O artigo descreve técnicas de proteção que devem ser aplicadas durante os seguintes estágios durante o ciclo de vida de instalação e configuração:

* **Pré-instalação:** Use essas técnicas antes de instalar o AEM Forms no JEE.
* **Instalação:** Use essas técnicas durante o processo de instalação do AEM Forms no JEE.
* **Pós-instalação:** Use essas técnicas após a instalação e periodicamente a partir de então.

O AEM Forms no JEE é altamente personalizável e pode funcionar em vários ambientes diferentes. Algumas recomendações podem não se ajustar às necessidades de sua organização.

## Pré-instalação {#preinstallation}

Antes de instalar o AEM Forms no JEE, você pode aplicar soluções de segurança à camada de rede e ao sistema operacional. Esta seção descreve alguns problemas e faz recomendações para reduzir as vulnerabilidades de segurança nessas áreas.

**Instalação e configuração no UNIX e Linux**

Você não deve instalar ou configurar o AEM Forms no JEE usando um shell raiz. Por padrão, os arquivos são instalados no diretório /opt, e o usuário que executa a instalação precisa de todas as permissões de arquivo em /opt. Como alternativa, uma instalação pode ser executada no diretório /user de um usuário individual onde ele já tem todas as permissões de arquivo.

**Instalação e configuração no Windows**

Você deve executar a instalação no Windows como administrador se estiver instalando o AEM Forms no JEE em JBoss usando o método turnkey ou se estiver instalando o PDF Generator. Além disso, ao instalar o PDF Generator no Windows com suporte a aplicativos nativos, você deve executar a instalação como o mesmo usuário do Windows que instalou o Microsoft Office. Para obter mais informações sobre privilégios de instalação, consulte o documento* Instalação e implantação do AEM Forms no JEE* para o seu servidor de aplicativos.

### Segurança de camada de rede {#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de proteção dos hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o fortalecimento da pilha do protocolo de controle de transmissão/protocolo de Internet (TCP/IP) e o uso de firewalls para proteção de host.

A tabela a seguir descreve processos comuns que reduzem as vulnerabilidades de segurança da rede.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrição</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Zonas desmilitarizadas (DMZs)</p> </td> 
   <td><p>Implantar servidores de formulários em uma zona desmilitarizada (DMZ). A segmentação deve existir em pelo menos dois níveis, com o servidor de aplicativos usado para executar o AEM Forms no JEE, colocado atrás do firewall interno. Separe a rede externa da DMZ que contém os servidores Web, que por sua vez devem ser separados da rede interna. Use firewalls para implementar as camadas de separação. Categorize e controle o tráfego que passa por cada camada de rede para garantir que apenas o mínimo absoluto de dados necessários seja permitido.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Endereços IP privados</p> </td> 
   <td><p>Use a Conversão de Endereços de Rede (NAT) com endereços IP privados RFC 1918 no servidor de aplicativos AEM Forms. Atribua endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear o tráfego de e para um host interno NAT pela Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewalls</p> </td> 
   <td><p>Use os seguintes critérios para selecionar uma solução de firewall:</p> 
    <ul> 
     <li><p>Implementar firewalls que suportam servidores proxy e/ou <em>inspeção com estado</em> em vez de soluções simples de filtragem de pacotes.</p> </li> 
     <li><p>Use um firewall que ofereça suporte a <em>negar todos os serviços, exceto os explicitamente permitidos</em> paradigmas de segurança.</p> </li> 
     <li><p>Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o mais alto nível de segurança e ajuda a impedir que usuários não autorizados ignorem a segurança do firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Portas do banco de dados</p> </td> 
   <td><p>Não usar portas de escuta padrão para bancos de dados (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Para obter informações sobre como alterar portas de banco de dados, consulte a documentação do banco de dados.</p> <p>O uso de uma porta de banco de dados diferente afeta a configuração geral do AEM Forms no JEE. Se você alterar as portas padrão, deverá fazer modificações correspondentes em outras áreas de configuração, como as fontes de dados do AEM Forms no JEE.</p> <p>Para obter informações sobre como configurar fontes de dados no AEM Forms no JEE, consulte Instalar e atualizar o AEM Forms no JEE ou atualizar para o AEM Forms no JEE para o servidor de aplicativos em <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guia do usuário do AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do sistema operacional {#operating-system-security}

A tabela a seguir descreve algumas abordagens possíveis para minimizar as vulnerabilidades de segurança encontradas no sistema operacional.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p></th> 
   <th><p>Descrição</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Patches de segurança</p></td> 
   <td><p>Há um risco maior de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e as atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção.</p><p>Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software de proteção contra vírus</p></td> 
   <td><p>Verificadores de vírus podem identificar arquivos infectados ao verificar uma assinatura ou observar comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como novos vírus são descobertos com frequência, você deve atualizar esse arquivo com frequência para que o verificador de vírus identifique todos os vírus atuais.</p></td> 
  </tr> 
  <tr> 
   <td><p>Protocolo de tempo de rede (NTP)</p></td> 
   <td><p>Para análise jurídica, mantenha o tempo preciso nos servidores de formulários. Use o NTP para sincronizar o horário em todos os sistemas conectados diretamente à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Para obter informações adicionais sobre segurança para seu sistema operacional, consulte [&quot;Informações de segurança do sistema operacional&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Instalação {#installation}

Esta seção descreve técnicas que você pode usar durante o processo de instalação do AEM Forms para reduzir vulnerabilidades de segurança. Em alguns casos, essas técnicas usam opções que fazem parte do processo de instalação. A tabela a seguir descreve essas técnicas.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrição</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Privilégios</p> </td> 
   <td><p>Use o número mínimo de privilégios necessários para instalar o software. Faça logon no computador usando uma conta que não esteja no grupo Administradores. No Windows, você pode usar o comando Executar como para executar o instalador do AEM Forms no JEE como um usuário administrativo. Em sistemas UNIX e Linux, use um comando como <code>sudo</code> para instalar o software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fonte de software</p> </td> 
   <td><p>Não baixe nem execute o AEM Forms no JEE a partir de fontes não confiáveis.</p> <p>Programas mal-intencionados podem conter código para violar a segurança de várias maneiras, incluindo roubo, modificação e exclusão de dados e negação de serviço. Instale o AEM Forms no JEE a partir do DVD de Adobe ou somente a partir de uma fonte confiável.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partições de disco</p> </td> 
   <td><p>Coloque o AEM Forms no JEE em uma partição de disco dedicada. A segmentação de disco é um processo que mantém dados específicos do servidor em discos físicos separados para aumentar a segurança. A organização de dados dessa maneira reduz o risco de ataques de travessia de diretório. Plano para criar uma partição separada da partição do sistema na qual você pode instalar o AEM Forms no diretório de conteúdo JEE. (No Windows, a partição do sistema contém o diretório system32 ou a partição de inicialização.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componentes</p> </td> 
   <td><p>Avalie os serviços existentes e desative ou desinstale os que não forem necessários. Não instale componentes e serviços desnecessários.</p> <p>A instalação padrão de um servidor de aplicativos pode incluir serviços que não são necessários para o seu uso. Você deve desativar todos os serviços desnecessários antes da implantação para minimizar os pontos de entrada de um ataque. Por exemplo, no JBoss, você pode comentar serviços desnecessários no arquivo do descritor META-INF/jboss-service.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Arquivo de política entre domínios</p> </td> 
   <td><p>A presença de uma <code>crossdomain.xml</code> arquivo no servidor pode enfraquecer imediatamente esse servidor. É recomendável tornar a lista de domínios o mais restritiva possível. Não coloque o <code>crossdomain.xml</code> arquivo que foi usado durante o desenvolvimento na produção ao usar os Guias <em>(obsoleto)</em>. Para um guia que usa serviços da Web, se o serviço estiver no mesmo servidor que serviu o guia, um <code>crossdomain.xml</code> o arquivo não é necessário. Mas se o serviço estiver em outro servidor ou se houver clusters envolvidos, a presença de um <code>crossdomain.xml</code> arquivo seria necessário. Consulte <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>, para obter mais informações sobre o arquivo crossdomain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de segurança do sistema operacional</p> </td> 
   <td><p>Se você precisar usar criptografia XML de 192 ou 256 bits nas plataformas Solaris, certifique-se de instalar <code>pkcs11_softtoken_extra.so</code> em vez de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Etapas de pós-instalação {#post-installation-steps}

Depois de instalar o AEM Forms no JEE com êxito, é importante manter o ambiente periodicamente de uma perspectiva de segurança.

A seção a seguir descreve em detalhes as diferentes tarefas recomendadas para proteger o Forms Server implantado.

### Segurança do AEM Forms {#aem-forms-security}

As configurações recomendadas a seguir se aplicam ao servidor do AEM Forms no JEE fora do aplicativo Web administrativo. Para reduzir os riscos de segurança para o servidor, aplique essas configurações imediatamente após instalar o AEM Forms no JEE.

**Patches de segurança**

Há um risco maior de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e as atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção para garantir a compatibilidade e a disponibilidade dos aplicativos. Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. As atualizações do AEM Forms no JEE estão no site de download de produtos Enterprise.

**Contas de serviço (JBoss turnkey no Windows apenas)**

O AEM Forms no JEE instala um serviço, por padrão, usando a conta LocalSystem. A conta de usuário LocalSystem interna tem um alto nível de acessibilidade; ela faz parte do grupo Administradores. Se uma identidade do processo de trabalho for executada como a conta de usuário LocalSystem, esse processo de trabalho terá acesso total a todo o sistema.

Para executar o servidor de aplicativos no qual o AEM Forms no JEE é implantado, usando uma conta não administrativa específica, siga estas instruções:

1. No Microsoft Management Console (MMC), crie um usuário local para o serviço Forms Server para fazer logon como:

   * Selecionar **Usuário não pode alterar senha**.
   * No **Membro de** , verifique se **Usuários** grupo está listado.

   >[!NOTE]
   >
   >Não é possível alterar essa configuração para PDF Generator.

1. Selecionar **Início** > **Configurações** > **Ferramentas administrativas** > **Serviços**.
1. Clique duas vezes no JBoss para AEM Forms no JEE e interrompa o serviço.
1. No **Fazer Logon** selecione **Esta conta**, procure a conta de usuário que você criou e digite a senha da conta.
1. No MMC, abra **Configurações de segurança locais** e selecione **Políticas Locais** > **Atribuição de direitos do usuário**.
1. Atribua os seguintes direitos à conta de usuário em que o Forms Server está sendo executado:

   * Negar logon pelos Serviços de Terminal
   * Negar logon local
   * Fazer logon como serviço (já deve estar definido)

1. Conceda à nova conta de usuário permissões de modificação nos seguintes diretórios:
   * **Diretório de Armazenamento Global de Documentos (GDS)**: o local do diretório GDS é configurado manualmente durante o processo de instalação do AEM Forms. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório do repositório CRX**: o local padrão é `[AEM-Forms-installation-location]\crx-repository`
   * **Diretórios temporários do AEM Forms**:
      * Caminho TMP ou TEMP (Windows) conforme definido nas variáveis de ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectado Em sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como o diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Conceda à nova conta de usuário permissões de gravação nos seguintes diretórios:
   * [JBoss-diretory]\independente\implantação
   * [JBoss-diretory]\autônomo\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   >O local de instalação padrão do JBoss Application Server:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/

1. Inicie o servidor de aplicativos.

**Desabilitando o servlet de inicialização do Configuration Manager**

O Configuration Manager usou um servlet implantado em seu servidor de aplicativos para executar a inicialização do AEM Forms no banco de dados JEE. Como o Configuration Manager acessa esse servlet antes que a configuração seja concluída, o acesso a ele não foi protegido para usuários autorizados e deve ser desativado após você ter usado com êxito o Configuration Manager para configurar o AEM Forms no JEE.

1. Descompacte o adobe-livecycle-[appserver]arquivo .ear.
1. Abra o arquivo META-INF/application.xml.
1. Procure a seção adobe-bootstrapper.war:

   ```java
   <!-- bootstrapper start --> 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   <!-- bootstrapper end-->
   ```

1. Pare o servidor do AEM Forms.
1. Comente o adobe-bootstrapper.war e o adobe-lcm-bootstrapper-rediretory. módulos war como se segue:

   ```java
   <!-- bootstrapper start --> 
   <!-- 
   <module id="WebApp_adobe_bootstrapper"> 
       <web> 
           <web-uri>adobe-bootstrapper.war</web-uri> 
           <context-root>/adobe-bootstrapper</context-root> 
       </web> 
   </module> 
   <module id="WebApp_adobe_lcm_bootstrapper_redirector"> 
       <web> 
           <web-uri>adobe-lcm-bootstrapper-redirector.war</web-uri> 
           <context-root>/adobe-lcm-bootstrapper</context-root> 
       </web> 
   </module> 
   --> 
   <!-- bootstrapper end-->
   ```

1. Salve e feche o arquivo META-INF/application.xml
1. Compacte o arquivo EAR e reimplante-o no servidor de aplicativos.
1. Inicie o servidor do AEM Forms.
1. Digite o URL abaixo em um navegador para testar a alteração e garantir que ela não funcione mais.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Bloquear acesso remoto ao Armazenamento de Confiança**

O Configuration Manager permite que você carregue uma credencial de extensões do Acrobat Reader DC na loja de confiança do AEM Forms no JEE. Isso significa que o acesso ao Serviço de Credenciais do Armazenamento de Confiança em protocolos remotos (SOAP e EJB) foi habilitado por padrão. Esse acesso não será mais necessário depois que você tiver carregado a credencial de Direitos usando o Configuration Manager ou se decidir usar o Console de Administração posteriormente para gerenciar credenciais.

Você pode desabilitar o acesso remoto a todos os serviços de Armazenamento Confiável seguindo as etapas da seção [Desativar o acesso remoto não essencial aos serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Desabilitar todo o acesso anônimo não essencial**

Alguns serviços do Forms Server têm operações que podem ser chamadas por um chamador anônimo. Se o acesso anônimo a esses serviços não for necessário, desative-o seguindo as etapas em [Desabilitação de acesso anônimo não essencial a serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Alterar a senha padrão do administrador {#change-the-default-administrator-password}

Quando o AEM Forms no JEE é instalado, uma única conta de usuário padrão é configurada para o usuário Super Administrador/ administrador de ID de logon com uma senha padrão de *senha*. Você deve alterar essa senha imediatamente usando o Gerenciador de configurações.

1. Digite o seguinte URL em um navegador da Web:

   ```java
   https://[host name]:[port]/adminui
   ```

   O número de porta padrão é um destes:

   **JBoss:** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080.

1. No **Nome do usuário** campo, tipo `administrator` e, no **Senha** campo, tipo `password`.
1. Clique em **Configurações** > **User Management** > **Usuários e grupos**.
1. Tipo `administrator` no **Localizar** e clique em **Localizar**.
1. Clique em **Superadministrador** na lista de usuários.
1. Clique em **Alterar senha** na página Editar Usuário.
1. Especifique a nova senha e clique em **Salvar**.

Além disso, é recomendável alterar a senha padrão do Administrador do CRX executando as seguintes etapas:

1. Efetue logon no `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` usando o nome de usuário/senha padrão.
1. Digite Administrador no campo de pesquisa e clique em **Ir**.
1. Selecionar **Administrador** do resultado da pesquisa e clique no botão **Editar** no canto inferior direito da interface.
1. Especifique a nova senha na caixa **Nova senha** e a senha antiga na caixa **Sua senha** campo.
1. Clique no ícone Salvar na parte inferior direita da interface.

#### Desativar geração de WSDL {#disable-wsdl-generation}

A geração da WSDL (Web Service Definition Language) deve ser ativada somente para ambientes de desenvolvimento, onde a geração WSDL é usada pelos desenvolvedores para criar seus aplicativos clientes. Você pode optar por desativar a geração WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

1. Digite o seguinte URL em um navegador da Web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Selecionar **Configurações > Configurações principais do sistema > Configurações**.
1. Desmarcar **Ativar WSDL** e selecione **OK**.

### Segurança do servidor de aplicativos {#application-server-security}

A tabela a seguir descreve algumas técnicas para proteger o servidor de aplicativos após a instalação do aplicativo AEM Forms no JEE.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrição</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Console administrativo do servidor de aplicativos</p> </td> 
   <td><p>Depois de instalar, configurar e implantar o AEM Forms no JEE em seu servidor de aplicativos, você deve desabilitar o acesso aos consoles administrativos do servidor de aplicativos. Consulte a documentação do servidor de aplicativos para obter detalhes.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de cookie do servidor de aplicativos</p> </td> 
   <td><p>Os cookies do aplicativo são controlados pelo servidor do aplicativo. Ao disponibilizar a aplicação, o administrador do servidor de aplicações pode especificar preferências de cookie em todo o servidor ou com base na aplicação específica. Por padrão, as configurações do servidor têm preferência.</p> <p>Todos os cookies de sessão gerados pelo seu servidor de aplicativos devem incluir o <code>HttpOnly</code> atributo. Por exemplo, ao usar o servidor da aplicação JBoss, você pode modificar o elemento SessionCookie para <code>httpOnly="true"</code> no <code>WEB-INF/web.xml</code> arquivo.</p> <p>Você pode restringir os cookies a serem enviados usando somente HTTPS. Como resultado, eles não são enviados não criptografados por HTTP. Os administradores do servidor de aplicativos devem ativar cookies seguros para o servidor globalmente. Por exemplo, ao usar o JBoss Application Server, você pode modificar o elemento do conector para <code>secure=true</code> no <code>server.xml</code> arquivo.</p> <p>Consulte a documentação do servidor de aplicativos para obter mais detalhes sobre configurações de cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Navegação no diretório</p> </td> 
   <td><p>Quando alguém solicita uma página que não existe ou solicita o nome de um diretório (a string de solicitação termina com uma barra (/)), o servidor de aplicativos não deve retornar o conteúdo desse diretório. Para evitar que isso aconteça, você pode desativar a navegação de diretórios no seu servidor de aplicativos. Você deve fazer isso para o aplicativo do console de administração e para outros aplicativos em execução no servidor.</p> <p>Para JBoss, defina o valor do parâmetro de inicialização listings de <code>DefaultServlet</code> propriedade para <code>false</code> no arquivo web.xml, conforme mostrado neste exemplo:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;padrão&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listagens&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Para o WebSphere, defina o <code>directoryBrowsingEnabled</code> no arquivo ibm-web-ext.xmi para <code>false</code>.</p> <p>Para o WebLogic, defina as propriedades index-directories no arquivo weblogic.xml como <code>false</code>, conforme mostrado neste exemplo:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do banco de dados {#database-security}

Ao proteger seu banco de dados, você deve implementar as medidas descritas pelo fornecedor do banco de dados. Você deve alocar um usuário do banco de dados com as permissões de banco de dados mínimas necessárias concedidas para uso pelo AEM Forms no JEE. Por exemplo, não use uma conta com privilégios de administrador de banco de dados.

No Oracle, a conta do banco de dados que você usa precisa apenas dos privilégios CONNECT, RESOURCE e CREATE VIEW. Para requisitos semelhantes em outros bancos de dados, consulte [Preparando para instalar o AEM Forms no JEE (servidor único)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configurando segurança integrada para SQL Server no Windows para JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modificar [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} para adicionar `integratedSecurity=true` ao URL de conexão, conforme mostrado neste exemplo:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Adicione o arquivo sqljdbc_auth.dll ao caminho de sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado com a instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Modifique a propriedade do serviço JBoss do Windows (JBoss para AEM Forms em JEE) para Fazer logon como no sistema local para uma conta de logon que tenha um banco de dados AEM Forms e um conjunto mínimo de privilégios. Se você estiver executando o JBoss na linha de comando e não como um serviço do Windows, não será necessário executar essa etapa.
1. Definir Segurança para o SQL Server a partir de **Misto** para **Somente Autenticação do Windows**.

#### Configurando a segurança integrada do SQL Server no Windows para WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Inicie a Console de Administração do WebLogic Server digitando o seguinte URL na linha URL de um web browser:

   ```java
   https://[host name]:7001/console
   ```

1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura do domínio, clique em *[base_domain]* > **Serviços** > **JDBC** > **Fontes de dados** e, no painel direito, clique em **IDP_DS**.
1. Na tela seguinte, na guia **Configuração** clique na guia **Pool de conexão** e, na guia **Propriedades** caixa, digite `integratedSecurity=true`.
1. Em Estrutura do domínio, clique em **[base_domain]** > **Serviços** > **JDBC** > **Fontes de dados** e, no painel direito, clique em **RM_DS**.
1. Na tela seguinte, na guia **Configuração** clique na guia **Pool de conexão** e, na guia **Propriedades** caixa, digite `integratedSecurity=true`.
1. Adicione o arquivo sqljdbc_auth.dll ao caminho de sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado com a instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Definir Segurança para o SQL Server a partir de **Misto** para **Somente Autenticação do Windows**.

#### Configuração da segurança integrada do SQL Server no Windows para WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

No WebSphere, você pode configurar a segurança integrada somente quando usar um driver JDBC externo do SQL Server, não o driver JDBC do SQL Server incorporado ao WebSphere.

1. Faça logon no Console administrativo do WebSphere.
1. Na árvore de navegação, clique em **Recursos** > **JDBC** > **Fontes de dados** e, no painel direito, clique em **IDP_DS**.
1. No painel direito, em Propriedades adicionais, clique em **Propriedades Personalizadas** e clique em **Novo**.
1. No **Nome** caixa, digite `integratedSecurity` e, no **Valor** caixa, digite `true`.
1. Na árvore de navegação, clique em **Recursos** > **JDBC** > **Fontes de dados** e, no painel direito, clique em **RM_DS**.
1. No painel direito, em Propriedades adicionais, clique em **Propriedades Personalizadas** e clique em **Novo**.
1. No **Nome** caixa, digite `integratedSecurity` e, no **Valor** caixa, digite `true`.
1. No computador em que o WebSphere está instalado, adicione o arquivo sqljdbc_auth.dll ao caminho de sistemas do Windows (C:\Windows). O arquivo sqljdbc_auth.dll está no mesmo local que a instalação do driver Microsoft SQL JDBC 1.2 (o padrão é *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Selecionar **Início** > **Painel de controle do Campaign** > **Serviços**, clique com o botão direito do mouse no serviço Windows para WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) e selecione **Propriedades**.
1. Na caixa de diálogo Propriedades, clique na guia **Fazer Logon** guia.
1. Selecionar **Esta conta** e forneça as informações necessárias para definir a conta de logon que deseja usar.
1. Definir Segurança no SQL Server a partir de **Misto** para **Somente Autenticação do Windows**.

### Proteção do acesso a conteúdo confidencial no banco de dados {#protecting-access-to-sensitive-content-in-the-database}

O schema do banco de dados do AEM Forms contém informações confidenciais sobre a configuração do sistema e os processos comerciais e deve estar oculto atrás do firewall. O banco de dados deve ser considerado dentro do mesmo limite de confiança que o Forms Server. Para evitar a divulgação de informações e o roubo de dados de negócios, o banco de dados deve ser configurado pelo administrador do banco de dados (DBA) para permitir o acesso somente por administradores autorizados.

Como precaução adicional, você deve considerar o uso de ferramentas específicas do fornecedor do banco de dados para criptografar colunas em tabelas que contenham os seguintes dados:

* Chaves do documento Rights Management
* Chave de criptografia do PIN HSM do armazenamento de confiança
* Hashes de Senha de Usuário Local

Para obter informações sobre ferramentas específicas de fornecedores, consulte [&quot;Informações de segurança do banco de dados&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Segurança LDAP {#ldap-security}

Um diretório LDAP (Lightweight Diretory Access Protocol) é normalmente usado pelo AEM Forms no JEE como uma origem para informações de usuários e grupos empresariais e um meio de executar a autenticação de senha. Você deve garantir que seu diretório LDAP esteja configurado para usar SSL (Secure Socket Layer) e que o AEM Forms no JEE esteja configurado para acessar seu diretório LDAP usando sua porta SSL.

#### Negação de serviço LDAP {#ldap-denial-of-service}

Um ataque comum usando o LDAP envolve um invasor que deliberadamente não consegue se autenticar várias vezes. Isso força o Servidor de Diretório LDAP a bloquear um usuário de todos os serviços dependentes de LDAP.

Você pode definir o número de tentativas com falha e o tempo de bloqueio subsequente que a AEM Forms implementa quando um usuário falha repetidamente ao autenticar no AEM Forms. No Console de administração, escolha valores baixos. Ao selecionar o número de tentativas com falha, é importante compreender que, após todas as tentativas, o AEM Forms bloqueará o usuário antes que o Servidor de Diretório LDAP o faça.

#### Definir bloqueio automático de conta {#set-automatic-account-locking}

1. Faça logon no Console de administração.
1. Clique em **Configurações** > **User Management** > **Gerenciamento de domínio**.
1. Em Configurações de bloqueio automático de conta, defina **Máximo de falhas de autenticação consecutivas** para um número baixo, como 3.
1. Clique em **Salvar**.

### Auditoria e registro {#auditing-and-logging}

O uso adequado e seguro da auditoria e do registro de aplicativos pode ajudar a garantir que eventos de segurança e outros eventos anômalos sejam rastreados e detectados o mais rápido possível. O uso eficiente da auditoria e do registro em um aplicativo inclui itens como rastreamento de logons bem-sucedidos e com falha e eventos-chave do aplicativo, como a criação ou a exclusão de registros-chave.

Você pode usar a auditoria para detectar muitos tipos de ataques, incluindo estes:

* Ataques de senha com força bruta
* Ataques de negação de serviço
* Injeção de entrada hostil e classes relacionadas de ataques de script

Esta tabela descreve as técnicas de auditoria e registro que podem ser usadas para reduzir as vulnerabilidades do servidor.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p> </th> 
   <th><p>Descrição</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>ACLs de arquivo de log</p> </td> 
   <td><p>Defina o AEM Forms apropriado nas listas de controle de acesso (ACLs) do arquivo de log JEE.</p> <p>Definir as credenciais apropriadas ajuda a impedir que invasores excluam os arquivos.</p> <p>As permissões de segurança no diretório do arquivo de log devem ser Controle Total para Administradores e grupos SYSTEM. A conta de usuário do AEM Forms deve ter permissões somente de Leitura e Gravação.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redundância de arquivo de log</p> </td> 
   <td><p>Se os recursos permitirem, envie logs para outro servidor em tempo real que não esteja acessível pelo invasor (somente gravação) usando Syslog, Tivoli, Microsoft Operations Manager (MOM) Server ou outro mecanismo.</p> <p>Proteger registros dessa maneira ajuda a impedir adulterações. Além disso, o armazenamento de logs em um repositório central auxilia na correlação e no monitoramento (por exemplo, se vários servidores de formulários estiverem em uso e um ataque de detecção de senha estiver ocorrendo em vários computadores onde cada computador é consultado para obter uma senha).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Permitir que um usuário não administrador execute o PDF Generator

Você pode permitir que um usuário não administrador use o PDF Generator. Normalmente, somente usuários com privilégios administrativos podem usar o PDF Generator. Execute as seguintes etapas para permitir que um usuário não administrador execute o PDF Generator:

1. Crie um nome de variável de ambiente PDFG_NON_ADMIN_ENABLED.

1. Defina o valor da variável como TRUE.

1. Reinicie a instância do AEM Forms.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Configuração do AEM Forms no JEE para acesso fora da empresa {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Depois de instalar o AEM Forms no JEE, é importante manter a segurança do ambiente periodicamente. Esta seção descreve as tarefas recomendadas para manter a segurança do AEM Forms no servidor de produção JEE.

### Configuração de um proxy reverso para acesso à Web {#setting-up-a-reverse-proxy-for-web-access}

A *proxy reverso* pode ser usado para garantir que um conjunto de URLs para o AEM Forms em aplicações Web JEE esteja disponível para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos em que o AEM Forms no JEE está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor da aplicação que está executando o AEM Forms no JEE. Os usuários só têm acesso de rede ao proxy reverso e só podem tentar conexões de URL compatíveis com o proxy reverso.

**AEM Forms em URLs raiz JEE para uso com servidor proxy reverso**

Os seguintes URLs raiz da aplicação para cada AEM Forms na aplicação Web JEE. Você deve configurar seu proxy reverso apenas para expor URLs para a funcionalidade do aplicativo web que você deseja fornecer aos usuários finais.

Determinados URLs são destacados como aplicações Web voltadas para o usuário final. Você deve evitar expor outros URLs do Configuration Manager para acesso a usuários externos por meio do proxy reverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL raiz</p> </th> 
   <th><p>Finalidade e/ou aplicativo web associado</p> </th> 
   <th><p>Interface baseada na Web</p> </th> 
   <th><p>Acesso do usuário final</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>aplicativo web do usuário final de extensões do Acrobat Reader DC para aplicar direitos de uso a documentos do PDF</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>aplicativo web de usuário final do Rights Management</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL do serviço Web para o Rights Management</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>aplicativo web de administração de PDF Generator</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace/*</p> </td> 
   <td><p>Aplicativo Web do usuário final do Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets e serviços de dados do Workspace exigidos pelo aplicativo cliente do Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet para inicializar o AEM Forms no repositório JEE</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Página de informações dos serviços Web do Forms Server</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL do serviço da Web para todos os serviços do Forms Server</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>aplicativo web de administração de Rights Management</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Home page do Console de Administração</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>seguro/*</p> </td> 
   <td><p>Páginas de administração do Gerenciamento de Repositório de Confiança</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Aplicativo IVS do Forms para teste e depuração da renderização de formulários</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Aplicativo IVS de saída para serviço de teste e depuração de saída</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rmws/*</p> </td> 
   <td><p>URL REST para Rights Management</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputAdmin/*</p> </td> 
   <td><p>Páginas de administração de saída</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Arquivos de aplicativo web do Forms</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Usado para obter JavaScript durante a transformação de HTML</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Páginas de administração do Forms</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/repository/*</p> </td> 
   <td><p>URL para acesso WebDAV (depuração)</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/AACComponent/*</p> </td> 
   <td><p>Interface do usuário de aplicativos e serviços</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Páginas de administração do Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Páginas de suporte rest</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>Página de configurações do AEM Forms na configuração principal do JEE</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/</p> </td> 
   <td><p>Autenticação do Gerenciamento de usuários</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/um/*</p> </td> 
   <td><p>Interface de administração do Gerenciamento de usuários</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/DocumentManager/*</p> </td> 
   <td><p>Upload e download de documentos que devem ser processados ao acessar endpoints remotos, endpoints WSDL de SOAP e o SDK do Java sobre transporte SOAP ou transporte EJB com documentos HTTP ativados.</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
 </tbody> 
</table>

## Proteção contra ataques de falsificação de solicitação entre sites {#protecting-from-cross-site-request-forgery-attacks}

Um ataque de falsificação de solicitação entre sites (CSRF) explora a confiança que um site tem para o usuário, para transmitir comandos não autorizados e não intencionais pelo usuário. O ataque é configurado incluindo um link ou um script em uma página da Web, ou um URL em uma mensagem de email, para acessar outro site para o qual o usuário já foi autenticado.

Por exemplo, você pode estar conectado ao Console de administração enquanto navega simultaneamente por outro site. Uma das páginas da Web pode incluir uma tag de imagem de HTML com um `src` que direciona um script do lado do servidor no site da vítima. Ao usar o mecanismo de autenticação de sessão baseado em cookies fornecido pelos navegadores da Web, o site de ataque pode enviar solicitações mal-intencionadas para esse script do lado do servidor vítima, disfarçado de usuário legítimo. Para obter mais exemplos, consulte [https://owasp.org/www-community/attacks/csrf#Examples](https://owasp.org/www-community/attacks/csrf#Examples).

As seguintes características são comuns ao CSRF:

* Envolvem sites que dependem da identidade de um usuário.
* Explorar a confiança do site nessa identidade.
* Induzir o navegador do usuário a enviar solicitações HTTP para um site de destino.
* Envolva solicitações HTTP que tenham efeitos colaterais.

O AEM Forms no JEE usa o recurso Filtro referenciador para bloquear ataques CSRF. Os termos a seguir são usados nesta seção para descrever o mecanismo de Filtragem do referenciador:

* **Referenciador permitido:** Referenciador é o endereço da página de origem que envia uma solicitação ao servidor. Para páginas ou formulários JSP, os Referenciadores são geralmente a página anterior no histórico de navegação. Normalmente, o referenciador de imagens são as páginas nas quais as imagens são exibidas. Você pode identificar o Referenciador que tem acesso permitido aos recursos do servidor, adicionando-o à lista Referenciador permitido.
* **Exceções de referenciador permitidas:** Talvez você queira restringir o escopo de acesso de um determinado Referenciador na sua lista de Referenciadores permitidos. Para impor essa restrição, você pode adicionar caminhos individuais desse Referenciador à lista de Exceções permitidas do Referenciador. As solicitações originadas de caminhos na lista Exceções de referenciador permitidas são impedidas de invocar qualquer recurso no Forms Server. Você pode definir Exceções de referenciador permitidas para um aplicativo específico e também usar uma lista global de exceções que se aplicam a todos os aplicativos.
* **URIs permitidos:** Esta é uma lista de recursos que devem ser atendidos sem verificar o Cabeçalho do referenciador. Recursos, por exemplo, páginas de ajuda, que não resultam em alterações de estado no servidor, podem ser adicionados a esta lista. Os recursos na lista de URIs permitidos nunca são bloqueados pelo Filtro referenciador independentemente de quem seja o Referenciador.
* **Referenciador nulo:** Uma solicitação de servidor que não está associada a ou não se origina de uma página da Web pai é considerada uma solicitação de um Referenciador nulo. Por exemplo, ao abrir uma nova janela do navegador, digitar um endereço e pressionar Enter, o Referenciador enviado ao servidor será nulo. Um aplicativo de desktop (.NET ou SWING) que faz uma solicitação HTTP para um servidor Web também envia um Referenciador nulo para o servidor.

### Filtragem de referenciador {#referer-filtering}

O processo de Filtragem de referenciador pode ser descrito da seguinte maneira:

1. O Forms Server verifica o método HTTP usado para invocação:

   1. Se for POST, o Forms Server executará a verificação do cabeçalho do Referenciador.
   1. Se for GET, o Forms Server ignorará a verificação do Referenciador, a menos que *CSRF_CHECK_GETS* está definido como verdadeiro, nesse caso, ele executa a verificação do cabeçalho Referenciador. *CSRF_CHECK_GETS* é especificado na variável *web.xml* arquivo para seu aplicativo.

1. O Forms Server verifica se o URI solicitado existe na inclui na lista de permissões:

   1. Incluir na lista de permissões Se o URI for selecionado, o servidor aceitará a solicitação.
   1. Incluir na lista de permissões Se o URI solicitado não for reconhecido, o servidor recuperará o Referenciador da solicitação.

1. Se houver um Referenciador na solicitação, o servidor verificará se ele é um Referenciador permitido. Se for permitido, o servidor verificará uma Exceção do referenciador:

   1. Se for uma exceção, a solicitação será bloqueada.
   1. Se não for uma exceção, a solicitação será transmitida.

1. Se não houver um Referenciador na solicitação, o servidor verificará se um Referenciador nulo é permitido:

   1. Se um referenciador nulo for permitido, a solicitação será transmitida.
   1. Se um Referenciador nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para o Referenciador nulo e lidará com a solicitação adequadamente.

### Gerenciando a filtragem do referenciador {#managing-referer-filtering}

O AEM Forms no JEE fornece um Filtro referenciador para especificar o Referenciador que tem acesso permitido aos recursos do servidor. Por padrão, o filtro Referenciador não filtra solicitações que usam um método HTTP seguro, por exemplo, GET, a menos que *CSRF_CHECK_GETS* está definido como verdadeiro. Se o número da porta de uma entrada Referenciador permitido for definido como 0, o AEM Forms no JEE permitirá todas as solicitações com Referenciador desse host, independentemente do número da porta. Se nenhum número de porta for especificado, somente as solicitações da porta padrão 80 (HTTP) ou porta 443 (HTTPS) serão permitidas. A Filtragem de referenciador será desativada se todas as entradas na lista Referenciador permitido forem excluídas.

Quando você instala os Serviços de documento pela primeira vez, a lista Referenciador permitido é atualizada com o endereço do servidor no qual os Serviços de documento estão instalados. As entradas do servidor incluem o nome do servidor, o endereço IPv4, o endereço IPv6, se IPv6 estiver habilitado, o endereço de loopback e uma entrada de host local. Os nomes adicionados à lista Referenciador permitido são retornados pelo sistema operacional Host. Por exemplo, um servidor com endereço IP 10.40.54.187 incluirá as seguintes entradas: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Para qualquer nome não qualificado retornado pelo sistema operacional do Host (nomes que não têm endereço IPv4, endereço IPv6 ou nome de domínio qualificado), a inclui na lista de permissões não é atualizada. Modifique a lista Referenciador permitido para se adequar ao seu ambiente empresarial. Não implante o Forms Server no ambiente de produção com a lista de Referenciadores permitidos padrão. Após modificar qualquer um dos Referenciadores Permitidos, Exceções de Referenciador ou URIs, reinicie o servidor para que as alterações entrem em vigor.

**Gerenciar lista de referenciadores permitidos**

Você pode gerenciar a lista Referenciador permitido na Interface de gerenciamento de usuários do Console de administração. A Interface de gerenciamento de usuários fornece a funcionalidade de criar, editar ou excluir a lista. Consulte o * [Prevenção de ataques CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* seção do *ajuda administrativa* para obter mais informações sobre como trabalhar com a lista Referenciador permitido.

**Gerenciar listas de Exceção de referenciador e URI permitidos**

O AEM Forms no JEE fornece APIs para gerenciar a lista Exceção de referenciador permitido e a lista URI permitido. Você pode usar essas APIs para recuperar, criar, editar ou excluir a lista. Veja a seguir uma lista de APIs disponíveis:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Consulte * AEM Forms na Referência da API JEE * para obter mais informações sobre as APIs.

Use o ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** lista para Exceções de Referenciador Permitidas no nível global, ou seja, para definir exceções que sejam aplicáveis a todos os aplicativos. Esta lista contém apenas URIs com um caminho absoluto (por exemplo, `/index.html`) ou um caminho relativo (por exemplo, `/sample/`). Você também pode anexar uma expressão regular ao final de um URI relativo, por exemplo, `/sample/(.)*`.

A variável ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** a ID da lista é definida como uma constante na variável `UMConstants` classe do `com.adobe.idp.um.api` namespace, encontrado em `adobe-usermanager-client.jar`. Você pode usar as APIs do AEM Forms para criar, modificar ou editar essa lista. Por exemplo, para criar a lista Exceções globais permitidas do referenciador, use:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Use o ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** para exceções específicas do aplicativo.

**Desabilitar o filtro referenciador**

Caso o Filtro referenciador bloqueie completamente o acesso ao Servidor do Forms e você não possa editar a lista Referenciador permitido, é possível atualizar o script de inicialização do servidor e desativar a Filtragem do referenciador.

Inclua o `-Dlc.um.csrffilter.disabled=true` Argumento JAVA no script de inicialização e reinicie o servidor. Certifique-se de excluir o argumento JAVA depois de reconfigurar apropriadamente a lista Referenciador permitido.

**Filtragem de referenciador para arquivos WAR personalizados**

Você pode ter criado arquivos WAR personalizados para trabalhar com o AEM Forms no JEE para atender aos requisitos da sua empresa. Para ativar a Filtragem de referenciador para seus arquivos WAR personalizados, inclua ***adobe-usermanager-client.jar*** no caminho de classe para o WAR e inclua uma entrada de filtro no arquivo * web.xml* com os seguintes parâmetros:

**CSRF_CHECK_GETS** controla a verificação do Referenciador nas solicitações do GET. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua esse parâmetro somente se desejar filtrar suas solicitações do GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** é a ID da lista de Exceções do Referenciador Permitido. O Filtro referenciador impede que as solicitações originadas de referenciadores na lista identificada pela ID da lista chamem qualquer recurso no Forms Server.

**CSRF_ALLOWED_URIS_LIST_NAME** é a ID da lista de URIs permitidos. O Filtro referenciador não bloqueia solicitações para qualquer um dos recursos na lista identificados pela ID da lista, independentemente do valor do cabeçalho Referenciador na solicitação.

**CSRF_ALLOW_NULL_REFERER** controla o comportamento do Filtro do referenciador quando o Referenciador é nulo ou não está presente. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua esse parâmetro somente se desejar permitir Referenciadores nulos. Permitir referenciadores nulos pode permitir alguns tipos de ataques de falsificação de solicitação entre sites.

**CSRF_NULL_REFERER_EXCEPTIONS** é uma lista dos URIs para os quais uma verificação do Referenciador não é executada quando o Referenciador é nulo. Esse parâmetro é ativado somente quando *CSRF_ALLOW_NULL_REFERER* está definido como falso. Separe vários URIs na lista com uma vírgula.

Veja a seguir um exemplo da entrada de filtro no *web.xml* arquivo para um ***AMOSTRA*** Arquivo WAR:

```java
<filter> 
       <filter-name> filter-name </filter-name> 
       <filter-class> com.adobe.idp.um.auth.filter.RemoteCSRFFilter </filter-class> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_ALLOW_NULL_REFERER </param-name> 
      <param-value> false </param-value> 
     </init-param> 
     <!-- default is false --> 
     <init-param> 
      <param-name> CSRF_CHECK_GETS </param-name> 
      <param-value> true </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
       <param-name> CSRF_NULL_REFERER_EXCEPTIONS </param-name> 
       <param-value> /SAMPLE/login, /SAMPLE/logout  </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_REFERER_EXCEPTIONS </param-name> 
      <param-value> SAMPLE_ALLOWED_REF_EXP_ID </param-value> 
     </init-param> 
     <!-- Optional --> 
     <init-param> 
      <param-name> CSRF_ALLOWED_URIS_LIST_NAME </param-name> 
      <param-value> SAMPLE_ALLOWED_URI_LIST_ID     </param-value> 
     </init-param> 
</filter> 
    ........ 
    <filter-mapping> 
      <filter-name> filter-name </filter-name> 
      <url-pattern>/*</url-pattern> 
    </filter-mapping>
```

**Resolução de Problemas**

Se solicitações legítimas do servidor estiverem sendo bloqueadas pelo filtro CSRF, tente um dos seguintes procedimentos:

* Se a solicitação rejeitada tiver um cabeçalho Referenciador, considere adicioná-lo cuidadosamente à lista Referenciador permitido. Adicionar somente Referenciador confiável.
* Se a solicitação rejeitada não tiver um cabeçalho Referenciador, modifique o aplicativo cliente para incluir um cabeçalho Referenciador.
* Se o cliente puder trabalhar em um navegador, experimente esse modelo de implantação.
* Como último recurso, é possível adicionar o recurso à lista de URIs permitidos. Essa não é uma configuração recomendada.

## Configuração de rede segura {#secure-network-configuration}

Esta seção descreve os protocolos e portas exigidos pelo AEM Forms no JEE e fornece recomendações para implantar o AEM Forms no JEE em uma configuração de rede segura.

### Protocolos de rede usados pelo AEM Forms no JEE {#network-protocols-used-by-aem-forms-on-jee}

Ao configurar uma arquitetura de rede segura conforme descrito na seção anterior, os seguintes protocolos de rede são necessários para a interação entre o AEM Forms no JEE e outros sistemas na rede corporativa.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocolo</p> </th> 
   <th><p>Utilização</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>HTTP</p> </td> 
   <td> 
    <ul> 
     <li><p>O navegador exibe o Configuration Manager e os aplicativos Web do usuário final</p> </li> 
     <li><p>Todas as conexões SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Aplicativos cliente de serviços Web, como aplicativos .NET</p> </li> 
     <li><p>A Adobe Reader® usa SOAP para os serviços Web do AEM Forms no servidor JEE</p> </li> 
     <li><p>aplicativos Adobe Flash® usam SOAP para serviços Web do Forms Server</p> </li> 
     <li><p>Chamadas de SDK do AEM Forms no JEE quando usadas no modo SOAP</p> </li> 
     <li><p>Ambiente de design do Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>Chamadas de AEM Forms no SDK JEE quando usadas no modo Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP/POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrada baseada em email para um serviço (endpoint de email)</p> </li> 
     <li><p>Notificações de tarefa do usuário por email</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>E/S de Arquivo UNC</p> </td> 
   <td><p>Monitoramento do AEM Forms no JEE de pastas monitoradas para entrada em um serviço (endpoint de pasta monitorada)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizações de informações de usuários e grupos organizacionais em um diretório</p> </li> 
     <li><p>Autenticação LDAP para usuários interativos</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Chamadas de consulta e procedimento feitas a um banco de dados externo durante a execução de um processo usando o serviço JDBC</p> </li> 
     <li><p>AEM Forms de acesso interno no repositório JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permite a navegação remota do AEM Forms no repositório de tempo de design do JEE (formulários, fragmentos e assim por diante) por qualquer cliente WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>aplicativos de Flash Adobe, em que os serviços do servidor AEM Forms em JEE são configurados com um terminal Remoting</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>O AEM Forms no JEE expõe MBeans para monitoramento usando JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Portas para servidores de aplicativos {#ports-for-application-servers}

Esta seção descreve as portas default (e intervalos de configuração alternativos) para cada tipo de servidor de aplicativos suportado. Essas portas devem ser ativadas ou desativadas no firewall interno, dependendo da funcionalidade de rede que você deseja permitir para os clientes que se conectam ao servidor de aplicativos que executa o AEM Forms no JEE.

>[!NOTE]
>
>Por padrão, o servidor expõe vários MBeans JMX no namespace adobe.com. Somente as informações úteis para o monitoramento da integridade do servidor são expostas. No entanto, para evitar a divulgação de informações, você deve impedir que chamadores em uma rede não confiável procurem MBeans JMX e acessem métricas de integridade.

**Portas JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Propósito</p> </th> 
   <th><p>Porta</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acesso a aplicações web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>HTTP/1.1 Porta do conector 8080</p> <p>Porta do conector 8009 do AJP 1.3</p> <p>Porta do conector SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Suporte para CORBA</p> </td> 
   <td><p>[JBoss root]/server/all/conf/jacorb.properties</p> <p>Porta OAP 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Portas do WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Propósito</p> </th> 
   <th><p>Porta</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acesso a aplicações web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do Admin Server: o padrão é 7001</p> </li> 
     <li><p>Porta de escuta SSL do Admin Server: o padrão é 7002</p> </li> 
     <li><p>Porta configurada para o servidor gerenciado, por exemplo, 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Portas de administração do WebLogic não necessárias para acessar o AEM Forms no JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do Servidor gerenciado: configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta SSL do Servidor Gerenciado: Configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta do Gerenciador de nós: o padrão é 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Portas do WebSphere**

Para obter informações sobre as portas do WebSphere exigidas pelo AEM Forms no JEE, vá para a configuração Número da porta na interface do usuário do WebSphere Application Server.

### Configuração do SSL {#configuring-ssl}

Consultando a arquitetura física descrita na seção [Arquitetura física do AEM Forms no JEE](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), você deve configurar o SSL para todas as conexões que planeja usar. Especificamente, todas as conexões do SOAP devem ser conduzidas por SSL para evitar a exposição das credenciais do usuário em uma rede.

Para obter instruções sobre como configurar SSL em JBoss, WebLogic e WebSphere, consulte &quot;Configuring SSL&quot; no [ajuda administrativa](https://www.adobe.com/go/learn_aemforms_admin_64).

Para obter instruções sobre como importar certificados para a JVM (Java Virtual Machine) configurada para um servidor AEM Forms, consulte a seção Autenticação mútua em [Ajuda do AEM Forms Workbench](https://www.adobe.com/go/learn_aemforms_workbench_65).

### Configuração do redirecionamento de SSL {#configuring-ssl-redirect}

Após configurar seu servidor de aplicativos para suportar SSL, você deve garantir que todo o tráfego HTTP para aplicativos e serviços seja forçado a usar a porta SSL.

Para configurar o redirecionamento SSL para WebSphere ou WebLogic, consulte a documentação do servidor de aplicativos.

1. Abra o prompt de comando, navegue até o diretório /JBOSS_HOME/standalone/configuration e execute o seguinte comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Abra o arquivo JBOSS_HOME/standalone/configuration/standalone.xml para edição.

   Depois que a variável &lt;subsystem xmlns=&quot;urn&lt;span id=&quot; translate=&quot;no&quot; />domínio:web:Elemento 1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;> , adicione os seguintes detalhes::jboss:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Adicione o seguinte código no elemento de conector https:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salve e feche o arquivo standalone.xml.

## Recomendações de segurança específicas para Windows {#windows-specific-security-recommendations}

Esta seção contém recomendações de segurança específicas para o Windows quando usadas para executar o AEM Forms no JEE.

### Contas do serviço JBoss {#jboss-service-accounts}

A instalação completa do AEM Forms no JEE configura uma conta de serviço, por padrão, usando a conta Sistema local. A conta de usuário do Sistema local interna tem um alto nível de acessibilidade; ela faz parte do grupo Administradores. Se uma identidade de processo de trabalho for executada como a conta de usuário do Sistema Local, esse processo de trabalho terá acesso total a todo o sistema.

#### Executar o servidor de aplicativos usando uma conta não administrativa {#run-the-application-server-using-a-non-administrative-account}

1. No Microsoft Management Console (MMC), crie um usuário local para o serviço Forms Server para fazer logon como:

   * Selecionar **Usuário não pode alterar senha**.
   * No **Membro de** verifique se o grupo Usuários está listado.

1. Selecionar **Configurações** > **Ferramentas administrativas** > **Serviços**.
1. Clique duas vezes no serviço do servidor de aplicativos e pare o serviço.
1. No **Fazer Logon** selecione **Esta conta**, procure a conta de usuário que você criou e digite a senha da conta.
1. Na janela Configurações de segurança locais, em Atribuição de direitos de usuário, conceda os seguintes direitos à conta de usuário na qual o Forms Server está sendo executado:

   * Negar logon pelos Serviços de Terminal
   * Negar logon no locallyxx
   * Fazer logon como serviço (já deve estar definido)

1. Conceda à nova conta de usuário permissões de modificação nos seguintes diretórios:
   * **Diretório de Armazenamento Global de Documentos (GDS)**: o local do diretório GDS é configurado manualmente durante o processo de instalação do AEM Forms. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório do repositório CRX**: o local padrão é `[AEM-Forms-installation-location]\crx-repository`
   * **Diretórios temporários do AEM Forms**:
      * Caminho TMP ou TEMP (Windows) conforme definido nas variáveis de ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectado Em sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como o diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Conceda à nova conta de usuário permissões de gravação nos seguintes diretórios:
   * [JBoss-diretory]\independente\implantação
   * [JBoss-diretory]\autônomo\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   >O local de instalação padrão do JBoss Application Server:
   >
   >* Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   >* Linux: /opt/jboss/.

1. Inicie o serviço do servidor de aplicativos.

### Segurança do sistema de arquivos {#file-system-security}

O AEM Forms no JEE usa o sistema de arquivos das seguintes maneiras:

* Armazena arquivos temporários que são usados durante o processamento de entrada e saída de documentos
* Armazena arquivos no repositório de arquivamento global que são usados para dar suporte aos componentes da solução que estão instalados
* As pastas monitoradas armazenam arquivos soltos que são usados como entrada para um serviço a partir de um local de pasta do sistema de arquivos

Ao usar pastas monitoradas como uma maneira de enviar e receber documentos com um serviço do Forms Server, tome precauções adicionais com a segurança do sistema de arquivos. Quando um usuário solta o conteúdo na pasta monitorada, esse conteúdo é exposto por meio da pasta monitorada. Nesse caso, o serviço não autentica o usuário final real. Em vez disso, ele depende da segurança de nível de ACL e Compartilhamento para ser definida no nível da pasta a fim de determinar quem pode efetivamente chamar o serviço.

## Recomendações de segurança específicas para JBoss {#jboss-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos que são específicas para JBoss 7.0.6 quando usado para executar o AEM Forms no JEE.

### Desativar o console de gerenciamento JBoss e o console JMX {#disable-jboss-management-console-and-jmx-console}

O acesso à Console de gerenciamento JBoss e à Console JMX já está configurado (a monitoração JMX está desativada) quando você instala o AEM Forms no JEE em JBoss usando o método de instalação turnkey. Se você estiver usando seu próprio JBoss Application Server, certifique-se de que o acesso ao JBoss Management Console e ao console de monitoramento JMX esteja protegido. O acesso ao console de monitoramento JMX é definido no arquivo de configuração JBoss chamado jmx-invoker-service.xml.

### Desativar a navegação no diretório {#disable-directory-browsing}

Depois de fazer logon no Console de administração, é possível navegar pela lista de diretórios da console modificando o URL. Por exemplo, se você alterar o URL para um dos seguintes URLs, uma lista de diretórios poderá ser exibida:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recomendações de segurança específicas do WebLogic {#weblogic-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebLogic 9.1 ao executar o AEM Forms no JEE.

### Desativar a navegação no diretório {#disable_directory_browsing-1}

Defina as propriedades index-directories no arquivo weblogic.xml para `false`, conforme mostrado neste exemplo:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Habilitar Porta SSL do WebLogic {#enable-weblogic-ssl-port}

Por padrão, o WebLogic não ativa a Porta de escuta SSL padrão, 7002. Habilite essa porta no Console de Administração do WebLogic Server antes de configurar o SSL.

## Recomendações de segurança específicas do WebSphere {#websphere-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebSphere que executa o AEM Forms no JEE.

### Desativar a navegação no diretório {#disable_directory_browsing-2}

Defina o `directoryBrowsingEnabled` no arquivo ibm-web-ext.xml para `false`.

### Habilitar a segurança administrativa do WebSphere {#enable-websphere-administrative-security}

1. Faça logon no Console administrativo do WebSphere.
1. Na árvore de navegação, acesse **Segurança** > **Segurança global**
1. Selecionar **Habilitar segurança administrativa**.
1. Desmarcar ambos **Habilitar segurança de aplicativos** e **Usar segurança do Java 2**.
1. Clique em **OK** ou **Aplicar**.
1. No **Mensagens** clique em **Salvar diretamente na configuração principal**.
