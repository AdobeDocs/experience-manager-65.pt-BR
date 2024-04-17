---
title: Perguntas frequentes sobre entrega de conteúdo HTTP2
description: Saiba mais sobre a entrega de conteúdo HTTP2 e como ela pode aumentar o desempenho geral do seu conteúdo da Web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# Perguntas frequentes sobre entrega de conteúdo HTTP2{#http-delivery-of-content-faq}

A Adobe está animada em anunciar a disponibilidade da entrega de conteúdo HTTP/2. Quando você usa HTTP/2, percebe um aumento geral no desempenho.

## O que é HTTP/2? {#what-is-http}

HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de poder de processamento necessária.

O site a seguir descreve o HTTP/2 e seus benefícios de maneira breve e simples:

[O que você deve saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html).

## Quais são os principais benefícios da migração para HTTP/2 na entrega de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

A melhoria do desempenho varia amplamente com base em fatores como o código do site, como você usa o Dynamic Media, o dispositivo, a tela e a localização do cliente.

Os próprios testes de Adobe produziram os seguintes resultados:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram em dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou em 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso mudar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use a CDN (content delivery network) agrupada em Adobe como parte de sua licença do Dynamic Media.
* Use um domínio dedicado (ou seja, `images.company.com` ou `mycompany.scene7.com`), não um domínio Dynamic Media genérico (ou seja, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

  Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa. Em seguida, acesse **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**. Procure o campo rotulado **Nome do servidor publicado**. Se você estiver usando um domínio Dynamic Media genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

## Qual é o processo de habilitação do HTTP/2 para minha conta do Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Use o Admin Console para criar um caso de suporte](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html?lang=pt-BR) e solicitar a mudança para HTTP/2; isso não é feito automaticamente para você.
1. Forneça as seguintes informações no seu caso de suporte:

   * Nome do contato principal, email e número de telefone.
   * Todos os domínios que serão transferidos para HTTP2. Ou seja, `images.company.com` ou `mycompany.scene7.com`.

     Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa. Em seguida, acesse **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**. Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**.

   * Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
   * Verifique se você está usando o CDN por meio do Adobe e se não é gerenciado com um relacionamento direto.
   * Verifique se você está usando um domínio dedicado. Ou seja, `images.company.com` ou `mycompany.scene7.com`, não um domínio genérico do Dynamic Media, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

     Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa. Em seguida, acesse **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**. Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**. Se você estiver usando um domínio Dynamic Media genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

1. O Suporte ao cliente do Adobe adiciona você à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o suporte entrará em contato com você para coordenar a transição e definir uma data limite.
1. Você será notificado após a conclusão e poderá verificar uma transição bem-sucedida para HTTP2.

## Quando posso esperar a transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Suporte ao cliente do Adobe.

>[!NOTE]
>
>O lead time é longo porque a transição para HTTP/2 envolve a limpeza do cache. Portanto, somente algumas transições de clientes podem ser tratadas de cada vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa seu cache na CDN porque envolve a mudança para uma nova configuração de CDN.

O conteúdo não armazenado em cache atinge diretamente os servidores de origem do Adobe até que o cache seja recriado novamente. Por causa dessa ação, o Adobe planeja lidar com algumas transições de cliente de cada vez, para que o desempenho aceitável seja mantido ao extrair solicitações da origem Adobe.

## Como você pode verificar se um URL ou site está ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Baixe uma extensão que você pode usar com o navegador da Web. Para Firefox e Chrome, há uma extensão chamada **[!UICONTROL Indicador HTTP/2 e SPDY]**. Os navegadores só são compatíveis com HTTP/2 de forma segura, portanto, é necessário chamar um URL com HTTPS para verificar. Se houver suporte para HTTP/2, ele será indicado pela extensão no formato de um símbolo de Flash azul, e um cabeçalho &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
