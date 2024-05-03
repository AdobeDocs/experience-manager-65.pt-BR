---
title: Noções básicas do gerenciamento de certificados e credenciais
description: Saiba mais sobre as noções básicas de gerenciamento de certificados e credenciais.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_certificates_and_credentials
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 74bf0e77-f47b-475a-b2a7-52cfb3baaa22
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Noções básicas do gerenciamento de certificados e credenciais {#basics-of-managing-certificates-and-credentials}

A *credencial* contém as informações da chave privada necessárias para assinar ou identificar documentos. A *certificado* são informações de chave pública que você configura para confiança. Os formulários AEM usam certificados e credenciais para várias finalidades:

* As extensões do Acrobat Reader DC usam uma credencial para ativar os direitos de uso do Adobe Reader em documentos do PDF. (Consulte [Configuração de credenciais para uso com extensões do Acrobat Reader DC](/help/forms/using/admin-help/configuring-credentials-acrobat-reader-dc.md#configuring-credentials-for-use-with-acrobat-reader-dc-extensions).)
* Você pode configurar o Rights Management para exibir credenciais para uso no Acrobat somente de emissores confiáveis. (Consulte [Definir configurações de exibição de Rights Management](/help/forms/using/admin-help/configuring-client-server-options.md#configure-document-security-display-settings).) A Common Name (CN) deve estar presente no certificado.
* O serviço de Assinatura acessa certificados e credenciais. Para obter detalhes sobre o serviço de assinatura, consulte [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_65).

**Gerar uma chave de par**

O AEM Forms usa seu armazenamento de confiança para armazenar e gerenciar certificados, credenciais e listas de certificados revogados (CRLs). Além disso, você pode usar um dispositivo HSM (Hardware Security Module, módulo de segurança de hardware) independente para armazenar chaves privadas.

O AEM Forms não fornece nenhuma opção para gerar um par de chaves. No entanto, você pode gerá-lo usando ferramentas, como a ferramenta de chave Java, e importá-lo no AEM Forms Trust Store. Para obter mais informações sobre a ferramenta Java keytool, consulte o seguinte:

[https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html](https://docs.oracle.com/javase/tutorial/security/toolsign/step3.html)

[https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html](https://docs.oracle.com/cd/E19798-01/821-1841/gjrgy/index.html)

[https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL](https://helpcenter.gsx.com/hc/en-us/articles/115015960428-How-to-Generate-a-Self-Signed-Certificate-and-Private-Key-using-OpenSSL)

Os seguintes tipos de assinatura são suportados e podem ser importados em formulários AEM:

* Assinatura XML
* XMLTimeStampToken
* RFC 3161 Token de carimbo de data/hora
* PKCS#7
* PKCS#1
* Assinaturas DSA

**Tratamento de chave perdida ou comprometida**

Se você suspeitar que a chave foi perdida ou comprometida, execute as seguintes ações:

1. Informe a autoridade de certificação para que ela adicione a chave comprometida à lista de certificados revogados para revogar a chave.
1. Obter uma nova chave e seus certificados da autoridade de certificação.
1. Assine os documentos que foram assinados usando a chave comprometida novamente usando a nova chave.
