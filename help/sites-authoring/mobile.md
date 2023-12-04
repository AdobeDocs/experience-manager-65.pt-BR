---
title: Criação de uma página de conteúdo para dispositivos móveis
description: Ao criar para dispositivos móveis, você pode alternar entre vários emuladores para ver o que o usuário final vê.
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 63%

---

# Criação de uma página para dispositivos móveis  {#authoring-a-page-for-mobile-devices}

Ao criar uma página para dispositivos móveis, a página será exibida de uma forma que emula o dispositivo móvel. Ao criar a página, será possível alternar entre vários emuladores para ver o que o usuário final verá ao acessá-la.

Os dispositivos são agrupados nas recurso de categorias, inteligente e de toque, de acordo com as capacidades dos dispositivos que renderizarão a página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detectará o dispositivo e enviará a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site para dispositivos móveis com base em um site padrão já existente, crie uma live copy do site padrão. (Consulte [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (Consulte [Criando filtros do grupo de dispositivos](/help/sites-developing/groupfilters.md).)

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. Na navegação global, abra o console **Sites**.
1. Abrir a página **We.Retail** > **Estados Unidos** > **Inglês**.

1. Alternar para **Visualizar** modo.
1. Alterne para o emulador desejado, clicando no ícone de dispositivo na parte superior da página.
1. Arraste e solte componentes do navegador de componentes para a página.

A página é semelhante ao seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de autor é solicitada em um dispositivo móvel.
