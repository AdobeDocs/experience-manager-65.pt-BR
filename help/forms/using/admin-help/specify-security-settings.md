---
title: Especificar configurações de segurança
description: Saiba como especificar configurações de segurança para proteger arquivos de dados XML. O recurso de configuração de segurança controla as entidades externas nas entradas XML.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1f544485-5a01-4a4a-ab0f-dcee67e1a38b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '101'
ht-degree: 0%
---
# Especificar configurações de segurança {#specify-security-settings}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Output permite controlar se entidades externas em entradas XML são resolvidas. Por padrão, elas são resolvidas, mas você pode alterar esse comportamento para aumentar a segurança do sistema de formulários do AEM.

**Impedir o processamento de arquivos de dados XML que contêm referências a entidades externas**

1. No console de administração, clique em Serviços > saída.
1. Desmarque a caixa de seleção Resolver entidades externas.
1. Clique em Salvar.
