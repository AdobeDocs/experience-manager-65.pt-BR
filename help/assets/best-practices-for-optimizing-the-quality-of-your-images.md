---
title: Práticas recomendadas para otimização da qualidade de imagens no Dynamic Media
description: Conheça as práticas recomendadas para otimização da qualidade de imagem no Dynamic Media
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '1497'
ht-degree: 4%

---

# Práticas recomendadas para otimização da qualidade de imagens no Dynamic Media {#best-practices-for-optimizing-the-quality-of-your-images}

A otimização da qualidade da imagem pode ser um processo demorado, pois muitos fatores contribuem para a obtenção de resultados aceitáveis. O resultado é parcialmente subjetivo porque os indivíduos percebem a qualidade da imagem de forma diferente. A experimentação estruturada é fundamental.

O Adobe Experience Manager inclui mais de 100 comandos de entrega de imagens do Dynamic Media para ajustar e otimizar imagens e renderizar resultados. As diretrizes a seguir podem ajudar você a simplificar o processo e obter bons resultados rapidamente usando alguns comandos essenciais e práticas recomendadas.

## Práticas recomendadas para formato de imagem (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG ou PNG são as melhores opções para fornecer imagens em boa qualidade e com tamanho e peso gerenciáveis.
* Se nenhum comando format for fornecido no URL, o Dynamic Media Image Delivery assume o padrão JPG para entrega.
* O JPG é compactado a uma proporção de 10:1 e geralmente produz arquivos de imagem menores. O PNG é compactado em uma proporção de aproximadamente 2:1, exceto às vezes, como quando as imagens contêm um fundo branco. Geralmente, porém, os tamanhos dos arquivos PNG são maiores que os arquivos JPG.
* O JPG usa compactação com perdas, o que significa que os elementos de imagem (pixels) são descartados durante a compactação. Por outro lado, o PNG usa compactação sem perdas.
* O JPG geralmente compacta imagens fotográficas com melhor fidelidade do que imagens sintéticas com bordas nítidas e contraste.
* Se suas imagens contiverem transparência, use PNG porque o JPG não oferece suporte a transparência.

Como prática recomendada para o formato de imagem, comece com a configuração mais comum `&fmt=JPG`.

## Práticas recomendadas para tamanho de imagem {#best-practices-for-image-size}

Reduzir dinamicamente o tamanho da imagem é uma das tarefas mais comuns. Envolve a especificação do tamanho e, opcionalmente, o modo de redução da resolução usado para diminuir a escala da imagem.

* Para dimensionamento de imagens, a melhor e mais simples abordagem é usar `&wid=<value>` e `&hei=<value>,`ou apenas `&hei=<value>`. Esses parâmetros definem automaticamente a largura da imagem de acordo com a taxa de proporção.
* `&resMode=<value>`controla o algoritmo usado para diminuir a resolução. Iniciar com `&resMode=sharp2`. Esse valor fornece a melhor qualidade de imagem. Ao usar a redução da resolução `value =bilin` for mais rápido, geralmente resultará no suavização de artefatos.

Como prática recomendada para dimensionamento de imagem, use `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`

## Práticas recomendadas para nitidez de imagem {#best-practices-for-image-sharpening}

A nitidez de imagem é o aspecto mais complexo de controlar imagens no seu site e no qual muitos erros são cometidos. Reserve tempo para saber mais sobre como a nitidez e a nitidez do mascaramento funcionam no Experience Manager, consultando os seguintes recursos úteis:

White paper de práticas recomendadas [Nitidez de imagens no Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf) que se aplica ao Experience Manager também.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Com o Experience Manager, você pode ajustar a nitidez de imagens na assimilação, no delivery ou em ambos. No entanto, geralmente, ajuste a nitidez de imagens usando apenas um método ou outro, mas não ambos. A nitidez de imagens no delivery, em um URL, normalmente fornece os melhores resultados.

Há dois métodos de nitidez de imagem que podem ser usados:

* Nitidez simples ( `&op_sharpen`) - Semelhante ao filtro de nitidez usado no Photoshop, a nitidez simples aplica a nitidez básica à exibição final da imagem após o redimensionamento dinâmico. No entanto, esse método não é configurável pelo usuário. A prática recomendada é não usar &amp;op_sharpen, a menos que seja necessário.
* Mascaramento sem nitidez ( `&op_USM`) - Tirar nitidez da máscara é um filtro de nitidez padrão do setor. A prática recomendada é tornar mais nítidas as imagens com mascaramento sem nitidez, seguindo as diretrizes abaixo. O mascaramento sem nitidez permite controlar os três parâmetros a seguir:

   * `&op_sharpen=amount,radius,threshold`

      * **[!UICONTROL *quantidade *]**(0-5, intensidade do efeito.)
      * **[!UICONTROL *raio *]**(0-250, largura das &quot;linhas de nitidez&quot; desenhadas ao redor do objeto com nitidez, medida em pixels.)

     Lembre-se de que o raio e a quantidade dos parâmetros funcionam uns contra os outros. A redução do raio pode ser compensada pelo aumento da quantidade. O raio permite um controle mais fino, pois um valor mais baixo aplica nitidez apenas aos pixels da borda, enquanto um valor mais alto aplica nitidez a uma faixa mais ampla de pixels.

      * **[!UICONTROL *limite *]**(0-255, sensibilidade do efeito.)

            Esse parâmetro determina como deve ser a diferença dos pixels com nitidez em relação à área ao redor antes de serem considerados pixels de borda e o filtro ajuste a nitidez deles. O parâmetro **[!UICONTROL limite]** ajuda a evitar áreas de nitidez excessiva com cores semelhantes, como tons de pele. Por exemplo, um valor limite de 12 ignora pequenas variações no brilho do tom da pele para evitar a adição de &quot;ruído&quot;, enquanto ainda adiciona o contraste da borda a áreas de alto contraste, como onde as pálpebras tocam a pele.
        
        Para obter mais informações sobre como você define esses três parâmetros, incluindo as práticas recomendadas para usar com o filtro, consulte os seguintes recursos:

        Experience Manager Tópico da Ajuda sobre Nitidez de uma imagem.

        White paper de práticas recomendadas [Nitidez de imagens no Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf).

      * Experience Manager também permite controlar um quarto parâmetro: monocromático (0,1). Esse parâmetro determina se a máscara de nitidez é aplicada separadamente a cada componente de cor usando o valor 0 ou ao brilho/intensidade da imagem usando o valor 1.

Como prática recomendada, comece com o parâmetro Tirar nitidez do raio da máscara. As configurações de raio com as quais você pode começar são as seguintes:

* **[!UICONTROL Site]** - 0,2-0,3 pixels
* **[!UICONTROL Impressão fotográfica (250-300 ppi)]** - 0,3-0,5 pixels
* **[!UICONTROL Impressão offset (266-300 ppi)]** - 0,7-1,0 pixels
* **[!UICONTROL Impressão de tela de desenho (150 ppi)]** - 1,5 a 2,0 pixels

Aumente gradualmente a quantidade de 1,75 para 4. Se a nitidez ainda não for a desejada, aumente o raio em um ponto decimal e execute a quantidade novamente de 1,75 para 4. Repita conforme necessário.

Deixe a configuração de parâmetro monocromático em 0.

### Práticas recomendadas para compactação de JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Esse parâmetro controla a qualidade da codificação do JPG. Um valor mais alto significa uma imagem de qualidade superior, mas um tamanho de arquivo grande; como alternativa, um valor mais baixo significa uma imagem de qualidade inferior, mas um tamanho de arquivo menor. O intervalo desse parâmetro é de 0 a 100.
* Para otimizar a qualidade, não defina o valor do parâmetro como 100. A diferença entre uma configuração de 90 ou 95 e 100 é quase imperceptível, mas 100 aumenta desnecessariamente o tamanho do arquivo de imagem. Portanto, para otimizar a qualidade, mas evitar que os arquivos de imagem fiquem muito grandes, defina o `qlt= value` 90 ou 95.
* Para otimizar o tamanho de um arquivo de imagem pequeno, mas manter a qualidade da imagem em um nível aceitável, defina o `qlt= value` a 80. Valores abaixo de 70 a 75 resultam em degradação significativa da qualidade da imagem.
* Como prática recomendada, para ficar no meio, defina o `qlt= value` 85 para ficar no meio.
* Uso do sinalizador de croma no `qlt=`

   * A variável `qlt=` tem uma segunda configuração que permite ativar a redução de resolução de cromaticidade de RGB usando o valor `,1` ou off usando o valor `,0`.
   * Para simplificar, comece com a redução de resolução de cromaticidade de RGB desativada (`,0`). Essa configuração geralmente resulta em melhor qualidade de imagem, especialmente para imagens sintéticas com muitas bordas e contraste nítidos.

Como prática recomendada para o uso da compactação JPG `&qlt=85,0`.

## Práticas recomendadas para dimensionamento de JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize é um parâmetro útil se você quiser garantir que uma imagem não exceda um determinado tamanho para ser entregue a dispositivos que tenham memória limitada.

* Esse parâmetro é definido em quilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Ele define o tamanho máximo permitido para a entrega de imagens.
* `&jpegSize=` O interage com o parâmetro de compactação JPG `&qlt=`. Se a resposta do JPG com o parâmetro de compactação de JPG especificado (`&qlt=`) não exceder o valor jpegSize, a imagem será retornada com `&qlt=` conforme definido. Caso contrário, `&qlt=` é diminuído gradualmente até que a imagem se ajuste ao tamanho máximo permitido ou até que o sistema determine que não é possível se ajustar e retorne um erro.

Como prática recomendada, defina `&jpegSize=` e adicione o parâmetro `&qlt=` se estiver fornecendo imagens de JPG para dispositivos com memória limitada.

## Resumo de práticas recomendadas {#best-practices-summary}

Como prática recomendada, para atingir uma alta qualidade de imagem e um tamanho de arquivo pequeno, comece com a seguinte combinação de parâmetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Esta combinação de produtos de configurações excelentes resultados na maioria das circunstâncias.

Se a imagem exigir mais otimização, ajuste gradualmente os parâmetros de nitidez (mascaramento sem nitidez), começando com um raio definido como 0,2 ou 0,3. Em seguida, aumente gradualmente o valor de 1,75 para no máximo 4 (equivalente a 400% no Photoshop). Verifique se o resultado desejado foi atingido.

Se os resultados da nitidez ainda não forem satisfatórios, aumente o raio em incrementos decimais. Para cada incremento decimal, reinicie o valor em 1,75 e aumente gradualmente para 4. Repita esse processo até atingir o resultado desejado. Embora os valores acima sejam uma abordagem validada pelos estúdios de criação, lembre-se de que você pode começar com outros valores e seguir outras estratégias. Se os resultados são satisfatórios para você ou não é uma questão subjetiva, portanto, a experimentação estruturada é fundamental.

À medida que você experimenta, as seguintes sugestões gerais podem ser úteis para otimizar ainda mais seu fluxo de trabalho:

* Experimente e teste diferentes parâmetros em tempo real, diretamente em um URL.
* Como prática recomendada, lembre-se de que é possível agrupar comandos do Servidor de imagens do Dynamic Media em uma predefinição de imagem. Uma predefinição de imagem consiste basicamente em macros de comando de URL com nomes predefinidos personalizados, como `$thumb_low$` e `&product_high$`. O nome da predefinição personalizada em um caminho de URL chama essas predefinições. Essa funcionalidade ajuda a gerenciar comandos e configurações de qualidade para diferentes padrões de uso de imagens no site e reduz o comprimento geral dos URLs.
* O Experience Manager também oferece maneiras mais avançadas de ajustar a qualidade da imagem, como aplicar nitidez às imagens na assimilação. Para casos de uso avançados em que há opções para ajustar e otimizar os resultados de renderização, [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) O pode ajudá-lo com insights e práticas recomendadas personalizadas.
