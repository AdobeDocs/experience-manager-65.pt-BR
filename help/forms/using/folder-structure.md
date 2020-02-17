---
title: Compreensão da estrutura de pastas
seo-title: Compreensão da estrutura de pastas
description: Como entender a estrutura de pastas do código-fonte da área de trabalho do AEM Forms para personalizar.
seo-description: Como entender a estrutura de pastas do código-fonte da área de trabalho do AEM Forms para personalizar.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Compreensão da estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho do AEM Forms são projetados na arquitetura MVC usando Backbone. Cada componente tem um arquivo para:

* Modelo, que contém lógica comercial.
* Modelo, que é um arquivo HTML que contém controles de interface.
* Exibir, que atua como uma classe Controladora para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e navegue até `/libs/ws/js/runtime/`.

**modelos** contêm modelos de backbone.

**exibições** Contém exibições de backbone.

**modelos** Contém apenas os modelos HTML para os componentes.

**rotas** contém rotas universais. A pasta Templates dentro de rotas contém o código HTML e as referências aos componentes.

**services** Contém interface de serviço para chamar as APIs do servidor Adobe Experience Manager no terminal REST.

**util** Contém utilitários genéricos utilizáveis por vários componentes.

**[Contate o suporte](https://www.adobe.com/account/sign-in.supportportal.html)**
