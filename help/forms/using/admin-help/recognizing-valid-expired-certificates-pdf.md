---
title: Reconhecimento de certificados válidos e expirados em documentos do PDF
description: Saiba como reconhecer certificados válidos e expirados em documentos do PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: dfe2823a-3a0d-4e45-8765-f618529e22dd
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%
---
# Reconhecimento de certificados válidos e expirados em documentos do PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando um documento do PDF com direitos de uso aplicados pelas extensões do Reader é aberto no Adobe Reader, é exibida uma barra de status que descreve os direitos de uso específicos ativados no documento do PDF.

Quando o certificado digital que especifica os direitos de uso de um documento do PDF expira e o documento do PDF é aberto no Adobe Reader, uma caixa de diálogo informa ao usuário que o documento do PDF tem direitos de uso, mas esses direitos estão desativados. Embora a mensagem indique que o documento do PDF foi alterado ou adulterado, esse não é necessariamente o caso. O Adobe Reader exibe essa mensagem quando um certificado expira ou um documento é modificado. No Adobe Reader 7.0.x ou posterior, não é possível determinar em qual caso está o problema no momento.

Após fechar a caixa de diálogo, o Adobe Reader abre o documento do PDF. Os direitos de uso aplicados com o uso das extensões do Acrobat Reader DC não estão disponíveis, conforme esperado. Se o documento do PDF for um formulário interativo, os campos de formulário serão bloqueados e o usuário não poderá alterar os dados do formulário.
