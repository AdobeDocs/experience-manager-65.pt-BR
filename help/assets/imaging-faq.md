---
title: Imagens inteligentes
description: A geração de imagens inteligentes aproveita as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
uuid: c11e52ba-8d64-4dc5-b30a-fc10c2b704e5
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Imagem inteligente {#smart-imaging}

## O que é a geração inteligente de imagens? {#what-is-smart-imaging}

A geração de imagens inteligentes aproveita as características de exibição exclusivas de cada usuário para fornecer automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento. A geração de imagens inteligentes funciona com as predefinições de imagens existentes e usa inteligência no último milissegundo de entrega para reduzir ainda mais o tamanho do arquivo de imagem com base na velocidade do navegador ou da conexão de rede.

A geração de imagens inteligentes se beneficia do aumento de desempenho da integração total com o melhor serviço premium CDN da classe. Este serviço encontra a melhor rota da Internet entre servidores, redes e pontos de peering que tem a menor latência e/ou a menor taxa de perda de pacotes do que a rota padrão da Internet.

## Quais são os principais benefícios da criação de imagens inteligentes? {#what-are-the-key-benefits-of-smart-imaging}

A geração de imagens inteligentes proporciona um melhor desempenho de entrega de imagens, otimizando automaticamente o tamanho do arquivo de imagem com base nas características do usuário. Como as imagens constituem a maioria do tempo de carregamento de uma página, o aprimoramento do desempenho pode ter um impacto profundo nos KPIs comerciais, como conversão mais alta, tempo gasto no site, taxa de rejeição do site mais baixa e assim por diante. A Adobe comparou o desempenho da entrega de imagem padrão com a geração de imagens inteligentes em diferentes formatos de arquivo, navegadores e configurações de qualidade (QLT). Em geral, você pode esperar uma melhora de 22 a 47% no desempenho, dependendo das configurações predefinidas da imagem e das características específicas do usuário final.

![image2017-11-14_133226](assets/image2017-11-14_133226.png)

## Há algum custo de licenciamento associado à geração de imagens inteligentes? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. A geração de imagens inteligentes está incluída na licença existente do Dynamic Media Classic (Scene7) ou do Dynamic Media. Não há custos adicionais para aproveitar esse novo recurso.

## Como funciona a geração de imagens inteligentes? {#how-does-smart-imaging-work}

Quando uma imagem é solicitada pela primeira vez por um consumidor, verificamos as características do usuário e convertemos para o formato de imagem apropriado com base no navegador. Além disso, criamos simultaneamente todas as conversões de formato que são armazenadas em cache no CDN. Quando os clientes em navegadores diferentes solicitarem essa imagem posteriormente, o formato de imagem apropriado será automaticamente entregue diretamente do cache CDN. Essas conversões de formato são feitas sem perdas, o que não diminui a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos, com base na capacidade do navegador, da seguinte forma:

* Converta automaticamente em WebP sem perdas para navegadores compatíveis com o formato WebP, como Chrome, Android e Opera.
* Converta automaticamente em JPEGXR sem perdas para navegadores compatíveis com o formato JPEGXR, como o Internet Explorer 9+.
* Converta automaticamente em JPEG2000 sem perdas para navegadores compatíveis com o formato JPEG2000, como o Safari.
* Para navegadores que não suportam esses formatos, o formato de imagem solicitado originalmente é atendido.

## Quais formatos de imagem são suportados? {#what-image-formats-are-supported}

Os seguintes formatos de imagem são suportados para geração de imagens inteligente:

* JPEG RGB
* PNG RGB
* TIFF RGB
* JPEG CMYK
* TIFF CMYK

## Como a geração de imagens inteligentes funciona com nossas predefinições de imagens já em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

A geração de imagens inteligentes funciona com as predefinições de imagens existentes e observa praticamente todas as configurações de imagem, como tamanho, qualidade, nitidez e assim por diante. O que mudará é o formato de imagem ou, nos casos de velocidade lenta da conexão com a rede, a configuração de qualidade. Para conversão de formato, mantemos a fidelidade visual completa, conforme definido pelas configurações predefinidas da imagem, mas em um tamanho de arquivo menor.

Por exemplo, suponha que uma predefinição de imagem esteja definida com o formato JPEG, tamanho 500x500, qualidade=85 e máscara de nitidez=0,1,1,5. Quando detectamos que um usuário está no navegador Chrome, a imagem é convertida em formato WebP sem perdas, com tamanho 500x500, qualidade=85 e máscara sem nitidez=0,1,1,5.

## Será necessário alterar quaisquer URLs, predefinições de imagens ou implantar qualquer novo código no meu site para geração de imagens inteligente? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Não. A geração de imagens inteligentes funciona perfeitamente com os URLs de imagem e as predefinições de imagens existentes. Além disso, a geração de imagens inteligentes não exige a adição de nenhum código em seu site para detectar diferentes características do usuário (navegador, largura de banda, dispositivo etc.). Tudo isso é feito automaticamente pela Adobe.

A única alteração que pode ser necessária é atualizar a configuração **[!UICONTROL Tempo de vida]** (TTL). Esta configuração define quanto tempo os ativos são armazenados em cache pelo CDN. Para maximizar as melhorias de desempenho da geração inteligente de imagens, a Adobe recomenda configurar o TTL para 24 horas ou mais. Para alterar essa configuração:

* Se você estiver usando o Dynamic Media Classic, toque em **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor]** de imagem. Defina o valor Tempo de vida **** padrão do Cache do cliente como 24 ou mais.

* Se você estiver usando o Dynamic Media, siga as instruções para [Configurar as configurações](config-dynamic.md) de imagem do Dynamic Media. Defina o valor de **[!UICONTROL Expiração]** para 24 horas ou mais.

>[!NOTE]
>
>Se definir TTL &lt;= 1 hora, a geração de imagens inteligentes não funcionará.

## A geração de imagens inteligentes funciona com HTTPS? Que tal HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

A geração de imagens inteligentes funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Estou qualificado para usar imagens inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para usar imagens inteligentes, o Dynamic Media Classic ou o Dynamic Media da sua empresa na conta do AEM deve atender aos seguintes requisitos:

* Use o CDN (Content Delivery Network) fornecido pela Adobe como parte da sua licença.
* Use um domínio dedicado (isto é, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (isto é, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

   Para localizar seus domínios, faça logon em sua conta ou contas da empresa.

   Toque em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações]** gerais. Procure o campo Nome **[!UICONTROL do servidor]** publicado. Se você estiver usando um domínio genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

* Não solicite imagens JPEG CMYK. Como parte de seu processamento, a geração de imagens inteligentes converte imagens JPEG CMYK em RGB. Se precisar obter imagens JPEG CMYK, não será possível usar a geração de imagens inteligentes.

## Qual é o processo para ativar a geração inteligente de imagens para minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Você deve iniciar a solicitação para usar a geração inteligente de imagens; ela não é ativada automaticamente.

1. Iniciar uma solicitação de suporte técnico (email: s7support@adobe.com).
1. Forneça as seguintes informações em sua solicitação de suporte:

   1. Nome do contato principal, email, telefone.
   1. Todos os domínios a serem ativados para geração de imagens inteligente (ou seja, images.company.com ou mycompany.sceno7.com).

      Para localizar seus domínios, faça logon em sua conta ou contas da empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações]** gerais.

      Procure o campo Nome **[!UICONTROL do servidor]** publicado.
   1. Verifique se você está usando o CDN pela Adobe e não é gerenciado com um relacionamento direto.
   1. Verifique se você está usando um domínio dedicado, como `images.company.com` ou `mycompany.scene7.com`, e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para localizar seus domínios, faça logon em sua conta ou contas da empresa.

      Clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configurações]** gerais.

      Procure o campo Nome **[!UICONTROL do servidor]** publicado. Se você estiver usando um domínio genérico do Dynamic Media Classic, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.
   1. Indique se você também precisa que isso funcione em HTTP/2

1. O suporte técnico adicionará você à Lista de espera do cliente de criação de imagens inteligente com base na ordem em que as solicitações foram enviadas.
1. Quando a Adobe estiver pronta para lidar com sua solicitação, o suporte entrará em contato com você para coordenar e definir uma data de destino.
1. Opcional: Você tem a opção de testar a geração inteligente de imagens no armazenamento temporário antes de a Adobe colocar o novo recurso em produção.
1. Você é notificado após a conclusão pelo suporte.
1. Para maximizar as melhorias de desempenho da geração inteligente de imagens, a Adobe recomenda configurar o Tempo de vida (TTL) para 24 horas ou mais. O TTL define quanto tempo os ativos são armazenados em cache pelo CDN. Para alterar essa configuração:

   1. Se você usar o Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração de aplicativo > Configuração de publicação > Servidor]** de imagem. Defina o valor Tempo de vida **** padrão do Cache do cliente como 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](config-dynamic.md). Defina o valor de **[!UICONTROL Expiração]** 24 horas ou mais.

## Quando posso esperar que minha conta seja habilitada com imagens inteligentes? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Suporte Técnico, de acordo com a Lista de Espera.

>[!NOTE]
Pode haver um longo lead time porque a habilitação de imagens inteligentes envolve a limpeza do cache. Portanto, apenas algumas transições de clientes podem ser tratadas a qualquer momento.

## Quais são os riscos da mudança para usar imagens inteligentes? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

A transição para a geração de imagens inteligentes limpa seu cache no CDN, pois envolve mudar para uma nova configuração do Dynamic Media Classic ou Dynamic Media no AEM.

Durante a transição inicial, as imagens não armazenadas em cache atingem diretamente os servidores de origem da Adobe até que o cache seja reconstruído novamente. Por esse motivo, a Adobe planeja lidar com algumas transições de clientes de cada vez para que o desempenho aceitável seja mantido ao retirar solicitações de nossa origem. Para a maioria dos clientes, o cache é totalmente construído novamente no CDN dentro de aproximadamente 1 a 2 dias.

## Como posso verificar se a geração de imagens inteligentes está funcionando como esperado?  {#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que sua conta for configurada com imagens inteligentes, carregue um URL de imagem do Dynamic Media Classic(S7)/Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome clicando em **[!UICONTROL Exibir > Desenvolvedor > Ferramentas]** do desenvolvedor no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Verifique se o cache está desativado quando as ferramentas do desenvolvedor estiverem abertas.

   1. No Windows, navegue até as configurações no painel de ferramentas do desenvolvedor e marque a caixa de seleção **[!UICONTROL Desativar cache (enquanto as ferramentas do desenvolvedor estiverem abertas)]** .
   1. No Mac, no painel do desenvolvedor, na guia **[!UICONTROL Rede]** , selecione **[!UICONTROL desativar cache]** .

1. Na solicitação inicial, a imagem não será otimizada. Normalmente, leva cerca de 15 minutos para retornar a imagem otimizada se ela não estiver no cache CDN.
1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A seguinte captura de tela mostra a imagem PNG sendo convertida dinamicamente em WebP no Chrome.
1. Repita esse teste em navegadores e condições de usuário diferentes.

>[!NOTE]
Nem todas as imagens são convertidas. A geração de imagens inteligentes decide se a conversão é necessária para melhorar o desempenho. Em alguns casos, quando não há ganho de desempenho esperado, a imagem não é convertida.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

