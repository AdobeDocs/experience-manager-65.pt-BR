---
title: Imagem inteligente
description: A Smart Imaging aplica as características de visualização exclusivas de cada usuário para fornecer as imagens certas otimizadas automaticamente para sua experiência, resultando em melhor desempenho e envolvimento.
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
feature: Asset Management,Renditions
role: User, Admin
exl-id: e427d4ee-d5c8-421b-9739-f3cf2de36e41
solution: Experience Manager, Experience Manager Assets
source-git-commit: 7fb3ec9654b56605321f0d12a4c1e23d2e18dab9
workflow-type: tm+mt
source-wordcount: '3322'
ht-degree: 0%

---

# Imagem inteligente {#smart-imaging}

A Smart Imaging aplica as características de visualização exclusivas de cada usuário para fornecer as imagens certas otimizadas automaticamente para sua experiência, resultando em melhor desempenho e envolvimento.

## Sobre imagens inteligentes {#what-is-smart-imaging}

A tecnologia Smart Imaging aplica os recursos de IA do Adobe Sensei e funciona com as &quot;predefinições de imagem&quot; existentes. Ele funciona para aprimorar o desempenho do delivery de imagens, otimizando automaticamente o formato, o tamanho e a qualidade da imagem com base nos recursos do navegador do cliente.

E agora, obtenha uma melhor pontuação do Google Core Web Vital para LCP (Largest Contentful Paint) com imagens inteligentes aprimoradas, que agora vêm com suporte para AVIF e WebP.

>[!IMPORTANT]
>
>A Criação de imagens inteligentes exige o uso do CDN (Content Delivery Network) pronto para uso que é fornecido com o Adobe Experience Manager - Dynamic Media. Qualquer outra CDN personalizada não é compatível com esse recurso.

>[!TIP]
>
>Experimente e descubra os benefícios dos modificadores de imagem do Dynamic Media e do Smart Imaging, usando o [_Instantâneo_](https://snapshot.scene7.com/) do Dynamic Media.
>
>O Instantâneo é uma ferramenta de demonstração visual criada para ilustrar o potencial do Dynamic Media para entrega de imagens otimizadas e dinâmicas. Experimente com imagens de teste ou URLs do Dynamic Media, para observar visualmente a saída de vários modificadores de imagem do Dynamic Media e otimizações de Imagem inteligente para o seguinte:
>
>* Tamanho do arquivo (com entrega WebP e AVIF)
>* Largura de banda de rede
>* DPR (Relação de pixels do dispositivo)
>
>Para saber como é fácil usar o Instantâneo, reproduza o [Vídeo de treinamento do Instantâneo](https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minutos e 17 segundos).

A Smart Imaging se beneficia do aumento de desempenho de estar totalmente integrado ao melhor serviço premium de CDN (Content Delivery Network) do Adobe. Este serviço encontra a rota de Internet ideal entre servidores, redes e pontos de correspondência. Ele encontra uma rota que tem a menor latência e a menor taxa de perda de pacotes em vez de usar a rota padrão na Internet.

Os seguintes exemplos de ativos de imagem representam a otimização da Imagem inteligente adicionada:

| Imagem (URL) | Miniatura  | Tamanho (JPEG) | Tamanho (WebP) com imagem inteligente | Tamanho (AVIF) com Smart Imaging | % de redução com WebP | % de redução com AVIF |
|---|---|---|---|---|---|---|
| [Imagem 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagem1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90,2 KB | 26,89% | 37,79% |
| [Imagem 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagem2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01% | 72,57% |
| [Imagem 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagem3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87,1 KB | 14,47% | 60,58% |
| [Imagem 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagem4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25% | 51,85% |

Semelhante ao acima, o Adobe também executou um teste com um conjunto de amostras maior. O formato AVIF forneceu 20% de redução extra do tamanho em relação ao WebP, que forneceu 27% de redução em relação ao JPEG. Tudo com a mesma qualidade visual. No total, a AVIF fornece redução média de até 41% no tamanho do JPEG.

Compare WebP e AVIF com PNG, você pode observar uma redução de 84% no tamanho com WebP e 87% com AVIF. E, como os formatos WebP e AVIF são compatíveis com transparência e animações de várias imagens, é um bom substituto para arquivos PNG e GIF transparentes.

Consulte também [Otimização de imagem com formatos de imagem de próxima geração (WebP e AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

## Benefícios da imagem inteligente {#what-are-the-key-benefits-of-smart-imaging}

A Imagem inteligente melhora a entrega de imagens, otimizando automaticamente o tamanho do arquivo com base no navegador do usuário, na exibição do dispositivo e nas condições da rede. Essa abordagem garante tempos de carregamento mais rápidos e uma melhor experiência de visualização em diferentes ambientes. Como as imagens constituem a maior parte do tempo de carregamento de uma página, qualquer melhoria de desempenho pode ter um profundo impacto nos KPIs de negócios, como o seguinte:

* Taxas de conversão mais altas.
* Tempo gasto em um site.
* Taxas de rejeição do site mais baixas.

Os principais benefícios mais recentes da Smart Imaging mais recente incluem:

* Suporta o formato AVIF da próxima geração.
* PNG para WebP e AVIF agora oferece suporte a conversões com perdas. Como o PNG é um formato sem perdas, o WebP e o AVIF anteriores eram sem perdas.
* Conversão de Formato de Navegador (`bfc`)
* Proporção de pixels do dispositivo (`dpr`)
* Largura de banda de rede (`network`)

### Sobre a Conversão de Formato de Navegador (bfc) {#bfc}

Ativar a Conversão de Formato de Navegador anexando `bfc=on` à URL da imagem converte automaticamente o JPEG e PNG em AVIF com perdas, WebP com perdas, JPEGXR com perdas, JPEG2000 com perdas para navegadores diferentes. Para navegadores que não oferecem suporte a esses formatos, o Smart Imaging continua a servir o JPEG ou o PNG. O recurso Smart Imaging recalcula a qualidade do novo formato junto com a alteração do formato.

Você pode desativar o Smart Imaging anexando `bfc=off` ao URL da imagem.

Consulte também [bfc](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc) na API de disponibilização e renderização de imagens do Dynamic Media.

### Sobre a otimização da Relação de pixels do dispositivo (dpr) {#dpr}

A Proporção de pixels do dispositivo (DPR), também chamada de Proporção de pixels CSS, representa a relação entre os pixels físicos e os pixels lógicos de um dispositivo. Com o aumento da retina, a resolução de pixels de dispositivos móveis modernos tem aumentado rapidamente.

Ativar a otimização da Proporção de pixels do dispositivo renderiza a imagem na resolução nativa da tela, o que a torna nítida.

Atualmente, a densidade de pixels da exibição vem dos valores de cabeçalho da CDN Akamai.

| Valores permitidos no URL de uma imagem | Descrição |
|---|---|
| `dpr=off` | Desative a otimização de DPR em um nível de URL de imagem individual. |
| `dpr=on,dprValue` | Substitua o valor do DPR detectado pelo Smart Imaging, com um valor personalizado (conforme detectado por qualquer lógica do lado do cliente ou por outros meios). O valor permitido para `dprValue` é qualquer número maior que 0. |

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

A ativação da largura de banda da rede ajusta automaticamente a qualidade da imagem fornecida com base na largura de banda real da rede. Para uma largura de banda de rede ruim, a otimização da DPR (Relação de pixels do dispositivo) é automaticamente desativada, mesmo que já esteja ativada.

Sua empresa pode desabilitar a otimização da largura de banda de rede para imagens individuais anexando `network=off` à URL da imagem.

| Valor permitido no URL de uma imagem | Descrição |
|---|---|
| `network=off` | Desativa a otimização de rede em um nível de URL de imagem individual. |

Os valores de DPR e largura de banda da rede são baseados nos valores detectados do lado do cliente do CDN empacotado. Esses valores às vezes são imprecisos. Por exemplo, iPhone5 com DPR=2 e iPhone12 com `dpr=3`, ambos mostram `dpr=2`. Mesmo assim, para dispositivos de alta resolução, enviar `dpr=2` é melhor do que enviar `dpr=1`. No entanto, a melhor maneira de superar essa imprecisão é usar a DPR do lado do cliente para fornecer valores 100% precisos. E funciona para qualquer dispositivo, seja Apple ou qualquer outro dispositivo que tenha sido iniciado. Consulte [Usar Imagem Inteligente com Proporção de Pixels do Dispositivo no lado do cliente](/help/assets/client-side-dpr.md).

### Principais benefícios adicionais da geração de imagens inteligentes

* Classificação da SEO do Google aprimorada para páginas da Web que usam a Imagem inteligente mais recente.
* Fornece conteúdo otimizado imediatamente (no tempo de execução).
* Usa a tecnologia Adobe Sensei para converter de acordo com a qualidade (`qlt`) especificada na solicitação de imagem.
* TTL (Time To Live) independente. Anteriormente, um TTL mínimo de 12 horas era obrigatório para que o Smart Imaging funcionasse.
* Anteriormente, as imagens originais e derivadas eram armazenadas em cache e era um processo de duas etapas para invalidar o cache. Na última geração do Smart Imaging, somente os derivados são armazenados em cache, permitindo um processo de invalidação de cache de etapa única.
* Os clientes que usam cabeçalhos personalizados em seu conjunto de regras se beneficiam da geração de Smart Imaging mais recente, pois esses cabeçalhos não são bloqueados, ao contrário da versão anterior do Smart Imaging. Por exemplo, &quot;Origem de permissão de tempo&quot; e &quot;X-Robot&quot; como sugerido em [Adicionar um valor de cabeçalho personalizado às respostas da imagem|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Perguntas frequentes

+++Há custos de licenciamento associados ao Smart Imaging?

Não. A imagem inteligente está incluída em sua licença atual do. Essa regra é verdadeira para Dynamic Media Classic ou Experience Manager - Dynamic Media (No local, AMS e Experience Manager as a Cloud Service).

>[!NOTE]
>
>A Criação de imagens inteligentes não está disponível para clientes Dynamic Media - Hybrid.

+++

+++Como funciona o Smart Imaging?

Quando um consumidor solicita uma imagem, o Smart Imaging analisa as características do usuário e as converte no formato apropriado com base no navegador. Essas conversões de formato são feitas de uma maneira que não prejudica a fidelidade visual. A geração de imagens inteligentes converte automaticamente imagens em diferentes formatos com base na capacidade do navegador da seguinte maneira.

* Converter automaticamente para AVIF se o navegador der suporte ao formato
* Converter automaticamente em WebP se a conversão AVIF não foi benéfica ou se o navegador não oferece suporte a AVIF
* Converter automaticamente para JPEG2000 se o Safari não for compatível com WebP
* Converter automaticamente em JPEGXR para IE 9+ ou se o Edge não for compatível com WebP

  | Formato da imagem | Navegadores compatíveis |
  |---|---|
  | AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
  | WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
  | JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
  | JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |

* Para navegadores que não aceitam esses formatos, o formato de imagem solicitado originalmente é fornecido.

Se o tamanho original da imagem for menor do que o produzido pela Smart Imaging, a imagem original será fornecida.

+++

+++Quais formatos de imagem são compatíveis?

Os formatos de imagem a seguir são compatíveis com o Smart Imaging:

* JPEG
* PNG

O recurso Smart Imaging recalcula a qualidade dos formatos de arquivo de imagem JPEG ao converter para um novo formato.

Para formatos de arquivo de imagem que oferecem suporte a transparência, como PNG, você pode configurar a Imagem inteligente para fornecer AVIF e WebP com perdas. Para a conversão de formato com perdas, o Smart Imaging usa a qualidade mencionada no URL da imagem ou a qualidade configurada na conta da empresa do Dynamic Media.

+++

+++Como o Smart Imaging funciona com minhas predefinições de imagem existentes que já estão em uso?

A Smart Imaging integra-se perfeitamente com suas predefinições de imagens existentes, respeitando todas as suas configurações de imagem.

Os únicos ajustes envolvem o formato da imagem, a qualidade ou ambos. Durante a conversão de formatos, a Imagem inteligente preserva a fidelidade visual total de acordo com as configurações predefinidas, mas fornece um tamanho de arquivo menor. Basta habilitá-lo adicionando `bfc=on`, `dpr=on,dprValue`, `network=on` ou todas as três configurações de parâmetro às suas URLs ou predefinições existentes.

Por exemplo, digamos que uma predefinição de imagem especifique um formato de JPEG a 500 × 500 pixels, com `quality=85` e `unsharp mask=0.1,1,5`. A Smart Imaging detecta se o usuário está em um navegador Chrome. Em seguida, converte a imagem em WebP com as mesmas dimensões (500 × 500) e uma máscara de nitidez correspondente às configurações de JPEG. O sistema então compara os tamanhos dos arquivos das versões WebP e JPEG e serve o menor para o usuário.

+++

<!--

### Do I have to change any URLs, image presets, or deploy any new code on my site for Smart Imaging? 

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++O Smart Imaging funciona com HTTPS? E HTTP/2?

A Criação de imagens inteligentes funciona com imagens entregues por HTTP ou HTTPS. Além disso, também funciona por HTTP/2.

+++

+++Posso usar a Criação de imagens inteligentes?

A Criação de imagens inteligentes está disponível imediatamente para todos os clientes. Para começar a aproveitar seus benefícios, basta adicionar `bfc=on`, `dpr=on,dprValue`, `network=on` ou todas as três configurações de parâmetro às suas URLs ou predefinições existentes.

Para usar a Imagem inteligente, a conta Dynamic Media Classic ou Dynamic Media on Experience Manager de sua empresa deve incluir o CDN (Content Delivery Network) incluído no Adobe como parte de sua licença.

+++

+++Qual é o processo para habilitar a Imagem inteligente de uma conta?

Para começar a usar Smart Imaging, anexe `bfc=on`, `dpr=on,dprValue`, `network=on` ou todas as três configurações de parâmetro às suas URLs ou predefinições existentes. Se preferir não fazer essas alterações manualmente, é possível habilitar o Smart Imaging por padrão criando um caso de suporte.

Ao criar o caso de suporte, especifique quais recursos de Imagem inteligente você deseja ativar em sua conta:

* Conversão de formato de navegador (WebP ou AVIF)
* Otimização da largura de banda da rede

>[!NOTE]
>
>O DPR requer ajustes do lado do cliente para determinar o `dprValue` correto. Portanto, o Adobe recomenda habilitar o DPR por meio de URLs, anexando `dpr=on,dprValue`.

**Para criar um caso de suporte para habilitar a Imagem Inteligente na sua conta:**

1. [Use o Admin Console para iniciar a criação de um novo caso de suporte](https://helpx.adobe.com/br/enterprise/using/support-for-experience-cloud.html).
1. Forneça as seguintes informações no seu caso de suporte:

   * **Detalhes do contato primário:**

      * Forneça seu nome, email e número de telefone.

   * **Recursos de Imagem Inteligente a serem habilitados:**

      * Liste os recursos que deseja para sua conta:

         * Conversão do formato do navegador: WebP ou AVIF
         * Otimização da largura de banda da rede
         * DPR: O DPR requer ajustes do lado do cliente para determinar o `dprValue` correto. Portanto, o Adobe recomenda habilitar o DPR por meio de URLs, anexando `dpr=on,dprValue`.

   * **Domínio para Smart Imaging:**

      * Listar todos os domínios relevantes, como *`company.com`* ou *`mycompany.scene7.com`*
      * A Imagem inteligente é compatível com domínios genéricos e personalizados.
      * Para identificar seus domínios, abra o [aplicativo de desktop do Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started) e entre na conta da sua empresa.

         1. Navegue até **[!UICONTROL Configuração]** > **[!UICONTROL Configuração do Aplicativo]** > **[!UICONTROL Configurações Gerais]**.
         1. Procure o campo **[!UICONTROL Nome do Servidor Publicado]** para confirmar seu domínio.
         1. Verifique se você está usando o CDN do Adobe em vez de um gerenciado por outro provedor.

   * **Indicar suporte HTTP/2:**

      * Especifique se você precisa que o Smart Imaging funcione em HTTP/2.

1. O Suporte ao cliente do Adobe ativa os recursos de Imagem inteligente solicitados por padrão, eliminando a necessidade de anexar parâmetros manualmente aos URLs.
1. A Adobe recomenda definir o TTL (Time To Live) para pelo menos 24 horas, a fim de maximizar o desempenho por meio do armazenamento em cache.
Para ajustar o TTL:

   1. **Para Dynamic Media Classic:**
      1. Navegue até **[!UICONTROL Instalação]** > **[!UICONTROL Instalação do Aplicativo]** > **[!UICONTROL Instalação do Publish]** > **[!UICONTROL Servidor de Imagens]**.
      1. Defina o valor **[!UICONTROL Tempo de Vida do Cache de Cliente Padrão]** para 24 horas ou mais.
   1. **Para Dynamic Media no Adobe Experience Manager:**
      1. Siga [estas instruções](/help/assets/dm-publish-settings.md#common-thumbnail-attributes-tab).
      1. Defina o valor de **[!UICONTROL Expiration]** para 24 horas ou mais.

+++

+++Quando posso esperar que uma conta seja ativada com o Smart Imaging?

O Suporte ao cliente processa as solicitações na ordem em que elas as recebem, seguindo a Lista de espera.

>[!NOTE]
>
>O lead time pode ser longo, pois a ativação do Smart Imaging envolve a limpeza do cache pelo Adobe. Portanto, somente algumas transições de clientes podem ser tratadas em um determinado momento.

+++

+++Quais são os riscos da alternância para o uso do Smart Imaging?

Não há riscos para a página da Web de um cliente. No entanto, a transição para o Smart Imaging limpa seu cache de CDN. Essa operação envolve a mudança para uma nova configuração do Dynamic Media Classic ou Dynamic Media no Experience Manager.

Durante a transição inicial, as imagens não armazenadas em cache atingem diretamente os servidores de origem do Adobe até que o cache seja reconstruído. Dessa forma, o Adobe planeja lidar com algumas transições de clientes de cada vez, para que o desempenho aceitável seja mantido ao extrair solicitações da origem. Para a maioria dos clientes, o cache é totalmente reconstruído na CDN dentro de ~1 a 2 dias.

+++

+++Como posso verificar se o Smart Imaging está funcionando como esperado?

1. Depois que sua conta for configurada com o Smart Imaging, carregue um URL de imagem do Dynamic Media Classic ou do Adobe Experience Manager - Dynamic Media no navegador.
1. Abra o painel do desenvolvedor do Chrome acessando **[!UICONTROL Exibir]** > **[!UICONTROL Desenvolvedor]** > **[!UICONTROL Ferramentas do desenvolvedor]** no navegador. Ou escolha qualquer ferramenta de desenvolvedor de navegador de sua escolha.

1. Certifique-se de que o cache esteja desativado quando as ferramentas do desenvolvedor estiverem abertas.

   * No Windows®, navegue até as configurações no painel de ferramentas do desenvolvedor e marque a caixa de seleção **[!UICONTROL Desabilitar cache (enquanto devtools estiver aberto)]**.
   * No macOS, no painel Desenvolvedor, na guia **[!UICONTROL Rede]**, selecione **[!UICONTROL desabilitar cache]**.

1. Observe que o Tipo de conteúdo é transformado no formato apropriado. A captura de tela a seguir mostra uma imagem PNG sendo convertida dinamicamente em WebP no Chrome. Se o domínio tiver o AVIF ativado, também será possível esperar ver o AVIF no Tipo de conteúdo.
1. Repita esse teste em navegadores diferentes e condições do usuário.

>[!NOTE]
>
>Nem todas as imagens são convertidas. O recurso Smart Imaging decide se a conversão pode melhorar o desempenho. Às vezes, quando não há ganho de desempenho esperado ou o formato não é JPEG ou PNG, a imagem não é convertida.

![image2017-11-14_15398](/help/assets/assets/image2017-11-14_15398.png)

+++

+++Como saber o ganho de desempenho? Existe uma maneira de conhecer os benefícios do Smart Imaging?

O cabeçalho Smart Imaging determina os benefícios da Smart Imaging. Quando a Imagem inteligente estiver habilitada, após solicitar uma imagem, no cabeçalho **[!UICONTROL Cabeçalhos de resposta]**, você poderá ver `-X-Adobe-Smart-Imaging` como visto no exemplo destacado a seguir:

![Cabeçalho de imagens inteligentes](/help/assets/assets-dm/smart-imaging-header2.png)

Esse cabeçalho informa o seguinte:

* As imagens inteligentes estão funcionando para a empresa.
* Um valor positivo significa que a conversão foi bem-sucedida. Nesse caso, uma nova imagem WebP é retornada.
* Um valor negativo significa que a conversão não foi bem-sucedida. Nesse caso, a imagem original solicitada é retornada (JPEG por padrão, se não especificado).
* Um valor positivo mostra a diferença em bytes entre a imagem solicitada e a nova imagem. No exemplo acima, os bytes salvos são `75048` ou aproximadamente 75 KB para uma imagem.
* Um valor negativo significa que a imagem solicitada é menor que a nova imagem. A diferença negativa de tamanho é mostrada, mas a imagem veiculada é somente a imagem solicitada original.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 com o WebP sendo entregue**
>
>Se o valor de `X-Adobe-Smart-Imaging` for -1 e o WebP ainda estiver sendo entregue, o Smart Imaging estará ativo. No entanto, os benefícios de tamanho não foram calculados devido ao cache desatualizado. Você pode usar `cache=update` (apenas uma vez) na URL da imagem para corrigir esse problema.
>Um exemplo de uso do modificador:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Para invalidar todo o cache, você deve criar um caso de suporte.

+++

+++Como posso desabilitar a otimização de AVIF no Smart Imaging?

Se quiser voltar a servir WebP por padrão, crie um caso de suporte para o mesmo. Como de costume, você pode desativar o Smart Imaging adicionando o parâmetro `bfc=off` ao URL da imagem. No entanto, não é possível selecionar WebP ou AVIF no modificador de URL para Imagem inteligente. Essa capacidade é mantida no nível da conta da empresa.

+++

+++O recurso Smart Imaging pode ser desativado para qualquer solicitação?

Sim. Você pode desativar o Smart Imaging adicionando qualquer um dos seguintes modificadores:

* `bfc=off` para desativar a Conversão de Formato de Navegador. Consulte também [Conversão de formato de navegador](#bfc).
* `dpr=off` para desativar a Proporção de Pixels do Dispositivo. Consulte também [Proporção de pixels do dispositivo](#dpr).
* `network=off` para desativar a largura de banda da rede. Consulte também [Largura de Banda da Rede](#network).

+++

+++Que &quot;ajuste&quot; está disponível? Há configurações ou comportamentos que podem ser definidos?

A Imagem inteligente tem três opções que podem ser ativadas ou desativadas.

* [Conversão de Formato de Navegador](#bfc)
* [Proporção de pixels do dispositivo](#dpr)
* [Largura de banda de rede](#network)

+++

+++Eu tenho um URL com fmt=tif no navegador da Web do Chrome. Mas minha solicitação falha com um erro ImageServer. Por quê?

Esse erro não ocorrerá se a Imagem inteligente não estiver ativada em sua conta. A imagem inteligente funciona somente com os formatos JPEG ou PNG.

Para evitar esse erro, você pode:

* Especifique JPEG ou PNG ou
* Não usar o modificador `fmt`, ou
* Use um formato de preferência de navegador definido pelo Smart Imaging. Por exemplo, você pode usar WebP para o navegador da Web Chrome.

+++

+++Desejo baixar uma imagem de TIFF do URL de uma imagem. Como faço isso?

Adicione `fmt=tif` e `bfc=off` ao caminho da URL da imagem.

+++

+++O Smart Imaging gerencia apenas o formato de imagem ou também as configurações de qualidade de imagem para obter os melhores resultados?

A imagem inteligente usa formato e qualidade. O restante dos parâmetros permanece o mesmo, se solicitado no URL da imagem.

+++

+++Se a Imagem inteligente gerenciar as configurações de qualidade, há mínimos e máximos que posso definir? Em outras palavras, uma qualidade que não seja inferior a 60 e não superior a 80?

Atualmente não há esse provisionamento.

+++

+++O Smart Imaging ajusta automaticamente a configuração de saída de qualidade percentual ou essa é uma configuração ajustada manualmente e se aplica a todas as imagens? Dentro de que alcance?

A Smart Imaging ajusta automaticamente a porcentagem de qualidade. Essa qualidade é determinada usando um algoritmo de aprendizado de máquina desenvolvido pelo Adobe. Essa porcentagem não é específica de intervalo.

+++

+++Com Smart Imaging, quais comandos do Servidor de imagens são suportados ou ignorados?

Os únicos comandos ignorados são `fmt` e `qlt`. Todos os comandos restantes são suportados.

+++

+++Somente imagens em JPEG são substituídas pelo recurso Smart Imaging? E se eu solicitar um WebP, PNG ou algo diferente?

Essa funcionalidade funciona somente para JPEG e PNG.

+++

+++Por que uma imagem de JPEG às vezes é retornada ao Chrome em vez de WebP?

O recurso Smart Imaging determina se a conversão é benéfica ou não. Ela retorna a nova imagem, somente da conversão que é benéfica.

+++

+++Por que a funcionalidade de Proporção de pixels de dispositivo (dpr) não funciona como esperado com imagens compostas?

Se uma imagem composta envolver muitas camadas, a funcionalidade da dpr poderá ser afetada ao usar um modificador de posição. Esse problema é conhecido e deve ser corrigido em versões futuras do Smart Imaging. Se outras funcionalidades do Smart Imaging não estiverem funcionando como esperado, você poderá criar um caso de suporte para reportar o problema.

+++

+++Por que o PNG do Smart Imaging ainda é convertido em WebP/AVIF sem perdas?

Como o PNG é um formato sem perdas, os WebP e AVIF anteriores entregues não tiveram perdas, o resultado é um tamanho maior do que o esperado. O Smart Imaging agora oferece suporte à conversão com perdas. Você pode usar o modificador `cache=update` (apenas uma vez) em uma solicitação de imagem para corrigir esse problema. Um exemplo de uso desse modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar todo o cache, você deve criar um caso de suporte solicitando esse esforço.

+++

+++Como posso continuar usando PNG para conversão sem perdas no Smart Imaging?

O Smart Imaging agora oferece suporte à conversão com perdas com base no nível de qualidade. Você pode continuar usando a conversão sem perdas definindo a qualidade para 100, seja através das configurações da sua empresa, ou adicionando `qlt=100` ao caminho de URL da imagem.

+++

