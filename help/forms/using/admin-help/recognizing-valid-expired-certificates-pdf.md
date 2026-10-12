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
source-wordcount: '198'
ht-degree: 0%
---
# Reconhecimento de certificados válidos e expirados em documentos do PDF {#recognizing-valid-and-expired-certificates-in-pdf-documents}

Quando um documento do PDF com direitos de uso aplicados pelas extensões do Reader é aberto no Adobe Reader, é exibida uma barra de status que descreve os direitos de uso específicos ativados no documento do PDF.

Quando o certificado digital que especifica os direitos de uso de um documento do PDF expira e o documento do PDF é aberto no Adobe Reader, uma caixa de diálogo informa ao usuário que o documento do PDF tem direitos de uso, mas esses direitos estão desativados. Embora a mensagem indique que o documento do PDF foi alterado ou adulterado, esse não é necessariamente o caso. O Adobe Reader exibe essa mensagem quando um certificado expira ou um documento é modificado. No Adobe Reader 7.0.x ou posterior, não é possível determinar em qual caso está o problema no momento.

Após fechar a caixa de diálogo, o Adobe Reader abre o documento do PDF. Os direitos de uso aplicados com o uso das extensões do Acrobat Reader DC não estão disponíveis, conforme esperado. Se o documento do PDF for um formulário interativo, os campos de formulário serão bloqueados e o usuário não poderá alterar os dados do formulário.
