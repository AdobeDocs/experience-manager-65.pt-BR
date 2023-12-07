---
title: Como entender a estrutura de pastas
description: Como entender a estrutura de pastas do código-fonte do espaço de trabalho do AEM Forms para personalizar.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: a4c1d3d8-477e-4edf-9dde-4ef9c766be5a
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Como entender a estrutura de pastas {#understanding-the-folder-structure}

Os componentes do espaço de trabalho do AEM Forms foram projetados na arquitetura MVC usando o Backbone (rede de transmissão). Cada componente tem um arquivo para:

* Modelo, que contém lógica de negócios.
* Modelo, que é um arquivo HTML contendo controles de interface.
* Exibição, que atua como uma classe Controlador para Modelo.

Os ativos de todos os componentes são colocados na estrutura de pastas descrita abaixo. Para acessar os ativos, faça logon no CRXDE Lite e procure `/libs/ws/js/runtime/`.

**modelos** Contém modelos de backbone.

**visualizações** Contém exibições de backbone.

**modelos** Contém apenas os modelos de HTML para os componentes.

**roteiros** Contém rotas universais. A pasta Templates dentro de rotas contém o código HTML e as referências aos componentes.

**serviços** Contém a interface de serviço para chamar as APIs do servidor do Adobe Experience Manager no ponto de extremidade REST.

**util** Contém utilitários genéricos utilizáveis por vários componentes.
