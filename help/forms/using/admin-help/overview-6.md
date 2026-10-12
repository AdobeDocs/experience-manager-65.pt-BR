---
title: Visão geral da configuração do SSL
description: Saiba como melhorar a segurança da comunicação configurando o SSL.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: fbe1487e-c830-4be8-9841-6022e6a98ae7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%
---
# Visão geral da configuração do SSL {#overview-of-configuring-ssl}

Você pode criar credenciais SSL (Secure Sockets Layer) e configurar o SSL no servidor de aplicativos para melhorar a segurança da comunicação com o servidor de aplicativos.

Como produto de segurança, o Rights Management exige a configuração do SSL. Ao configurar certificados SSL, certifique-se de usar somente chaves RSA. Certificados SSL com chaves DSA não são compatíveis.

As informações fornecidas se aplicam às instalações manuais, automáticas e turnkey. Ele oferece um exemplo de um método para configurar o SSL. Você também pode usar outros métodos mais apropriados para sua rede ou organização.

>[!NOTE]
>
>É recomendável concluir a instalação, a configuração e a implantação dos módulos de formulários do AEM e garantir que os produtos estejam sendo executados corretamente antes de configurar o SSL no servidor de aplicativos.

>[!NOTE]
>
>Ao criar certificados de segurança SSL e credenciais, use os mesmos privilégios de conta de usuário que você usou para executar o servidor de aplicativos. Se o servidor de aplicativos for executado usando outros privilégios de usuário, o formulário poderá não ser renderizado corretamente para representações PDFForm quando ContentRootURI apontar para https.

Se você tiver um servidor LDAP habilitado para SSL, configure o Gerenciamento de usuários para trabalhar com ele. (Consulte [Configurar o Gerenciamento de Usuários para um servidor LDAP habilitado para SSL](/help/forms/using/admin-help/configure-user-management-ssl-enabled.md#configure-user-management-for-an-ssl-enabled-ldap-server).)
