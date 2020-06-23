---
title: Invalidação do conteúdo em cache do CDN
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 29%

---


# Invalidação do conteúdo em cache do CDN {#invalidating-your-cdn-cached-content}

Os ativos Dynamic Media são armazenados em cache pelo CDN para delivery rápido. No entanto, ao fazer atualizações em um ativo, você pode desejar que essas alterações entrem em vigor imediatamente. A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.

Consulte também Visão geral do [cache no Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o conteúdo em cache CDN:**

1. Faça logon em sua conta do Dynamic Media Classic (Scene7):

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Suas credenciais e logon foram fornecidos pela Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]**
1. Na página Configurações gerais do aplicativo, no cabeçalho do grupo Servidores, localize a caixa de texto Modelo **[!UICONTROL de invalidação]** CDN.

1. Especifique o modelo usado para invalidar o cache CDN (Rede de Delivery de Conteúdo).

   Por exemplo, suponha que você insira um URL de imagem (incluindo predefinições ou modificadores de imagem) referenciando `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo apenas contiver `<ID>`, a Dynamic Media preencherá `https://<server>/is/image` onde está `<server>` o Nome do Servidor de Publicação definido em Configurações Gerais e &lt;ID> são os ativos selecionados para invalidação.

1. In the lower-right corner of the page, click **[!UICONTROL Close.]**
1. Na interface do usuário do Dynamic Media Classic (Scene7), selecione um ou mais ativos e clique em **[!UICONTROL Arquivo > Invalidar CDN.]** Você verá uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Published Server Name&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de Invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você clica em **[!UICONTROL Arquivo > Invalidar CDN]** , isso resulta no seguinte URL gerado na interface do usuário de Invalidação CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa lista do URL, clique em **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. Observe que é possível editar um URL ou adicioná-lo digitando-o ou colando-o na caixa lista do URL; não é necessário definir CDN Invalidate Template antecipadamente.

   Depois de clicar em **[!UICONTROL Continuar]**, um indicador é exibido que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos e clicou em **[!UICONTROL Arquivo > Invalidar CDN]**, cada ativo é referenciado no **[!UICONTROL URL de modelo salvo.]** Portanto, você pode definir um **[!UICONTROL Modelo de invalidação CDN]** referenciando cada predefinição de imagem do URL referenciada em seu site (como detalhes do produto, resultados de pesquisa e assim por diante). Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e, em seguida, clicar em **[!UICONTROL Arquivo > Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com o objetivo de invalidar a partir da Rede de fornecimento de conteúdo (CDN). Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completos à lista **[!UICONTROL Invalidar CDN]** . Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a opção **[!UICONTROL Arquivo > Invalidar CDN]** .

