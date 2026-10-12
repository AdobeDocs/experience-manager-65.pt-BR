---
title: Trabalhar com fluxos de trabalho
description: Os fluxos de trabalho no Adobe Experience Manager permitem automatizar uma série de etapas executadas em uma página ou ativo.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%
---
# Trabalhar com fluxos de trabalho{#working-with-workflows}

Os fluxos de trabalho do AEM permitem automatizar uma série de etapas executadas em (uma ou mais) páginas e/ou ativos.

Por exemplo, ao publicar, um(a) editor(a) precisa revisar o conteúdo, antes que o(a) admin do site ative a página. Um fluxo de trabalho que automatiza esse exemplo notifica cada participante quando é hora de executar o trabalho necessário:

1. O(a) autor(a) aplica o fluxo de trabalho à página.
1. Editores(as) recebem um item de trabalho que indica que é necessário revisar o conteúdo da página. Ao terminar, é necessário confirmar que o item de trabalho foi concluído.
1. O administrador do site recebe um item de trabalho que solicita a ativação da página. Ao terminar, é necessário confirmar que o item de trabalho foi concluído.

Normalmente:

* Autores(as) de conteúdo aplicam fluxos de trabalho às páginas e participam de fluxos de trabalho.
* Os fluxos de trabalho usados são específicos para os processos comerciais da organização.

As seguintes páginas abordam:

* [Aplicação de fluxos de trabalho a páginas](/help/sites-authoring/workflows-applying.md)
* [Participar de fluxos de trabalho](/help/sites-authoring/workflows-participating.md)
