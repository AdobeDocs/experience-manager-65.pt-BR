---
title: Criação de uma página de conteúdo para dispositivos móveis
description: Ao criar para dispositivos móveis, você pode alternar entre vários emuladores para ver o que o usuário final vê.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 63%
---
# Criação de uma página para dispositivos móveis{#authoring-a-page-for-mobile-devices}

Ao criar uma página para dispositivos móveis, a página será exibida de uma forma que emula o dispositivo móvel. Ao criar a página, será possível alternar entre vários emuladores para ver o que o usuário final verá ao acessá-la.

Os dispositivos são agrupados nas recurso de categorias, inteligente e de toque, de acordo com as capacidades dos dispositivos que renderizarão a página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detectará o dispositivo e enviará a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site para dispositivos móveis com base em um site padrão já existente, crie uma live copy do site padrão. (Consulte [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (Consulte [Criando Filtros de Grupos de Dispositivos](/help/sites-developing/groupfilters.md).)

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. Na navegação global, abra o console **Sites**.
1. Abra a página **We.Retail** > **Estados Unidos** > **Inglês**.

1. Alternar para o modo **Visualização**.
1. Alterne para o emulador desejado, clicando no ícone de dispositivo na parte superior da página.
1. Arraste e solte componentes do navegador de componentes para a página.

A página é semelhante ao seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de criação é solicitada em um dispositivo móvel.
