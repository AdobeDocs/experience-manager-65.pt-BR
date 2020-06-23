---
title: Perguntas frequentes sobre entrega de conteúdo HTTP2
seo-title: Perguntas frequentes sobre entrega de conteúdo HTTP2
description: Saiba mais sobre o delivery de conteúdo HTTP2.
seo-description: Saiba mais sobre o delivery de conteúdo HTTP2.
uuid: e837c3e0-6e48-46f1-b510-847c9976807a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: afbe9f80-c2a3-4a46-b9d6-4c9406667d7f
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 4%

---


# Perguntas frequentes sobre entrega de conteúdo HTTP2{#http-delivery-of-content-faq}

A Adobe está empolgada em anunciar a disponibilidade do delivery HTTP/2 de conteúdo. Ao usar HTTP/2, você observará um aumento geral no desempenho.

## O que é HTTP/2? {#what-is-http}

O HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de energia de processamento necessária.

O site a seguir descreve o HTTP/2 e seus benefícios de uma forma breve e simples:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quais são os principais benefícios da mudança para HTTP/2 para o delivery de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

O aprimoramento do desempenho varia muito com base em fatores como o código do seu site, como você está usando o Scene7, o dispositivo do consumidor, a tela e o local, e assim por diante.

Os próprios testes da Adobe resultaram nos seguintes resultados:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram nos dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 versus HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Estou qualificado para alternar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use o CDN (content delivery network) fornecido pela Adobe como parte da sua licença do Dynamic Media Classic.
* Use um domínio dedicado (isto é, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico do Dynamic Media Classic (isto é, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

   Para localizar seus domínios, [faça logon na sua instância do Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada conta de empresa.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]** Procure o campo Nome **do servidor** publicado. Se você estiver usando um domínio genérico do Scene7, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

## Qual é o processo para habilitar HTTP/2 para minha conta do Dynamic Media Classic? {#what-is-the-process-for-enabling-http-for-my-scene-account}

Você deve iniciar uma solicitação de suporte técnico da Adobe (`s7support@adobe.com`) para alternar para HTTP/2; isso não é feito automaticamente para você.

1. Forneça as seguintes informações em sua solicitação de suporte:

   * Nome do contato principal, email e número de telefone.
   * Todos os domínios a serem transferidos para HTTP2. Isso é, `images.company.com` ou `mycompany.scene7.com`.

   Para localizar seus domínios, [faça logon na sua instância do Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada conta de empresa.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]** Procure o campo Nome do servidor **[!UICONTROL publicado.]**

   * Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
   * Verifique se você está usando o CDN pela Adobe e não é gerenciado com um relacionamento direto.
   * Verifique se você está usando um domínio dedicado. Isso não é, `images.company.com` ou `mycompany.scene7.com`, um domínio genérico do Scene7 como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para localizar seus domínios, [faça logon na sua instância do Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) para cada conta de empresa.

   Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações gerais.]** Procure o campo Nome do servidor **[!UICONTROL publicado.]** Se você estiver usando um domínio genérico do Scene7, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

   1. O suporte técnico o adiciona à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
   1. Quando a Adobe estiver pronta para lidar com sua solicitação, o Suporte entrará em contato com você para coordenar a transição e definir uma data de público alvo.
   1. Você será notificado após a conclusão e poderá verificar uma transição bem-sucedida em HTTP2.



## Quando posso esperar a transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Suporte Técnico.

>[!NOTE]
>
>Pode haver um longo lead time porque a transição para HTTP/2 envolve a limpeza do cache. Portanto, somente algumas transições de clientes podem ser tratadas de cada vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa o cache no CDN porque envolve a mudança para uma nova configuração de CDN.

O conteúdo não armazenado em cache atinge diretamente os servidores de origem da Adobe até que o cache seja reconstruído novamente. Por esse motivo, a Adobe planeja lidar com algumas transições de clientes de cada vez para que o desempenho aceitável seja mantido ao retirar solicitações de nossa origem.

## Como verificar se um URL ou site é ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Você precisa baixar uma externidade para usar com seu navegador da Web. Para Firefox e Chrome há uma extensão chamada **[!UICONTROL HTTP/2 e Indicador SPDY.]** Os navegadores só suportam HTTP/2 com segurança, portanto, é necessário chamar um URL com HTTPS para verificar. Se o HTTP/2 for suportado, isso será indicado pela extensão na forma de um símbolo Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
