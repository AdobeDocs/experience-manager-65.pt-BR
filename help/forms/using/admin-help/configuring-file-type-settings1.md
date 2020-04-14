---
title: Definição das configurações de tipo de arquivo
seo-title: Definição das configurações de tipo de arquivo
description: Saiba como configurar as configurações de tipo de arquivo.
seo-description: Saiba como configurar as configurações de tipo de arquivo.
uuid: 58a05500-ffbb-4fa2-8ae1-8ac80ab2d099
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 89f4d3cf-eb2e-4d55-8209-16ecbba03792
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Definição das configurações de tipo de arquivo {#configuring-file-type-settings}

No Gerador de PDF, você pode configurar as configurações do aplicativo para os tipos de arquivo suportados. No Windows, você pode configurar as configurações do aplicativo para cada tipo de arquivo suportado. No UNIX e no Linux, você pode configurar as configurações do aplicativo para HTML-PDF e OpenOffice.

Na página Configurações de tipo de arquivo, é possível executar estas tarefas:

* [Criar ou editar uma configuração de Tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)
* Especificar quais configurações de tipo de arquivo usar por padrão (consulte [Importação e exportação de arquivos](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)de configuração do Gerador de PDF)
* [Alterar as configurações padrão](/help/forms/using/admin-help/configuring-file-type-settings1.md#change-the-default-settings)
* [Habilitar suporte a PDF/A](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)
* [Excluir uma configuração de Tipo de arquivo](https://helpx.adobe.com/aem-forms/6-2/admin-help/enable-pdf-a-support.html)

>[!NOTE]
>
>As configurações de tipo de arquivo não estão disponíveis para os conversores de fallback, como o Acrobat para conversão HTML em PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Criar ou editar configurações de Tipo de arquivo {#create-or-edit-file-type-settings}

Crie ou edite uma configuração de tipo de arquivo para especificar como o aplicativo lida com a conversão de tipos de arquivo suportados. No Windows, você pode configurar as configurações do aplicativo para cada tipo de arquivo suportado. No UNIX e no Linux, você pode configurar as configurações do aplicativo para HTML-PDF e OpenOffice.

1. No console de administração, clique em **[!UICONTROL Serviços]** > Gerador **[!UICONTROL de]** PDF > Configurações **[!UICONTROL de tipo de]** arquivo.
1. Clique em Novo ou no nome de uma configuração.
1. Na caixa Extensões de nome de arquivo, digite as extensões de nome de arquivo, separadas por vírgulas, para tipos de arquivo aceitos para este aplicativo. Não inclua o período anterior ou um espaço entre as extensões. O padrão é `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para usar o reconhecimento óptico de código (OCR) do texto em gráficos ou imagens, selecione Usar OCR e defina as seguintes opções:

**Principal idioma OCRL:** O idioma para o mecanismo de OCR usar para identificar os caracteres. O padrão é inglês (EUA).

**Estilo de saída do PDF:** Selecione Imagem pesquisável para ter uma imagem de bitmap das páginas em primeiro plano e o texto digitalizado em uma camada invisível abaixo. A aparência da página não muda, mas o texto se torna selecionável e legível. Selecione Texto e gráficos formatados para reconstruir a página original usando texto, fontes, imagens e outros elementos gráficos reconhecidos. O padrão é Imagem pesquisável (Exata).

**Diminuir resolução de imagens:** Diminui o número de pixels em imagens coloridas, em tons de cinza e monocromáticas. A redução da resolução de imagens digitalizadas é realizada após a conclusão do OCR. O padrão é Lowest (600 dpi). Essa opção não estará disponível se você definir o estilo de saída PDF como Imagem pesquisável (Exata).

1. Preencha as informações necessárias nestas seções:

   [Importação e exportação de arquivos de configuração do Gerador de PDF](https://helpx.adobe.com/aem-forms/6-2/admin-help/importing-exporting-pdf-generator-configuration.html)

   [Configurações de exportação do Adobe PDF (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-2)

   [Configurações de HTML para PDF](#html-to-pdf-settings)

   [Configurações de vídeos Flash para PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-9)

   [Configurações do XPS para PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-10)

   [Configurações do otimizador de PDF](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-11)

   [Configurações do Microsoft Excel (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-excel-settings-windows-only)

   [Configurações do Microsoft PowerPoint (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-powerpoint-settings-windows-only)

   [Configurações do Microsoft Project (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-project-settings-windows-only)

   [Configurações do Microsoft Word (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-word-settings-windows-only)

   [Configurações do Microsoft Visio (somente Windows)](#visio)

   [Configurações do Microsoft Publisher (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#microsoft-publisher-settings-windows-only)

   [Configurações do AutoCAD (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings1.md#autocad-settings-windows-only)

   [Configurações do OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings1.md#openoffice-settings)

   [Configurações de outros aplicativos (somente Windows)](#other-applications-settings-windows-only)

   Para ir para outra seção, clique no link correspondente na página da Web ou use os botões **[!UICONTROL Avançar]**ou **[!UICONTROL Anterior]** .

1. Depois de concluir todas as seções, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar como]** e forneça um nome para a configuração.

O suporte para vários tipos de arquivos pode ser personalizado. (Consulte &quot; [Adicionar suporte para formatos](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)de arquivo nativos adicionais&quot; em [Programação com formulários](https://www.adobe.com/go/learn_lc_programming_11)AEM.)

## Alterar as configurações padrão {#change-the-default-settings}

Você pode alterar o valor padrão das configurações do Adobe PDF, das configurações de segurança e das configurações de tipo de arquivo que se aplicam às fontes recém-criadas. Alterar os padrões não afeta as configurações de fontes existentes.

1. No Console de administração, clique em **[!UICONTROL Serviços > Gerador]** de PDF.
1. Na página Configurações **[!UICONTROL do]** Adobe PDF, Configurações **[!UICONTROL de tipo de]** arquivo ou Configurações **[!UICONTROL de]** segurança, clique em **[!UICONTROL Definir configurações]** padrão.
1. Selecione suas configurações padrão preferenciais. Uma ou mais das seguintes configurações estão disponíveis na página Definir configurações padrão:

   **[!UICONTROL Configuração]** do Adobe PDF: O padrão original é Standard (Acrobat 6).

   **[!UICONTROL Configurações]** de segurança: O padrão original é Sem segurança (Acrobat 5).

   **[!UICONTROL Configurações]** de tipo de arquivo: O padrão original é Standard.

1. Clique em **[!UICONTROL Salvar]**.

## Excluir uma configuração de Tipo de arquivo {#delete-a-file-type-setting}

É possível excluir uma configuração de tipo de arquivo que não é mais usada.

1. No console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF > Configurações]** de tipo de arquivo.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. É possível selecionar várias fontes. As configurações que não têm uma caixa de seleção ao lado delas são sempre incluídas no Gerador de PDF e não podem ser excluídas.
1. Clique em **[!UICONTROL Excluir]** e, na página Confirmação de exclusão, clique em **[!UICONTROL Excluir]**.

## Configurações de imagem para PDF {#image-to-pdf-settings}

As opções a seguir determinam como os arquivos de imagem são convertidos em PDF. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações](configuring-file-type-settings.md#create-or-edit-file-type-settings)de tipo de arquivo.

**Extensões de nome de arquivo:** lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

**Tente Conversor de fallback:** O Gerador de PDF pode usar o Java™ ou o Acrobat para converter arquivos de imagem em PDF. Quando essa opção é selecionada e uma conversão falha ou atinge o limite de tempo limite especificado, o Gerador de PDF tenta a conversão usando o método alternativo. Se um método alternativo falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

***Observação **: Arquivos JPEG 2000 só podem ser convertidos usando o Acrobat.*

**Usar OCR:** Especifica se o OCR (reconhecimento óptico de caracteres) deve ser aplicado ao PDF. O software OCR permite que você pesquise, corrija e copie o texto no PDF.

***observação **: O recurso OCR PDF (PDF pesquisável) é compatível somente com o Microsoft Windows.*

**Idioma principal do OCR:** Especifica o idioma a ser usado pelo mecanismo de OCR para identificar os caracteres.

**Estilo de saída do PDF:** Determina o tipo de PDF a ser produzido. Todos os formatos aplicam OCR e reconhecimento de fontes e páginas às imagens de texto e as convertem em texto normal.

**Imagem pesquisável:** Garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original, a desmarca conforme necessário e coloca uma camada de texto invisível sobre ela. A opção Diminuir resolução de imagens determina se a imagem está com resolução reduzida e em que extensão.

**Imagem pesquisável (Exata):** Garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original e coloca uma camada de texto invisível sobre ela. Recomendado para casos que exigem fidelidade máxima à imagem original.

**ClearScan:** Sintetiza uma nova fonte Tipo 3 que aproxima o original de perto e preserva o plano de fundo da página usando uma cópia de baixa resolução.

**Diminuir resolução de imagens:** Diminui o número de pixels em cores, tons de cinza e imagens monocromáticas após a conclusão do OCR. Escolha o grau de redução da resolução a ser aplicado. As opções com numeração mais alta reduzem a resolução, o que produz PDFs com resolução mais alta.

## Configurações de exportação do Adobe PDF (somente Windows) {#adobe-pdf-export-settings-windows-only}

A configuração Exportar tipo de arquivo na seção de configurações de exportação do Adobe PDF é usada para converter um arquivo PDF em outro formato. O padrão é HTML 4.01 com folhas de estilos em cascata (CSS) 1.0(&amp;ast;.htm, &amp;ast;.html).

Para obter instruções sobre como acessar essa configuração, consulte [Criar ou editar configurações](configuring-file-type-settings.md#create-or-edit-file-type-settings)de tipo de arquivo.

## Configurações de HTML para PDF {#html-to-pdf-settings}

As opções a seguir determinam como os arquivos HTML são convertidos em PDF. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](configuring-file-type-settings.md#create-or-edit-file-type-settings)de tipo de arquivo.

**Tente Conversor de fallback:** O Gerador de PDF pode usar o Java™ ou o Acrobat para converter arquivos HTML em PDF. Quando essa opção é selecionada e uma conversão falha ou atinge o limite de tempo limite especificado, o Gerador de PDF tenta a conversão usando o método alternativo. Se um método alternativo falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Codificação padrão:** Define a codificação de entrada do texto do arquivo a partir de um menu de sistemas operacionais e alfabetos. Usa a seleção mostrada na opção Codificação padrão somente se o arquivo de origem HTML não especificar um tipo de codificação.

**Forçar codificação selecionada:** Ignora qualquer codificação especificada no arquivo de origem HTML e usa a seleção mostrada na opção Codificação padrão.

### Configurações de aranha {#spidering-settings}

*O Spidering* verifica as páginas da Web em busca de links para outras páginas da Web. Quando um link para outra página da Web é encontrado, a página de destino é buscada e incluída no documento PDF gerado. Ative estas opções para definir o número de níveis a serem obtidos e convertidos em PDF:

**Obter Apenas Níveis X:** Spiders e converte páginas até uma profundidade do nível especificado a partir do URL da página base. Um valor de 1 converte apenas o URL fornecido.

**Obter site inteiro:** Converte o site inteiro, começando pelo URL fornecido.

**Permaneça No Mesmo Caminho:** Quaisquer links que apontem para páginas que não estejam no mesmo caminho relativo do URL base não serão convertidos durante o spidering.

**Permaneça No Mesmo Servidor:** Quaisquer links que apontem para páginas em servidores diferentes não são convertidos durante a aranha. Somente os links que apontam para o mesmo servidor que o URL especificado são convertidos.

### Configurações de conversão de página {#page-conversion-settings}

Ative essas opções para especificar como as páginas HTML são convertidas. Com base no tamanho da página, os valores de largura, altura e margem se ajustam de acordo.

**Tamanho da página:** Escolha personalizado e especifique a largura e a altura, ou selecione dimensões predefinidas.

**Orientação:** Selecione retrato ou paisagem para o documento PDF convertido.

**Margens:** Especifica as margens (Superior, Inferior, Esquerda e Direita) no documento PDF gerado.

**Adicionar marcadores ao PDF:** Adiciona marcadores ao documento PDF.

**Ativar PDF marcado:** Incorpora tags ao documento PDF.

**Definir configurações de Visualização inicial:** Permite configurar Opções de Documento, Opções de Janela e Opções de Interface do Usuário. Essas configurações determinam como o conteúdo é exibido inicialmente.

### Opções de Documento {#document-options}

Ative essas opções para especificar como exibir o conteúdo, como exibir as páginas no documento PDF e como especificar o nível de ampliação:

**Mostrar:** Selecione os painéis a serem abertos no Acrobat quando o documento PDF for aberto.

**Layout da página:** Selecione o tipo de layout de página para o documento PDF.

**Ampliação:** Escolha a ampliação predefinida para a visualização inicial do documento PDF ou selecione um valor personalizado. A escolha de uma configuração padrão indica que a ampliação padrão do Acrobat será usada.

**Abrir no número da página:** Especifique o número de página para o qual o PDF será aberto.

### Opções da janela {#window-options}

Ative essas opções para especificar como a janela é dimensionada e exibida.

**Redimensionar Janela Para Página Inicial:** Redimensiona a janela do Acrobat para o tamanho da página inicial.

**Centralizar janela na tela:** Abre a janela no centro da tela.

**Abrir no modo de tela cheia:** Abre a janela no modo de tela cheia.

**Mostrar:** Exibe o título do documento ou nome do arquivo na janela.

### Opções da interface do usuário {#user-interface-options}

Ative estas opções para especificar a aparência da janela:

**Ocultar barra de menus:** Oculta a barra de menus no documento PDF.

**Ocultar barras de ferramentas:** Oculta as barras de ferramentas no documento PDF.

**Ocultar controles de janela:** Oculta os controles da janela no documento PDF.

## Configurações de vídeos Flash para PDF {#flash-videos-to-pdf-settings}

O Gerador de PDF suporta a capacidade de enviar um vídeo para o Adobe Flash (arquivo SWF ou FLV) e criar um arquivo PDF com um vídeo para o Adobe Flash incorporado. Essa conversão não exige que o Adobe Flash Player seja instalado no servidor de formulários. Para obter instruções sobre como acessar essa opção, consulte [Criar ou editar configurações](configuring-file-type-settings.md#create-or-edit-file-type-settings)de tipo de arquivo.

**Extensões de nome de arquivo:** lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

## Configurações do XPS para PDF {#xps-to-pdf-settings}

A Especificação de papel XML (XPS) é usada na máquina de impressão do Windows. Este é um formato Microsoft e pode ser criado a partir de qualquer aplicativo do Microsoft Office. Formulários AEM fornecem a capacidade de converter arquivos XPS em PDF.

**Extensões de nome de arquivo:** Uma lista separada por vírgulas de todas as extensões de nome de arquivo XPS que podem ser convertidas. Atualmente, há um formato: .xps.

## Configurações do otimizador de PDF {#pdf-optimizer-settings}

O Gerador de PDF oferece suporte à capacidade de reduzir o tamanho dos arquivos PDF. Se você usar todas essas configurações ou apenas algumas depende de como pretende usar os arquivos e das propriedades essenciais que um arquivo deve ter. Na maioria dos casos, as configurações padrão são apropriadas para eficiência máxima - economizando espaço removendo fontes incorporadas, compactando imagens e removendo itens dos arquivos que não são mais necessários.

>[!NOTE]
>
>Otimizar um documento assinado digitalmente remove e invalida as assinaturas digitais.

Para obter instruções sobre como acessar essa configuração, consulte [Criar ou editar configurações](configuring-file-type-settings.md#create-or-edit-file-type-settings)de tipo de arquivo.

**Versão PDF do Público alvo:** Especifica a versão do Acrobat com a qual o PDF é compatível.

### Fontes {#fonts}

1. Selecione **Fontes.**
1. Selecione uma destas opções:

   **Desincorporar todas as fontes:** Desincorpora todas as fontes incorporadas.

   **Não desincorpore nenhuma fonte:** Não desincorpora nenhuma fonte.

   **Desincorporar algumas fontes:** Desincorpora somente as fontes especificadas. Siga estas etapas para especificar as fontes que deseja desincorporar:

   * Se necessário, selecione um diretório de fontes diferente no menu suspenso Fonte **** fonte. Este menu suspenso lista diretórios de fontes especificados em **Início > Configurações > Sistema principal > Configurações** principais.
   * Selecione uma ou mais fontes na lista Fontes **** disponíveis e clique em **Adicionar**. Essas fontes são adicionadas às **Fontes para a lista Não incorporada** .
   * Se desejar desincorporar algumas fontes que não existem no servidor de formulários, digite os nomes dessas fontes na caixa **Adicionar fontes a serem desincorporadas** . Clique em **Adicionar**.
   >[!NOTE]
   >
   >*Se desejar desincorporar algumas fontes cujos subconjuntos estão incorporados ao documento, coloque o sinal + no prefixo do nome da fonte. Por exemplo, &quot;+Helvetica&quot;.*

1. Se desejar incorporar apenas os subconjuntos em uso das fontes incorporadas, selecione **Subconjunto de todas as fontes** incorporadas.

   >[!NOTE]
   >
   >*Se você estiver usando essa opção em combinação com a opção **Desincorporar algumas fontes**, as fontes em ****Adicionar fontes à lista não incorporada ainda serão completamente desincorporadas.*

   >[!NOTE]
   >
   >*O subconjunto de fontes é a técnica de incorporar apenas uma parte de uma fonte. Um subconjunto de fontes contém apenas os caracteres usados no documento.*

### Transparência {#transparency}

Se o documento PDF incluir arte-final que contenha transparência, você poderá usar as configurações do Otimizador de PDF para nivelar a transparência e reduzir o tamanho do arquivo.

>[!NOTE]
>
>Se o Acrobat 4.0 e posterior for selecionado como a versão PDF do Público alvo, todos os objetos transparentes serão nivelados. Para outras versões de PDF de Público alvo, a transparência é suportada e você pode definir as configurações de transparência.

Selecione **Transparência** para definir as configurações de transparência ao otimizar documentos PDF.

**Nível** de transparência Especifica a quantidade de informações vetoriais que serão preservadas. Configurações mais altas preservam mais objetos de vetor, enquanto configurações mais baixas rasterizam mais objetos de vetor; as configurações intermediárias preservam áreas simples em forma de vetor e rasterizam áreas complexas. Selecione a configuração mais baixa para rasterizar toda a arte-final.

>[!NOTE]
>
>A quantidade de rasterização que ocorre depende da complexidade da página e dos tipos de objetos sobrepostos.

**Resolução de linha e texto** para a qual todos os objetos, incluindo imagens, arte-final vetorial, texto e gradientes, são rasterizados. Os valores suportados são de 1 pixel por polegada (ppi) a 9600 ppi.

>[!NOTE]
>
>A resolução de Arte de linha e Texto deve geralmente ser definida como 600 a 1200 ppi para fornecer rasterização de alta qualidade, especialmente em tipos serif ou de tamanho pequeno.

**Resolução de gradiente e malhas** em que o gradiente e as malhas são rasterizados. Os valores suportados são de 1 ppi a 1200 ppi.

>[!NOTE]
>
>A resolução de gradiente e malha deve geralmente ser definida como 150 a 300 ppi, pois a qualidade dos gradientes, sombras e penas não melhora com resoluções mais altas, mas o tempo de impressão e o tamanho do arquivo aumentam.

**Converter todo o texto em contornos** Converte todos os objetos de tipo (tipo de ponto, tipo de área e tipo de caminho) em contornos e descarta todas as informações de glifo de tipo nas páginas que contêm transparência. Essa opção garante que a largura do texto permaneça consistente durante o nivelamento. Observe que ativar essa opção fará com que fontes pequenas apareçam ligeiramente mais espessas quando visualizadas no Acrobat ou impressas em impressoras de mesa de baixa resolução. Isso não afeta a qualidade do tipo impresso em impressoras de alta resolução ou fotocompositoras.

**Converter todos os traçados em contornos** Converte todos os traçados em caminhos preenchidos simples nas páginas que contêm transparência. Essa opção garante que a largura dos traçados permaneça consistente durante o nivelamento. Observe que ativar essa opção faz com que os traçados finos apareçam ligeiramente mais espessos e podem degradar o desempenho do nivelamento.

**Recortar regiões** complexas garante que os limites entre a arte-final vetorial e a arte-final rasterizada caiam ao longo de caminhos de objetos. Esta opção reduz a sutura de artefatos que resultam quando parte de um registro] &quot;>

>[!NOTE]
>
>Alguns drivers de impressão processam rasterização e arte vetorial de forma diferente, às vezes resultando em pontos coloridos. Você pode minimizar os problemas de costura desabilitando algumas configurações de gerenciamento de cores específicas do driver de impressão. Essas configurações variam de acordo com cada impressora; portanto, consulte a documentação que acompanha a impressora para obter detalhes.

Preservar superimposição: Mescla a cor da arte transparente com a cor do plano de fundo para criar um efeito de superimposição.

A tabela a seguir mostra os tipos comuns de impressoras e sua resolução medida em dpi, sua resolução de tela padrão medida em linhas por polegada (lpi) e uma resolução de reamostragem para imagens medidas em pixels por polegada (ppi). Por exemplo, se você estivesse imprimindo em uma impressora a laser de 600 dpi, insira 170 para obter a resolução na qual as imagens devem ser reamostradas.

**Imagens** Selecione Imagens para especificar as opções de compactação e reamostragem para imagens coloridas, em tons de cinza e monocromáticas. Talvez você queira experimentar essas opções para encontrar um equilíbrio apropriado entre o tamanho do arquivo e a qualidade da imagem.A configuração de resolução para imagens coloridas e em tons de cinza deve ser de 1,5 a 2 vezes a regra de tela de linha na qual o arquivo será impresso. A resolução para imagens monocromáticas deve ser a mesma do dispositivo de saída, mas lembre-se de que salvar uma imagem monocromática em uma resolução superior a 1500 dpi aumenta o tamanho do arquivo sem melhorar visivelmente a qualidade da imagem. Imagens que serão ampliadas, como mapas, podem exigir resoluções mais altas.

>[!NOTE]
>
>A reamostragem de imagens monocromáticas pode ter resultados de visualização inesperados, como sem exibição de imagem. Se isso acontecer, desative a redefinição da amostra e converta o arquivo novamente. Esse problema provavelmente ocorrerá com a subamostragem e, provavelmente, com a diminuição da resolução bicúbica.

<table>
 <tbody>
  <tr>
   <th><p><strong>Resolução da impressora</strong></p> </th>
   <th><p><strong>Tela de linha padrão</strong></p> </th>
   <th><p><strong>Resolução da imagem</strong></p> </th>
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

#### Descartar objetos {#discard-objects}

* Selecione **Descartar objetos** para especificar objetos a serem removidos do PDF e para otimizar linhas curvas em desenhos CAD.
* **Descartar Todas As Ações** De Envio, Importação E Redefinição De Formulários: Desativa todas as ações relacionadas ao envio ou importação de dados de formulário e redefine os campos de formulário. Essa opção retém objetos de formulário aos quais as ações estão vinculadas.
* **Descartar todas as ações** do JavaScript: Remove do PDF todas as ações que usam JavaScript.
* **Descartar miniaturas** de página incorporadas: Remove miniaturas de página incorporadas. Essa opção é útil para documentos grandes, que podem levar muito tempo para desenhar miniaturas de página depois de clicar no botão Páginas.
* **Converter linhas suaves em curvas**: Reduz o número de pontos de controle usados para criar curvas em desenhos CAD, o que resulta em arquivos PDF menores e renderização na tela mais rápida.
* **Descartar configurações** de impressão incorporadas: Remove as configurações de impressão incorporadas, como o dimensionamento de página e o modo duplex, do documento.
* **Descartar marcadores**: Remove todos os marcadores do documento.
* **Nivelar campos** de formulário: Torna os campos de formulário inutilizáveis sem alteração na aparência. Os dados do formulário são unidos à página para se tornarem conteúdo da página.
* **Descartar todas as imagens** alternativas: Remove todas as versões de uma imagem, exceto a versão destinada à visualização na tela. Alguns PDFs incluem várias versões da mesma imagem para fins diferentes, como visualização na tela de baixa resolução e impressão de alta resolução.
* **Descartar tags** de Documento: Remove as tags do documento, o que também remove a acessibilidade e os recursos de refluxo do texto.
* **Detectar E Mesclar Fragmentos** De Imagem: Procura imagens ou máscaras que são fragmentadas em fatias finas e tenta mesclar as fatias em uma única imagem ou máscara.
* **Descartar índice** de pesquisa incorporado: Remove os índices de pesquisa incorporados, o que reduz o tamanho do arquivo.

#### Descartar dados do usuário {#discard-user-data}

Selecione **Descartar dados** do usuário para remover quaisquer informações pessoais que você não deseja distribuir ou compartilhar com outros usuários.

* **Descarte Todos Os Comentários, Formulários E Multimídia**: Remove todos os comentários, formulários, campos de formulário e multimídia do PDF.
* **Descartar todos os dados** do objeto: Remove todos os objetos do PDF.
* **Descartar referências** cruzadas externas: Remove links para outros documentos. Links que saltam para outros locais no PDF não são removidos.
* **Descarte O Conteúdo Oculto Da Camada E Nivele As Camadas** Visíveis: Diminui o tamanho do arquivo. O documento otimizado se parece com o PDF original, mas não contém informações de camada.
* **Descartar Informações E Metadados** Do Documento: Remove informações no dicionário de informações do documento e todos os fluxos de metadados. (Use o comando Salvar como para restaurar fluxos de metadados para uma cópia do PDF.)
* **Descartar anexos** de arquivo: Remove todos os anexos de arquivo, incluindo anexos adicionados ao PDF como comentários. (O Otimizador de PDF não otimiza os arquivos anexados.)
* **Descartar Dados Privados De Outros Aplicativos**: Remove informações de um documento PDF que é útil somente para o aplicativo que criou o documento. Essa configuração não afeta a funcionalidade do PDF, mas diminui o tamanho do arquivo.

### Limpar {#clean-up}

Selecione **Limpar** para remover itens desnecessários do documento.
Esses itens incluem elementos que são obsoletos ou desnecessários para o uso pretendido do documento. A remoção de certos elementos pode afetar seriamente a funcionalidade do PDF. Por padrão, somente os elementos que não afetam a funcionalidade são selecionados. Se não tiver certeza das implicações da remoção de outras opções, use as seleções padrão.

**Compactação**

Selecione uma das seguintes opções de compactação Flate no menu suspenso:

* Compactar o arquivo inteiro
* Compactar estrutura do documento
* Remover compactação
* Deixe a compactação inalterada

**Use Flate Para Codificar Fluxos Não Codificados**: Aplica a compactação Flate a todos os fluxos que não estão codificados.

**Descartar marcadores** inválidos: Remove marcadores que apontam para páginas no documento que são excluídas.

**Descartar Destinos Nomeados Não Referenciados**: Remove os destinos nomeados que não estão sendo referenciados internamente do documento PDF. Essa opção não verifica se há links de outros arquivos PDF ou sites.

**Otimize O PDF Para Visualização** Rápida Na Web: Reestrutura um documento PDF para download de página por vez (serviço de bytes) de servidores da Web.

**Em Fluxos Que Usam Codificação LZW, Use Flate Em Vez**: Aplica a compactação Flate a todos os fluxos de conteúdo e imagens que usam a codificação LZW.

**Descartar links** inválidos: Remove links que levam a destinos inválidos.

**Otimizar conteúdo** da página: Converte todos os caracteres de fim de linha em caracteres de espaço, o que melhora a compactação Flate.

## Configurações do Microsoft Excel (somente Windows) {#microsoft-excel-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Excel são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)de tipo de arquivo.

**Experimente o OpenOffice como Conversor** de fallback: Quando essa opção é selecionada e uma conversão usando o Microsoft Excel falha ou atinge o limite de tempo limite especificado, o Gerador de PDF tenta a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Extensões** de nome de arquivo: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `xls,xlsx`. Não inclua um período antes ou um espaço entre as extensões.

**Criar arquivo** compatível com PDF/A-1a: Força o uso da configuração PDF RGB do Adobe PDF PDF PDF PDF PDF/A-1b:2005.

**Adicionar marcadores ao Adobe PDF**: Converte nomes de planilhas do Excel em marcadores. Esta opção está selecionada por padrão.

**Ajustar Planilha A Uma Única Página**: Reduz o tamanho do texto para ajustar a planilha em uma única página.

**Converter toda a pasta de trabalho**: Converte todas as planilhas no arquivo Excel. Se essa opção não estiver selecionada, somente a página atual será convertida.

**Executar macros automaticamente**: Executa todas as macros no documento do Excel (como uma macro que insere a hora atual) antes de converter o documento.

**Converter informações** do Documento: Adiciona propriedades de documento PDF com base nas informações do documento no arquivo de origem. Isso inclui informações como título do documento, autor, assunto e palavras-chave.

**Adicionar links ao Adobe PDF**: Converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**Anexar arquivo de origem ao Adobe PDF**: Quando essa opção é selecionada, a planilha original do Excel é inserida como um anexo dentro do documento PDF gerado.

**Ative A Acessibilidade E O Refluxo Com Adobe PDF** Marcado: Incorpora tags no documento PDF para permitir a acessibilidade e o refluxo.

**Lista De Adições Do Excel A Carregar**: Por padrão (por motivos de segurança), nenhum suplemento do Excel é executado quando um arquivo do Excel é convertido em PDF. Para permitir que determinados suplementos do Excel sejam executados durante a conversão, forneça uma lista separada por vírgulas dos nomes dos suplementos.

**Lista De Planilhas Para Converter**: Quando essa caixa estiver vazia, todas as planilhas na planilha do Excel serão incluídas no PDF gerado. Para converter seletivamente um subconjunto das planilhas, forneça uma lista separada por vírgulas de nomes de planilhas.

## Configurações do Microsoft PowerPoint (somente Windows) {#microsoft-powerpoint-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft PowerPoint são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)de tipo de arquivo.

**[!UICONTROL Experimente o OpenOffice como Conversor]** de fallback: Quando essa opção for selecionada e uma conversão usando o Microsoft PowerPoint falhar ou atingir o limite de tempo limite especificado, o Gerador de PDF tentará a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões]** de nome de arquivo: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é ppt,pptx. Não inclua um período antes ou um espaço entre as extensões.

**[!UICONTROL Converter informações]** do Documento: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar marcadores ao Adobe PDF]**: Converte títulos do PowerPoint em marcadores. Esta opção está selecionada por padrão.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como um anexo. Por padrão, essa opção não é selecionada.

**[!UICONTROL Ative A Acessibilidade E O Refluxo Com Adobe PDF]** Marcado: Incorpora tags ao arquivo PDF. Por padrão, essa opção não é selecionada.

**[!UICONTROL Converta Multimídia em Multimídia]** PDF: Converte multimídia em multimídia PDF, onde possível. Esta opção está selecionada por padrão.

**[!UICONTROL Converter notas]** do locutor: Converte notas do palestrante em PDF.

**[!UICONTROL Executar macros automaticamente]**: Executa todas as macros no documento do PowerPoint (como uma macro que insere a hora atual) antes de converter o documento.

**[!UICONTROL Layout de PDF com base nas configurações]** da impressora do PowerPoint: Usa as configurações de impressora do PowerPoint para dispor o documento PDF.

**[!UICONTROL Adicionar links ao Adobe PDF]**: Preserva os links existentes quando o arquivo é convertido. A aparência dos links geralmente não é alterada. Os links podem ser criados somente se a opção Ativar acessibilidade também estiver selecionada. Por padrão, essa opção não é selecionada.

**[!UICONTROL Salve Transições De Slides No Adobe PDF]**: Converte transições de slide. Esta opção está selecionada por padrão.

**[!UICONTROL Salvar animações no Adobe PDF]**: Salva animações convertidas no arquivo PDF.

**[!UICONTROL Converter slides ocultos em páginas]** PDF: Converte slides ocultos.

**[!UICONTROL Criar arquivo]** compatível com PDF/A-1a: Força o uso da configuração PDF RGB do Adobe PDF PDF PDF PDF PDF/A-1b:2005. Alguns recursos do PowerPoint não são convertidos ao produzir um arquivo PDF. Se uma transição do PowerPoint não tiver uma transição equivalente no Acrobat, uma transição semelhante será substituída. Se vários efeitos de animação estiverem no mesmo slide, um único efeito será usado. As transições de página e os marcadores são convertidos.

## Configurações do Microsoft Project (somente Windows) {#microsoft-project-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Project são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)de tipo de arquivo.

1. **[!UICONTROL Extensões de nome de arquivo:]** Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `mpp`. Não inclua um período antes ou um espaço entre as extensões.

1. **[!UICONTROL Converter informações]** do Documento: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.
1. **[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como um anexo.
1. **[!UICONTROL Criar arquivo]** compatível com PDF/A-1a: Força o uso da configuração PDF RGB do Adobe PDF PDF PDF PDF PDF/A-1b:2005.
1. **[!UICONTROL Executar macros automaticamente]**: Executa todas as macros no documento do Microsoft Project (como uma macro que insere a hora atual) antes de converter o documento.

## Configurações do Microsoft Word (somente Windows) {#microsoft-word-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Word são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)de tipo de arquivo.

**[!UICONTROL Experimente o OpenOffice como Conversor]** de fallback: Quando essa opção é selecionada e uma conversão usando o Microsoft Word falha ou atinge o limite de tempo limite especificado, o Gerador de PDF tenta a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões]** de nome de arquivo: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `doc,docx,rtf,txt`. Não inclua um período antes ou um espaço entre as extensões.

**[!UICONTROL Converter informações]** do Documento: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar marcadores ao Adobe PDF]**: Converte cabeçalhos em marcadores. Esta opção está selecionada por padrão.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como um anexo.

**[!UICONTROL Converter Referências Cruzadas E Sumário Em Links]**: Converte todas as referências cruzadas e entradas de sumário em links. Esta opção está selecionada por padrão.

**[!UICONTROL Ative A Acessibilidade E O Refluxo Com Adobe PDF]** Marcado: Incorpora tags ao arquivo PDF. Esta opção está selecionada por padrão.

**[!UICONTROL Criar arquivo]** compatível com PDF/A-1a: Se selecionada, força a configuração PDF RGB do PDF PDF PDF PDF/A-1b:2005 a ser usada.

**[!UICONTROL Executar macros automaticamente]**: Executa todas as macros no documento do Word (como uma macro que insere a hora atual) antes de converter o documento.

**[!UICONTROL Preservar marcação de Documento no Adobe PDF]**: Converte a marcação no documento do Word em anotações no arquivo PDF.

**[!UICONTROL Adicionar links ao Adobe PDF]**: Converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**[!UICONTROL Converter Links]** De Nota De Rodapé E De Nota De Fim: Cria links a partir das citações de nota de rodapé e de nota de fim para notas no documento PDF.

**[!UICONTROL Converter comentários exibidos em notas no Adobe PDF]**: Converte comentários no documento do Word em notas de texto no documento PDF.

**[!UICONTROL Ativar Marcação]** avançada: Adiciona tags avançadas para melhorar a acessibilidade.

**[!UICONTROL Converter todos os estilos em marcadores]**: Converte todos os estilos no documento do Word em marcadores no documento PDF.

**[!UICONTROL Estilos com Níveis]**: Especifica quais estilos no documento do Word são convertidos em marcadores no documento PDF. Especifica também o nível dos marcadores. Para usar esse recurso, desmarque a opção **[!UICONTROL Converter todos os estilos em marcadores]** e especifique os nomes dos estilos no seguinte formato:

styleName1=level1[,styleName2=level2...]

Se um nome de estilo do Microsoft Word incluir uma vírgula (,) ou sinal igual (=), preceda os caracteres especiais com o caractere de escape (&quot;\_). Por exemplo, especifique um estilo chamado &quot;Cabeçalho, 1&quot; como Cabeçalho\, 1.

## Configurações do Microsoft Visio (somente Windows) {#visio}

**Converter informações** do Documento: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão. Essa opção é ativada por padrão.

**Adicionar links ao Adobe PDF**: Preserva todos os links. Esta opção está selecionada por padrão.

**Adicionar marcadores ao Adobe PDF**: Converte cabeçalhos em marcadores. Esta opção está selecionada por padrão.

**Anexar arquivo de origem ao Adobe PDF**: Adiciona o arquivo de origem ao arquivo PDF como um anexo.

**Sempre achatar camadas no Adobe PDF**: Nivela todas as camadas do Visio.

**Converter todas as páginas**: Converte todas as páginas do arquivo do Visio.

**Abra O Painel Camadas Quando Visualizado No Adobe Acrobat**: Se as camadas do Visio não estiverem niveladas, abre uma janela onde é possível especificar as camadas preservadas no arquivo PDF quando abertas com o Acrobat. Esta opção está selecionada por padrão.

**Criar arquivo** compatível com PDF/A-1b: Força o uso da Configuração de PDF da Adobe PDF PDF PDF/A-1b:2005 (RGB).

**Converter comentários em comentários** do Adobe PDF: Converte notas do Visio em comentários em PDF.

## Configurações do Microsoft Publisher (somente Windows) {#microsoft-publisher-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Publisher são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#main-pars-heading-0)de tipo de arquivo.

**[!UICONTROL Extensões]** de nome de arquivo: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `pub`. Não inclua um período antes ou um espaço entre as extensões.

## Configurações do AutoCAD (somente Windows) {#autocad-settings-windows-only}

Essas opções determinam como os arquivos AutoCAD são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)de tipo de arquivo.

**[!UICONTROL Extensões]** de nome de arquivo: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `dwg`. Não inclua um período antes ou um espaço entre as extensões.

**[!UICONTROL Converter informações]** do Documento: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar marcadores ao Adobe PDF]**: Converte cabeçalhos em marcadores.

**[!UICONTROL Sempre achatar camadas no Adobe PDF]**: Nivela todas as camadas do AutoCAD.

**[!UICONTROL Abra O Painel Camadas Quando Visualizado No Adobe Acrobat]**: Mostra a estrutura das camadas quando o PDF é aberto no Acrobat.

**[!UICONTROL Criar arquivo]** compatível com PDF/E-1: Cria um arquivo compatível com PDF/E-1. O PDF/E é um padrão ISO para troca de documentação técnica e de engenharia. Para obter mais informações sobre PDF/E-1, consulte [Adobe e padrões](https://www.adobe.com/enterprise/standards/index.html)do setor.

**[!UICONTROL Converter todos os layouts]**: Inclui todos os layouts no PDF.

**[!UICONTROL Converter espaço modelo em 3D]**: Quando selecionado, o layout do espaço do modelo é convertido em uma anotação 3D no PDF.

**[!UICONTROL Adicionar links ao Adobe PDF]**: Se selecionado, preserva todos os links.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como um anexo.

**[!UICONTROL Criar arquivo]** compatível com PDF/A-1b: Força o uso da configuração PDF PDF PDF/A-1b da Adobe.

**[!UICONTROL Converter todas as camadas]**: Por padrão, o Gerador de PDF converte somente a camada padrão de arquivos AutoCAD em PDF em vez de todas as camadas no arquivo. Selecione essa opção para converter todas as camadas do arquivo.

**[!UICONTROL Incorporar informações]** de escala: Preserva informações de escala de desenho.

**[!UICONTROL Converter layout]** atual: Inclui apenas o layout atual no PDF.

**[!UICONTROL Lista De Layouts Do AutoCAD Para Converter]**: Um desenho do AutoCAD pode ter vários layouts. Quando essa caixa estiver vazia, todos os layouts no desenho do AutoCAD serão incluídos no documento PDF gerado. Para converter seletivamente um subconjunto dos layouts, forneça uma lista separada por vírgulas de nomes de layout.

## Configurações do OpenOffice {#openoffice-settings}

Essas opções determinam como os arquivos OpenOffice são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações](/help/forms/using/admin-help/configuring-file-type-settings1.md#create-or-edit-file-type-settings)de tipo de arquivo.

**Tente o PDFMaker como conversor** de fallback: Quando essa opção é selecionada e uma conversão usando o OpenOffice falha ou atinge o limite de tempo limite especificado, o Gerador de PDF tenta a conversão usando o PDFMaker. Se a conversão que usa o PDFMaker falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Extensões** de nome de arquivo: Especifique as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Não inclua um período antes ou um espaço entre as extensões.

**Intervalo**: Converta todas as páginas ou especifique páginas específicas ou um intervalo de páginas. Se um intervalo de páginas não estiver definido, todas as páginas serão convertidas. Para exportar um intervalo de páginas, use o formato 3-6. Para exportar páginas únicas, use o formato 7;9;11. É possível exportar uma combinação de intervalos de páginas e páginas únicas usando um formato como 3-6;8;10;12.

**Orientação** da página: Somente para arquivos de texto sem formatação, selecione retrato ou paisagem para o documento PDF convertido.

**Imagens**: Configure como as imagens são convertidas. As imagens EPS com pré-visualizações incorporadas são exportadas somente como pré-visualizações. As imagens EPS sem pré-visualizações incorporadas são exportadas como espaços reservados vazios. Com a compactação sem perdas de imagens, todos os pixels são preservados. Com a compactação de imagens JPEG e um nível de alta qualidade, quase todos os pixels são preservados. Com um nível de qualidade baixa, alguns pixels se perdem e artefatos são introduzidos, mas o tamanho dos arquivos é reduzido.

**Geral**: Ative as opções para converter um PDF marcado ou exportar notas de documento do Writer e do FormCalc, Imprimir efeitos de transição de slides ou páginas em branco para o PDF. Quando as tags são exportadas, o tamanho do arquivo pode aumentar em grandes quantidades. Algumas tags exportadas são sumários, hiperlinks e controles.

Também é possível especificar como os formulários são submetidos. As opções são XML, FDF, PDF ou HTML. Essa configuração substitui a propriedade de URL do controle definida no documento. Somente uma configuração comum pode ser selecionada para o documento PDF:

* PDF (envia o documento inteiro)
* FDF (envia o conteúdo do controle)
* HTML
* XML

**PDF** marcado: Permite a criação de PDF marcado a partir de documentos do OpenOffice. O PDF marcado contém informações sobre a estrutura do conteúdo do documento. Isso pode ajudar a exibir o documento em dispositivos com telas diferentes e ao usar o software de leitor de tela. Também ajuda o software de acessibilidade a executar várias operações úteis com o documento PDF, como ler em voz alta o conteúdo do documento PDF.

**Exportar notas**: Converte as notas em documentos do OpenOffice em notas no documento PDF gerado.

**Usar efeitos** de Transição: Converte os efeitos de transição de slide nas apresentações do OpenOffice em efeitos de transição de PDF correspondentes.

**Enviar Formulários No Formato**: Cria um formulário PDF que pode ser preenchido e impresso pelo usuário do documento PDF.

**Exportar páginas** em branco automaticamente inseridas: Quando essa opção é selecionada, as páginas em branco inseridas automaticamente são incluídas no documento PDF gerado. Isso é útil se você estiver imprimindo um documento PDF nos lados do duplo. Por exemplo, um livro pode ser configurado para que a primeira página do capítulo sempre seja start em uma página ímpar. Se o capítulo anterior terminar em uma página ímpar, o OpenOffice inserirá uma página par em branco. Essa opção controla se a página par deve ser incluída no PDF gerado.

## Outras configurações do aplicativo (somente Windows) {#other-applications-settings-windows-only}

Não é possível alterar as configurações de outros aplicativos por meio do console de administração; eles exibem as extensões de nome de arquivo para os tipos de arquivo suportados. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html)de tipo de arquivo.

* Corel WordPerfect: `wpd`
* Adobe PageMaker: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

O suporte para esses tipos de arquivos pode precisar ser personalizado. Para obter mais informações, consulte &quot;Adicionar suporte para formatos de arquivo nativos adicionais&quot; em [Programação com formulários](https://www.adobe.com/go/learn_aemforms_programming_62)AEM.

Para obter ajuda sobre como configurar uma impressora de rede PDFG, consulte [Configuração de uma impressora de rede PDFG (somente Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
