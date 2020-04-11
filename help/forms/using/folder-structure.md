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
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Compreensão da estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho do AEM Forms são projetados na arquitetura MVC usando o Backbone. Cada componente tem um arquivo para:

* Modelo, que contém lógica comercial.
* Modelo, que é um arquivo HTML que contém controles de interface.
* Visualização, que atua como uma classe Controller para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e navegue até `/libs/ws/js/runtime/`.

**modelos** contêm modelos de backbone.

**O visualização** contém visualizações de backbone.

**modelos** Contém apenas os modelos HTML para os componentes.

**rotas** Contém rotas universais. A pasta Templates dentro de rotas contém o código HTML e as referências aos componentes.

**services** Contém a interface de serviço para chamar as APIs do servidor Adobe Experience Manager no terminal REST.

**util** Contém utilitários genéricos utilizáveis por vários componentes.
