---
title: Práticas recomendadas para otimização da qualidade de imagens
description: Conheça as práticas recomendadas para otimizar a qualidade da imagem no Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
feature: Gerenciamento de ativos
role: User, Admin
exl-id: 7a568cae-e505-4b3a-abc5-8aae723460c3
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 6%

---

# Práticas recomendadas para otimização da qualidade de imagens {#best-practices-for-optimizing-the-quality-of-your-images}

A otimização da qualidade da imagem pode ser um processo demorado, pois muitos fatores contribuem para a renderização de resultados aceitáveis. O resultado é parcialmente subjetivo porque os indivíduos percebem a qualidade da imagem de forma diferente. A experimentação estruturada é fundamental.

O Adobe Experience Manager inclui mais de 100 comandos de delivery de imagens Dynamic Media para ajustar e otimizar imagens e resultados de renderização. As diretrizes a seguir podem ajudar você a simplificar o processo e obter bons resultados rapidamente usando alguns comandos essenciais e práticas recomendadas.

## Práticas recomendadas para o formato de imagem (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG ou PNG são as melhores opções para fornecer imagens em boa qualidade e com tamanho e peso gerenciáveis.
* Se nenhum comando format for fornecido no URL, o padrão do Dynamic Media Image Delivery é JPG para entrega.
* O JPG compacta em uma proporção de 10:1 e geralmente produz tamanhos de arquivo de imagem menores. O PNG compacta em uma proporção de cerca de 2:1, exceto às vezes, como quando as imagens contêm um fundo branco. Normalmente, porém, os tamanhos dos arquivos PNG são maiores que os arquivos JPG.
* O JPG usa compactação com perdas, o que significa que os elementos da imagem (pixels) são soltos durante a compactação. Por outro lado, o PNG usa compactação sem perdas.
* O JPG geralmente compacta imagens fotográficas com mais fidelidade do que imagens sintéticas com bordas e contraste nítidos.
* Se suas imagens contêm transparência, use o PNG, pois o JPG não oferece suporte à transparência.

Como prática recomendada para o formato de imagem, comece com a configuração mais comum `&fmt=JPG`.

## Práticas recomendadas para o tamanho da imagem {#best-practices-for-image-size}

A redução dinâmica do tamanho da imagem é uma das tarefas mais comuns. Ela envolve especificar o tamanho e, opcionalmente, qual modo de diminuição da amostragem é usado para fazer o downscale da imagem.

* Para dimensionamento de imagem, a melhor e mais simples abordagem é usar `&wid=<value>` e `&hei=<value>,`ou apenas `&hei=<value>`. Esses parâmetros definem automaticamente a largura da imagem de acordo com a proporção.
* `&resMode=<value>`controla o algoritmo usado para a resolução. Comece com `&resMode=sharp2`. Esse valor fornece a melhor qualidade de imagem. Embora o uso da amostragem decrescente `value =bilin` seja mais rápido, ele geralmente resulta na aliasing de artefatos.

Como prática recomendada para o dimensionamento de imagem, use `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`

## Práticas recomendadas para nitidez da imagem {#best-practices-for-image-sharpening}

A nitidez da imagem é o aspecto mais complexo do controle de imagens em seu site, e onde muitos erros são cometidos. Reserve tempo para saber mais sobre como a nitidez e o mascaramento nítido funcionam no Experience Manager, referindo-se aos seguintes recursos úteis:

White paper de práticas recomendadas [Nitidez imagens no Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf) que também se aplica ao Experience Manager.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Com o Experience Manager, é possível aprimorar as imagens na ingestão, na entrega ou em ambos. No entanto, normalmente, imagens com nitidez usando apenas um método ou o outro, mas não ambos. A nitidez de imagens na entrega, em um URL, normalmente fornece os melhores resultados.

Existem dois métodos de nitidez de imagem que você pode usar:

* Nitidez simples ( `&op_sharpen`) - Semelhante ao filtro de nitidez usado no Photoshop, a nitidez simples aplica nitidez básica à exibição final da imagem após o redimensionamento dinâmico. No entanto, esse método não é configurável pelo usuário. A prática recomendada é não usar &amp;op_sharpen, a menos que seja necessário.
* Mascaramento com nitidez ( `&op_USM`) - O mascaramento com nitidez é um filtro de nitidez padrão do setor. A prática recomendada é aprimorar as imagens com máscara nítida seguindo as diretrizes abaixo. O mascaramento de nitidez permite controlar os três parâmetros a seguir:

   * `&op_sharpen=`quantia,raio,limite

      * **[!UICONTROL montante]**  (0-5, intensidade do efeito).
      * **[!UICONTROL radius]**  (0-250, largura das &quot;linhas de nitidez&quot; desenhadas ao redor do objeto com nitidez, conforme medido em pixels.)

      Lembre-se de que o raio e a quantidade dos parâmetros funcionam uns contra os outros. A redução do raio pode ser compensada pelo aumento do montante. O Raio permite um controle mais fino como um valor mais baixo ajuste somente os pixels da borda, enquanto um valor mais alto aumenta a nitidez de uma faixa maior de pixels.

      * **[!UICONTROL limiar]**  (0-255, sensibilidade do efeito.)

             Esse parâmetro determina como deve ser a diferença dos pixels com nitidez em relação à área ao redor antes de serem considerados pixels de borda e o filtro ajuste a nitidez deles. O parâmetro **[!UICONTROL limite]** ajuda a evitar áreas de nitidez excessiva com cores semelhantes, como tons de pele. Por exemplo, um valor limite de 12 ignora pequenas variações no brilho do tom da pele para evitar a adição de &quot;ruído&quot;, enquanto ainda adiciona o contraste da borda a áreas de alto contraste, como onde as pálpebras tocam a pele.
         
         Para obter mais informações sobre como você define esses três parâmetros, incluindo práticas recomendadas para usar com o filtro, consulte os seguintes recursos:

         Tópico de Ajuda do Experience Manager sobre Nitidez de uma imagem.

         White paper de práticas recomendadas [Nitidez imagens no Adobe Dynamic Media Classic](/help/assets/assets/sharpening_images.pdf).

      * O Experience Manager também permite controlar um quarto parâmetro: monocromático (0,1). Esse parâmetro determina se o mascaramento com nitidez é aplicado a cada componente de cor separadamente usando o valor 0 ou o brilho/intensidade da imagem usando o valor 1.


Como prática recomendada, comece com o parâmetro de raio da máscara de nitidez. As configurações de Raio que você pode começar são as seguintes:

* **[!UICONTROL Site]**  - 0.2-0.3 pixels
* **[!UICONTROL Impressão fotográfica (250-300 ppi)]**  - 0,3-0,5 pixels
* **[!UICONTROL Impressão offset (266-300 ppi)]**  - 0,7-1,0 pixels
* **[!UICONTROL Impressão de tela (150 ppi)]**  - 1,5-2,0 pixels

Aumente gradualmente o montante de 1,75 para 4. Se a nitidez ainda não for a maneira desejada, aumente o raio em um ponto decimal e execute o valor novamente de 1,75 para 4. Repita conforme necessário.

Deixe a configuração do parâmetro monocromático em 0.

### Práticas recomendadas para compactação JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Esse parâmetro controla a qualidade da codificação JPG. Um valor mais elevado significa uma imagem de qualidade superior, mas com um tamanho de ficheiro grande; como alternativa, um valor mais baixo significa uma imagem de qualidade mais baixa, mas com um tamanho de arquivo menor. O intervalo desse parâmetro é de 0 a 100.
* Para otimizar a qualidade, não defina o valor do parâmetro como 100. A diferença entre uma configuração de 90 ou 95 e 100 é quase imperceptível, mas 100 aumenta desnecessariamente o tamanho do arquivo de imagem. Portanto, para otimizar a qualidade, mas evitar que os arquivos de imagem fiquem muito grandes, defina `qlt= value` como 90 ou 95.
* Para otimizar para um pequeno tamanho de arquivo de imagem, mas manter a qualidade da imagem em um nível aceitável, defina `qlt= value` como 80. Valores inferiores a 70 a 75 resultam em degradação significativa da qualidade da imagem.
* Como prática recomendada, para permanecer no meio, defina o `qlt= value` como 85 para permanecer no meio.
* Uso do sinalizador de croma em `qlt=`

   * O parâmetro `qlt=` tem uma segunda configuração que permite ativar a redução da amostragem de cromaticidade RGB usando o valor `,1` ou desligado usando o valor `,0`.
   * Para simplificar, comece com a redução da amostragem de cromaticidade RGB desativada (`,0`). Essa configuração geralmente resulta em melhor qualidade de imagem, especialmente para imagens sintéticas com muitas bordas e contraste nítidos.

Como prática recomendada para a compactação JPG, use `&qlt=85,0`.

## Práticas recomendadas para dimensionamento JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize é um parâmetro útil se você quiser garantir que uma imagem não excede um determinado tamanho para ser entregue a dispositivos com memória limitada.

* Esse parâmetro é definido em kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Ela define o tamanho máximo permitido para a entrega de imagens.
* `&jpegSize=` interage com o parâmetro de compactação JPG  `&qlt=`. Se a resposta JPG com o parâmetro de compactação JPG especificado (`&qlt=`) não exceder o valor de jpegSize, a imagem será retornada com `&qlt=`, conforme definido. Caso contrário, `&qlt=` será reduzido gradualmente até que a imagem se ajuste ao tamanho máximo permitido ou até que o sistema determine que não é possível ajustar e retorne um erro.

Como prática recomendada, defina `&jpegSize=` e adicione o parâmetro `&qlt=` se estiver fornecendo imagens JPG a dispositivos com memória limitada.

## Resumo das práticas recomendadas {#best-practices-summary}

Como prática recomendada, para obter uma alta qualidade de imagem e um tamanho de arquivo pequeno, comece com a seguinte combinação de parâmetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Essa combinação de configurações de produtos é um excelente resultado na maioria das circunstâncias.

Se a imagem exigir mais otimização, ajuste gradualmente os parâmetros de nitidez (mascaramento com nitidez), começando com um raio definido como 0,2 ou 0,3. Em seguida, aumente gradualmente a quantidade de 1,75 para um máximo de 4 (equivalente a 400% no Photoshop). Verifique se o resultado desejado foi atingido.

Se os resultados de nitidez ainda não forem satisfatórios, aumente o raio em incrementos decimais. Para cada incremento decimal, reinicie o valor em 1,75 e aumente-o gradualmente para 4. Repita esse processo até atingir o resultado desejado. Embora os valores acima sejam uma abordagem que os estúdios criativos validaram, lembre-se de que é possível começar com outros valores e seguir outras estratégias. Se os resultados são ou não satisfatórios para si é uma questão subjetiva, por isso a experimentação estruturada é fundamental.

À medida que você experimenta, as seguintes sugestões gerais podem ser úteis para otimizar ainda mais seu fluxo de trabalho:

* Tente e teste diferentes parâmetros em tempo real, diretamente em um URL.
* Como prática recomendada, lembre-se de que é possível agrupar comandos do Dynamic Media Image Serving em uma predefinição de imagem. Uma predefinição de imagem é basicamente macros de comando de URL com nomes predefinidos personalizados, como `$thumb_low$` e `&product_high$`. O nome predefinido personalizado em um caminho de URL chama essas predefinições. Essa funcionalidade ajuda você a gerenciar comandos e configurações de qualidade para diferentes padrões de uso de imagens no seu site e reduz o tamanho geral dos URLs.
* O Experience Manager também oferece formas mais avançadas de ajustar a qualidade da imagem, como aplicar imagens de nitidez na assimilação. Para casos de uso avançado em que há opções para ajustar e otimizar os resultados de renderização, o [Adobe Professional Services](https://business.adobe.com/customers/consulting-services/main.html) pode ajudá-lo com o insight personalizado e as práticas recomendadas.
