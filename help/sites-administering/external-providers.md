---
title: Analytics com provedores externos
description: Saiba como configurar sua própria instância de trechos de análise genérica para definir uma nova configuração de serviço.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 9bf818f9-6e33-4557-b2e4-b0d4900f2a05
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Analytics com provedores externos {#analytics-with-external-providers}

O Analytics pode fornecer informações importantes e interessantes sobre como seu site está sendo usado.

Várias configurações prontas para uso estão disponíveis para integração com o serviço apropriado, por exemplo:

* [Adobe Analytics](/help/sites-administering/adobeanalytics.md)
* [Adobe Target](/help/sites-administering/target.md)

Você também pode configurar sua própria instância dos **Trechos de Análise Genérica** para definir uma nova configuração de serviço.

As informações são então coletadas por pequenos fragmentos de código que são adicionados às páginas da Web. Por exemplo:

>[!CAUTION]
>
>Não coloque scripts em `script` tags.

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

Esses snippets permitem que os dados sejam coletados e os relatórios gerados. Os dados reais coletados dependem do provedor e do trecho de código real usado. As estatísticas de exemplo incluem:

* quantos visitantes ao longo do tempo
* quantas páginas visitadas
* termos de pesquisa usados
* landing pages

>[!CAUTION]
>
>O site de demonstração Geometrixx-Outdoors é configurado de forma que os atributos fornecidos nas Propriedades da página sejam anexados ao código fonte html (logo acima da tag final `</html>`) no script `js` correspondente.
>
>Se seu próprio `/apps` não for herdado do componente de página padrão ( `/libs/foundation/components/page`), você (ou seus desenvolvedores) deverão se certificar de que os scripts `js` correspondentes sejam incluídos, por exemplo, incluindo `cq/cloudserviceconfigs/components/servicescomponents` ou usando um mecanismo semelhante.
>
>Sem isso, nenhum dos serviços (Genérico, Analytics, Target e assim por diante) funcionará.

## Criação de um serviço com um trecho genérico {#creating-a-new-service-with-a-generic-snippet}

Para a configuração básica:

1. Abra o console **Ferramentas**.
1. No painel esquerdo, expanda **Configurações do Cloud Service**.
1. Clique duas vezes em **Fragmento de análise genérico** para abrir a página:

   ![Fragmento de análise genérico](assets/analytics_genericoverview.png)

1. Clique em + para adicionar uma nova configuração usando a caixa de diálogo. No mínimo, atribua um nome, por exemplo, Google Analytics:

   ![Criar configuração](assets/analytics_addconfig.png)

1. Clique em **Criar**, a caixa de diálogo de trecho será aberta imediatamente. Cole o trecho apropriado do JavaScript no campo:

   ![Editando o componente](assets/analytics_snippet.png)

1. Clique em **OK** para salvar.

## Usar seu novo serviço nas páginas {#using-your-new-service-on-pages}

Após criar a configuração do serviço, você deve configurar as páginas necessárias para usá-lo:

1. Navegue até a página.
1. Abra as **Propriedades da página** no sidekick e depois a guia **Cloud Service**.
1. Clique em **Adicionar Serviço** e selecione o serviço necessário. Por exemplo, o **trecho de análise genérico**:

   ![Adicionando um serviço de nuvem](assets/analytics_selectservice.png)

1. Clique em **OK** para salvar.
1. Você retornará à guia **Cloud Service**. O **Trecho de Análise Genérico** agora está listado com a mensagem `Configuration reference missing`. Use a lista suspensa para selecionar sua instância de serviço específica. Por exemplo, google-analytics:

   ![Adicionando configuração do serviço de nuvem](assets/analytics_selectspecificservice.png)

1. Clique em **OK** para salvar.

   O trecho agora poderá ser visto se você exibir a Source da página.

   Após um período, é possível exibir as estatísticas coletadas.

   >[!NOTE]
   >
   >Se a configuração for anexada a uma página que tem páginas secundárias, o serviço também será herdado por elas.
