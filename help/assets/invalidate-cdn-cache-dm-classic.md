---
title: Como invalidar o cache CDN por meio do Dynamic Media Classic
description: A invalidação do conteúdo em cache CDN (Content Delivery Network) permite que você atualize rapidamente os ativos entregues pelo Dynamic Media Classic, em vez de aguardar a expiração do cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 996780c3fac85f0ce0deeddd5ff4e74e01df436e
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 17%

---


# Invalidar o cache CDN por meio do Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Os ativos Dynamic Media são armazenados em cache pela CDN (Content Delivery Network, Rede de conteúdo) para delivery rápido. No entanto, quando você faz atualizações em um ativo, deseja que essas alterações entrem em vigor imediatamente. A invalidação do conteúdo em cache do CDN permite atualizar rapidamente ativos entregues pela Dynamic Media, em vez de aguardar a expiração do cache.

>[!NOTE]
>
>Este recurso exige que você use o CDN pronto para uso fornecido com a Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é suportado com este recurso.

>[!IMPORTANT]
>
>As etapas a seguir se aplicam apenas à Dynamic Media no AEM 6.5, Service Pack 5 (AEM 6.5.5) ou anterior.<br>Se você usar o Dynamic Media no AEM 6.5, Service Pack 6 (AEM 6.5.6) ou posterior, siga as etapas encontradas em  [Invalidar o cache CDN por meio do Dynamic Media.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

Consulte também [Visão geral do cache no Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar o cache CDN por meio do Dynamic Media Classic:**

1. Abra o [aplicativo Dynamic Media Classic para desktop](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app) e faça logon em sua conta.

   Suas credenciais e logon foram fornecidos pelo Adobe no momento do provisionamento. Se você não tiver essas informações, entre em contato com o Suporte Técnico.

1. Próximo ao canto superior direito da página, toque em **[!UICONTROL Configuração > Configuração de Aplicativo > Configurações Gerais.]**
1. Na página Configurações gerais do aplicativo, no cabeçalho do grupo Servidores, localize a caixa de texto **[!UICONTROL Modelo de invalidação CDN]**.

1. Especifique o modelo usado para invalidar o cache CDN (Rede de Delivery de Conteúdo).

   Por exemplo, suponha que você insira um URL de imagem (incluindo predefinições ou modificadores de imagem) referenciando `<ID>`, em vez de uma ID de imagem específica, como no exemplo a seguir:

   `https://server.com/is/image/Company/<ID>?$product$`

   Se o Modelo contiver apenas `<ID>`, a Dynamic Media preencherá `https://<server>/is/image`, onde `<server>` é o Nome do Servidor de Publicação definido em Configurações Gerais, e &lt;ID> serão os ativos selecionados para invalidação.

1. No canto inferior direito da página, clique em **[!UICONTROL Fechar.]**
1. Na interface do usuário do Dynamic Media Classic, selecione um ou mais ativos e clique em **[!UICONTROL Arquivo > Invalidar CDN.]** Você verá uma lista de um ou mais URLs gerados a partir do modelo criado e dos ativos selecionados. Ele usa o URL do servidor listado em &quot;Published Server Name&quot; nas Configurações gerais do aplicativo.

   Por exemplo, com o Modelo de Invalidação CDN definido na etapa anterior, suponha que você tenha selecionado uma única imagem de ativo de imagem chamada `Backpack_B`. Quando você toca em **[!UICONTROL Arquivo > Invalidar CDN]**, isso resulta no seguinte URL gerado na interface do usuário de Invalidação CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Na caixa lista do URL, toque em **[!UICONTROL Continuar]** para limpar o cache de cada URL específico. É possível editar um URL ou adicioná-lo digitando-o ou colando-o na caixa lista do URL; não é necessário definir CDN Invalidate Template antecipadamente.

   Após clicar em **[!UICONTROL Continuar]**, um indicador é exibido que fornece uma estimativa de quanto tempo levará para limpar o cache.

   Se você selecionou vários ativos, depois tocou em **[!UICONTROL Arquivo > Invalidar CDN]**, cada ativo é referenciado no URL do modelo **[!UICONTROL salvo.]** Portanto, você pode definir um  **[!UICONTROL CDN Invalidate]** Templaterereferenciando cada predefinição de imagem de URL referenciada em seu site (como detalhes do produto e resultados de pesquisa). Em seguida, ao selecionar uma ou mais imagens para invalidação do cache, os URLs preenchem automaticamente a interface.

   >[!NOTE]
   >
   >Ao selecionar ativos e, em seguida, clicar em **[!UICONTROL Arquivo > Invalidar CDN]**, o Dynamic Media usa um modelo CDN de invalidação para criar URLs automaticamente com o objetivo de invalidar a partir da Rede de fornecimento de conteúdo (CDN). Se não houver nada na caixa de texto **[!UICONTROL Invalidar modelo CDN]**, você receberá uma lista de URLs em branco. O armazenamento em cache na CDN não se baseia em ativos, ele é baseado em URL. Portanto, é necessário estar ciente de todos os URLs que estão em seu site. Depois de determinar esses URLs, você pode adicioná-los à caixa de texto **[!UICONTROL Invalidar modelo CDN]** anteriormente nas etapas. Em seguida, selecione esses ativos e invalide os URLs em uma etapa.
   >
   >Outra opção é adicionar URLs completos à lista **[!UICONTROL Invalidar CDN]**. Se você seguir essa abordagem, não será necessário selecionar ativos no Dynamic Media Classic antes de ir para a opção **[!UICONTROL Arquivo > Invalidar CDN]**.

