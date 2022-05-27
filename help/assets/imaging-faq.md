---
title: Imagem inteligente
description: O Smart Imaging aplica as características de exibição exclusivas de cada usuário para veicular automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: bb42b5990993b0f8cea95cf1f6c033aed2713c1c
workflow-type: tm+mt
source-wordcount: '3519'
ht-degree: 1%

---

# Imagem inteligente {#smart-imaging}

## O que é &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

A tecnologia Smart Imaging aplica os recursos do Adobe Sensei AI e funciona com &quot;predefinições de imagens&quot; existentes. Funciona para aprimorar o desempenho da entrega de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem com base nos recursos do navegador do cliente.

E agora, obtenha uma melhor pontuação Google Core Web Vital para LCP (Grande Pintor Contentível) com Smart Imaging aprimorado que agora vem com suporte para AVIF e WebP.

>[!IMPORTANT]
>
>A Smart Imaging requer o uso da CDN (Content Delivery Network) pronta para uso que é fornecida com o Adobe Experience Manager - Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.

O Smart Imaging se beneficia do aumento de desempenho adicional de ser totalmente integrado ao melhor serviço premium CDN (Content Delivery Network) do Adobe. Esse serviço encontra a rota ideal da Internet entre servidores, redes e pontos de peering. Ele encontra uma rota que tem a latência mais baixa e a menor taxa de perda de pacotes em vez de usar a rota padrão na Internet.

Os seguintes exemplos de ativos de imagem representam a otimização adicionada da imagem inteligente:

| Imagem (URL) | Miniatura  | Tamanho (JPEG) | Tamanho (WebP) com Smart Imaging | Tamanho (AVIF) com Smart Imaging | % de redução com WebP | % de redução com AVIF |
|---|---|---|---|---|---|---|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26,89% | 37,79% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01% | 72,57% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14,47% | 60,58% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25% | 51,85% |

Semelhante ao acima, o Adobe também executou um teste com um conjunto de amostras maior. O formato AVIF proporcionou uma redução extra de tamanho de 20% em relação ao WebP, o que proporcionou uma redução de 27% em relação ao JPEG. Tudo com a mesma qualidade visual. No total, a AVIF fornece até 41% de redução média do tamanho em relação ao JPEG.

Compare WebP e AVIF com PNG, você pode observar uma redução de 84% no tamanho com WebP e 87% com AVIF. E, como os formatos WebP e AVIF são compatíveis com transparência e várias animações de imagem, é uma boa substituição para arquivos PNG e GIF transparentes.

Consulte também [Otimização de imagem com formatos de imagem de próxima geração (WebP e AVIF)](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Quais são os principais benefícios do último Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

O Smart Imaging fornece um desempenho de entrega de imagem melhor, otimizando automaticamente o tamanho do arquivo de imagem com base no navegador do cliente em uso, a exibição do dispositivo e as condições da rede. Como as imagens constituem a maior parte do tempo de carregamento de uma página, qualquer melhoria de desempenho pode ter um impacto profundo nos KPIs de negócios, como taxas de conversão mais altas, tempo gasto em um site e taxas de rejeição do site mais baixas.

Os principais benefícios mais recentes do Smart Imaging incluem:

* Agora oferece suporte ao formato AVIF da próxima geração.
* O PNG para WebP e AVIF agora oferecem suporte para conversão com perdas. Como o PNG é um formato sem perdas, a WebP e a AVIF anteriores eram entregues sem perdas.
* Conversão do formato do navegador (`bfc`)
* Proporção de pixels do dispositivo (`dpr`)
* Largura de banda de rede (`network`)

### Sobre a conversão de formato do navegador (bfc) {#bfc}

Ativar a conversão de formato do navegador ao anexar `bfc=on` para o URL da imagem, converte automaticamente o JPEG e o PNG em AVIF com perdas, WebP com perdas, JPEGXR com perdas, JPEG2000 com perdas para navegadores diferentes. Para navegadores que não aceitam esses formatos, a Imagem inteligente continua a servir o JPEG ou PNG. Junto com o formato , a qualidade do novo formato é recalculada pelo Smart Imaging.

A imagem inteligente também pode ser desativada ao anexar `bfc=off` ao URL da imagem.

Consulte também [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) na API de disponibilização e renderização de imagens do Dynamic Media.

### Sobre a otimização da taxa de pixels do dispositivo (dpr) {#dpr}

Proporção de pixels do dispositivo (DPR) - também conhecida como proporção de pixels CSS - é a relação entre os pixels físicos e os pixels lógicos de um dispositivo. Especialmente com o advento das telas de retina, a resolução de pixels dos dispositivos móveis modernos está crescendo a um ritmo rápido.

Ativar a otimização da taxa de pixels do dispositivo renderiza a imagem na resolução nativa da tela, o que a faz parecer nítida.

Atualmente, a densidade de pixels da exibição vem dos valores do cabeçalho Akamai CDN.

| Valores permitidos no URL de uma imagem | Descrição |
|---|---|
| `dpr=off` | Desative a otimização do DPR em um nível de URL de imagem individual. |
| `dpr=on,dprValue` | Substitua o valor do DPR detectado pelo Smart Imaging, com um valor personalizado (como detectado por qualquer lógica do lado do cliente ou outros meios). Valor permitido para `dprValue` é qualquer número maior que 0. |

>[!NOTE]
>
>* Você pode usar `dpr=on,dprValue` mesmo que a configuração do DPR no nível da empresa esteja desativada.
>* Devido à otimização do DPR, quando a imagem resultante é maior que a configuração MaxPix Dynamic Media , a largura MaxPix é sempre reconhecida pela manutenção da proporção da imagem.


| Tamanho da imagem solicitada | Valor da Proporção de pixels do dispositivo (dpr) | Tamanho da imagem entregue |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Consulte também [Ao trabalhar com imagens](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Ao trabalhar com o Recorte inteligente](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Sobre a otimização da largura de banda da rede {#network}

Ativar a Largura de Banda da Rede ajusta automaticamente a qualidade da imagem veiculada com base na largura de banda real da rede. Para uma largura de banda de rede ruim, a otimização do DPR (Device Pixel Ratio) é automaticamente desativada, mesmo que já esteja ativada.

Se desejar, sua empresa pode recusar a otimização da largura de banda da rede no nível de imagem individual ao anexar `network=off` ao URL da imagem.

| Valor permitido no URL de uma imagem | Descrição |
|---|---|
| `network=off` | Desativa a otimização de rede em um nível de URL de imagem individual. |

O DPR e os valores de largura de banda da rede são baseados nos valores detectados do lado do cliente do CDN empacotado. Esses valores às vezes são imprecisos. Por exemplo, iPhone5 com DPR=2 e iPhone12 com `dpr=3`, ambos exibem `dpr=2`. Ainda, para dispositivos de alta resolução, envio `dpr=2` é melhor do que enviar `dpr=1`. A melhor maneira de superar essa imprecisão, no entanto, é usar o DPR do lado do cliente para fornecer valores 100% precisos. E funciona para qualquer dispositivo, seja Apple ou qualquer outro dispositivo que foi iniciado. Consulte [Usar imagem inteligente com relação de pixels de dispositivo do lado do cliente](/help/assets/client-side-dpr.md).

### Principais benefícios do Smart Imaging

* Melhoria na classificação de SEO do Google para páginas da Web que usam o Smart Imaging mais recente.
* Atua conteúdo otimizado imediatamente (no tempo de execução).
* Usa a tecnologia Adobe Sensei para conversão de acordo com a qualidade (`qlt`) especificado na solicitação de imagem.
* TTL (Tempo de vida útil) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que a Smart Imaging funcionasse.
* Anteriormente, as imagens original e derivada eram armazenadas em cache e era um processo de duas etapas para invalidar o cache. No último Smart Imaging, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de uma única etapa.
* Os clientes que usam cabeçalhos personalizados em seus conjuntos de regras se beneficiam do Smart Imaging mais recente, pois esses cabeçalhos não estão bloqueados, ao contrário da versão anterior do Smart Imaging. Por exemplo, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot;, conforme sugerido em [Adicionar um valor de cabeçalho personalizado às respostas da imagem|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Há algum custo de licenciamento associado ao Smart Imaging? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. A Smart Imaging está incluída em sua licença existente. Essa regra é verdadeira para o Dynamic Media Classic ou o Experience Manager - Dynamic Media (No local, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>O Smart Imaging não está disponível para Dynamic Media - Clientes híbridos.

## Como funciona a Smart Imaging? {#how-does-smart-imaging-work}

Quando uma imagem é solicitada por um consumidor, o Smart Imaging verifica as características do usuário e a converte para o formato de imagem apropriado, com base no navegador em uso. Essas conversões de formato são feitas de maneira que não degrade a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos com base na capacidade do navegador da seguinte maneira.

* Converter automaticamente para AVIF se o navegador suportar o formato
* Converter automaticamente para WebP se a conversão de AVIF não tiver sido benéfica ou o navegador não oferecer suporte a AVIF
* Converter automaticamente para JPEG2000 se o Safari não suportar WebP
* Converta automaticamente em JPEGXR para IE 9+ ou se o Edge não for compatível com WebP\
   | Formato de imagem | Navegadores compatíveis | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* Para navegadores que não aceitam esses formatos, o formato de imagem solicitado originalmente é exibido.

Se o tamanho da imagem original for menor do que o produzido pela Imagem inteligente, a imagem original será veiculada.

## Quais formatos de imagem são compatíveis? {#what-image-formats-are-supported}

Os formatos de imagem a seguir são compatíveis com a Smart Imaging:

* JPEG
* PNG

Para o formato de arquivo de imagem JPEG, a qualidade do novo formato é recalculada pelo Smart Imaging.

Para formatos de arquivo de imagem que oferecem suporte à transparência como PNG, você pode configurar o Smart Imaging para fornecer AVIF e WebP com perdas. Para a conversão de formato com perdas, o Smart Imaging usa a qualidade mencionada no URL da imagem ou a qualidade configurada na conta da empresa do Dynamic Media.

## Como o Smart Imaging funciona com minhas predefinições de imagem existentes que já estão em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

O Smart Imaging funciona com suas predefinições de imagem existentes e observa todas as suas configurações de imagem. O que muda é o formato da imagem, ou a configuração de qualidade, ou ambos. Para conversão de formato, o Smart Imaging mantém a fidelidade visual completa conforme definido pelas configurações predefinidas da imagem, mas em um tamanho de arquivo menor.

Por exemplo, suponha que uma predefinição de imagem seja definida com formato JPEG, tamanho 500 x 500, qualidade=85 e máscara de nitidez=0,1,1,5. Quando a Smart Imaging detecta que um usuário está em um navegador Chrome, a imagem é convertida para o formato WebP, com tamanho 500 x 500, e a nitidez da máscara=0,1,1,5 em uma qualidade WebP que corresponde a uma qualidade de JPEG de 85 o mais próximo possível. O impacto dessa conversão da WebP é comparado ao JPEG, e o menor dos dois é retornado.

## Preciso alterar quaisquer URLs, predefinições de imagens ou implantar qualquer novo código no meu site para Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Não. O Smart Imaging funciona perfeitamente com seus URLs de imagem e predefinições de imagem existentes. Além disso, o Smart Imaging não requer que você adicione código ao seu site para detectar o navegador de um usuário. Toda essa funcionalidade é manipulada automaticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## O Smart Imaging funciona com HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

O Smart Imaging funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Posso usar a Smart Imaging? {#am-i-eligible-to-use-smart-imaging}

Para usar a Smart Imaging, a Dynamic Media Classic ou Dynamic Media na Experience Manager deve atender aos seguintes requisitos:

* Use a CDN (Content Delivery Network) fornecida pelo Adobe como parte de sua licença.
* Usar um domínio dedicado (por exemplo, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (por exemplo, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

Para localizar seus domínios, abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta ou contas da empresa.

Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**. Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**. Se você usa um domínio genérico no momento, é possível solicitar a transferência para seu próprio domínio personalizado. Faça essa solicitação de transição ao enviar um caso de suporte.

Seu primeiro domínio personalizado não tem custo adicional com uma licença do Dynamic Media.

## Qual é o processo para ativar a Smart Imaging na minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Você inicia uma solicitação para usar a Smart Imaging; ele não é ativado automaticamente.

Crie um caso de suporte conforme descrito abaixo. No seu caso de suporte, certifique-se de mencionar quais dos seguintes recursos de Smart Imaging (um ou mais) você deseja ativar em sua conta:

* WebP
* AVIF
* Otimização do DPR e da largura de banda da rede
* PNG para AVIF com perdas ou WebP com perdas

Se você já tiver o Smart Imaging ativado com o WebP, mas desejar outros novos recursos, conforme listado acima, é necessário criar um caso de suporte.

**Para criar um caso de suporte para ativar o Smart Imaging em sua conta:**

1. [Use o Admin Console para iniciar a criação de um novo caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Forneça as seguintes informações no caso de suporte:

   * Nome do contato principal, email, telefone.

   * Liste quais dos seguintes recursos de Smart Imaging (um ou mais) você deseja ativar em sua conta:
      * WebP
      * AVIF
      * Otimização do DPR e da largura de banda da rede
      * PNG para AVIF com perdas ou WebP com perdas
   * Todos os domínios a serem ativados para Smart Imaging (ou seja, `images.company.com` ou `mycompany.scene7.com`).

      Para localizar seus domínios, abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta ou contas da empresa.

      Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**.

   * Verifique se você está usando a CDN por meio do Adobe e não é gerenciada com uma relação direta.

   * Verifique se você está usando um domínio dedicado como `images.company.com` ou `mycompany.scene7.com`e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para localizar seus domínios, abra o [Aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon em sua conta ou contas da empresa.

      Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**. Se você estiver usando um domínio genérico do Dynamic Media Classic no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

   * Indique se deseja que funcione em HTTP/2.


1. O Suporte ao cliente do Adobe adiciona você à Lista de espera do cliente de Smart Imaging com base na ordem em que as solicitações são enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Suporte ao cliente entrará em contato com você para coordenar e definir uma data de destino.
1. **Opcional**: Como opção, você pode testar a Imagem inteligente na Preparação antes do Adobe colocar o novo recurso em produção.
1. Você será notificado após a conclusão pelo Suporte ao cliente.
1. Para maximizar os aprimoramentos de desempenho do Smart Imaging, o Adobe recomenda definir o Time To Live (TTL) para 24 horas ou mais. O TTL define quanto tempo os ativos são armazenados em cache pela CDN. Para alterar essa configuração:

   1. Se você usar o Dynamic Media Classic, acesse **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configuração de publicação]** > **[!UICONTROL Servidor de imagem]**. Defina as **[!UICONTROL Tempo de Vida do Cache do Cliente Padrão]** para 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). Defina as **[!UICONTROL Expiração]** 24 horas ou mais.

## Quando posso esperar que minha conta seja ativada com a Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Suporte ao cliente, de acordo com a Lista de espera.

>[!NOTE]
>
>Pode haver um longo lead time, pois a ativação da Imagem inteligente envolve a limpeza do cache pelo Adobe. Portanto, apenas algumas transições de clientes podem ser tratadas a qualquer momento.

## Quais são os riscos ao mudar para usar a Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Não há risco para uma página da Web do cliente. No entanto, a transição para o Smart Imaging limpa o cache CDN. Essa operação envolve mover para uma nova configuração do Dynamic Media Classic ou Dynamic Media no Experience Manager.

Durante a transição inicial, as imagens não armazenadas em cache acessam diretamente os servidores de origem do Adobe até que o cache seja recriado. Dessa forma, o Adobe pretende lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao puxar solicitações da origem. Para a maioria dos clientes, o cache é totalmente criado novamente na CDN dentro de 1 a 2 dias.

## Como posso verificar se a Smart Imaging está funcionando como esperado?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que sua conta for configurada com Smart Imaging, carregue um URL de imagem Dynamic Media Classic ou Adobe Experience Manager - Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome acessando **[!UICONTROL Exibir]** > **[!UICONTROL Desenvolvedor]** > **[!UICONTROL Ferramentas do desenvolvedor]** no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows®, navegue até as configurações no painel de ferramentas do desenvolvedor e selecione **[!UICONTROL Desabilitar cache (enquanto as ferramentas do dispositivo estão abertas)]** caixa de seleção.
   * No macOS, no painel do desenvolvedor, em **[!UICONTROL Rede]** guia , selecione **[!UICONTROL desativar cache]**.

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A captura de tela a seguir mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome. Se o seu domínio tiver o AVIF ativado, você também pode esperar ver o AVIF no Tipo de conteúdo.
1. Repita esse teste em navegadores e condições de usuário diferentes.

>[!NOTE]
>
>Nem todas as imagens são convertidas. O Smart Imaging decide se a conversão pode melhorar o desempenho. Às vezes, onde não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## Como saber o ganho em desempenho? Existe uma maneira de conhecer os benefícios do Smart Imaging? {#benefits}

O cabeçalho Smart Imaging determina os benefícios do Smart Imaging. Quando a Smart Imaging estiver ativada, depois de solicitar uma imagem, sob a **[!UICONTROL Cabeçalhos de resposta]** título, você pode ver `-X-Adobe-Smart-Imaging` como visto no exemplo destacado a seguir:

![Cabeçalho de imagem inteligente](/help/assets/assets-dm/smart-imaging-header2.png)

Esse cabeçalho informa o seguinte:

* O Smart Imaging está funcionando para a empresa.
* Um valor positivo significa que a conversão é bem-sucedida. Nesse caso, uma nova imagem da WebP é retornada.
* Um valor negativo significa que a conversão não foi bem-sucedida. Nesse caso, a imagem original solicitada é retornada (JPEG por padrão, se não especificada).
* Um valor positivo mostra a diferença em bytes entre a imagem solicitada e a nova imagem. No exemplo acima, os bytes salvos são `75048` ou aproximadamente 75 KB para uma imagem.
* Um valor negativo significa que a imagem solicitada é menor que a nova imagem. A diferença de tamanho negativo é mostrada, mas a imagem veiculada é somente a imagem solicitada original.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 com WebP sendo entregue**
>
>Se o valor de `X-Adobe-Smart-Imaging` for -1 e o WebP ainda estiver sendo entregue, significa que o Smart Imaging está funcionando, mas os benefícios de tamanho não foram calculados devido ao cache antigo. Você pode usar `cache=update` (somente uma vez) no URL da imagem para corrigir esse problema.
>Um exemplo de uso do modificador:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Para invalidar o cache inteiro, você deve criar um caso de suporte.

## Como posso desativar a otimização de AVIF no Smart Imaging?{#disable-avif}

Se quiser voltar a servir o WebP por padrão, crie um caso de suporte para o mesmo. Como de costume, você pode desativar o Smart Imaging adicionando o parâmetro `bfc=off` ao URL da imagem. No entanto, você não pode selecionar WebP ou AVIF no modificador de URL para Smart Imaging. Essa capacidade é mantida no nível da conta da sua empresa.

## A Smart Imaging pode ser desativada para qualquer solicitação?{#turning-off-smart-imaging}

Sim. Você pode desativar a Smart Imaging adicionando um dos seguintes modificadores:

* `bfc=off` para desativar a conversão de formato do navegador. Consulte também [Conversão de formato do navegador](#bfc).
* `dpr=off` para desativar a Proporção de pixels do dispositivo. Consulte também [Proporção de pixels do dispositivo](#dpr).
* `network=off` para desativar a largura de banda da rede. Consulte também [Largura de banda da rede](#network).

## Que &quot;ajuste&quot; está disponível? Existem configurações ou comportamentos que podem ser definidos? {#tuning-settings}

A Imagem inteligente tem três opções que você pode ativar ou desativar.

* [Conversão de formato do navegador](#bfc)
* [Proporção de pixels do dispositivo](#dpr)
* [Largura de banda da rede](#network)

## Tenho um URL com fmt=tif no navegador web Chrome. Mas minha solicitação falha com um erro do ImageServer. Por quê? {#fmt-tif}

Esse erro não ocorre se a Imagem inteligente não estiver ativada em sua conta. A Imagem inteligente funciona somente com formatos JPEG ou PNG.

Para evitar esse erro, é possível:

* Especifique JPEG ou PNG, ou
* Não use o `fmt` modificador, ou
* Use um formato preferencial do navegador definido pelo Smart Imaging. Por exemplo, você pode usar o WebP para navegador da Web Chrome.

## Quero baixar uma imagem TIFF do URL de uma imagem. Como faço isso? {#download-tif}

Adicionar `fmt=tif` e `bfc=off` para o caminho do URL da imagem.

## O Smart Imaging só gerencia o formato de imagem ou também gerencia as configurações de qualidade de imagem para obter melhores resultados?

O Smart Imaging usa formato e qualidade. O restante dos parâmetros permanecem os mesmos, se solicitado no URL da imagem.

## Se o Smart Imaging gerenciar as configurações de qualidade, há mínimos e máximos que eu posso definir? Ou seja, uma qualidade que não é inferior a 60 e não é superior a 80? {#quality-setting}

Atualmente, não há esse provisionamento.

## O Smart Imaging ajusta automaticamente a configuração de saída de porcentagem de qualidade ou é uma configuração que é ajustada manualmente e se aplica a todas as imagens? Dentro de que intervalo? {#percent-quality}

A Smart Imaging ajusta automaticamente a porcentagem de qualidade. Esse percentual de qualidade é determinado por meio de um algoritmo de aprendizado de máquina desenvolvido pelo Adobe. Essa porcentagem não é específica do intervalo.

## Com a Smart Imaging, quais comandos de veiculação de imagens são suportados ou ignorados? {#support-ignore}

Os únicos comandos que são ignorados são `fmt` e `qlt`. Todos os comandos restantes são suportados.

## As imagens de JPEG são substituídas apenas por Imagens inteligentes? E se eu solicitar um WebP, PNG ou algo mais? {#replace-request}

Essa funcionalidade funciona somente para JPEG e PNG.

## Por que uma imagem JPEG às vezes é retornada ao Chrome em vez de WebP? {#jpeg-returned}

O Smart Imaging determina se a conversão é benéfica ou não. Ele retorna a nova imagem somente da conversão que é benéfica.

## Por que a funcionalidade da Proporção de pixels do dispositivo (dpr) não funciona conforme o esperado com imagens compostas? {#composite-images}

Se uma imagem composta envolver muitas camadas, a funcionalidade do dpr pode ser afetada ao usar um modificador de posição. Esse problema é conhecido e será corrigido em versões futuras do Smart Imaging. Se outra funcionalidade de Smart Imaging não estiver funcionando como esperado, você pode criar um caso de suporte para relatar o problema.

## Por que o PNG do Smart Imaging ainda é convertido em WebP/AVIF sem perdas? {#convert-to-lossless}

Como o PNG é um formato sem perdas, o WebP e o AVIF anteriores eram entregues sem perdas, resultando em um tamanho maior do que o esperado. O Smart Imaging agora suporta conversão com perdas. Você pode usar o modificador `cache=update` (somente uma vez) em uma solicitação de imagem para corrigir esse problema. Um exemplo de uso deste modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar o cache inteiro, você deve criar um caso de suporte solicitando esse esforço.

## Como posso continuar usando o PNG para conversão sem perdas no Smart Imaging? {#continue-using}

O Smart Imaging agora oferece suporte à conversão com perdas com base no nível de qualidade. Para continuar usando a conversão sem perdas, você pode usar a qualidade 100 definida pela configuração da sua empresa ou pelo URL da imagem usando `qlt=100` no caminho.