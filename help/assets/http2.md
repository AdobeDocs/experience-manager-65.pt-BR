---
title: Entrega de conteúdo HTTP2
description: HTTP/2 melhora a forma como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e reduzindo a quantidade de poder de processamento necessário.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publicação,Configuração
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 2%

---

# Entrega de conteúdo HTTP/2 {#http-delivery-of-content}

A Adobe está animada em anunciar a disponibilidade da entrega de conteúdo HTTP/2 com o benefício geral de um melhor desempenho.

>[!NOTE]
>
>Esse recurso exige que você use a CDN predefinida fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.

## O que é HTTP/2? {#what-is-http}

O HTTP/2 melhora a forma como os navegadores e servidores se comunicam, permitindo uma transferência mais rápida de informações e ao mesmo tempo reduzindo a quantidade de poder de processamento necessário.

O site a seguir descreve o HTTP/2 e seus benefícios de uma maneira breve e simples:

[O que você deve saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quais são os principais benefícios da migração para HTTP/2 para a entrega de conteúdo? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

A melhoria do desempenho pode variar bastante. É baseado em vários fatores, como o código do seu site, como você usa o Dynamic Media, o dispositivo do consumidor, a tela e a localização.

Resultados dos testes próprios:

* Para imagens, o tempo de resposta melhorou de 7% a 28%, dependendo do dispositivo e do navegador. Os ganhos de desempenho mais notáveis foram em dispositivos iOS.
* Para visualizadores, o desempenho do tempo de carregamento melhorou em 15%.

A demonstração a seguir ilustra a diferença entre o carregamento HTTP/1 e HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Posso mudar para HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para usar HTTP/2, você deve atender aos seguintes requisitos:

* Use HTTPS seguro para suas solicitações de mídia avançada.
* Use a CDN (rede de entrega de conteúdo) fornecida pelo Adobe como parte de sua licença da Dynamic Media.
* Use um domínio dedicado (não-company-h.assetsadobe#.com).

   Se você já tiver um domínio dedicado, poderá optar por participar por meio do Suporte técnico.

   Se você não tiver um domínio dedicado, o Adobe planeja agendar sua transição para HTTP/2 em 2018.

## Qual é o processo para habilitar HTTP/2 para minha conta Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Você inicia a solicitação para alternar para HTTP/2; isso não é feito automaticamente para você.

1. Para mudar para HTTP/2, inicie uma solicitação de Atendimento ao cliente do Adobe. Consulte [Acessar o portal de suporte do Adobe Experience Manager](https://helpx.adobe.com/experience-manager/kb/accessing-aem-support-portal.html).

   1. Forneça as seguintes informações em sua solicitação de suporte:

      1. Nome do contato principal, email, telefone.
      1. Todos os domínios a serem transferidos para HTTP/2.
      1. Verifique se você usa HTTPS seguro para solicitações de mídia avançada.
      1. Verifique se você usa a CDN por meio do Adobe e não é gerenciada com um relacionamento direto.
      1. Verifique se você usa um domínio dedicado. Se usar o Dynamic Media, você usará um domínio dedicado.
   1. O Atendimento ao cliente adiciona você à lista de espera do cliente HTTP/2, com base na ordem em que as solicitações foram enviadas.
   1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Atendimento ao cliente entrará em contato com você para coordenar a transição e definir uma data de destino.
   1. Você é notificado após a conclusão e pode verificar a transição bem-sucedida para HTTP2.

      Como o navegador não declara esse fato, é necessário baixar uma extensão.

      Para o Firefox e o Chrome, há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores só suportam http/2 com segurança, portanto, é necessário chamar um URL com https para verificar. Se http/2 for suportado, ele será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quando posso esperar uma transição para HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

As solicitações são processadas na ordem em que são recebidas pelo Atendimento ao cliente.

>[!NOTE]
>
>Pode haver um lead time longo, pois a transição para HTTP/2 envolve a limpeza do cache. Portanto, apenas algumas transições de clientes podem ser tratadas por vez.

## Quais são os riscos com a mudança para HTTP/2? {#what-are-the-risks-with-moving-to-http}

A transição para HTTP/2 limpa seu cache no CDN porque envolve mudar para uma nova configuração de CDN.

O conteúdo armazenado em cache atinge diretamente os servidores de origem não-Adobe até que o cache seja recriado novamente. Dessa forma, o Adobe pretende lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao puxar solicitações da origem.

## Como é possível verificar se um URL ou site está ativado com HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Como o navegador não declara esse fato, é necessário baixar uma extensão.

Para o Firefox e o Chrome, há uma extensão chamada &quot;Indicador HTTP/2 e SPDY&quot;. Os navegadores só suportam http/2 com segurança, portanto, é necessário chamar um URL com https para verificar. Se http/2 for suportado, ele será indicado pela extensão na forma de um símbolo de Flash azul e um cabeçalho `X-Firefox-Spdy` : `h2`.
