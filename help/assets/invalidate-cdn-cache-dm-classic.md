---
title: Invalidar o cache da rede de entrega de conteúdo por meio do Dynamic Media Classic
description: Invalidar o conteúdo em cache da CDN (Content Delivery Network) permite atualizar rapidamente os ativos entregues pelo Dynamic Media Classic, em vez de esperar a expiração do cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: e17747bc-9b7b-44e6-a443-f54229a02620
    internal-label: Integrations
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: fc27aefe-8efd-48a6-89bf-c46e0e334a63
    internal-label: CDN cache
  - id: c12bda38-aa1a-4647-b62e-42cd4537dac6
    internal-label: Dynamic Media Classic
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 13%
---
# Invalidar o cache da rede de entrega de conteúdo por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida. No entanto, quando você atualiza um ativo, deseja que essas alterações entrem em vigor imediatamente. Invalidar o conteúdo em cache do CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar a expiração do cache.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao Dynamic Media no Adobe Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) ou anterior.<br>Se você usar o Dynamic Media no Experience Manager 6.5, Service Pack 6 (Experience Manager 6.5.6) ou posterior, siga as etapas encontradas em [Invalidar o cache da CDN por meio do Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar o cache CDN por meio do Dynamic Media Classic:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=pt-BR#system-requirements-dmc-app) e entre na sua conta.

   Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte ao cliente da Adobe.

1. Próximo ao canto superior direito da página, navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]**.
1. Na página Configurações Gerais do Aplicativo, no cabeçalho do grupo Servidores, localize a caixa de texto **[!UICONTROL Modelo de Invalidação de CDN]**.

1. Especifique o modelo usado para invalidar o cache CDN (Content Delivery Network).

   Por exemplo, suponha que você insira uma URL de imagem (incluindo predefinições de imagem ou modificadores) referenciando `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo contiver apenas `<ID>`, o Dynamic Media preencherá `https://<server>/is/image`, onde `<server>` é o Nome do Servidor de Publicação definido em Configurações Gerais e &lt;ID> são os ativos selecionados para serem invalidados.

1. No canto inferior direito da página, selecione **[!UICONTROL Fechar]**.
1. Na interface do usuário do Dynamic Media Classic, selecione um ou mais ativos, depois vá para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**. Você verá uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Nome do servidor publicado&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você vai para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, isso resulta na seguinte URL gerada na interface de usuário de Invalidação da CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa de listagem URL, selecione **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. Você pode editar um URL ou adicionar um URL digitando ou colando-o na caixa de lista de URL; não é necessário definir o Modelo de invalidação CDN antecipadamente.

   Após selecionar **[!UICONTROL Continuar]**, será exibido um indicador que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos e foi para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, cada ativo é referenciado na **[!UICONTROL URL de modelo]** salva. Portanto, você pode definir um **[!UICONTROL Modelo de invalidação CDN]** referenciando cada predefinição de imagem da URL referenciada em seu site (como detalhes do produto e resultados de pesquisa). Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e ir para **[!UICONTROL Arquivo]** > **[!UICONTROL Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com o objetivo de invalidar a partir da Rede de Entrega de Conteúdo (CDN). Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completas à lista **[!UICONTROL Invalidar CDN]**. Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de acessar a opção **[!UICONTROL Arquivo > Invalidar CDN]**.
