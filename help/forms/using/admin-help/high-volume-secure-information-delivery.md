---
title: Entrega segura de informações de alto volume
description: A segurança de documentos oferece suporte à associação de licenças a usuários, e não a documentos em ambientes de produção em massa.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: 616e8821-ca96-4471-9120-0e1076a06178
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# Entrega segura de informações de alto volume {#high-volume-secure-information-delivery}

Em um ambiente de produção em massa, como o que gera faturas mensais seguras para uma empresa de telecomunicações, criar licenças específicas para cada documento pode se tornar um processo que consome muitos recursos. Nesses casos, a segurança de documentos oferece suporte à associação de licenças a usuários, e não a documentos. A licença gerada para um usuário é usada para todos os documentos protegidos para esse usuário.

Uma vantagem dessa abordagem é que o tamanho do banco de dados de segurança de documentos não cresce linearmente com os documentos, e sim com o número de usuários. Além disso, como é necessário criar a licença apenas uma vez para um usuário, a proteção subsequente de documentos por meio dessas políticas torna-se mais rápida. Recursos como acesso offline, expiração de documentos e revogação são suportados para todos esses documentos.

A segurança de documentos também oferece suporte a Políticas abstratas. Políticas abstratas são modelos de política que contêm todos os atributos de política, como configurações de segurança de documentos e direitos de uso, mas não contêm uma lista de principais. Os administradores podem criar qualquer número de políticas a partir da política abstrata com princípios diferentes que devem ter acesso aos documentos. As alterações feitas na política abstrata não afetam as políticas reais geradas pelas políticas abstratas.

Se houver uma geração de fatura mensal para uma empresa de telecomunicações, você criará uma política abstrata, criará usuários e, em seguida, gerará licenças exclusivas para cada usuário. As licenças são aplicadas posteriormente a documentos para cada usuário.

A criação de uma política abstrata é suportada somente por meio do SDK Java de segurança de documentos. No entanto, você pode administrar as políticas criadas a partir da política abstrata das páginas da Web de segurança de documentos. As políticas criadas usando esse método são idênticas em comportamento às criadas nas páginas da Web de segurança de documentos.

Consulte [Programação com AEM](https://www.adobe.com/go/learn_aemforms_programming_63) para obter mais informações.
