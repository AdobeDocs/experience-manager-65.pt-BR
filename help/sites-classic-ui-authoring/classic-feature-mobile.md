---
title: Criação de uma página para dispositivos móveis
description: Ao criar uma página para dispositivos móveis, a página será exibida de uma forma que emula o dispositivo móvel. Ao criar a página, será possível alternar entre vários emuladores para ver o que o usuário final verá ao acessá-la.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 58%
---
# Criação de uma página para dispositivos móveis{#authoring-a-page-for-mobile-devices}

Ao criar uma página para dispositivos móveis, a página será exibida de uma forma que emula o dispositivo móvel. Ao criar a página, será possível alternar entre vários emuladores para ver o que o usuário final verá ao acessá-la.

Os dispositivos são agrupados nas recurso de categorias, inteligente e de toque, de acordo com as capacidades dos dispositivos que renderizarão a página. Quando o usuário final acessa uma página para dispositivos móveis, o AEM detectará o dispositivo e enviará a representação que corresponde ao seu grupo de dispositivos.

>[!NOTE]
>
>Para criar um site para dispositivos móveis com base em um site padrão já existente, crie uma live copy do site padrão. (Consulte [Criação de uma Live Copy para diferentes canais](/help/sites-administering/msm-livecopy.md).)
>
>Os desenvolvedores do AEM podem criar novos grupos de dispositivos. (Consulte [Criando Filtros de Grupos de Dispositivos.](/help/sites-developing/groupfilters.md))

Use o procedimento a seguir para criar uma página para dispositivos móveis:

1. No navegador, vá para o console **Siteadmin**.
1. Abra a página **Produtos** abaixo de **Sites** >> **Site de demonstração do Geometrixx Mobile** >> **Inglês**.

1. Alternar para um emulador diferente. Para fazer isso, é possível:

   * Clique no ícone do dispositivo na parte superior da página.
   * Clique no botão **Editar** no **Sidekick** e selecione o dispositivo no menu suspenso.

1. Arraste e solte o componente **Texto e Imagem** da guia Dispositivo móvel do Sidekick para a página.
1. Edite o componente e adicione texto. Clique em **OK** para salvar as alterações.

A página tem a mesma aparência do seguinte:

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Os emuladores são desativados quando uma página na instância de criação é solicitada em um dispositivo móvel. A criação pode ser feita usando a interface habilitada para toque.
