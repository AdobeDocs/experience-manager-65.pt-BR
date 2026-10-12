---
title: Fragmentos do documento
description: Fragmentos de documento, como Texto, listas, condições e fragmentos de layout, no Gerenciamento de correspondência permitem formar os componentes estáticos, dinâmicos e repetíveis de correspondência do cliente.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: ff3a4cba-a1a6-4fc9-8466-da7f28a74fb5
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 3f00fc92-85ee-583e-abd1-3bc3d96de3a0
    internal-label: Correspondence Management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%
---
# Fragmentos do documento {#document-fragments}

Os fragmentos de documento são partes/componentes reutilizáveis de uma correspondência usando a qual você pode compor Comunicações/letras interativas. Os fragmentos de documento são dos seguintes tipos:

* **Texto**: um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.

  * [Textos em comunicações interativas](/help/forms/using/texts-interactive-communications.md)

* **Condição**: as condições permitem que você defina qual conteúdo será incluído no momento da criação da correspondência, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. Uma variável de controle pode ser um elemento do dicionário de dados ou um espaço reservado.

  * [Condições em comunicações interativas](/help/forms/using/conditions-interactive-communications.md)

* **Lista:** Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens. A ordem dos elementos da lista pode ser fixa ou editável. Ao criar uma correspondência, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos.
* **Fragmento de layout**: um fragmento de layout é um layout que pode ser usado em uma ou mais letras. Um fragmento de layout é usado para criar padrões repetíveis, especialmente tabelas dinâmicas. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Os layouts (XDPs) são criados no Designer e, em seguida, são carregados no AEM Forms.
