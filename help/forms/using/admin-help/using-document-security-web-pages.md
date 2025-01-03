---
title: Uso das páginas da Web de segurança de documentos
description: Saiba como fazer logon, navegar e usar as páginas da Web de segurança de documentos.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: caa31752-a02d-4d20-b7d9-c4aad5d0fae6
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Uso das páginas da Web de segurança de documentos {#using-the-document-security-webpages}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Usuários e administradores usam as páginas da Web de segurança de documentos para criar e gerenciar políticas, gerenciar documentos protegidos por política e monitorar eventos associados a documentos protegidos por política. Os administradores também usam as páginas da Web para criar conjuntos de políticas e designar coordenadores de definições de políticas, definir configurações padrão de segurança de documentos, gerenciar contas e registros de usuários convidados e monitorar e gerenciar eventos relacionados a servidores, políticas, usuários e documentos.

>[!NOTE]
>
>Você também pode fazer logon na segurança de documentos por meio do Acrobat e de outros aplicativos clientes usando sua conta de logon de usuário. (Consulte [Configuração do acesso à segurança de documentos de aplicativos clientes](using-document-security-web-pages.md#setting-up-access-to-document-security-from-client-applications).)

Para abrir as páginas da Web, você precisa de um navegador, do URL e de suas informações de logon para garantir a segurança dos documentos. O URL para usuários é diferente do URL para administradores.

Como a segurança de documentos faz referência aos diretórios existentes da sua organização para obter informações do usuário, as informações de logon da segurança de documentos podem ser as mesmas informações usadas para fazer logon na rede e em outros aplicativos. Consulte o administrador do sistema ou o administrador para obter informações sobre a conta.

Para fazer logon como administrador, você precisa ter a função de administrador atribuída a você. Você pode usar a conta de superadministrador default criada durante o processo de instalação.

## Fazer logon nas páginas da Web {#log-in-to-the-web-pages}

Para fazer logon nas páginas da Web usando um navegador do, você precisa do URL de segurança do documento e de uma conta. O URL para usuários é diferente do URL para administradores. Os administradores também podem fazer logon nas páginas de usuário para criar políticas.

Se você tiver acesso a mais de uma instalação de segurança de documentos, precisará do URL da instância de segurança de documentos que deseja acessar. Consulte o administrador se não tiver essas informações. A URL padrão para as páginas de usuário é `https://[host]:[port]/edc`. O número da porta pode não ser necessário em alguns casos. Peça detalhes ao administrador.

A URL padrão para administradores é `https://[host]:[port]/adminui`.

Para administradores, uma conta de superadministrador padrão é criada durante a instalação. Você pode usar essa conta para fazer logon quando a segurança de documentos for instalada pela primeira vez.

>[!NOTE]
>
>Você também pode acessar as páginas da Web no Acrobat e em outros aplicativos clientes. Consulte a Ajuda do Acrobat ou a Ajuda das extensões apropriadas do Acrobat Reader DC para obter detalhes.

1. Digite o URL no navegador:

   URL de segurança de documentos: `https://[host]:[port]/edc`

   ou URL do Console de Administração: `https://[host]:[port]/adminui`

1. Na janela de login, digite seu nome de usuário e senha e clique em OK.
1. No Administration Console, clique em Serviços > segurança de documentos.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e as setas para trás e para a frente, pois essa ação pode causar problemas de captura de dados indesejados e exibição de dados.

## Navegação nas páginas da Web {#navigating-the-web-pages}

Ao fazer logon nas páginas da Web do usuário, você verá links para as páginas de usuário Políticas, Documentos e Eventos.

Ao fazer logon no console de administração e navegar até a página principal da segurança de documentos, você também poderá ver um ou dois links adicionais, um para a página Configuração e outro para a página Usuários convidados e locais. A página Usuários convidados e locais é exibida somente se o registro do usuário convidado estiver habilitado.

Use esses links para acessar as várias páginas, onde você cria e gerencia políticas e documentos protegidos por política.

**Exibir uma página**

1. Clique no nome da página; por exemplo, clique em Políticas.

**Voltar à página anterior**

1. Clique no link de navegação na parte superior da página para a página para a qual você deseja voltar.

**Atualizar a lista de dados em uma página**

1. Na página principal, clique no link da página que deseja atualizar.

>[!NOTE]
>
>Ao trabalhar com as páginas da Web, evite usar os botões do navegador, como o botão Voltar, o botão Atualizar e as setas para trás e para a frente, pois essa ação pode causar problemas de captura de dados indesejados e exibição de dados.

## Configuração do acesso à segurança de documentos a partir de aplicativos clientes {#setting-up-access-to-document-security-from-client-applications}

Os aplicativos clientes devem ser configurados para se conectar à segurança de documentos para proteger documentos, abrir documentos protegidos por política e conectar-se às páginas da Web de segurança de documentos. Consulte a *Ajuda do Acrobat* ou a *Ajuda do RightsManagementExtension* apropriada para obter informações sobre como configurar a conexão no aplicativo cliente.

A segurança de documentos é acessada por SSL (Secure Sockets Layer). Instale o certificado do site em seu armazenamento de certificados para poder acessar a segurança de documentos por meio dos aplicativos clientes.

<!-- Fix broken link See Configuring SSL for information on SSL.-->

Essas instruções são específicas do Internet Explorer, mas você pode instalar o certificado usando qualquer navegador da Web compatível. Para obter mais informações, consulte a Ajuda do navegador.

**Instalar o certificado do servidor usando o Internet Explorer**

1. Abra o navegador da Web e digite o URL base para segurança de documentos na caixa Endereço. Por exemplo, digite `https://[host]:[port]`. Uma caixa de diálogo Alerta de segurança é exibida.
1. Clique em Exibir certificado, clique em Instalar certificado e selecione os padrões para instalação. O certificado precisa ser instalado nas Autoridades de Certificação Raiz Confiáveis.
1. Feche a sessão do navegador.
1. Abra outra janela do navegador e digite o mesmo URL na caixa Endereço. Uma caixa de diálogo Alerta de segurança não deve ser exibida. Este teste confirma se o certificado está instalado corretamente.

## Fazer logoff das páginas da Web {#log-out-of-the-web-pages}

Faça logout quando terminar de usar as páginas da Web, para que possa usar com segurança seu navegador da Web para outras finalidades. Dependendo de como a segurança de documentos está configurada, talvez seja necessário fechar o navegador para fazer logoff completamente.

1. No canto superior direito da página, clique em Logout.
1. Se uma mensagem for exibida na página Logout, feche a janela do navegador para fazer logout completamente. Caso contrário, você pode continuar a usar o navegador para outros propósitos.
