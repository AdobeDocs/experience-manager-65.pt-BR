---
title: Utilização das páginas Web de segurança do documento
seo-title: Utilização das páginas Web de segurança do documento
description: Saiba como fazer logon, navegar e usar as páginas da Web de segurança do documento.
seo-description: Saiba como fazer logon, navegar e usar as páginas da Web de segurança do documento.
uuid: b4863343-cda5-474a-a101-a20e39b1f8c7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 2878b145-e6c0-48d3-810c-3540de13c826
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Utilização das páginas Web de segurança do documento {#using-the-document-security-webpages}

Os usuários e administradores usam as páginas da Web de segurança do documento para criar e gerenciar políticas, gerenciar documentos protegidos por política e monitorar eventos associados a documentos protegidos por política. Os administradores também usam as páginas da Web para criar conjuntos de políticas e designar coordenadores de conjuntos de políticas, configurar as configurações padrão de segurança do documento, gerenciar registros de usuários convidados e contas, além de monitorar e gerenciar eventos relacionados a servidores, políticas, usuários e documentos.

>[!NOTE]
>
>Você também pode fazer logon na segurança do documento por meio do Acrobat e de outros aplicativos clientes usando sua conta de logon de usuário. (Consulte [Configuração do acesso à segurança do documento de aplicativos](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications)clientes.)

Para abrir as páginas da Web, você precisa de um navegador e o URL e suas informações de logon para a segurança do documento. O URL para usuários é diferente do URL para administradores.

Como a segurança do documento faz referência aos diretórios existentes de sua organização para obter informações sobre o usuário, suas informações de login de segurança do documento podem ser as mesmas que você usa para fazer logon na rede e em outros aplicativos. Consulte o administrador do sistema ou o administrador para obter informações sobre sua conta.

Para fazer logon como administrador, é necessário ter a função de administrador atribuída a você. Você pode usar a conta de superadministrador padrão criada durante o processo de instalação.

## Fazer logon nas páginas da Web {#log-in-to-the-web-pages}

Para fazer logon nas páginas da Web usando um navegador, você precisa do URL de segurança do documento e de uma conta. O URL para usuários é diferente do URL para administradores. Os administradores também podem fazer logon nas páginas do usuário para criar políticas.

Se você tiver acesso a mais de uma instalação da segurança do documento, precisará do URL da instância de segurança do documento que deseja acessar. Consulte o administrador se você não tiver essas informações. O URL padrão das páginas do usuário é `https://[host]:[port]/edc`. O número da porta pode não ser necessário em alguns casos. Peça detalhes ao administrador.

O URL padrão para administradores é `https://[host]:[port]/adminui`.

Para administradores, uma conta de superadministrador padrão é criada durante a instalação. Você pode usar essa conta para fazer logon quando a segurança do documento for instalada pela primeira vez.

>[!NOTE]
>
>Você também pode acessar as páginas da Web do Acrobat e de outros aplicativos clientes. Consulte a Ajuda do Acrobat ou a Ajuda das extensões apropriadas do Acrobat Reader DC para obter detalhes.

1. Digite o URL no seu navegador:

   URL de segurança do Documento: `https://[host]:[port]/edc`

   ou URL do Console de administração: `https://[host]:[port]/adminui`

1. Na janela de logon, digite seu nome de usuário e senha e clique em OK.
1. No Console de administração, clique em Serviços > Segurança do documento.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e as setas para frente e para trás, pois essa ação pode causar problemas indesejados de captura de dados e exibição de dados.

## Navegação nas páginas da Web {#navigating-the-web-pages}

Ao fazer logon nas páginas da Web do usuário, você verá links para as páginas de usuário Políticas, Documentos e Eventos.

Ao fazer logon no console de administração e navegar até a página principal de segurança do documento, você também pode ver um ou dois links adicionais, um para a página Configuração e outro para a página Usuários convidados e locais. A página Usuários convidados e locais é exibida somente se o registro de usuários convidados estiver ativado.

Use esses links para acessar as várias páginas, onde você cria e gerencia políticas e documentos protegidos por política.

**Exibir uma página**

1. Clique no nome da página; como políticas de cliques.

**Voltar para a página anterior**

1. Clique no link de navegação na parte superior da página para a página que deseja voltar.

**Atualizar a listagem de dados em uma página**

1. Na página principal, clique no link para a página que deseja atualizar.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e as setas para frente e para trás, pois essa ação pode causar problemas indesejados de captura de dados e exibição de dados.

## Configurar acesso à segurança do documento a partir de aplicativos clientes {#setting-up-access-to-document-security-from-client-applications}

Os aplicativos cliente devem ser configurados para se conectar à segurança do documento para proteger documentos, abrir documentos protegidos por política e se conectar às páginas da Web de segurança do documento. Consulte a Ajuda *do* Acrobat ou a Ajuda *apropriada do* RightsManagementExtension para obter informações sobre como configurar a conexão no aplicativo cliente.

A segurança do Documento é acessada por SSL (Secure Sockets Layer). É necessário instalar o certificado do site no repositório de certificados para que você possa acessar a segurança do documento pelos aplicativos clientes.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Essas instruções são específicas do Internet Explorer, mas você pode instalar o certificado usando qualquer navegador da Web compatível. Para obter mais informações, consulte a Ajuda do seu navegador.

**Instale o certificado do servidor usando o Internet Explorer**

1. Abra o navegador da Web e digite o URL básico para a segurança do documento na caixa Endereço. For example, type `https://[host]:[port]`. Uma caixa de diálogo Alerta de segurança é exibida.
1. Clique em Certificado de Visualização e, em seguida, clique em Instalar certificado e selecione os padrões para instalação. O certificado precisa ser instalado nas Autoridades de Certificação Raiz Confiáveis.
1. Feche a sessão do navegador.
1. Abra outra janela do navegador e digite o mesmo URL na caixa Endereço. Uma caixa de diálogo Alerta de segurança não deve ser exibida. Este teste confirma que o certificado está instalado corretamente.

## Fazer logout das páginas da Web {#log-out-of-the-web-pages}

Desconecte-se quando terminar de usar as páginas da Web para que você possa usar com segurança seu navegador da Web para outros fins. Dependendo de como a segurança do documento está configurada, talvez seja necessário fechar o navegador para encerrar a sessão.

1. No canto superior direito da página, clique em Logout.
1. Se uma mensagem for exibida na página Logout, feche a janela do navegador para efetuar logout completo. Caso contrário, você pode continuar usando o navegador para outros fins.

