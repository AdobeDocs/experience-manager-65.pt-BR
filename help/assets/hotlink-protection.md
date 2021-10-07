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
ht-degree: 0%

---

# Ativar a proteção de hotlink no Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Hot linking é quando um site de terceiros usa o código de HTML para exibir uma imagem de seu site. Eles usam sua largura de banda toda vez que a imagem é solicitada, pois o navegador do visitante a está acessando diretamente do seu servidor. Hotlink *protection* é um método para impedir que outros sites vinculem diretamente a imagens, CSS ou JavaScript nas suas páginas da Web. Esse tipo de blindagem ajuda a reduzir o uso desnecessário da largura de banda em sua conta do Dynamic Media.

[O ](https://experienceleague.adobe.com/?support-solution=Experience+Manager#support) Suporte ao cliente do Experience Manager pode configurar um filtro de referenciador no nível da CDN (Content Delivery Network) para que o conteúdo do Dynamic Media seja enviado somente aos sites da sua lista de sites permitidos para o domínio.

>[!NOTE]
>
>Esse recurso exige que você use a CDN predefinida fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso. Para ativar a proteção de hotlink, um administrador deve criar um tíquete de suporte ao cliente do Adobe para solicitar a alteração da configuração na sua conta do Dynamic Media. Não há custo adicional para ativar a proteção de hot link.
