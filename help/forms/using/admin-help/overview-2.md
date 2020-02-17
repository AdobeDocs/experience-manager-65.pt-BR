---
title: Noções básicas para o gerenciamento de certificados e credenciais
seo-title: Noções básicas para o gerenciamento de certificados e credenciais
description: Saiba mais sobre as noções básicas de gerenciamento de certificados e credenciais.
seo-description: Saiba mais sobre as noções básicas de gerenciamento de certificados e credenciais.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Noções básicas para o gerenciamento de certificados e credenciais {#basics-of-managing-certificates-and-credentials}

Uma *credencial* contém suas informações de chave privada necessárias para assinar ou identificar documentos. Um *certificado* é uma informação de chave pública configurada para confiança. Os formulários do AEM usam certificados e credenciais para vários fins:

* As extensões do Acrobat Reader DC usam uma credencial para habilitar os direitos de uso do Adobe Reader em documentos PDF. (Consulte [Configurar credenciais para uso com extensões](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions)do Acrobat Reader DC.)
* Você pode configurar o Rights Management para exibir credenciais para uso no Acrobat somente de emissores confiáveis. (Consulte [Configurar configurações](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings)de exibição do Rights Management.) O nome comum (CN) deve constar do certificado.
* O serviço de assinatura acessa certificados e credenciais. Para obter detalhes sobre o serviço de assinatura, consulte Referência [de](https://www.adobe.com/go/learn_aemforms_services_63)serviços.

**Gerando uma chave de par**

Os formulários do AEM usam seu Repositório de confiança para armazenar e gerenciar certificados, credenciais e CRLs (certificate Revolutions lists). Além disso, você pode usar um dispositivo HSM (Hardware Security Module, módulo de segurança de hardware) independente para armazenar chaves privadas.

Os formulários AEM não fornecem nenhuma opção para gerar um par de chaves. No entanto, você pode gerá-lo usando ferramentas, como o Java keytool, e importá-lo no AEM Forms Trust Store. Para obter mais informações sobre o Java keytool, consulte:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html](https://blogs.adobe.com/livecycle/2010/01/creating_ssl_keys_and_certific.html)

Os seguintes tipos de assinatura são suportados e podem ser importados em formulários AEM:

* Assinatura XML
* XMLTimeStampToken
* TimeStampToken RFC 3161
* PKCS#7
* PKCS#1
* Assinaturas DSA

**Manuseio de chave perdida ou comprometida**

Se você suspeitar que sua chave foi perdida ou comprometida, execute as seguintes ações:

1. Informe a autoridade de certificação para que ela adicione a chave comprometida na lista de revogação de certificado para revogar a chave.
1. Obtenha uma nova chave e seus certificados da autoridade de certificação.
1. Assine os documentos que foram assinados usando a chave comprometida novamente usando a nova chave.

