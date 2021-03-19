---
title: Fornecimento de informações seguras de alto volume
seo-title: Fornecimento de informações seguras de alto volume
description: A segurança de documentos oferece suporte à associação de licenças aos usuários, em vez de aos documentos em ambientes de produção em massa.
seo-description: A segurança de documentos oferece suporte à associação de licenças aos usuários, em vez de aos documentos em ambientes de produção em massa.
uuid: 9747d283-506c-434e-9850-e50b95290cc8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b76d7d93-23a5-4c08-81f5-a56267b1556a
feature: Segurança de documentos
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---


# Entrega de informações seguras de alto volume {#high-volume-secure-information-delivery}

Em um ambiente de produção em massa, como o que gera faturas mensais seguras para uma empresa de telecomunicações, criar licenças específicas para cada documento pode se tornar um processo que consome muitos recursos. Nesses casos, a segurança dos documentos é compatível com a associação de licenças aos usuários, e não com os documentos. A licença gerada para um usuário é usada para todos os documentos protegidos para esse usuário.

Uma vantagem dessa abordagem é que o tamanho do banco de dados de segurança de documentos não aumenta linearmente com os documentos, em vez do número de usuários. Além disso, como é necessário criar a licença apenas uma vez para um usuário, a proteção subsequente dos documentos por meio dessas políticas se torna mais rápida. Recursos como acesso offline, expiração de documento e revogação são suportados em todos esses documentos.

A segurança de documentos também oferece suporte às Políticas abstratas. As políticas abstratas são modelos de política que contêm todos os atributos de política, como configurações de segurança de documento e direitos de uso, mas não contêm uma lista de principais. Os administradores podem criar qualquer número de políticas a partir da política abstrata com diferentes entidades que devem ter acesso aos documentos. As alterações introduzidas na política abstrata não afetam as políticas reais geradas pelas políticas abstratas.

No caso da geração mensal de faturas para uma empresa de telecomunicações, você cria uma política abstrata, cria usuários e gera licenças exclusivas para cada usuário. As licenças são posteriormente aplicadas a documentos de cada usuário.

A criação de uma política abstrata é compatível somente por meio do SDK Java de segurança de documento. No entanto, você pode administrar as políticas criadas a partir da política abstrata nas páginas da Web de segurança de documentos. As políticas que são criadas usando esse método são idênticas em comportamento às criadas nas páginas da Web de segurança de documentos.

Consulte [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_63) para obter mais informações.
