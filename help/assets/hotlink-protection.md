---
title: Ativação da proteção de hot link no Dynamic Media
description: Informações sobre como ativar a proteção de hot link no Dynamic Media.
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
role: User, Admin
exl-id: 698e8bdb-9b31-49ab-8560-26b05109bb23
feature: Configuration
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: da0dfbce-df02-4f8b-b32d-a4e3b1d05085
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 3%
---
# Ativar a proteção de hot link no Dynamic Media {#activating-hotlink-protection-in-dynamic-media}

Hot linking é quando um site de terceiros usa o código HTML para exibir uma imagem do seu site. Eles usam a largura de banda sempre que a foto é solicitada porque o navegador do visitante está acessando-a diretamente do seu servidor. A *proteção* do Hotlink é um método para impedir que outros sites vinculem diretamente a imagens, CSS ou JavaScript em suas páginas da Web. Esse tipo de blindagem ajuda a reduzir o uso desnecessário da largura de banda na conta do Dynamic Media.

O [Suporte ao Cliente do Experience Manager](https://experienceleague.adobe.com/?support-solution=Experience+Manager&lang=pt-BR#support) pode configurar um filtro de referenciador no nível da CDN (Content Delivery Network) para que o conteúdo do Dynamic Media seja enviado somente aos sites da sua lista de sites permitidos para o domínio.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso. Para ativar a proteção de hot link, um administrador precisa criar um tíquete de suporte ao cliente da Adobe para solicitar a alteração de configuração em sua conta do Dynamic Media. Não há custo adicional para ativar a proteção de hot link.
