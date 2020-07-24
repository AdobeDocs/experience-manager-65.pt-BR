---
title: Práticas recomendadas para otimização da qualidade de imagens
description: Conheça as práticas recomendadas para otimizar a qualidade de imagem no Dynamic Media
uuid: b73f0918-c723-4a0d-a63f-4242223c2d47
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 12baf001-dfc9-410a-9821-a3bae1324392
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 5%

---


# Práticas recomendadas para otimização da qualidade de imagens {#best-practices-for-optimizing-the-quality-of-your-images}

A otimização da qualidade da imagem pode ser um processo demorado, já que muitos fatores contribuem para a renderização de resultados aceitáveis. O resultado é parcialmente subjetivo porque os indivíduos percebem a qualidade da imagem de forma diferente. Experimentação estruturada é fundamental.

O AEM inclui mais de 100 comandos de delivery de imagem do Dynamic Media para ajustar e otimizar imagens e resultados de renderização. As diretrizes a seguir podem ajudá-lo a dinamizar o processo e obter bons resultados rapidamente usando alguns comandos essenciais e práticas recomendadas.

## Práticas recomendadas para o formato de imagem (`&fmt=`) {#best-practices-for-image-format-fmt}

* JPG ou PNG são as melhores opções para fornecer imagens em boa qualidade e com tamanho e peso gerenciáveis.
* Se nenhum comando format for fornecido no URL, o Delivery de Imagem Dynamic Media assumirá como padrão o JPG para o delivery.
* O JPG compacta com uma proporção de 10:1 e geralmente produz arquivos de imagem menores. O PNG compacta com uma proporção de aproximadamente 2:1, exceto em alguns casos, como quando imagens contêm um fundo branco. Normalmente, porém, os tamanhos de arquivo PNG são maiores que os arquivos JPG.
* O JPG usa compactação com perdas, o que significa que os elementos da imagem (pixels) são descartados durante a compactação. Por outro lado, o PNG usa compactação sem perdas.
* Muitas vezes, o JPG compacta imagens fotográficas com melhor fidelidade do que imagens sintéticas com bordas e contraste nítidos.
* Se suas imagens contiverem transparência, use PNG, pois o JPG não oferece suporte para transparência.

Como prática recomendada para o formato de imagem, start com a configuração mais comum `&fmt=JPG`.

## Práticas recomendadas para o tamanho da imagem {#best-practices-for-image-size}

Reduzir dinamicamente o tamanho da imagem é uma das tarefas mais comuns. Ela envolve especificar o tamanho e, opcionalmente, qual modo de redução de resolução é usado para diminuir a escala da imagem.

* Para dimensionamento de imagem, a melhor e mais simples abordagem é usar `&wid=<value>` e `&hei=<value>,`ou apenas `&hei=<value>`. Esses parâmetros definem automaticamente a largura da imagem de acordo com a proporção.
* `&resMode=<value>`controla o algoritmo usado para diminuir a resolução. Start com `&resMode=sharp2`. Esse valor fornece a melhor qualidade de imagem. Embora a redução da resolução `value =bilin` seja mais rápida, geralmente resulta na suavização de artefatos.

Como prática recomendada para dimensionamento de imagem, use `&wid=<value>&hei=<value>&resMode=sharp2` ou `&hei=<value>&resMode=sharp2`

## Práticas recomendadas para a nitidez da imagem {#best-practices-for-image-sharpening}

O ajuste da nitidez da imagem é o aspecto mais complexo do controle de imagens em seu site e onde muitos erros são cometidos. Aproveite o tempo para saber mais sobre como a nitidez e o mascaramento nítido funcionam no AEM, consultando os seguintes recursos úteis:

White paper de práticas recomendadas [O ajuste de nitidez de imagens no Adobe Scene7 Publishing System e no Image Server](/help/assets/assets/s7_sharpening_images.pdf) também se aplica ao AEM.

<!-- To be reviewed and updated: Broken link.
See also [Sharpening an image with unsharp mask](https://helpx.adobe.com/photoshop/atv/cs6-tutorials/sharpening-an-image-with-unsharp-mask.html). -->

Com o AEM, você pode aumentar a nitidez das imagens na ingestão, no delivery ou em ambos. Entretanto, na maioria dos casos, é necessário aumentar a nitidez das imagens usando apenas um método ou outro, mas não ambos. O compartilhamento de imagens no delivery, em um URL, geralmente oferece os melhores resultados.

Existem dois métodos de nitidez de imagem que você pode usar:

* Nitidez simples ( `&op_sharpen`) - Semelhante ao filtro de nitidez usado no Photoshop, a nitidez simples aplica a nitidez básica à visualização final da imagem após o redimensionamento dinâmico. No entanto, esse método não é configurável pelo usuário. A prática recomendada é não usar &amp;op_sharpen, a menos que necessário.
* Mascaramento com nitidez ( `&op_USM`) - O mascaramento com nitidez é um filtro de nitidez padrão do setor. A prática recomendada é tornar as imagens nítidas com máscaras nítidas, seguindo as diretrizes abaixo. O mascaramento de nitidez permite controlar os três parâmetros a seguir:

   * `&op_sharpen=`quantidade,raio,limite

      * **[!UICONTROL quantidade]** (0-5, intensidade do efeito.)
      * **[!UICONTROL raio]** (0-250, largura das &quot;linhas de nitidez&quot; desenhadas ao redor do objeto com nitidez, conforme medido em pixels.)

         Lembre-se de que o raio e a quantidade dos parâmetros funcionam uns contra os outros. A redução do raio pode ser compensada pelo aumento do montante. O Raio permite um controle mais fino como um valor mais baixo aumenta a nitidez apenas dos pixels da borda, enquanto um valor mais alto aumenta a nitidez de uma faixa maior de pixels.

      * **[!UICONTROL limiar]** (0-255, sensibilidade do efeito.)

         Esse parâmetro determina como deve ser a diferença dos pixels com nitidez em relação à área ao redor antes de serem considerados pixels de borda e o filtro ajuste a nitidez deles. The **[!UICONTROL threshold]** parameter helps to avoid over-sharpening areas with similar colors, such as skin tones. Por exemplo, um valor limite de 12 ignora pequenas variações no brilho do tom da pele para evitar a adição de &quot;ruído&quot;, enquanto ainda adiciona o contraste da borda a áreas de alto contraste, como onde as pálpebras tocam a pele.
      Para obter mais informações sobre como você define esses três parâmetros, incluindo as práticas recomendadas para usar com o filtro, consulte os seguintes recursos:

      Tópico da Ajuda do AEM sobre como aumentar a nitidez de uma imagem.

      White paper de práticas recomendadas [Compartilhando imagens no Adobe Scene7 Publishing System e no Image Server](/help/assets/assets/s7_sharpening_images.pdf).

   * O AEM também permite controlar um quarto parâmetro: monocromático (0,1). Esse parâmetro determina se a máscara de nitidez é aplicada a cada componente de cor separadamente usando o valor 0 ou o brilho/intensidade da imagem usando o valor 1.


Como prática recomendada, start com o parâmetro de raio de máscara de nitidez. As configurações de Raio que você pode start são as seguintes:

* **[!UICONTROL Site]**: 0,2-0,3 pixels
* **[!UICONTROL Impressão fotográfica (250 a 300 ppi)]**: 0,3-0,5 pixels
* **[!UICONTROL Impressão offset (266 a 300 ppi)]**: 0,7 a 1,0 pixels
* **[!UICONTROL Impressão de tela (150 ppi)]**: 1,5 a 2,0 pixels

Aumentar gradualmente o montante de 1,75 para 4. Se a nitidez ainda não for a forma desejada, aumente o raio em um ponto decimal e execute a quantidade novamente de 1,75 a 4. Repita conforme necessário.

Deixe a configuração do parâmetro monocromático em 0.

### Práticas recomendadas para compactação JPEG (`&qlt=`) {#best-practices-for-jpeg-compression-qlt}

* Esse parâmetro controla a qualidade da codificação JPG. Um valor mais elevado significa uma imagem de qualidade mais elevada, mas com um tamanho de ficheiro grande; como alternativa, um valor mais baixo significa uma imagem de qualidade mais baixa, mas com um tamanho de arquivo menor. O intervalo para este parâmetro é de 0 a 100.
* Para otimizar a qualidade, não defina o valor do parâmetro como 100. A diferença entre uma configuração de 90 ou 95 e 100 é quase imperceptível, mas 100 aumenta desnecessariamente o tamanho do arquivo de imagem. Portanto, para otimizar a qualidade, mas evitar que os arquivos de imagem fiquem muito grandes, defina o valor `qlt= value` para 90 ou 95.
* Para otimizar para um pequeno tamanho de arquivo de imagem, mas manter a qualidade da imagem em um nível aceitável, defina `qlt= value` o como 80. Valores abaixo de 70 a 75 resultam em degradação significativa da qualidade da imagem.
* Como prática recomendada, para ficar no meio, defina `qlt= value` para 85 para ficar no meio.
* Usando o sinalizador de croma em `qlt=`

   * O `qlt=` parâmetro tem uma segunda configuração que permite ativar a redução da resolução de cromaticidade RGB usando o valor `,1` ou desativando usando o valor `,0`.
   * Para mantê-lo simples, o start com a redução da resolução de cromaticidade RGB desativada (`,0`). Essa configuração geralmente resulta em melhor qualidade de imagem, especialmente para imagens sintéticas com muitas bordas nítidas e contraste.

Como prática recomendada para o uso da compactação JPG `&qlt=85,0`.

## Práticas recomendadas para dimensionamento JPEG (`&jpegSize=`) {#best-practices-for-jpeg-sizing-jpegsize}

jpegSize é um parâmetro útil se você quiser garantir que uma imagem não exceda um determinado tamanho para delivery a dispositivos com memória limitada.

* Esse parâmetro é definido em kilobytes (`jpegSize=&lt;size_in_kilobytes&gt;`). Define o tamanho máximo permitido para o delivery de imagem.
* `&jpegSize=` interage com o parâmetro de compactação JPG `&qlt=`. Se a resposta JPG com o parâmetro de compactação JPG (`&qlt=`) especificado não exceder o valor jpegSize, a imagem será retornada com `&qlt=` a definição. Caso contrário, `&qlt=` será gradualmente diminuído até que a imagem se ajuste ao tamanho máximo permitido ou até que o sistema determine que ela não se ajusta e retorne um erro.

Como prática recomendada, defina `&jpegSize=` e adicione o parâmetro `&qlt=` se você estiver fornecendo imagens JPG a dispositivos com memória limitada.

## Resumo das práticas recomendadas {#best-practices-summary}

Como prática recomendada, para obter uma alta qualidade de imagem e um pequeno tamanho de arquivo, start com a seguinte combinação de parâmetros:

`fmt=jpg&qlt=85,0&resMode=sharp2&op_usm=1.75,0.3,2,0`

Essa combinação de configurações de produtos resulta em excelentes resultados na maioria das circunstâncias.

Se a imagem exigir otimização adicional, ajuste gradualmente os parâmetros de nitidez (máscara de nitidez) iniciando com um raio definido como 0,2 ou 0,3. Em seguida, aumente gradualmente a quantidade de 1,75 para um máximo de 4 (equivalente a 400% no Photoshop). Verifique se o resultado desejado foi obtido.

Se os resultados da nitidez ainda não forem satisfatórios, aumente o raio em incrementos decimais. Para cada incremento decimal, reinicie o valor em 1,75 e aumente-o gradualmente para 4. Repita esse processo até obter o resultado desejado. Embora os valores acima sejam uma abordagem que os estúdios criativos validaram, lembre-se de que você pode start com outros valores e seguir outras estratégias. Se os resultados são ou não satisfatórios para si é uma questão subjetiva, por isso é fundamental uma experimentação estruturada.

Durante o experimento, você também pode achar as seguintes sugestões gerais úteis para otimizar seu fluxo de trabalho:

* Tente testar diferentes parâmetros em tempo real, diretamente em um URL ou usando a funcionalidade de ajuste de imagem do Scene7 Publishing System, que fornece pré-visualizações em tempo real para operações de ajuste.
* Como prática recomendada, lembre-se de que é possível agrupar comandos do Dynamic Media Image Server em uma predefinição de imagem. Uma predefinição de imagem é basicamente macros de comando de URL com nomes predefinidos personalizados, como `$thumb_low$` e `&product_high$`. O nome predefinido personalizado em um caminho de URL faz uma chamada para essas predefinições. Essa funcionalidade ajuda a gerenciar comandos e configurações de qualidade para diferentes padrões de uso de imagens em seu site e reduz a duração geral dos URLs.
* O AEM também oferece maneiras mais avançadas de ajustar a qualidade da imagem, como aplicar imagens de nitidez na ingestão. Para casos de uso avançado em que essa pode ser uma opção para ajustar e otimizar ainda mais os resultados da renderização, o [Adobe Professional Services](https://www.adobe.com/experience-cloud/consulting-services.html) pode ajudá-lo com insight personalizado e práticas recomendadas.

