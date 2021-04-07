---
title: Invalidar o cache CDN por meio do Dynamic Media Classic
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite atualizar rapidamente os ativos entregues pelo Dynamic Media Classic, em vez de esperar que o cache expire.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Cache CDN,Dynamic Media Classic
role: Business Practitioner, Administrator
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 16%

---

# Invalidar o cache CDN por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos do Dynamic Media são armazenados em cache pela CDN (Content Delivery Network) para entrega rápida. No entanto, quando você faz atualizações em um ativo, deseja que essas alterações entrem em vigor imediatamente. A invalidação do conteúdo em cache do CDN permite atualizar rapidamente os ativos entregues pelo Dynamic Media, em vez de esperar que o cache expire.

>[!NOTE]
>
>Esse recurso exige que você use a CDN predefinida fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam somente ao Dynamic Media no AEM 6.5, Service Pack 5 (AEM 6.5.5) ou anterior.<br>Se você usar o Dynamic Media no AEM 6.5, Service Pack 6 (AEM 6.5.6) ou posterior, siga as etapas encontradas em  [Invalidar o cache CDN por meio do Dynamic Media.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

Consulte também [Visão geral do cache no Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o cache CDN por meio do Dynamic Media Classic:**

1. Abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app) e faça logon em sua conta.

   Suas credenciais e logon foram fornecidas pelo Adobe no momento do provisionamento. Caso não tenha essas informações, entre em contato com o Suporte Técnico.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]**
1. Na página Configurações gerais do aplicativo , no cabeçalho do grupo Servidores , localize a caixa de texto **[!UICONTROL Modelo de invalidação CDN]** .

1. Especifique o modelo que é usado para invalidar o cache CDN (Content Delivery Network).

   Por exemplo, suponha que você insira um URL de imagem (incluindo predefinições ou modificadores de imagem) que faça referência a `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo contiver apenas `<ID>`, o Dynamic Media preencherá `https://<server>/is/image`, onde `<server>` é o Nome do Servidor de Publicação definido nas Configurações Gerais e &lt;ID> será o ativo selecionado para invalidação.

1. No canto inferior direito da página, clique em **[!UICONTROL Fechar.]**
1. Na interface do usuário do Dynamic Media Classic, selecione um ou mais ativos e clique em **[!UICONTROL Arquivo > Invalidar CDN.]** Você vê uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Nome do servidor publicado&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de Invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Ao tocar em **[!UICONTROL File > Invalidate CDN]**, o resultado é o seguinte URL gerado na interface do usuário de Invalidação CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa de listagem URL, toque em **[!UICONTROL Continue]** para limpar o cache de cada URL específico. Você pode editar um URL ou adicionar um URL digitando-o ou colando-o na caixa de listagem do URL; não é necessário definir o Modelo de Invalidação CDN antecipadamente.

   Depois de clicar em **[!UICONTROL Continuar]**, é exibido um indicador que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos e tocou em **[!UICONTROL File > Invalidate CDN]**, cada ativo é referenciado no URL de modelo **[!UICONTROL salvo.]** Portanto, você pode definir um  **[!UICONTROL modelo de invalidação]** CDN referenciando cada predefinição de imagem do URL referenciada em seu site (como detalhes do produto e resultados de pesquisa). Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e, em seguida, clicar em **[!UICONTROL Arquivo > Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com o objetivo de invalidar a partir da Rede de fornecimento de conteúdo (CDN). Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completos à lista **[!UICONTROL Invalidar CDN]**. Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a opção **[!UICONTROL File > Invalidate CDN]** .
