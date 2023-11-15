---
title: Reconhecimento de certificados válidos e expirados em documentos do PDF
description: Saiba como reconhecer certificados válidos e expirados em documentos PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Reconhecimento de certificados válidos e expirados em documentos do PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando um documento PDF que tem direitos de uso aplicados por extensões Reader é aberto no Adobe Reader, é exibida uma barra de status que descreve os direitos de uso específicos ativados no documento PDF.

Quando o certificado digital que especifica os direitos de uso de um documento PDF expirar e o documento PDF for aberto no Adobe Reader, uma caixa de diálogo avisará ao usuário que o documento PDF tem direitos de uso, mas esses direitos estarão desativados. Embora a mensagem indique que o documento PDF foi alterado ou adulterado, esse não é necessariamente o caso. O Adobe Reader exibe essa mensagem quando um certificado expira ou um documento é modificado. No Adobe Reader 7.0.x ou posterior, não é possível determinar qual caso está ocorrendo no momento.

Após fechar a caixa de diálogo, o Adobe Reader abre o documento PDF. Os direitos de uso aplicados com o uso das extensões do Acrobat Reader DC não estão disponíveis, conforme esperado. Se o documento PDF for um formulário interativo, os campos de formulário serão bloqueados e o usuário não poderá alterar os dados do formulário.
