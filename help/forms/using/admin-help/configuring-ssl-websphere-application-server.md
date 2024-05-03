---
title: Configuração do SSL para o WebSphere Application Server
description: Saiba como configurar o SSL para o WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b0786b52-879e-4a24-9cc9-bd9dcb2473cc
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 0%

---

# Configuração do SSL para o WebSphere Application Server {#configuring-ssl-for-websphere-application-server}

Esta seção inclui as seguintes etapas para configurar o SSL com seu IBM WebSphere Application Server.

## Criação de uma conta de usuário local no WebSphere {#creating-a-local-user-account-on-websphere}

Para habilitar o SSL, o WebSphere precisa acessar uma conta de usuário no registro de usuário do SO local que tenha permissão para administrar o sistema:

* (Windows) Crie um usuário do Windows que faça parte do grupo Administradores e tenha o privilégio de atuar como parte do sistema operacional. (Consulte [Criar um usuário do Windows para o WebSphere](configuring-ssl-websphere-application-server.md#create-a-windows-user-for-websphere).)
* (Linux, UNIX) O usuário pode ser um usuário root ou outro usuário que tenha privilégios root. Ao habilitar o SSL no WebSphere, use a identificação e a senha do servidor desse usuário.

### Criar um usuário Linux ou UNIX para o WebSphere {#create-a-linux-or-unix-user-for-websphere}

1. Faça logon como o usuário raiz.
1. Criar um usuário inserindo o seguinte comando em um prompt de comando:

   * (Linux e Sun Solaris) `useradd`
   * (IBM AIX) `mkuser`

1. Defina o senha do novo usuário inserindo no prompt de `passwd` comando.
1. (Linux e Solaris) Criar um arquivo de senha sombra inserindo `pwconv` (sem parâmetros) no prompt de comando.

   >[!NOTE]
   >
   >(Linux e Solaris) Para que o registro de segurança do sistema operacional local do WebSphere Application Server funcione, um arquivo de senha sombra deve existir. O arquivo de senha sombra geralmente é nomeado **/etc/shadow** e é baseado no arquivo /etc/passwd. Se a sombra senha arquivo não existir, ocorrerá um erro após ativar a segurança global e configurar o registro de usuário como sistema operacional local.

1. Abra o arquivo de grupo do diretório /etc em um editor de texto.
1. Adicione a usuário criada na etapa 2 à `root` grupo.
1. Salvar e fechar o arquivo.
1. (UNIX com SSL ativado) Inicie e interrompa o WebSphere como o usuário raiz.

### Criar um usuário do Windows para o WebSphere {#create-a-windows-user-for-websphere}

1. Faça logon no Windows usando uma conta de usuário administrador.
1. Selecionar **Iniciar > Painel de controle > Ferramentas administrativas > Gerenciamento do computador > Usuários e grupos locais**.
1. Clique com o botão direito do mouse em Usuários e selecione **Novo usuário**.
1. Digite um nome de usuário e senha nas caixas apropriadas e digite quaisquer outras informações necessárias nas caixas restantes.
1. Desmarcar **O Usuário Deve Alterar A Senha No Próximo Logon**, clique em **Criar** e clique em **Fechar**.
1. Clique em **Usuários**, clique com o botão direito do mouse no usuário criado e selecione **Propriedades**.
1. Clique em **Membro de** e clique em **Adicionar**.
1. Na caixa Inserir os Nomes de Objeto a Serem Selecionados, digite `Administrators`, clique em Verificar nomes para garantir que o nome do grupo esteja correto.
1. Clique em **OK** e clique em **OK** novamente.
1. Selecionar **Iniciar > Painel de controle > Ferramentas administrativas > Política de segurança local > Políticas locais**.
1. Clique em Atribuição de direitos de usuário, clique com o botão direito em Agir como parte do sistema operacional e selecione Propriedades.
1. Clique em **Adicionar usuário ou grupo**.
1. Na caixa Inserir os Nomes de Objetos a Serem Selecionados, digite o nome do usuário que você criou na etapa 4, clique em **Verificar nomes** para garantir que o nome esteja correto e clique em **OK**.
1. Clique em **OK** para fechar a caixa de diálogo Agir como parte das propriedades do sistema operacional.

### Configurar o WebSphere para usar o usuário recém-criado como administrador {#configure-websphere-to-use-the-newly-created-user-as-administrator}

1. Certifique-se de que o WebSphere esteja em execução.
1. No Console administrativo do WebSphere, selecione **Segurança > Segurança global**.
1. Em Segurança administrativa, selecione **Funções de usuário administrativo**.
1. Clique em Adicionar e faça o seguinte:

   1. Tipo **&amp;ast;** na caixa pesquisar e clique em pesquisar.
   1. Clique em **Administrador** em funções.
   1. Adicione o usuário recém-criado à função Mapeado para e mapeie-o para Administrador.

1. Clique em **OK** e salve as alterações.
1. Reinicie o perfil do WebSphere.

## Habilitar segurança administrativa {#enable-administrative-security}

1. No Console administrativo do WebSphere, selecione **Segurança > Segurança global**.
1. Clique em **Assistente de configuração de segurança**.
1. Assegurar **Habilitar Segurança de Aplicativo** está ativada. Clique em **Avançar**.
1. Selecionar **Repositórios federados** e clique em **Próxima**.
1. Especifique as credenciais que deseja definir e clique em **Próxima**.
1. Clique em **Concluir**.
1. Reinicie o perfil do WebSphere.

   O WebSphere começa a usar o keystore e o truststore padrão.

## Habilitar SSL (chave personalizada e truststore) {#enable-ssl-custom-key-and-truststore}

Truststores e keystores podem ser criados usando o utilitário ikeyman ou o Admin Console. Para fazer o ikeyman funcionar corretamente, certifique-se de que o caminho de instalação do WebSphere não contenha parênteses.

1. No Console administrativo do WebSphere, selecione **Segurança > Gerenciamento de chaves e certificados SSL**.
1. Clique em **Armazenamento de chaves e certificados** em Itens relacionados.
1. No **Principais usos do armazenamento** , verifique se **Armazenamento de chaves SSL** está selecionada. Clique em **Novo**.
1. Digite um nome lógico e uma descrição.
1. Especifique o caminho onde deseja que o armazenamento de chaves seja criado. Se você já criou um armazenamento de chaves por meio do ikeyman, especifique o caminho para o arquivo de armazenamento de chaves.
1. Especifique e confirme a senha.
1. Escolha o tipo de armazenamento de chaves e clique em **Aplicar**.
1. Salve a configuração principal.
1. Clique em **Certificado pessoal**.
1. Se você tiver adicionado um armazenamento de chaves já criado usando ikeyman, seu certificado será exibido. Caso contrário, você precisará adicionar um novo certificado autoassinado executando as seguintes etapas:

   1. Selecione **Criar > certificado** autoassinado.
   1. Especifique os valores apropriados no formulário de certificado. Certifique-se de manter o Alias e o nome comum como nome de domínio totalmente qualificado da máquina.
   1. Clique em **Aplicar**.

1. Repita as etapas de 2 a 10 para criar um truststore.

## Aplicar armazenamento de chaves personalizado e armazenamento confiável no servidor {#apply-custom-keystore-and-truststore-to-the-server}

1. No Console Administrativo do WebSphere, selecione **Segurança > certificado SSL e gerenciamento** de chaves.
1. Clique **em Gerenciar configuração** de segurança de endpoint. O mapa de topologia local é aberto.
1. Em Entrada, selecione o filho direto dos nós.
1. Em itens relacionados, selecione **as configurações** de SSL.
1. Selecione **NodeafultSSLSetting**.
1. Nas listas suspensas nome da truststore e nome da keystore, selecione a truststore e a keystore personalizadas que você criou.
1. Clique em **Aplicar**.
1. Salve a configuração principal.
1. Reinicie o perfil do WebSphere.

   Seu perfil agora é executado nas configurações personalizadas de SSL e em seu certificado.

## Habilitação de suporte para nativos de formulários AEM {#enabling-support-for-aem-forms-natives}

1. No Console administrativo do WebSphere, selecione **Segurança > Segurança global**.
1. Na seção Autenticação, expanda **Segurança RMI/IIOP** e clique em **Comunicações de entrada CSIv2**.
1. Assegure que **Compatível com SSL** está selecionado na lista suspensa Transport.
1. Reinicie o perfil do WebSphere.

## Configuração do WebSphere para converter URLs que começam com https {#configuring-websphere-to-convert-urls-that-begins-with-https}

Para converter um URL que comece com https, adicione um certificado de Signatário para esse URL ao servidor WebSphere.

**Criar um certificado de signatário para um site habilitado para https**

1. Certifique-se de que o WebSphere esteja em execução.
1. No Console administrativo do WebSphere, navegue até Certificados do assinante e clique em Segurança > Certificado SSL e gerenciamento de chaves > Armazenamentos e certificados de chaves > NodeDefaultTrustStore > Certificados do assinante.
1. Clique em Recuperar da Porta e execute estas tarefas:

   * Na caixa Host, digite o URL. Por exemplo, digite `www.paypal.com`.
   * Na caixa Porta, digite `443`. Essa é a porta SSL padrão.
   * Na caixa Alias, digite um alias.

1. Clique em Recuperar informações do assinante e verifique se as informações foram recuperadas.
1. Clique em Aplicar e em Salvar.

A conversão de HTML para PDF do site cujo certificado foi adicionado agora funcionará no serviço Gerar PDF.

>[!NOTE]
>
>Para que um aplicativo se conecte a sites SSL de dentro do WebSphere, é necessário um certificado Signatário. Ele é usado pelo Java Secure Socket Extensions (JSSE) para validar certificados que o lado remoto da conexão enviada durante um handshake SSL.

## Configuração de portas dinâmicas {#configuring-dynamic-ports}

O IBM WebSphere não permite várias chamadas para ORB.init() quando a Segurança global está ativada. Você pode ler sobre a restrição permanente em https://www-01.ibm.com/support/docview.wss?uid=swg1PK58704.

Execute as seguintes etapas para definir a porta como dinâmica e resolver o problema:

1. No Console administrativo do WebSphere, selecione **Servidores** > **Tipos de servidor** > **Servidor de aplicativos WebSphere**.
1. Na seção Preferências, selecione o servidor.
1. No **Configuração** guia, em **Comunicações** seção, expandir **Portas** e clique em **Detalhes**.
1. Clique nos seguintes nomes de porta e altere o **número da porta** para 0 e clique em **OK**.

   * `ORB_LISTENER_ADDRESS`
   * `SAS_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_SERVERAUTH_LISTENER_ADDRESS`
   * `CSIV2_SSL_MUTUALAUTH_LISTENER_ADDRESS`

## Configurar o arquivo sling.properties {#configure-the-sling-properties-file}

1. Abertura `[aem-forms_root]`arquivo \crx-repository\launchpad\sling.properties para edição.
1. Localize o `sling.bootdelegation.ibm` propriedade e adicionar `com.ibm.websphere.ssl.*`ao seu campo de valor. O campo atualizado tem a seguinte aparência:

   ```shell
   sling.bootdelegation.ibm=com.ibm.xml.*, com.ibm.websphere.ssl.*
   ```

1. Salve o arquivo e reinicie o servidor.
