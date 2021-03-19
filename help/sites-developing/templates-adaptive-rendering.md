---
title: Renderização do modelo adaptável
seo-title: Renderização do modelo adaptável
description: Renderização do modelo adaptável
seo-description: 'null'
uuid: 97226ae1-e42a-40ae-a5e0-886cd77559d8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: f5cb0e98-0d6e-4f14-9b94-df1a9d8cbe5b
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---


# Renderização do modelo adaptável{#adaptive-template-rendering}

A renderização do modelo adaptável fornece uma maneira de gerenciar uma página com variações. Originalmente útil para fornecer várias saídas HTML para dispositivos móveis (por exemplo, telefone de recurso vs. smartphone), esse recurso é útil quando experiências precisam ser entregues a vários dispositivos que precisam de marcação ou saída HTML diferente.

## Visão geral {#overview}

Em geral, os modelos são criados em torno de uma grade responsiva e as páginas criadas com base nesses modelos são totalmente responsivas, ajustando-se automaticamente à janela de visualização do dispositivo cliente. Usando a barra de ferramentas Emulador no editor de páginas, os autores podem direcionar layouts para dispositivos específicos.

Também é possível configurar templates para suportar renderização adaptável. Quando os grupos de dispositivos são configurados corretamente, a página é renderizada com um seletor diferente no URL ao selecionar um dispositivo no modo emulador. Usando um seletor, uma renderização de página específica pode ser chamada diretamente pelo URL.

Lembre-se ao configurar os grupos de dispositivos:

* Cada dispositivo deve estar em pelo menos um grupo de dispositivos.
* Um dispositivo pode estar em vários grupos de dispositivos.
* Como os dispositivos podem estar em vários grupos de dispositivos, os seletores podem ser combinados.
* A combinação de seletores é avaliada de cima para baixo, pois são persistentes no repositório.

>[!NOTE]
>
>O grupo de dispositivos **Dispositivos responsivos** nunca terá um seletor porque os dispositivos reconhecidos como compatíveis com o design responsivo não precisam de um layout adaptável

## Configuração {#configuration}

Os seletores de renderização adaptáveis podem ser configurados para grupos de dispositivos existentes ou para [grupos que você mesmo criou.](/help/sites-developing/mobile.md#device-groups)

Neste exemplo, vamos configurar o grupo de dispositivos existente **Smart Phones** para ter um seletor de renderização adaptável como parte do modelo **Experience Page** no We.Retail.

1. Edite o grupo de dispositivos que requer um seletor adaptável em `http://localhost:4502/miscadmin#/etc/mobile/groups`

   Defina a opção **Desativar emulador** e salve.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. O seletor estará disponível para o **Blackberry** e **iPhone 4** desde que o grupo de dispositivos **Smart Phone** seja adicionado ao modelo e às estruturas de página nas etapas a seguir.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Usando o CRX DE Lite, permita que o grupo de dispositivos seja usado no modelo, adicionando-o à propriedade de sequência de caracteres de vários valores `cq:deviceGroups` na estrutura do modelo.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Por exemplo, se desejarmos adicionar o grupo de dispositivos do Smart Phone:

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Usando o CRX DE Lite, permita que o grupo de dispositivos seja usado em seu site, adicionando-o à propriedade de sequência de caracteres de vários valores `cq:deviceGroups` na estrutura de seu site.

   `/content/<your-site>/jcr:content`

   Por exemplo, se queremos permitir o grupo de dispositivos **Telefone inteligente**:

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Agora, ao usar o [emulador](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) no editor de páginas (como quando [modificar o layout](/help/sites-authoring/responsive-layout.md)) e escolher um dispositivo do grupo de dispositivos configurado, a página será renderizada com um seletor como parte do URL.

Em nosso exemplo, ao editar uma página com base no modelo **Página de experiência** e escolher iPhone 4 no emulador, a página é renderizada, incluindo o seletor como `arctic-surfing-in-lofoten.smart.html` em vez de `arctic-surfing-in-lofoten.html`

A página também pode ser chamada diretamente usando esse seletor.

![chlimage_1-161](assets/chlimage_1-161.png)

