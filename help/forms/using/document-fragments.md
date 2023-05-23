---
title: Fragmentos do documento
description: Fragmentos de documento, como Texto, listas, condições e fragmentos de layout, no Gerenciamento de correspondência permitem formar os componentes estáticos, dinâmicos e repetíveis de correspondência do cliente.
uuid: 053a17e5-69a5-463d-af4f-46a86534158f
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 1f48548c-4222-454d-ad16-53da37170de2
feature: Correspondence Management
exl-id: ff3a4cba-a1a6-4fc9-8466-da7f28a74fb5
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 1%

---

# Fragmentos do documento {#document-fragments}

Os fragmentos de documento são partes/componentes reutilizáveis de uma correspondência usando a qual você pode compor Comunicações/letras interativas. Os fragmentos de documento são dos seguintes tipos:

* **Texto**: um ativo de texto é um conteúdo que consiste em um ou mais parágrafos de texto. Um parágrafo pode ser estático ou dinâmico.

   * [Textos em comunicações interativas](/help/forms/using/texts-interactive-communications.md)

* **Condição**: As condições permitem definir qual conteúdo é incluído no momento da criação da correspondência, com base nos dados fornecidos. A condição é descrita em termos de variáveis de controle. Uma variável de controle pode ser um elemento do dicionário de dados ou um espaço reservado.

   * [Condições em comunicações interativas](/help/forms/using/conditions-interactive-communications.md)

* **Lista:** Lista é um grupo de fragmentos de documento, incluindo texto, listas, condições e imagens. A ordem dos elementos da lista pode ser fixa ou editável. Ao criar uma correspondência, você pode usar alguns ou todos os elementos da lista para replicar um padrão reutilizável de elementos.
* **Fragmento de layout**: um fragmento de layout é um layout que pode ser usado com uma ou mais letras. Um fragmento de layout é usado para criar padrões repetíveis, especialmente tabelas dinâmicas. O layout pode conter campos de formulário típicos, como &quot;Endereço&quot; e &quot;Número de referência&quot;. Também contém subformulários vazios que indicam áreas de destino. Os layouts (XDPs) são criados no Designer e, em seguida, são carregados no AEM Forms.
