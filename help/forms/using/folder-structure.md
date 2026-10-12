---
title: Como entender a estrutura de pastas
description: Como entender a estrutura de pastas do código-fonte do espaço de trabalho do AEM Forms para personalizar.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%
---
# Como entender a estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho do AEM Forms foram projetados na arquitetura MVC usando o Backbone (rede de transmissão). Cada componente tem um arquivo para:

* Modelo, que contém lógica de negócios.
* Modelo, que é um arquivo HTML contendo controles de interface.
* Exibição, que atua como uma classe Controlador para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e navegue até `/libs/ws/js/runtime/`.

**templates** Contém modelos de backbone.

**exibições** contém exibições de backbone.

**modelos** Contém apenas os modelos HTML para os componentes.

**rotas** contém rotas universais. A pasta Templates dentro de rotas contém o código HTML e as referências aos componentes.

**services** Contém interface de serviço para chamar APIs de servidor do Adobe Experience Manager no ponto de extremidade REST.

**util** Contém utilitários genéricos utilizáveis por vários componentes.
