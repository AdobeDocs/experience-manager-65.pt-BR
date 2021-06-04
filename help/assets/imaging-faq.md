---
title: Imagem inteligente
description: A geração de imagens inteligentes aplica as características de exibição exclusivas de cada usuário para veicular automaticamente as imagens certas, otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Gerenciamento de ativos,Representações
role: Business Practitioner, Administrator
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: 99230f2b9ce8179de4034d8bd739a5535b2cc0da
workflow-type: tm+mt
source-wordcount: '1917'
ht-degree: 1%

---


# Imagem inteligente {#smart-imaging}

## O que é &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

A tecnologia Smart Imaging aplica os recursos do Adobe Sensei AI e funciona com &quot;predefinições de imagens&quot; existentes para aprimorar o desempenho do delivery de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem, com base nos recursos do navegador do cliente.

>[!NOTE]
>
>Esse recurso exige o uso da CDN (Content Delivery Network) pronta para uso que é fornecida com o Adobe Experience Manager Dynamic Media. Nenhum outro CDN personalizado é compatível com esse recurso.

O Smart Imaging também se beneficia do aumento de desempenho de ser totalmente integrado ao melhor serviço de CDN premium do Adobe. Esse serviço encontra a rota ideal da Internet entre servidores, redes e pontos de peering. Ele encontra uma rota que tem a latência mais baixa e a menor taxa de perda de pacotes em vez de usar a rota padrão na Internet.

Os seguintes exemplos de ativos de imagem representam a otimização adicionada da imagem inteligente:

| Imagem<br>(URL) | Miniatura  | Size<br> (JPEG) | Tamanho (WebP)<br> (com Smart Imaging) | % redução |
|---|---|---|---|---|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 73.75 KB | 45.92 KB | 38% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 191 KB | 70.66 KB | 63% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 96.64 KB | 39.44 KB | 59% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 315.80 KB | 178.19 KB | 44% |
|  |  |  |  | Média = 51% |

Semelhante ao acima, o Adobe também executou um teste com URLs 7009 de sites de clientes ativos. Eles conseguiram atingir uma média de 38% mais de otimização do tamanho do arquivo para JPEG. Para PNG com formato WebP, eles conseguiram atingir uma média de 31% a mais de otimização no tamanho do arquivo. Esse tipo de otimização é possível por causa da capacidade de Smart Imaging.

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible.

### About device pixel ratio optimization {#dpr}

Device pixel ratio (DPR) &ndash; also known as CSS pixel ratio &ndash; is the relation between a device’s physical pixels and logical pixels. Especially with the advent of retina screens, the pixel resolution of modern mobile devices is growing at a fast rate.

Enabling Device Pixel Ratio optimization renders the image at the native resolution of the screen which makes it look crisp.

Turning on Smart Imaging DPR configuration automatically adjusts the requested image based on pixel density of the display the request is being served from. Currently, the pixel density of the display comes from Akamai CDN header values.

| Permitted values in the URL of an image | Description |
|---|---|
| `dpr=off` | Turn off DPR optimization at an individual image URL level.| 
| `dpr=on,dprValue` | Override the DPR value detected by Smart Imaging, with a custom value (as detected by any client-side logic or other means). Permitted value for `dprValue` is any number greater than 0. Specified values of 1.5, 2, or 3 are typical. |

>[!NOTE]
>
>* You can use `dpr=on,dprValue` even if the company level DPR setting as off.
>* Owing to DPR optimization, when the resultant image is greater than the MaxPix Dynamic Media setting, MaxPix width is always recognized by maintaining the image's aspect ratio.

| Requested Image size | DPR value | Delivered image size |
|---|---|---|
| 816x500 | 1 | 816x500 |
| 816x500 | 2 | 1632x1000 |

See also [When working with images](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### About network bandwidth optimization {#network-bandwidth-optimization}

Turning on Network Bandwidth automatically adjusts the image quality that is served based on actual network bandwidth. For poor network bandwidth, DPR optimization is automatically turned off, even if it is already on.

If desired, your company can opt out of network bandwidth optimization at the individual image level by appending `network=off` to the URL of the image.

| Permitted value in the URL of an image | Description |
|---|---|
| `network=off` | Turns off network optimization at an individual image URL level. |

>[!NOTE]
>
>DPR and network bandwidth values are based on the detected client-side values of the bundled CDN. These values are sometimes inaccurate. For example, iPhone5 with DPR=2 and iPhone12 with DPR=3, both show DPR=2. Still, for high-resolution devices, sending DPR=2 is better than sending DPR=1. Coming soon: Adobe is working on client-side code to accurately determine an end user's DPR. -->

## Quais são os principais benefícios do último Smart Imaging? {#what-are-the-key-benefits-of-smart-imaging}

Como as imagens constituem a maior parte do tempo de carregamento de uma página, a melhoria de desempenho pode ter um impacto profundo em um negócio, como conversão mais alta, tempo gasto no site e taxa de rejeição mais baixa do site.

Aprimoramentos na versão mais recente do Smart Imaging:

* Melhoria na classificação de SEO do Google para páginas da Web que utilizam a Imagem inteligente mais recente.
* Atua conteúdo otimizado imediatamente (no tempo de execução).
* Usa a tecnologia Adobe Sensei para converter de acordo com a qualidade (qlt) especificada na solicitação de imagem.
* A Imagem inteligente pode ser desativada usando o parâmetro de URL &quot;bfc&quot;.
* TTL (Tempo de vida útil) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que a Smart Imaging funcionasse.
* Anteriormente, as imagens original e derivada eram armazenadas em cache e era um processo de duas etapas para invalidar o cache. No último Smart Imaging, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de uma única etapa.
* Os clientes que usam cabeçalhos personalizados em seus conjuntos de regras se beneficiam do Smart Imaging mais recente, pois esses cabeçalhos não estão bloqueados, ao contrário da versão anterior do Smart Imaging. Por exemplo, &quot;Timing Allow Origin&quot;, &quot;X-Robot&quot;, conforme sugerido em [Adicionar um valor de cabeçalho personalizado às respostas da imagem|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Há algum custo de licenciamento associado à geração inteligente de imagens? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. O Smart Imaging está incluído em sua licença existente do Dynamic Media Classic ou do Adobe Experience Manager - Dynamic Media (no local, AMS e Adobe Experience Manager as a Cloud Service).

>[!NOTE]
>
>O Smart Imaging não está disponível para Dynamic Media - Clientes híbridos.

## Como funciona a geração inteligente de imagens? {#how-does-smart-imaging-work}

Quando uma imagem é solicitada por um consumidor, o Smart Imaging verifica as características do usuário e converte para o formato de imagem apropriado com base no navegador em uso. Essas conversões de formato são feitas de maneira que não degrade a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos com base na capacidade do navegador da seguinte maneira.

<!--   * Safari 14.0 +
    * Safari 14 only with iOS 14.0 and above and macOS BigSur and above -->

* Converta automaticamente em WebP para os seguintes navegadores:
   * Cromo
   * Firefox
   * Microsoft® Edge
   * O Safari (em iOS, macOS, iPadOS), forneceu suporte à versão de navegador e SO da WebP
   * Android™
   * Opera
* Suporte a navegador herdado para o seguinte:

   | Navegador | Versão do navegador/SO | Formato |
   | --- | --- | --- |
   | Safari | Anterior ao iOS/iPad 14.0 ou macOS BigSur | JPEG2000 |
   | Edge | Anterior a 18 | JPEGXR |
   | Internet Explorer | 9+ | JPEGXR |
* Para navegadores que não aceitam esses formatos, o formato de imagem solicitado originalmente é exibido.

Se o tamanho da imagem original for menor do que o produzido pela Imagem inteligente, a imagem original será veiculada.

## Quais formatos de imagem são compatíveis? {#what-image-formats-are-supported}

Os formatos de imagem a seguir são compatíveis com a Smart Imaging:

* JPEG
* PNG

<!-- CQDOC-15846 For any other format mentioned in a URL, you should explicity turn off Smart Imaging.  Append modifier `bfc=off` to the URL for file formats other than JPEG and PNG. You can accomplish this by using either one of the following methods:

* Use a ruleset if the `fmt` modifier is mentioned in the URL. 
* Append in URL modifiers field of the presets concerned.

Adobe is working on a permanent fix that does not require you to append `bfc=off` for `fmt !=JPEG` or `fmt !=PNG`. This topic will be updated after the fix is delivered. -->

## Como o Smart Imaging funciona com minhas predefinições de imagem existentes que já estão em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

O Smart Imaging funciona com suas &quot;predefinições de imagem&quot; existentes e observa todas as suas configurações de imagem, exceto qualidade (`qlt`) e formato (`fmt`), se o formato de arquivo solicitado for JPEG ou PNG. Para conversão de formato, o Smart Imaging mantém a fidelidade visual completa conforme definido pelas configurações predefinidas da imagem, mas em um tamanho de arquivo menor. Se o tamanho da imagem original for menor do que o produzido pela Imagem inteligente, a imagem original será veiculada.

<!-- CQDOC-15846 In addition, if your image presets are used to return `fmt !=JPEG` or `fmt !=PNG`, be sure append `bfc=off` in the preset modifier field to return the requested file format. -->

## Preciso alterar quaisquer URLs, predefinições de imagens ou implantar qualquer novo código no meu site para Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

O Smart Imaging funciona perfeitamente com seus URLs de imagem existentes e predefinições de imagem se você configurar o Smart Imaging em seu domínio personalizado existente. Além disso, o Smart Imaging não requer que você adicione qualquer código ao seu site para detectar o navegador de um usuário. Tudo é manipulado automaticamente.

Caso você precise configurar um novo domínio personalizado para usar a Smart Imaging, os URLs devem ser atualizados para refletir esse domínio personalizado.

Para entender os pré-requisitos para Smart Imaging, consulte [Posso usar Smart Imaging?](#am-i-eligible-to-use-smart-imaging)

<!-- No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. All of this is handled automatically. -->

<!-- As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## O Smart Imaging funciona com HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

O Smart Imaging funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Posso usar a geração inteligente de imagens? {#am-i-eligible-to-use-smart-imaging}

Para usar a Smart Imaging, a conta do Dynamic Media Classic ou Dynamic Media no Experience Manager de sua empresa deve atender aos seguintes requisitos:

* Use a CDN (Content Delivery Network) fornecida pelo Adobe como parte de sua licença.
* Use um domínio dedicado (por exemplo, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (por exemplo, `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta ou contas da empresa.

Toque em **[!UICONTROL Configurar]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]** Procure o campo rotulado **[!UICONTROL Nome do Servidor Publicado]**. Se você estiver usando um domínio genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição ao enviar um tíquete de suporte técnico.

Seu primeiro domínio personalizado não tem custo adicional com uma licença do Dynamic Media.

## Qual é o processo para ativar a Smart Imaging na minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Você inicia a solicitação para usar a geração inteligente de imagens; ele não é ativado automaticamente.

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 By default, Smart Imaging DPR and network optimization is disabled (turned off) for a Dynamic Media company account. If you want to enable (turn on) one or both of these out-of-the-box enhancements, create a support case as described below.

The release schedule for Smart Imaging DPR and network optimization is as follows:

| Region | Target date |
|---|---|
| North America | 24 May 2021 | 
| Europe, Middle East, Africa | 25 Jun 2021 | 
| Asia-Pacific | 19 Jul 2021 | -->

1. [Use o Admin Console para criar um caso](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) de suporte.
1. Forneça as seguintes informações no caso de suporte:

   1. Nome do contato principal, email, telefone.
   1. Todos os domínios a serem ativados para geração inteligente de imagens (ou seja, `images.company.com` ou `mycompany.scene7.com`).

      Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta ou contas da empresa.

      Clique em **[!UICONTROL Configurar]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do Servidor Publicado]**.
   1. Verifique se você está usando a CDN por meio do Adobe e não é gerenciada com uma relação direta.
   1. Verifique se você está usando um domínio dedicado, como `images.company.com` ou `mycompany.scene7.com`, e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e faça logon em sua conta ou contas da empresa.

      Clique em **[!UICONTROL Configurar]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do Servidor Publicado]**. Se você estiver usando um domínio genérico do Dynamic Media Classic, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.
   1. Indique se você também precisa de Smart Imaging para funcionar via HTTP/2.

1. O Atendimento ao cliente do Adobe adiciona você à Lista de espera do cliente de Smart Imaging com base na ordem em que as solicitações foram enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o suporte entrará em contato para coordenar e definir uma data de destino.
1. **Opcional**: Como opção, você pode testar a geração inteligente de imagens no Estágio antes de o Adobe colocar o novo recurso em produção.
1. Você é notificado após a conclusão pelo Atendimento ao cliente.
1. Para maximizar os aprimoramentos de desempenho do Smart Imaging, o Adobe recomenda definir o Time To Live (TTL) para 24 horas ou mais. O TTL define quanto tempo os ativos são armazenados em cache pela CDN. Para alterar essa configuração:

   1. Se você usa o Dynamic Media Classic, clique em **[!UICONTROL Configuração > Configuração do aplicativo > Configuração de publicação > Servidor de imagem]**. Defina o valor **[!UICONTROL Default Client Cache Time To Live]** como 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](config-dynamic.md). Defina o valor **[!UICONTROL Expiration]** 24 horas ou mais.

## Quando posso esperar que minha conta seja ativada com a Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Atendimento ao cliente, de acordo com a Lista de espera.

>[!NOTE]
>
>Pode haver um longo lead time, pois a ativação da Imagem inteligente envolve a limpeza do cache pelo Adobe. Portanto, apenas algumas transições de clientes podem ser tratadas a qualquer momento.

## Quais são os riscos ao mudar para usar a Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Não há risco para uma página da Web do cliente. No entanto, a transição para a Smart Imaging limpa o cache na CDN, pois envolve mudar para uma nova configuração do Dynamic Media Classic ou Dynamic Media no Experience Manager.

Durante a transição inicial, as imagens não armazenadas em cache acessam diretamente os servidores de origem do Adobe até que o cache seja recriado. Como resultado, o Adobe planeja lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao puxar solicitações da origem. Para a maioria dos clientes, o cache é totalmente criado novamente na CDN dentro de 1 a 2 dias.

## Como posso verificar se a geração de imagens inteligentes está funcionando como esperado?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que sua conta for configurada com geração inteligente de imagens, carregue um URL de imagem do Dynamic Media Classic ou Adobe Experience Manager - Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome clicando em **[!UICONTROL Exibir]** > **[!UICONTROL Desenvolvedor]** > **[!UICONTROL Ferramentas do desenvolvedor]** no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows®, navegue até as configurações no painel de ferramentas do desenvolvedor e selecione a caixa de seleção **[!UICONTROL Desativar cache (enquanto as ferramentas do dispositivo estão abertas)]**.
   * No macOS, no painel do desenvolvedor, na guia **[!UICONTROL Rede]**, selecione **[!UICONTROL desativar cache]**.

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A captura de tela a seguir mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome.
1. Repita esse teste em navegadores e condições de usuário diferentes.

>[!NOTE]
>
>Nem todas as imagens são convertidas. O Smart Imaging decide se a conversão pode melhorar o desempenho. Às vezes, onde não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

## A Smart Imaging pode ser desativada para qualquer solicitação? {#turning-off-smart-imaging}

Sim. Você pode desativar a Imagem inteligente adicionando o modificador `bfc=off` ao URL.

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 ## Can I request DPR and network optimization to be turned off at the company level? {#dpr-companylevel-turnoff}

Yes. To disable DPR and network optimization at your company, create a support case as described earlier in this topic. -->

## Que &quot;ajuste&quot; está disponível? Existem configurações ou comportamentos que podem ser definidos? (#tuning-settings)

Atualmente, você pode ativar ou desativar o Smart Imaging. Nenhum outro ajuste está disponível.

## Se o Smart Imaging gerenciar as configurações de qualidade, há mínimos e máximos a serem definidos? Por exemplo, é possível definir &quot;no lower than 60&quot; e &quot;no greater than 80 quality&quot;? (#Minimum-maximum)

Não há essa capacidade de provisionamento no Smart Imaging atual.

## Às vezes, uma imagem JPEG é retornada ao Chrome em vez de uma imagem WebP. Por que essa mudança acontece? (#jpeg-webp)

O Smart Imaging determina se a conversão é benéfica ou não. Ele retorna a nova imagem somente se a conversão resultar em um tamanho de arquivo menor com qualidade comparável.

<!-- CQDOC-17915 HIDDEN FOR NOW AS OF MAY 28 2021 ## How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop). -->
