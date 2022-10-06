---
title: Definição das configurações de tipo de arquivo
seo-title: Configuring file type settings
description: Saiba como definir configurações de tipo de arquivo.
seo-description: Learn how to configure file type settings.
uuid: ab037659-c6ff-4de9-9417-f5a6fc8122cb
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ab19b248-8931-4cf6-b6a5-fb7b067c4a49
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '6158'
ht-degree: 2%

---

# Definição das configurações de tipo de arquivo {#configuring-file-type-settings}

No PDF Generator, você pode configurar as configurações do aplicativo para os tipos de arquivos suportados. No Windows, você pode configurar as configurações do aplicativo para cada tipo de arquivo suportado. No UNIX e Linux, você pode configurar as configurações do aplicativo para HTML para PDF e OpenOffice.

Na página Configurações de tipo de arquivo , é possível executar as seguintes tarefas:

* [Criar ou editar uma configuração de Tipo de arquivo](#create-or-edit-file-type-settings)
* Especificar quais configurações de tipo de arquivo usar por padrão (consulte [Importação e exportação de arquivos de configuração do PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Alterar as configurações padrão](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Habilitar o suporte ao PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Excluir uma configuração de Tipo de arquivo](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>As configurações de tipo de arquivo não estão disponíveis para os conversores de fallback, como Acrobat para conversão do HTML para o PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Criar ou editar configurações de Tipo de arquivo {#create-or-edit-file-type-settings}

Crie ou edite uma configuração de tipo de arquivo para especificar como o aplicativo lida com a conversão de tipos de arquivo suportados. No Windows, você pode configurar as configurações do aplicativo para cada tipo de arquivo suportado. No UNIX e Linux, você pode configurar as configurações do aplicativo para HTML para PDF e OpenOffice.

1. No console de administração, clique em **[!UICONTROL Serviços]** > **[!UICONTROL Gerador de PDF]** > **[!UICONTROL Configurações de tipo de arquivo]**.
1. Clique em New ou clique no nome de uma configuração.
1. Na caixa Extensões de nome de arquivo, digite as extensões de nome de arquivo, separadas por vírgulas, para tipos de arquivo aceitos para esse aplicativo. Não inclua o período antes ou um espaço entre as extensões. O padrão é `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para usar o reconhecimento de código óptico (OCR) do texto em gráficos ou imagens, selecione Usar OCR e defina as seguintes opções:

**Idioma Principal do OCR:** O idioma usado pelo mecanismo OCR para identificar os caracteres. O padrão é inglês (EUA).

**Estilo de saída do PDF:** Selecione Imagem pesquisável para ter uma imagem de bitmap das páginas em primeiro plano e o texto digitalizado em uma camada invisível abaixo. A aparência da página não muda, mas o texto se torna selecionável e legível. Selecione Texto e gráficos formatados para reconstruir a página original usando texto, fontes, imagens e outros elementos gráficos reconhecidos. O padrão é Imagem pesquisável (Exata).

**Reduzir a amostra de imagens:** Diminui o número de pixels em cores, tons de cinza e imagens monocromáticas. A amostragem de imagens digitalizadas é realizada após a conclusão do OCR. O padrão é Menor (600 dpi). Essa opção não estará disponível se você definir o estilo de saída PDF para Imagem pesquisável (Exata).

1. Preencha as informações necessárias nestas seções:

[Importação e exportação de arquivos de configuração do PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Configurações de exportação do Adobe PDF (somente Windows)](#adobe-pdf-export-settings-windows-only)

[configurações HTML para PDF](#html-to-pdf-settings)

[Vídeos do Flash para configurações do PDF](#flash-videos-to-pdf-settings)

[Configurações XPS para PDF](#xps-to-pdf-settings)

[Configurações do PDF Otimizer](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Configurações do Microsoft Excel (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Configurações do Microsoft PowerPoint (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Configurações do Microsoft Project (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Configurações do Microsoft Word (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Configurações do Microsoft Visio (somente Windows)](#visio)

[Configurações do Microsoft Publisher (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[Configurações do AutoCAD (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[Definições do OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[Configurações de outros aplicativos (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Para acessar outra seção, clique no link na página da Web ou use a variável **[!UICONTROL Próximo]** ou **[!UICONTROL Anterior]** botões.

1. Após concluir todas as seções, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar como]** e forneça um nome para a configuração.

O suporte para vários tipos de arquivos pode ser personalizado. (Consulte &quot; [Adicionar suporte para formatos de arquivo nativos adicionais](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; in [Programação com formulários AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Alterar as configurações padrão {#change-the-default-settings}

Você pode alterar o valor padrão das configurações do Adobe PDF, configurações de segurança e configurações de tipo de arquivo que se aplicam a fontes recém-criadas. Alterar os padrões não afeta as configurações das fontes existentes.

1. No Console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF]**.
1. No **[!UICONTROL Configurações do Adobe PDF]**, **[!UICONTROL Configurações de tipo de arquivo]** ou **[!UICONTROL Configurações de segurança]** página, clique em **[!UICONTROL Definir configurações padrão]**.
1. Selecione as configurações padrão preferidas. Uma ou mais das seguintes configurações estão disponíveis na página Definir configurações padrão :

   **[!UICONTROL Configuração do Adobe PDF]**: O padrão original é Padrão (Acrobat 6).

   **[!UICONTROL Configurações de segurança]**: O padrão original é Sem segurança (Acrobat 5).

   **[!UICONTROL Configurações de tipo de arquivo]**: O padrão original é Padrão.

1. Clique em **[!UICONTROL Salvar]**.

## Excluir uma configuração de Tipo de arquivo {#delete-a-file-type-setting}

É possível excluir uma configuração de tipo de arquivo que não é mais usada.

1. No console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF> Configurações de tipo de arquivo]**.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. É possível selecionar várias fontes. As configurações que não têm uma caixa de seleção ao lado delas são sempre incluídas com PDF Generator e não podem ser excluídas.
1. Clique em **[!UICONTROL Excluir]** e, na página Confirmação de exclusão, clique em **[!UICONTROL Excluir]**.

## Configurações de imagem para PDF {#image-to-pdf-settings}

As opções a seguir determinam como os arquivos de imagem são convertidos em PDF. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensões de nome de arquivo:** Lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

**Tente Conversor de Fallback:** O PDF Generator pode usar Java™ ou Acrobat para converter arquivos de imagem em PDF. Quando essa opção é selecionada e uma conversão falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o método alternativo. Se um método alternativo falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

>[!NOTE]
>
>Arquivos JPEG 2000 só podem ser convertidos usando o Acrobat.

**Usar OCR:** Especifica se o OCR (reconhecimento ótico de caracteres) deve ser aplicado ao PDF. O software OCR permite pesquisar, corrigir e copiar o texto no PDF.

***observação **: O recurso PDF OCR (PDF pesquisável) é compatível somente no Microsoft Windows.*

**Idioma Principal do OCR:** Especifica o idioma a ser usado pelo mecanismo OCR para identificar os caracteres.

**Estilo de saída do PDF:** Determina o tipo de PDF a ser produzido. Todos os formatos aplicam OCR, fonte e reconhecimento de página às imagens de texto e as convertem em texto normal.

**Imagem pesquisável:** Garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original, a desenha conforme necessário e coloca uma camada de texto invisível sobre ela. A opção Reduzir amostra de imagens determina se a imagem terá resolução reduzida e em que extensão.

**Imagem pesquisável (Exata):** Garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original e coloca uma camada de texto invisível sobre ela. Recomendado para casos que exigem fidelidade máxima à imagem original.

**ClearScan:** Sintetiza uma nova fonte Tipo 3 que aproxima o original de perto e preserva o plano de fundo da página usando uma cópia de baixa resolução.

**Reduzir a amostra de imagens:** Diminui o número de pixels em cor, escala de cinza e imagens monocromáticas após a conclusão do OCR. Escolha o grau de amostragem decrescente a ser aplicado. As opções de número mais alto fazem menos downsampling, o que produz PDF de resolução mais alta.

## Configurações de exportação do Adobe PDF (somente Windows) {#adobe-pdf-export-settings-windows-only}

A configuração Exportar tipo de arquivo na seção de configurações de exportação do Adobe PDF é usada para converter um arquivo PDF para outro formato. O padrão é HTML 4.01 com folhas de estilos em cascata (CSS) 1.0 (*.htm, *.html).

Para obter instruções sobre como acessar essa configuração, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## configurações HTML para PDF {#html-to-pdf-settings}

As opções a seguir determinam como os arquivos HTML são convertidos em PDF. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Tente Conversor de Fallback:** O PDF Generator pode usar Java™ ou Acrobat para converter arquivos HTML para PDF. Quando essa opção é selecionada e uma conversão falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o método alternativo. Se um método alternativo falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Codificação padrão:** Define a codificação de entrada do texto do arquivo a partir de um menu de sistemas operacionais e alfabetos. Usa a seleção mostrada na opção Codificação padrão somente se o arquivo de origem do HTML não especificar um tipo de codificação.

**Forçar Codificação Selecionada:** Ignora qualquer codificação especificada no arquivo de origem do HTML e usa a seleção mostrada na opção Codificação padrão .

### Configurações de borda {#spidering-settings}

*Aranha* O verifica páginas da Web em busca de links para outras páginas da Web. Quando um link para outra página da Web é encontrado, a página de destino é buscada e incluída no documento do PDF que é gerado. Ative essas opções para definir o número de níveis a serem obtidos e convertidos em PDF:

**Obter Apenas Níveis X:** Spiders e converte páginas até uma profundidade do nível especificado a partir do URL da página base. Um valor de 1 converte somente o URL fornecido.

**Obter todo o site:** Converte o site inteiro, começando pelo URL fornecido.

**Fique No Mesmo Caminho:** Os links que apontam para páginas que não estão no mesmo caminho relativo do URL base não são convertidos durante a criação de spiders.

**Permaneça No Mesmo Servidor:** Os links que apontam para páginas em servidores diferentes não são convertidos durante a criação de spidering. Somente os links que apontam para o mesmo servidor como o URL especificado são convertidos.

### Configurações de conversão de página {#page-conversion-settings}

Ative essas opções para especificar como as páginas de HTML são convertidas. Com base no tamanho da página, os valores de largura, altura e margem se ajustam de acordo.

**Tamanho da página:** Escolha personalizado e especifique a largura e a altura, ou selecione dimensões predefinidas.

**Orientação:** Selecione retrato ou paisagem para o documento PDF convertido.

**Margens:** Especifica as margens (Superior, Inferior, Esquerda e Direita) no documento PDF gerado.

**Adicionar Marcadores Ao PDF:** Adiciona marcadores ao documento PDF.

**Habilitar PDF marcado:** Incorpora tags no documento PDF.

**Definir configurações da exibição inicial:** Permite configurar Opções de Documento, Opções de Janela e Opções de Interface do Usuário. Essas configurações determinam como o conteúdo é exibido inicialmente.

### Opções de documento {#document-options}

Ative essas opções para especificar como exibir o conteúdo, como exibir páginas no documento do PDF e como especificar o nível de ampliação:

**Mostrar:** Selecione os painéis a serem abertos no Acrobat quando o documento do PDF for aberto.

**Layout da página:** Selecione o tipo de layout de página para o documento PDF.

**Ampliação:** Escolha a ampliação predefinida para a exibição inicial do documento PDF ou selecione um valor personalizado. A escolha de uma configuração padrão indica que a ampliação padrão do Acrobat será usada.

**Abrir para número de página:** Especifique o número de página para o qual o PDF é aberto.

### Opções de Janela {#window-options}

Ative essas opções para especificar como a janela é dimensionada e exibida.

**Redimensionar Janela Para Página Inicial:** Redimensiona a janela Acrobat para o tamanho da página inicial.

**Centralizar janela na tela:** Abre a janela no centro da tela.

**Abra No Modo De Tela Cheia:** Abre a janela no modo de tela cheia.

**Mostrar:** Exibe o título do documento ou nome do arquivo na janela.

### Opções da interface do usuário {#user-interface-options}

Ative essas opções para especificar a aparência da janela:

**Ocultar barra de menus:** Oculta a barra de menu no documento PDF.

**Ocultar barras de ferramentas:** Oculta as barras de ferramentas no documento PDF.

**Ocultar controles da janela:** Oculta os controles da janela no documento PDF.

## Vídeos do Flash para configurações do PDF {#flash-videos-to-pdf-settings}

O PDF Generator oferece suporte à capacidade de enviar um vídeo para o Adobe Flash (arquivo SWF ou FLV) e criar um arquivo PDF com um vídeo para Adobe Flash integrado. Essa conversão não exige que o Adobe Flash Player seja instalado no servidor de formulários. Para obter instruções sobre como acessar essa opção, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensões de nome de arquivo:** Lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

## Configurações XPS para PDF {#xps-to-pdf-settings}

A Especificação de Papel XML (XPS) é usada na máquina de impressão do Windows. Este é um formato Microsoft e pode ser criado de qualquer aplicativo do Microsoft Office. AEM formulários fornece a capacidade de converter arquivos XPS PDF.

**Extensões de nome de arquivo:** Uma lista separada por vírgulas de todas as extensões de nome de arquivo XPS que podem ser convertidas. Atualmente, há um formato: .xps.

## Configurações do PDF Otimizer {#pdf-optimizer-settings}

O PDF Generator oferece suporte à capacidade de reduzir o tamanho dos arquivos PDF. Se você usar todas essas configurações ou apenas algumas depende de como pretende usar os arquivos e das propriedades essenciais que um arquivo deve ter. Na maioria dos casos, as configurações padrão são apropriadas para o máximo de eficiência - economizando espaço ao remover fontes incorporadas, compactar imagens e remover itens dos arquivos que não são mais necessários.

>[!NOTE]
>
>Otimizar um documento assinado digitalmente remove e invalida as assinaturas digitais.

Para obter instruções sobre como acessar essa configuração, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versão PDF do Target:** Especifica a versão do Acrobat com a qual o PDF é compatível.

### Fontes {#fonts}

1. Selecionar **Fontes.**
1. Selecione uma destas opções:

   **Desincorporar todas as fontes:** Desintegra todas as fontes incorporadas.

   **Não desincorpore nenhuma fonte:** Não desintegra nenhuma fonte.

   **Desincorporar algumas fontes:** Desintegra somente as fontes especificadas. Siga estas etapas para especificar as fontes que deseja desincorporar:

   * Se necessário, selecione um diretório de fontes diferente do **Fonte** menu suspenso. Esse menu suspenso lista os diretórios de fontes especificados em **Início > Configurações > Sistema principal > Configurações principais**.
   * Selecione uma ou mais fontes no **Fontes disponíveis** e clique em **Adicionar**. Essas fontes são adicionadas ao **Fontes a serem desincorporadas** lista.
   * Para desincorporar algumas fontes que não existem no servidor de formulários, insira os nomes dessas fontes no **Adicionar fontes para desincorporar** caixa. Clique em **Adicionar**.

   >[!NOTE]
   >
   >*Se você quiser desincorporar algumas fontes cujos subconjuntos estão incorporados no documento, coloque o nome da fonte no prefixo + sinal. Por exemplo, &quot;+Helvetica&quot;.*

1. Se quiser incorporar apenas os subconjuntos em uso das fontes incorporadas, selecione **Subconjunto todas as fontes incorporadas**.

   >[!NOTE]
   >
   >*Se estiver usando essa opção em combinação com **Desincorporar algumas fontes**, fontes no **Adicionar fontes para desincorporar**As listas ainda estão completamente desincorporadas.*

   >[!NOTE]
   >
   >*O subconjunto de fontes é a técnica de incorporar apenas uma parte de uma fonte. Um subconjunto de fontes contém apenas os caracteres usados no documento.*

### Transparência {#transparency}

Se o documento do PDF incluir arte-final que contenha transparência, você poderá usar as configurações do PDF Otimizer para nivelar a transparência e reduzir o tamanho do arquivo.

>[!NOTE]
>
>Se Acrobat 4.0 e posterior forem selecionadas como a versão do PDF do Target, todos os objetos transparentes serão nivelados. Para outras versões do Target PDF, a transparência é suportada e você pode definir as configurações de transparência.

Selecionar **Transparência** para configurar as configurações de transparência e otimizar documentos do PDF.

**Nível de transparência** Especifica a quantidade de informações de vetor que será preservada. As configurações mais altas preservam mais objetos vetoriais, enquanto as configurações mais baixas rasterizam mais objetos vetoriais; as configurações intermediárias preservam áreas simples em forma de vetor e rasterizam áreas complexas. Selecione a configuração mais baixa para rasterizar toda a arte-final.

>[!NOTE]
>
>A quantidade de rasterização que ocorre depende da complexidade da página e dos tipos de objetos sobrepostos.

**Arte da linha e texto** Resolução para a qual todos os objetos, incluindo imagens, arte vetorial, texto e gradientes são rasterizados. Os valores suportados são de 1 pixels por polegada (ppi) a 9600 ppi.

>[!NOTE]
>
>A resolução de Linha e Texto deve geralmente ser definida como 600-1200 ppi para fornecer rasterização de alta qualidade, especialmente no tipo serif ou de pequeno tamanho de ponto.

**Gradiente e malhas** Resolução a que o gradiente e as malhas são rasterizados. Os valores compatíveis são de 1 ppi a 1200 ppi.

>[!NOTE]
>
>A resolução de gradiente e malha deve geralmente ser definida como 150-300 ppi, pois a qualidade dos gradientes, sombras e penas não melhora com resoluções mais altas, mas o tempo de impressão e o tamanho do arquivo aumentam.

**Converter todo o texto em contornos** Converte todos os objetos do tipo (tipo de ponto, tipo de área e tipo de caminho) em contornos e descarta todas as informações de glifo do tipo nas páginas que contêm transparência. Essa opção garante que a largura do texto permaneça consistente durante o nivelamento. Observe que ativar essa opção fará com que as fontes pequenas pareçam ligeiramente mais espessas quando visualizadas no Acrobat ou impressas em impressoras de desktop de baixa resolução. Isso não afeta a qualidade do tipo impresso em impressoras ou imagens de alta resolução.

**Converter todos os traçados em contornos** Converte todos os traçados em caminhos preenchidos simples em páginas que contêm transparência. Essa opção garante que a largura dos traçados permaneça consistente durante o nivelamento. Observe que ativar essa opção faz com que os traçados finos pareçam um pouco mais grossos e podem degradar o desempenho do nivelamento.

**Clip de regiões complexas** Garante que os limites entre a arte-final vetorial e a arte-final rasterizada caiam ao longo de caminhos de objetos. Essa opção reduz os artefatos de costura que resultam quando parte de um log

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alguns drivers de impressão processam raster e arte vetorial de forma diferente, às vezes resultando em união de cores. Talvez seja possível minimizar os problemas de costura desativando algumas configurações de gerenciamento de cores específicas do driver de impressão. Essas configurações variam de acordo com cada impressora, portanto, consulte a documentação que acompanha a impressora para obter detalhes.

Preservar Superimposição: Combina a cor da arte transparente com a cor de plano de fundo para criar um efeito de superimposição.

A tabela a seguir mostra tipos comuns de impressoras e sua resolução medida em dpi, sua resolução de tela padrão medida em linhas por polegada (lpi) e uma resolução de reamostragem para imagens medidas em pixels por polegada (ppi). Por exemplo, se você estivesse imprimindo em uma impressora a laser de 600 dpi, seria digitado 170 para obter a resolução na qual as imagens seriam reclassificadas.

**Imagens** Selecione Imagens para especificar as opções de compactação e reamostragem para imagens coloridas, em tons de cinza e monocromáticas. Talvez você queira experimentar essas opções para encontrar um equilíbrio apropriado entre o tamanho do arquivo e a qualidade da imagem.A configuração de resolução para imagens coloridas e em tons de cinza deve ser de 1,5 a 2 vezes a regra de tela de linha na qual o arquivo será impresso. A resolução para imagens monocromáticas deve ser a mesma do dispositivo de saída, mas esteja ciente de que salvar uma imagem monocromática em uma resolução superior a 1500 dpi aumenta o tamanho do arquivo sem melhorar visivelmente a qualidade da imagem. Imagens que serão ampliadas, como mapas, podem exigir resoluções mais altas.

>[!NOTE]
>
>A reamostragem de imagens monocromáticas pode ter resultados de exibição inesperados, como sem exibição de imagem. Se isso acontecer, desative a reamostragem e converta o arquivo novamente. Esse problema provavelmente ocorrerá com a subamostragem e, menos provavelmente, com a desamostragem bicúbica.

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

#### Descartar objetos {#discard-objects}

* Selecionar **Descartar objetos** especificar objetos a serem removidos do PDF e otimizar linhas curvas em desenhos CAD.
* **Descartar Todas As Ações De Envio, Importação E Redefinição De Formulários**: Desativa todas as ações relacionadas ao envio ou importação de dados de formulário e redefine os campos de formulário. Essa opção retém objetos de formulário aos quais as ações estão vinculadas.
* **Descartar todas as ações do JavaScript**: Remove do PDF qualquer ação que usa JavaScript.
* **Descartar miniaturas de página incorporadas**: Remove as miniaturas de página incorporadas. Essa opção é útil para documentos grandes, que podem levar muito tempo para desenhar miniaturas de página depois de clicar no botão Páginas .
* **Converter linhas suaves em curvas**: Reduz o número de pontos de controle usados para criar curvas em desenhos CAD, o que resulta em arquivos PDF menores e renderização na tela mais rápida.
* **Descartar configurações de impressão incorporadas**: Remove as configurações de impressão incorporadas, como dimensionamento de página e modo duplex, do documento.
* **Descartar marcadores**: Remove todos os marcadores do documento.
* **Nivelar campos de formulário**: Torna os campos de formulário inutilizáveis sem alterações na aparência. Os dados do formulário são unidos à página para se tornarem conteúdo da página.
* **Descartar todas as imagens alternativas**: Remove todas as versões de uma imagem, exceto a versão destinada à visualização na tela. Alguns PDF incluem várias versões da mesma imagem para diferentes propósitos, como visualização na tela de baixa resolução e impressão de alta resolução.
* **Descartar Tags de Documento**: Remove as tags do documento, o que também remove a acessibilidade e os recursos de refluxo do texto.
* **Detectar E Mesclar Fragmentos De Imagem**: Procura imagens ou máscaras que são fragmentadas em fatias finas e tenta mesclar as fatias em uma única imagem ou máscara.
* **Descartar Índice de Pesquisa Incorporado**: Remove índices de pesquisa incorporados, o que reduz o tamanho do arquivo.

#### Descartar dados do usuário {#discard-user-data}

Selecionar **Descartar dados do usuário** para remover quaisquer informações pessoais que você não deseja distribuir ou compartilhar com outros usuários.

* **Descartar Todos Os Comentários, Forms E Multimídia**: Remove todos os comentários, formulários, campos de formulário e multimídia do PDF.
* **Descartar Todos os Dados de Objeto**: Remove todos os objetos do PDF.
* **Descartar referências cruzadas externas**: Remove links para outros documentos. Os links que saltam para outros locais no PDF não são removidos.
* **Descartar Conteúdo De Camada Oculto E Nivelar Camadas Visíveis**: Diminui o tamanho do arquivo. O documento otimizado se parece com o PDF original, mas não contém informações da camada.
* **Descartar Informações E Metadados Do Documento**: Remove informações no dicionário de informações do documento e em todos os fluxos de metadados. (Use o comando Salvar como para restaurar fluxos de metadados a uma cópia do PDF.)
* **Descartar Anexos de Arquivo**: Remove todos os anexos de arquivo, incluindo anexos adicionados ao PDF como comentários. (O PDF Otimizer não otimiza os arquivos anexados.)
* **Descartar Dados Privados De Outros Aplicativos**: Remove informações de um documento do PDF que é útil somente para o aplicativo que criou o documento. Essa configuração não afeta a funcionalidade do PDF, mas diminui o tamanho do arquivo.

### Limpar {#clean-up}

Selecionar **Limpar** para remover itens desnecessários do documento.
Esses itens incluem elementos obsoletos ou desnecessários para o uso pretendido do documento. A remoção de determinados elementos pode afetar seriamente a funcionalidade do PDF. Por padrão, somente os elementos que não afetam a funcionalidade são selecionados. Se não tiver certeza das implicações da remoção de outras opções, use as seleções padrão.

**Compactação**

Selecione uma das seguintes opções de compactação Flate no menu suspenso:

* Compactar todo o arquivo
* Compactar estrutura do documento
* Remover compactação
* Deixe a compactação intocada

**Usar Flate Para Codificar Fluxos Que Não Estão Codificados**: Aplica a compactação Flate a todos os fluxos que não estão codificados.

**Descartar marcadores inválidos**: Remove marcadores que apontam para páginas no documento que são excluídas.

**Descartar Destinos Nomeados Não Referenciados**: Remove destinos nomeados que não estão sendo referenciados internamente do documento PDF. Essa opção não verifica links de outros arquivos PDF ou sites.

**Otimize O PDF Para O Fast Web View**: Reestrutura um documento PDF para download de página por vez (fornecimento de bytes) de servidores da Web.

**Em Fluxos Que Usam Codificação LZW, Use Flate Em Vez Disso**: Aplica a compactação Flate a todos os fluxos de conteúdo e imagens que usam a codificação LZW.

**Descartar Links Inválidos**: Remove links que saltam para destinos inválidos.

**Otimizar o conteúdo da página**: Converte todos os caracteres de fim de linha em caracteres de espaço, o que melhora a compactação de Flate.

## Configurações do Microsoft Excel (somente Windows) {#microsoft-excel-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Excel são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**Tente o OpenOffice como Conversor de Fallback**: Quando essa opção é selecionada e uma conversão usando o Microsoft Excel falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Extensões de nome de arquivo**: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `xls,xlsx`. Não inclua um ponto antes ou um espaço entre as extensões.

**Criar arquivo compatível com o PDF/A-1a**: Força o uso da configuração PDF/A-1b:2005 RGB Adobe PDF.

**Adicionar Marcadores Ao Adobe PDF**: Converte nomes de planilhas do Excel em marcadores. Esta opção está selecionada por padrão.

**Ajustar A Planilha A Uma Única Página**: Reduz o tamanho do texto para que caiba na planilha em uma única página.

**Converter toda a pasta de trabalho**: Converte todas as planilhas no arquivo Excel. Se essa opção não estiver selecionada, somente a página atual será convertida.

**Executar macros automaticamente**: Executa todas as macros no documento do Excel (como uma macro que insere o tempo atual) antes de converter o documento.

**Converter Informações do Documento**: Adiciona propriedades de documento PDF com base nas informações do documento no arquivo de origem. Isso inclui informações como título do documento, autor, assunto e palavras-chave.

**Adicionar Links Ao Adobe PDF**: Converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**Anexar arquivo de origem ao Adobe PDF**: Quando essa opção é selecionada, a planilha original do Excel é inserida como um anexo dentro do documento PDF gerado.

**Habilitar Acessibilidade E Reflow Com Adobe PDF Marcado**: Incorpora tags dentro do documento PDF para ativar a acessibilidade e o refluxo.

**Lista De Adições Do Excel A Serem Carregadas**: Por padrão (por motivos de segurança), nenhum complemento do Excel é executado quando um arquivo do Excel é convertido em PDF. Para permitir que determinados suplementos do Excel sejam executados durante a conversão, forneça uma lista separada por vírgulas dos nomes dos suplementos.

**Lista De Planilhas Para Converter**: Quando essa caixa estiver vazia, todas as planilhas na planilha do Excel serão incluídas no PDF gerado. Para converter seletivamente um subconjunto de planilhas, forneça uma lista separada por vírgulas de nomes de planilhas.

## Configurações do Microsoft PowerPoint (somente Windows) {#microsoft-powerpoint-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft PowerPoint são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Tente o OpenOffice como Conversor de Fallback]**: Quando essa opção é selecionada e uma conversão usando o Microsoft PowerPoint falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões de nome de arquivo]**: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é ppt, pptx. Não inclua um ponto antes ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar Marcadores Ao Adobe PDF]**: Converte títulos do PowerPoint em marcadores. Esta opção está selecionada por padrão.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como anexo. Por padrão, essa opção não é selecionada.

**[!UICONTROL Habilitar Acessibilidade E Reflow Com Adobe PDF Marcado]**: Incorpora tags ao arquivo PDF. Por padrão, essa opção não é selecionada.

**[!UICONTROL Converter multimídia em multimídia PDF]**: Converte multimídia em PDF multimídia, quando possível. Esta opção está selecionada por padrão.

**[!UICONTROL Converter Notas do Orador]**: Converte as notas do alto-falante em PDF.

**[!UICONTROL Executar macros automaticamente]**: Executa qualquer macros no documento do PowerPoint (como uma macro que insere o tempo atual) antes de converter o documento.

**[!UICONTROL Layout de PDF com base nas configurações da impressora do PowerPoint]**: Usa configurações de impressora do PowerPoint para dispor o documento PDF.

**[!UICONTROL Adicionar Links Ao Adobe PDF]**: Preserva os links existentes quando o arquivo é convertido. A aparência dos links geralmente permanece inalterada. Os links só poderão ser criados se a opção Habilitar acessibilidade também estiver selecionada. Por padrão, essa opção não é selecionada.

**[!UICONTROL Salvar Transições De Slides No Adobe PDF]**: Converte transições de slide. Esta opção está selecionada por padrão.

**[!UICONTROL Salvar Animações No Adobe PDF]**: Salva as animações convertidas no arquivo PDF.

**[!UICONTROL Converter Slides Ocultos Em Páginas PDF]**: Converte slides ocultos.

**[!UICONTROL Criar arquivo compatível com o PDF/A-1a]**: Força o uso da configuração PDF/A-1b:2005 RGB Adobe PDF. Alguns recursos do PowerPoint não são convertidos quando você produz um arquivo PDF. Se uma transição do PowerPoint não tiver uma transição equivalente no Acrobat, uma transição semelhante será substituída. Se vários efeitos de animação estiverem no mesmo slide, um único efeito será usado. As transições de página e os marcadores são convertidos.

## Configurações do Microsoft Project (somente Windows) {#microsoft-project-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Project são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensões de nome de arquivo:]** Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `mpp`. Não inclua um ponto antes ou um espaço entre as extensões.

1. **[!UICONTROL Converter Informações do Documento]**: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.
1. **[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como anexo.
1. **[!UICONTROL Criar arquivo compatível com o PDF/A-1a]**: Força o uso da configuração PDF/A-1b:2005 RGB Adobe PDF.
1. **[!UICONTROL Executar macros automaticamente]**: Executa todas as macros no documento do Projeto do Microsoft (como uma macro que insere o tempo atual) antes de converter o documento.

## Configurações do Microsoft Word (somente Windows) {#microsoft-word-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Word são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**[!UICONTROL Tente o OpenOffice como Conversor de Fallback]**: Quando essa opção é selecionada e uma conversão usando o Microsoft Word falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o OpenOffice. Se a conversão usando o OpenOffice falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões de nome de arquivo]**: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `doc,docx,rtf,txt`. Não inclua um ponto antes ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar Marcadores Ao Adobe PDF]**: Converte cabeçalhos em marcadores. Esta opção está selecionada por padrão.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como anexo.

**[!UICONTROL Converter Referências Cruzadas E Índice Em Links]**: Converte todas as referências cruzadas e entradas do índice em links. Esta opção está selecionada por padrão.

**[!UICONTROL Habilitar Acessibilidade E Reflow Com Adobe PDF Marcado]**: Incorpora tags ao arquivo PDF. Esta opção está selecionada por padrão.

**[!UICONTROL Criar arquivo compatível com o PDF/A-1a]**: Se selecionada, força a configuração PDF/A-1b:2005 RGB Adobe PDF a ser usada.

**[!UICONTROL Executar macros automaticamente]**: Executa qualquer macros no documento do Word (como uma macro que insere o tempo atual) antes de converter o documento.

**[!UICONTROL Preservar A Marcação Do Documento No Adobe PDF]**: Converte marcação no documento do Word em anotações no arquivo PDF.

**[!UICONTROL Adicionar Links Ao Adobe PDF]**: Converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**[!UICONTROL Converter Links De Nota De Rodapé E De Nota De Fim]**: Cria links a partir das citações de nota de rodapé e nota de fim para notas no documento PDF.

**[!UICONTROL Converter comentários exibidos em notas no Adobe PDF]**: Converte comentários no documento do Word em notas de texto no documento do PDF.

**[!UICONTROL Habilitar marcação avançada]**: Adiciona tags avançadas para acessibilidade aprimorada.

**[!UICONTROL Converter todos os estilos em marcadores]**: Converte todos os estilos no documento do Word em marcadores no documento do PDF.

**[!UICONTROL Converter estilos especificados em marcadores]**: Converte os estilos definidos na variável **[!UICONTROL Estilos com níveis]** para marcadores no documento PDF.

**[!UICONTROL Estilos com Níveis]**: Especifica quais estilos no documento do Word são convertidos em marcadores no documento PDF. Especifica também o nível dos marcadores. Para usar esse recurso, desmarque a opção **[!UICONTROL Converter todos os estilos em marcadores]** e especifique os nomes do estilo no seguinte formato:

**styleName1=level1[,styleName2=level2...]**

Se um nome de estilo do Microsoft Word incluir uma vírgula (,) ou sinal igual (=), preceda os caracteres especiais com o caractere de escape (&quot;\_). Por exemplo, especifique um estilo chamado &quot;Cabeçalho, 1&quot; como Cabeçalho\, 1.

**Codificação do Acrobat PDFMaker:** Especifica o tipo de codificação dos arquivos de texto simples de entrada para o Acrobat PDFMaker. Por exemplo, se você estiver usando um arquivo codificado em UTF-8, selecione UTF-8 para obter melhores resultados.

## Configurações do Microsoft Visio (somente Windows) {#visio}

**Converter Informações do Documento**: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão. Essa opção é ativada por padrão.

**Adicionar Links Ao Adobe PDF**: Preserva todos os links. Esta opção está selecionada por padrão.

**Adicionar Marcadores Ao Adobe PDF**: Converte cabeçalhos em marcadores. Esta opção está selecionada por padrão.

**Anexar arquivo de origem ao Adobe PDF**: Adiciona o arquivo de origem ao arquivo PDF como anexo.

**Sempre Nivelar Camadas No Adobe PDF**: Nivela todas as camadas do Visio.

**Converter todas as páginas**: Converte todas as páginas do arquivo Visio.

**Abrir Painel Camadas Quando Exibido No Adobe Acrobat**: Se as camadas do Visio não estiverem niveladas, abre uma janela onde é possível especificar as camadas que são preservadas no arquivo PDF quando abertas com o Acrobat. Esta opção está selecionada por padrão.

**Criar arquivo compatível com PDF/A-1b**: Força o uso da Configuração do Adobe PDF PDF/A-1b:2005 (RGB).

**Converter Comentários Em Comentários Do Adobe PDF**: Converte observações do Visio em comentários do PDF.

## Configurações do Microsoft Publisher (somente Windows) {#microsoft-publisher-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Publisher são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**[!UICONTROL Extensões de nome de arquivo]**: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `pub`. Não inclua um ponto antes ou um espaço entre as extensões.

## Configurações do AutoCAD (somente Windows) {#autocad-settings-windows-only}

Essas opções determinam como os arquivos AutoCAD são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensões de nome de arquivo]**: Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `dwg`. Não inclua um ponto antes ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: Adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Esta opção está selecionada por padrão.

**[!UICONTROL Adicionar Marcadores Ao Adobe PDF]**: Converte cabeçalhos em marcadores.

**[!UICONTROL Sempre Nivelar Camadas No Adobe PDF]**: Nivela todas as camadas do AutoCAD.

**[!UICONTROL Abrir Painel Camadas Quando Exibido No Adobe Acrobat]**: Mostra a estrutura de camadas quando o PDF é aberto no Acrobat.

**[!UICONTROL Converter todos os layouts]**: Inclui todos os layouts no PDF.

**[!UICONTROL Converter espaço do modelo em 3D]**: Quando selecionado, o layout do espaço do modelo é convertido em uma anotação 3D no PDF.

**[!UICONTROL Adicionar Links Ao Adobe PDF]**: Se selecionada, preserva todos os links.

**[!UICONTROL Anexar arquivo de origem ao Adobe PDF]**: Adiciona o arquivo de origem ao arquivo PDF como anexo.

**[!UICONTROL Criar arquivo compatível com PDF/A-1b]**: Força o uso da configuração PDF/A-1b Adobe PDF.

**[!UICONTROL Converter todas as camadas]**: Por padrão, o PDF Generator converte somente a camada padrão de arquivos AutoCAD em PDF, em vez de todas as camadas dentro do arquivo. Selecione essa opção para converter todas as camadas do arquivo.

**[!UICONTROL Incorporar informações de escala]**: Preserva informações de escala de desenho.

**[!UICONTROL Converter layout atual]**: Inclui apenas o layout atual no PDF.

**[!UICONTROL Lista De Layouts Do AutoCAD A Serem Convertidos]**: Um desenho do AutoCAD pode ter vários layouts. Quando esta caixa está vazia, todos os layouts no desenho do AutoCAD são incluídos no documento PDF gerado. Para converter seletivamente um subconjunto dos layouts, forneça uma lista separada por vírgulas de nomes de layout.

## Definições do OpenOffice {#openoffice-settings}

Essas opções determinam como os arquivos OpenOffice são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Tente o PDFMaker como Conversor de Fallback**: Quando essa opção é selecionada e uma conversão usando o OpenOffice falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o PDFMaker. Se a conversão usando o PDFMaker falhar ou atingir o limite de tempo limite especificado, uma exceção será gravada no arquivo de log.

**Extensões de nome de arquivo**: Especifique as extensões de nome de arquivo para os tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Não inclua um ponto antes ou um espaço entre as extensões.

**Intervalo**: Converta todas as páginas ou especifique páginas específicas ou um intervalo de páginas. Se um intervalo de páginas não estiver definido, todas as páginas serão convertidas. Para exportar um intervalo de páginas, use o formato 3-6. Para exportar páginas únicas, use o formato 7;9;11. É possível exportar uma combinação de intervalos de página e páginas únicas usando um formato como 3-6;8;10;12.

**Orientação da página**: Para arquivos de texto simples somente, selecione retrato ou paisagem para o documento PDF convertido.

**Imagens**: Configure como as imagens são convertidas. Imagens EPS com visualizações incorporadas são exportadas somente como visualizações. Imagens EPS sem visualizações incorporadas são exportadas como espaços reservados vazios. Com a compactação sem perdas de imagens, todos os pixels são preservados. Com a compressão de JPEG de imagens e um nível de alta qualidade, quase todos os pixels são preservados. Com um nível de baixa qualidade, alguns pixels são perdidos e artefatos são introduzidos, mas os tamanhos dos arquivos são reduzidos.

**Geral**: Ative as opções para converter um PDF marcado ou exportar notas de documento do Writer e FormCalc, Imprimir efeitos de transição de slides ou páginas em branco para o PDF. Quando as tags são exportadas, o tamanho do arquivo pode aumentar em grandes quantidades. Algumas tags exportadas são tabelas de conteúdo, hiperlinks e controles.

Também é possível especificar como os formulários são enviados. As opções são XML, FDF, PDF ou HTML. Essa configuração substitui a propriedade URL do controle definida no documento. Somente uma configuração comum pode ser selecionada para o documento PDF:

* PDF (envia o documento inteiro)
* FDF (envia o conteúdo do controle)
* HTML
* XML

**PDF com tags**: Permite a criação de PDF marcado a partir de documentos OpenOffice. O PDF marcado contém informações sobre a estrutura do conteúdo do documento. Isso pode ajudar ao exibir o documento em dispositivos com telas diferentes e ao usar software de leitor de tela. Também ajuda o software de acessibilidade a executar várias operações úteis com o documento PDF, como ler em voz alta o conteúdo do documento PDF.

**Exportar notas**: Converte as notas em documentos OpenOffice em notas no documento PDF gerado.

**Usar efeitos de transição**: Converte os efeitos de transição de slides em apresentações do OpenOffice em efeitos de transição de PDF correspondentes.

**Enviar Forms Em Formato**: Cria um formulário PDF que pode ser preenchido e impresso pelo usuário do documento PDF.

**Exportar páginas em branco automaticamente inseridas**: Quando essa opção é selecionada, as páginas em branco inseridas automaticamente são incluídas no documento PDF gerado. Isso é útil se você estiver imprimindo um documento PDF nos dois lados. Por exemplo, um livro pode ser configurado para que a primeira página do capítulo sempre inicie em uma página ímpar. Se o capítulo anterior terminar em uma página ímpar, o OpenOffice insere uma página par em branco. Essa opção controla se a página par deve ser incluída no PDF gerado.

## Outras configurações de aplicativo (somente Windows) {#other-applications-settings-windows-only}

Não é possível alterar as configurações de outros aplicativos por meio do console de administração; eles exibem as extensões de nome de arquivo dos tipos de arquivo suportados. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações de tipo de arquivo](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

O suporte para esses tipos de arquivos pode precisar ser personalizado. Para obter mais informações, consulte &quot;Adicionar suporte para formatos de arquivo nativos adicionais&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Para obter ajuda sobre como configurar uma impressora de rede PDFG, consulte [Configurando uma impressora de rede PDFG (somente Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
