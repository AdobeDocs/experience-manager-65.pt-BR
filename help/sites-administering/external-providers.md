---
title: Analytics com provedores externos
seo-title: Analytics com provedores externos
description: Saiba mais sobre o Analytics com provedores externos.
seo-description: Saiba mais sobre o Analytics com provedores externos.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
translation-type: tm+mt
source-git-commit: 90c99e527a40bb663d4f32d8746b46cf34a2319f
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 4%

---


# Analytics com provedores externos {#analytics-with-external-providers}

O Analytics pode fornecer informações importantes e interessantes sobre como seu site está sendo usado.

Várias configurações prontas para uso estão disponíveis para integração com o serviço apropriado, por exemplo:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Você também pode configurar sua própria instância dos Trechos **do Analytics** Genérico para definir novas configurações de serviço.

As informações são então coletadas por meio de pequenos trechos de código que são adicionados às páginas da Web. Por exemplo:

>[!CAUTION]
>
>Os scripts não devem estar entre `script` tags.

```
var _gaq = _gaq || [];
_gaq.push(['_setAccount', 'UA-XXXXX-X']);
_gaq.push(['_trackPageview']);

(function() {
    var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'https://www') + '.google-analytics.com/ga.js';
    var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
})();
```

Esses trechos permitem coletar dados e gerar relatórios. Os dados reais coletados dependem do provedor e do trecho de código real usado. As estatísticas de exemplo incluem:

* quantos visitantes ao longo do tempo
* quantas páginas visitaram
* termos de pesquisa usados
* landings page

>[!CAUTION]
>
>O site de demonstração do Geometrixx-Outdoors está configurado de forma que os atributos fornecidos nas Propriedades da página sejam anexados ao código fonte html (logo acima da `</html>` tag de extremidade) no `js` script correspondente.
>
>Se `/apps` não herdar do componente de página padrão ( `/libs/foundation/components/page`), você (ou seus desenvolvedores) precisará verificar se os `js` scripts correspondentes foram incluídos, por exemplo, incluindo `cq/cloudserviceconfigs/components/servicescomponents`, ou usando um mecanismo semelhante.
>
>Sem isso, nenhum dos serviços (Genérico, Analytics, Público alvo etc.) funcionará.

## Criação de um novo serviço com um trecho genérico {#creating-a-new-service-with-a-generic-snippet}

Para a configuração básica:

1. Open the **Tools** console.
1. No painel esquerdo, expanda Configurações de **Cloud Services**.
1. Clique com o duplo no trecho **** Genérico do Analytics para abrir a página:

   ![](assets/analytics_genericoverview.png)

1. Clique em + para adicionar uma nova configuração usando a caixa de diálogo; no mínimo, atribua um nome, por exemplo, análises do google:

   ![](assets/analytics_addconfig.png)

1. Clique em **Criar**, a caixa de diálogo de snippet será aberta imediatamente - cole o snippet javascript apropriado no campo:

   ![](assets/analytics_snippet.png)

1. Clique em **OK** para salvar.

## Usando seu novo serviço em páginas {#using-your-new-service-on-pages}

Depois de criar a configuração de serviço, agora é necessário configurar as páginas necessárias para usá-la:

1. Navegue até a página.
1. Abra as Propriedades **da** página no sidekick e, em seguida, na guia **Cloud Services** .
1. Clique em **Adicionar serviço** e selecione o serviço necessário; por exemplo, o trecho **Genérico do Analytics**:

   ![](assets/analytics_selectservice.png)

1. Clique em **OK** para salvar.
1. Você será redirecionado para a guia **Cloud Services** . O trecho **do Analytics** genérico agora está listado com a mensagem `Configuration reference missing`. Use a lista suspensa para selecionar sua instância de serviço específica; por exemplo google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Clique em **OK** para salvar.

   O snippet agora pode ser visto se você visualização a Origem da página para a página.

   Decorrido um período de tempo adequado, poderá visualização das estatísticas recolhidas.

   >[!NOTE]
   >
   >Se a configuração estiver anexada a uma página que tem páginas secundárias, o serviço também será herdado por elas.
