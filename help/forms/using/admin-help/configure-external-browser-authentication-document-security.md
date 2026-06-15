---
title: Configurar a autenticação estendida a partir do navegador externo para segurança de documentos
description: Saiba como configurar a autenticação externa do navegador para que os usuários possam autenticar para documentos protegidos por política do PDF no Acrobat ou no Reader usando o navegador da Web padrão do sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 98a772829d3568a5826ea9e3ae65760f1587040f
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 1%

---

# Configurar a autenticação estendida a partir do navegador externo para segurança de documentos {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> Verifique se você tem privilégios de administrador para acessar o console de administração do AEM Forms.

A autenticação estendida de um navegador externo permite que os usuários autentiquem documentos do PDF protegidos por política usando o navegador da Web padrão do sistema (como o Microsoft Edge ou o Google Chrome) em vez do controle do navegador incorporado no Acrobat ou no Reader. Isso permite métodos de autenticação modernos, como PassKey, autenticação biométrica e outros recursos do Provedor de identidade (IDP) que exigem um navegador moderno.

Quando ativado, abrir um documento protegido por política no Acrobat ou Reader inicia a página de logon do IDP no navegador padrão do usuário. Após a autenticação, o usuário é redirecionado automaticamente de volta para o Acrobat ou Reader e o documento é desbloqueado.

## Pré-requisitos {#prerequisites}

Antes de configurar a autenticação externa do navegador, verifique se os seguintes requisitos foram atendidos:

* AEM Forms 6.5 em JEE com Service Pack 6.5.25.0 implantado ou Service Pack 6.5.24.0 com o patch de hotfix de JEE aplicável instalado em um servidor de aplicativos com suporte (JBoss, WebLogic ou WebSphere). Consulte [Links de distribuição de software para AEM Forms JEE Hotfix2 6.5.24.0](#software-distribution-links).
* A autenticação estendida (autenticação de terceiros) já está habilitada e funcional com um IDP. Consulte [Configurações do servidor](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings) e [Adicionar o provedor de autenticação estendida](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider).
* Adobe Acrobat Pro ou Adobe Acrobat Reader (64 bits) instalado no PC cliente Windows com a atualização mais recente

### Links de distribuição de software para AEM Forms JEE Hotfix2 6.5.24.0 {#software-distribution-links}

A autenticação de navegador externo está disponível no AEM Forms no JEE Service Pack 6.5.25.0 e posterior.

Se você estiver no AEM Forms no JEE Service Pack 6.5.24.0 ou anterior, siga um destes procedimentos:

* Atualize para o [AEM Forms no JEE Service Pack 6.5.25.0](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip).
* Instale o patch do AEM Forms JEE Hotfix 6.5.24.0 para o servidor de aplicativos e plataforma usando os links abaixo.

Baixe e instale o patch do AEM Forms JEE Hotfix 6.5.24.0 para sua plataforma em [Adobe Software Distribution](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html):

**JBoss**

* Windows: [Hotfix do AEM Service Pack 6.5.24.0 no Windows para JBoss JEE server](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)
* Linux: [Hotfix do AEM Service Pack 6.5.24.0 no Linux para servidor JBoss JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows: [Hotfix do AEM Service Pack 6.5.24.0 no Windows para o servidor WebSphere JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)
* Linux: [Hotfix do AEM Service Pack 6.5.24.0 no Linux para servidor WebSphere JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows: [Hotfix do AEM Service Pack 6.5.24.0 no Windows para servidor WebLogic JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)
* Linux: [Hotfix do AEM Service Pack 6.5.24.0 no Linux para servidor WebLogic JEE](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

Para obter instruções de instalação, consulte [Instalar um patch de JEE](/help/release-notes/jee-patch-installer-65.md).

## Habilitar autenticação externa do navegador {#enable-external-browser-authentication}

Este vídeo mostra como habilitar a autenticação de navegador externo no servidor do AEM Forms Document Security.

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. No console de administração, clique em **Serviços** > **Segurança de Documentos** > **Configuração** > **Configuração do Servidor**.
1. Localize a seção **Permitir autenticação estendida do navegador externo para aplicativos cliente Adobe**.
1. Marque a caixa de seleção de cada plataforma de cliente Adobe que deseja ativar:
   * **Adobe Acrobat e Reader (64 bits) - Área de Trabalho**
   * **Adobe Acrobat Reader (32 bits) - Área de Trabalho**
1. Clique em **OK**.

Para obter a descrição da configuração do servidor, consulte [Configurações do servidor](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings).

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## Verificação {#verification}

Este vídeo mostra como verificar a autenticação externa do navegador: abra um PDF protegido por política no Acrobat, faça logon por meio do navegador padrão e confirme se o documento é desbloqueado após a autenticação.

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Crie um documento do PDF protegido por política usando o servidor de Segurança de documentos.
1. Em uma máquina cliente Windows, abra a PDF protegida no Acrobat Pro ou Acrobat Reader.
1. Uma caixa de diálogo de consentimento é exibida no Acrobat. Clique em **Entrar**.
1. Verifique se o navegador padrão do sistema é aberto com a página de logon do IDP.
1. Autenticação completa.
1. Verifique se o documento protegido foi aberto com êxito.

## Resolução de problemas {#troubleshooting}

### O navegador incorporado se abre em vez do navegador do sistema {#embedded-browser-opens-instead-of-system-browser}

* Verifique se a autenticação do navegador externo está habilitada no servidor. Consulte [Habilitar autenticação de navegador externo](#enable-external-browser-authentication).
* Confirme se a versão do Acrobat ou do Reader é compatível com esse recurso.

### A autenticação é bem-sucedida no navegador, mas o documento não é desbloqueado {#authentication-succeeds-but-document-does-not-unlock}

* Verifique se o Acrobat ou o Reader está em execução e se não está bloqueado por firewall ou software de segurança.
* Se o problema persistir, reinstale ou repare a instalação do Acrobat ou do Reader para restaurar o registro do manipulador de protocolo.

### A mensagem &quot;Não foi possível entrar&quot; é exibida no Acrobat {#we-couldnt-sign-you-in-message}

* O usuário pode ter levado muito tempo para concluir a autenticação. Tente novamente.
* Verifique a conectividade de rede entre o navegador e o servidor do AEM Forms.

### A opção de autenticação não é exibida na página de logon {#authentication-option-does-not-appear}

* Os métodos e as opções de autenticação são configurados pelo IDP, não pelo AEM Forms ou Acrobat. Verifique se o IDP é compatível com o método de autenticação que você deseja usar.
* Verifique se a página de logon está sendo carregada no navegador do sistema (não no navegador incorporado).
