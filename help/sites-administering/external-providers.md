---
title: Analytics com provedores externos
seo-title: Analytics with External Providers
description: Saiba mais sobre o Analytics com provedores externos.
seo-description: Learn about Analytics with External Providers.
uuid: 31a773ca-901e-45f2-be8f-951c26f9dbc5
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: bab465bc-1ff4-4f21-9885-e4a875c73a8d
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 4%

---

# Analytics com provedores externos {#analytics-with-external-providers}

O Analytics pode fornecer informações importantes e interessantes sobre como seu site está sendo usado.

Várias configurações prontas para uso estão disponíveis para integração com o serviço apropriado, por exemplo:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Você também pode configurar sua própria instância do **Trechos Genéricos do Analytics** para definir novas configurações de serviço.

As informações são coletadas por meio de pequenos trechos de código adicionados às páginas da Web. Por exemplo:

>[!CAUTION]
>
>Os scripts não devem ser colocados em `script` tags.

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

Esses trechos permitem que os dados sejam coletados e os relatórios sejam gerados. Os dados reais coletados dependem do provedor e do snippet de código real usado. As estatísticas de exemplo incluem:

* quantos visitantes ao longo do tempo
* quantas páginas visitaram
* termos de pesquisa usados
* páginas de aterrissagem

>[!CAUTION]
>
>O site de demonstração Geometrixx-Outdoors é configurado para que os atributos fornecidos nas Propriedades da página sejam anexados ao código fonte html (logo acima da função `</html>` endtag) no `js` script.
>
>Se seu próprio `/apps` não herdar do componente de página padrão ( `/libs/foundation/components/page`) você (ou seus desenvolvedores) deve garantir que o `js` scripts são incluídos, por exemplo, por meio de `cq/cloudserviceconfigs/components/servicescomponents`ou utilizar um mecanismo semelhante.
>
>Sem isso, nenhum dos serviços (Genérico, Analytics, Target etc.) funcionará.

## Criando um novo serviço com um trecho genérico {#creating-a-new-service-with-a-generic-snippet}

Para a configuração básica:

1. Abra o **Ferramentas** console.
1. No painel esquerdo, expanda **Configurações do Cloud Services**.
1. Clique duas vezes em **Snippet genérico do Analytics** para abrir a página:

   ![](assets/analytics_genericoverview.png)

1. Clique em + para adicionar uma nova configuração usando a caixa de diálogo; no mínimo, atribua um nome, por exemplo, google analytics:

   ![](assets/analytics_addconfig.png)

1. Clique em **Criar**, a caixa de diálogo do snippet será aberta imediatamente - cole o snippet do javascript apropriado no campo :

   ![](assets/analytics_snippet.png)

1. Clique em **OK** para salvar.

## Usar seu novo serviço em páginas {#using-your-new-service-on-pages}

Depois de criar a configuração de serviço, agora é necessário configurar as páginas necessárias para usá-la:

1. Navegue até a página .
1. Abra o **Propriedades da página** do sidekick, em seguida, o **Cloud Services** guia .
1. Clique em **Adicionar Serviço**, em seguida, selecione o serviço necessário; por exemplo, a variável **Snippet genérico do Analytics**:

   ![](assets/analytics_selectservice.png)

1. Clique em **OK** para salvar.
1. Você será retornado ao **Cloud Services** guia . O **Snippet genérico do Analytics** está listada com a mensagem `Configuration reference missing`. Use a lista suspensa para selecionar sua instância de serviço específica; por exemplo, google-analytics:

   ![](assets/analytics_selectspecificservice.png)

1. Clique em **OK** para salvar.

   O trecho agora pode ser visto se você visualizar a Fonte da página da página.

   Após um período adequado, você poderá visualizar as estatísticas coletadas.

   >[!NOTE]
   >
   >Se a configuração for anexada a uma página que tem páginas filhas, o serviço também será herdado por elas.
