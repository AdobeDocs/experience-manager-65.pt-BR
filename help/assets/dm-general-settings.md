---
title: Definir as configurações gerais do Dynamic Media
description: Saiba como gerenciar configurações gerais no Dynamic Media. Você pode definir o nome do servidor de publicação e o nome do servidor de origem aqui e definir uma opção de substituição de imagem. Também há opções de upload padrão para mascarar as imagens com nitidez e opções de upload de como você deseja processar arquivos PostScript, Adobe Photoshop, PDF e Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: 55cc7c57-87a0-4bfb-b226-36d01d36849a
source-git-commit: 9c548dbc0157607adda5ed76cab8ef970588e1e9
workflow-type: tm+mt
source-wordcount: '2498'
ht-degree: 4%

---

# Definir as configurações gerais do Dynamic Media

Configuração **[!UICONTROL Configurações gerais do Dynamic Media]** está disponível apenas se:

* Você está executando o Dynamic Media no modo Scene7. Consulte [Ativar o Dynamic Media no modo Scene7](/help/assets/config-dms7.md#enabling-dynamic-media-in-scene-mode).
* Você tem um *existente* **[!UICONTROL Configuração do Dynamic Media]** (em **[!UICONTROL Cloud Services]**) no Adobe Experience Manager 6.5.11 ou superior. Consulte [Criar uma configuração do Dynamic Media no Cloud Services](/help/assets/config-dms7.md#configuring-dynamic-media-cloud-services).
* Você é um administrador de sistema do Experience Manager com privilégios de administrador.

As Configurações gerais do Dynamic Media são destinadas ao uso por desenvolvedores e programadores de sites experientes. O Adobe Dynamic Media recomenda que os usuários que alteram essas configurações de publicação conheçam o Dynamic Media no Adobe Experience Manager e a tecnologia básica de geração de imagens.

Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos para sua empresa. Esses servidores são usados para criar strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas da sua conta do .

A página Configuração de publicação do Dynamic Media estabelece as configurações padrão que determinam como os ativos são entregues dos servidores do Adobe Dynamic Media para sites ou aplicativos da Web. Se nenhuma configuração for especificada, o servidor Adobe Dynamic Media fornece um ativo de acordo com uma configuração padrão que foi configurada na página Configuração de publicação do Dynamic Media.

Consulte também [Opcional - Configuração e configuração do Dynamic Media - Configurações do modo Scene7](/help/assets/config-dms7.md#optional-setup-and-configuration-of-dynamic-media-scene7-mode-settings) para tarefas de configuração mais opcionais.

>[!NOTE]
>
>Atualização do Dynamic Media Classic para o Dynamic Media no Adobe Experience Manager? A página Configurações gerais e [Configuração de publicação](/help/assets/dm-publish-settings.md) no Dynamic Media são preenchidas previamente com os valores obtidos da sua conta do Dynamic Media Classic. As exceções são todos os valores listados na variável **[!UICONTROL Opções de upload padrão]** da página Configurações gerais . Esses valores já estão no Experience Manager. Dessa forma, quaisquer alterações feitas sob **[!UICONTROL Opções de upload padrão]**, em qualquer uma das cinco guias, por meio da interface do usuário do Experience Manager, são refletidas no Dynamic Media, não no Dynamic Media Classic. Todas as outras configurações e valores na página Configurações gerais e na [Configuração de publicação](/help/assets/dm-publish-settings.md) são mantidas entre o Dynamic Media Classic e o Dynamic Media no Experience Manager.

**Para configurar as Configurações gerais do Dynamic Media:**

1. No modo Autor do Experience Manager, selecione o logotipo do Experience Manager para acessar o console de navegação global.
1. No painel à esquerda, selecione o ícone Ferramentas e vá para **[!UICONTROL Ativos]** > **[!UICONTROL Configurações gerais do Dynamic Media]**.
1. Na página Servidor , defina seu **[!UICONTROL Nome do servidor publicado]** e **[!UICONTROL Nome do servidor de origem]** e, em seguida, use as cinco guias para configurar as opções de upload padrão para Edição de imagem e para arquivos Postscript, Photoshop, PDF e Illustrator.

   * [Servidor](#server-general-setting)
   * [Carregar no aplicativo](#upload-to-application)
   * [Edição de imagem](#image-editing-tab) guia
   * [PostScript](#postscript-tab) guia
   * [Photoshop](#photoshop-tab) guia
   * [PDF](#pdf-tab) guia
   * [Illustrator](#illustrator-tab) guia

   ![Página Configurações gerais do Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *página Configurações gerais do Dynamic Media , com o **[!UICONTROL Edição de imagem]**selecionada.*<br><br>

1. Quando terminar, próximo ao canto superior direito da página, selecione **[!UICONTROL Salvar]**.

## Servidor {#server-general-setting}

Na criação da conta, o Adobe Dynamic Media fornece automaticamente os servidores atribuídos para sua empresa. Esses servidores são usados para criar strings de URL para seu site e aplicativos. Essas chamadas de URL são específicas da sua conta do .

| Opção | Descrição |
| --- | --- |
| **[!UICONTROL Nome do servidor publicado]** | Obrigatório.<br>O nome deve usar `https://` no caminho.<br>Este servidor é o servidor CDN (Content Deliver Network) ao vivo usado em todas as chamadas de URL geradas pelo sistema que são específicas da sua conta. Não altere o nome deste servidor a menos que seja instruído a fazê-lo pelo Suporte Técnico Adobe. |
| **[!UICONTROL Nome do servidor de origem]** | Obrigatório.<br>Este servidor é usado somente para testes de controle de qualidade. Não altere o nome deste servidor a menos que seja instruído a fazê-lo pelo Suporte Técnico Adobe. |

## Carregar no aplicativo {#upload-to-application}

* **[!UICONTROL Substituir imagens]**

   O Adobe Dynamic Media não permite que dois arquivos tenham o mesmo nome. A Adobe Dynamic Media ID de cada item (o nome da imagem menos a extensão do nome do arquivo) deve ser exclusiva. Por causa dessa regra, **[!UICONTROL Fazer upload para o aplicativo]** tem uma substituição. O efeito exato dessa opção depende da opção de Substituição de imagens especificada que você escolheu. Essas opções especificam como as imagens de substituição são carregadas: se eles substituem as imagens originais ou se tornam imagens duplicadas. Imagens duplicadas são renomeadas com um `-1`. Por exemplo, `chair.tif` é renomeado `chair-1.tif`. Essas opções afetam as imagens carregadas em uma pasta diferente da original ou as imagens com uma extensão de nome de arquivo diferente da original, como JPG, TIF ou PNG.

   >[!NOTE]
   >
   >Para manter a consistência com o Experience Manager, selecione a opção Substituir imagens **[!UICONTROL Substituir na pasta atual, mesmo nome/extensão base]**.

   | Opção Substituir imagens | Descrição |
   | --- | --- |
   | **[!UICONTROL Substituir na pasta atual, mesmo nome base/extensão]** | *Padrão* somente para novas contas do Dynamic Media.<br>Essa opção é a regra mais rígida para substituição. Ela requer que você carregue a imagem de substituição na mesma pasta do original e que a imagem de substituição tenha a mesma extensão de nome de arquivo do original. Se esses requisitos não forem atendidos, uma duplicata será criada.<br>*Para manter a consistência com o Experience Manager, selecione essa opção*. |
   | **[!UICONTROL Substituir na pasta atual, mesmo nome base independentemente da extensão]** | Requer que você carregue a imagem de substituição na mesma pasta do original, no entanto, a extensão do nome do arquivo pode ser diferente do original. Por exemplo, chair.tif substitui chair.jpg. |
   | **[!UICONTROL Substituir em qualquer pasta, mesmo nome/extensão do ativo base]** | Requer que a imagem de substituição tenha a mesma extensão de nome de arquivo que a imagem original (por exemplo, chair.jpg deve substituir chair.jpg, não chair.tif). No entanto, é possível fazer upload da imagem de substituição para uma pasta diferente da original. A imagem atualizada reside na nova pasta; o arquivo não pode mais ser encontrado em seu local original. |
   | **[!UICONTROL Substituir em qualquer pasta, mesmo nome de ativo base independentemente da extensão]** | Essa é a regra de substituição mais inclusiva. Você pode fazer upload de uma imagem de substituição para uma pasta diferente do original, fazer upload de um arquivo com uma extensão de nome de arquivo diferente e substituir o arquivo original. Se o arquivo original estiver em uma pasta diferente, a imagem de substituição residirá na nova pasta para a qual foi carregada. |

* **[!UICONTROL Preservar corte]**

   Controla a preservação de qualquer definição manual de cultura existente.

   Consulte também `preserveCrop` em [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) e [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambos no Guia de referência de visualizadores do Dynamic Media.

## Opções padrão de upload {#default-upload-options}

### Guia Edição de imagem {#image-editing-tab}

Esse filtro permite ajustar um efeito de filtro de nitidez na imagem final com resolução reduzida. Ajuda a controlar a intensidade do efeito, o raio do efeito (conforme medido em pixels) e um limite de contraste que é ignorado.

O efeito Tirar nitidez da máscara usa as mesmas opções do filtro Tirar nitidez da máscara da Photoshop. Ao contrário do que o nome sugere, Tirar nitidez da máscara é um filtro de nitidez.

| Tirar nitidez das opções de Máscara | Descrição |
| --- | --- |
| **[!UICONTROL Quantidade]** | Obrigatório.<br>Controla a quantidade de contraste que é aplicada aos pixels da borda.<br>Pense nisso como a intensidade do efeito. A principal diferença entre os valores de quantidade de Tirar nitidez da máscara no Adobe Dynamic Media e os valores de quantidade no Adobe Photoshop é que o Photoshop tem um intervalo de quantidade de 1% a 500%. Enquanto no Adobe Dynamic Media, o intervalo de valores é `0.0` para `5.0`. Um valor de 5,0 no Adobe Dynamic Media é o equivalente aproximado de 500% no Photoshop; um valor de 0,9 é o equivalente a 90%, e assim por diante. |
| **[!UICONTROL Raio]** | Obrigatório.<br>Controla o raio do efeito.<br>O intervalo de valores é `0` para `250`. O efeito é executado em todos os pixels em uma imagem e irradia de todos os pixels em todas as direções. O raio é medido em pixels. Por exemplo, para obter um efeito de nitidez semelhante para uma imagem de 2000 x 2000 pixels e imagem de 500 x 500 pixels, você define um raio de dois pixels na imagem de 2000 x 2000 pixels. Em seguida, defina um valor de raio de um pixel na imagem de 500 x 500 pixels. Um valor maior é usado para uma imagem que tem mais pixels. |
| **[!UICONTROL Limite]** | Obrigatório.<br>O limite é um intervalo de contraste que é ignorado quando o filtro Tirar nitidez da máscara é aplicado. Esse efeito é importante para que nenhum &quot;ruído&quot; seja introduzido em uma imagem quando esse filtro for usado. O intervalo de valores é `0` - `255`, que é o número de etapas de brilho em uma imagem em tons de cinza. `0`=black, `128`=50% cinza e `255`=branco.<br>Um valor limite de `12` O ignora pequenas variações é o brilho do tom da pele para evitar a adição de ruído, mas ainda adiciona o contraste da borda a áreas contrastantes, como onde as pálpebras tocam a pele.<br>Se você tiver uma foto do rosto de alguém, a máscara de nitidez afeta as partes contrastantes da imagem. Por exemplo, onde as pálpebras e a pele se encontram para criar uma área de contraste óbvia e a própria pele lisa. Mesmo a pele mais suave apresenta alterações sutis nos valores de brilho. Se você não usar um valor de limite, o filtro acentuará essas sutis alterações em pixels da pele. Por sua vez, um efeito ruidoso e indesejável é criado enquanto o contraste nas pálpebras aumenta, aumentando a nitidez.<br>Para evitar esse problema, é introduzido um valor limite que informa ao filtro para ignorar pixels que não alteram o contraste drasticamente, como pele lisa.<br>No gráfico zipper mostrado anteriormente, observe a textura ao lado dos zippers. O ruído da imagem é exibido porque os valores de limite eram muito baixos para suprimir o ruído. |
| **[!UICONTROL Monocromático]** | Selecione para ativar o brilho (intensidade) da imagem da máscara de nitidez.<br>Desmarque para desfazer a nitidez de cada componente de cor separadamente. |

Consulte também [Nitidez de imagens no Adobe Dynamic Media e no servidor de imagens](/help/assets/assets/sharpening_images.pdf).

### Guia PostScript {#postscript-tab}

Você pode rasterizar arquivos Adobe PostScript®, manter planos de fundo transparentes, escolher uma resolução e escolher um espaço de cores.

Você pode usar arquivos Adobe PostScript® (EPS) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao carregar arquivos de imagem PostScript (EPS), você pode formatá-los de várias maneiras. Você pode rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores.

| Opção PostScript | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter plano de fundo transparente em imagens renderizadas]** | Preserva a transparência em segundo plano do arquivo. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |

### Guia Photoshop {#photoshop-tab}

Você pode criar modelos a partir de arquivos Adobe® Photoshop®, manter camadas, especificar como as camadas são nomeadas, extrair texto e especificar como as imagens são ancoradas em modelos.

| Opção Photoshop | Descrição |
| --- | --- |
| **[!UICONTROL Manter camadas]** | Arrasta as camadas na PSD, se houver, para ativos individuais. As camadas de ativo permanecem associadas ao PSD. É possível visualizá-los abrindo o arquivo PSD na Exibição de detalhes e selecionando o painel de camada. Consulte Exibição e edição de camadas em um arquivo PSD. |
| **[!UICONTROL Criar modelo]** | Cria um modelo a partir das camadas no arquivo PSD. |
| **[!UICONTROL Extrair texto]** | Extrai o texto para que os usuários possam pesquisar por texto em um Visualizador. |
| **[!UICONTROL Estender camadas ao tamanho do plano de fundo]** | Estende o tamanho das camadas de imagem cortadas até o tamanho da camada de plano de fundo. |
| **[!UICONTROL Nomeação de camada]** | Estende o tamanho das camadas de imagem cortadas até o tamanho da camada de plano de fundo.<br>・ ・ **[!UICONTROL Nome da camada]** - Nomeia as imagens depois dos nomes das camadas no arquivo PSD. Por exemplo, uma camada chamada Tag de preço no arquivo PSD original se torna uma imagem chamada Tag de preço. No entanto, se os nomes de camada no arquivo PSD forem nomes de camada padrão do Photoshop (Plano de fundo, Camada 1, Camada 2 e assim por diante), as imagens serão nomeadas após seus números de camada no arquivo PSD. <br>・ ・ **[!UICONTROL Photoshop e número da camada]** - Nomes das imagens depois de seus números de camada no arquivo PSD, ignorando nomes de camada originais. As imagens são nomeadas com o nome do arquivo Photoshop e um número de camada anexado. Por exemplo, a segunda camada de um arquivo chamado `Spring Ad.psd` é nomeado `Spring Ad_2` mesmo que tivesse um nome não padrão no Photoshop.<br>・ ・ **[!UICONTROL Photoshop e nome da camada]** - Nomeia as imagens após o PSD, seguido do nome da camada ou do número da camada. O número da camada é usado se os nomes da camada no arquivo PSD forem nomes padrão da camada do Photoshop. Por exemplo, uma camada chamada `Price Tag` em um arquivo PSD `SpringAd` é nomeado `Spring Ad_Price Tag`. Uma camada com o nome padrão Camada 2 é chamada `Spring Ad_2`. |
| **[!UICONTROL Âncora]** | Especifique como as imagens são ancoradas em modelos que são gerados a partir da composição em camadas produzida a partir do arquivo PSD. Por padrão, a âncora é o centro. Uma âncora central permite que imagens de substituição preencham melhor o mesmo espaço, independentemente da proporção da imagem de substituição. Imagens com um aspecto diferente que substituem essa imagem, ao referenciar o modelo e usar substituição de parâmetro, ocupam efetivamente o mesmo espaço. Altere para uma configuração diferente se o aplicativo exigir as imagens de substituição para preencher o espaço alocado no modelo. |

### Guia PDF {#pdf-tab}

Você pode optar por rasterizar os arquivos, extrair palavras de pesquisa e links, definir a resolução e escolher um espaço de cores.

| opção PDF | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | ・ ・ **[!UICONTROL Nenhum]** - Não é efetuado qualquer processamento do PDF.<br>・ ・ **[!UICONTROL Miniatura]** - Remove cada página do arquivo PDF e a converte em uma imagem em miniatura.<br> ・ ・ **[!UICONTROL Rasterizar]** - Remove as páginas do arquivo PDF e converte gráficos vetoriais em imagens de bitmap. Para criar um eCatalog, escolha essa opção. |
| **[!UICONTROL Extrair]** | ・ ・ **[!UICONTROL Nenhum]** - Nenhuma palavra de pesquisa ou link é extraído do PDF.<br>・ ・ **[!UICONTROL Pesquisar palavras]** - Extrai palavras de pesquisa do arquivo PDF para que o arquivo possa ser pesquisado por palavra-chave em um visualizador de eCatalog.<br>・ ・ **[!UICONTROL Links]** - Extrai links dos arquivos do PDF e os converte em mapas de imagem usados em um visualizador de eCatalog.<br>・ ・ **[!UICONTROL Pesquisar palavras e links]** - Extrai palavras de pesquisa e links para uso em um visualizador de eCatalog. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Esta configuração determina quantos pixels são exibidos por polegada no arquivo PDF. O padrão é 150. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo PDF.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |

### Guia Illustrator {#illustrator-tab}

Você pode rasterizar arquivos Adobe Illustrator®, manter planos de fundo transparentes, escolher uma resolução e escolher um espaço de cores.

Você pode usar arquivos Adobe® Illustrator® (AI) no Adobe Dynamic Media. O Adobe Dynamic Media oferece comandos para configurar esses arquivos à medida que você os carrega.

Ao carregar arquivos de imagem do Illustrator (AI), você pode formatá-los de várias maneiras. Você pode rasterizar os arquivos, manter o plano de fundo transparente, escolher uma resolução e escolher um espaço de cores. As opções para formatar arquivos PostScript e Illustrator estão disponíveis na tela Upload em Opções de PostScript e Opções do Illustrator na caixa Opções de trabalho de upload .


| Opção Illustrator | Descrição |
| --- | --- |
| **[!UICONTROL Processando]** | Escolha Rasterizar para converter gráficos vetoriais no arquivo para o formato de bitmap. |
| **[!UICONTROL Manter plano de fundo transparente em imagens renderizadas]** | Preserva a transparência em segundo plano do arquivo. |
| **[!UICONTROL Resolução(pixel/polegada)]** | Determina a configuração de resolução. Essa configuração determina quantos pixels são exibidos por polegada no arquivo. |
| **[!UICONTROL Espaço de cores]** | ・ ・ **[!UICONTROL Detectar automaticamente]** - Mantém o espaço de cores do arquivo.<br>・ ・ **[!UICONTROL Forçar como RGB]** - Converte para o espaço de cores RGB.<br>・ ・ **[!UICONTROL Forçar como CMYK]** - Converte para o espaço de cores CMYK.<br>・ ・ **[!UICONTROL Forçar como Escala de Cinza]** - Converte para o espaço de cor Escala de Cinza. |
