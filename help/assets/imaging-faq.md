---
title: Imagem inteligente
description: A Smart Imaging aplica as características de visualização exclusivas de cada usuário para fornecer automaticamente as imagens certas otimizadas para sua experiência, resultando em melhor desempenho e envolvimento.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: bf8c6bbd-847d-43d7-9ff4-7231bfd8d107
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
source-git-commit: ea983b24da66edd02f86614690f8bc5e1e2499d9
workflow-type: tm+mt
source-wordcount: '3624'
ht-degree: 1%

---

# Imagem inteligente {#smart-imaging}

## O que é &quot;Smart Imaging&quot;? {#what-is-smart-imaging}

A tecnologia Smart Imaging aplica os recursos de IA do Adobe Sensei e funciona com &quot;predefinições de imagem&quot; existentes. Ele funciona para aprimorar o desempenho do delivery de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem com base nos recursos do navegador do cliente.

E agora, obtenha uma melhor pontuação do Google Core Web Vital para LCP (Largest Contentful Paint) com imagens inteligentes aprimoradas que agora vêm com suporte para AVIF e WebP.

>[!IMPORTANT]
>
>A Criação de imagens inteligentes exige o uso do CDN (Content Delivery Network) pronto para uso que é fornecido com o Adobe Experience Manager - Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

>[!TIP]
>
>Experimente e descubra os benefícios dos modificadores de imagem do Dynamic Media e do Smart Imaging, usando o Dynamic Media [_Instantâneo_](https://snapshot.scene7.com/).
>
> O Instantâneo é uma ferramenta de demonstração visual criada para ilustrar o potencial do Dynamic Media para entrega de imagens otimizadas e dinâmicas. Experimente com imagens de teste ou URLs do Dynamic Media, para observar visualmente a saída de vários modificadores de imagem do Dynamic Media e otimizações de Imagem inteligente para o seguinte:
>* Tamanho do arquivo (com entrega WebP e AVIF)
>* Largura de banda de rede
>* DPR (Relação de pixels do dispositivo)
>
>Para saber como é fácil usar o Snapshot, reproduza o [Vídeo de treinamento de instantâneos](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) (3 minutos e 17 segundos).

A Smart Imaging se beneficia do aumento de desempenho de estar totalmente integrado ao melhor serviço premium de CDN (Content Delivery Network) do Adobe. Este serviço encontra a rota de Internet ideal entre servidores, redes e pontos de correspondência. Ele encontra uma rota que tem a menor latência e a menor taxa de perda de pacotes em vez de usar a rota padrão na Internet.

Os seguintes exemplos de ativos de imagem representam a otimização da Imagem inteligente adicionada:

| Imagem (URL) | Miniatura  | Tamanho (JPEG) | Tamanho (WebP) com imagem inteligente | Tamanho (AVIF) com Smart Imaging | % de redução com WebP | % de redução com AVIF |
|---|---|---|---|---|---|---|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90.2 KB | 26.89% | 37.79% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16.01% | 72.57% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87.1 KB | 14.47% | 60.58% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![picture4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8.25% | 51.85% |

Semelhante ao acima, o Adobe também executou um teste com um conjunto de amostras maior. O formato AVIF forneceu 20% de redução extra do tamanho em relação ao WebP, que forneceu 27% de redução em relação ao JPEG. Tudo com a mesma qualidade visual. No total, a AVIF fornece redução média de até 41% no tamanho do JPEG.

Compare WebP e AVIF com PNG, você pode observar uma redução de 84% no tamanho com WebP e 87% com AVIF. E, como os formatos WebP e AVIF são compatíveis com transparência e animações de várias imagens, é um bom substituto para arquivos PNG e GIF transparentes.

Consulte também [Otimização de imagem com formatos de imagem de última geração (WebP e AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Quais são os principais benefícios da geração de imagens inteligentes mais recente? {#what-are-the-key-benefits-of-smart-imaging}

A Imagem inteligente oferece melhor desempenho de entrega de imagens, otimizando automaticamente o tamanho do arquivo de imagem com base no navegador do cliente em uso, na exibição do dispositivo e nas condições da rede. Como as imagens constituem a maioria do tempo de carregamento de uma página, qualquer melhoria de desempenho pode ter um impacto profundo nos KPIs de negócios, como taxas de conversão mais altas, tempo gasto em um site e taxas de rejeição mais baixas.

Os principais benefícios mais recentes da Smart Imaging mais recente incluem:

* Agora é compatível com o formato AVIF da próxima geração.
* PNG para WebP e AVIF agora oferece suporte a conversões com perdas. Como o PNG é um formato sem perdas, o WebP e o AVIF anteriores eram sem perdas.
* Conversão de formato de navegador (`bfc`)
* Proporção de pixels do dispositivo (`dpr`)
* Largura de banda de rede (`network`)

### Sobre a Conversão de Formato de Navegador (bfc) {#bfc}

Ativando a Conversão de Formato de Navegador anexando `bfc=on` para o URL da imagem converte automaticamente o JPEG e PNG em AVIF com perdas, WebP com perdas, JPEGXR com perdas, JPEG2000 com perdas para navegadores diferentes. Para navegadores que não oferecem suporte a esses formatos, o Smart Imaging continua a servir o JPEG ou o PNG. Juntamente com o formato, a qualidade do novo formato é recalculada pelo Smart Imaging.

As imagens inteligentes também podem ser desativadas anexando `bfc=off` ao URL da imagem.

Consulte também [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) na API do Dynamic Media Image Serving and Rendering.

### Sobre a otimização da Relação de pixels do dispositivo (dpr) {#dpr}

Proporção de pixels do dispositivo (DPR) - também conhecida como Proporção de pixels CSS - é a relação entre os pixels físicos e os pixels lógicos de um dispositivo. Especialmente com o advento das telas retina, a resolução de pixels de dispositivos móveis modernos está crescendo a uma taxa rápida.

Ativar a otimização da Proporção de pixels do dispositivo renderiza a imagem na resolução nativa da tela, o que a torna nítida.

Atualmente, a densidade de pixels da exibição vem dos valores de cabeçalho da CDN Akamai.

| Valores permitidos no URL de uma imagem | Descrição |
|---|---|
| `dpr=off` | Desative a otimização de DPR em um nível de URL de imagem individual. |
| `dpr=on,dprValue` | Substitua o valor do DPR detectado pelo Smart Imaging, com um valor personalizado (conforme detectado por qualquer lógica do lado do cliente ou por outros meios). Valor permitido para `dprValue` é qualquer número maior que 0. |

>[!NOTE]
>
>* Você pode usar `dpr=on,dprValue` mesmo que a configuração da DPR no nível da empresa esteja desativada.
>* Devido à otimização da DPR, quando a imagem resultante é maior que a configuração MaxPix Dynamic Media, a largura MaxPix é sempre reconhecida ao manter a proporção da imagem.


| Tamanho da imagem solicitada | Valor da Proporção de pixels do dispositivo (dpr) | Tamanho da imagem entregue |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Consulte também [Ao trabalhar com imagens](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-images) e [Ao trabalhar com o Recorte inteligente](/help/assets/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Sobre a otimização da largura de banda da rede {#network}

Ativar a Largura de Banda da Rede ajusta automaticamente a qualidade da imagem fornecida com base na largura de banda real da rede. Para uma largura de banda de rede ruim, a otimização da DPR (Relação de pixels do dispositivo) é automaticamente desativada, mesmo que já esteja ativada.

Se desejar, sua empresa pode recusar a otimização da largura de banda da rede no nível da imagem individual anexando `network=off` ao URL da imagem.

| Valor permitido no URL de uma imagem | Descrição |
|---|---|
| `network=off` | Desativa a otimização de rede em um nível de URL de imagem individual. |

Os valores de DPR e largura de banda da rede são baseados nos valores detectados do lado do cliente do CDN empacotado. Esses valores às vezes são imprecisos. Por exemplo, iPhone5 com DPR=2 e iPhone12 com `dpr=3`, ambos mostram `dpr=2`. Ainda, para dispositivos de alta resolução, enviar `dpr=2` é melhor do que enviar `dpr=1`. No entanto, a melhor maneira de superar essa imprecisão é usar a DPR do lado do cliente para fornecer valores 100% precisos. E funciona para qualquer dispositivo, seja Apple ou qualquer outro dispositivo que tenha sido iniciado. Consulte [Usar Imagem inteligente com proporção de pixels do dispositivo no lado do cliente](/help/assets/client-side-dpr.md).

### Principais benefícios adicionais da geração de imagens inteligentes

* Classificação da SEO do Google aprimorada para páginas da Web que usam a Imagem inteligente mais recente.
* Fornece conteúdo otimizado imediatamente (no tempo de execução).
* Usa a tecnologia Adobe Sensei para converter de acordo com a qualidade (`qlt`) especificado na solicitação de imagem.
* TTL (Time To Live) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que o Smart Imaging funcionasse.
* Anteriormente, as imagens originais e derivadas eram armazenadas em cache e era um processo de duas etapas para invalidar o cache. Na Smart Imaging mais recente, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de etapa única.
* Os clientes que usam cabeçalhos personalizados em seu conjunto de regras se beneficiam da geração de Smart Imaging mais recente, pois esses cabeçalhos não são bloqueados, ao contrário da versão anterior do Smart Imaging. Por exemplo, &quot;Origem de permissão de tempo&quot;, &quot;X-Robot&quot; conforme sugerido em [Adicione um valor de cabeçalho personalizado às respostas da imagem|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Há algum custo de licenciamento associado ao Smart Imaging? {#are-there-any-licensing-costs-associated-with-smart-imaging}

Não. A imagem inteligente está incluída em sua licença atual do. Essa regra é verdadeira para Dynamic Media Classic ou Experience Manager - Dynamic Media (no local, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>A Criação de imagens inteligentes não está disponível para clientes Dynamic Media - Hybrid.

## Como funciona o Smart Imaging? {#how-does-smart-imaging-work}

Quando uma imagem é solicitada por um consumidor, o Smart Imaging verifica as características do usuário e as converte para o formato de imagem apropriado com base no navegador em uso. Essas conversões de formato são feitas de uma maneira que não prejudica a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos com base na capacidade do navegador da seguinte maneira.

* Converter automaticamente em AVIF se o navegador der suporte ao formato
* Converter automaticamente para WebP se a conversão AVIF não foi benéfica ou o navegador não é compatível com AVIF
* Converter automaticamente para JPEG2000 se o Safari não for compatível com WebP
* Converter automaticamente em JPEGXR para IE 9+ ou se o Edge não for compatível com WebP\
   | Formato da imagem | Navegadores compatíveis | |—|—| | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) | | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) | | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) | | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* Para navegadores que não aceitam esses formatos, o formato de imagem solicitado originalmente é fornecido.

Se o tamanho original da imagem for menor do que o produzido pela Smart Imaging, a imagem original será fornecida.

## Quais formatos de imagem são compatíveis? {#what-image-formats-are-supported}

Os formatos de imagem a seguir são compatíveis com o Smart Imaging:

* JPEG
* PNG

Para o formato de arquivo de imagem JPEG, a qualidade do novo formato é recalculada pelo Smart Imaging.

Para formatos de arquivo de imagem que oferecem suporte a transparência, como PNG, você pode configurar a Imagem inteligente para fornecer AVIF e WebP com perdas. Para a conversão de formato com perdas, o Smart Imaging usa a qualidade mencionada no URL da imagem ou a qualidade configurada na conta da empresa do Dynamic Media.

## Como o Smart Imaging funciona com minhas predefinições de imagem existentes que já estão em uso? {#how-does-smart-imaging-work-with-our-existing-image-presets-that-are-already-in-use}

A Imagem inteligente funciona com suas predefinições de imagens existentes e observa todas as suas configurações de imagem. O que muda é o formato da imagem, a configuração de qualidade ou ambos. Para a conversão de formatos, o Smart Imaging mantém a fidelidade visual total, conforme definido pelas suas configurações de predefinição de imagem, mas em um tamanho de arquivo menor.

Por exemplo, suponha que uma predefinição de imagem esteja definida com o formato JPEG, tamanho 500 x 500, qualidade=85 e máscara não nítida=0,1,1,5. Quando a Imagem inteligente detecta que um usuário está em um navegador Chrome, a imagem é convertida para o formato WebP, com tamanho 500 x 500. E, unsharp mask=0.1,1,5 está em uma qualidade WebP que corresponde a uma qualidade de JPEG de 85 o mais próximo possível. O espaço dessa conversão WebP é comparado com o JPEG e o menor dos dois é retornado.

## Preciso alterar URLs, predefinições de imagens ou implantar um novo código no meu site para o Smart Imaging? {#will-i-have-to-change-any-urls-image-presets-or-deploy-any-new-code-on-my-site-for-smart-imaging}

Não. O recurso Smart Imaging funciona perfeitamente com os URLs de imagem e as predefinições de imagem existentes. Além disso, o Smart Imaging não requer a adição de código ao seu site para detectar o navegador do usuário. Toda essa funcionalidade é tratada automaticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

## O recurso Smart Imaging funciona com HTTPS? E HTTP/2? {#does-smart-imaging-working-with-https-how-about-http}

A Criação de imagens inteligentes funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

## Posso usar imagens inteligentes? {#am-i-eligible-to-use-smart-imaging}

Para usar a Smart Imaging, a conta Dynamic Media Classic ou Dynamic Media on Experience Manager de sua empresa deve atender aos seguintes requisitos:

* Use a CDN (Content Delivery Network) agrupada em Adobe como parte de sua licença.
* Use um domínio dedicado (por exemplo, `images.company.com` ou `mycompany.scene7.com`), não um domínio genérico (por exemplo, `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa.

Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**. Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**. Se você usa um domínio genérico no momento, é possível solicitar a mudança para seu próprio domínio personalizado. Faça essa solicitação de transição ao enviar um caso de suporte.

Seu primeiro domínio personalizado não tem custo adicional com uma licença do Dynamic Media.

## Qual é o processo de ativação de Imagem inteligente para minha conta? {#what-is-the-process-for-enabling-smart-imaging-for-my-account}

Quando uma solicitação é iniciada para usar a Imagem inteligente, ela não é ativada automaticamente.

Crie um caso de suporte conforme descrito abaixo. Em seu caso de suporte, mencione qual dos seguintes recursos de Imagem inteligente (um ou mais) você deseja habilitar em sua conta:

* WebP
* AVIF
* Otimização da DPR e da largura de banda da rede
* PNG para AVIF com perda ou WebP com perda

Se você já tiver o recurso Smart Imaging habilitado com o WebP, mas quiser outros recursos novos como os listados acima, crie um caso de suporte.

**Para criar um caso de suporte para habilitar a Imagem inteligente na sua conta:**

1. [Use o Admin Console para iniciar a criação de um novo caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Forneça as seguintes informações no seu caso de suporte:

   * Nome do contato principal, email, telefone.

   * Liste quais dos seguintes recursos de Imagem inteligente (um ou mais) você deseja habilitar em sua conta:
      * WebP
      * AVIF
      * Otimização da DPR e da largura de banda da rede
      * PNG para AVIF com perda ou WebP com perda
   * Todos os domínios a serem ativados para Smart Imaging (ou seja, `images.company.com` ou `mycompany.scene7.com`).

      Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa.

      Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**.

   * Verifique se você está usando o CDN por meio do Adobe e se não é gerenciado com um relacionamento direto.

   * Verifique se você está usando um domínio dedicado, como `images.company.com` ou `mycompany.scene7.com`, e não um domínio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

      Para encontrar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), em seguida, faça logon na(s) conta(s) da empresa.

      Ir para **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configurações gerais]**.

      Procure o campo rotulado **[!UICONTROL Nome do servidor publicado]**. Se você estiver usando um domínio Dynamic Media Classic genérico no momento, poderá solicitar a mudança para seu próprio domínio personalizado como parte dessa transição.

   * Indique se deseja que ele funcione em HTTP/2.


1. O Suporte ao cliente do Adobe adiciona você à Lista de espera do cliente do Smart Imaging com base na ordem em que as solicitações são enviadas.
1. Quando o Adobe estiver pronto para lidar com sua solicitação, o Suporte ao cliente entrará em contato com você para coordenar e definir uma data limite.
1. **Opcional**: opcionalmente, é possível testar a Criação de imagens inteligentes no armazenamento temporário antes que o Adobe coloque o novo recurso em produção.
1. Você será notificado após a conclusão pelo Suporte ao cliente.
1. Para maximizar as melhorias de desempenho do Smart Imaging, a Adobe recomenda configurar o TTL (Time To Live) para 24 horas ou mais. O TTL define por quanto tempo os ativos são armazenados em cache pelo CDN. Para alterar essa configuração:

   1. Se você usar o Dynamic Media Classic, acesse **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do aplicativo]** > **[!UICONTROL Configuração de publicação]** > **[!UICONTROL Servidor de imagens]**. Defina o **[!UICONTROL Tempo de vida padrão do cache do cliente]** para 24 ou mais.
   1. Se você usar o Dynamic Media, siga [estas instruções](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab). Defina o **[!UICONTROL Expiração]** valor de 24 horas ou mais.

## Quando posso esperar que minha conta seja habilitada com o Smart Imaging? {#when-can-i-expect-my-account-to-be-enabled-with-smart-imaging}

As solicitações são processadas na ordem em que são recebidas pelo Suporte ao cliente, de acordo com a Lista de espera.

>[!NOTE]
>
>O lead time pode ser longo, pois a ativação do Smart Imaging envolve a limpeza do cache pelo Adobe. Portanto, somente algumas transições de clientes podem ser tratadas em um determinado momento.

## Quais são os riscos da mudança para o uso do Smart Imaging? {#what-are-the-risks-with-switching-over-to-use-smart-imaging}

Não há riscos para a página da Web de um cliente. No entanto, a transição para o Smart Imaging limpa seu cache de CDN. Essa operação envolve a mudança para uma nova configuração do Dynamic Media Classic ou Dynamic Media no Experience Manager.

Durante a transição inicial, as imagens não armazenadas em cache atingem diretamente os servidores de origem do Adobe até que o cache seja reconstruído. Dessa forma, o Adobe planeja lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao extrair solicitações da origem. Para a maioria dos clientes, o cache é totalmente reconstruído na CDN dentro de ~1 a 2 dias.

## Como posso verificar se a Imagem inteligente está funcionando como esperado?{#how-can-i-verify-whether-smart-imaging-is-working-as-expected}

1. Depois que sua conta for configurada com o Smart Imaging, carregue um URL de imagem do Dynamic Media Classic ou do Adobe Experience Manager - Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome acessando **[!UICONTROL Exibir]** > **[!UICONTROL Desenvolvedor]** > **[!UICONTROL Ferramentas do desenvolvedor]** no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows®, navegue até configurações no painel de ferramentas do desenvolvedor e selecione **[!UICONTROL Desabilitar cache (enquanto devtools estiver aberto)]** caixa de seleção
   * No macOS, no painel do desenvolvedor, em **[!UICONTROL Rede]** selecione **[!UICONTROL desativar cache]**.

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A captura de tela a seguir mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome. Se o domínio tiver o AVIF ativado, também será possível esperar ver o AVIF no Tipo de conteúdo.
1. Repita esse teste em navegadores diferentes e condições do usuário.

>[!NOTE]
>
>Nem todas as imagens são convertidas. O recurso Smart Imaging decide se a conversão pode melhorar o desempenho. Às vezes, quando não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

## Como saber o ganho de desempenho? Existe uma maneira de conhecer os benefícios do Smart Imaging? {#benefits}

O cabeçalho Smart Imaging determina os benefícios da Smart Imaging. Quando a Imagem inteligente estiver ativada, depois de solicitar uma imagem, na **[!UICONTROL Cabeçalhos de resposta]** cabeçalho, você pode ver `-X-Adobe-Smart-Imaging` como visto no exemplo destacado a seguir:

![Cabeçalho de imagens inteligentes](/help/assets/assets-dm/smart-imaging-header2.png)

Esse cabeçalho informa o seguinte:

* As imagens inteligentes estão funcionando para a empresa.
* Um valor positivo significa que a conversão foi bem-sucedida. Nesse caso, uma nova imagem WebP é retornada.
* Um valor negativo significa que a conversão não foi bem-sucedida. Nesse caso, a imagem original solicitada é retornada (JPEG por padrão, se não especificado).
* Um valor positivo mostra a diferença em bytes entre a imagem solicitada e a nova imagem. No exemplo acima, os bytes salvos são `75048` ou aproximadamente 75 KB para uma imagem.
* Um valor negativo significa que a imagem solicitada é menor que a nova imagem. A diferença negativa de tamanho é mostrada, mas a imagem veiculada é somente a imagem solicitada original.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 com o WebP sendo fornecido**
>
>Se o valor de `X-Adobe-Smart-Imaging` é -1 e o WebP ainda está sendo fornecido, significa que o Smart Imaging está funcionando, mas os benefícios de tamanho não foram calculados devido ao cache antigo. Você pode usar `cache=update` (somente uma vez) no URL da imagem para corrigir esse problema.
>Um exemplo de uso do modificador:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Para invalidar todo o cache, você deve criar um caso de suporte.

## Como posso desativar a otimização de AVIF na Imagem inteligente?{#disable-avif}

Se quiser voltar a servir WebP por padrão, crie um caso de suporte para o mesmo. Como de costume, é possível desativar o Smart Imaging adicionando o parâmetro `bfc=off` ao URL da imagem. No entanto, não é possível selecionar WebP ou AVIF no modificador de URL para Imagem inteligente. Essa capacidade é mantida no nível da conta da empresa.

## O recurso Smart Imaging pode ser desativado para qualquer solicitação?{#turning-off-smart-imaging}

Sim. Você pode desativar o Smart Imaging adicionando qualquer um dos seguintes modificadores:

* `bfc=off` para desativar a Conversão de Formato de Navegador. Consulte também [Conversão de Formato de Navegador](#bfc).
* `dpr=off` para desativar a Proporção de pixels do dispositivo. Consulte também [Proporção de pixels do dispositivo](#dpr).
* `network=off` para desativar a largura de banda da rede. Consulte também [Largura de banda de rede](#network).

## Que &quot;ajuste&quot; está disponível? Há configurações ou comportamentos que podem ser definidos? {#tuning-settings}

A Imagem inteligente tem três opções que podem ser ativadas ou desativadas.

* [Conversão de Formato de Navegador](#bfc)
* [Proporção de pixels do dispositivo](#dpr)
* [Largura de banda de rede](#network)

## Eu tenho um URL com fmt=tif no navegador Chrome. Mas minha solicitação falha com um erro ImageServer. Por quê? {#fmt-tif}

Esse erro não ocorrerá se a Imagem inteligente não estiver ativada em sua conta. A imagem inteligente funciona somente com os formatos JPEG ou PNG.

Para evitar esse erro, você pode:

* Especifique JPEG ou PNG ou
* Não usar o `fmt` modificador, ou
* Use um formato de preferência de navegador definido pelo Smart Imaging. Por exemplo, você pode usar WebP para navegador Chrome.

## Quero baixar uma imagem de TIFF do URL de uma imagem. Como faço isso? {#download-tif}

Adicionar `fmt=tif` e `bfc=off` para o caminho do URL da imagem.

## A Imagem inteligente gerencia apenas o formato de imagem ou também as configurações de qualidade de imagem para obter melhores resultados?

A imagem inteligente usa formato e qualidade. O restante dos parâmetros permanece o mesmo, se solicitado no URL da imagem.

## Se a Imagem inteligente gerenciar as configurações de qualidade, há mínimos e máximos que eu posso definir? Em outras palavras, uma qualidade que não seja inferior a 60 e não superior a 80? {#quality-setting}

Atualmente não há esse provisionamento.

## O Smart Imaging ajusta automaticamente a configuração de saída percentual de qualidade ou essa é uma configuração ajustada manualmente e se aplica a todas as imagens? Dentro de que alcance? {#percent-quality}

A Smart Imaging ajusta automaticamente a porcentagem de qualidade. Essa porcentagem de qualidade é determinada usando um algoritmo de aprendizado de máquina desenvolvido pelo Adobe. Essa porcentagem não é específica de intervalo.

## Com o Smart Imaging, quais comandos de veiculação de imagens são suportados ou ignorados? {#support-ignore}

Os únicos comandos ignorados são `fmt` e `qlt`. Todos os comandos restantes são suportados.

## Somente imagens JPEG são substituídas por imagens inteligentes? E se eu solicitar um WebP, PNG ou algo diferente? {#replace-request}

Essa funcionalidade funciona somente para JPEG e PNG.

## Por que uma imagem JPEG às vezes é retornada ao Chrome em vez de WebP? {#jpeg-returned}

O recurso Smart Imaging determina se a conversão é benéfica ou não. Ela retorna a nova imagem, somente da conversão que é benéfica.

## Por que a funcionalidade da Proporção de pixels do dispositivo (dpr) não funciona como esperado com imagens compostas? {#composite-images}

Se uma imagem composta envolver muitas camadas, a funcionalidade da dpr poderá ser afetada ao usar um modificador de posição. Esse problema é conhecido e será corrigido em versões futuras do Smart Imaging. Se outras funcionalidades do Smart Imaging não estiverem funcionando como esperado, você poderá criar um caso de suporte para reportar o problema.

## Por que o PNG do Smart Imaging ainda é convertido em WebP/AVIF sem perdas? {#convert-to-lossless}

Como o PNG é um formato sem perdas, o WebP e o AVIF anteriores entregues sem perdas resultantes têm um tamanho maior do que o esperado. O Smart Imaging agora oferece suporte à conversão com perdas. Você pode usar o modificador `cache=update` (somente uma vez) em uma solicitação de imagem para corrigir esse problema. Um exemplo de uso desse modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar todo o cache, você deve criar um caso de suporte solicitando esse esforço.

## Como posso continuar usando o PNG para conversão sem perdas no Smart Imaging? {#continue-using}

O Smart Imaging agora oferece suporte à conversão com perdas com base no nível de qualidade. Para continuar usando a conversão sem perdas, você pode usar a qualidade 100 definida pelas configurações de sua empresa ou pelo URL da imagem usando `qlt=100` no caminho.