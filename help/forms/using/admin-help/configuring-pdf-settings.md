---
title: Definição das configurações do Adobe PDF
seo-title: Definição das configurações do Adobe PDF
description: Saiba como configurar as configurações do Adobe PDF.
seo-description: Saiba como configurar as configurações do Adobe PDF.
uuid: 980c9d6a-f75e-4e7d-b050-d2d07a10ef33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: ab018b6d-0233-4439-bb75-58c5421d769a
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Definição das configurações do Adobe PDF{#configuring-adobe-pdf-settings}

A página Configurações do Adobe PDF mostra as configurações de conversão que você pode especificar para suas fontes usarem. Você pode usar qualquer uma das configurações predefinidas do PDF ou criar suas próprias configurações. As configurações do PDF determinam precisamente como os arquivos são convertidos e sua estrutura e recursos do PDF resultante. As configurações do Adobe PDF eram anteriormente conhecidas como parâmetros do Distiller® ou opções de trabalho.

Na página Configurações do Adobe PDF, você pode fazer as seguintes tarefas:

* Visualização das configurações predefinidas do PDF. (Consulte [Sobre as configurações](configuring-pdf-settings.md#about-the-predefined-pdf-settings)predefinidas do PDF.)
* Crie uma configuração de PDF ou edite uma que você tenha criado anteriormente. (Consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.)
* Especifique as configurações padrão de PDF. (Consulte [Alterar as configurações](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)padrão)
* Carregue um arquivo de configurações de PDF no servidor. (Consulte [Carregar configurações](configuring-pdf-settings.md#upload-pdf-settings)de PDF.)
* Exclua configurações personalizadas de PDF. (Consulte [Excluir configurações](configuring-pdf-settings.md#delete-pdf-settings)de PDF.)
* Carregue e baixe arquivos de prólogo e epílogo. (Consulte [Fazer upload e download de arquivos](configuring-pdf-settings.md#uploading-and-downloading-prologue-and-epilogue-files)de prólogo e de epílogo.)

As configurações do Adobe PDF são aplicáveis somente às conversões baseadas no PDFMaker. Elas incluem as seguintes conversões:

* documento do Microsoft Word (DOC, DOCX, RTF, TXT)
* documento do Microsoft Excel (XLS, XLSX)
* documento do Microsoft PowerPoint (PPT, PPTX)
* documento do Microsoft Project (MPP)
* documento do Microsoft Visio (VSD)

>[!NOTE]
>
>Ao usar o OpenOffice para converter os formatos acima, as configurações do Adobe PDF não são aplicadas.

## Sobre as configurações predefinidas do PDF {#about-the-predefined-pdf-settings}

O Gerador de PDF fornece várias configurações predefinidas de PDF para uso. Não é possível modificar essas configurações predefinidas; no entanto, você pode criar uma configuração com base em uma existente editando-a e salvando-a com um novo nome.

**Impressão de alta qualidade:** Cria arquivos PDF para saída de alta qualidade. Esta configuração:

* reduz a resolução de imagens coloridas e em tons de cinza em 300 dpi
* reduz a resolução de imagens monocromáticas em 1200 dpi
* imprime em uma resolução de imagem mais alta
* usa outras configurações para preservar a quantidade máxima de informações sobre o documento original.

Esses arquivos PDF podem ser abertos no Adobe Acrobat 5 e Adobe Acrobat Reader® 5 ou posterior.

**Páginas de tamanho maior:** Cria documentos PDF adequados para exibição e impressão confiáveis de desenhos de engenharia maiores que 200 x 200 polegadas. documentos PDF criados podem ser abertos no Adobe Acrobat Professional e Acrobat Standard, versão 7 ou posterior, e no Adobe Reader 7 ou posterior.

**PDF/A-1B 2005 CMYK / PDF/A-1B 2005 RGB:** Verifica a conformidade das tarefas recebidas com o padrão ISO para preservação a longo prazo (arquivamento) de documentos eletrônicos e cria arquivos PDF/A somente se estiverem em conformidade. Esses arquivos são usados principalmente para arquivamento. Arquivos compatíveis podem conter apenas texto, imagens rasterizadas e objetos vetoriais; eles não podem conter criptografia e scripts. Além disso, todas as fontes devem ser incorporadas para que os documentos possam ser abertos e exibidos como criados. O PDF/A-1b usa o PDF 1.4 e converte todas as cores em CMYK ou RGB, dependendo do padrão escolhido. Os arquivos PDF criados com esse arquivo de configurações podem ser abertos no Acrobat 5 e no Acrobat Reader 5 e posterior. Para obter mais informações sobre PDF/A, consulte Adobe e padrões do setor.

**PDF/X-1a 2001:** Verifica a conformidade de trabalhos recebidos com PDF/X-1a e cria arquivos PDF somente se compatíveis. PDF/X-1a é um padrão ISO para troca de conteúdo gráfico. O PDF/X-1a requer que todas as fontes sejam incorporadas, que as caixas PDF apropriadas sejam especificadas e que a cor seja exibida como cores CMYK ou spot. Os arquivos PDF que atendem aos requisitos de PDF/X-1a são direcionados a uma condição de saída específica, como impressão offset na Web de acordo com as Especificações Publicações de compensação na Web. Para obter mais informações sobre PDF/X, consulte Adobe e padrões do setor.

**PDF/X-3 2002:** Verifica a conformidade de trabalhos recebidos com PDF/X-3 e cria arquivos PDF somente se compatíveis. Como o PDF/X-1a, o PDF/X-3 é um padrão ISO para troca de conteúdo gráfico. A principal diferença é que o PDF/X-3 suporta cores independentes de dispositivo.

**Qualidade de impressão:** Cria arquivos PDF para produção de impressão de alta qualidade (por exemplo, em uma fotocompositora ou platesetter). Nesse caso, o tamanho do arquivo não é uma consideração. O objetivo é manter todas as informações em um arquivo PDF que uma impressora comercial ou um provedor de serviço de pré-impressão precisa para imprimir o documento corretamente. Esse conjunto de opções:

* reduz a resolução de imagens coloridas e em tons de cinza em 300 dpi
* reduz a resolução de imagens monocromáticas em 1200 dpi
* incorpora subconjuntos de todas as fontes usadas no documento
* imprime uma resolução de imagem mais alta,
* não gira páginas automaticamente com base na orientação dos comentários do texto ou das convenções de estruturação de documentos (DSC)
* usa outras configurações para preservar a quantidade máxima de informações sobre o documento original.

Os trabalhos de impressão falharão se tiverem fontes que não podem ser incorporadas. Esses arquivos PDF podem ser abertos no Acrobat 5 e no Acrobat Reader 5 e posterior.

>[!NOTE]
>
>Antes de criar um arquivo PDF para enviar a uma impressora comercial ou para pré-pressionar um provedor de serviço, determine a resolução de saída e outras configurações ou solicite um arquivo .joboptions com as configurações recomendadas. Talvez seja necessário personalizar as configurações do Adobe PDF para um provedor específico e fornecer um arquivo .joboptions próprio.

**Menor tamanho de arquivo:** Cria arquivos PDF para exibição na Web ou em uma intranet, ou para distribuição por meio de um sistema de email para visualização na tela. Esse conjunto de opções usa compactação, diminuição da resolução e uma resolução de imagem relativamente baixa. Ele converte todas as cores em sRGB e não incorpora fontes, a menos que necessário. Também otimiza arquivos para o serviço de bytes. Esses arquivos PDF podem ser abertos no Acrobat 5 e no Acrobat Reader 5.0 e posterior.

**Padrão:** Cria arquivos PDF para imprimir em impressoras de desktop ou copiadoras digitais, publicar em um CD ou enviar para um cliente como prova de publicação. Esse conjunto de opções usa compactação e redução de resolução para reduzir o tamanho do arquivo. Também incorpora subconjuntos de todas as fontes usadas no arquivo, converte todas as cores em sRGB e imprime em uma resolução média para criar uma representação razoavelmente precisa do documento original. Observe que os subconjuntos de fontes do Microsoft Windows não estão incorporados por padrão. Esses arquivos PDF podem ser abertos no Acrobat 5 e no Acrobat Reader 5.0 e posterior.

## Adicionar ou editar configurações de PDF {#add-or-edit-pdf-settings}

As configurações de PDF determinam com precisão como os arquivos são convertidos e sua estrutura e recursos de PDF resultantes. Defina uma nova configuração de PDF ou edite uma que tenha sido criada anteriormente. Não é possível modificar configurações predefinidas, mas é possível criar uma configuração com base em uma existente, editando a configuração e salvando-a com um novo nome.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em Novo ou clique no nome de uma configuração existente.
1. Na página Nova/Editar configuração do Adobe PDF, preencha as informações necessárias nestas seções:

   [Opções gerais](configuring-pdf-settings.md#general-options)

   [Opções de imagens](configuring-pdf-settings.md#images-options)

   [Opções de fontes](configuring-pdf-settings.md#fonts-options)

   [Opções de cor](configuring-pdf-settings.md#color-options)

   [Opções avançadas](configuring-pdf-settings.md#advanced-options)

   [Opções de conformidade e relatórios de padrões](configuring-pdf-settings.md#standards-reporting-and-compliance-options)

   [Opções de visualização inicial](configuring-pdf-settings.md#initial-view-options)

   Para ir para outra seção, clique no link na página da Web ou use os botões Próximo e Anterior.

1. Depois de concluir as informações em todas as seções, clique em Salvar ou Salvar como e forneça um nome para a configuração.

## Carregar configurações de PDF {#upload-pdf-settings}

É possível ter configurações de PDF disponíveis no servidor do Gerador de PDF fazendo upload delas em um computador local ou em um local de rede.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF e clique em Carregar.
1. Na página Carregar configurações do Adobe PDF, clique em Procurar, localize o arquivo de configurações do PDF e clique em Abrir.
1. Clique em OK e em OK novamente.

## Excluir configurações de PDF {#delete-pdf-settings}

É possível excluir permanentemente as configurações do PDF se elas não forem mais necessárias.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. É possível selecionar várias configurações.
1. Clique em Excluir e, na página Confirmação de exclusão, clique em Excluir novamente.

## Opções gerais {#general-options}

Use as opções gerais para especificar a versão do Acrobat a ser usada para compatibilidade de arquivos e outras opções de arquivo e dispositivo. Para obter instruções sobre como acessar as opções Gerais, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

### Opções de arquivo {#file-options}

**Compatibilidade:** O nível de compatibilidade do arquivo PDF. Para documentos que serão amplamente distribuídos, considere selecionar o Acrobat 4 (PDF 1.3) ou o Acrobat 5 (PDF 1.4) para garantir que todos os usuários possam visualização e imprimir o documento. Se você criar arquivos usando a compatibilidade do Acrobat 5 ou posterior, eles podem não ser compatíveis com versões anteriores do Acrobat. As subseções a seguir mostram algumas das diferenças entre os arquivos PDF criados usando diferentes níveis de compatibilidade do Acrobat.

<table>
 <tbody>
  <tr>
   <th><p>Acrobat 4 (PDF 1.3)</p> </th>
   <th><p>Acrobat 5 (PDF 1.4)</p> </th>
   <th><p>Acrobat 6 (PDF 1.5)</p> </th>
   <th><p>Acrobat 7 (PDF 1.6) e Acrobat 8 (PDF 1.7)</p> </th>
  </tr>
  <tr>
   <td><p>Pode ser aberto com o Acrobat 3.0 e o Acrobat Reader 3.0 e posterior.</p> </td>
   <td><p>Pode ser aberto com o Acrobat 3.0 e o Acrobat Reader 3.0 e posterior. Os recursos específicos de versões posteriores podem ser perdidos ou não podem ser exibidos.</p> </td>
   <td><p>A maioria pode ser aberta com o Acrobat 4 e o Acrobat Reader 4.0 e posterior. Os recursos específicos de versões posteriores podem ser perdidos ou não podem ser exibidos.</p> </td>
   <td><p>A maioria pode ser aberta com o Acrobat 4 e o Acrobat Reader 4.0 e posterior. Os recursos específicos de versões posteriores podem ser perdidos ou não podem ser exibidos.</p> </td>
  </tr>
  <tr>
   <td><p>Não pode conter arte-final que usa efeitos de transparência ativa. Qualquer transparência deve ser nivelada antes da conversão para PDF 1.3.</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller acelera a transparência.)</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller acelera a transparência.)</p> </td>
   <td><p>Suporta o uso da transparência ao vivo no trabalho artístico. (O recurso Acrobat Distiller acelera a transparência.)</p> </td>
  </tr>
  <tr>
   <td><p>Camadas não são suportadas.</p> </td>
   <td><p>Camadas não são suportadas.</p> </td>
   <td><p>Preserva camadas ao criar arquivos PDF a partir de aplicativos que suportam a geração de documentos PDF em camadas, como o Adobe Illustrator® CS ou o Adobe InDesign® CS e posterior.</p> </td>
   <td><p>Preserva camadas ao criar arquivos PDF a partir de aplicativos que suportam a geração de documentos PDF em camadas, como o Illustrator CS ou o InDesign CS e posterior.</p> </td>
  </tr>
  <tr>
   <td><p>O espaço de cores DeviceN com 8 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com 8 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com até 31 corantes é suportado.</p> </td>
   <td><p>O espaço de cores DeviceN com até 31 corantes é suportado.</p> </td>
  </tr>
  <tr>
   <td><p>Fontes multibyte podem ser incorporadas. (O Distiller converte as fontes ao incorporá-las.)</p> </td>
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

**Compactação no nível do objeto:** Consolida pequenos objetos (cada um deles não é compactado) em fluxos que podem ser compactados com eficiência.

**Desligado:** Não compacta nenhuma informação estrutural no documento PDF. Selecione essa opção se desejar que os usuários visualizações, naveguem e interajam com marcadores e outras informações estruturais usando o Acrobat 5 e posterior.

**Somente tags:** Compacta as informações estruturais no documento PDF. O uso dessa opção resulta em um arquivo PDF que pode ser aberto e impresso usando o Acrobat 5. Os usuários não podem visualização nenhuma informação de acessibilidade, estrutura ou PDF marcado no Acrobat 5 ou no Acrobat Reader 5.0, mas podem visualização essa informação no Acrobat 6 e no Adobe Reader 6.0.

**Girar páginas automaticamente:** Define a rotação automática de páginas com base na orientação do texto ou dos comentários do DSC. Por exemplo, algumas páginas (como páginas que contêm tabelas) podem exigir que o usuário as vire de lado para lê-las. Selecione Individualmente para girar cada página com base na direção do texto nessa página. Selecione Coletivamente por arquivo para girar todas as páginas no documento com base na orientação da maioria do texto.

>[!NOTE]
>
>Se Processar comentários do DSC estiver selecionado nas configurações avançadas e se %%Visualizar comentários de orientação forem incluídos, esses comentários terão prioridade ao determinar a orientação da página.

**Vínculo:** Especifica se um arquivo PDF deve ser exibido com vínculo à esquerda ou à direita. Essa configuração afeta a exibição de páginas na Página oposta - Layout contínuo e a exibição de miniaturas lado a lado.

**Resolução:** Define a emulação para a resolução de uma impressora para arquivos de entrada que ajustam seu comportamento de acordo com a resolução da impressora para a qual estão sendo impressas. Para a maioria dos arquivos de entrada, uma configuração de resolução mais alta resulta em arquivos PDF maiores, mas de qualidade mais alta, e uma configuração mais baixa resulta em arquivos PDF menores, mas de qualidade mais baixa. Normalmente, a resolução determina o número de etapas em um gradiente ou uma mesclagem. Você pode inserir um valor de 72 a 4000. Mantenha essa configuração como padrão, a menos que planeje imprimir o arquivo PDF em uma impressora específica e deseje emular a resolução definida no arquivo de entrada original.

>[!NOTE]
>
>O aumento da configuração de resolução aumenta o tamanho do arquivo e pode aumentar ligeiramente o tempo necessário para processar alguns arquivos.

**Todas as páginas ou páginas de:** Especifica quais páginas serão convertidas. Deixe a caixa Para vazia para criar um intervalo do número da página inserido na caixa De até o final do arquivo.

**Otimizar Para Visualização Rápida Na Web:** Reestrutura o arquivo para download de página por vez (serviço de bytes) de servidores da Web. Essa opção compacta texto e arte em linha, independentemente do que você selecionou como configurações de compactação na guia Imagens. A compactação resulta em acesso e visualização mais rápidos ao baixar o arquivo da Web ou de uma rede. Por padrão, essa opção não está ativada.

### Tamanho padrão da página {#default-page-size}

As opções de Tamanho de página padrão especificam o tamanho de página a ser usado quando um não for especificado no arquivo original. Normalmente, os arquivos do Adobe PostScript incluem essas informações, exceto os arquivos Encapsulated PostScript (EPS), que fornecem um tamanho de caixa delimitadora, mas não um tamanho de página. O tamanho máximo de página permitido é de 15.000.000 polegadas (31.800.000 cm) em ambas as direções. Essas opções configuram o tamanho de página padrão:

**Largura:** Largura da página

**Altura:** Altura da página

**Unidades:** Unidades a serem usadas para as configurações de largura e altura

## Opções de imagens {#images-options}

As opções de Imagens especificam compactação e redefinição de resolução para imagens. Você pode experimentar essas opções para encontrar um equilíbrio apropriado entre o tamanho do arquivo e a qualidade da imagem. Para obter instruções sobre como acessar as configurações de Imagens, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

Essas opções configuram imagens coloridas, em tons de cinza e monocromáticas:

**Diminuir resolução:** Defina um valor para cada tipo de imagem. Para reduzir a resolução de imagens coloridas, em tons de cinza ou monocromáticas, o Gerador de PDF combina pixels em uma área de amostra para tornar um pixel maior. Forneça a resolução do dispositivo de saída em pontos por polegada (dpi) e insira uma resolução em dpi na caixa Para imagens acima. Para imagens com uma resolução acima desse limite, o Gerador de PDF combina pixels, conforme necessário, para reduzir a resolução da imagem (pixels por polegada) à configuração de dpi especificada. Para desativar a redução da resolução, selecione Desativado. Estas são as opções:

**Diminuição Média De Resolução Para:** Calcula a média dos pixels em uma área de amostra e substitui a área inteira pela cor média dos pixels na resolução especificada.

**Diminuição Da Resolução Bicúbica Para:** Usa uma média ponderada para determinar a cor dos pixels e geralmente gera melhores resultados que o método de média simples de redução da resolução. O bicúbico é o método mais lento, mas mais preciso, e resulta nas gradações tonais mais suaves.

**Subamostragem Para:** Seleciona um pixel no centro da área de amostra e substitui a área inteira por esse pixel na resolução especificada. A subamostragem reduz significativamente o tempo de conversão em comparação à diminuição da resolução, mas resulta em imagens menos suaves e contínuas.

A configuração de resolução para cor e escala de cinza deve ser de 1,5 a 2 vezes a resolução da tela de linha na qual o arquivo será impresso. (Desde que você não fique abaixo dessa configuração de resolução recomendada, as imagens que não contêm linhas retas ou padrões geométricos ou repetitivos não serão afetadas por uma resolução mais baixa.) A resolução para imagens monocromáticas deve ser a mesma do dispositivo de saída. No entanto, lembre-se de que salvar uma imagem monocromática em uma resolução superior a 1500 dpi aumenta o tamanho do arquivo sem melhorar visivelmente a qualidade da imagem.

Além disso, considere se os usuários precisam ampliar uma página. Por exemplo, se você estiver criando um documento PDF de um mapa, considere usar uma resolução de imagem mais alta para que os usuários possam ampliar o mapa.

>[!NOTE]
>
>A reamostragem de imagens monocromáticas pode ter resultados de visualização inesperados, como sem exibição de imagem. Se esse problema ocorrer, desative a reamostragem e converta o arquivo novamente. Este problema é mais provável de ocorrer com a diminuição da amostragem e menos provável de ocorrer com a diminuição da amostragem bicúbica.

Esta tabela mostra os tipos de impressoras e sua resolução medida em dpi, sua resolução de tela padrão medida em linhas por polegada (lpi) e uma resolução de reamostragem para imagens que são medidas em pixels por polegada (ppi). Por exemplo, para imprimir em uma impressora a laser de 600 dpi, digite 170 para obter a resolução de reamostrar as imagens.

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
   <td><p>1200 dpi (fotocompositora)</p> </td>
   <td><p>120 lpi</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 dpi (fotocompositora)</p> </td>
   <td><p>150 lpi</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

**Compactação:** Defina um valor para aplicar a imagens coloridas, em tons de cinza e monocromáticas. Para imagens coloridas e em tons de cinza, também defina a qualidade da imagem:

* Para imagens coloridas ou em tons de cinza, selecione ZIP para aplicar compactação que funcione bem em imagens que tenham grandes áreas de cores únicas ou padrões repetitivos. Exemplos são capturas de tela, imagens simples criadas com programas de tinta e imagens monocromáticas que contêm padrões repetidos. Selecione JPEG, de qualidade mínima a máxima, para aplicar a compactação adequada para imagens em tons de cinza ou coloridas, como fotografias em tons contínuos que contêm mais detalhes do que o que pode ser reproduzido na tela ou na impressão. Selecione Automático (JPEG) para determinar automaticamente a melhor qualidade para imagens coloridas e em tons de cinza.
* Para imagens monocromáticas, selecione CCITT Group 4, CCITT Group 3, ZIP, JPEG200, Automatic (JPEG2000) ou Run Length compression (Comprimento de execução).

Verifique se as imagens monocromáticas são digitalizadas como monocromáticas e não como em tons de cinza. O texto digitalizado às vezes é salvo como imagens em tons de cinza por padrão. O texto em tons de cinza compactado com o método de compactação JPEG não está claro e pode estar ilegível.

**Qualidade da imagem:** Configura a qualidade da imagem para imagens coloridas e em tons de cinza. As opções são mínimo, baixo, médio, alto e máximo.

**Suavização de borda para cinza:** Suaviza bordas irregulares em imagens monocromáticas. Selecione 2 bits, 4 bits ou 8 bits para especificar níveis de 4, 16 ou 256 de cinza. (A suavização de borda pode desfocar linhas pequenas ou finas.)

>[!NOTE]
>
>A compactação de texto e arte de linha está sempre ativada.

**Política de imagem:** Defina uma política para imagens coloridas, em tons de cinza e monocromáticas. Se a resolução da imagem cair abaixo da resolução especificada, você ainda poderá optar por continuar (Ignorar), fornecer uma mensagem de aviso ou cancelar o trabalho.

## Opções de fontes {#fonts-options}

As opções Fontes especificam quais fontes devem ser incorporadas a um arquivo PDF e se devem incorporar um subconjunto de caracteres usados no arquivo PDF. Para obter instruções sobre como acessar as opções de Fontes, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

>[!NOTE]
>
>Quando você combina arquivos PDF com o mesmo subconjunto de fontes, o Gerador de PDF tenta combinar os subconjuntos de fontes.

**Incorporar todas as fontes:** Incorpora todas as fontes usadas no arquivo. A incorporação de fonte é necessária para conformidade com PDF/X.

**Subconjunto De Fontes Incorporadas Quando A Porcentagem De Caracteres Usados É Menor Que:** Se você selecionar essa opção, especifique uma porcentagem limite para incorporar apenas um subconjunto das fontes. Por exemplo, se o limite for 35 e menos de 35% dos caracteres forem usados, o Gerador de PDF incorporará apenas esses caracteres. Somente as fontes com bits de permissão apropriados são incorporadas.

**Quando a incorporação falhar:** Especifica como o Gerador de PDF responde se não conseguir localizar uma fonte a ser incorporada ao processar um arquivo. Você pode fazer com que o Gerador de PDF ignore a solicitação e substitua a fonte, avise e substitua a fonte ou cancele o processamento do trabalho atual.

**Fonte:** O local das fontes que o Gerador de PDF usa.

### Especificar quais fontes serão incorporadas {#specify-which-fonts-to-embed}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em Novo ou no nome de uma configuração.
1. Clique em Fontes e desmarque Incorporar todas as fontes.
1. Na lista Fonte, selecione uma fonte e clique em Ir para atualizar a lista de fontes na caixa à esquerda.
1. Clique em uma fonte na caixa à esquerda. Em seguida, clique em Adicionar ao lado da caixa apropriada para movê-la para a lista Sempre incorporar ou Nunca incorporar. Repita o procedimento para cada fonte. Clique com a tecla Ctrl pressionada para selecionar várias fontes a serem movidas.
1. Para remover uma fonte da lista Sempre incorporar ou Nunca incorporar, selecione-a e clique em Remover ao lado da caixa apropriada. Esta ação não remove a fonte do sistema; apenas remove a referência a ela na lista.
1. Se a fonte que você deseja especificar não for exibida, digite seu nome na caixa Adicionar fonte e clique em Sempre incorporar ou Nunca incorporar. Os nomes de fontes não podem conter caracteres alfanuméricos.

>[!NOTE]
>
>Uma fonte TrueType pode conter uma configuração adicionada pelo designer de fontes que impede que a fonte seja incorporada em arquivos PDF.

>[!NOTE]
>
>As fontes são escolhidas do cache de fontes do sistema do Windows e é necessário reiniciar o sistema para atualizar o cache. Depois de especificar o diretório de fontes do Cliente, reinicie o sistema no qual os formulários AEM estão instalados.

## Opções de cor {#color-options}

As opções de Cor definem todas as informações de gerenciamento de cores do Gerador de PDF. Para obter instruções sobre como acessar as opções de Cor, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

### Configurações de cores da Adobe {#adobe-color-settings}

**Arquivo de configurações:** Esta lista contém uma lista de configurações de cores que também são usadas em aplicativos gráficos principais, como o Adobe Photoshop e o Adobe Illustrator. A configuração de cor selecionada determina as outras configurações de cor da Adobe nesta página. Por exemplo, se você selecionar uma configuração diferente de Nenhum, todas as opções diferentes daquelas para Dados dependentes de dispositivo serão predefinidas e esmaecidas. Você pode editar as configurações de Políticas de gerenciamento de cores e Espaços de trabalho somente se selecionar Nenhum para Arquivo de configurações.

### Políticas de gerenciamento de cores {#color-management-policies}

Se você selecionou Nenhum para o Arquivo de configurações, a área Políticas de gerenciamento de cores especifica como o Gerador de PDF converte cores não gerenciadas em um arquivo PostScript.

**Deixe a cor inalterada:** Deixa inalteradas as cores dependentes do dispositivo e preserva as cores independentes do dispositivo como o equivalente mais próximo possível no PDF. Essa opção é útil para as lojas de impressão que calibraram todos os dispositivos, usaram essas informações para especificar a cor no arquivo e a saída apenas para esses dispositivos.

**Marque tudo para Gerenciamento de cores:** Incorpora um perfil do International Color Consortium ao destilar arquivos e calibrar cores nas imagens, o que torna as cores dos arquivos PDF resultantes independentes do dispositivo se você selecionou o Acrobat 4 (PDF 1.3) ou posterior compatibilidade. Entretanto, os espaços de cores dependentes de dispositivo em arquivos (RGB, Tons de cinza e CMYK) são convertidos em espaços de cores independentes de dispositivo (CalRGB, CalGray e LAB).

**Imagens somente tag para gerenciamento de cores:** Incorpora perfis ICC somente em imagens, não em texto ou gráficos, ao destilar arquivos se você selecionou a compatibilidade do Acrobat 4 (PDF 1.3). Essa opção impede que o texto preto sofra qualquer mudança de cor. Entretanto, os espaços de cores dependentes de dispositivo em imagens (RGB, Tons de cinza e CMYK) são convertidos em espaços de cores independentes de dispositivo (CalRGB, CalGray e LAB). Texto e gráficos não são convertidos.

**Converter todas as cores em sRGB ou Converter todas as cores em CMYK:** Calibra a cor no arquivo, tornando a cor independente do dispositivo, semelhante a Tag All for Color Management. Se você selecionou a compatibilidade do Acrobat 4 (PDF 1.3) ou posterior e converteu para sRGB, as imagens CMYK e RGB são convertidas em sRGB.

Independentemente da opção de compatibilidade selecionada, as imagens em tons de cinza permanecem inalteradas. Isso geralmente reduz o tamanho e aumenta a velocidade de exibição de arquivos PDF, pois são necessárias menos informações para descrever imagens RGB do que para descrever imagens CMYK. Como RGB é o espaço de cor nativo usado em monitores, nenhuma conversão de cores é necessária durante a exibição, o que contribui para uma visualização on-line rápida. Essa opção é recomendada se o arquivo PDF for usado on-line ou com impressoras de baixa resolução.

**Propósito de renderização do Documento:** O método para mapear cores entre espaços de cores. O resultado de qualquer método específico depende dos perfis dos espaços de cores. Por exemplo, alguns perfis produzem resultados idênticos com métodos diferentes. Estas opções estão disponíveis:

>[!NOTE]
>
>Em todos os casos, as intenções podem ser ignoradas ou substituídas por operações de gerenciamento de cores que ocorrem após a criação do arquivo PDF.

**Preservar:** Significa que a intenção é especificada no dispositivo de saída, e não no arquivo PDF. Em muitos dispositivos de saída, Colorimétrico relativo é o propósito padrão.

**Perceptivo:** Mantém os valores de cor relativos entre os pixels originais à medida que são mapeados para a gama de destino. Este método preserva a relação visual entre as cores, embora os próprios valores de cor possam mudar.

**Saturação:** Mantém os valores de saturação relativos dos pixels originais. Este método é adequado para gráficos comerciais, onde a relação exata entre as cores não é tão importante quanto ter cores saturadas brilhantes.

**Colorimétrico relativo:** Remapeia o ponto branco do espaço de origem para o ponto branco do espaço de destino.

**Colorimétrico absoluto:** Desativa a correspondência de pontos brancos e pretos ao converter cores. Este método não é recomendado a menos que seja necessário preservar as cores da assinatura, como as usadas em marcas comerciais ou logotipos.

### Espaços de trabalho {#working-spaces}

Para todos os valores na lista em Políticas de gerenciamento de cores, exceto Deixar a cor inalterada, selecione uma das listas na área Espaço de trabalho para especificar quais perfis ICC são usados para definir e calibrar os espaços de cores em tons de cinza, RGB e CMYK em arquivos PDF destilados. Estas opções estão disponíveis:

**Cinza:** Define o espaço de cores de todas as imagens em tons de cinza nos arquivos. Essa opção está disponível somente se você escolher Tag All (Tudo) para Gerenciamento de cores ou Tag Only Images para Gerenciamento de cores. O perfil ICC padrão para imagens em cinza é Gama cinza 2.2. Você também pode selecionar Nenhum para impedir que imagens em tons de cinza sejam convertidas.

**RGB:** Define o espaço de cores de todas as imagens RGB em arquivos. O padrão, sRGB IEC61966-2.1, é geralmente uma boa escolha porque está se tornando um padrão industrial e muitos dispositivos de saída o reconhecem. Você também pode selecionar Nenhum para impedir que imagens RGB sejam convertidas.

**CMYK:** Define o espaço de cores de todas as imagens CMYK nos arquivos. O padrão é U.S. Web Coated (SWOP) v2. Você também pode selecionar Nenhum para impedir que imagens CMYK sejam convertidas.

>[!NOTE]
>
>Selecionar Nenhum para todos os três espaços de trabalho tem o mesmo efeito que selecionar Deixar cor inalterada.

**Preservar valores CMYK para espaços de cores CMYK calibrados:** Quando selecionados, os valores CMYK independentes de dispositivo são tratados como valores dependentes de dispositivo (DeviceCMYK), os espaços de cores independentes de dispositivo são descartados e os arquivos PDF/X-1a usam o valor Converter todas as cores em CMYK. Quando desmarcada, os espaços de cores independentes de dispositivo são convertidos em CMYK se a política de gerenciamento de cores estiver definida como Converter todas as cores em CMYK.

### Dados dependentes de dispositivo {#device-dependent-data}

Essas opções se aplicam se você trabalhar com documentos criados com documentação sofisticada e aplicativos gráficos, como o Adobe Illustrator e o Adobe InDesign. Para obter mais informações, consulte a documentação que acompanha o aplicativo.

As funções de transferência são utilizadas para efeitos artísticos e para ajustar as especificações de um dispositivo de saída específico. Por exemplo, um arquivo destinado à saída em uma fotocompositora específica pode conter funções de transferência que compensam o ganho de pontos inerente a essa impressora.

**Preservar A Remoção De Cores Abaixo E A Geração De Preto:** Mantém essas configurações se elas existem no arquivo PostScript. A geração de preto calcula a quantidade de preto a ser usada quando você está tentando reproduzir uma cor específica. A remoção de subcores (UCR) reduz a quantidade de componentes ciano, magenta e amarelo para compensar a quantidade de preto que a geração de preto adicionou. Por utilizar menos tinta, o UCR é geralmente utilizado para papel de jornal e material não revestido.

**Quando as funções de transferência forem encontradas:** Determina o que fazer quando as funções de transferência forem encontradas:

**Preservar:** Retém as funções de transferência tradicionalmente usadas para compensar o ganho de pontos ou a perda de pontos que pode ocorrer quando uma imagem é transferida para um filme. O ganho de pontos ocorre quando os pontos de tinta que compõem uma imagem impressa são maiores (por exemplo, devido a espalhamento em papel) do que na tela de meio-tom; a perda de pontos ocorre quando os pontos são impressos menores. Com essa opção, as funções de transferência são mantidas como parte do arquivo e são aplicadas ao arquivo quando o arquivo é enviado.

**Aplicar:** Não mantém a função de transferência, mas a aplica ao arquivo, o que altera as cores no arquivo. Essa opção é útil para criar efeitos de cor em um arquivo. Por padrão, essa opção é selecionada para novas configurações.

**Remover:** Remove quaisquer funções de transferência aplicadas. Remova funções de transferência aplicadas, a menos que o arquivo PDF seja enviado para o mesmo dispositivo para o qual o arquivo PostScript de origem foi criado.

**Preservar informações de meio-tom:** Mantém as informações de meio-tom nos arquivos. As informações de meio-tom consistem em pontos que controlam a quantidade de dispositivos de meio-tom de tinta depositada em um local específico no papel. Variar o tamanho e a densidade dos pontos cria a ilusão de variações de cinza ou cor contínua. Para uma imagem CMYK, são usadas quatro telas de meio-tom, uma para cada tinta usada no processo de impressão.

Na produção de impressão tradicional, um meio-tom é produzido colocando uma tela de meio-tom entre um filme e a imagem e depois expondo o filme. Equivalentes eletrônicos, como no Adobe Photoshop, permitem que os usuários especifiquem os atributos da tela de meio-tom antes de produzirem a saída de filme ou papel. As informações de meio-tom são destinadas ao uso com um dispositivo de saída específico.

## Opções avançadas {#advanced-options}

As opções avançadas especificam quais comentários do DSC (Convenções de estruturação de Documentos) devem ser mantidos no arquivo PDF e como definir outras opções que afetam a conversão do PostScript. Em um arquivo PostScript, os comentários do DSC contêm informações sobre o arquivo (como o aplicativo de origem, a data de criação e a orientação da página). Eles também fornecem estrutura para as descrições de página no arquivo (como instruções de início e término para uma seção de prolog). Os comentários do DSC podem ser úteis quando seu documento for imprimir ou pressionar. Para obter instruções sobre como acessar as opções avançadas, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

Ao trabalhar com as opções avançadas, é útil conhecer a linguagem PostScript e como ela é traduzida para PDF. (Consulte [Adobe PostScript 3](https://www.adobe.com/products/postscript/main.html).)

**Permitir que o arquivo PostScript substitua as configurações do Adobe PDF:** Usa configurações armazenadas em um arquivo PostScript em vez do arquivo atual de configurações do Adobe PDF. Antes de processar um arquivo PostScript, você pode colocar parâmetros no arquivo para controlar os seguintes aspectos:

* compactação de texto e gráficos
* diminuição da amostragem e codificação de imagens de amostra
* incorporação de fontes Tipo 1 e instâncias de fontes Múltiplas Tipo 1

**Permitir PostScript XObjects:** PostScript XObjects armazenam informações que aparecem em muitas páginas do mesmo arquivo, como uma imagem de plano de fundo ou informações de cabeçalho e rodapé. O uso de PostScript XObjects pode resultar em impressão mais rápida, mas requer mais memória da impressora. Para impedir que PostScript XObjects sejam criados, desmarque essa opção se você criar arquivos PDF com o Acrobat 5 (PDF 1.4) ou compatibilidade posterior.

**Converter gradientes em sombras suaves:** Converte misturas em sombras suaves para o Acrobat 4 e posterior, tornando os arquivos PDF menores e potencialmente melhorando a qualidade da saída final. O Gerador de PDF converte gradientes do Adobe Illustrator, Adobe InDesign, Adobe FreeHand MX, CorelDraw, Quark Xpress e Microsoft PowerPoint.

**Converter linhas suaves em curvas:** Reduz a quantidade de pontos de controle usados para criar curvas em desenhos CAD, o que resulta em PDFs menores e renderização na tela mais rápida.

**Preservar seminários de Copypage do Nível 2:** Usa o operador copypage definido em LanguageLevel 2 PostScript em vez de LanguageLevel 3 PostScript. Se você tiver um arquivo PostScript e selecionar essa opção, um operador de página de cópia copiará a página. Se essa opção não for selecionada, o equivalente a uma operação de página de exibição será executado, mas o estado gráfico não será reinicializado.

**Preservar configurações de superimposição:** Mantém qualquer configuração de superimposição em arquivos que estão sendo convertidos em PDF. As cores sobrepostas são duas ou mais tintas impressas uma sobre a outra. Por exemplo, quando uma tinta ciano é impressa sobre uma tinta amarela, a impressão sobreposta resultante é uma cor verde. Sem impressão sobreposta, o amarelo subjacente não seria impresso, resultando numa cor ciana.

**O padrão de superimposição é impressão sobreposta diferente de zero:** Impede que objetos superimpressos com valores CMYK zero destruam objetos CMYK que estão abaixo deles. Esse efeito é obtido inserindo o parâmetro de estado gráfico OPM 1 no arquivo PDF onde o operador de impressão sobreposta estiver presente.

**Salvar configurações do Adobe PDF dentro do arquivo PDF:** Incorpora o arquivo de configurações usado para criar o arquivo PDF. Você pode abrir e visualização o arquivo de configurações (que tem uma extensão de arquivo .joboptions) na caixa de diálogo Anexos de arquivo no Acrobat. O arquivo de configurações do Adobe PDF torna-se um item na árvore Arquivos incorporados dentro do arquivo PDF.

**Salve as imagens JPEG originais em PDF, se possível:** Processa quaisquer imagens JPEG compactadas (imagens que já estão compactadas usando a codificação DCT) sem a recompactação. Se essa opção for selecionada, o Gerador de PDF descompactará as imagens JPEG para garantir que elas não estejam corrompidas. No entanto, ele não reprime imagens válidas, portanto, processando a imagem original intocada. Com essa opção selecionada, o desempenho melhora porque somente a descompactação (e não a recompactação) ocorre e os dados e metadados da imagem são preservados.

**Salvar tíquete de trabalho portátil dentro do arquivo PDF:** Preserva um tíquete de tarefa PostScript em um arquivo PDF. O ticket de tarefa contém informações sobre o arquivo PostScript, como tamanho da página, resolução e informações de interrupção, em vez de informações sobre conteúdo. Essas informações podem ser usadas posteriormente em um fluxo de trabalho ou para impressão do PDF.

**Use Prolog.ps e Epilog.ps:** Envia um arquivo de prólogo e epílogo com cada tarefa. Esses arquivos têm muitas finalidades. Por exemplo, os arquivos de prólogo podem ser editados para especificar páginas de capa. Arquivos de log podem ser editados para resolver uma série de procedimentos em um arquivo PostScript. Você pode fazer upload ou download dos arquivos. (Consulte Upload e download de arquivos de prólogo e de epílogo.)

**Processar comentários do DSC:** Mantém as informações do DSC de um arquivo PostScript. Essas subopções estão disponíveis:

**Registrar avisos do DSC:** Exibe mensagens de aviso sobre comentários DSC problemáticos durante o processamento e as adiciona a um arquivo de log.

**Preservar informações de EPS do DSC:** Retém informações, como o aplicativo de origem e a data de criação de um arquivo EPS. Se essa opção estiver desmarcada, a página será dimensionada e centralizada com base no canto superior esquerdo do objeto superior esquerdo e no canto inferior direito do objeto inferior direito na página.

**Preservar comentários OPI:** Mantém as informações necessárias para substituir uma imagem For Placement Only (FPO) ou um comentário pela imagem de alta resolução localizada nos servidores que suportam as versões 1.3 e 2.0 da Open Prepress Interface (OPI).

**Preservar informações do Documento do DSC:** Mantém informações como título, data de criação e hora. Quando um arquivo PDF é aberto no Acrobat, essas informações são exibidas no painel Descrição das propriedades do Documento.

**Redimensionar página e centralizar arte-final para arquivos EPS:** Centraliza uma imagem EPS e redimensiona a página para ajustá-la de perto à imagem. Esta opção se aplica somente a trabalhos que consistem em um único arquivo EPS.

## Opções de conformidade e relatórios de padrões {#standards-reporting-and-compliance-options}

O Gerador de PDF pode verificar o conteúdo do documento em um arquivo PostScript para garantir que ele atenda aos critérios padrão PDF/X-1a, PDF/X-3 ou PDF/A antes de criar o arquivo PDF. Para arquivos compatíveis com PDF/X, também é possível exigir que o arquivo PostScript atenda a critérios adicionais selecionando outras opções em &quot;relatórios padrão e conformidade&quot;. A disponibilidade das opções depende do padrão selecionado.

Os arquivos compatíveis com PDF/X são usados principalmente como um formato padronizado para troca de arquivos PDF destinados à produção de impressão de alta resolução. A menos que você esteja criando um documento PDF para produção de impressão, poderá ignorar os padrões de conformidade do PDF/X.

Os arquivos compatíveis com PDF/A são usados principalmente para arquivamento. Como a preservação a longo prazo é o objetivo, o documento deve conter apenas o que é necessário para abrir e visualizar durante toda a vida útil planejada do documento. Por exemplo, arquivos compatíveis com PDF/A podem conter apenas texto, imagens rasterizadas e objetos vetoriais; eles não podem conter criptografia e scripts. Além disso, todas as fontes devem ser incorporadas para que os documentos possam ser abertos e exibidos como criados. Em outras palavras, os documentos compatíveis com PDF/A são *mais finos* do que seus equivalentes PDF/X, que são destinados à produção high-end.

>[!NOTE]
>
>Se você configurar uma pasta monitorada para criar arquivos compatíveis com PDF/A, certifique-se de não adicionar segurança à pasta; o padrão PDF/A não permite criptografia.

Para obter instruções sobre como acessar o relatórios de padrões e as opções de conformidade, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

**Padrão de conformidade:** Selecione um padrão para produzir um relatório que indique se o arquivo está em conformidade com os requisitos e, em caso negativo, quais problemas foram encontrados. Quando a opção Compatibilidade na página Configurações gerais estiver definida como Acrobat 4.0, as seguintes opções serão ativadas. Quando Compatibilidade estiver definida como Acrobat 5.0, somente as opções do Acrobat 5.0 estarão disponíveis para seleção. Quando a opção Compatibilidade estiver definida como uma opção alternativa, as seguintes opções estarão esmaecidas:

* PDF/X-1a (compatível com o Acrobat 4.0)
* PDF/X-3 (compatível com o Acrobat 4.0)
* PDF/X-1a (compatível com o Acrobat 5.0)
* PDF/X-3 (compatível com o Acrobat 5.0)
* PDF/A-1b (compatível com o Acrobat 5.0)

### Opções para padrões PDF/X {#options-for-pdf-x-standards}

**Quando não for compatível:** Especifica se o arquivo PDF deve ser criado se o arquivo PostScript não estiver em conformidade com os requisitos do PDF/X. Essa opção está disponível quando o Padrão de conformidade na página Relatórios de padrões e conformidade está definido para uma opção diferente de Nenhum.

**Continue:** Cria um arquivo PDF.

**Cancelar tarefa:** Cria um arquivo PDF somente se o arquivo PostScript atender aos requisitos de PDF/X das opções de relatório selecionadas e for válido. Se ambas as opções de relatório PDF/X estiverem selecionadas e o arquivo PostScript atender somente a um conjunto de critérios PDF/X (por exemplo, PDF/X-3), o Gerador de PDF criará o arquivo compatível.

**Se TrimBox E ArtBox Não Estiverem Especificados:** Disponível quando o Padrão de conformidade na página Relatórios de padrões e conformidade estiver definido para uma opção diferente de Nenhum.

**Relatório como erro:** Sinaliza o arquivo PostScript como não compatível se uma das opções de relatórios estiver selecionada e uma caixa de aparo ou caixa de arte estiver ausente em qualquer página.

**Defina TrimBox Como MediaBox Com Deslocamentos:** Calcula os valores em pontos para a caixa de apara com base nos deslocamentos para a caixa de mídia das respectivas páginas se nem a caixa de apara nem a caixa de arte forem especificadas. A caixa de apara é sempre tão pequena ou menor que a caixa de mídia circundante.

**Se BleedBox Não Estiver Especificado:** Disponível quando o Padrão de conformidade na página Relatórios de padrões e conformidade estiver definido para uma opção diferente de Nenhum.

**Defina BleedBox como MediaBox:** Usa os valores da caixa de mídia para a caixa de sangria se a caixa de sangria não for especificada.

**Defina BleedBox como TrimBox com Deslocamentos:** Calcula valores em pontos para a caixa de sangria com base nos deslocamentos para a caixa de aparagem das respectivas páginas se a caixa de sangria não for especificada. A caixa de sangria é sempre tão grande ou maior que a caixa de aparagem fechada.

**Valores Padrão Se Não Especificados No Documento:** Essa opção está disponível quando o Padrão de conformidade na página Relatórios de padrões e conformidade está definido para uma opção diferente de Nenhum.

**Nome do Perfil do propósito de saída:** Indica a condição de impressão caracterizada para a qual o documento está preparado. Se um documento não especificar um nome de Propósito de Saída, o Gerador de PDF usará o valor selecionado nesse menu. Você pode selecionar um dos nomes fornecidos ou digitar um nome no espaço fornecido. Se o fluxo de trabalho exigir que o documento especifique o propósito de saída, selecione Nenhum. Qualquer documento que não atende aos requisitos falha na verificação de conformidade.

**Identificador da condição de saída:** Indica o nome de referência especificado pelo registro do nome do perfil do propósito de saída.

**Condição de saída:** Descreve a condição de impressão pretendida. Essa entrada pode ser útil para o receptor pretendido do documento PDF.

**Nome do Registro (URL):** Indica o endereço da Web para obter mais informações sobre o registro. O URL é inserido automaticamente para nomes de registro ICC.

**Interrompido:** Indica o estado do trapping no documento. A conformidade com o PDF/X requer um valor Verdadeiro ou Falso. Se o documento não especificar o estado capturado, o valor fornecido aqui será usado. Se o fluxo de trabalho exigir que o documento especifique o estado capturado, selecione Deixar indefinido. Qualquer documento que não atende aos requisitos falha na verificação de conformidade.

### Opções para o padrão PDF/A {#options-for-pdf-a-standard}

Essas opções são ativadas quando a opção Compatibilidade (na área Geral) está definida como Acrobat 4 (PDF 1.3) ou Acrobat 5 (PDF 1.4).

**Quando não for compatível:** Especifica se o arquivo PDF deve ser criado se o arquivo PostScript não estiver em conformidade com os requisitos de PDF/A.

**Continue:** Cria um arquivo PDF mesmo se o arquivo PostScript não atender aos requisitos do padrão.

**Cancelar tarefa:** Cria um arquivo PDF somente se o arquivo PostScript atender aos requisitos de PDF/A e for válido.

**Nome do Perfil do propósito de saída:** Indica a condição de impressão caracterizada para a qual o documento foi preparado e é necessário para conformidade com PDF/A. Se o fluxo de trabalho exigir que o documento especifique as informações de Propósito de saída, selecione &quot;Nenhum&quot;. A verificação de conformidade do documento falhará se essas informações não forem fornecidas.

**Condição de saída:** Descreve a condição de impressão pretendida. Essa entrada não é obrigatória, mas pode ser usada para fornecer informações úteis ao destinatário pretendido do documento PDF.

## Opções de visualização inicial {#initial-view-options}

Essas opções são organizadas em três áreas: Opções de Documento, Opções de janela e Opções de interface do usuário. Para obter instruções sobre como acessar as opções de visualização inicial, consulte [Adicionar ou editar configurações](configuring-pdf-settings.md#add-or-edit-pdf-settings)de PDF.

Para usar qualquer opção, selecione Definir configurações de Visualização inicial.

### Opções de Documento {#document-options}

As opções de documento controlam a aparência do documento dentro da janela do documento, como o nível de ampliação e como ele rola.

**Mostrar:** Determina quais painéis e guias são exibidos na janela do aplicativo por padrão. O Painel de marcadores e a Página abrem o painel documento e exibem a guia Marcadores.

**Layout da página:** Determina se o documento é exibido no modo de página única, página oposta, página contínua ou página oposta contínua.

**Ampliação:** Define o nível de zoom usado para exibir o documento quando aberto. O padrão usa o valor de ampliação configurado pelo usuário nas preferências do Acrobat ou do Adobe Reader.

**Abrir no número da página:** Define a página na qual o documento é aberto, que geralmente é a página 1.

>[!NOTE]
>
>A configuração Padrão para as opções de ampliação e layout de página usa as configurações individuais do usuário nas preferências de Exibição de página no Acrobat ou Adobe Reader.

### Opções de janela {#window-options}

As opções de janela determinam como a janela se ajusta na área da tela quando um usuário abre a documento. No entanto, as opções não têm efeito quando um documento PDF é exibido dentro de um navegador da Web.

**Redimensionar Janela Para Página Inicial:** Ajusta a janela do documento para ajustá-la suavemente à página de abertura, de acordo com as opções selecionadas em Opções do Documento.

**Centralizar janela na tela:** Posiciona a janela no centro da área da tela.

**Abrir no modo de tela cheia:** Maximiza a janela do documento e exibe o documento sem a barra de menus, a barra de ferramentas ou os controles da janela.

**Mostrar:** O nome do arquivo mostra o nome do arquivo na barra de título da janela. O título do Documento mostra o título do documento na barra de título da janela.

### Opções da interface do usuário {#user-interface-options}

As opções da interface do usuário determinam quais controles são exibidos ou ocultos quando o usuário abre o documento.

**Ocultar barra de menus:** Se selecionado, oculta a barra de menus

**Ocultar barras de ferramentas:** Se selecionado, oculta as barras de ferramentas

**Ocultar controles de janela:** Se selecionado, oculta os controles da janela

>[!NOTE]
>
>Se você ocultar a barra de menus e a barra de ferramentas, os usuários não poderão aplicar comandos e selecionar ferramentas, a menos que saibam os atalhos do teclado ao abrir o arquivo no Acrobat.

## Fazer upload e download de arquivos de perfil e epilog {#uploading-and-downloading-prologue-and-epilogue-files}

Os arquivos de perfil são usados para adicionar código PostScript personalizado que é executado no início de cada tarefa PostScript que está sendo destilado. Os arquivos de log são usados para adicionar código PostScript personalizado que é executado no final de cada tarefa PostScript. Você pode baixar arquivos de prólogo e epílogo do servidor para salvá-los localmente. Talvez você queira baixar os arquivos para configurá-los independentemente ou carregá-los em outro local ou em outro computador.

Esses arquivos têm muitas finalidades. Por exemplo, os arquivos de perfil podem ser editados para especificar páginas de capa; arquivos epilog podem ser editados para resolver uma série de procedimentos em um arquivo PostScript. Você também pode selecionar e fazer upload dos arquivos de prólogo e de epílogo para enviar com cada tarefa.

### Baixar um arquivo prolog ou epilog {#download-a-prologue-or-epilogue-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em Novo ou no nome de uma configuração.
1. Clique em Avançado e, ao lado da opção Usar Prolog.ps e Epilog.ps, clique em Download.
1. Na página Baixar arquivos do Prolog e do Epilog, clique em Prolog.ps ou Epilog.ps e clique em Salvar.

### Carregar um arquivo de prólogo ou epílogo {#upload-a-prologue-or-epilogue-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações do Adobe PDF.
1. Clique em Novo ou no nome de uma configuração.
1. Clique em Avançado e, ao lado da opção Usar Prolog.ps e Epilog.ps, clique em Carregar.
1. Na página Carregar arquivos do Prolog e do Epilog, clique em Procurar para selecionar um arquivo do prolog ou de epilog.
1. Localize o arquivo e clique em Abrir.
1. Para usar o arquivo, verifique se Usar o Prolog.ps e o Epilog.ps está selecionado na área Avançado da página Nova/Editar configuração do Adobe PDF.
1. Clique em Salvar

>[!NOTE]
>
>O Gerador de PDF suporta arquivos de prólogo e epilog somente para conversão de arquivos PostScript e Encapsulated PostScript em PDF.

