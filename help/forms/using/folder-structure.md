---
title: Noções básicas sobre a estrutura de pastas
seo-title: Understanding the folder structure
description: Como entender a estrutura de pastas do código-fonte do espaço de trabalho do AEM Forms para personalizar.
seo-description: How to understand the folder structure of AEM Forms workspace source code to customize.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Noções básicas sobre a estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho do AEM Forms são projetados na arquitetura MVC usando Backbone. Cada componente tem um arquivo para:

* Modelo, que contém lógica de negócios.
* Modelo, que é um arquivo HTML contendo controles de interface.
* Exibir, que atua como uma classe Controladora para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e navegue até `/libs/ws/js/runtime/`.

**modelos** Contém modelos de backbone.

**exibições** Contém visualizações de backbone.

**modelos** Contém apenas os modelos HTML para os componentes.

**rotas** Contém rotas universais. A pasta Modelos nas rotas contém o código HTML e as referências aos componentes.

**serviços** Contém a interface de serviço para chamar APIs do servidor do Adobe Experience Manager no terminal REST.

**util** Contém utilitários genéricos utilizáveis por vários componentes.
