---
title: Como fortalecer seus AEM Forms no Ambiente JEE
seo-title: Como fortalecer seus AEM Forms no Ambiente JEE
description: Saiba mais sobre várias configurações de segurança para aumentar a segurança dos AEM Forms no JEE em execução em uma intranet corporativa.
seo-description: Saiba mais sobre várias configurações de segurança para aumentar a segurança dos AEM Forms no JEE em execução em uma intranet corporativa.
uuid: f6c63690-6376-4fe1-9df2-a14fbfd62aff
content-type: reference
topic-tags: Security
products: SG_EXPERIENCEMANAGER/6.4
discoiquuid: 6b380e92-f90d-4875-b7a2-f3958daf2364
translation-type: tm+mt
source-git-commit: 6cb05cab9ecbb9fc88e16cc1ab24cafccf7d0b16
workflow-type: tm+mt
source-wordcount: '7603'
ht-degree: 0%

---


# Como fortalecer seus AEM Forms no Ambiente JEE {#hardening-your-aem-forms-on-jee-environment}

Saiba mais sobre várias configurações de segurança para aumentar a segurança dos AEM Forms no JEE em execução em uma intranet corporativa.

O artigo descreve recomendações e práticas recomendadas para proteger servidores que executam AEM Forms no JEE. Este não é um documento abrangente que endurece o host para seu sistema operacional e servidores de aplicativos. Em vez disso, este artigo descreve uma variedade de configurações de segurança que você deve implementar para melhorar a segurança dos AEM Forms no JEE que está sendo executado em uma intranet corporativa. No entanto, para garantir que os AEM Forms nos servidores de aplicativos JEE permaneçam protegidos, você também deve implementar procedimentos de monitoramento, detecção e resposta de segurança.

O artigo descreve técnicas de endurecimento que devem ser aplicadas durante os seguintes estágios durante o ciclo de vida da instalação e configuração:

* **Pré-instalação:** Use essas técnicas antes de instalar o AEM Forms no JEE.
* **Instalação:** Use essas técnicas durante os AEM Forms no processo de instalação do JEE.
* **Pós-instalação:** Use essas técnicas após a instalação e periodicamente a partir daí.

AEM Forms em JEE são altamente personalizáveis e podem funcionar em vários ambientes diferentes. Algumas das recomendações podem não atender às necessidades de sua organização.

## Pré-instalação {#preinstallation}

Antes de instalar AEM Forms no JEE, você pode aplicar soluções de segurança à camada de rede e ao sistema operacional. Esta seção descreve alguns problemas e faz recomendações para reduzir as vulnerabilidades de segurança nessas áreas.

**Instalação e configuração em UNIX e Linux**

Você não deve instalar ou configurar AEM Forms no JEE usando um shell raiz. Por padrão, os arquivos são instalados no diretório /opt e o usuário que executa a instalação precisa de todas as permissões de arquivo em /opt. Como alternativa, uma instalação pode ser executada sob o diretório /usuário de um usuário individual, onde ele já tem todas as permissões de arquivo.

**Instalação e configuração no Windows**

Você deve executar a instalação no Windows como um administrador se estiver instalando AEM Forms no JEE em JBoss usando o método chave na mão ou se estiver instalando o Gerador de PDF. Além disso, ao instalar o Gerador de PDF no Windows com suporte a aplicativo nativo, você deve executar a instalação como o mesmo usuário do Windows que instalou o Microsoft Office. Para obter mais informações sobre os privilégios de instalação, consulte o documento* Installing and Deploying AEM Forms on JEE* para seu servidor de aplicativos.

### Segurança da camada de rede {#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de endurecimento de hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o endurecimento da pilha do protocolo de controle de transmissão/protocolo TCP/IP e o uso de firewalls para proteção de host.

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
   <td><p>Implante servidores de formulários em uma zona desmilitarizada (DMZ). A segmentação deve existir em pelo menos dois níveis com o servidor de aplicativos usado para executar AEM Forms em JEE colocados atrás do firewall interno. Separe a rede externa da DMZ que contém os servidores da Web, que, por sua vez, devem ser separados da rede interna. Use firewalls para implementar as camadas de separação. Categorize e controle o tráfego que passa por cada camada de rede para garantir que somente o mínimo absoluto de dados necessários seja permitido.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Endereços IP privados</p> </td> 
   <td><p>Use a tradução de endereço de rede (NAT) com endereços IP privados RFC 1918 no servidor de aplicativos AEM Forms. Atribua endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear tráfego de e para um host interno de NAT pela Internet.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Firewalls</p> </td> 
   <td><p>Use os seguintes critérios para selecionar uma solução de firewall:</p> 
    <ul> 
     <li><p>Implemente firewalls que suportam servidores proxy e/ou inspeção <em></em> com monitoração de estado em vez de soluções simples de filtragem de pacotes.</p> </li> 
     <li><p>Use um firewall que suporte uma <em>negação de todos os serviços, exceto aqueles que são explicitamente permitidos</em> pelos paradigmas de segurança.</p> </li> 
     <li><p>Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o maior nível de segurança e ajuda a impedir que usuários não autorizados ignorem a segurança do firewall.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>Portas de banco de dados</p> </td> 
   <td><p>Não use portas de escuta padrão para bancos de dados (MySQL - 3306, Oracle - 1521, MS SQL - 1433). Para obter informações sobre como alterar portas de banco de dados, consulte a documentação de seu banco de dados.</p> <p>O uso de uma porta de banco de dados diferente afeta os AEM Forms gerais na configuração do JEE. Se você alterar as portas padrão, deverá fazer as modificações correspondentes em outras áreas de configuração, como as fontes de dados para AEM Forms no JEE.</p> <p>Para obter informações sobre como configurar fontes de dados em AEM Forms no JEE, consulte Instalar e atualizar AEM Forms no JEE ou Atualizar para AEM Forms no JEE para seu servidor de aplicativos no guia <a href="/help/forms/using/introduction-aem-forms.md" target="_blank">do usuário do</a>AEM Forms.</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do sistema operacional {#operating-system-security}

A tabela a seguir descreve algumas abordagens possíveis para minimizar vulnerabilidades de segurança encontradas no sistema operacional.

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
   <td><p>Existe um risco aumentado de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção.</p><p>Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente.</p></td> 
  </tr> 
  <tr> 
   <td><p>Software de proteção contra vírus</p></td> 
   <td><p>Os verificadores de vírus podem identificar arquivos infectados digitalizando uma assinatura ou observando um comportamento incomum. Os scanners mantêm suas assinaturas de vírus em um arquivo, que geralmente é armazenado no disco rígido local. Como os novos vírus são descobertos com frequência, você deve atualizar esse arquivo com frequência para o verificador de vírus para identificar todos os vírus atuais.</p></td> 
  </tr> 
  <tr> 
   <td><p>NTP (Network Time Protocol, protocolo de tempo de rede)</p></td> 
   <td><p>Para a análise forense, mantenha o tempo exato nos servidores de formulários. Use o NTP para sincronizar o tempo em todos os sistemas conectados diretamente à Internet.</p></td> 
  </tr> 
 </tbody> 
</table>

Para obter informações adicionais de segurança para seu sistema operacional, consulte [&quot;Informações de segurança do sistema operacional&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#operating_system_security_information).

## Instalação {#installation}

Esta seção descreve as técnicas que você pode usar durante o processo de instalação do AEM Forms para reduzir as vulnerabilidades de segurança. Em alguns casos, essas técnicas usam opções que fazem parte do processo de instalação. A tabela a seguir descreve essas técnicas.

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
   <td><p>Use o menor número de privilégios necessários para instalar o software. Faça logon no computador usando uma conta que não esteja no grupo Administradores. No Windows, você pode usar o comando Executar como para executar os AEM Forms no instalador JEE como um usuário administrativo. Em sistemas UNIX e Linux, use um comando como <code>sudo</code> para instalar o software.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Fonte do software</p> </td> 
   <td><p>Não baixe nem execute AEM Forms em JEE de fontes não confiáveis.</p> <p>programas mal-intencionados podem conter código para violar a segurança de várias maneiras, incluindo roubo, modificação e exclusão de dados e negação de serviço. Instale AEM Forms no JEE a partir do Adobe DVD ou somente a partir de uma fonte confiável.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Partições de disco</p> </td> 
   <td><p>Coloque AEM Forms em JEE em uma partição de disco dedicada. A segmentação de disco é um processo que mantém dados específicos no servidor em discos físicos separados para aumentar a segurança. Organizar os dados dessa forma reduz o risco de ataques cruzados de diretórios. Planeje criar uma partição separada da partição do sistema na qual você possa instalar os AEM Forms no diretório de conteúdo JEE. (No Windows, a partição do sistema contém o diretório system32 ou a partição de inicialização.)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Componentes</p> </td> 
   <td><p>Avalie os serviços existentes e desabilite ou desinstale quaisquer que não sejam necessários. Não instale componentes e serviços desnecessários.</p> <p>A instalação padrão de um servidor de aplicativos pode incluir serviços que não são necessários para o seu uso. Você deve desativar todos os serviços desnecessários antes da implantação para minimizar os pontos de entrada de um ataque. Por exemplo, no JBoss, você pode comentar serviços desnecessários no arquivo META-INF/jboss-service.xml descritor.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Arquivo de política entre domínios</p> </td> 
   <td><p>A presença de um <code>crossdomain.xml</code> arquivo no servidor pode enfraquecer imediatamente esse servidor. É recomendável tornar a lista de domínios o mais restritiva possível. Não coloque o <code>crossdomain.xml</code> arquivo que foi usado durante o desenvolvimento em produção ao usar Guias <em>(obsoleto)</em>. Para um guia que usa serviços da Web, se o serviço estiver no mesmo servidor que serviu o guia, um <code>crossdomain.xml</code> arquivo não será necessário. Mas se o serviço estiver em outro servidor, ou se houver clusters envolvidos, a presença de um <code>crossdomain.xml</code> arquivo será necessária. Consulte <a href="https://kb2.adobe.com/cps/142/tn_14213.html">https://kb2.adobe.com/cps/142/tn_14213.html</a>para obter mais informações sobre o arquivo crossdomain.xml.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de segurança do sistema operacional</p> </td> 
   <td><p>Se você precisar usar criptografia XML de 192 bits ou 256 bits em plataformas Solaris, certifique-se de instalar <code>pkcs11_softtoken_extra.so</code> em vez de <code>pkcs11_softtoken.so</code>.</p> </td> 
  </tr> 
 </tbody> 
</table>

## Etapas pós-instalação {#post-installation-steps}

Depois de instalar o AEM Forms com êxito no JEE, é importante manter o ambiente periodicamente de uma perspectiva de segurança.

A seção a seguir descreve em detalhes as diferentes tarefas recomendadas para proteger o servidor de formulários implantados.

### segurança AEM Forms {#aem-forms-security}

As configurações recomendadas a seguir se aplicam aos AEM Forms no servidor JEE fora do aplicativo da Web administrativo. Para reduzir os riscos de segurança para o servidor, aplique essas configurações imediatamente após a instalação de AEM Forms no JEE.

**Patches de segurança**

Existe um risco aumentado de que um usuário não autorizado possa obter acesso ao servidor de aplicativos se os patches e atualizações de segurança do fornecedor não forem aplicados em tempo hábil. Teste os patches de segurança antes de aplicá-los aos servidores de produção para garantir a compatibilidade e disponibilidade dos aplicativos. Além disso, crie políticas e procedimentos para verificar e instalar patches regularmente. AEM Forms em atualizações JEE estão no site de download de produtos Enterprise.

**Contas de serviço (chave de acesso JBoss somente no Windows)**

O AEM Forms no JEE instala um serviço, por padrão, usando a conta LocalSystem. A conta de usuário LocalSystem integrada tem um alto nível de acessibilidade; faz parte do grupo Administradores. Se uma identidade de processo de trabalho for executada como a conta de usuário LocalSystem, esse processo de trabalho terá acesso total ao sistema inteiro.

Para executar o servidor de aplicativos no qual os AEM Forms no JEE são implantados, usando uma conta específica não administrativa, siga estas instruções:

1. No Microsoft Management Console (MMC), crie um usuário local para que o serviço do servidor de formulários faça logon como:

   * Selecione **Usuário não pode alterar a senha**.
   * Na guia **Membro de** , verifique se o grupo **Usuários** está listado.

   >[!NOTE]
   >
   >Não é possível alterar essa configuração para o Gerador de PDF.

1. Selecione **Start** > **Configurações** > Ferramentas **** administrativas > **Serviços**.
1. Duplo clique no JBoss para AEM Forms no JEE e pare o serviço.
1. Na guia **Logon** , selecione **Esta conta**, procure a conta de usuário que você criou e digite a senha da conta.
1. No MMC, abra Configurações **de segurança** local e selecione Políticas **** locais > Atribuição **de direitos de** usuário.
1. Atribua os seguintes direitos à conta de usuário na qual o servidor de formulários está sendo executado:

   * Negar logon por meio dos Serviços de Terminal
   * Negar logon localmente
   * Fazer logon como Serviço (já deve estar definido)

1. Atribua à nova conta de usuário permissões de modificação nos seguintes diretórios:
   * **Diretório** GDS: O local do diretório GDS é configurado manualmente durante o processo de instalação do AEM Forms. Se a configuração de localização permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório** CRX-Repository: O local padrão é `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms de diretórios** temporários:
      * (Windows) Caminho TMP ou TEMP conforme definido nas variáveis do ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectadoEm sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Atribua à nova conta de usuário permissões de gravação nos seguintes diretórios:
   * [JBoss-diretory]\standalone\deployment
   * [JBoss-diretory]\standalone\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   > O local de instalação padrão do JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jpatrão/

1. Start o servidor de aplicativos.

**Desativação do servlet de inicialização do Configuration Manager**

O Configuration Manager utilizou um servlet implantado no servidor de aplicativos para executar o carregamento automático dos AEM Forms no banco de dados JEE. Como o Configuration Manager acessa este servlet antes da configuração ser concluída, o acesso a ele não foi protegido para usuários autorizados e ele deve ser desativado depois que você tiver usado o Configuration Manager com êxito para configurar AEM Forms no JEE.

1. Descompacte o arquivo adobe-livecycle-[appserver].ear.
1. Abra o arquivo META-INF/application.xml.
1. Procure a seção adobe-bootstrapper.war:

   ```as3
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

1. Pare o servidor AEM Forms.
1. Comente o adobe-bootstrapper.war e o adobe-lcm-bootstrapper-rediretory. módulos de guerra como se segue:

   ```as3
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
1. compacte o arquivo EAR e implante-o novamente no servidor de aplicativos.
1. Start o servidor AEM Forms.
1. Digite o URL abaixo em um navegador para testar a alteração e garantir que ela não funcione mais.

   https://&lt;localhost>:&lt;porta>/adobe-bootstrapper/bootstrap

**Bloquear o acesso remoto ao Repositório de Confiança**

O Configuration Manager permite que você carregue uma credencial de extensões do Acrobat Reader DC para os AEM Forms no armazenamento confiável JEE. Isso significa que o acesso ao Serviço de Credencial do Repositório de Confiança por protocolos remotos (SOAP e EJB) foi ativado por padrão. Esse acesso não é mais necessário depois de fazer upload das credenciais de Direitos usando o Configuration Manager ou se você decidir usar o Console de administração mais tarde para gerenciar as credenciais.

Você pode desativar o acesso remoto a todos os serviços da Trust Store seguindo as etapas na seção [Desabilitando o acesso remoto não essencial aos serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_remote_access_to_services).

**Desativar todo o acesso anônimo não essencial**

Alguns serviços de servidor de formulários têm operações que podem ser chamadas por um chamador anônimo. Se o acesso anônimo a esses serviços não for necessário, desative-o seguindo as etapas em [Desabilitando o acesso anônimo não essencial aos serviços](https://helpx.adobe.com/aem-forms/6-1/hardening-security/configuring-secure-administration-settings-aem.html#disabling_non_essential_anonymous_access_to_services).

#### Alterar a senha padrão do administrador {#change-the-default-administrator-password}

Quando o AEM Forms no JEE é instalado, uma única conta de usuário padrão é configurada para o usuário Super Administrator/ login-id Administrator com uma senha padrão de *senha*. Você deve alterar essa senha imediatamente usando o Configuration Manager.

1. Digite o seguinte URL em um navegador da Web:

   ```as3
   https://[host name]:[port]/adminui
   ```

   O número padrão da porta é um destes:

   **JBoss:** 8080

   **Servidor WebLogic:** 7001

   **WebSphere:** 9080.

1. No campo Nome **de** usuário, digite `administrator` e, no campo **Senha** , digite `password`.
1. Clique em **Configurações** > Gerenciamento **** do usuário > **Usuários e grupos**.
1. Digite `administrator` o campo **Localizar** e clique em **Localizar**.
1. Clique em **Super Administrador** na lista de usuários.
1. Clique em **Alterar senha** na página Editar usuário.
1. Especifique a nova senha e clique em **Salvar**.

Além disso, é recomendável alterar a senha padrão para o Administrador do CRX executando as seguintes etapas:

1. Faça logon `https://[server]:[port]/lc/libs/granite/security/content/useradmin.html` usando o nome de usuário/senha padrão.
1. Digite Administrador no campo de pesquisa e clique em **Ir**.
1. Selecione **Administrador** no resultado da pesquisa e clique no ícone **Editar** na parte inferior direita da interface do usuário.
1. Especifique a nova senha no campo **Nova senha** e a senha antiga no campo **Sua senha** .
1. Clique no ícone Salvar na parte inferior direita da interface do usuário.

#### Desativar geração WSDL {#disable-wsdl-generation}

A geração WSDL (Web Service Definition Language) deve ser ativada somente para ambientes de desenvolvimento, onde a geração WSDL é usada pelos desenvolvedores para criar seus aplicativos clientes. Você pode optar por desativar a geração WSDL em um ambiente de produção para evitar a exposição dos detalhes internos de um serviço.

1. Digite o seguinte URL em um navegador da Web:

   ```as3
   https://[host name]:[port]/adminui
   ```

1. Clique em **Configurações > Configurações principais do sistema > Configurações**.
1. Desmarque **Ativar WSDL** e clique em **OK**.

### Segurança do servidor de aplicativos {#application-server-security}

A tabela a seguir descreve algumas técnicas para proteger seu servidor de aplicativos depois que os AEM Forms no aplicativo JEE são instalados.

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
   <td><p>Depois de instalar, configurar e implantar AEM Forms no JEE no servidor de aplicativos, você deve desativar o acesso aos consoles administrativos do servidor de aplicativos. Consulte a documentação do servidor de aplicativos para obter detalhes.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Configurações de cookie do servidor de aplicativos</p> </td> 
   <td><p>Os cookies do aplicativo são controlados pelo servidor de aplicativos. Ao implantar o aplicativo, o administrador do servidor de aplicativos pode especificar as preferências de cookie em todo o servidor ou em base específica do aplicativo. Por padrão, as configurações do servidor têm preferência.</p> <p>Todos os cookies de sessão gerados pelo servidor de aplicativos devem incluir o <code>HttpOnly</code> atributo. Por exemplo, ao usar o JBoss Application Server, você pode modificar o elemento SessionCookie para <code>httpOnly="true"</code> no <code>WEB-INF/web.xml</code> arquivo.</p> <p>Você pode restringir cookies a serem enviados usando apenas HTTPS. Como resultado, eles não são enviados sem criptografia por HTTP. Os administradores do servidor de aplicativos devem habilitar cookies seguros para o servidor em uma base global. Por exemplo, ao usar o JBoss Application Server, você pode modificar o elemento do conector para <code>secure=true</code> no <code>server.xml</code> arquivo.</p> <p>Consulte a documentação do servidor de aplicativos para obter mais detalhes sobre as configurações de cookies.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Navegação no diretório</p> </td> 
   <td><p>Quando alguém solicita uma página que não existe ou solicita o nome de um diretor (a string de solicitação termina com uma barra (/)), o servidor de aplicativos não deve retornar o conteúdo desse diretório. Para evitar isso, você pode desativar a navegação no diretório no servidor de aplicativos. Isso deve ser feito para o aplicativo do console de administração e para outros aplicativos em execução no servidor.</p> <p>Para JBoss, defina o valor do parâmetro de inicialização de listagens da <code>DefaultServlet</code> propriedade como <code>false</code> no arquivo web.xml, como mostrado neste exemplo:</p> <p>&lt;servlet&gt;</p> <p>&lt;servlet-name&gt;default&lt;/servlet-name&gt;</p> <p>&lt;classe servlet&gt;</p> <p>org.apache.catalina.servlets.DefaultServlet</p> <p>&lt;/servlet-class&gt;</p> <p>&lt;init-param&gt;</p> <p>&lt;param-name&gt;listagens&lt;/param-name&gt;</p> <p>&lt;param-value&gt;false&lt;/param-value&gt;</p> <p>&lt;/init-param&gt;</p> <p>&lt;load-on-startup&gt;1&lt;/load-on-startup&gt;</p> <p>&lt;/servlet&gt;</p> <p>Para WebSphere, defina a <code>directoryBrowsingEnabled</code> propriedade no arquivo ibm-web-ext.xmi como <code>false</code>.</p> <p>Para WebLogic, defina as propriedades de diretórios de índice no arquivo weblogic.xml como <code>false</code>, conforme mostrado neste exemplo:</p> <p>&lt;container-descriptor&gt;</p> <p>&lt;index-diretory-enabled&gt;false</p> <p>&lt;/index-diretory-enabled&gt;</p> <p>&lt;/container-descriptor&gt;</p> </td> 
  </tr> 
 </tbody> 
</table>

### Segurança do banco de dados {#database-security}

Ao proteger seu banco de dados, você deve implementar as medidas descritas pelo fornecedor do banco de dados. Você deve alocar um usuário do banco de dados com as permissões mínimas exigidas para uso pelos AEM Forms no JEE. Por exemplo, não use uma conta com privilégios de administrador de banco de dados.

No Oracle, a conta de banco de dados usada precisa apenas dos privilégios CONNECT, RESOURCE e CREATE VISUALIZAÇÃO. Para obter requisitos semelhantes em outros bancos de dados, consulte [Preparação para instalar AEM Forms no JEE (Single Server)](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_64).

#### Configurando a segurança integrada para SQL Server no Windows para JBoss {#configuring-integrated-security-for-sql-server-on-windows-for-jboss}

1. Modifique [JBOSS_HOME]\\standalone\configuration\lc_{datasource.xml} para adicionar `integratedSecurity=true` ao URL de conexão, como mostrado neste exemplo:

   ```as3
    jdbc:sqlserver://<serverhost>:<port>;databaseName=<dbname>;integratedSecurity=true
   ```

1. Adicione o arquivo sqljdbc_auth.dll ao caminho dos sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado na instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Modifique a propriedade do serviço JBoss Windows (JBoss para AEM Forms no JEE) para Logon como do Sistema local para uma conta de logon que tenha um banco de dados AEM Forms e um conjunto mínimo de privilégios. Se você estiver executando JBoss na linha de comando em vez de como um serviço do Windows, não será necessário executar essa etapa.
1. Defina Segurança para SQL Server do modo **Misto** para Autenticação **do Windows somente**.

#### Configurando a segurança integrada para o SQL Server no Windows for WebLogic {#configuring-integrated-security-for-sql-server-on-windows-for-weblogic}

1. Start o Console de administração do WebLogic Server digitando o seguinte URL na linha de URL de um navegador da Web:

   ```as3
   https://[host name]:7001/console
   ```

1. Em Centro de alterações, clique em **Bloquear e editar**.
1. Em Estrutura do domínio, clique em *[base_domain]* > **Serviços** > **JDBC** > Fontes **de** dados e, no painel direito, clique em **IDP_DS**.
1. Na tela seguinte, na guia **Configuração** , clique na guia Pool **de** conexão e, na caixa **Propriedades** , digite `integratedSecurity=true`.
1. Em Estrutura do domínio, clique em **[base_domain]** > **Serviços** > **JDBC** > Fontes **de** dados e, no painel direito, clique em **RM_DS**.
1. Na tela seguinte, na guia **Configuração** , clique na guia Pool **de** conexão e, na caixa **Propriedades** , digite `integratedSecurity=true`.
1. Adicione o arquivo sqljdbc_auth.dll ao caminho dos sistemas do Windows no computador que está executando o servidor de aplicativos. O arquivo sqljdbc_auth.dll está localizado na instalação do driver Microsoft SQL JDBC 6.2.1.0.
1. Defina Segurança para SQL Server do modo **Misto** para Autenticação **do Windows somente**.

#### Configurando a segurança integrada para SQL Server no Windows for WebSphere {#configuring-integrated-security-for-sql-server-on-windows-for-websphere}

No WebSphere, você pode configurar a segurança integrada somente quando usa um driver SQL Server JDBC externo, não o driver SQL Server JDBC incorporado ao WebSphere.

1. Faça logon no Console administrativo do WebSphere.
1. Na árvore de navegação, clique em **Recursos** > **JDBC** > Fontes **** de dados e, no painel direito, clique em **IDP_DS**.
1. No painel direito, em Propriedades adicionais, clique em Propriedades **** personalizadas e, em seguida, clique em **Novo**.
1. Na caixa **Nome** , digite `integratedSecurity` e, na caixa **Valor** , digite `true`.
1. Na árvore de navegação, clique em **Recursos** > **JDBC** > Fontes **** de dados e, no painel direito, clique em **RM_DS**.
1. No painel direito, em Propriedades adicionais, clique em Propriedades **** personalizadas e, em seguida, clique em **Novo**.
1. Na caixa **Nome** , digite `integratedSecurity` e, na caixa **Valor** , digite `true`.
1. No computador em que o WebSphere está instalado, adicione o arquivo sqljdbc_auth.dll ao caminho dos sistemas Windows (C:\Windows). O arquivo sqljdbc_auth.dll está no mesmo local que a instalação do driver JDBC 1.2 do Microsoft SQL (o padrão é *[InstallDir]*/sqljdbc_1.2/enu/auth/x86).
1. Selecione **Start** > Painel **de controle >** Serviços **, clique com o botão direito do mouse no serviço Windows para WebSphere (IBM WebSphere Application Server &lt;version> - &lt;node>) e selecione** Propriedades ****.
1. Na caixa de diálogo Propriedades, clique na guia **Logon** .
1. Selecione **Esta conta** e forneça as informações necessárias para definir a conta de logon que deseja usar.
1. Defina Segurança no SQL Server do modo **Misto** para Autenticação **do Windows somente**.

### Protegendo o acesso a conteúdo sigiloso no banco de dados {#protecting-access-to-sensitive-content-in-the-database}

O schema de banco de dados do AEM Forms contém informações confidenciais sobre a configuração do sistema e os processos de negócios e deve estar oculto atrás do firewall. O banco de dados deve ser considerado dentro do mesmo limite de confiança que o servidor de formulários. Para evitar a divulgação de informações e o roubo de dados comerciais, o banco de dados deve ser configurado pelo administrador do banco de dados (DBA) para permitir o acesso somente por administradores autorizados.

Como precaução adicional, você deve considerar o uso de ferramentas específicas do fornecedor do banco de dados para criptografar colunas em tabelas que contêm os seguintes dados:

* Chaves do Documento do Rights Management
* Chave de criptografia do PIN HSM do Repositório de Confiança
* Hash de senha de usuário local

Para obter informações sobre ferramentas específicas do fornecedor, consulte [&quot;Informações de segurança do banco de dados&quot;](https://helpx.adobe.com/aem-forms/6-1/hardening-security/general-security-considerations.html#database_security_information).

### Segurança LDAP {#ldap-security}

Um diretório LDAP (Lightweight Diretory Access Protocol) geralmente é usado por AEM Forms no JEE como fonte de informações de grupo e de usuário corporativo, além de um meio de executar a autenticação de senha. Você deve garantir que seu diretório LDAP esteja configurado para usar SSL (Secure Socket Layer) e que os AEM Forms no JEE estejam configurados para acessar seu diretório LDAP usando sua porta SSL.

#### Negação de serviço LDAP {#ldap-denial-of-service}

Um ataque comum que usa LDAP envolve um invasor que deliberadamente falha na autenticação várias vezes. Isso faz com que o Servidor de Diretório LDAP bloqueie um usuário de todos os serviços confiáveis ao LDAP.

Você pode definir o número de tentativas de falha e o tempo de bloqueio subsequente que o AEM Forms implementa quando um usuário falha repetidamente na autenticação para AEM Forms. No Console de administração, escolha valores baixos. Ao selecionar o número de tentativas de falha, é importante entender que após todas as tentativas, o AEM Forms bloqueia o usuário antes que o Servidor de Diretório LDAP o faça.

#### Definir bloqueio automático de conta {#set-automatic-account-locking}

1. Faça logon no Console de administração.
1. Clique em **Configurações** > Gerenciamento **** do usuário > Gerenciamento **** de domínio.
1. Em Configurações automáticas de bloqueio de conta, defina **Máximo de falhas** de autenticação consecutivas para um número baixo, como 3.
1. Clique em **Salvar**.

### Auditoria e registro {#auditing-and-logging}

O uso correto e seguro de auditoria e registro de aplicativos pode ajudar a garantir que a segurança e outros eventos anômalos sejam rastreados e detectados o mais rápido possível. O uso eficaz de auditoria e registro em um aplicativo inclui itens como rastreamento de logons bem-sucedidos e com falha, bem como eventos-chave do aplicativo, como a criação ou exclusão de registros-chave.

Você pode usar a auditoria para detectar vários tipos de ataques, incluindo estes:

* Ataques de senha de força bruta
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
   <td><p>Defina AEM Forms apropriados nas ACLs (listas de controle de acesso) do arquivo de log JEE.</p> <p>Definir as credenciais apropriadas ajuda a impedir que os invasores excluam os arquivos.</p> <p>As permissões de segurança no diretório do arquivo de log devem ser Controle total para administradores e grupos SYSTEM. A conta de usuário do AEM Forms deve ter somente permissões de Leitura e Gravação.</p> </td> 
  </tr> 
  <tr> 
   <td><p>Redundância do arquivo de log</p> </td> 
   <td><p>Se os recursos permitirem, envie registros para outro servidor em tempo real que não esteja acessível ao invasor (somente gravação) usando o Syslog, Tivoli, Microsoft Operations Manager (MOM) Server ou outro mecanismo.</p> <p>Proteger os registros dessa forma ajuda a impedir a adulteração. Além disso, o armazenamento de registros em um repositório central auxilia na correlação e no monitoramento (por exemplo, se vários servidores de formulários estiverem em uso e um ataque de adivinhação de senha estiver ocorrendo em vários computadores em que cada computador for consultado para obter uma senha).</p> </td> 
  </tr> 
 </tbody> 
</table>

## Configurando AEM Forms no JEE para acesso além da empresa {#configuring-aem-forms-on-jee-for-access-beyond-the-enterprise}

Depois de instalar o AEM Forms com êxito no JEE, é importante manter periodicamente a segurança do seu ambiente. Esta seção descreve as tarefas recomendadas para manter a segurança de seus AEM Forms no servidor de produção JEE.

### Configurar um proxy reverso para acesso à Web {#setting-up-a-reverse-proxy-for-web-access}

Um proxy ** reverso pode ser usado para garantir que um conjunto de URLs para AEM Forms em aplicativos da Web JEE esteja disponível para usuários externos e internos. Essa configuração é mais segura do que permitir que os usuários se conectem diretamente ao servidor de aplicativos em que o AEM Forms no JEE está sendo executado. O proxy reverso executa todas as solicitações HTTP para o servidor de aplicativos que está executando AEM Forms no JEE. Os usuários têm apenas acesso de rede ao proxy reverso e só podem tentar conexões de URL compatíveis com o proxy reverso.

**AEM Forms em URLs raiz JEE para uso com o servidor proxy reverso**

Os seguintes URLs raiz do aplicativo para cada AEM Forms no aplicativo da Web JEE. Você deve configurar seu proxy reverso somente para expor URLs para a funcionalidade do aplicativo da Web que deseja fornecer aos usuários finais.

Determinados URLs são destacados como aplicativos da Web voltados para o usuário final. Evite expor outros URLs para o Configuration Manager para acesso a usuários externos por meio do proxy reverso.

<table> 
 <thead> 
  <tr> 
   <th><p>URL raiz</p> </th> 
   <th><p>Finalidade e/ou aplicação Web associada</p> </th> 
   <th><p>Interface baseada na Web</p> </th> 
   <th><p>Acesso do usuário final</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>/ReaderExtensions/*</p> </td> 
   <td><p>O Acrobat Reader DC extende o aplicativo da Web de usuário final para aplicar direitos de uso a documentos PDF</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/*</p> </td> 
   <td><p>Aplicativo Web de usuário final do Rights Management</p> </td> 
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
   <td><p>Aplicativo da Web de administração do Gerador de PDF</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/espaço de trabalho/*</p> </td> 
   <td><p>Aplicativo Web do usuário final do espaço de trabalho</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/workspace-server/*</p> </td> 
   <td><p>Servlets e serviços de dados da Workspace exigidos pelo aplicativo cliente Workspace</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adobe-bootstrapper/*</p> </td> 
   <td><p>Servlet para carregamento automático de AEM Forms no repositório JEE</p> </td> 
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
   <td><p>URL do serviço Web para todos os serviços do servidor de formulários</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/edc/admin/*</p> </td> 
   <td><p>Aplicativo da Web de administração do Rights Management</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/adminui/*</p> </td> 
   <td><p>home page do Console de administração</p> </td> 
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
   <td><p>Aplicativo Forms IVS para teste e depuração de renderização de formulário</p> </td> 
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
   <td><p>URL REST para o Rights Management</p> </td> 
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
   <td><p>Arquivos de aplicativos da Web para formulários</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServer/GetImage</p> <p>Servlet</p> </td> 
   <td><p>Usado para buscar o JavaScript durante a transformação de HTML</p> </td> 
   <td><p>Não</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/FormServerAdmin/*</p> </td> 
   <td><p>Páginas de administração de formulários</p> </td> 
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
   <td><p>Interface de usuário dos Aplicativos e Serviços</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/WorkspaceAdmin/*</p> </td> 
   <td><p>Páginas de administração do espaço de trabalho</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/rest/*</p> </td> 
   <td><p>Restaurar páginas de suporte</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Não</p> </td> 
  </tr> 
  <tr> 
   <td><p>/CoreSystemConfig/*</p> </td> 
   <td><p>AEM Forms na página de configurações do JEE Core Configuration</p> </td> 
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
   <td><p>Upload e download de documentos que devem ser processados ao acessar pontos de extremidade remotos, pontos de extremidade WSDL SOAP e o SDK Java sobre transporte SOAP ou transporte EJB com documentos HTTP habilitados.</p> </td> 
   <td><p>Sim</p> </td> 
   <td><p>Sim</p> </td> 
  </tr> 
 </tbody> 
</table>

## Proteção contra ataques de falsificação de solicitação entre sites {#protecting-from-cross-site-request-forgery-attacks}

Um ataque CSRF (Cross-Site Request Forgery) explora a confiança que um site tem para o usuário, para transmitir comandos que não são autorizados e não são intencionais pelo usuário. O ataque é configurado incluindo um link ou script em uma página da Web, ou um URL em uma mensagem de email para acessar outro site para o qual o usuário já foi autenticado.

Por exemplo, você pode estar conectado ao Console de administração enquanto navega simultaneamente em outro site. Uma das páginas da Web pode incluir uma tag de imagem HTML com um `src` atributo que público alvo um script do lado do servidor no site da vítima. Ao aproveitar o mecanismo de autenticação de sessão com base em cookies fornecido pelos navegadores da Web, o site de ataque pode enviar solicitações mal-intencionadas para esse script do lado do servidor vítima, mascarando-se como o usuário legítimo. Para obter mais exemplos, consulte [https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF)#Examples).

As seguintes características são comuns ao QREF:

* Envolver sites que dependem da identidade de um usuário.
* Explore a confiança do site nessa identidade.
* Faça com que o navegador do usuário envie solicitações HTTP para um site do público alvo.
* Envolva solicitações HTTP que tenham efeitos colaterais.

AEM Forms no JEE usam o recurso Filtro de Quem indicou para bloquear ataques CSRF. Os termos a seguir são usados nesta seção para descrever o mecanismo de Filtragem de Quem indicou:

* **Quem indicou permitida:** Uma Quem indicou é o endereço da página de origem que envia uma solicitação para o servidor. Para páginas ou formulários JSP, as Quens indicou são normalmente a página anterior no histórico de navegação. A Quem indicou de imagens geralmente são as páginas nas quais as imagens são exibidas. Você pode identificar a Quem indicou que tem acesso permitido aos recursos do servidor adicionando-os à lista de Quem indicou permitida.
* **Exceções de Quem indicou Permitidas:** Talvez você queira restringir o escopo de acesso de uma Quem indicou específica na lista de Quem indicou permitida. Para aplicar essa restrição, você pode adicionar caminhos individuais dessa Quem indicou à lista Exceções de Quem indicou Permitidas. As solicitações provenientes de caminhos na lista Exceções de Quem indicou Permitidas não podem chamar nenhum recurso no servidor de formulários. Você pode definir Exceções de Quem indicou Permitidas para um aplicativo específico e também usar uma lista global de exceções que se aplicam a todos os aplicativos.
* **URIs permitidos:** Esta é uma lista de recursos que devem ser fornecidos sem verificar o Cabeçalho da Quem indicou. Recursos, por exemplo, páginas de ajuda, que não resultam em alterações de estado no servidor, podem ser adicionados a essa lista. Os recursos na lista de URIs permitidos nunca são bloqueados pelo Filtro de Quem indicou, independentemente de quem seja a Quem indicou.
* **Quem indicou nula:** Uma solicitação de servidor que não está associada ou não se origina de uma página da Web pai é considerada uma solicitação de uma Quem indicou Nula. Por exemplo, quando você abre uma nova janela do navegador, digita um endereço e pressione Enter, a Quem indicou enviada para o servidor é nula. Um aplicativo de desktop (.NET ou SWING) que faz uma solicitação HTTP para um servidor da Web, também envia uma Quem indicou Nula para o servidor.

### Filtragem de Quem indicou {#referer-filtering}

O processo de Filtragem de Quem indicou pode ser descrito da seguinte maneira:

1. O servidor de formulários verifica o método HTTP usado para a invocação:

   1. Se for POST, o servidor de formulários executará a verificação do cabeçalho da Quem indicou.
   1. Se for GET, o servidor de formulários ignorará a verificação de Quem indicou, a menos que *CSRF_CHECK_GETS* esteja definido como true, caso em que executa a verificação do cabeçalho da Quem indicou. *CSRF_CHECK_GETS* está especificado no arquivo *web.xml* do seu aplicativo.

1. O servidor de formulários verifica se o URI solicitado existe na lista permitida:

   1. Se o URI for permitido na lista, o servidor aceitará a solicitação.
   1. Se o URI solicitado não estiver listado, o servidor recuperará a Quem indicou da solicitação.

1. Se houver uma Quem indicou na solicitação, o servidor verificará se é uma Quem indicou permitida. Se for permitido, o servidor verifica se há uma Exceção de Quem indicou:

   1. Se for uma exceção, a solicitação será bloqueada.
   1. Se não for uma exceção, a solicitação será transmitida.

1. Se não houver Quem indicou na solicitação, o servidor verificará se uma Quem indicou Nula é permitida:

   1. Se uma Quem indicou Nula for permitida, a solicitação será transmitida.
   1. Se uma Quem indicou Nula não for permitida, o servidor verificará se o URI solicitado é uma exceção para a Quem indicou Nulo e lidará com a solicitação de acordo.

### Gerenciamento da filtragem de Quens indicou {#managing-referer-filtering}

AEM Forms no JEE fornecem um Filtro de Quem indicou para especificar Quens indicou que podem acessar os recursos do servidor. Por padrão, o filtro de Quem indicou não filtra solicitações que usam um método HTTP seguro, por exemplo, GET, a menos que *CSRF_CHECK_GETS* esteja definido como true. Se o número da porta para uma entrada de Quem indicou permitida for definido como 0, os AEM Forms no JEE permitirão todas as solicitações com Quem indicou desse host, independentemente do número da porta. Se nenhum número de porta for especificado, somente as solicitações da porta padrão 80 (HTTP) ou da porta 443 (HTTPS) serão permitidas. A Filtragem de Quem indicou é desativada se todas as entradas na lista de Quem indicou Permitida forem excluídas.

Quando você instala os Serviços de Documento pela primeira vez, a lista de Quem indicou permitida é atualizada com o endereço do servidor no qual os Serviços de Documento estão instalados. As entradas para o servidor incluem o nome do servidor, o endereço IPv4, o endereço IPv6 se IPv6 estiver ativado, o endereço de loopback e uma entrada de host local. Os nomes adicionados à lista de Quem indicou Permitida são retornados pelo sistema operacional Host. Por exemplo, um servidor com um endereço IP de 10.40.54.187 incluirá as seguintes entradas: `https://server-name:0, https://10.40.54.187:0, https://127.0.0.1:0, http://localhost:0`. Para qualquer nome não qualificado retornado pelo sistema operacional Host (nomes que não têm endereço IPv4, endereço IPv6 ou nome de domínio qualificado), a lista permitida não é atualizada. Modifique a lista de Quem indicou permitida para adequá-la ao seu ambiente comercial. Não implante o servidor de formulários no ambiente de produção com a lista de Quem indicou permitida padrão. Depois de modificar qualquer Quem indicou, Exceções de Quem indicou ou URIs Permitidas, certifique-se de reiniciar o servidor para que as alterações entrem em vigor.

**Gerenciando lista de Quem indicou permitida**

Você pode gerenciar a lista de Quem indicou Permitida na Interface de Gerenciamento de Usuário do Console de Administração. A interface de gerenciamento de usuários oferece a funcionalidade de criar, editar ou excluir a lista. Consulte a seção * [Impedindo ataques](/help/forms/using/admin-help/preventing-csrf-attacks.md)CSRF* da ajuda *da* administração para obter mais informações sobre como trabalhar com a lista de Quem indicou permitida.

**Gerenciando exceções de Quem indicou permitidas e listas de URI permitidas**

AEM Forms no JEE fornecem APIs para gerenciar a lista de Exceção de Quem indicou Permitida e a lista de URI Permitida. Você pode usar essas APIs para recuperar, criar, editar ou excluir a lista. Veja a seguir uma lista de APIs disponíveis:

* createAllowedURIsList
* getAllowedURIsList
* updateAllowedURIsList
* deleteAllowedURIsList
* addAllowedRefererExceptions
* getAllowedRefererExceptions
* updateAllowedRefererExceptions
* deleteAllowedRefererExceptions

Consulte os AEM Forms* da Referência API JEE* para obter mais informações sobre as APIs.

Use a lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** para Exceções de Quem indicou Permitidas no nível global, isto é, para definir exceções aplicáveis a todos os aplicativos. Esta lista contém apenas URIs com um caminho absoluto (por exemplo, `/index.html`) ou um caminho relativo (por exemplo, `/sample/`). Também é possível anexar uma expressão regular ao final de um URI relativo, por exemplo, `/sample/(.)*`.

A ID de lista ***LC_GLOBAL_ALLOWED_REFERER_EXCEPTION*** é definida como uma constante na `UMConstants` classe da `com.adobe.idp.um.api` namespace, encontrada em `adobe-usermanager-client.jar`. Você pode usar as APIs do AEM Forms para criar, modificar ou editar essa lista. Por exemplo, para criar a lista Exceções de Quem indicou Permitidas Globais, use:

```as3
addAllowedRefererExceptions(UMConstants.LC_GLOBAL_ALLOWED_REFERER_EXCEPTION, Arrays.asList("/index.html", "/sample/(.)*"))
```

Use a lista ***CSRF_ALLOWED_REFERER_EXCEPTIONS*** para obter exceções específicas do aplicativo.

**Desativação do filtro de Quem indicou**

No evento em que o Filtro de Quem indicou bloqueia completamente o acesso ao servidor de formulários e não é possível editar a lista de Quem indicou Permitida, você pode atualizar o script de inicialização do servidor e desativar a Filtragem de Quem indicou.

Inclua o argumento `-Dlc.um.csrffilter.disabled=true` JAVA no script de inicialização e reinicie o servidor. Certifique-se de excluir o argumento JAVA depois de reconfigurar apropriadamente a lista de Quem indicou Permitida.

**Filtragem de Quem indicou para arquivos WAR personalizados**

Você pode ter criado arquivos WAR personalizados para trabalhar com AEM Forms no JEE a fim de atender às suas necessidades comerciais. Para ativar a Filtragem de Quem indicou para seus arquivos WAR personalizados, inclua ***adobe-usermanager-client.jar*** no caminho de classe para a WAR e inclua uma entrada de filtro no arquivo* web.xml* com os seguintes parâmetros:

**CSRF_CHECK_GETS** controla a verificação de Quem indicou em solicitações GET. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua este parâmetro somente se desejar filtrar suas solicitações GET.

**CSRF_ALLOWED_REFERER_EXCEPTIONS** é a ID da lista de Exceções de Quem indicou Permitidas. O Filtro de Quem indicou impede que solicitações originárias de Quens indicou na lista identificada pela ID da lista cheguem a qualquer recurso no servidor de formulários.

**CSRF_ALLOWED_URIS_LISTA_NAME** é a ID da lista de URIs permitidos. O Filtro de Quem indicou não bloqueia solicitações de nenhum dos recursos na lista identificada pela ID da lista, independentemente do valor do cabeçalho da Quem indicou na solicitação.

**CSRF_ALLOW_NULL_REFERER** controla o comportamento do Filtro de Quem indicou quando a Quem indicou é nula ou não está presente. Se esse parâmetro não estiver definido, o valor padrão será definido como false. Inclua esse parâmetro somente se desejar permitir Quens indicou Nulas. A permissão de quens indicou nulas pode permitir alguns tipos de ataques de Permissão de Solicitação entre Sites.

**CSRF_NULL_REFERER_EXCEPTIONS** é uma lista dos URIs para os quais uma verificação de Quem indicou não é realizada quando a Quem indicou é nula. Esse parâmetro é ativado somente quando *CSRF_ALLOW_NULL_REFERER* está definido como falso. Separe vários URIs na lista com uma vírgula.

Veja a seguir um exemplo da entrada de filtro no arquivo *web.xml* para um arquivo ***SAMPLE*** WAR:

```as3
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

Se as solicitações legítimas do servidor estiverem sendo bloqueadas pelo filtro CSRF, tente uma das seguintes opções:

* Se a solicitação rejeitada tiver um cabeçalho de Quem indicou, considere cuidadosamente adicioná-la à lista de Quem indicou permitida. Adicione somente Quem indicou em que você confia.
* Se a solicitação rejeitada não tiver um cabeçalho de Quem indicou, modifique o aplicativo cliente para incluir um cabeçalho de Quem indicou.
* Se o cliente puder trabalhar em um navegador, experimente esse modelo de implantação.
* Como último recurso, você pode adicionar o recurso à lista URIs permitidos. Esta não é uma configuração recomendada.

## Configuração de rede segura {#secure-network-configuration}

Esta seção descreve os protocolos e portas exigidos pelos AEM Forms no JEE e fornece recomendações para a implantação de AEM Forms no JEE em uma configuração de rede segura.

### Protocolos de rede usados por AEM Forms no JEE {#network-protocols-used-by-aem-forms-on-jee}

Quando você configura uma arquitetura de rede segura conforme descrito na seção anterior, os seguintes protocolos de rede são necessários para a interação entre AEM Forms no JEE e outros sistemas em sua rede corporativa.

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
     <li><p>O navegador exibe o Configuration Manager e os aplicativos da Web do usuário final</p> </li> 
     <li><p>Todas as conexões SOAP</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>SOAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Aplicativos cliente de serviço da Web, como aplicativos .NET</p> </li> 
     <li><p>O Adobe Reader® usa SOAP para AEM Forms em serviços Web de servidor JEE</p> </li> 
     <li><p>Aplicativos Adobe Flash® usam SOAP para serviços da Web de servidores de formulários</p> </li> 
     <li><p>AEM Forms em chamadas JEE SDK quando usadas no modo SOAP</p> </li> 
     <li><p>ambiente de design do Workbench</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>RMI</p> </td> 
   <td><p>AEM Forms em chamadas JEE SDK quando usadas no modo Enterprise JavaBeans (EJB)</p> </td> 
  </tr> 
  <tr> 
   <td><p>IMAP / POP3</p> </td> 
   <td> 
    <ul> 
     <li><p>Entrada por email para um serviço (terminal de email)</p> </li> 
     <li><p>Notificações de tarefa do usuário por email</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>E/S de arquivo UNC</p> </td> 
   <td><p>AEM Forms no monitoramento JEE de pastas monitoradas para entrada em um serviço (ponto de extremidade da pasta monitorada)</p> </td> 
  </tr> 
  <tr> 
   <td><p>LDAP</p> </td> 
   <td> 
    <ul> 
     <li><p>Sincronizações de informações de grupo e usuário organizacional em um diretório</p> </li> 
     <li><p>Autenticação LDAP para usuários interativos</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>JDBC</p> </td> 
   <td> 
    <ul> 
     <li><p>Chamadas de Query e procedimento feitas para um banco de dados externo durante a execução de um processo usando o serviço JDBC</p> </li> 
     <li><p>AEM Forms de acesso interno no repositório JEE</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>WebDAV</p> </td> 
   <td><p>Permite a navegação remota dos AEM Forms no repositório em tempo de design do JEE (formulários, fragmentos etc.) por qualquer cliente WebDAV</p> </td> 
  </tr> 
  <tr> 
   <td><p>AMF</p> </td> 
   <td><p>Aplicativos Adobe Flash, onde AEM Forms em serviços de servidor JEE são configurados com um terminal Remoting</p> </td> 
  </tr> 
  <tr> 
   <td><p>JMX</p> </td> 
   <td><p>AEM Forms no JEE expõe MBeans para monitoramento usando JMX</p> </td> 
  </tr> 
 </tbody> 
</table>

### Portas para servidores de aplicativos {#ports-for-application-servers}

Esta seção descreve as portas padrão (e intervalos de configuração alternativos) para cada tipo de servidor de aplicativos suportado. Essas portas devem ser ativadas ou desativadas no firewall interno, dependendo da funcionalidade de rede que você deseja permitir para clientes que se conectam ao servidor de aplicativos que executam AEM Forms no JEE.

>[!NOTE]
>
>Por padrão, o servidor expõe vários MBeans JMX na namespace adobe.com. Somente as informações úteis para o monitoramento de integridade do servidor são expostas. No entanto, para impedir a divulgação de informações, você deve impedir que os chamadores em uma rede não confiável pesquisem MBeans JMX e acessem métricas de integridade.

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
   <td><p>Acesso a aplicativos da Web</p> </td> 
   <td><p>[JBOSS_Root]/standalone/configuration/lc_[database].xml</p> <p>Porta do conector HTTP/1.1 8080</p> <p>Porta do conector AJP 1.3 8009</p> <p>Porta do conector SSL/TLS 8443</p> </td> 
  </tr> 
  <tr> 
   <td><p>Suporte CORBA</p> </td> 
   <td><p>[Raiz JBoss]/server/all/conf/jacorb.properties</p> <p>OAPort 3528</p> <p>OASSLPort 3529</p> </td> 
  </tr> 
 </tbody> 
</table>

**Portas WebLogic**

<table> 
 <thead> 
  <tr> 
   <th><p>Propósito</p> </th> 
   <th><p>Porta</p> </th> 
  </tr> 
 </thead> 
 <tbody>
  <tr> 
   <td><p>Acesso a aplicativos da Web</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do servidor de administração: o padrão é 7001</p> </li> 
     <li><p>Porta de escuta SSL do servidor de administração: o padrão é 7002</p> </li> 
     <li><p>Porta configurada para Servidor gerenciado, por exemplo 8001</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>As portas de administração WebLogic não são necessárias para acesso a AEM Forms no JEE</p> </td> 
   <td> 
    <ul> 
     <li><p>Porta de escuta do Servidor Gerenciado: Configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta SSL do Servidor Gerenciado: Configurável de 1 a 65534</p> </li> 
     <li><p>Porta de escuta do Gerenciador de nós: o padrão é 5556</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

**Portas WebSphere**

Para obter informações sobre portas WebSphere exigidas pelo AEM Forms no JEE, vá para a configuração de número de porta na interface do usuário do WebSphere Application Server.

### Configuração do SSL {#configuring-ssl}

Referindo-se à arquitetura física descrita nos [AEM Forms de seção sobre a arquitetura](hardening-aem-forms-jee-environment.md#aem-forms-on-jee-physical-architecture)física JEE, configure o SSL para todas as conexões que você planeja usar. Especificamente, todas as conexões SOAP devem ser conduzidas por SSL para evitar a exposição das credenciais do usuário em uma rede.

Para obter instruções sobre como configurar o SSL em JBoss, WebLogic e WebSphere, consulte &quot;Configuração do SSL&quot; na ajuda [](https://www.adobe.com/go/learn_aemforms_admin_64)administrativa.

### Configuração do redirecionamento SSL {#configuring-ssl-redirect}

Depois de configurar seu servidor de aplicativos para suportar SSL, você deve garantir que todo o tráfego HTTP para aplicativos e serviços seja forçado a usar a porta SSL.

Para configurar o redirecionamento SSL para WebSphere ou WebLogic, consulte a documentação do servidor de aplicativos.

1. Abra o prompt de comando, navegue até o diretório /JBOSS_HOME/standalone/configuration e execute o seguinte comando:

   `keytool -genkey -alias jboss7 -keyalg RSA -keystore server.keystore -validity 10950`

1. Abra o arquivo JBOSS_HOME/standalone/configuration/standalone.xml para edição.

   Depois do elemento &lt;subsistema xmlns=&quot;urn:jensor:domain:web:1.1&quot; native=&quot;false&quot; default-virtual-server=&quot;default-host&quot;>, adicione os seguintes detalhes:

   &lt;nome do conector=&quot;https&quot; protocol=&quot;HTTP/1.1&quot; schema=&quot;https&quot; socket-binding=&quot;https&quot; enabled=&quot;true&quot; secure=&quot;true&quot;/>

1. Adicione o seguinte código no elemento do conector https:

   ```
   <connector name="https" protocol="HTTP/1.1" scheme="https" socket-binding="https" secure="true" enabled="true"> 
    <ssl name="jboss7_ssl" key-alias="jboss71" password="Tibco321" certificate-key-file="../standalone/configuration/server.keystore" protocol="TLSv1"/> 
    </connector>
   ```

   Salve e feche o arquivo standalone.xml.

## Recomendações de segurança específicas do Windows {#windows-specific-security-recommendations}

Esta seção contém recomendações de segurança específicas ao Windows quando usadas para executar AEM Forms no JEE.

### Contas do Serviço JBoss {#jboss-service-accounts}

Por padrão, os AEM Forms na instalação chave na JEE configuram uma conta de serviço usando a conta Sistema local. A conta de utilizador integrada da rede local tem um elevado nível de acessibilidade; faz parte do grupo Administradores. Se uma identidade de processo de trabalho for executada como a conta de usuário do Sistema local, esse processo de trabalho terá acesso total ao sistema inteiro.

#### Execute o servidor de aplicativos usando uma conta não administrativa {#run-the-application-server-using-a-non-administrative-account}

1. No Microsoft Management Console (MMC), crie um usuário local para que o serviço do servidor de formulários faça logon como:

   * Selecione **Usuário não pode alterar a senha**.
   * Na guia **Membro de** , verifique se o grupo Usuários está listado.

1. Selecione **Configurações** > Ferramentas **** administrativas > **Serviços**.
1. Duplo clique no serviço do servidor de aplicativos e pare o serviço.
1. Na guia **Logon** , selecione **Esta conta**, procure a conta de usuário que você criou e digite a senha da conta.
1. Na janela Configurações de segurança local, em Atribuição de direitos de usuário, atribua os seguintes direitos à conta de usuário na qual o servidor de formulários está sendo executado:

   * Negar logon por meio dos Serviços de Terminal
   * Negar logon no local
   * Fazer logon como Serviço (já deve estar definido)

1. Atribua à nova conta de usuário permissões de modificação nos seguintes diretórios:
   * **Diretório** GDS: O local do diretório GDS é configurado manualmente durante o processo de instalação do AEM Forms. Se a configuração de localização permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos em `[JBoss root]/server/[type]/svcnative/DocumentStorage`
   * **Diretório** CRX-Repository: O local padrão é `[AEM-Forms-installation-location]\crx-repository`
   * **AEM Forms de diretórios** temporários:
      * (Windows) Caminho TMP ou TEMP conforme definido nas variáveis do ambiente
      * (AIX, Linux ou Solaris) Diretório inicial do usuário conectadoEm sistemas baseados em UNIX, um usuário não raiz pode usar o seguinte diretório como diretório temporário:
      * (Linux) /var/tmp ou /usr/tmp
      * (AIX) /tmp ou /usr/tmp
      * (Solaris) /var/tmp ou /usr/tmp
1. Atribua à nova conta de usuário permissões de gravação nos seguintes diretórios:
   * [JBoss-diretory]\standalone\deployment
   * [JBoss-diretory]\standalone\
   * [JBoss-diretory]\bin\

   >[!NOTE]
   >
   > O local de instalação padrão do JBoss Application Server:
   > * Windows: C:\Adobe\Adobe_Experience_Manager_Forms\jboss
   > * Linux: /opt/jpatrão/.


1. Start do serviço do servidor de aplicativos.

### Segurança do sistema de arquivos {#file-system-security}

O AEM Forms no JEE usa o sistema de arquivos das seguintes maneiras:

* Armazena arquivos temporários que são usados durante o processamento da entrada e saída do documento
* Armazena arquivos no repositório de arquivamento global que são usados para suportar os componentes da solução instalados
* Pastas monitoradas armazenam arquivos descartados usados como entrada em um serviço a partir de um local de pasta do sistema de arquivos

Ao usar pastas monitoradas como uma forma de enviar e receber documentos com um serviço de servidor de formulários, tome precauções extras com a segurança do sistema de arquivos. Quando um usuário solta o conteúdo na pasta assistida, ele é exposto pela pasta assistida. Nesse caso, o serviço não autentica o usuário final real. Em vez disso, ele depende da segurança de nível de ACL e Compartilhamento para ser definida no nível da pasta para determinar quem pode chamar efetivamente o serviço.

## Recomendações de segurança específicas para JBoss {#jboss-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos que são específicas ao JBoss 7.0.6 quando usadas para executar AEM Forms no JEE.

### Desativar o Console de Gerenciamento JBoss e o Console JMX {#disable-jboss-management-console-and-jmx-console}

O acesso ao console de gerenciamento JBoss e ao console JMX já está configurado (o monitoramento JMX está desativado) quando você instala AEM Forms no JEE em JBoss usando o método de instalação chave na mão. Se você estiver usando seu próprio JBoss Application Server, verifique se o acesso ao console de gerenciamento JBoss e ao console de monitoramento JMX estão protegidos. O acesso ao console de monitoramento JMX é definido no arquivo de configuração JBoss chamado jmx-invoker-service.xml.

### Desativar a navegação no diretório {#disable-directory-browsing}

Depois de fazer logon no Console de administração, é possível navegar na lista de diretórios do console modificando o URL. Por exemplo, se você alterar o URL para um dos seguintes URLs, uma listagem de diretório poderá ser exibida:

```as3
https://<servername>:8080/adminui/secured/ 
https://<servername>:8080/um/
```

## Recomendações de segurança específicas do WebLogic {#weblogic-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebLogic 9.1 ao executar AEM Forms no JEE.

### Desativar a navegação no diretório {#disable_directory_browsing-1}

Defina as propriedades de diretórios de índice no arquivo weblogic.xml como `false`, como mostra este exemplo:

```as3
<container-descriptor> 
    <index-directory-enabled>false 
    </index-directory-enabled> 
</container-descriptor>
```

### Habilitar Porta SSL do WebLogic {#enable-weblogic-ssl-port}

Por padrão, o WebLogic não ativa a Porta de escuta SSL padrão, 7002. Ative esta porta no Console de Administração do WebLogic Server antes de configurar o SSL.

## Recomendações de segurança específicas do WebSphere {#websphere-specific-security-recommendations}

Esta seção contém recomendações de configuração do servidor de aplicativos para proteger o WebSphere executando AEM Forms no JEE.

### Desativar a navegação no diretório {#disable_directory_browsing-2}

Defina a `directoryBrowsingEnabled` propriedade no arquivo ibm-web-ext.xml como `false`.

### Habilitar a segurança administrativa do WebSphere {#enable-websphere-administrative-security}

1. Faça logon no Console administrativo do WebSphere.
1. Na árvore de navegação, vá até **Segurança** > Segurança **global**
1. Selecione **Ativar segurança** administrativa.
1. Desmarque **Ativar segurança** do aplicativo e **Usar segurança** Java 2.
1. Clique em **OK** ou em **Aplicar**.
1. Na caixa **Mensagens** , clique em **Salvar diretamente na configuração** mestre.