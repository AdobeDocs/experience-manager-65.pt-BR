---
title: DELIVERY HTTP2 do conteúdo
description: O HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de energia de processamento necessária.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---


# DELIVERY HTTP2 do conteúdo {#http-delivery-of-content}

A Adobe está empolgada em anunciar a disponibilidade do delivery HTTP/2 de conteúdo com o benefício geral de um melhor desempenho.

## O que é HTTP/2? {#what-is-http}

O HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de energia de processamento necessária.

O site a seguir descreve o HTTP/2 e seus benefícios de uma forma breve e simples:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quais são os principais benefícios da mudança para HTTP/2 para o delivery de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

O aprimoramento do desempenho varia muito com base em fatores como o código do seu site, a forma como você está usando o Dynamic Media, o dispositivo do consumidor, a tela e o local, e assim por diante.

Os resultados obtidos foram os seguintes:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram nos dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 versus HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Estou qualificado para alternar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use o CDN (content delivery network) fornecido no Adobe como parte da sua licença do Dynamic Media.
* Use um domínio dedicado (não-empresa-h.assetsadobe#.com).

   Se você já tiver um domínio dedicado, poderá aceitar por meio do Suporte Técnico.

   Se você não tiver um domínio dedicado, o Adobe agendará sua transição para HTTP/2 em 2018.

## Qual é o processo para habilitar HTTP/2 para minha conta do Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

É necessário iniciar a solicitação para alternar para HTTP/2; isso não é feito automaticamente para você.

1. Inicie uma solicitação de suporte técnico para alternar para HTTP2. Consulte [Acessar o Portal de suporte AEM](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Forneça as seguintes informações em sua solicitação de suporte:

      1. Nome do contato principal, email, telefone.
      1. Todos os domínios a serem transferidos para HTTP2.
      1. Verifique se você está usando HTTPS seguro para solicitações de mídia avançada.
      1. Verifique se você está usando o CDN através do Adobe e se não é gerenciado com um relacionamento direto.
      1. Verifique se você está usando um domínio dedicado. Se você usar o Dynamic Media, você já estará usando um domínio dedicado.
   1. O Suporte Técnico adicionará você à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
   1. Quando o Adobe estiver pronto para lidar com sua solicitação, o suporte entrará em contato com você para coordenar a transição e definir uma data de público alvo.
   1. Você será notificado após a conclusão e poderá verificar a transição bem-sucedida em HTTP2.

      Como o navegador não declara esse fato, é necessário baixar uma extensão.

      Para o Firefox e o Chrome há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores suportam somente http/2 com segurança, portanto, é necessário chamar um URL com https para verificar. Se http/2 for suportado, isso será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.


## Quando posso esperar a transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações serão processadas na ordem em que forem recebidas pelo Suporte Técnico.

>[!NOTE]
>
>Pode haver um longo lead time porque a transição para HTTP/2 envolve a limpeza do cache. Portanto, somente algumas transições de clientes podem ser tratadas de cada vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa o cache no CDN porque envolve a mudança para uma nova configuração de CDN.

O conteúdo armazenado em cache atinge diretamente os servidores de Adobe não armazenados em cache até que o cache seja reconstruído novamente. Por esse motivo, a Adobe planeja lidar com algumas transições de clientes de cada vez para que o desempenho aceitável seja mantido ao retirar solicitações de nossa origem.

## Como verificar se um URL ou site é ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Como o navegador não declara esse fato, é necessário baixar uma extensão.

Para o Firefox e o Chrome há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores suportam somente http/2 com segurança, portanto, é necessário chamar um URL com https para verificar. Se http/2 for suportado, isso será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
