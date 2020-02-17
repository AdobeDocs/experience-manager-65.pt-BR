---
title: Fornecimento de informações seguras de alto volume
seo-title: Fornecimento de informações seguras de alto volume
description: A segurança de documentos suporta a associação de licenças aos usuários, em vez de aos documentos em ambientes de produção em massa.
seo-description: A segurança de documentos suporta a associação de licenças aos usuários, em vez de aos documentos em ambientes de produção em massa.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Fornecimento de informações seguras de alto volume {#high-volume-secure-information-delivery}

Em um ambiente de produção em massa, como o que gera faturas mensais seguras para uma empresa de telecom, a criação de licenças específicas para cada documento pode se tornar um processo que consome muitos recursos. Nesses casos, a segurança dos documentos suporta a associação de licenças aos usuários, e não aos documentos. A licença gerada para um usuário é usada para todos os documentos protegidos para esse usuário.

Uma vantagem dessa abordagem é que o tamanho do banco de dados de segurança do documento não cresce linearmente com os documentos, em vez do número de usuários. Além disso, como é necessário criar a licença apenas uma vez para um usuário, a proteção subsequente dos documentos por meio dessas políticas se torna mais rápida. Recursos como acesso offline, expiração de documento e revogação são suportados para todos esses documentos.

A segurança de documentos também suporta Políticas abstratas. Políticas abstratas são modelos de política que contêm todos os atributos de política, como configurações de segurança do documento e direitos de uso, mas não contêm uma lista de principais. Os administradores podem criar qualquer número de políticas a partir da política abstrata com diferentes principais que devem ter acesso aos documentos. As alterações introduzidas na política abstrata não afetam as políticas efetivas geradas pelas políticas abstratas.

No caso de geração de fatura mensal para uma empresa telecom, você cria uma política abstrata, cria usuários e gera licenças exclusivas para cada usuário. As licenças são aplicadas posteriormente aos documentos de cada usuário.

A criação de uma política abstrata é suportada somente por meio da segurança do documento do Java SDK. Entretanto, é possível administrar as políticas que você cria a partir da política abstrata a partir das páginas da Web de segurança do documento. As políticas criadas usando esse método são idênticas no comportamento às criadas a partir de páginas da Web de segurança do documento.

Consulte [Programação com formulários](https://www.adobe.com/go/learn_aemforms_programming_63) AEM para obter mais informações.
