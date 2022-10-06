---
title: Visão geral da configuração do SSL
seo-title: Overview of configuring SSL
description: Saiba mais sobre como melhorar a segurança da comunicação configurando o SSL.
seo-description: Learn about how to enhance security of communication by configuring SSL.
uuid: 3e99d2bf-137b-45ba-8384-309624094623
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e107abb-861f-4063-b600-c87e34639019
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Visão geral da configuração do SSL {#overview-of-configuring-ssl}

Você pode criar credenciais SSL (Secure Sockets Layer) e configurar o SSL no servidor de aplicativos para melhorar a segurança da comunicação com seu servidor de aplicativos.

Como produto de segurança, o Rights Management requer a configuração do SSL. Ao configurar certificados SSL, certifique-se de usar somente chaves RSA. Certificados SSL com chaves DSA não são suportados.

As informações fornecidas se aplicam às instalações chave, automática e manual. Ele oferece um exemplo de método para configurar o SSL. Você também pode usar outros métodos mais apropriados para sua rede ou organização.

>[!NOTE]
>
>É recomendável concluir a instalação, configuração e implantação dos módulos de formulários AEM e garantir que os produtos estejam sendo executados corretamente antes de configurar o SSL no servidor de aplicativos.

>[!NOTE]
>
>Ao criar certificados e credenciais de segurança SSL, use os mesmos privilégios de conta de usuário usados para executar o servidor de aplicativos. Se o servidor de aplicativos for executado usando outros privilégios de usuário, o formulário poderá não ser renderizado corretamente para representações PDFForm quando o ContentRootURI apontar para https.

Se você tiver um servidor LDAP habilitado para SSL, configure o Gerenciamento de usuários para funcionar com ele. (Consulte [Configurar o gerenciamento de usuários para um servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
