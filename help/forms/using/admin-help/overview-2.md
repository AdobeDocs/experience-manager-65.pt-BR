---
title: Noções básicas para o gerenciamento de certificados e credenciais
seo-title: Basics of managing certificates and credentials
description: Saiba mais sobre as noções básicas do gerenciamento de certificados e credenciais.
seo-description: Learn about the basics of managing certificates and credentials.
uuid: f421e206-e7b5-416c-b9fb-974094f10a66
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 986d16fc-4c81-4785-b1f3-fe8bd7ff669e
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Noções básicas para o gerenciamento de certificados e credenciais {#basics-of-managing-certificates-and-credentials}

A *credencial* contém as informações da chave privada necessárias para assinar ou identificar documentos. A *certificate* são informações de chave pública configuradas para confiança. Os formulários AEM usam certificados e credenciais para várias finalidades:

* As extensões do Acrobat Reader DC usam uma credencial para habilitar os direitos de uso do Adobe Reader em documentos do PDF. (Consulte [Configurar credenciais para uso com extensões do Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Você pode configurar o Rights Management para exibir credenciais para uso no Acrobat somente de emissores confiáveis. (Consulte [Definir configurações de exibição de Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) O nome comum (NC) deve constar do certificado.
* O serviço de assinatura acessa certificados e credenciais. Para obter detalhes sobre o serviço de assinatura, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_65).

**Gerar uma chave de par**

AEM formulários usa o Armazenamento de confiança para armazenar e gerenciar certificados, credenciais e CRLs (certificate&#39;&#39; lists). Além disso, você pode usar um dispositivo HSM (Hardware Security Module, Módulo de segurança de hardware) independente para armazenar chaves privadas.

AEM forms não fornece nenhuma opção para gerar um par de chaves. No entanto, você pode gerá-lo usando ferramentas, como o keytool do Java, e importá-lo AEM forms Trust Store. Para obter mais informações sobre a ferramenta-chave Java, consulte o seguinte:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

Os seguintes tipos de assinatura são suportados e podem ser importados em AEM formulários:

* Assinatura XML
* XMLTimeStampToken
* RFC 3161 TimeStampToken
* PKCS#7
* PKCS#1
* Assinaturas DSA

**Manuseio de chave perdida ou comprometida**

Se você suspeitar que sua chave foi perdida ou comprometida, execute as seguintes ações:

1. Informe a autoridade de certificação para que ela adicione a chave comprometida na lista de revogação de certificado para revogar a chave.
1. Obter uma nova chave e seus certificados da autoridade de certificação.
1. Assine os documentos que foram assinados usando a chave comprometida novamente usando a nova chave.
