---
title: Entrega de conteúdo HTTP2
description: Saiba mais sobre como o HTTP/2 melhora a maneira como navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de poder de processamento necessária.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---

# Entrega de conteúdo HTTP/2 {#http-delivery-of-content}

A Adobe está animada em anunciar a disponibilidade da entrega de conteúdo HTTP/2 com o benefício geral de um melhor desempenho.

>[!NOTE]
>
>Esse recurso exige o uso da CDN pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

## O que é HTTP/2? {#what-is-http}

HTTP/2 melhora a maneira como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de poder de processamento necessária.

O site a seguir descreve o HTTP/2 e seus benefícios de maneira breve e simples:

[O que você deve saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quais são os principais benefícios da migração para HTTP/2 na entrega de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

A melhora do desempenho pode variar muito. Ela se baseia em muitos fatores, como o código do site, a forma como você usa o Dynamic Media, o dispositivo do consumidor, a tela e a localização.

Os próprios testes de Adobe produziram os seguintes resultados:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram em dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou em 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso mudar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use a CDN (content delivery network) agrupada em Adobe como parte de sua licença do Dynamic Media.
* Use um domínio dedicado (não company-h.assetsadobe#.com).

  Se você já tiver um domínio dedicado, poderá aceitar por meio do Suporte ao cliente do Adobe.

  Se você não tiver um domínio dedicado, o Adobe planeja agendar sua transição para HTTP/2 em 2018.

## Qual é o processo de habilitação do HTTP/2 para minha conta do Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Você inicia a solicitação para mudar para HTTP/2; isso não é feito automaticamente para você.

1. Para mudar para HTTP/2, inicie uma solicitação Adobe de Suporte ao cliente. Consulte [Abrir um tíquete de suporte](https://experienceleague.adobe.com/pt-br?support-solution=General&amp;lang=en&amp;support-tab=home#support).

   1. Forneça as seguintes informações em sua solicitação de suporte:

      1. Nome do contato principal, email, telefone.
      1. Todos os domínios que serão transferidos para HTTP/2.
      1. Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
      1. Verifique se você usa o CDN por meio do Adobe e se não é gerenciado com um relacionamento direto.
      1. Verifique se você usa um domínio dedicado. Se você usar o Dynamic Media, use um domínio dedicado.

   1. O Suporte ao cliente adiciona você à lista de espera do cliente HTTP/2 com base na ordem em que as solicitações foram enviadas.
   1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Suporte ao cliente entrará em contato com você para coordenar a transição e definir uma data limite.
   1. Você é notificado após a conclusão e pode verificar se a transição para HTTP2 foi bem-sucedida.

      Como o navegador não declara esse fato, é necessário baixar uma extensão.

      Para o Firefox e o Chrome, há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores só são compatíveis com http/2 de forma segura, portanto, é necessário chamar um URL com https para verificação. Se http/2 for suportado, ele será indicado pela extensão na forma de um símbolo de Flash azul, e um cabeçalho &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.

## Quando posso esperar a transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Suporte ao cliente.

>[!NOTE]
>
>Pode haver um lead time longo, pois a transição para HTTP/2 envolve a limpeza do cache. Portanto, somente algumas transições de clientes podem ser tratadas de cada vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa seu cache na CDN porque envolve a mudança para uma nova configuração de CDN.

O conteúdo não armazenado em cache atinge diretamente os servidores de origem do Adobe até que o cache seja recriado novamente. Dessa forma, o Adobe planeja lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao extrair solicitações da origem.

## Como você pode verificar se um URL ou site está ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Como o navegador não declara esse fato, é necessário baixar uma extensão.

Para o Firefox e o Chrome, há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores só são compatíveis com http/2 de forma segura, portanto, é necessário chamar um URL com https para verificação. Se houver suporte para http/2, ele será indicado pela extensão no formato de um símbolo de Flash azul e um cabeçalho `X-Firefox-Spdy` : `h2`.
