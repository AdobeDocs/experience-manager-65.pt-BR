---
title: Otimizar sua AEM Forms no ambiente JEE
seo-title: Otimizar sua AEM Forms no ambiente JEE
description: Saiba mais sobre uma variedade de configurações de proteção de segurança para melhorar a segurança do AEM Forms no JEE em execução em uma intranet corporativa.
seo-description: Saiba mais sobre uma variedade de configurações de proteção de segurança para melhorar a segurança do AEM Forms no JEE em execução em uma intranet corporativa.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
role: Admin
exl-id: 6fb260f9-d0f8-431e-8d4e-535b451e4124
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '7696'
ht-degree: 1%

---

# Otimizar sua AEM Forms no ambiente JEE {#hardening-your-aem-forms-on-jee-environment}

Saiba mais sobre uma variedade de configurações de proteção de segurança para melhorar a segurança do AEM Forms no JEE em execução em uma intranet corporativa.

O artigo descreve recomendações e práticas recomendadas para proteger servidores que executam o AEM Forms no JEE. Este não é um documento abrangente de proteção de host para seu sistema operacional e servidores de aplicativos. Em vez disso, este artigo descreve uma variedade de configurações de proteção de segurança que você deve implementar para melhorar a segurança do AEM Forms no JEE que está sendo executado em uma intranet corporativa. No entanto, para garantir que o AEM Forms nos servidores de aplicativos JEE permaneça seguro, você também deve implementar procedimentos de monitoramento, detecção e resposta de segurança.

O artigo descreve técnicas de endurecimento que devem ser aplicadas durante os seguintes estágios durante o ciclo de vida da instalação e configuração:

* **Pré-instalação:** use essas técnicas antes de instalar o AEM Forms no JEE.
* **Instalação:** use essas técnicas durante o processo de instalação do AEM Forms no JEE.
* **Pós-instalação:** Utilize estas técnicas após a instalação e periodicamente a partir daí.

O AEM Forms no JEE é altamente personalizável e pode funcionar em vários ambientes diferentes. Algumas das recomendações podem não atender às necessidades de sua organização.

## Pré-instalação {#preinstallation}

Antes de instalar o AEM Forms no JEE , você pode aplicar soluções de segurança à camada de rede e ao sistema operacional. Esta seção descreve alguns problemas e faz recomendações para reduzir vulnerabilidades de segurança nessas áreas.

**Instalação e configuração em UNIX e Linux**

Você não deve instalar ou configurar o AEM Forms no JEE usando um shell raiz. Por padrão, os arquivos são instalados no diretório /opt e o usuário que executa a instalação precisa de todas as permissões do arquivo em /opt. Como alternativa, uma instalação pode ser executada no diretório /usuário de um usuário individual, onde já tem todas as permissões de arquivo.

**Instalação e configuração no Windows**

Você deve executar a instalação no Windows como um administrador se estiver instalando o AEM Forms no JEE no JBoss usando o método turnkey ou se estiver instalando o Gerador de PDF. Além disso, ao instalar o PDF Generator no Windows com suporte a aplicativos nativos, você deve executar a instalação como o mesmo usuário do Windows que instalou o Microsoft Office. Para obter mais informações sobre privilégios de instalação, consulte o documento* Instalando e implantando o AEM Forms no JEE* para seu servidor de aplicativos.

### Segurança da camada de rede {#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de proteção de hosts na rede contra essas vulnerabilidades. Ele trata da segmentação de rede, da proteção de pilha do protocolo TCP/IP (Transmission Control Protocol/Internet Protocol) e do uso de firewalls para proteção de host.

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
   <td><p>Implante servidores de formulários em uma zona desmilitarizada (DMZ). A segmentação deve existir em pelo menos dois níveis com o servidor de aplicativos usado para executar o AEM Forms no JEE, colocado atrás do firewall interno. Separe a rede externa da DMZ que contém os servidores da Web, que, por sua vez, devem ser separados da rede interna. Use firewalls para implementar as camadas de separação. Categorize e controle o tráfego que passa por cada camada de rede para garantir que somente o mínimo absoluto de dados necessários seja permitido.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Endereços IP privados</p> </td> 
   <td><p>Use a NAT (Network Address Translation, tradução de endereço de rede) com endereços IP privados RFC 1918 no servidor de aplicativos AEM Forms. Atribua endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear tráfego de e para um host interno de NAT por meio da Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewalls</p> </td> 
   <td><p>Use os seguintes critérios para selecionar uma solução de firewall:</p> 
    <ul> 
     <li><p>Implemente firewalls que sejam compatíveis com servidores proxy e/ou <em>inspeção de estado</em> em vez de soluções de filtragem de pacotes simples.</p> </li> 
     <li><p>Use um firewall que ofereça suporte a <em>negar todos os serviços, exceto aqueles explicitamente permitidos</em> paradigmas de segurança.</p> </li> 
     <li><p>Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o maior nível de segurança e ajuda a impedir que usuários não autorizados ignorem a segurança do firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Portas de banco de dados</p> </td> 
   <td><p>Não use portas de escuta padrão para bancos de dados (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Para obter informações sobre como alterar portas do banco de dados, consulte a documentação do banco de dados.</p> <p>O uso de uma porta de banco de dados diferente afeta o AEM Forms geral na configuração JEE. Se você alterar as portas padrão, deverá fazer as modificações correspondentes em outras áreas da configuração, como as fontes de dados do AEM Forms no JEE.</p> <p>Para obter informações sobre como configurar fontes de dados no AEM Forms no JEE, consulte Instalar e atualizar o AEM Forms no JEE ou Atualizar para o AEM Forms no JEE para seu servidor de aplicativos em <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">Guia do usuário do AEM Forms</a>.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do sistema operacional {#operating-system-security}

A tabela a seguir descreve algumas possíveis abordagens para minimizar as vulnerabilidades de segurança encontradas no sistema operacional.

<table> 
 <thead> 
  <tr> 
   <th><p>Problema</p></th> 
   <th><p>Descrição</p></th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Correções de segurança</p></td> 
   <td><p>Há um risco maior de um usuário não autorizado ter acesso ao servidor de aplicativos se os patches e upgrades de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção.</p><p>Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software de proteção antivírus</p></td> 
   <td><p>Os scanners de vírus podem identificar arquivos infectados digitalizando uma assinatura ou observando um comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como os novos vírus são detectados com frequência, você deve atualizar esse arquivo com frequência para que o antivírus identifique todos os vírus atuais.</p></td> 
  </tr> 
  <tr> 
   <td><p>Protocolo de Hora da Rede (NTP)</p></td> 
   <td><p>Para análise forense, mantenha o tempo preciso nos servidores de formulários. Use o NTP para sincronizar o tempo em todos os sistemas conectados diretamente à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Para obter informações de segurança adicionais para seu sistema operacional, consulte [&quot;Informações de segurança do sistema operacional&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Instalação {#installation}

Esta seção descreve técnicas que podem ser usadas durante o processo de instalação do AEM Forms para reduzir vulnerabilidades de segurança. Em alguns casos, essas técnicas usam opções que fazem parte do processo de instalação. A tabela a seguir descreve essas técnicas.

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
   <td><p>Use o menor número de privilégios necessários para instalar o software. Faça logon no computador usando uma conta que não esteja no grupo Administradores. No Windows, você pode usar o comando Executar como para executar o instalador do AEM Forms no JEE como um usuário administrativo. Em sistemas UNIX e Linux, use um comando como <code>sudo</code> para instalar o software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fonte de software</p> </td> 
   <td><p>Não baixe nem execute o AEM Forms no JEE a partir de fontes não confiáveis.</p> <p>Programas mal-intencionados podem conter código para violar a segurança de várias maneiras, incluindo roubo de dados, modificação e exclusão de dados e negação de serviço. Instale o AEM Forms no JEE a partir do Adobe DVD ou apenas de uma fonte confiável.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partições de disco</p> </td> 
   <td><p>Coloque o AEM Forms no JEE em uma partição de disco dedicada. A segmentação de disco é um processo que mantém dados específicos em seu servidor em discos físicos separados para aumentar a segurança. Organizar os dados dessa forma reduz o risco de ataques de travessia do diretório. Planeje criar uma partição separada da partição do sistema na qual você pode instalar o AEM Forms no diretório de conteúdo JEE. (No Windows, a partição do sistema contém o diretório system32 ou a partição de inicialização.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componentes</p> </td> 
   <td><p>Avalie os serviços existentes e desative ou desinstale qualquer um que não seja necessário. Não instale componentes e serviços desnecessários.</p> <p>A instalação padrão de um servidor de aplicativos pode incluir serviços que não são necessários para sua utilização. Você deve desativar todos os serviços desnecessários antes da implantação para minimizar os pontos de entrada de um ataque. Por exemplo, no JBoss, você pode comentar serviços desnecessários no arquivo META-INF/jboss-service.xml descriptor .</p> </td> 
  </tr> 
  <tr> 
   <td><p>Arquivo de política entre domínios</p> </td> 
   <td><p>A presença de um arquivo <code>crossdomain.xml</code> no servidor pode enfraquecer imediatamente esse servidor. É recomendável tornar a lista de domínios o mais restritiva possível. Não coloque o arquivo <code>crossdomain.xml</code> que foi usado durante o desenvolvimento em produção ao usar os Guias <em>(obsoleto)</em>. Para um guia que usa serviços da Web, se o serviço estiver no mesmo servidor que serviu o guia, um arquivo <code>crossdomain.xml</code> não será necessário. Mas se o serviço estiver em outro servidor ou se os clusters estiverem envolvidos, a presença de um arquivo <code>crossdomain.xml</code> seria necessária. Consulte <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a> para obter mais informações sobre o arquivo cross-domain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de segurança do sistema operacional</p> </td> 
   <td><p>Se precisar usar a criptografia XML de 192 bits ou 256 bits em plataformas Solaris, certifique-se de instalar <code>pkcs11_softtoken_extra.so</code> em vez de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Etapas pós-instalação {#post-installation-steps}

Depois de instalar o AEM Forms com êxito no JEE, é importante manter periodicamente o ambiente de uma perspectiva de segurança.

A seção a seguir descreve detalhadamente as diferentes tarefas recomendadas para proteger o servidor de formulários implantado.

### Segurança AEM Forms {#aem-forms-security}

As configurações recomendadas a seguir se aplicam ao AEM Forms no servidor JEE fora do aplicativo Web administrativo. Para reduzir os riscos de segurança para o servidor, aplique essas configurações imediatamente após instalar o AEM Forms no JEE.

**Correções de segurança**

Há um risco maior de um usuário não autorizado ter acesso ao servidor de aplicativos se os patches e upgrades de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção para garantir a compatibilidade e disponibilidade dos aplicativos. Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. As atualizações do AEM Forms no JEE estão no site de download de produtos Enterprise.

**Contas de serviço (chave turnkey do JBoss somente no Windows)**

O AEM Forms no JEE instala um serviço, por padrão, usando a conta LocalSystem . A conta de usuário LocalSystem integrada tem um alto nível de acessibilidade; faz parte do grupo Administradores . Se uma identidade de processo de trabalho for executada como a conta de usuário LocalSystem, esse processo de trabalho terá acesso total a todo o sistema.

Para executar o servidor de aplicativos no qual o AEM Forms no JEE é implantado, usando uma conta específica não administrativa, siga estas instruções:

1. No Console de Gerenciamento da Microsoft (MMC), crie um usuário local para que o serviço do servidor de formulários faça logon como:

   * Selecione **O usuário não pode alterar a senha**.
   * Na guia **Member Of** , verifique se o grupo **Users** está listado.

   >[!NOTE]
   >
   >Não é possível alterar essa configuração para o Gerador de PDF.

1. Selecione **Iniciar** > **Definições** > **Ferramentas Administrativas** > **Serviços**.
1. Clique duas vezes no JBoss para AEM Forms no JEE e pare o serviço.
1. Na guia **Fazer logon**, selecione **Esta conta**, procure a conta de usuário criada e insira a senha da conta.
1. No MMC, abra **Configurações de segurança local** e selecione **Políticas locais** > **Atribuição de direitos de usuário**.
1. Atribua os seguintes direitos à conta de usuário na qual o servidor de formulários está sendo executado:

   * Negar logon por meio dos Serviços de Terminal
   * Negar logon localmente
   * Fazer logon como Serviço (já deve estar definido)

1. Forneça permissões de modificação à nova conta de usuário nos seguintes diretórios:
   * **Diretório** Global Document Storage (GDS): A localização do diretório GDS é configurada manualmente durante o processo de instalação do AEM Forms. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório** CRX-Repository: O local padrão é  `[AEM-Forms-installation-location]\crx-repository`
   * **Diretórios** temporários do AEM Forms:
      * (Windows) Caminho TMP ou TEMP conforme definido nas variáveis de ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectado
Em sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Forneça permissões de gravação à nova conta de usuário nos seguintes diretórios:
   * [JBoss-diretory]\standalone\deployment
   * [JBoss-diretory]\standalone\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   > O local de instalação padrão do JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/

1. Inicie o servidor de aplicativos.

**Desativar o servlet de inicialização do Configuration Manager**

O Configuration Manager utilizou um servlet implantado no servidor de aplicativos para executar o bootstrapping do AEM Forms no banco de dados JEE. Como o Configuration Manager acessa este servlet antes da conclusão da configuração, o acesso a ele não foi protegido para usuários autorizados e deve ser desativado depois que você tiver usado com êxito o Configuration Manager para configurar o AEM Forms no JEE.

1. Descompacte o arquivo adobe-livecycle-[appserver].ear.
1. Abra o arquivo META-INF/application.xml .
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
1. Comente o adobe-bootstrapper.war e o diretório adobe-lcm-bootstrapper-rediretory. Módulos de guerra como se segue:

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

1. Salve e feche o arquivo META-INF/application.xml.
1. Comprima o arquivo EAR e reimplante-o no servidor de aplicativos.
1. Inicie o servidor do AEM Forms.
1. Digite o URL abaixo em um navegador para testar a alteração e garantir que ela não funcione mais.

   https://&lt;localhost>:&lt;port>/adobe-bootstrapper/bootstrap

**Bloquear o acesso remoto ao Armazenamento de Confiança**

O Configuration Manager permite fazer upload de uma credencial de extensões do Acrobat Reader DC para a AEM Forms no armazenamento confiável JEE. Isso significa que o acesso ao Serviço de Credenciais da Loja de Confiança por protocolos remotos (SOAP e EJB) foi ativado por padrão. Esse acesso não é mais necessário depois de ter carregado a credencial de direitos usando o Configuration Manager ou se decidir usar o Console de administração posteriormente para gerenciar as credenciais.

Você pode desabilitar o acesso remoto a todos os serviços do Armazenamento de Confiança seguindo as etapas da seção [Desabilitando o acesso remoto não essencial a serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Desativar todo o acesso anônimo não essencial**

Alguns serviços de servidor de formulários têm operações que podem ser chamadas por um chamador anônimo. Se o acesso anônimo a esses serviços não for necessário, desative-o seguindo as etapas em [Desabilitando o acesso anônimo não essencial a serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Alterar a senha padrão do administrador {#change-the-default-administrator-password}

Quando o AEM Forms no JEE é instalado, uma única conta de usuário padrão é configurada para Superadministrador/ login-id Administrador do usuário com uma senha padrão de *senha*. Você deve alterar essa senha imediatamente usando o Gerenciador de configuração.

1. Digite o seguinte URL em um navegador da Web:

   ```java
   https://[host name]:[port]/adminui
   ```

   O número padrão da porta é um destes:

   **JBoss:** 8080

   **WebLogic Server:** 7001

   **WebSphere:** 9080.

1. No campo **Nome de Usuário**, digite `administrator` e, no campo **Senha**, digite `password`.
1. Clique em **Configurações** > **Gerenciamento de usuários** > **Usuários e grupos**.
1. Digite `administrator` no campo **Localizar** e clique em **Localizar**.
1. Clique em **Super Administrator** na lista de usuários.
1. Clique em **Alterar senha** na página Editar usuário.
1. Especifique a nova senha e clique em **Salvar**.

Além disso, é recomendável alterar a senha padrão do Administrador do CRX executando as seguintes etapas:

1. Faça logon em `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` usando o nome de usuário/senha padrão.
1. Digite Administrador no campo de pesquisa e clique em **Ir**.
1. Selecione **Administrador** no resultado da pesquisa e clique no ícone **Editar** na parte inferior direita da interface do usuário.
1. Especifique a nova senha no campo **Nova Senha** e a senha antiga no campo **Sua Senha**.
1. Clique no ícone Save na parte inferior direita da interface do usuário.

#### Desativar geração de WSDL {#disable-wsdl-generation}

A geração WSDL (Linguagem de definição de serviço da Web) deve ser ativada somente para ambientes de desenvolvimento, onde a geração de WSDL é usada pelos desenvolvedores para criar seus aplicativos clientes. Você pode optar por desativar a geração de WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

1. Digite o seguinte URL em um navegador da Web:

   ```java
   https://[host name]:[port]/adminui
   ```

1. Clique em **Configurações > Configurações principais do sistema > Configurações**.
1. Desmarque **Ativar WSDL** e clique em **OK**.

### Segurança do servidor de aplicativos {#application-server-security}

A tabela a seguir descreve algumas técnicas para proteger seu servidor de aplicativos depois que o aplicativo AEM Forms no JEE é instalado.

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
   <td><p>Depois de instalar, configurar e implantar o AEM Forms no JEE no servidor de aplicativos, você deve desativar o acesso aos consoles administrativos do servidor de aplicativos. Consulte a documentação do servidor de aplicativos para obter detalhes.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de cookie do servidor de aplicativos</p> </td> 
   <td><p>Os cookies do aplicativo são controlados pelo servidor de aplicativos. Ao implantar o aplicativo, o administrador do servidor de aplicativos pode especificar as preferências de cookie em todo o servidor ou em uma base específica do aplicativo. Por padrão, as configurações do servidor têm preferência.</p> <p>Todos os cookies de sessão gerados pelo servidor de aplicativos devem incluir o atributo <code>HttpOnly</code> . Por exemplo, ao usar o Servidor de Aplicativos JBoss, você pode modificar o elemento SessionCookie para <code>httpOnly="true"</code> no arquivo <code>WEB-INF/web.xml</code>.</p> <p>Você pode restringir o envio de cookies somente por HTTPS. Como resultado, eles não são enviados criptografados por HTTP. Os administradores do servidor de aplicativos devem ativar cookies seguros para o servidor de forma global. Por exemplo, ao usar o JBoss Application Server, você pode modificar o elemento do conector para <code>secure=true</code> no arquivo <code>server.xml</code>.</p> <p>Consulte a documentação do servidor de aplicativos para obter mais detalhes sobre as configurações de cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Navegação no diretório</p> </td> 
   <td><p>Quando alguém solicita uma página que não existe ou solicita o nome de um diretor (a cadeia de caracteres de solicitação termina com uma barra (/)), o servidor de aplicativos não deve retornar o conteúdo desse diretório. Para evitar isso, você pode desativar a navegação no diretório no servidor de aplicativos. Você deve fazer isso no aplicativo do console de administração e em outros aplicativos em execução no servidor.</p> <p>Para JBoss, defina o valor do parâmetro de inicialização de listagens da propriedade <code>DefaultServlet</code> para <code>false</code> no arquivo web.xml, como mostrado neste exemplo:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;servlet-class&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listagens&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Para o WebSphere, defina a propriedade <code>directoryBrowsingEnabled</code> no arquivo ibm-web-ext.xmi para <code>false</code>.</p> <p>Para WebLogic, defina as propriedades de index-diretórios no arquivo weblogic.xml para <code>false</code>, conforme mostrado neste exemplo:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-directory-enabled&gt;false</p> <p>&lt;/index-directory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do banco de dados {#database-security}

Ao proteger seu banco de dados, você deve implementar as medidas descritas pelo fornecedor do banco de dados. Você deve alocar um usuário do banco de dados com as permissões mínimas necessárias do banco de dados concedidas para uso pelo AEM Forms no JEE. Por exemplo, não use uma conta com privilégios de administrador de banco de dados.

No Oracle, a conta de banco de dados usada precisa apenas dos privilégios CONNECT, RECURSO e CRIAR EXIBIÇÃO. Para obter requisitos semelhantes em outros bancos de dados, consulte [Preparando para instalar o AEM Forms no JEE (Servidor único)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configuração da segurança integrada para SQL Server no Windows para JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifique [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} para adicionar `integratedSecurity=true` ao URL de conexão, conforme mostrado neste exemplo:

   ```java
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Adicione o arquivo sqljdbc_auth.dll ao caminho de sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado com a instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Modifique a propriedade JBoss Windows service (JBoss para AEM Forms no JEE) para Logon como do sistema local para uma conta de logon que tenha o banco de dados AEM Forms e um conjunto mínimo de privilégios. Se você estiver executando o JBoss a partir da linha de comando em vez de um serviço do Windows, não será necessário executar essa etapa.
1. Defina Segurança para o SQL Server a partir do modo **Misto** para **Autenticação do Windows apenas**.

#### Configurando a segurança integrada para SQL Server no Windows for WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Inicie o Console de Administração do WebLogic Server digitando o seguinte URL na linha de URL de um navegador da Web:

   ```java
   https://[host name]:7001/console
   ```

1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura de domínio, clique em *[domínio_base]* > **Serviços** > **JDBC** > **Origens de Dados** e, no painel direito, clique em **IDP_DS**.
1. Na próxima tela, na guia **Configuration**, clique na guia **Connection Pool** e, na caixa **Properties**, digite `integratedSecurity=true`.
1. Em Estrutura de domínio, clique em **[domínio_base]** > **Serviços** > **JDBC** > **Origens de Dados** e, no painel direito, clique em **RM_DS**.
1. Na próxima tela, na guia **Configuration**, clique na guia **Connection Pool** e, na caixa **Properties**, digite `integratedSecurity=true`.
1. Adicione o arquivo sqljdbc_auth.dll ao caminho de sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado com a instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Defina Segurança para o SQL Server a partir do modo **Misto** para **Autenticação do Windows apenas**.

#### Configurando a segurança integrada para SQL Server no Windows para WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

No WebSphere, você pode configurar a segurança integrada somente quando usar um driver JDBC externo do SQL Server, não o driver JDBC do SQL Server incorporado no WebSphere.

1. Faça logon no Console Administrativo do WebSphere.
1. Na árvore de navegação, clique em **Resources** > **JDBC** > **Data Sources** e, no painel direito, clique em **IDP_DS**.
1. No painel direito, em Propriedades adicionais, clique em **Propriedades personalizadas** e em **Novo**.
1. Na caixa **Nome**, digite `integratedSecurity` e, na caixa **Valor**, digite `true`.
1. Na árvore de navegação, clique em **Resources** > **JDBC** > **Data Sources** e, no painel direito, clique em **RM_DS**.
1. No painel direito, em Propriedades adicionais, clique em **Propriedades personalizadas** e em **Novo**.
1. Na caixa **Nome**, digite `integratedSecurity` e, na caixa **Valor**, digite `true`.
1. No computador em que o WebSphere está instalado, adicione o arquivo sqljdbc_auth.dll ao caminho dos sistemas Windows (C:\Windows). O arquivo sqljdbc_auth.dll está no mesmo local que a instalação do driver JDBC 1.2 do Microsoft SQL (o padrão é *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Selecione **Iniciar** > **Painel de Controle** > **Serviços**, clique com o botão direito do mouse no serviço Windows para WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) e selecione **Propriedades**.
1. Na caixa de diálogo Propriedades, clique na guia **Logon**.
1. Selecione **Esta Conta** e forneça as informações necessárias para definir a conta de logon que deseja usar.
1. Defina a Segurança no SQL Server do modo **Misto** para **Apenas Autenticação do Windows**.

### Proteção do acesso a conteúdo confidencial no banco de dados {#protecting-access-to-sensitive-content-in-the-database}

O schema do banco de dados do AEM Forms contém informações confidenciais sobre a configuração do sistema e os processos de negócios e deve estar oculto atrás do firewall. O banco de dados deve ser considerado dentro do mesmo limite de confiança que o servidor de formulários. Para proteger contra divulgação de informações e roubo de dados de negócios, o banco de dados deve ser configurado pelo administrador do banco de dados (DBA) para permitir acesso somente por administradores autorizados.

Como precaução adicional, você deve considerar o uso de ferramentas específicas do fornecedor do banco de dados para criptografar colunas em tabelas que contenham os seguintes dados:

* Chaves de documento Rights Management
* Chave de criptografia de PIN do HSM do Armazenamento de Confiança
* Hash de senha de usuário local

Para obter informações sobre ferramentas específicas do fornecedor, consulte [&quot;Informações de segurança do banco de dados&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Segurança LDAP {#ldap-security}

Um diretório LDAP (Lightweight Diretory Access Protocol) normalmente é usado pelo AEM Forms no JEE como fonte para informações de usuários e grupos da empresa e um meio de executar autenticação de senha. Você deve garantir que seu diretório LDAP esteja configurado para usar SSL (Secure Socket Layer) e que o AEM Forms no JEE esteja configurado para acessar seu diretório LDAP usando sua porta SSL.

#### Negação de serviço LDAP {#ldap-denial-of-service}

Um ataque comum usando o LDAP envolve um invasor deliberadamente falhando na autenticação várias vezes. Isso força o Servidor de Diretório LDAP a bloquear um usuário de todos os serviços dependentes de LDAP.

Você pode definir o número de tentativas de falha e o tempo de bloqueio subsequente que o AEM Forms implementa quando um usuário falha repetidamente na autenticação no AEM Forms. No Console de administração, escolha valores baixos. Ao selecionar o número de tentativas de falha, é importante entender que, depois de todas as tentativas serem feitas, o AEM Forms bloqueia o usuário antes que o Servidor de Diretório LDAP o faça.

#### Definir bloqueio de conta automática {#set-automatic-account-locking}

1. Faça logon no Console de administração.
1. Clique em **Configurações** > **Gerenciamento de Usuário** > **Gerenciamento de Domínio**.
1. Em Configurações automáticas de bloqueio de conta, defina **Máximo de falhas de autenticação consecutiva** para um número baixo, como 3.
1. Clique em **Salvar**.

### Auditoria e registro {#auditing-and-logging}

O uso correto e seguro da auditoria e registro de aplicativos pode ajudar a garantir que a segurança e outros eventos anômalos sejam rastreados e detectados o mais rápido possível. O uso eficiente de auditoria e registro em um aplicativo inclui itens como rastreamento de logons bem-sucedidos e com falha, bem como eventos-chave do aplicativo, como a criação ou exclusão de registros-chave.

Você pode usar a auditoria para detectar vários tipos de ataques, incluindo estes:

* Ataques de senha de força bruta
* Ataques de negação de serviço
* Injeção de entrada hostil e classes relacionadas de ataques de script

Esta tabela descreve técnicas de auditoria e registro que podem ser usadas para reduzir as vulnerabilidades do seu servidor.

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
   <td><p>Defina o AEM Forms apropriado nas ACLs (listas de controle de acesso) do arquivo de log JEE.</p> <p>Definir as credenciais apropriadas ajuda a impedir que os invasores excluam os arquivos.</p> <p>As permissões de segurança no diretório do arquivo de log devem ser Controle Total para Administradores e grupos SYSTEM. A conta de usuário do AEM Forms deve ter somente permissões de Leitura e Gravação.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redundância do arquivo de log</p> </td> 
   <td><p>Se os recursos permitirem, envie registros para outro servidor em tempo real que não seja acessível pelo invasor (somente gravação) usando o Syslog, Tivoli, Microsoft Operations Manager (MOM) Server ou outro mecanismo.</p> <p>Proteger logs dessa forma ajuda a impedir a adulteração. Além disso, o armazenamento de logs em um repositório central auxilia na correlação e no monitoramento (por exemplo, se vários servidores de formulários estiverem em uso e um ataque de adivinhação de senha estiver ocorrendo em vários computadores, onde cada computador é consultado por uma senha).</p> </td> 
  </tr> 
 </tbody> 
</table>

### Ativar um usuário não administrador para executar o Gerador de PDF

Você pode ativar um usuário não administrador para usar o Gerador de PDF. Normalmente, somente os usuários com privilégios administrativos podem usar o Gerador de PDF. Execute as etapas a seguir para permitir que um usuário não administrador execute o Gerador de PDF:

1. Crie um nome de variável de ambiente PDFG_NON_ADMIN_ENABLED.

1. Defina o valor da variável como TRUE.

1. Reinicie a instância do AEM Forms.

## Configuração do AEM Forms no JEE para acesso além da empresa {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Depois de instalar o AEM Forms com êxito no JEE, é importante manter periodicamente a segurança do seu ambiente. Esta seção descreve as tarefas recomendadas para manter a segurança do AEM Forms no servidor de produção JEE.

### Configurar um proxy reverso para acesso à Web {#setting-up-a-reverse-proxy-for-web-access}

Um *proxy reverso* pode ser usado para garantir que um conjunto de URLs para AEM Forms em aplicativos Web JEE esteja disponível para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos no qual o AEM Forms no JEE está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor de aplicativos que está executando o AEM Forms no JEE. Os usuários têm somente acesso de rede ao proxy reverso e só podem tentar conexões de URL compatíveis com o proxy reverso.

**AEM Forms em URLs raiz JEE para uso com servidor proxy reverso**

Os seguintes URLs raiz do aplicativo para cada AEM Forms no aplicativo Web JEE. Você deve configurar seu proxy reverso somente para expor URLs para a funcionalidade de aplicativos Web que deseja fornecer aos usuários finais.

Determinados URLs são destacados como aplicativos da Web voltados para o usuário final. Você deve evitar expor outros URLs para o Configuration Manager para acesso a usuários externos por meio do proxy reverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL raiz</p> </th> 
   <th><p>Finalidade e/ou aplicação web associada</p> </th> 
   <th><p>Interface baseada na Web</p> </th> 
   <th><p>Acesso do usuário final</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>Aplicação Web do usuário final das extensões do Acrobat Reader DC para aplicar direitos de uso a documentos PDF</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Aplicativo web Rights Management end-user</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edcws/*</p> </td> 
   <td><p>URL do serviço Web para Rights Management</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/pdfgui/*</p> </td> 
   <td><p>Aplicativo web de administração do Gerador de PDF</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/espaço de trabalho/*</p> </td> 
   <td><p>Aplicativo Web do usuário final do Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets e serviços de dados do Workspace necessários para o aplicativo cliente do Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet para bootstrapping do AEM Forms no repositório JEE</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/*</p> </td> 
   <td><p>Página de informações para serviços da Web do servidor de formulários</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/soap/services/*</p> </td> 
   <td><p>URL do serviço da Web para todos os serviços do servidor de formulários</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Aplicativo web de administração de Rights Management</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>Página inicial do Console de administração</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/TruststoreComponent/</p> <p>protegido/*</p> </td> 
   <td><p>Páginas de administração do Gerenciamento de Armazenamento de Confiança</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormsIVS/*</p> </td> 
   <td><p>Aplicativo IVS do Forms para teste e depuração da renderização do formulário</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/OutputIVS/*</p> </td> 
   <td><p>Aplicativo IVS de saída para teste e depuração do serviço de saída</p> </td> 
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
   <td><p>Páginas de administração da saída</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/*</p> </td> 
   <td><p>Arquivos de aplicativos Web Forms</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Usado para buscar o JavaScript durante a transformação do HTML</p> </td> 
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
   <td><p>Interface do usuário de Aplicativos e Serviços</p> </td> 
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
   <td><p>Páginas de suporte do Rest</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms na página de configurações principais do JEE</p> </td> 
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
   <td><p>/DoumentManager/*</p> </td> 
   <td><p>Upload e download de documentos que devem ser processados ao acessar pontos de extremidade remotos, pontos de extremidade WSDL de SOAP e o SDK Java sobre transporte SOAP ou transporte EJB com documentos HTTP ativados.</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
 </tbody> 
</table>

## Proteção contra ataques de falsificação de solicitação entre sites {#protecting-from-cross-site-request-forgery-attacks}

Um ataque CSRF (Cross-Site Request Forgery) explora a confiança que um site tem para o usuário, para transmitir comandos que são não autorizados e não intencionais pelo usuário. O ataque é configurado ao incluir um link ou script em uma página da Web ou um URL em uma mensagem de email para acessar outro site no qual o usuário já foi autenticado.

Por exemplo, você pode estar conectado ao Console de administração enquanto navega simultaneamente em outro site. Uma das páginas da Web pode incluir uma tag de imagem HTML com um atributo `src` que direciona um script do lado do servidor no site da vítima. Ao utilizar o mecanismo de autenticação de sessão baseado em cookies fornecido pelos navegadores da Web, o site de ataque pode enviar solicitações mal-intencionadas para esse script do lado do servidor da vítima, mascarando-o como o usuário legítimo. Para obter mais exemplos, consulte [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

As seguintes características são comuns ao CSRF:

* Envolva sites que dependem da identidade de um usuário.
* Explore a confiança do site nessa identidade.
* Faça com que o navegador do usuário envie solicitações HTTP para um site de destino.
* Envolva solicitações HTTP que tenham efeitos colaterais.

O AEM Forms no JEE usa o recurso de Filtro de referenciador para bloquear ataques de CSRF. Os termos a seguir são usados nesta seção para descrever o mecanismo de Filtragem do referenciador:

* **Referenciador Permitido:** Referenciador é o endereço da página de origem que envia uma solicitação ao servidor. Para páginas ou formulários JSP, os Referenciadores geralmente são a página anterior no histórico de navegação. Referenciador de imagens geralmente são as páginas em que as imagens são exibidas. Você pode identificar o Referenciador que tem acesso aos recursos do seu servidor, adicionando-o à lista Referenciador Permitido.
* **Exceções de Referenciador Permitidas:** Você pode querer restringir o escopo de acesso de um Referenciador específico em sua lista de Referenciador Permitido. Para impor essa restrição, você pode adicionar caminhos individuais desse Referenciador à lista Exceções de Referenciador Permitidas. As solicitações originadas de caminhos na lista Exceções de referenciador permitidas são impedidas de chamar qualquer recurso no servidor de formulários. Você pode definir Exceções de Referenciador Permitidas para um aplicativo específico e também usar uma lista global de exceções que se aplicam a todos os aplicativos.
* **URIs permitidos:** é uma lista de recursos que devem ser veiculados sem verificar o Cabeçalho do Referenciador. Os recursos, por exemplo, as páginas de ajuda, que não resultam em alterações de estado no servidor, podem ser adicionados a esta lista. Os recursos na lista de URIs permitidos nunca são bloqueados pelo Filtro de Referenciador, independentemente de quem é o Referenciador.
* **Referenciador nulo:** uma solicitação de servidor que não está associada ou não é originária de uma página da Web pai é considerada uma solicitação de um Referenciador nulo. Por exemplo, quando você abre uma nova janela do navegador, digita um endereço e pressiona enter, o Referenciador enviado para o servidor é nulo. Um aplicativo de desktop (.NET ou SWING) que faz uma solicitação HTTP para um servidor da Web, também envia um Referenciador Nulo para o servidor.

### Filtragem do referenciador {#referer-filtering}

O processo de Filtragem do referenciador pode ser descrito da seguinte maneira:

1. O servidor de formulários verifica o método HTTP usado para invocação:

   1. Se for POST, o servidor de formulários executará a verificação do cabeçalho Referenciador.
   1. Se for GET, o servidor de formulários ignora a verificação do Referenciador, a menos que *CSRF_CHECK_GETS* esteja definido como true, nesse caso, ele executa a verificação do cabeçalho do Referenciador. *CSRF_CHECK_* GETSé especificado no arquivo  *web.* xmlfile do seu aplicativo.

1. O servidor de formulários verifica se o URI solicitado existe lista de permissões:

   1. Se o URI for incluir na lista de permissões, o servidor aceitará a solicitação.
   1. Se o URI solicitado não for incluir na lista de permissões, o servidor recuperará o Referenciador da solicitação.

1. Se houver um Referenciador na solicitação, o servidor verificará se é um Referenciador Permitido. Se for permitido, o servidor verifica se há uma Exceção de referenciador:

   1. Se for uma exceção, a solicitação será bloqueada.
   1. Se não for uma exceção, a solicitação será passada.

1. Se não houver um Referenciador na solicitação, o servidor verificará se um Referenciador Nulo é permitido:

   1. Se um Referenciador Nulo for permitido, a solicitação será passada.
   1. Se um Referenciador Nulo não for permitido, o servidor verificará se o URI solicitado é uma exceção para o Referenciador Nulo e tratará a solicitação de acordo.

### Gerenciar filtros de referenciador {#managing-referer-filtering}

O AEM Forms no JEE fornece um Filtro de referenciador para especificar Referenciador que tem acesso aos recursos do servidor. Por padrão, o filtro Referenciador não filtra solicitações que usam um método HTTP seguro, por exemplo, GET, a menos que *CSRF_CHECK_GETS* esteja definido como true. Se o número da porta de uma entrada de Referenciador Permitido for definido como 0, o AEM Forms no JEE permitirá todas as solicitações com Referenciador desse host, independentemente do número da porta. Se nenhum número de porta for especificado, somente as solicitações da porta padrão 80 (HTTP) ou da porta 443 (HTTPS) serão permitidas. A Filtragem de referenciador será desativada se todas as entradas na lista Referenciador permitido forem excluídas.

Quando você instala os Serviços de documento pela primeira vez, a lista Referenciador permitido é atualizada com o endereço do servidor no qual os Serviços de documento estão instalados. As entradas para o servidor incluem o nome do servidor, o endereço IPv4, o endereço IPv6 se IPv6 estiver ativado, o endereço de loopback e uma entrada de host local. Os nomes adicionados à lista Referenciador Permitido são retornados pelo sistema operacional Host. Por exemplo, um servidor com um endereço IP de 10.40.54.187 incluirá as seguintes entradas: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Para qualquer nome não qualificado retornado pelo sistema operacional Host (nomes que não têm endereço IPv4, endereço IPv6 ou nome de domínio qualificado) lista de permissões não é atualizada. Modifique a lista Referenciador permitido para atender ao seu ambiente de negócios. Não implante o servidor de formulários no ambiente de produção com a lista de Referenciadores permitidos padrão. Depois de modificar qualquer um dos Referenciador Permitido, Exceções de Referenciador ou URIs, certifique-se de reiniciar o servidor para que as alterações tenham efeito.

**Gerenciamento da lista de referenciadores permitidos**

Você pode gerenciar a lista Referenciador Permitido na Interface de Gerenciamento de Usuário do Console de Administração. A Interface de gerenciamento de usuários oferece a funcionalidade de criar, editar ou excluir a lista. Consulte a seção * [Impedindo ataques de CSRF](/help/forms/using/admin-help/preventing-csrf-attacks.md)* da *ajuda de administração* para obter mais informações sobre como trabalhar com a lista Referenciador Permitido.

**Gerenciando Exceções de Referenciador Permitidas e Listas de URI Permitidas**

O AEM Forms no JEE fornece APIs para gerenciar a lista Exceção de referenciador permitida e a lista URI permitido. Você pode usar essas APIs para recuperar, criar, editar ou excluir a lista. Veja a seguir uma lista de APIs disponíveis:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Consulte o* AEM Forms on JEE API Reference* para obter mais informações sobre as APIs.

Use a lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** para Exceções de Referenciador Permitidas no nível global, ou seja, para definir exceções aplicáveis a todos os aplicativos. Esta lista contém somente URIs com um caminho absoluto (por exemplo, `/index.html`) ou um caminho relativo (por exemplo, `/sample/`). Também é possível anexar uma expressão regular ao final de um URI relativo, por exemplo `/sample/(.)*`.

A ID da lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** é definida como uma constante na classe `UMConstants` do namespace `com.adobe.idp.um.api`, encontrada em `adobe-usermanager-client.jar`. Você pode usar as APIs do AEM Forms para criar, modificar ou editar essa lista. Por exemplo, para criar a lista Exceções de referenciador global permitidas use:

```java
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Use a lista ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** para exceções específicas do aplicativo.

**Desabilitação do filtro de referenciador**

Caso o Filtro de referência bloqueie completamente o acesso ao servidor de formulários e não seja possível editar a lista Referenciador permitido, é possível atualizar o script de inicialização do servidor e desativar a Filtragem de referenciador.

Inclua o argumento `-Dlc.um.csrffilter.disabled=true` JAVA no script de inicialização e reinicie o servidor. Certifique-se de excluir o argumento JAVA depois de reconfigurar apropriadamente a lista Referenciador permitido.

**Filtragem de referenciador para arquivos WAR personalizados**

Você pode ter criado arquivos WAR personalizados para trabalhar com o AEM Forms no JEE para atender às suas necessidades de negócios. Para ativar a Filtragem de referenciador para seus arquivos WAR personalizados, inclua ***adobe-usermanager-client.jar*** no caminho de classe para a WAR e inclua uma entrada de filtro no arquivo web.xml* com os seguintes parâmetros:

**CSRF_CHECK_** GETScontrola a verificação do Referenciador nas solicitações do GET. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua esse parâmetro somente se desejar filtrar as solicitações do GET.

**CSRF_ALLOWED_REFERER_** EXCEPTIONSé a ID da lista de Exceções de referenciador permitidas. O Filtro de referenciador impede que as solicitações originárias de Referenciadores na lista identificada pela ID da lista cheguem a qualquer recurso no servidor de formulários.

**CSRF_ALLOWED_URIS_LIST_** NAMEé a ID da lista de URIs permitidos. O Filtro de referenciador não bloqueia solicitações para nenhum dos recursos na lista identificada pela ID da lista, independentemente do valor do cabeçalho Referenciador na solicitação.

**CSRF_ALLOW_NULL_** REFERERcontrola o comportamento do Filtro referenciador quando o Referenciador é nulo ou não está presente. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua este parâmetro somente se desejar permitir Referenciadores nulos. Permitir referenciadores nulos pode permitir alguns tipos de ataques de falsificação de solicitação entre sites.

**CSRF_NULL_REFERER_** EXCEPTIONSé uma lista de URIs para os quais uma verificação do Referenciador não é executada quando o Referenciador é nulo. Esse parâmetro é ativado somente quando *CSRF_ALLOW_NULL_REFERER* é definido como falso. Separe vários URIs na lista com uma vírgula.

A seguir, um exemplo da entrada de filtro no arquivo *web.xml* para um arquivo ***SAMPLE*** WAR:

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

Se solicitações de servidor legítimas estiverem sendo bloqueadas pelo filtro CSRF, tente uma das seguintes opções:

* Se a solicitação rejeitada tiver um cabeçalho Referenciador, considere adicioná-la cuidadosamente à lista Referenciador permitido. Adicione somente o Referenciador em que você confia.
* Se a solicitação rejeitada não tiver um cabeçalho Referenciador, modifique seu aplicativo cliente para incluir um cabeçalho Referenciador.
* Se o cliente puder trabalhar em um navegador, tente esse modelo de implantação.
* Como último recurso, você pode adicionar o recurso à lista de URIs permitidos . Essa não é uma configuração recomendada.

## Configuração de rede segura {#secure-network-configuration}

Esta seção descreve os protocolos e as portas exigidos pelo AEM Forms no JEE e fornece recomendações para implantar o AEM Forms no JEE em uma configuração de rede segura.

### Protocolos de rede usados pelo AEM Forms no JEE {#network-protocols-used-by-aem-forms-on-jee}

Quando você configura uma arquitetura de rede segura conforme descrito na seção anterior, os seguintes protocolos de rede são necessários para a interação entre o AEM Forms no JEE e outros sistemas em sua rede corporativa.

<table> 
 <thead> 
  <tr> 
   <th><p>Protocolo</p> </th> 
   <th><p>Uso</p> </th> 
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
     <li><p>Aplicativos cliente do serviço da Web, como aplicativos .NET</p> </li> 
     <li><p>O Adobe Reader® usa SOAP para AEM Forms em serviços da Web do servidor JEE</p> </li> 
     <li><p>Os aplicativos do Flash Adobe® usam SOAP para serviços da Web de servidores de formulários</p> </li> 
     <li><p>AEM Forms em chamadas JEE SDK, quando usado no modo SOAP</p> </li> 
     <li><p>Ambiente de design do Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>AEM Forms em chamadas JEE SDK, quando usado no modo Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrada baseada em email para um serviço (endpoint de email)</p> </li> 
     <li><p>Notificações de tarefa do usuário por email</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>E/S de arquivo UNC</p> </td> 
   <td><p>Monitoramento do AEM Forms on JEE de pastas vigiadas para entrada em um serviço (ponto de extremidade de pasta monitorada)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizações de informações do usuário organizacional e do grupo em um diretório</p> </li> 
     <li><p>Autenticação LDAP para usuários interativos</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Chamadas de consulta e procedimento feitas para um banco de dados externo durante a execução de um processo usando o serviço JDBC</p> </li> 
     <li><p>Acesso interno ao AEM Forms no repositório JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permite a navegação remota do AEM Forms no repositório de tempo de design do JEE (formulários, fragmentos e assim por diante) por qualquer cliente WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Aplicativos Adobe Flash, onde o AEM Forms em serviços de servidor JEE é configurado com um terminal Remoting</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms no JEE expõe MBeans para monitoramento usando JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Portas para servidores de aplicativos {#ports-for-application-servers}

Esta seção descreve as portas padrão (e intervalos de configuração alternativos) para cada tipo de servidor de aplicativos suportado. Essas portas devem ser ativadas ou desativadas no firewall interno, dependendo da funcionalidade de rede que você deseja permitir para clientes que se conectam ao servidor de aplicativos que executa o AEM Forms no JEE.

>[!NOTE]
>
>Por padrão, o servidor expõe vários MBeans JMX no namespace adobe.com. Apenas informações úteis para monitoramento de integridade do servidor são expostas. No entanto, para evitar a divulgação de informações, você deve impedir que os chamadores em uma rede não confiável pesquisem MBeans JMX e acessem métricas de integridade.

**Portas JBoss**

<table> 
 <thead> 
  <tr> 
   <th><p>Propósito</p> </th> 
   <th><p>Port</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acesso a aplicações web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Porta do conector HTTP/1.1 8080</p> <p>Porta do conector AJP 1.3 8009</p> <p>Porta do conector SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Suporte a CORBA</p> </td> 
   <td><p>[Raiz do JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Portas WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Propósito</p> </th> 
   <th><p>Port</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acesso a aplicações web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do servidor de administração: o padrão é 7001</p> </li> 
     <li><p>Porta de escuta SSL do servidor de administração: o padrão é 7002</p> </li> 
     <li><p>Porta configurada para Servidor gerenciado, por exemplo 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>As portas de administração do WebLogic não são necessárias para acessar o AEM Forms no JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do Servidor Gerenciado: Configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta SSL do Servidor Gerenciado: Configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta do Gerenciador de nós: o padrão é 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Portas do WebSphere**

Para obter informações sobre portas WebSphere que o AEM Forms no JEE requer, vá para a configuração Número da porta na interface do usuário do WebSphere Application Server.

### Configuração de SSL {#configuring-ssl}

Referindo-se à arquitetura física descrita na seção [AEM Forms on JEE physical architecture](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture), você deve configurar o SSL para todas as conexões que planeja usar. Especificamente, todas as conexões SOAP devem ser realizadas por SSL para evitar a exposição de credenciais de usuário em uma rede.

Para obter instruções sobre como configurar o SSL em JBoss, WebLogic e WebSphere, consulte &quot;Configuração do SSL&quot; na [administration help](https://www.adobe.com/go/learn_aemforms_admin_64).

Para obter instruções sobre como importar certificados para a JVM (Java Virtual Machine) configurada para um servidor AEM Forms, consulte a seção Autenticação Mútua em [Ajuda do AEM Forms Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65).

### Configuração do redirecionamento SSL {#configuring-ssl-redirect}

Depois de configurar o servidor de aplicativos para suportar SSL, você deve garantir que todo o tráfego HTTP para aplicativos e serviços seja empregado para usar a porta SSL.

Para configurar o redirecionamento SSL para WebSphere ou WebLogic, consulte a documentação do servidor de aplicativos.

1. Abra o prompt de comando, navegue até o diretório /JBOSS_HOME/standalone/configuration e execute o seguinte comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Abra o arquivo JBOSS_HOME/standalone/configuration/standalone.xml para edição.

   Após o elemento &lt;subsistema xmlns=&quot;urn:jboss:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, adicione os seguintes detalhes:

   &lt;connector name=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; scheme=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot; />

1. Adicione o seguinte código no elemento do conector https:

   ```xml
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salve e feche o arquivo standalone.xml.

## Recomendações de segurança específicas do Windows {#windows-specific-security-recommendations}

Esta seção contém recomendações de segurança específicas do Windows quando usadas para executar o AEM Forms no JEE.

### Contas do Serviço JBoss {#jboss-service-accounts}

A instalação turnkey do AEM Forms em JEE configura uma conta de serviço, por padrão, usando a conta Sistema local. A conta de usuário integrada do Sistema local tem um alto nível de acessibilidade; faz parte do grupo Administradores . Se uma identidade de processo de trabalho for executada como a conta de usuário do Sistema Local, esse processo de trabalho terá acesso total ao sistema inteiro.

#### Executar o servidor de aplicativos usando uma conta não administrativa {#run-the-application-server-using-a-non-administrative-account}

1. No Console de Gerenciamento da Microsoft (MMC), crie um usuário local para que o serviço do servidor de formulários faça logon como:

   * Selecione **O usuário não pode alterar a senha**.
   * Na guia **Member Of** , verifique se o grupo Users é listado.

1. Selecione **Configurações** > **Ferramentas Administrativas** > **Serviços**.
1. Clique duas vezes no serviço do servidor de aplicativos e pare o serviço.
1. Na guia **Fazer logon**, selecione **Esta conta**, procure a conta de usuário criada e insira a senha da conta.
1. Na janela Configurações de segurança locais , em Atribuição de direitos de usuário, atribua os seguintes direitos à conta de usuário em que o servidor de formulários está sendo executado:

   * Negar logon por meio dos Serviços de Terminal
   * Negar logon localmente
   * Fazer logon como Serviço (já deve estar definido)

1. Forneça permissões de modificação à nova conta de usuário nos seguintes diretórios:
   * **Diretório** Global Document Storage (GDS): A localização do diretório GDS é configurada manualmente durante o processo de instalação do AEM Forms. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório** CRX-Repository: O local padrão é  `[AEM-Forms-installation-location]\crx-repository`
   * **Diretórios** temporários do AEM Forms:
      * (Windows) Caminho TMP ou TEMP conforme definido nas variáveis de ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectado
Em sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Forneça permissões de gravação à nova conta de usuário nos seguintes diretórios:
   * [JBoss-diretory]\standalone\deployment
   * [JBoss-diretory]\standalone\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   > O local de instalação padrão do JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jboss/.


1. Inicie o serviço do servidor de aplicativos.

### Segurança do sistema de arquivos {#file-system-security}

O AEM Forms no JEE usa o sistema de arquivos das seguintes maneiras:

* Armazena arquivos temporários que são usados durante o processamento da entrada e saída do documento
* Armazena arquivos no repositório de arquivamento global que são usados para suportar os componentes da solução que estão instalados
* As pastas vigiadas armazenam arquivos descartados usados como entrada para um serviço de um local de pasta do sistema de arquivos

Ao usar pastas vigiadas como uma maneira de enviar e receber documentos com um serviço de servidor de formulários, tome precauções extras com a segurança do sistema de arquivos. Quando um usuário solta o conteúdo na pasta assistida, ele é exposto por meio da pasta assistida. Nesse caso, o serviço não autentica o usuário final real. Em vez disso, ele depende da segurança de nível de ACL e Compartilhamento para ser definida no nível da pasta para determinar quem pode chamar efetivamente o serviço.

## Recomendações de segurança específicas do JBoss {#jboss-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos que são específicas para o JBoss 7.0.6 quando usado para executar o AEM Forms no JEE.

### Desativar o Console de Gerenciamento JBoss e o Console JMX {#disable-jboss-management-console-and-jmx-console}

O acesso ao Console de Gerenciamento JBoss e ao Console JMX já está configurado (o monitoramento JMX está desativado) quando você instala o AEM Forms no JEE no JBoss usando o método de instalação turnkey. Se estiver usando seu próprio JBoss Application Server, verifique se o acesso ao JBoss Management Console e ao console de monitoramento JMX estão protegidos. O acesso ao console de monitoramento JMX é definido no arquivo de configuração JBoss chamado jmx-invoker-service.xml.

### Desativar navegação no diretório {#disable-directory-browsing}

Depois de fazer logon no Console de administração, é possível navegar na lista de diretórios do console modificando o URL. Por exemplo, se você alterar o URL para um dos URLs a seguir, uma listagem de diretório pode ser exibida:

```java
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recomendações de segurança específicas do WebLogic {#weblogic-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebLogic 9.1 ao executar o AEM Forms no JEE.

### Desativar navegação no diretório {#disable_directory_browsing-1}

Defina as propriedades dos diretórios de índice no arquivo weblogic.xml para `false`, conforme mostrado neste exemplo:

```xml
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Habilitar Porta SSL do WebLogic {#enable-weblogic-ssl-port}

Por padrão, o WebLogic não habilita a Porta de escuta SSL padrão, 7002. Ative essa porta no Console de Administração do WebLogic Server antes de configurar o SSL.

## Recomendações de segurança específicas do WebSphere {#websphere-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebSphere executando o AEM Forms no JEE.

### Desativar navegação no diretório {#disable_directory_browsing-2}

Defina a propriedade `directoryBrowsingEnabled` no arquivo ibm-web-ext.xml para `false`.

### Habilitar a segurança administrativa do WebSphere {#enable-websphere-administrative-security}

1. Faça logon no Console Administrativo do WebSphere.
1. Na árvore de navegação, vá para **Segurança** > **Segurança Global**
1. Selecione **Ativar segurança administrativa**.
1. Desmarque **Ativar a segurança do aplicativo** e **Usar a segurança do Java 2**.
1. Clique em **OK** ou **Aplicar**.
1. Na caixa **Messages**, clique em **Save diretamente to the principal configuration**.
