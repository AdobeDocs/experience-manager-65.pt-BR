---
title: Compreensão da estrutura de pastas
seo-title: Compreensão da estrutura de pastas
description: Como entender a estrutura de pastas do código-fonte da área de trabalho do AEM Forms a ser personalizada.
seo-description: Como entender a estrutura de pastas do código-fonte da área de trabalho do AEM Forms a ser personalizada.
uuid: ee844f89-887e-4f07-9db3-389859baa374
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 7427858d-8eec-423d-a0a9-444140420620
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Compreensão da estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho AEM Forms são projetados na arquitetura MVC usando backbone. Cada componente tem um arquivo para:

* Modelo, que contém lógica comercial.
* Modelo, que é um arquivo HTML que contém controles de interface.
* Visualização, que atua como uma classe Controller para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e navegue até `/libs/ws/js/runtime/`.

**** ModelosContém modelos de backbone.

**** viewsContém visualizações de backbone.

**** ModelosContém apenas os modelos HTML para os componentes.

**** rotasContém rotas universais. A pasta Templates dentro de rotas contém o código HTML e as referências aos componentes.

**** servicesContém a interface de serviço para chamar APIs do servidor Adobe Experience Manager no terminal REST.

**** utilContém utilitários genéricos utilizáveis por vários componentes.
