---
title: Configuração do SSL para WebSphere Application Server
seo-title: Configuração do SSL para WebSphere Application Server
description: Saiba como configurar o SSL para o WebSphere Application Server.
seo-description: Saiba como configurar o SSL para o WebSphere Application Server.
uuid: f939a806-346e-41e0-b2c0-6d0ba83f8f6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7c0efcb3-5b07-4090-9119-b7318c8b7980
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---


# Configuração do SSL para WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

Esta seção inclui as seguintes etapas para configurar o SSL com seu IBM WebSphere Application Server.

## Criação de uma conta de usuário local no WebSphere {#creating-a-local-user-account-on-websphere}

Para habilitar o SSL, o WebSphere precisa de acesso a uma conta de usuário no registro de usuário local do SO que tenha permissão para administrar o sistema:

* (Windows) Crie um novo usuário do Windows que faça parte do grupo Administradores e tenha o privilégio de agir como parte do sistema operacional. (Consulte [Criar um usuário do Windows para WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) O usuário pode ser um usuário raiz ou outro usuário que tenha privilégios de raiz. Ao ativar o SSL no WebSphere, use a identificação do servidor e a senha desse usuário.

### Criar um usuário Linux ou UNIX para WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Faça logon como o usuário raiz.
1. Crie um usuário inserindo o seguinte comando em um prompt de comando:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Defina a senha do novo usuário digitando `passwd` no prompt de comando.
1. (Linux e Solaris) Crie um arquivo de senha de sombra digitando `pwconv` (sem parâmetros) no prompt de comando.

   >[!NOTE]
   >
   >(Linux e Solaris) Para que o registro de segurança do SO local do WebSphere Application Server funcione, um arquivo de senha de sombra deve existir. O arquivo de senha de sombra geralmente é nomeado **/etc/shadow** e é baseado no arquivo /etc/passwd. Se o arquivo de senha de sombra não existir, ocorrerá um erro após habilitar a segurança global e configurar o registro do usuário como SO local.

1. Abra o arquivo de grupo do diretório /etc em um editor de texto.
1. Adicione ao `root` grupo o usuário que você criou na etapa 2.
1. Salve e feche o arquivo.
1. (UNIX com SSL ativado) Start e parado o WebSphere como o usuário raiz.

### Criar um usuário do Windows para WebSphere {#create-a-windows-user-for-websphere}

1. Faça logon no Windows usando uma conta de usuário administrador.
1. Selecione **Start > Painel de controle do Campaign > Ferramentas administrativas > Gerenciamento do computador > Usuários e grupos** locais.
1. Clique com o botão direito do mouse em Usuários e selecione **Novo usuário**.
1. Digite um nome de usuário e senha nas caixas apropriadas e digite quaisquer outras informações necessárias nas caixas restantes.
1. Desmarque **Usuário deve alterar a senha no próximo logon**, clique em **Criar** e em **Fechar**.
1. Clique em **Usuários**, clique com o botão direito do mouse no usuário que acabou de criar e selecione **Propriedades**.
1. Clique na guia **Membro de** e, em seguida, clique em **Adicionar**.
1. Na caixa Digitar os nomes dos objetos a serem selecionados, digite `Administrators`, clique em Verificar nomes para garantir que o nome do grupo esteja correto.
1. Clique em **OK** e, em seguida, clique em **OK** novamente.
1. Selecione **Start > Painel de controle do Campaign > Ferramentas administrativas > Política de segurança local > Políticas** locais.
1. Clique em Atribuição de direitos de usuário, clique com o botão direito do mouse em Agir como parte do sistema operacional e selecione Propriedades.
1. Click **Add User or Group**.
1. Na caixa Digitar os nomes dos objetos a serem selecionados, digite o nome do usuário criado na etapa 4, clique em **Verificar nomes** para garantir que o nome esteja correto e clique em **OK**.
1. Clique em **OK** para fechar a caixa de diálogo Agir como parte da caixa de diálogo Propriedades do sistema operacional.

### Configurar o WebSphere para usar o usuário recém-criado como Administrador {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Verifique se o WebSphere está em execução.
1. No Console administrativo do WebSphere, selecione **Segurança > Segurança** global.
1. Em Segurança administrativa, selecione Funções **de usuário** administrativas.
1. Clique em Adicionar e faça o seguinte:

   1. Tipo **&amp;ast;** na caixa de pesquisa e clique em pesquisar.
   1. Clique em **Administrador** em funções.
   1. Adicione o usuário recém-criado à função Mapeado e mapeie-o para Administrador.

1. Click **OK** and save your changes.
1. Reinicie o perfil WebSphere.

## Habilitar segurança administrativa {#enable-administrative-security}

1. No Console administrativo do WebSphere, selecione **Segurança > Segurança** global.
1. Clique em Assistente **de configuração de** segurança.
1. Verifique se a caixa de seleção **Ativar segurança** do aplicativo está ativada. Clique em **Avançar**.
1. Selecione Repositórios **Federados** e clique em **Avançar**.
1. Especifique as credenciais que deseja definir e clique em **Avançar**.
1. Click **Finish**.
1. Reinicie o perfil WebSphere.

   O WebSphere será start usando o armazenamento de chaves padrão e o armazenamento de confiança.

## Habilitar SSL (chave personalizada e Truststore) {#enable-ssl-custom-key-and-truststore}

Truststores e keystores podem ser criados usando o utilitário ikeyman ou o console de administração. Para que o teclado funcione corretamente, verifique se o caminho de instalação do WebSphere não contém parênteses.

1. No Console administrativo do WebSphere, selecione **Segurança > Certificado SSL e gerenciamento** de chaves.
1. Clique em **Keystores e certificados** em Itens relacionados.
1. Na lista suspensa **Principais usos** do armazenamento, verifique se **SSL Keystores** está selecionado. Clique em **Novo**.
1. Digite um nome lógico e uma descrição.
1. Especifique o caminho onde deseja que o armazenamento de chaves seja criado. Se você já tiver criado um armazenamento de chaves por meio do teclado, especifique o caminho para o arquivo de armazenamento de chaves.
1. Especifique e confirme a senha.
1. Escolha o tipo de armazenamento de chaves e clique em **Aplicar**.
1. Salve a configuração principal.
1. Clique em Certificado **** pessoal.
1. Se você já tiver adicionado um armazenamento de chaves usando o teclado, seu certificado será exibido. Caso contrário, é necessário adicionar um novo certificado autoassinado executando as seguintes etapas:

   1. Select **Create > Self-signed Certificate**.
   1. Especifique os valores apropriados no formulário de certificado. Certifique-se de manter Alias e nome comum como nome de domínio totalmente qualificado da máquina.
   1. Clique em **Aplicar**.

1. Repita as etapas de 2 a 10 para criar uma loja confiável.

## Aplicar o armazenamento de chaves e a loja de confiança personalizados ao servidor {#apply-custom-keystore-and-truststore-to-the-server}

1. No Console administrativo do WebSphere, selecione **Segurança > Certificado SSL e gerenciamento** de chaves.
1. Clique em **Gerenciar configuração** de segurança do terminal. O mapa de topologia local é aberto.
1. Em Entrada, selecione filho direto de nós.
1. Em Itens relacionados, selecione configurações **** SSL.
1. Selecione **NodeDeafultSSLSetting**.
1. Nas listas suspensas nome da Truststore e nome da keystore, selecione a Truststore personalizada e a keystore que criou.
1. Clique em **Aplicar**.
1. Salve a configuração principal.
1. Reinicie o perfil WebSphere.

   Seu perfil agora é executado com configurações SSL personalizadas e seu certificado.

## Habilitar suporte para AEM nativos de formulários {#enabling-support-for-aem-forms-natives}

1. No Console administrativo do WebSphere, selecione **Segurança > Segurança** global.
1. Na seção Autenticação, expanda a segurança **** RMI/IIOP e clique em Comunicações **de entrada** CSIv2.
1. Certifique-se de que o suporte a **SSL** esteja selecionado na lista suspensa Transporte.
1. Reinicie o perfil WebSphere.

## Configuração do WebSphere para converter URLs que começam com https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Para converter um URL que comece com https, adicione um certificado de assinante para esse URL ao servidor WebSphere.

**Criar um certificado de signatário para um site habilitado para https**

1. Verifique se o WebSphere está em execução.
1. No Console administrativo do WebSphere, navegue até Certificados do assinante e clique em Segurança > Certificado SSL e Gerenciamento de chaves > Repositórios de chaves e certificados > NodeDefaultTrustStore > Certificados do assinante.
1. Clique em Recuperar da porta e execute estas tarefas:

   * Na caixa Host, digite o URL. For example, type `www.paypal.com`.
   * Na caixa Porta, digite `443`. Esta porta é a porta SSL padrão.
   * Na caixa Alias, digite um alias.

1. Clique em Recuperar informações do assinante e verifique se as informações foram recuperadas.
1. Clique em Aplicar e em Salvar.

A conversão de HTML em PDF do site cujo certificado é adicionado agora funcionará a partir do serviço Gerar PDF.

>[!NOTE]
>
>Para que um aplicativo se conecte a sites SSL de dentro do WebSphere, é necessário um certificado de assinante. Ele é usado pelo Java Secure Socket Extensions (JSSE) para validar certificados que o lado remoto da conexão enviado durante um handshake SSL.

## Configuração de portas dinâmicas {#configuring-dynamic-ports}

O IBM WebSphere não permite várias chamadas para ORB.init() quando o Global Security está ativado. Você pode ler sobre a restrição permanente em https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Execute as seguintes etapas para definir a porta como dinâmica e resolver o problema:

1. No Console administrativo do WebSphere, selecione **Servidores** > Tipos **de** servidor > Servidor **de aplicativos** WebSphere.
1. Na seção Preferências, selecione o servidor.
1. Na guia **Configuração** , na seção **Comunicações** , expanda **Portas** e clique em **Detalhes**.
1. Clique nos seguintes nomes de porta, altere o número **da** porta para 0 e clique em **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurar o arquivo sling.properties {#configure-the-sling-properties-file}

1. Abra o arquivo `[aem-forms_root]`\crx-repository\launchpad\sling.properties para edição.
1. Localize a `sling.bootdelegation.ibm` propriedade e adicione- `com.ibm.websphere.ssl.*`a ao seu campo de valor. O campo atualizado tem a seguinte aparência:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Salve o arquivo e reinicie o servidor.

