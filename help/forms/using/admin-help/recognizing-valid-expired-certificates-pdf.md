---
title: Como reconhecer certificados válidos e expirados em documentos PDF
seo-title: Como reconhecer certificados válidos e expirados em documentos PDF
description: Saiba como reconhecer certificados válidos e expirados em documentos PDF.
seo-description: Saiba como reconhecer certificados válidos e expirados em documentos PDF.
uuid: ceeff57a-586f-4f7b-852f-2a637f003d7e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4559218a-65ba-4577-ad26-7721e28971bc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Reconhecendo certificados válidos e expirados em documentos PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando um documento PDF com direitos de uso aplicados pelas extensões de Reader é aberto no Adobe Reader, uma barra de status é exibida descrevendo os direitos de uso específicos ativados no documento PDF.

Quando o certificado digital que especifica os direitos de uso de um documento PDF expira e o documento PDF é aberto no Adobe Reader, uma caixa de diálogo é exibida informando ao usuário que o documento PDF tem direitos de uso, mas esses direitos são desativados. Embora a mensagem indique que o documento PDF foi alterado ou adulterado, isso não é necessariamente o caso. O Adobe Reader exibe essa mensagem quando um certificado expira ou um documento é modificado. No Adobe Reader 7.0.x ou posterior, não é possível determinar qual caso é o problema no momento.

Após fechar a caixa de diálogo, o Adobe Reader abre o documento PDF. Os direitos de uso que foram aplicados usando extensões do Acrobat Reader DC não estão disponíveis, como esperado. Se o documento PDF for um formulário interativo, os campos do formulário serão bloqueados e o usuário não poderá alterar os dados do formulário.
