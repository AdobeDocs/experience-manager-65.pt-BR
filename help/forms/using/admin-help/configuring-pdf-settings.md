---
title: Definição das configurações do Adobe PDF
seo-title: Definição das configurações do Adobe PDF
description: Saiba como definir configurações do Adobe PDF.
seo-description: Saiba como definir configurações do Adobe PDF.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
feature: Gerador de PDF
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '7278'
ht-degree: 0%

---


# Definir configurações do Adobe PDF{#configuring-adobe-pdf-settings}

A página Configurações do Adobe PDF mostra as configurações de conversão que você pode especificar para suas fontes usarem. Você pode usar qualquer uma das configurações predefinidas do PDF ou criar as suas próprias configurações. As configurações do PDF determinam precisamente como os arquivos são convertidos e sua estrutura e recursos do PDF resultante. As configurações do Adobe PDF eram anteriormente conhecidas como parâmetros Distiller® ou opções de trabalho.

Na página Configurações do Adobe PDF , é possível realizar as seguintes tarefas:

* Exibir as configurações predefinidas do PDF. (Consulte [Sobre as configurações predefinidas do PDF](configuring-pdf-settings.md#about-the-predefined-pdf-settings).)
* Crie uma configuração de PDF ou edite uma que você criou anteriormente. (Consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).)
* Especifique as configurações padrão do PDF. (Consulte [Alterar as configurações padrão](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings))
* Faça upload de um arquivo de configurações do PDF para o servidor. (Consulte [Fazer upload das configurações do PDF](configuring-pdf-settings.md#upload-pdf-settings).)
* Excluir configurações personalizadas do PDF. (Consulte [Excluir configurações do PDF](configuring-pdf-settings.md#delete-pdf-settings).)
* Faça upload e download de arquivos de log e de log. (Consulte [Upload e download de arquivos de log e epilog](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files).)

As configurações do Adobe PDF são aplicáveis somente às conversões baseadas no PDFMaker. Isso inclui as seguintes conversões:

* Documento do Microsoft Word (DOC, DOCX, RTF, TXT)
* Documento do Microsoft Excel (XLS, XLSX)
* Documento do Microsoft PowerPoint (PPT, PPTX)
* Documento do Microsoft Project (MPP)
* Documento do Microsoft Visio (VSD)

>[!NOTE]
>
>Ao usar o OpenOffice para converter os formatos acima, as configurações do Adobe PDF não são aplicadas.

## Sobre as configurações predefinidas do PDF {#about-the-predefined-pdf-settings}

O Gerador de PDF fornece várias configurações predefinidas de PDF para uso. Não é possível modificar essas configurações predefinidas; no entanto, é possível criar uma configuração com base em uma existente, editando a configuração e salvando-a com um novo nome.

**Impressão de alta qualidade:** cria arquivos PDF para saída de alta qualidade. Esta configuração:

* baixa amostras de imagens coloridas e em tons de cinza em 300 dpi
* baixa amostras de imagens monocromáticas em 1200 dpi
* imprime em uma resolução de imagem mais alta
* O usa outras configurações para preservar a quantidade máxima de informações sobre o documento original.

Esses arquivos PDF podem ser abertos no Adobe Acrobat 5 e no Adobe Acrobat Reader® 5 ou posterior.

**Páginas de grande porte:** Cria documentos PDF adequados para exibição e impressão confiáveis de desenhos de engenharia que são maiores que 200 x 200 polegadas. Os documentos PDF criados podem ser abertos no Adobe Acrobat Professional e Acrobat Standard, versão 7 ou posterior, e Adobe Reader 7 ou posterior.

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** verifica os trabalhos recebidos quanto à conformidade com o padrão ISO para preservação a longo prazo (arquivamento) de documentos eletrônicos e cria arquivos PDF/A somente se estiverem em conformidade. Esses arquivos são usados principalmente para arquivamento. Arquivos compatíveis podem conter somente texto, imagens rasterizadas e objetos vetoriais; eles não podem conter criptografia e scripts. Além disso, todas as fontes devem ser incorporadas para que os documentos possam ser abertos e visualizados conforme criados. O PDF/A-1b usa o PDF 1.4 e converte todas as cores em CMYK ou RGB, dependendo do padrão escolhido. Os arquivos PDF criados com esse arquivo de configurações podem ser abertos no Acrobat 5 e Acrobat Reader 5 e posterior. Para obter mais informações sobre PDF/A, consulte Adobe e padrões do setor.

**PDF/X-1a 2001:** verifica as tarefas recebidas para fins de conformidade com PDF/X-1a e cria arquivos PDF somente se compatível. PDF/X-1a é um padrão ISO para troca de conteúdo gráfico. O PDF/X-1a requer que todas as fontes sejam incorporadas, as caixas PDF apropriadas sejam especificadas e a cor seja exibida como CMYK ou cores spot. Os arquivos PDF que atendem aos requisitos de PDF/X-1a são direcionados a uma condição de saída específica, como impressão em offset da Web de acordo com as Especificações Publicações de deslocamento da Web. Para obter mais informações sobre PDF/X, consulte Adobe e padrões do setor.

**PDF/X-3 2002:** verifica as tarefas de entrada quanto à conformidade com PDF/X-3 e cria arquivos PDF somente se compatível. Como PDF/X-1a, PDF/X-3 é um padrão ISO para troca de conteúdo gráfico. A principal diferença é que o PDF/X-3 suporta cores independentes de dispositivo.

**Qualidade de impressão:** cria arquivos PDF para produção de impressão de alta qualidade (por exemplo, em uma conta de imagem ou plaqueta). Nesse caso, o tamanho do arquivo não é uma consideração. O objetivo é manter todas as informações em um arquivo PDF que uma impressora comercial ou um provedor de serviços de pré-impressão precisa imprimir o documento corretamente. Esse conjunto de opções:

* baixa amostras de imagens coloridas e em tons de cinza em 300 dpi
* baixa amostras de imagens monocromáticas em 1200 dpi
* incorpora subconjuntos de todas as fontes usadas no documento
* imprime em uma resolução de imagem mais alta,
* não gira automaticamente páginas com base na orientação dos comentários do texto ou das convenções de estruturação de documentos (DSC)
* O usa outras configurações para preservar a quantidade máxima de informações sobre o documento original.

Os trabalhos de impressão falharão se tiverem fontes que não podem ser incorporadas. Esses arquivos PDF podem ser abertos no Acrobat 5 e Acrobat Reader 5 e posterior.

>[!NOTE]
>
>Antes de criar um arquivo PDF para enviar a uma impressora comercial ou a um provedor de serviço de pré-impressão, determine a resolução de saída e outras configurações ou solicite um arquivo .joboptions com as configurações recomendadas. Talvez seja necessário personalizar as configurações do Adobe PDF para um provedor específico e fornecer um arquivo .joboptions próprio.

**Menor tamanho de arquivo:** Cria arquivos PDF para exibição na Web ou em uma intranet, ou para distribuição por meio de um sistema de email para exibição na tela. Esse conjunto de opções usa compactação, redução da amostragem e uma resolução de imagem relativamente baixa. Ele converte todas as cores em sRGB e não incorpora fontes, a menos que necessário. Também otimiza arquivos para o serviço de bytes. Esses arquivos PDF podem ser abertos no Acrobat 5 e Acrobat Reader 5.0 e posterior.

**Padrão:** Cria arquivos PDF para imprimir em impressoras de desktop ou copiadoras digitais, publicar em um CD ou enviar para um cliente como prova de publicação. Esse conjunto de opções usa compactação e redução da amostragem para reduzir o tamanho do arquivo. Ele também incorpora subconjuntos de todas as fontes usadas no arquivo, converte todas as cores em sRGB e imprime em uma resolução média para criar uma representação razoavelmente precisa do documento original. Observe que os subconjuntos de fontes do Microsoft Windows não são incorporados por padrão. Esses arquivos PDF podem ser abertos no Acrobat 5 e Acrobat Reader 5.0 e posterior.

## Adicionar ou editar configurações de PDF {#add-or-edit-pdf-settings}

As configurações do PDF determinam precisamente como os arquivos são convertidos e sua estrutura e recursos do PDF resultante. Defina uma nova configuração de PDF ou edite uma que tenha criado anteriormente. Não é possível modificar configurações predefinidas, mas é possível criar uma configuração com base em uma existente, editando a configuração e salvando-a com um novo nome.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em Novo ou clique no nome de uma configuração existente.
1. Na página Nova/editar configuração do Adobe PDF , preencha as informações necessárias nestas seções:

   [Opções gerais](configuring-pdf-settings.md#general-options)

   [Opções de imagens](configuring-pdf-settings.md#images-options)

   [Opções de fontes](configuring-pdf-settings.md#fonts-options)

   [Opções de cor](configuring-pdf-settings.md#color-options)

   [Opções avançadas](configuring-pdf-settings.md#advanced-options)

   [Opções de emissão de relatórios e conformidade de padrões](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

   [Opções de exibição inicial](configuring-pdf-settings.md#initial-view-options)

   Para acessar outra seção, clique no link na página da Web ou use os botões Next e Previous .

1. Após concluir as informações em todas as seções, clique em Salvar ou Salvar como e forneça um nome para a configuração.

## Fazer upload de configurações de PDF {#upload-pdf-settings}

Você pode ter as configurações de PDF disponíveis no servidor Gerador de PDF, fazendo o upload delas de um computador local ou de um local de rede.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF e clique em Fazer upload.
1. Na página Fazer upload da configuração do Adobe PDF , clique em Procurar, localize o arquivo de configurações do PDF e clique em Abrir.
1. Clique em OK e em OK novamente.

## Excluir configurações do PDF {#delete-pdf-settings}

É possível excluir permanentemente as configurações do PDF se elas não forem mais necessárias.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. Você pode selecionar várias configurações.
1. Clique em Excluir e, na página Confirmação de exclusão, clique em Excluir novamente.

## Opções gerais {#general-options}

Use as opções gerais para especificar a versão do Acrobat a ser usada para compatibilidade de arquivos e outras opções de arquivo e dispositivo. Para obter instruções sobre como acessar as opções Gerais, consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Opções de arquivo {#file-options}

**Compatibilidade:** o nível de compatibilidade do arquivo PDF. Para documentos que serão amplamente distribuídos, considere selecionar Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4) para garantir que todos os usuários possam visualizar e imprimir o documento. Se você criar arquivos usando a compatibilidade do Acrobat 5 ou posterior, eles poderão não ser compatíveis com versões anteriores do Acrobat. As subseções a seguir mostram algumas das diferenças entre os arquivos PDF que são criados usando diferentes níveis de compatibilidade com o Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat 5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) e Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Pode ser aberto com o Acrobat 3.0 e Acrobat Reader 3.0 e posterior.</p> </td>
   <td><p>Pode ser aberto com o Acrobat 3.0 e Acrobat Reader 3.0 e posterior. Os recursos específicos das versões posteriores podem ser perdidos ou não podem ser visualizados.</p> </td>
   <td><p>A maioria pode ser aberta com o Acrobat 4 e Acrobat Reader 4.0 e posterior. Os recursos específicos das versões posteriores podem ser perdidos ou não podem ser visualizados.</p> </td>
   <td><p>A maioria pode ser aberta com o Acrobat 4 e Acrobat Reader 4.0 e posterior. Os recursos específicos das versões posteriores podem ser perdidos ou não podem ser visualizados.</p> </td>
  </tr>
  <tr>
   <td><p>Não pode conter arte-final que use efeitos de transparência ativa. Qualquer transparência deve ser nivelada antes da conversão para PDF 1.3.</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller nivela a transparência.)</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller nivela a transparência.)</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller nivela a transparência.)</p> </td>
  </tr>
  <tr>
   <td><p>Camadas não são compatíveis.</p> </td>
   <td><p>Camadas não são compatíveis.</p> </td>
   <td><p>Preserva camadas ao criar arquivos PDF a partir de aplicativos que suportam a geração de documentos PDF em camadas, como Adobe Illustrator® CS ou Adobe InDesign® CS e posterior.</p> </td>
   <td><p>Preserva camadas ao criar arquivos PDF a partir de aplicativos que oferecem suporte à geração de documentos PDF em camadas, como Illustrator CS ou InDesign CS e posterior.</p> </td>
  </tr>
  <tr>
   <td><p>O espaço de cores DeviceN com 8 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com 8 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com até 31 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com até 31 corantes é suportado.</p> </td>
  </tr>
  <tr>
   <td><p>Fontes multibyte podem ser incorporadas. (O Distiller converte as fontes ao incorporar.)</p> </td>
   <td><p>Fontes multibyte podem ser incorporadas.</p> </td>
   <td><p>Fontes multibyte podem ser incorporadas.</p> </td>
   <td><p>Fontes multibyte podem ser incorporadas.</p> </td>
  </tr>
  <tr>
   <td><p>A segurança RC4 de 40 bits é suportada.</p> </td>
   <td><p>A segurança RC4 de 128 bits é suportada.</p> </td>
   <td><p>A segurança RC4 de 128 bits é suportada.</p> </td>
   <td><p>Segurança RC4 de 128 bits e AES de 128 bits (Advanced Encryption Standard) suportada.</p> </td>
  </tr>
 </tbody>
</table>

**Compactação no nível do objeto:** consolida pequenos objetos (cada um dos quais não é compactável) em fluxos que podem ser compactados com eficiência.

**Desativado:** não compacta nenhuma informação estrutural no documento PDF. Selecione essa opção se desejar que os usuários visualizem, naveguem e interajam com marcadores e outras informações estruturais usando o Acrobat 5 e posterior.

**Somente tags:** compacta as informações estruturais no documento PDF. Usar essa opção resulta em um arquivo PDF que pode ser aberto e impresso usando o Acrobat 5. Os usuários não podem visualizar informações de acessibilidade, estrutura ou PDF marcado no Acrobat 5 ou Acrobat Reader 5.0, mas podem exibir essas informações no Acrobat 6 e no Adobe Reader 6.0.

**Girar páginas automaticamente:** define a rotação automática das páginas com base na orientação do texto ou dos comentários do DSC. Por exemplo, algumas páginas (como páginas que contêm tabelas) podem exigir que o usuário as vire de lado para lê-las. Selecione Individualmente para girar cada página com base na direção do texto nessa página. Selecione Coletivamente por arquivo para girar todas as páginas no documento com base na orientação da maioria dos textos.

>[!NOTE]
>
>Se Processar comentários do DSC estiver selecionado nas configurações avançadas e se %%Exibir orientação os comentários forem incluídos, esses comentários terão precedência em determinar a orientação da página.

**Vínculo:** Especifica se deve ser exibido um arquivo PDF com vínculo esquerdo ou direito. Essa configuração afeta a exibição de páginas na Página Facing - layout contínuo e a exibição de miniaturas lado a lado.

**Solução:** define a emulação para a resolução de uma impressora para arquivos de entrada que ajustam seu comportamento de acordo com a resolução da impressora para a qual estão sendo impressas. Para a maioria dos arquivos de entrada, uma configuração de resolução mais alta resulta em arquivos PDF maiores, mas de qualidade mais alta, e uma configuração mais baixa resulta em arquivos PDF menores, mas de qualidade mais baixa. Mais comumente, a resolução determina o número de etapas em um gradiente ou mesclagem. Você pode inserir um valor de 72 a 4000. Mantenha essa configuração como padrão, a menos que planeje imprimir o arquivo PDF em uma impressora específica e deseje emular a resolução definida no arquivo de entrada original.

>[!NOTE]
>
>Aumentar a configuração de resolução aumenta o tamanho do arquivo e pode aumentar um pouco o tempo necessário para processar alguns arquivos.

**Todas as páginas ou Páginas de:** Especifica quais páginas devem ser convertidas. Deixe a caixa Para vazia para criar um intervalo a partir do número da página inserido na caixa De até o final do arquivo.

**Otimizar para rápida visualização da Web:** Reestrutura o arquivo para download de página por vez (serviço de bytes) de servidores da Web. Essa opção compacta texto e arte da linha, independentemente do que você selecionou como configurações de compactação na guia Imagens. A compactação resulta em acesso e visualização mais rápidos ao baixar o arquivo da Web ou de uma rede. Por padrão, essa opção não está ativada.

### Tamanho de página padrão {#default-page-size}

As opções de Tamanho de página padrão especificam o tamanho de página a ser usado quando um não estiver especificado no arquivo original. Normalmente, os arquivos Adobe PostScript incluem essas informações, exceto os arquivos EPS (Encapsulated PostScript), que fornecem um tamanho de caixa delimitadora, mas não de página. O tamanho máximo de página permitido é de 15.000.000 polegadas (31.800.000 cm) em qualquer direção. Essas opções configuram o tamanho padrão da página:

**Largura:** largura da página

**Altura:** Altura da página

**Unidades:** Unidades a serem usadas nas configurações de largura e altura

## Opções de imagens {#images-options}

As opções Imagens especificam a compactação e a reamostragem das imagens. Você pode experimentar essas opções para encontrar um equilíbrio apropriado entre o tamanho do arquivo e a qualidade da imagem. Para obter instruções sobre como acessar as configurações de Imagens, consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Essas opções configuram cores, tons de cinza e imagens monocromáticas:

**Reduzir amostra:** Defina um valor para cada tipo de imagem. Para reduzir a amostra de cores, imagens em tons de cinza ou monocromáticas, o Gerador de PDF combina pixels em uma área de amostra para tornar um pixel maior. Forneça a resolução do seu dispositivo de saída em pontos por polegada (dpi) e insira uma resolução em dpi na caixa Para imagens acima. Para imagens com uma resolução acima desse limite, o Gerador de PDF combina pixels, conforme necessário, para reduzir a resolução da imagem (pixels por polegada) à configuração de dpi especificada. Para desativar a redução da amostragem, selecione Desativado. Estas são as opções:

**Redução média de amostragem para:** calcula a média dos pixels em uma área de amostra e substitui toda a área pela cor média de pixel na resolução especificada.

**Redução da amostragem bíbica para:** usa uma média ponderada para determinar a cor de pixels e geralmente produz melhores resultados que o método de média simples de redução da amostragem. O bicicleta é o método mais lento, mas preciso, e resulta em gradações tonais mais suaves.

**Subamostragem para:** Seleciona um pixel no centro da área de amostra e substitui a área inteira por esse pixel na resolução especificada. A subamostragem reduz significativamente o tempo de conversão em comparação à diminuição da amostragem, mas resulta em imagens menos suaves e contínuas.

A configuração de resolução para cor e escala de cinza deve ser de 1,5 a 2 vezes a regra da tela de linha na qual o arquivo será impresso. (Desde que não fique abaixo dessa configuração de resolução recomendada, imagens que não contêm linhas retas ou padrões geométricos ou repetitivos não serão afetadas por uma resolução mais baixa.) A resolução para imagens monocromáticas deve ser a mesma do dispositivo de saída. No entanto, lembre-se de que salvar uma imagem monocromática em uma resolução superior a 1500 dpi aumenta o tamanho do arquivo sem melhorar visivelmente a qualidade da imagem.

Além disso, considere se os usuários precisam aumentar uma página. Por exemplo, se você estiver criando um documento PDF de um mapa, considere usar uma resolução de imagem mais alta para que os usuários possam ampliar o mapa.

>[!NOTE]
>
>A reamostragem de imagens monocromáticas pode ter resultados de exibição inesperados, como sem exibição de imagem. Se esse problema ocorrer, desative a reamostragem e converta o arquivo novamente. Este problema é mais provável de ocorrer com a subamostragem e é menos provável que ocorra com a desamostragem bicúbica.

Esta tabela mostra os tipos de impressoras e sua resolução medida em dpi, sua resolução de tela padrão medida em linhas por polegada (lpi) e uma resolução de reamostragem para imagens medidas em pixels por polegada (ppi). Por exemplo, para imprimir em uma impressora a laser de 600 dpi, digite 170 para que a resolução redefina as imagens em.

<table>
 <tbody>
  <tr>
   <th><p>Resolução da impressora</p> </th>
   <th><p>Tela de linha padrão</p> </th>
   <th><p>Resolução da imagem</p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (impressora a laser)</p> </td>
   <td><p>60 lpi</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (impressora a laser)</p> </td>
   <td><p>85 lpi</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 dpi (imagesetter)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi (imagesetter)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

**Compactação:** defina um valor a ser aplicado a imagens coloridas, em tons de cinza e monocromáticas. Para imagens coloridas e em tons de cinza, também defina a qualidade da imagem:

* Para imagens coloridas ou em tons de cinza, selecione ZIP para aplicar a compactação que funcione bem em imagens que tenham grandes áreas de cores únicas ou padrões repetitivos. Exemplos são capturas de tela, imagens simples criadas com programas de tinta e imagens monocromáticas que contêm padrões repetitivos. Selecione JPEG, de qualidade mínima a máxima, para aplicar compactação adequada para imagens em tons de cinza ou coloridas, como fotografias em tons contínuos que contêm mais detalhes do que pode ser reproduzido na tela ou na impressão. Selecione Automático (JPEG) para determinar automaticamente a melhor qualidade para imagens coloridas e em tons de cinza.
* Para imagens monocromáticas, selecione CCITT Group 4, CCITT Group 3, ZIP, JPEG200, Automatic (JPEG2000) ou Run Length compression.

Certifique-se de que as imagens monocromáticas sejam digitalizadas como monocromáticas e não como tons de cinza. O texto digitalizado às vezes é salvo como imagens em tons de cinza por padrão. O texto em tons de cinza compactado com o método de compactação JPEG não está claro e pode estar ilegível.

**Qualidade da imagem:** define a qualidade da imagem para imagens coloridas e em tons de cinza. As opções são mínimo, baixo, médio, alto e máximo.

**Suavização de borda para cinza:**  suaviza bordas irregulares em imagens monocromáticas. Selecione 2 bits, 4 bits ou 8 bits para especificar os níveis de cinza 4, 16 ou 256. (A suavização de serrilhado pode desfocar linhas pequenas ou finas.)

>[!NOTE]
>
>A compactação de texto e arte de linha está sempre ativa.

**Política de imagem:** defina uma política para imagens coloridas, em tons de cinza e monocromáticas. Se a resolução da imagem cair abaixo da resolução especificada, você ainda poderá selecionar para continuar (Ignorar), fornecer uma mensagem de aviso ou cancelar a tarefa.

## Opções de fontes {#fonts-options}

As opções de Fontes especificam quais fontes incorporar em um arquivo PDF e se devem incorporar um subconjunto de caracteres que são usados no arquivo PDF. Para obter instruções sobre como acessar as opções de Fontes, consulte [Adicionar ou editar configurações de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

>[!NOTE]
>
>Ao combinar arquivos PDF com o mesmo subconjunto de fontes, o Gerador de PDF tenta combinar os subconjuntos de fontes.

**Incorporar todas as fontes:** Incorpora todas as fontes usadas no arquivo. A incorporação de fonte é necessária para conformidade com PDF/X.

**Subconjunto de fontes incorporadas quando a porcentagem de caracteres usados for menor que:** Se você selecionar essa opção, especifique uma porcentagem limite para incorporar apenas um subconjunto de fontes. Por exemplo, se o limite for 35 e menos de 35% dos caracteres forem usados, o Gerador de PDF incorporará somente esses caracteres. Apenas fontes com bits de permissão apropriados são incorporadas.

**Quando a incorporação falhar:** Especifica como o Gerador de PDF responde se não conseguir encontrar uma fonte a ser incorporada ao processar um arquivo. O Gerador de PDF pode ignorar a solicitação e substituir a fonte, avisá-lo e substituir a fonte ou cancelar o processamento da tarefa atual.

**Fonte:** O local das fontes que o Gerador de PDF usa.

### Especificar quais fontes incorporar {#specify-which-fonts-to-embed}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em New ou clique no nome de uma configuração.
1. Clique em Fontes e desmarque Incorporar todas as fontes.
1. Na lista Fonte, selecione uma fonte e clique em Ir para atualizar a lista de fontes na caixa à esquerda.
1. Clique em uma fonte na caixa à esquerda. Em seguida, clique em Adicionar ao lado da caixa apropriada para movê-la para a lista Sempre incorporado ou Nunca incorporado . Repita para cada fonte. Clique com a tecla Ctrl pressionada para selecionar várias fontes a serem movidas.
1. Para remover uma fonte da lista Sempre incorporar ou Nunca incorporar, selecione-a e clique em Remover ao lado da caixa apropriada. Essa ação não remove a fonte do sistema; ela simplesmente remove a referência a ela na lista.
1. Se a fonte que você deseja especificar não for exibida, digite o nome na caixa Adicionar fonte e clique em Sempre incorporar ou Nunca incorporar. Os nomes de fonte não podem conter caracteres alfanuméricos.

>[!NOTE]
>
>Uma fonte TrueType pode conter uma configuração adicionada pelo designer de fonte que impede a fonte de ser incorporada a arquivos PDF.

>[!NOTE]
>
>As fontes são selecionadas do cache de fontes do sistema Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do cliente, reinicie o sistema no qual AEM formulários está instalado.

## Opções de cor {#color-options}

As opções de Cor definem todas as informações de gerenciamento de cores para o Gerador de PDF. Para obter instruções sobre como acessar as opções de Cor, consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

### Configurações do Adobe Color {#adobe-color-settings}

**Arquivo de configurações:** esta lista contém uma lista de configurações de cores que também são usadas em aplicativos gráficos principais, como Adobe Photoshop e Adobe Illustrator. A configuração de cor selecionada determina as outras configurações de cor de Adobe nesta página. Por exemplo, se você selecionar uma configuração diferente de Nenhum, todas as opções além daquelas para Dados dependentes de dispositivo serão predefinidas e apagadas. Você pode editar as configurações de Políticas de gerenciamento de cores e Espaços de trabalho somente se selecionar Nenhum para o Arquivo de configurações.

### Políticas de gerenciamento de cores {#color-management-policies}

Se você selecionou Nenhum para o Arquivo de configurações, a área Políticas de gerenciamento de cores especifica como o Gerador de PDF converte cores não gerenciadas em um arquivo PostScript.

**Deixe a cor inalterada:** Deixa as cores dependentes do dispositivo inalteradas e preserva as cores independentes do dispositivo como o equivalente mais próximo possível em PDF. Essa opção é útil para imprimir lojas que calibraram todos os seus dispositivos, usaram essas informações para especificar a cor no arquivo e produziram apenas esses dispositivos.

**Marcar tudo para o gerenciamento de cores:** incorpora um perfil do International Color Consortium ao destilar arquivos e calibrar cores nas imagens, o que torna as cores dos arquivos PDF resultantes independentes do dispositivo se você selecionou Acrobat 4 (PDF 1.3) ou compatibilidade posterior. No entanto, os espaços de cores dependentes de dispositivo nos arquivos (RGB, Escala de cinza e CMYK) são convertidos em espaços de cores independentes de dispositivo (CalRGB, CalGray e LAB).

**Imagens somente tag para gerenciamento de cores:** incorpora perfis ICC apenas em imagens, não em texto ou gráficos, ao destilarar arquivos se você selecionou compatibilidade com o Acrobat 4 (PDF 1.3). Essa opção impede que o texto preto seja submetido a qualquer mudança de cor. No entanto, os espaços de cores dependentes de dispositivo em imagens (RGB, Escala de cinza e CMYK) são convertidos em espaços de cores independentes de dispositivo (CalRGB, CalGray e LAB). Texto e gráficos não são convertidos.

**Converter todas as cores em sRGB ou Converter todas as cores em CMYK:** calibra a cor do arquivo, tornando a cor independente do dispositivo, de modo semelhante a Tag Tudo para o gerenciamento de cores. Se você selecionou Acrobat 4 (PDF 1.3) ou compatibilidade posterior e converteu em sRGB, as imagens CMYK e RGB são convertidas em sRGB.

Independentemente da opção de compatibilidade selecionada, as imagens em tons de cinza permanecem inalteradas. Isso geralmente reduz o tamanho e aumenta a velocidade de exibição de arquivos PDF, pois são necessárias menos informações para descrever imagens RGB do que para descrever imagens CMYK. Como RGB é o espaço de cores nativo usado em monitores, nenhuma conversão de cores é necessária durante a exibição, o que contribui para uma exibição online rápida. Essa opção é recomendada se o arquivo PDF for usado online ou com impressoras de baixa resolução.

**Propósito de renderização do documento:** o método para mapear cores entre espaços de cores. O resultado de qualquer método específico depende dos perfis dos espaços de cores. Por exemplo, alguns perfis produzem resultados idênticos com métodos diferentes. Estas opções estão disponíveis:

>[!NOTE]
>
>Em todos os casos, as intenções podem ser ignoradas ou substituídas por operações de gerenciamento de cores que ocorrem após a criação do arquivo PDF.

**Preservar:** significa que a intenção é especificada no dispositivo de saída em vez de no arquivo PDF. Em muitos dispositivos de saída, a Colorimétrica relativa é a intenção padrão.

**Perceptual:** Mantém os valores de cor relativos entre os pixels originais conforme são mapeados para a gama de destino. Este método preserva a relação visual entre as cores, embora os próprios valores de cor possam mudar.

**Saturação:** mantém os valores relativos de saturação dos pixels originais. Esse método é adequado para gráficos comerciais, onde a relação exata entre cores não é tão importante quanto ter cores saturadas brilhantes.

**Colorimétrica relativa:** Mapeia novamente o ponto branco do espaço de origem para o ponto branco do espaço de destino.

**Colorimétrica absoluta:** desativa a correspondência de pontos brancos e negros ao converter cores. Esse método não é recomendado a menos que você tenha que preservar as cores da assinatura, como as usadas em marcas comerciais ou logotipos.

### Espaços de trabalho {#working-spaces}

Para todos os valores na lista em Políticas de gerenciamento de cores, exceto Deixar cor inalterada, selecione nas listas na área Espaço de trabalho para especificar quais perfis ICC são usados para definir e calibrar os espaços de cores em tons de cinza, RGB e CMYK em arquivos PDF destilados. Estas opções estão disponíveis:

**Cinza:** Define o espaço de cores de todas as imagens em tons de cinza em arquivos. Essa opção só estará disponível se você escolher Tag Tudo para gerenciamento de cores ou Tag Only Images para gerenciamento de cores. O perfil ICC padrão para imagens cinza é Gama cinza 2.2. Você também pode selecionar Nenhum para impedir que imagens em tons de cinza sejam convertidas.

**RGB:** Define o espaço de cores de todas as imagens RGB em arquivos. O padrão, sRGB IEC61966-2.1, é geralmente uma boa escolha porque está se tornando um padrão industrial e muitos dispositivos de saída o reconhecem. Você também pode selecionar Nenhum para impedir que imagens RGB sejam convertidas.

**CMYK:** Define o espaço de cores de todas as imagens CMYK em arquivos. O padrão é US Web Coated (SWOP) v2. Você também pode selecionar Nenhum para impedir que imagens CMYK sejam convertidas.

>[!NOTE]
>
>Selecionar Nenhum para todos os três espaços de trabalho tem o mesmo efeito que selecionar Deixar cor inalterada.

**Preservar valores CMYK para espaços de cores CMYK calibrados:** quando selecionados, valores CMYK independentes de dispositivo são tratados como valores dependentes de dispositivo (DeviceCMYK), espaços de cores independentes de dispositivo são descartados e arquivos PDF/X-1a usam o valor Converter todas as cores em CMYK. Quando desmarcada, espaços de cores independentes de dispositivo são convertidos em CMYK se a política de gerenciamento de cores estiver definida como Converter todas as cores em CMYK.

### Dados Dependentes do Dispositivo {#device-dependent-data}

Essas opções se aplicam se você trabalhar com documentos criados com documentação sofisticada e aplicativos gráficos, como Adobe Illustrator e Adobe InDesign. Para obter mais informações, consulte a documentação fornecida com o aplicativo.

As funções de transferência são utilizadas para efeitos artísticos e ajustam - se às especificações de um dispositivo de saída específico. Por exemplo, um arquivo destinado à saída em uma imagem específica pode conter funções de transferência que compensam o ganho de ponto inerente a essa impressora.

**Preservar em Remoção de cor e Geração de preto:** Mantém essas configurações, se existirem no arquivo PostScript. A geração de preto calcula a quantidade de preto a ser usada quando você está tentando reproduzir uma cor específica. A remoção de subcores (UCR) reduz a quantidade de componentes ciano, magenta e amarelo para compensar a quantidade de preto que a geração de preto adicionou. Por utilizar menos tinta, o UCR é geralmente utilizado para papel de jornal e material não revestido.

**Quando as funções de transferência são encontradas:** determina o que fazer quando as funções de transferência são encontradas:

**Preservar:** Retém as funções de transferência tradicionalmente usadas para compensar ganhos de pontos ou perdas de pontos que podem ocorrer quando uma imagem é transferida para um filme. O ganho de pontos ocorre quando os pontos de tinta que compõem uma imagem impressa são maiores (por exemplo, devido à propagação no papel) do que na tela de meio-tom; a perda de ponto ocorre quando os pontos são impressos menores. Com essa opção, as funções de transferência são mantidas como parte do arquivo e são aplicadas ao arquivo quando o arquivo é gerado.

**Aplicar:** Não mantém a função de transferência, mas a aplica ao arquivo, o que altera as cores no arquivo. Essa opção é útil para criar efeitos de cor em um arquivo. Por padrão, essa opção é selecionada para novas configurações.

**Remover:** remove qualquer função de transferência aplicada. Remova as funções de transferência aplicadas, a menos que o arquivo PDF seja enviado para o mesmo dispositivo para o qual o arquivo PostScript de origem foi criado.

**Preservar informações de meio-tom:** Mantém as informações de meio-tom nos arquivos. As informações de meio-tom consistem em pontos que controlam a quantidade de dispositivos de meio-tom de tinta depositados em um local específico no papel. Variar o tamanho e a densidade do ponto cria a ilusão de variações de cor cinza ou contínua. Para uma imagem CMYK, são usadas quatro telas de meio-tom, uma para cada tinta usada no processo de impressão.

Na produção tradicional da impressão, um meio-tom é produzido colocando uma tela de meio-tom entre um filme e a imagem e depois expondo o filme. Os equivalentes eletrônicos, como no Adobe Photoshop, permitem que os usuários especifiquem os atributos da tela de meio-tom antes de produzirem o filme ou a saída de papel. As informações de meio-tom são destinadas ao uso com um determinado dispositivo de saída.

## Opções avançadas {#advanced-options}

As opções Avançadas especificam quais DSC (Convenções de Estrutura de Documentos) comentários manter no arquivo PDF e como definir outras opções que afetam a conversão do PostScript. Em um arquivo PostScript, os comentários do DSC contêm informações sobre o arquivo (como o aplicativo de origem, a data de criação e a orientação da página). Eles também fornecem estrutura para descrições de página no arquivo (como instruções de início e término para uma seção de perfil). Os comentários do DSC podem ser úteis quando o documento for impresso ou pressionado. Para obter instruções sobre como acessar as opções Avançadas, consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Ao trabalhar com as opções Avançadas , é útil compreender a linguagem PostScript e como ela é traduzida para PDF. (Consulte [Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html).)

**Permitir que o arquivo PostScript substitua as configurações do Adobe PDF:** usa as configurações armazenadas em um arquivo PostScript, em vez do arquivo de configurações atual do Adobe PDF. Antes de processar um arquivo PostScript, você pode colocar parâmetros no arquivo para controlar os seguintes aspectos:

* compactação de texto e gráficos
* Redução da amostragem e codificação de imagens amostradas
* incorporação de fontes Tipo 1 e instâncias de Tipo 1 Fontes Principais múltiplas

**Permitir XObjects PostScript:** os XObjects PostScript armazenam informações exibidas em muitas páginas do mesmo arquivo, como uma imagem de fundo ou informações de cabeçalho e rodapé. O uso de XObjects PostScript pode resultar em impressão mais rápida, mas requer mais memória de impressora. Para impedir a criação de XObjects PostScript, desmarque essa opção se você criar arquivos PDF com compatibilidade Acrobat 5 (PDF 1.4) ou posterior.

**Converter gradientes em sombras suaves:** converte as misturas em tons suaves para o Acrobat 4 e posterior, tornando os arquivos PDF menores e melhorando potencialmente a qualidade da saída final. O PDF Generator converte gradientes do Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress e Microsoft PowerPoint.

**Converter linhas suaves em curvas:** reduz a quantidade de pontos de controle usados para criar curvas em desenhos CAD, o que resulta em PDFs menores e renderização mais rápida na tela.

**Preservar a semântica de página de cópia de nível 2:** Usa o operador de página de cópia definido em LanguageLevel 2 PostScript em vez de em LanguageLevel 3 PostScript. Se você tiver um arquivo PostScript e selecionar essa opção, um operador de página copiada copiará a página. Se essa opção não estiver selecionada, o equivalente a uma operação de página de exibição será executado, mas o estado dos gráficos não será reinicializado.

**Preservar configurações de superimposição:** Mantém todas as configurações de superimposição em arquivos que estão sendo convertidos em PDF. As cores impressas são duas ou mais tintas impressas em cima umas das outras. Por exemplo, quando uma tinta ciana é impressa sobre uma tinta amarela, a impressão sobreposta resultante é uma cor verde. Sem a impressão em excesso, o amarelo subjacente não seria impresso, resultando numa cor ciana.

**O padrão de superimposição é diferente de zero superimposição:** impede que objetos superimpressos com valores de CMYK zero destruam objetos CMYK que estão abaixo deles. Esse efeito é obtido inserindo o parâmetro de estado de gráficos OPM 1 no arquivo PDF, onde quer que o operador de impressão em conjunto esteja presente.

**Salvar configurações do Adobe PDF dentro do arquivo PDF:** Incorpora o arquivo de configurações usado para criar o arquivo PDF. Você pode abrir e exibir o arquivo de configurações (que tem uma extensão de arquivo .joboptions ) na caixa de diálogo Anexos de arquivo no Acrobat. O arquivo de configurações do Adobe PDF se torna um item na árvore EmbeddedFiles dentro do arquivo PDF.

**Salvar imagens JPEG originais em PDF, se possível:** processa quaisquer imagens JPEG compactadas (imagens que já estão compactadas usando a codificação DCT) sem recompactá-las. Se essa opção estiver selecionada, o Gerador de PDF descompactará as imagens JPEG para garantir que elas não estejam corrompidas. No entanto, não recomprime imagens válidas, processando a imagem original intocada. Com essa opção selecionada, o desempenho melhora porque somente a descompactação (e não a recompactação) ocorre e os dados e metadados da imagem são preservados.

**Salvar tíquete de trabalho portátil dentro do arquivo PDF:** reserva um tíquete de trabalho PostScript em um arquivo PDF. O tíquete de trabalho contém informações sobre o arquivo PostScript, como tamanho da página, resolução e informações de trapping, em vez de informações sobre conteúdo. Essas informações podem ser usadas posteriormente em um fluxo de trabalho ou para impressão do PDF.

**Use Prolog.ps e Epilog.ps:** Envia um arquivo de log e epilog com cada trabalho. Esses arquivos têm muitos objetivos. Por exemplo, os arquivos de perfil podem ser editados para especificar folhas de rosto. Arquivos de log podem ser editados para resolver uma série de procedimentos em um arquivo PostScript. Você pode fazer upload ou download dos arquivos. (Consulte Upload e download de arquivos de log e epilog.)

**Processar comentários do DSC:** mantém informações do DSC de um arquivo PostScript. Essas subopções estão disponíveis:

**Registrar avisos do DSC:** exibe mensagens de aviso sobre comentários do DSC problemáticos durante o processamento e as adiciona a um arquivo de log.

**Preservar informações de EPS do DSC:** mantém informações, como o aplicativo de origem e a data de criação de um arquivo EPS. Se essa opção estiver desmarcada, a página será dimensionada e centralizada com base no canto superior esquerdo do objeto superior esquerdo e no canto inferior direito do objeto inferior direito na página.

**Preservar comentários de OPI:** Retém as informações necessárias para substituir uma imagem ou comentário para posicionamento Somente para posicionamento (FPO) pela imagem de alta resolução localizada em servidores que oferecem suporte para OPI (Open Prepress Interface) versões 1.3 e 2.0.

**Preservar informações do documento do DSC:** mantém informações como título, data de criação e hora. Quando você abre um arquivo PDF no Acrobat, essas informações são exibidas no painel Descrição das propriedades do documento .

**Redimensionar página e Centralizar arte-final para arquivos EPS:** centraliza uma imagem EPS e redimensiona a página para ajustá-la de perto à imagem. Essa opção se aplica somente a tarefas que consistem em um único arquivo EPS.

## Opções de emissão de relatórios e conformidade de padrões {#standards-reporting-and-compliance-options}

O PDF Generator pode verificar o conteúdo do documento em um arquivo PostScript para garantir que ele atenda aos critérios PDF/X-1a, PDF/X-3 ou PDF/A padrão antes de criar o arquivo PDF. Para arquivos compatíveis com PDF/X, você também pode exigir que o arquivo PostScript atenda a critérios adicionais selecionando outras opções em &quot;Relatório padrão e conformidade&quot;. A disponibilidade das opções depende do padrão selecionado.

Arquivos compatíveis com PDF/X são usados principalmente como um formato padronizado para a troca de arquivos PDF destinados à produção de impressão em alta resolução. A menos que esteja criando um documento PDF para produção de impressão, você pode ignorar os padrões de conformidade do PDF/X.

Arquivos compatíveis com PDF/A são usados principalmente para arquivamento. Como a preservação a longo prazo é o objetivo, o documento deve conter apenas o que é necessário para abrir e visualizar durante toda a vida pretendida do documento. Por exemplo, arquivos compatíveis com PDF/A podem conter apenas texto, imagens rasterizadas e objetos vetoriais; eles não podem conter criptografia e scripts. Além disso, todas as fontes devem ser incorporadas para que os documentos possam ser abertos e visualizados conforme criados. Em outras palavras, os documentos compatíveis com PDF/A são *mais finos* do que seus equivalentes PDF/X, que são destinados à produção high-end.

>[!NOTE]
>
>Se você configurar uma pasta monitorada para criar arquivos compatíveis com PDF/A, certifique-se de não adicionar segurança à pasta; o padrão PDF/A não permite criptografia.

Para obter instruções sobre como acessar as opções de emissão de relatórios e conformidade de Padrões, consulte [Adicionar ou editar configurações de PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

**Padrão de conformidade:** selecione um padrão para produzir um relatório que indique se o arquivo está em conformidade com os requisitos e, se não, quais problemas foram encontrados. Quando Compatibilidade na página Configurações gerais é definida como Acrobat 4.0, as seguintes opções são ativadas. Quando a opção Compatibilidade estiver definida como Acrobat 5.0, somente as opções do Acrobat 5.0 estarão disponíveis para seleção. Quando a opção Compatibilidade é definida como uma opção alternativa, as seguintes opções estão esmaecidas:

* PDF/X-1a (compatível com Acrobat 4.0)
* PDF/X-3 (compatível com Acrobat 4.0)
* PDF/X-1a (compatível com Acrobat 5.0)
* PDF/X-3 (compatível com Acrobat 5.0)
* PDF/A-1b (compatível com Acrobat 5.0)

### Opções para padrões PDF/X {#options-for-pdf-x-standards}

**Quando não é compatível:** especifica se o arquivo PDF deve ser criado se o arquivo PostScript não estiver em conformidade com os requisitos de PDF/X. Essa opção está disponível quando o Padrão de conformidade na página Relato de padrões e Conformidade está definido como uma opção diferente de Nenhum.

**Continuar:** cria um arquivo PDF.

**Cancelar trabalho:** cria um arquivo PDF somente se o arquivo PostScript atender aos requisitos de PDF/X das opções de relatório selecionadas e for válido. Se ambas as opções de relatório PDF/X forem selecionadas e o arquivo PostScript atender a apenas um conjunto de critérios PDF/X (por exemplo, PDF/X-3), o PDF Generator criará o arquivo compatível.

**Se TrimBox ou ArtBox não estiverem especificadas:** Disponíveis quando o Padrão de conformidade na página Relatório de padrões e Conformidade estiver definido como uma opção diferente de Nenhum.

**Relatório como erro:** Sinaliza o arquivo PostScript como incompatível se uma das opções de relatório for selecionada e uma caixa de apara ou caixa de arte estiver ausente de qualquer página.

**Definir TrimBox para MediaBox com deslocamentos:** calcula os valores em pontos para a caixa de apara com base nos deslocamentos da caixa de mídia das respectivas páginas se nem a caixa de apara nem a caixa de arte forem especificadas. A caixa de apara é sempre tão pequena ou menor que a caixa de mídia de inclusão.

**Se BleedBox não for especificado:** disponível quando o Padrão de conformidade na página Relatório de padrões e Conformidade estiver definido como uma opção diferente de Nenhum.

**Definir BleedBox como MediaBox:** usa os valores da caixa de mídia para a caixa de sangria se a caixa de sangria não for especificada.

**Definir BleedBox como TrimBox com deslocamentos:** calcula os valores em pontos para a caixa de sangria com base nos deslocamentos para a caixa de trim das respectivas páginas se a caixa de sangria não for especificada. A caixa de sangria é sempre tão grande ou maior que a caixa de acabamento fechada.

**Valores Padrão Se Não Especificado no Documento:** Essa opção está disponível quando o Padrão de Conformidade na página Relatório de Padrões e Conformidade está definido como uma opção diferente de Nenhum.

**Nome do perfil de intenção de saída:** indica a condição de impressão caracterizada para a qual o documento está preparado. Se um documento não especificar um nome de OutputIntent, o Gerador de PDF usará o valor selecionado nesse menu. Você pode selecionar um dos nomes fornecidos ou inserir um nome no espaço fornecido. Se o fluxo de trabalho exigir que o documento especifique a intenção de saída, selecione Nenhum. Qualquer documento que não atende ao requisito não é submetido à verificação de conformidade.

**Identificador de condição de saída:** indica o nome de referência especificado pelo registro do nome do perfil de intenção de saída.

**Condição de saída:** descreve a condição de impressão pretendida. Essa entrada pode ser útil para o destinatário pretendido do documento PDF.

**Nome do registro (URL):** indica o endereço da Web para obter mais informações sobre o registro. O URL é inserido automaticamente para nomes de registro ICC.

**Trapped:** Indica o estado do trapping no documento. A conformidade com PDF/X requer um valor True ou False. Se o documento não especificar o estado capturado, o valor fornecido aqui será usado. Se o fluxo de trabalho exigir que o documento especifique o estado capturado, selecione Deixar indefinido. Qualquer documento que não atende ao requisito não é submetido à verificação de conformidade.

### Opções para PDF/A padrão {#options-for-pdf-a-standard}

Essas opções são ativadas quando a Compatibilidade (na área Geral) é definida como Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4).

**Quando não é compatível:** especifica se o arquivo PDF deve ser criado se o arquivo PostScript não estiver em conformidade com os requisitos de PDF/A.

**Continuar:** cria um arquivo PDF mesmo que o arquivo PostScript não atenda aos requisitos do padrão.

**Cancelar trabalho:** cria um arquivo PDF somente se o arquivo PostScript atender aos requisitos do PDF/A e for válido.

**Nome do perfil de intenção de saída:** indica a condição de impressão caracterizada para a qual o documento foi preparado e é necessário para conformidade com PDF/A. Se o fluxo de trabalho exigir que o documento especifique as informações de Propósito de saída, selecione &quot;Nenhum&quot;. O documento falhará na verificação de conformidade se essas informações não forem fornecidas.

**Condição de saída:** descreve a condição de impressão pretendida. Essa entrada não é obrigatória, mas pode ser usada para fornecer informações úteis ao destinatário pretendido do documento PDF.

## Opções de visualização inicial {#initial-view-options}

Essas opções são organizadas em três áreas: Opções de Documento, Opções de Janela e Opções de Interface do Usuário. Para obter instruções sobre como acessar as opções de Visualização inicial, consulte [Adicionar ou editar configurações do PDF](configuring-pdf-settings.md#add-or-edit-pdf-settings).

Para usar qualquer opção, selecione Definir configurações da exibição inicial.

### Opções de documento {#document-options}

As opções de documento controlam a aparência do documento dentro da janela do documento, como o nível de ampliação e como ele rola.

**Mostrar:** Determina quais painéis e guias são exibidos na janela do aplicativo por padrão. Painel de marcadores e Página abre o painel do documento e exibe a guia Marcadores .

**Layout de página:** Determina se o documento é exibido no modo de página única, página faceada, página contínua ou página faceada contínua.

**Ampliação:** define o nível de zoom usado para exibir o documento quando ele é aberto. O padrão usa o valor de ampliação configurado pelo usuário nas preferências do Acrobat ou Adobe Reader.

**Abrir para número de página:** define a página que o documento abre, que geralmente é a página 1.

>[!NOTE]
>
>Definir padrão para as opções de ampliação e layout de página usa as configurações de usuário individuais nas preferências de Exibição de página no Acrobat ou Adobe Reader.

### Opções da janela {#window-options}

As opções da janela determinam como a janela se ajusta na área da tela quando um usuário abre o documento. No entanto, as opções não têm efeito quando um documento PDF é visualizado em um navegador da Web.

**Redimensionar janela para página inicial:** Ajusta a janela do documento para ajustá-la de forma simples ao redor da página de abertura, de acordo com as opções selecionadas em Opções de documento.

**Centralizar janela na tela:** posiciona a janela no centro da área da tela.

**Abrir no modo de tela cheia:** maximiza a janela do documento e exibe o documento sem a barra de menu, a barra de ferramentas ou os controles da janela.

**Mostrar:** O nome do arquivo mostra o nome do arquivo na barra de título da janela. O título do documento mostra o título do documento na barra de título da janela.

### Opções da interface do usuário {#user-interface-options}

As opções da interface do usuário determinam quais controles são exibidos ou ocultos quando o usuário abre o documento.

**Ocultar barra de menus:** se selecionada, oculta a barra de menus

**Ocultar barras de ferramentas:** se esta opção estiver selecionada, oculta as barras de ferramentas

**Ocultar controles de janela:** se selecionado, oculta os controles de janela

>[!NOTE]
>
>Se você ocultar a barra de menus e a barra de ferramentas, os usuários não poderão aplicar comandos e selecionar ferramentas, a menos que saibam os atalhos do teclado quando abrem o arquivo no Acrobat.

## Upload e download de arquivos de log e epilog {#uploading-and-downloading-prologue-and-epilogue-files}

Os arquivos de perfil são usados para adicionar código PostScript personalizado que é executado no início de cada trabalho PostScript que está sendo destilado. Os arquivos de log são usados para adicionar código PostScript personalizado que é executado no final de cada trabalho PostScript. Você pode baixar os arquivos de log e de log do servidor para salvá-los localmente. Talvez você queira baixar os arquivos para configurá-los independentemente ou carregá-los em outro local ou em outro computador.

Esses arquivos têm muitos objetivos. Por exemplo, os arquivos de perfil podem ser editados para especificar folhas de rosto; Arquivos de log podem ser editados para resolver uma série de procedimentos em um arquivo PostScript. Você também pode selecionar e carregar os arquivos de log e de log a serem enviados com cada tarefa.

### Baixar um arquivo de log ou epilog {#download-a-prologue-or-epilogue-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em New ou clique no nome de uma configuração.
1. Clique em Avançado e, ao lado da opção Usar Prolog.ps e Epilog.ps , clique em Download.
1. Na página Baixar perfis e arquivos de log, clique em Prolog.ps ou Epilog.ps e clique em Salvar.

### Fazer upload de um arquivo de log ou epilog {#upload-a-prologue-or-epilogue-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em New ou clique no nome de uma configuração.
1. Clique em Avançado e, ao lado da opção Usar Prolog.ps e Epilog.ps , clique em Fazer upload.
1. Na página Fazer upload de arquivos de log e de log, clique em Procurar para selecionar um prolog ou um arquivo de epílogo.
1. Localize o arquivo e clique em Abrir.
1. Para usar o arquivo, verifique se Usar Prolog.ps e Epilog.ps está selecionado na área Avançado da página Nova/Editar configuração do Adobe PDF .
1. Clique em Salvar

>[!NOTE]
>
>O PDF Generator oferece suporte a arquivos de log e epilog somente para conversão de arquivos PostScript e PostScript Encapsulado em PDF.

