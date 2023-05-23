---
title: Ativação da proteção de hot link no Dynamic Media
description: Informações sobre como ativar a proteção de hot link no Dynamic Media.
uuid: 5f93bc27-5edd-4143-8701-87896c52f0af
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: a70aa448-0f58-4ed2-9381-afcc76fa827f
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
source-git-commit: 65af6e33ae3897519491952f4d3a6832700f77b2
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 2%

---

# Ativar a proteção de hot link no Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Hot linking é quando um site de terceiros usa o código HTML para exibir uma imagem do seu site. Eles usam a largura de banda sempre que a foto é solicitada porque o navegador do visitante está acessando-a diretamente do seu servidor. Hotlink *proteção* é um método para impedir que outros sites vinculem diretamente a imagens, CSS ou JavaScript nas suas páginas da Web. Esse tipo de blindagem ajuda a reduzir o uso desnecessário de largura de banda na sua conta do Dynamic Media.

[Suporte ao cliente Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&amp;lang=pt-BR#support) O pode configurar um filtro de referenciador no nível CDN (Content Delivery Network) para que o conteúdo do Dynamic Media seja enviado somente aos sites da lista de sites permitidos para o domínio.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso. Para ativar a proteção de hot link, um administrador precisa criar um tíquete de suporte ao cliente do Adobe para solicitar a alteração de configuração em sua conta da Dynamic Media. Não há custo adicional para ativar a proteção de hot link.
