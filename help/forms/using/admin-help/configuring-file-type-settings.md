---
title: Definição das configurações de tipo de arquivo
description: Saiba como definir configurações de tipo de arquivo. No PDF Generator, você pode definir a configuração do aplicativo para tipos de arquivos compatíveis para definir as configurações de tipo de arquivo.
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
feature: PDF Generator
exl-id: 1a6640cc-22ef-41d5-a0c6-7a2c2dabcef1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '6188'
ht-degree: 0%

---

# Definição das configurações de tipo de arquivo {#configuring-file-type-settings}

No PDF Generator, é possível definir as configurações do aplicativo para tipos de arquivos compatíveis. No Windows, você pode definir as configurações do aplicativo para cada tipo de arquivo compatível. No UNIX e Linux, você pode definir as configurações do aplicativo para HTML-para-PDF e OpenOffice.

Na página Definições de Tipo de Arquivo, você pode executar estas tarefas:

* [Criar ou editar uma configuração de Tipo de arquivo](#create-or-edit-file-type-settings)
* Especifique quais configurações de tipo de arquivo usar por padrão (consulte [Importação e exportação de arquivos de configuração de PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md))
* [Alterar as configurações padrão](/help/forms/using/admin-help/configuring-file-type-settings.md#change-the-default-settings)
* [Habilitar suporte para PDF/A](/help/forms/using/admin-help/enable-pdf-a-support.md)
* [Excluir uma configuração de Tipo de arquivo](/help/forms/using/admin-help/enable-pdf-a-support.md)

>[!NOTE]
>
>As configurações de tipo de arquivo não estão disponíveis para os conversores de fallback, como Acrobat para conversão de HTML para PDF, Microsoft PowerPoint, Microsoft Word e Microsoft Excel.

## Criar ou editar configurações de Tipo de Arquivo {#create-or-edit-file-type-settings}

Crie ou edite uma configuração de tipo de arquivo para especificar como o aplicativo lida com a conversão de tipos de arquivo compatíveis. No Windows, você pode definir as configurações do aplicativo para cada tipo de arquivo compatível. No UNIX e Linux, você pode definir as configurações do aplicativo para HTML-para-PDF e OpenOffice.

1. No console de administração, clique em **[!UICONTROL Serviços]** > **[!UICONTROL PDF Generator]** > **[!UICONTROL Configurações de Tipo de Arquivo]**.
1. Clique em Novo ou clique no nome de uma configuração.
1. Na caixa Extensões de nome de arquivo, digite as extensões de nome de arquivo, separadas por vírgulas, para os tipos de arquivo aceitos para este aplicativo. Não inclua o ponto anterior nem um espaço entre as extensões. O padrão é `bmp,gif,jpeg,jpg,tif,tiff,png`.
1. (Opcional) Para usar OCR (reconhecimento óptico de código) de texto em gráficos ou imagens, selecione Usar OCR e defina as seguintes opções:

**Idioma de OCR Primário:** O idioma a ser usado pelo mecanismo de OCR para identificar os caracteres. O padrão é inglês (EUA).

**Estilo de Saída PDF:** Selecione Imagem Pesquisável para ter uma imagem de bitmap das páginas em primeiro plano e o texto digitalizado em uma camada invisível abaixo. A aparência da página não é alterada, mas o texto se torna selecionável e legível. Selecione Texto e gráficos formatados para reconstruir a página original usando texto, fontes, imagens e outros elementos gráficos reconhecidos. O padrão é Imagem pesquisável (Exata).

**Reduzir Resolução de Imagens:** Diminui o número de pixels em imagens coloridas, em tons de cinza e monocromáticas. A redução da resolução de imagens digitalizadas é executada após a conclusão do OCR. O padrão é Menor (600 dpi). Essa opção não estará disponível se você definir o estilo de saída PDF como Imagem pesquisável (Exata).

1. Preencha as informações necessárias nestas seções:

[Importação e exportação de arquivos de configuração de PDF Generator](/help/forms/using/admin-help/importing-exporting-pdf-generator-configuration.md)

[Configurações de exportação do Adobe PDF (somente Windows)](#adobe-pdf-export-settings-windows-only)

[Configurações de HTML para PDF](#html-to-pdf-settings)

[Flash de vídeos para configurações de PDF](#flash-videos-to-pdf-settings)

[Configurações de XPS para PDF](#xps-to-pdf-settings)

[configurações do otimizador de PDF](/help/forms/using/admin-help/configuring-file-type-settings.md)

[Configurações do Microsoft Excel (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-excel-settings-windows-only)

[Configurações do Microsoft PowerPoint (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-powerpoint-settings-windows-only)

[Configurações de projeto do Microsoft (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-project-settings-windows-only)

[Configurações do Microsoft Word (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-word-settings-windows-only)

[Configurações do Microsoft Visio (somente Windows)](#visio)

[Configurações do Microsoft Publisher (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#microsoft-publisher-settings-windows-only)

[Configurações do AutoCAD (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#autocad-settings-windows-only)

[Configurações do OpenOffice](/help/forms/using/admin-help/configuring-file-type-settings.md#openoffice-settings)

[Configurações de outros aplicativos (somente Windows)](/help/forms/using/admin-help/configuring-file-type-settings.md#other-applications-settings-windows-only)

   Para ir para outra seção, clique no link na página da Web ou use os botões **[!UICONTROL Avançar]** ou **[!UICONTROL Anterior]**.

1. Após concluir todas as seções, clique em **[!UICONTROL Salvar]** ou **[!UICONTROL Salvar como]** e forneça um nome para a configuração.

O suporte para vários tipos de arquivos pode ser personalizado. (Consulte &quot; [Adicionar suporte para formatos de arquivo nativos adicionais](https://help.adobe.com/en_US/AEMForms/6.1/ProgramLC/WS624e3cba99b79e12e69a9941333732bac8-7756.2.html)&quot; em [Programação com formulários AEM](https://www.adobe.com/go/learn_lc_programming_11).)

## Alterar as configurações padrão {#change-the-default-settings}

Você pode alterar o valor padrão das configurações do Adobe PDF, de segurança e do tipo de arquivo que se aplicam às fontes recém-criadas. A alteração dos padrões não afeta as configurações das fontes existentes.

1. No Console de Administração, clique em **[!UICONTROL Serviços > PDF Generator]**.
1. Na página **[!UICONTROL Configurações do Adobe PDF]**, **[!UICONTROL Configurações de Tipo de Arquivo]** ou **[!UICONTROL Configurações de Segurança]**, clique em **[!UICONTROL Definir Configurações Padrão]**.
1. Selecione suas configurações padrão preferidas. Uma ou mais das seguintes configurações estão disponíveis na página Definir configurações padrão:

   **[!UICONTROL Configuração do Adobe PDF]**: o padrão original é Padrão (Acrobat 6).

   **[!UICONTROL Configurações de Segurança]**: o padrão original é Sem Segurança (Acrobat 5).

   **[!UICONTROL Configurações de Tipo de Arquivo]**: o padrão original é Padrão.

1. Clique em **[!UICONTROL Salvar]**.

## Excluir uma configuração de Tipo de arquivo {#delete-a-file-type-setting}

É possível excluir uma configuração de tipo de arquivo que não é mais usada.

1. No console de administração, clique em **[!UICONTROL Serviços > PDF Generator> Configurações de Tipo de Arquivo]**.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. Você pode selecionar várias origens. As configurações que não têm uma caixa de seleção ao lado delas são sempre incluídas com PDF Generator e não podem ser excluídas.
1. Clique em **[!UICONTROL Excluir]** e, na página Confirmação de Exclusão, clique em **[!UICONTROL Excluir]**.

## Configurações de imagem para PDF {#image-to-pdf-settings}

As opções a seguir determinam como os arquivos de imagem são convertidos em PDF. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensões de Nome de Arquivo:** Lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

**Tente o Conversor de Fallback:** o PDF Generator pode usar o Java™ ou o Acrobat para converter arquivos de imagem em PDF. Quando essa opção estiver selecionada e uma conversão falhar ou atingir o limite de tempo limite especificado, o PDF Generator tentará a conversão usando o método alternativo. Se o método alternativo falhar ou atingir o tempo limite especificado, uma exceção será gravada no arquivo de log.

>[!NOTE]
>
>Arquivos JPEG 2000 só podem ser convertidos usando o Acrobat.

**Usar OCR:** Especifica se o OCR (reconhecimento óptico de caracteres) deve ser aplicado ao PDF. O software de OCR permite pesquisar, corrigir e copiar o texto no PDF.

***observação **: o recurso PDF de OCR (PDF pesquisável) só tem suporte no Microsoft Windows.*

**Idioma de OCR Primário:** Especifica o idioma a ser usado pelo mecanismo de OCR para identificar os caracteres.

**Estilo de Saída PDF:** Determina o tipo de PDF a ser produzido. Todos os formatos aplicam o OCR e o reconhecimento de fonte e página às imagens de texto e as convertem em texto normal.

**Imagem pesquisável:** garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original, a distorce conforme necessário e coloca uma camada de texto invisível sobre ela. A opção Reduzir resolução das imagens determina se a imagem terá uma resolução reduzida e até que ponto.

**Imagem Pesquisável (Exata):** Garante que o texto seja pesquisável e selecionável. Essa opção mantém a imagem original e coloca uma camada de texto invisível sobre ela. Recomendado para casos que exigem fidelidade máxima à imagem original.

**ClearScan:** sintetiza uma nova fonte Type 3 que se aproxima muito do original e preserva o plano de fundo da página usando uma cópia de baixa resolução.

**Reduzir Resolução de Imagens:** Diminui o número de pixels em imagens coloridas, em escala de cinza e monocromáticas após a conclusão do OCR. Escolha o grau de redução de resolução a ser aplicado. As opções com números mais altos reduzem a resolução, o que produz PDF de resolução mais alta.

## Configurações de exportação do Adobe PDF (somente Windows) {#adobe-pdf-export-settings-windows-only}

A configuração Tipo de arquivo de exportação na seção de configurações de exportação do Adobe PDF é usada para converter um arquivo PDF em outro formato. O padrão é HTML 4.01 com folhas de estilos em cascata (CSS) 1.0 (*.htm, *.html).

Para obter instruções sobre como acessar esta configuração, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

## Configurações de HTML para PDF {#html-to-pdf-settings}

As opções a seguir determinam como os arquivos de HTML são convertidos em PDF. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Tente o Conversor de Fallback:** o PDF Generator pode usar o Java™ ou o Acrobat para converter arquivos HTML em PDF. Quando essa opção estiver selecionada e uma conversão falhar ou atingir o limite de tempo limite especificado, o PDF Generator tentará a conversão usando o método alternativo. Se o método alternativo falhar ou atingir o tempo limite especificado, uma exceção será gravada no arquivo de log.

**Codificação Padrão:** Define a codificação de entrada do texto do arquivo a partir de um menu de sistemas operacionais e alfabetos. Usa a seleção mostrada na opção Codificação padrão somente se o arquivo de origem HTML não especificar um tipo de codificação.

**Forçar Codificação Selecionada:** Ignora qualquer codificação especificada no arquivo de origem do HTML e usa a seleção mostrada na opção Codificação Padrão.

### Configurações de spidering {#spidering-settings}

*Aranha* verifica nas páginas da Web os links para outras páginas da Web. Quando um link para outra página da Web é encontrado, a página de destino é buscada e incluída no documento PDF gerado. Ative essas opções para definir o número de níveis que serão buscados e convertidos em PDF:

**Obter Somente X Níveis:** Aranhas e converte páginas até uma profundidade do nível especificado da URL da página base. Um valor igual a 1 converte somente o URL fornecido.

**Obter Site Inteiro:** Converte o site inteiro, iniciando da URL fornecida.

**Permanecer no Mesmo Caminho:** Todos os links que apontam para páginas que não estão no mesmo caminho relativo que a URL base não são convertidos durante o enriquecimento.

**Permanecer no Mesmo Servidor:** Todos os links que apontam para páginas em servidores diferentes não são convertidos durante a propagação. Somente os links que apontam para o mesmo servidor que a URL especificada são convertidos.

### Configurações de conversão de página {#page-conversion-settings}

Ative essas opções para especificar como as páginas de HTML são convertidas. Com base no tamanho da página, os valores de largura, altura e margem são ajustados de acordo.

**Tamanho da Página:** Escolha personalizado e especifique a largura e a altura ou selecione dimensões predefinidas.

**Orientação:** selecione retrato ou paisagem para o documento PDF convertido.

**Margens:** Especifica as margens (Superior, Inferior, Esquerda e Direita) no documento de PDF gerado.

**Adicionar Marcadores ao PDF:** Adiciona marcadores ao documento PDF.

**Habilitar PDF marcado:** incorpora marcas no documento PDF.

**Definir Configurações de Exibição Iniciais:** Permite que você configure Opções de Documento, Opções de Janela e Opções de Interface do Usuário. Essas configurações determinam como o conteúdo é exibido inicialmente.

### Opções de documento {#document-options}

Ative essas opções para especificar como exibir conteúdo, como exibir páginas no documento PDF e como especificar o nível de ampliação:

**Mostrar:** Selecione os painéis a serem abertos no Acrobat quando o documento PDF for aberto.

**Layout da página:** selecione o tipo de layout de página para o documento PDF.

**Ampliação:** escolha a ampliação predefinida para a exibição inicial do documento PDF ou selecione um valor personalizado. A escolha de uma configuração padrão indica que a ampliação padrão do Acrobat é usada.

**Abrir para Número de Página:** Especifique o número de página para o qual o PDF abre.

### Opções de janela {#window-options}

Habilite estas opções para especificar como a janela é dimensionada e exibida.

**Redimensionar Janela para Página Inicial:** Redimensiona a janela do Acrobat para o tamanho da página inicial.

**Centralizar Janela na Tela:** Abre a janela no centro da tela.

**Abrir no Modo de Tela Inteira** Abre a janela no modo de tela inteira.

**Mostrar:** Exibe o título ou o nome do arquivo do documento na janela.

### Opções da interface do usuário {#user-interface-options}

Ative estas opções para especificar a aparência da janela:

**Ocultar Barra de Menus:** oculta a barra de menus no documento PDF.

**Ocultar Barras de Ferramentas:** oculta as barras de ferramentas no documento PDF.

**Ocultar Controles de Janela:** Oculta os controles de janela no documento PDF.

## Flash de vídeos para configurações de PDF {#flash-videos-to-pdf-settings}

O PDF Generator suporta a capacidade de enviar um vídeo para o Flash Adobe (SWF ou arquivo FLV) e criar um arquivo PDF com um vídeo para o Flash Adobe incorporado. Essa conversão não requer que o Flash Player Adobe esteja instalado no servidor do Forms. Para obter instruções sobre como acessar esta opção, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Extensões de Nome de Arquivo:** Lista separada por vírgulas de extensões de nome de arquivo que podem ser convertidas.

## Configurações de XPS para PDF {#xps-to-pdf-settings}

XML Paper Specification (XPS) é usado na máquina de impressão do Windows. Este é um formato do Microsoft e pode ser criado a partir de qualquer aplicativo do Microsoft Office. Os formulários AEM oferecem a capacidade de converter PDF de arquivos XPS.

**Extensões de Nome de Arquivo:** Uma lista separada por vírgulas de todas as extensões de nome de arquivo XPS que podem ser convertidas. Atualmente há um formato: .xps.

## configurações do otimizador de PDF {#pdf-optimizer-settings}

O PDF Generator suporta a capacidade de reduzir o tamanho dos arquivos PDF. Se você usa todas essas configurações ou apenas algumas dependem de como você pretende usar os arquivos e das propriedades essenciais que um arquivo deve ter. Na maioria dos casos, as configurações padrão são apropriadas para eficiência máxima - economizando espaço removendo fontes incorporadas, compactando imagens e removendo itens dos arquivos que não são mais necessários.

>[!NOTE]
>
>A otimização de um documento assinado digitalmente remove e invalida as assinaturas digitais.

Para obter instruções sobre como acessar esta configuração, consulte [Criar ou editar configurações de tipo de arquivo](configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Versão do PDF de Destino:** Especifica a versão do Acrobat com a qual o PDF é compatível.

### Fontes {#fonts}

1. Selecione **Fontes.**
1. Selecione uma das seguintes opções:

   **Desincorporar todas as fontes:** desincorpora todas as fontes inseridas.

   **Não desincorporar nenhuma fonte:** Não desincorpora nenhuma fonte.

   **Desincorporar algumas fontes:** desincorpora apenas as fontes especificadas. Siga estas etapas para especificar as fontes que deseja desincorporar:

   * Se necessário, selecione um diretório de fontes diferente no menu suspenso **Fonte**. Este menu suspenso lista diretórios de fontes especificados em **Início > Configurações > Sistema Principal > Configurações Principais**.
   * Selecione uma ou mais fontes na lista **Fontes Disponíveis** e clique em **Adicionar**. Estas fontes foram adicionadas à lista **Fontes a serem desincorporadas**.
   * Para desincorporar algumas fontes que não existem no Forms Server, digite os nomes dessas fontes na caixa **Adicionar fontes a desincorporar**. Clique em **Adicionar**.

   >[!NOTE]
   >
   >*Para desincorporar algumas fontes cujos subconjuntos estão inseridos no documento, adicione o sinal + ao nome da fonte. Por exemplo, &quot;+Helvetica&quot;.*

1. Para incorporar apenas os subconjuntos em uso das fontes inseridas, selecione **Subdefinir todas as fontes inseridas**.

   >[!NOTE]
   >
   >*Se você estiver usando esta opção em combinação com **Desincorporar algumas fontes**, as fontes da lista **Adicionar fontes a desincorporar**ainda serão completamente desincorporadas.*

   >[!NOTE]
   >
   >*Subconjunto de fontes é a técnica de incorporar apenas uma parte de uma fonte. Um subconjunto de fontes contém apenas os caracteres usados no documento.*

### Transparência {#transparency}

Se o documento PDF incluir um trabalho artístico que contenha transparência, você poderá usar as configurações do Otimizador de PDF para nivelar a transparência e reduzir o tamanho do arquivo.

>[!NOTE]
>
>Se Acrobat 4.0 e posterior for selecionado como a versão do PDF de destino, todos os objetos transparentes serão nivelados. Para outras versões do Target PDF, a transparência é suportada e você pode definir as configurações de transparência.

Selecione **Transparência** para definir as configurações de transparência ao otimizar documentos PDF.

**Nível de transparência** Especifica a quantidade de informações vetoriais que serão preservadas. Configurações mais altas preservam mais objetos vetoriais, enquanto configurações mais baixas rasterizam mais objetos vetoriais; configurações intermediárias preservam áreas simples na forma vetorial e rasterizam as complexas. Selecione a configuração mais baixa para rasterizar todo o trabalho artístico.

>[!NOTE]
>
>A quantidade de rasterização que ocorre depende da complexidade da página e dos tipos de objetos sobrepostos.

**Line-Art e Resolução de Texto** para a qual todos os objetos, incluindo imagens, arte vetorial, texto e gradientes, são rasterizados. Os valores compatíveis são de 1 pixel por polegada (ppi) a 9600 ppi.

>[!NOTE]
>
>A Arte em linha e a resolução de texto geralmente devem ser definidas como 600-1200 ppi para fornecer rasterização de alta qualidade, especialmente em texto serif ou de tamanho de ponto pequeno.

**Resolução de gradiente e malhas** para a qual gradiente e malhas são rasterizados. Os valores compatíveis são de 1 ppi a 1200 ppi.

>[!NOTE]
>
>A resolução de gradiente e malha geralmente deve ser definida para 150-300 ppi, pois a qualidade dos gradientes, sombras projetadas e difusões não melhora com resoluções mais altas, mas o tempo de impressão e o tamanho do arquivo aumentam.

**Converter Todo o Texto em Contornos** Converte todos os objetos de tipo (tipo de ponto, tipo de área e tipo de caminho) em contornos e descarta todas as informações de glifo de tipo em páginas que contêm transparência. Essa opção garante que a largura do texto permaneça consistente durante o nivelamento. Observe que ativar essa opção fará com que fontes pequenas apareçam um pouco mais espessas quando visualizadas no Acrobat ou impressas em impressoras de desktop de baixa resolução. A qualidade do tipo impresso em impressoras ou fotocompositoras de alta resolução não é afetada.

**Converter todos os traçados em contornos** Converte todos os traçados em caminhos simples preenchidos em páginas que contêm transparência. Essa opção garante que a largura dos traçados permaneça consistente durante o nivelamento. Observe que ativar essa opção faz com que os traçados finos pareçam um pouco mais espessos e pode degradar o desempenho do nivelamento.

**Regiões de Clipe Complexas** Garante que os limites entre o trabalho artístico de vetor e o trabalho artístico rasterizado estejam ao longo de caminhos de objeto. Essa opção reduz a compilação de artefatos que resultam quando parte de um log

<!--
NOTE to WRITER: Unfinished sentence above.
-->

>[!NOTE]
>
>Alguns drivers de impressão processam rasterizações e arte vetorial de forma diferente, às vezes resultando em costura de cores. Talvez seja possível minimizar os problemas de costura desativando algumas configurações de gerenciamento de cores específicas do driver de impressão. Essas configurações variam com cada impressora, portanto, consulte a documentação que veio com sua impressora para obter detalhes.

Preservar superimposição: mescla a cor do trabalho artístico transparente com a cor do plano de fundo para criar um efeito de superimposição.

A tabela a seguir mostra tipos comuns de impressoras e sua resolução medida em dpi, sua regra de tela padrão medida em linhas por polegada (lpi) e uma resolução de reamostragem para imagens medidas em pixels por polegada (ppi). Por exemplo, se você estivesse imprimindo em uma impressora a laser de 600 dpi, insira 170 para a resolução na qual as imagens serão reamostradas.

**Imagens** Selecione Imagens para especificar as opções de compactação e reamostragem para imagens coloridas, em tons de cinza e monocromáticas. Talvez você queira experimentar essas opções para encontrar um equilíbrio adequado entre o tamanho do arquivo e a qualidade da imagem.A configuração de resolução para imagens coloridas e em tons de cinza deve ser de 1,5 a 2 vezes maior que a regra da tela de linha na qual o arquivo será impresso. A resolução para imagens monocromáticas deve ser a mesma do dispositivo de saída, mas salvar uma imagem monocromática em uma resolução superior a 1500 dpi aumenta o tamanho do arquivo sem melhorar notavelmente a qualidade da imagem. Imagens que serão ampliadas, como mapas, podem exigir resoluções mais altas.

>[!NOTE]
>
>A reamostragem de imagens monocromáticas pode ter resultados de visualização inesperados, como nenhuma exibição de imagem. Se isso acontecer, desative a reamostragem e converta o arquivo novamente. Esse problema é mais provável de ocorrer com a subamostragem e menos provável com a redução da resolução bicúbica.

<table>
 <tbody>
  <tr>
   <th><p><strong>Resolução da impressora</strong></p> </th>
   <th><p><strong>Tela de linha padrão</strong></p> </th>
   <th><p><strong>Resolução da imagem</strong></p> </th>
  </tr>
  <tr>
   <td><p>300 dpi (impressora a laser)</p> </td>
   <td><p>60 lpp</p> </td>
   <td><p>120 ppi</p> </td>
  </tr>
  <tr>
   <td><p>600 dpi (impressora a laser)</p> </td>
   <td><p>85 lpp</p> </td>
   <td><p>170 ppi</p> </td>
  </tr>
  <tr>
   <td><p>1200 ppp (fotocompositora)</p> </td>
   <td><p>120 lpp</p> </td>
   <td><p>240 ppi</p> </td>
  </tr>
  <tr>
   <td><p>2400 ppp (fotocompositora)</p> </td>
   <td><p>150 lpp</p> </td>
   <td><p>300 ppi</p> </td>
  </tr>
 </tbody>
</table>

#### Descartar objetos {#discard-objects}

* Selecione **Descartar Objetos** para especificar objetos a serem removidos do PDF e para otimizar linhas curvas em desenhos CAD.
* **Descartar Todas as Ações de Envio, Importação e Redefinição de Formulário**: desabilita todas as ações relacionadas ao envio ou à importação de dados de formulário e redefine campos de formulário. Essa opção retém objetos de formulário aos quais as ações estão vinculadas.
* **Descartar Todas as Ações do JavaScript**: remove do PDF as ações que usam o JavaScript.
* **Descartar Miniaturas de Página Inseridas**: remove as miniaturas de página inseridas. Essa opção é útil para documentos grandes, que podem levar muito tempo para desenhar miniaturas de página depois de clicar no botão Páginas.
* **Converter linhas suaves em curvas**: reduz o número de pontos de controle usados para criar curvas em desenhos CAD, o que resulta em arquivos PDF menores e em renderização mais rápida na tela.
* **Descartar Configurações de Impressão Inseridas**: remove do documento as configurações de impressão inseridas, como dimensionamento de página e modo duplex.
* **Descartar Marcadores**: remove todos os marcadores do documento.
* **Nivelar campos de formulário**: torna os campos de formulário inutilizáveis sem alterar sua aparência. Os dados de formulário são mesclados com a página para se tornarem conteúdo de página.
* **Descartar Todas as Imagens Alternativas**: Remove todas as versões de uma imagem, exceto a versão destinada à exibição na tela. Alguns PDF incluem várias versões da mesma imagem para diferentes propósitos, como visualização em tela de baixa resolução e impressão de alta resolução.
* **Descartar marcas de documento**: remove marcas do documento, o que também remove os recursos de acessibilidade e refluxo do texto.
* **Detectar e Mesclar Fragmentos de Imagem**: procura imagens ou máscaras fragmentadas em fatias finas e tenta mesclar as fatias em uma única imagem ou máscara.
* **Descartar Índice de Pesquisa Inserido**: remove os índices de pesquisa inseridos, o que reduz o tamanho do arquivo.

#### Descartar dados do usuário {#discard-user-data}

Selecione **Descartar Dados do Usuário** para remover as informações pessoais que você não deseja distribuir ou compartilhar com outros usuários.

* **Descartar todos os comentários, Forms e multimídia**: remove todos os comentários, formulários, campos de formulário e multimídia do PDF.
* **Descartar Todos os Dados do Objeto**: remove todos os objetos do PDF.
* **Descartar Referências Cruzadas Externas**: remove os links para outros documentos. Os links que saltam para outros locais no PDF não são removidos.
* **Descartar Conteúdo de Camada Oculta e Nivelar Camadas Visíveis**: Diminui o tamanho do arquivo. O documento otimizado se parece com o PDF original, mas não contém informações de camada.
* **Descartar Informações e Metadados do Documento**: remove informações do dicionário de informações do documento e de todos os fluxos de metadados. (Use o comando Salvar como para restaurar fluxos de metadados para uma cópia do PDF.)
* **Descartar anexos de arquivo**: remove todos os anexos de arquivo, incluindo anexos adicionados ao PDF como comentários. (O PDF Otimizer não otimiza os arquivos anexados.)
* **Descartar Dados Privados de Outros Aplicativos**: elimina informações de um documento PDF que sejam úteis somente para o aplicativo que criou o documento. Essa configuração não afeta a funcionalidade do PDF, mas diminui o tamanho do arquivo.

### Limpar {#clean-up}

Selecione **Limpar** para remover itens desnecessários do documento.
Esses itens incluem elementos obsoletos ou desnecessários para o uso pretendido do documento. A remoção de determinados elementos pode afetar seriamente a funcionalidade do PDF. Por padrão, somente os elementos que não afetam a funcionalidade são selecionados. Se não tiver certeza das implicações da remoção de outras opções, use as seleções padrão.

**Compactação**

Selecione uma das seguintes opções de compactação Flate no menu suspenso:

* Compactar todo o arquivo
* Compactar estrutura do documento
* Remover compactação
* Deixe a compactação intocada

**Usar Flate para Codificar Fluxos Não Codificados**: Aplica a compactação Flate a todos os fluxos não codificados.

**Descartar Indicadores Inválidos**: Remove os marcadores que apontam para páginas do documento que foram excluídas.

**Descartar Destinos Nomeados Não Referenciados**: Remove destinos nomeados que não estão sendo referenciados internamente de dentro do documento PDF. Esta opção não verifica se há links de outros arquivos PDF ou sites.

**Otimizar o PDF para o Modo de Exibição Rápido da Web**: reestrutura um documento PDF para download de página por vez (serviço de bytes) de servidores Web.

**Em Fluxos que Usam Codificação LZW, Use Flate**: Aplica a compactação Flate a todos os fluxos de conteúdo e imagens que usam codificação LZW.

**Descartar Links Inválidos**: remove links que saltam para destinos inválidos.

**Otimizar Conteúdo da Página**: converte todos os caracteres de fim de linha em caracteres de espaço, o que melhora a compactação Flate.

## Configurações do Microsoft Excel (somente Windows) {#microsoft-excel-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Excel são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**Tentar OpenOffice como Conversor de Fallback**: quando esta opção estiver selecionada e uma conversão usando o Microsoft Excel falhar ou atingir o limite de tempo limite especificado, o PDF Generator tentará a conversão usando OpenOffice. Se a conversão usando OpenOffice falhar ou atingir o limite de tempo especificado, uma exceção será gravada no arquivo de log.

**Extensões de Nome de Arquivo**: especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `xls,xlsx`. Não inclua um ponto anterior ou um espaço entre as extensões.

**Criar arquivo compatível com PDF/A-1a**: força o uso da configuração de Adobe PDF de RGB PDF/A-1b:2005.

**Adicionar Marcadores ao Adobe PDF**: Converte nomes de planilhas do Excel em marcadores. Essa opção é selecionada por padrão.

**Ajustar planilha a uma única página**: reduz o tamanho do texto para ajustá-la a uma única página.

**Converter Pasta de Trabalho Inteira**: converte todas as planilhas no arquivo do Excel. Se essa opção não estiver selecionada, somente a página atual será convertida.

**Executar Macros Automaticamente**: executa todas as macros no documento do Excel (como uma macro que insere a hora atual) antes de converter o documento.

**Converter Informações do Documento**: adiciona propriedades do documento PDF com base nas informações do documento no arquivo de origem. Isso inclui informações como título do documento, autor, assunto e palavras-chave.

**Adicionar Links ao Adobe PDF**: converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**Anexar arquivo do Source ao Adobe PDF**: quando esta opção é selecionada, a planilha original do Excel é inserida como um anexo dentro do documento PDF gerado.

**Habilitar Acessibilidade e Reflow com Adobe PDF Marcado**: incorpora marcas no documento PDF para habilitar a acessibilidade e o refluxo.

**Lista De Suplementos Do Excel A Serem Carregados**: Por padrão (por motivos de segurança), nenhum suplemento do Excel é executado quando um arquivo do Excel é convertido em PDF. Para permitir que determinados suplementos do Excel sejam executados durante a conversão, forneça uma lista separada por vírgulas com os nomes dos suplementos.

**Lista De Planilhas A Serem Convertidas**: Quando esta caixa está vazia, todas as planilhas na planilha do Excel são incluídas no PDF gerado. Para converter seletivamente um subconjunto das planilhas, forneça uma lista separada por vírgulas de nomes de planilhas.

## Configurações do Microsoft PowerPoint (somente Windows) {#microsoft-powerpoint-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft PowerPoint são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Tentar OpenOffice como Conversor de Fallback]**: quando esta opção estiver selecionada e uma conversão usando o Microsoft PowerPoint falhar ou atingir o limite de tempo limite especificado, o PDF Generator tentará a conversão usando OpenOffice. Se a conversão usando OpenOffice falhar ou atingir o limite de tempo especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões de Nome de Arquivo]**: especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é ppt,pptx. Não inclua um ponto anterior ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Essa opção é selecionada por padrão.

**[!UICONTROL Adicionar Marcadores ao Adobe PDF]**: converte títulos do PowerPoint em marcadores. Essa opção é selecionada por padrão.

**[!UICONTROL Anexar arquivo Source ao Adobe PDF]**: adiciona o arquivo de origem ao arquivo PDF como anexo. Essa opção é desmarcada por padrão.

**[!UICONTROL Habilitar Acessibilidade E Reflow Com Adobe PDF Marcado]**: Incorpora marcas no arquivo PDF. Essa opção é desmarcada por padrão.

**[!UICONTROL Converter multimídia em multimídia de PDF]**: converte multimídia em multimídia de PDF, quando possível. Essa opção é selecionada por padrão.

**[!UICONTROL Converter Anotações do Orador]**: Converte anotações do orador em PDF.

**[!UICONTROL Executar Macros Automaticamente]**: executa todas as macros no documento do PowerPoint (como uma macro que insere a hora atual) antes de converter o documento.

**[!UICONTROL Layout de PDF com base nas Configurações de Impressora do PowerPoint]**: usa as configurações de impressora do PowerPoint para dispor o documento de PDF.

**[!UICONTROL Adicionar links ao Adobe PDF]**: preserva os links existentes quando o arquivo é convertido. A aparência dos links geralmente não é alterada. Os links só poderão ser criados se a opção Habilitar acessibilidade também estiver selecionada. Essa opção é desmarcada por padrão.

**[!UICONTROL Salvar Transições De Slides No Adobe PDF]**: Converte Transições De Slides. Essa opção é selecionada por padrão.

**[!UICONTROL Salvar animações no Adobe PDF]**: salva as animações convertidas no arquivo PDF.

**[!UICONTROL Converter Slides Ocultos em Páginas de PDF]**: Converte slides ocultos.

**[!UICONTROL Criar arquivo compatível com PDF/A-1a]**: força o uso da configuração de Adobe PDF de RGB PDF/A-1b:2005. Alguns recursos do PowerPoint não são convertidos quando você produz um arquivo PDF. Se uma transição do PowerPoint não tiver uma transição equivalente no Acrobat, uma transição semelhante será substituída. Se vários efeitos de animação estiverem no mesmo slide, um único efeito será usado. As transições de página e os marcadores são convertidos.

## Configurações de projeto do Microsoft (somente Windows) {#microsoft-project-settings-windows-only}

Essas opções determinam como os arquivos do Projeto do Microsoft são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

1. **[!UICONTROL Extensões de Nome de Arquivo:]** Especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `mpp`. Não inclua um ponto anterior ou um espaço entre as extensões.

1. **[!UICONTROL Converter Informações do Documento]**: adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Essa opção é selecionada por padrão.
1. **[!UICONTROL Anexar arquivo Source ao Adobe PDF]**: adiciona o arquivo de origem ao arquivo PDF como anexo.
1. **[!UICONTROL Criar arquivo compatível com PDF/A-1a]**: força o uso da configuração de Adobe PDF de RGB PDF/A-1b:2005.
1. **[!UICONTROL Executar Macros Automaticamente]**: executa qualquer macro no documento do Projeto do Microsoft (como uma macro que insere a hora atual) antes de converter o documento.

## Configurações do Microsoft Word (somente Windows) {#microsoft-word-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Word são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**[!UICONTROL Tentar OpenOffice como Conversor de Fallback]**: quando esta opção estiver selecionada e uma conversão usando o Microsoft Word falhar ou atingir o limite de tempo limite especificado, o PDF Generator tentará a conversão usando OpenOffice. Se a conversão usando OpenOffice falhar ou atingir o limite de tempo especificado, uma exceção será gravada no arquivo de log.

**[!UICONTROL Extensões de Nome de Arquivo]**: especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `doc,docx,rtf,txt`. Não inclua um ponto anterior ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Essa opção é selecionada por padrão.

**[!UICONTROL Adicionar Marcadores ao Adobe PDF]**: converte cabeçalhos em marcadores. Essa opção é selecionada por padrão.

**[!UICONTROL Anexar arquivo Source ao Adobe PDF]**: adiciona o arquivo de origem ao arquivo PDF como anexo.

**[!UICONTROL Converter Referências Cruzadas e Sumário em Links]**: Converte todas as referências cruzadas e entradas de sumário em links. Essa opção é selecionada por padrão.

**[!UICONTROL Habilitar Acessibilidade E Reflow Com Adobe PDF Marcado]**: Incorpora marcas no arquivo PDF. Essa opção é selecionada por padrão.

**[!UICONTROL Criar arquivo compatível com PDF/A-1a]**: se selecionado, força a configuração de Adobe PDF de RGB PDF/A-1b:2005 a ser usada.

**[!UICONTROL Executar Macros Automaticamente]**: executa todas as macros no documento do Word (como uma macro que insere a hora atual) antes de converter o documento.

**[!UICONTROL Preservar Marcação do Documento no Adobe PDF]**: converte a marcação no documento do Word em anotações no arquivo PDF.

**[!UICONTROL Adicionar Links ao Adobe PDF]**: converte hiperlinks no arquivo de origem em hiperlinks no documento PDF.

**[!UICONTROL Converter Links de Notas de Rodapé e Notas de Fim]**: Cria links a partir de citações de notas de rodapé e notas de fim para notas no documento PDF.

**[!UICONTROL Converter comentários exibidos em notas no Adobe PDF]**: converte comentários no documento do Word em notas de texto no documento PDF.

**[!UICONTROL Habilitar Marcação Avançada]**: adiciona marcas avançadas para acessibilidade aprimorada.

**[!UICONTROL Converter todos os estilos em marcadores]**: converte todos os estilos do documento do Word em marcadores no documento PDF.

**[!UICONTROL Converter estilos especificados em marcadores]**: converte os estilos definidos no campo **[!UICONTROL Estilos com níveis]** em marcadores no documento PDF.

**[!UICONTROL Estilos com Níveis]**: especifica quais estilos no documento do Word são convertidos em marcadores no documento PDF. Especifica também o nível dos marcadores. Para usar este recurso, desmarque a opção **[!UICONTROL Converter todos os estilos em marcadores]** e especifique os nomes dos estilos no seguinte formato:

**styleName1=level1[,styleName2=level2...]**

Se um nome de estilo do Microsoft Word incluir uma vírgula (,) ou sinal de igual (=), preceda os caracteres especiais com o caractere de escape (&quot;\_). Por exemplo, especifique um estilo chamado &quot;Título, 1&quot; como Título\, 1.

**Codificação do Acrobat PDFMaker:** Especifica o tipo de codificação dos arquivos de texto sem formatação de entrada para o Acrobat PDFMaker. Por exemplo, se estiver usando um arquivo codificado em UTF-8, selecione UTF-8 para obter melhores resultados.

## Configurações do Microsoft Visio (somente Windows) {#visio}

**Converter Informações do Documento**: adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Essa opção é selecionada por padrão. Essa opção está ativada por padrão.

**Adicionar Links Ao Adobe PDF**: Preserva todos os links. Essa opção é selecionada por padrão.

**Adicionar Marcadores ao Adobe PDF**: converte cabeçalhos em marcadores. Essa opção é selecionada por padrão.

**Anexar arquivo Source ao Adobe PDF**: adiciona o arquivo de origem ao arquivo PDF como anexo.

**Sempre Nivelar Camadas no Adobe PDF**: Nivela todas as camadas do Visio.

**Converter Todas as Páginas**: converte todas as páginas do arquivo do Visio.

**Abrir painel Camadas quando visualizado no Adobe Acrobat**: se as camadas do Visio não estiverem niveladas, abre uma janela onde você pode especificar as camadas que são preservadas no arquivo PDF quando abertas usando o Acrobat. Essa opção é selecionada por padrão.

**Criar arquivo compatível com PDF/A-1b**: força o uso da configuração de Adobe PDF PDF/A-1b:2005 (RGB).

**Converter comentários em comentários do Adobe PDF**: converte as anotações do Visio em comentários PDF.

## Configurações do Microsoft Publisher (somente Windows) {#microsoft-publisher-settings-windows-only}

Essas opções determinam como os arquivos do Microsoft Publisher são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](#create-or-edit-file-type-settings).

**[!UICONTROL Extensões de Nome de Arquivo]**: especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `pub`. Não inclua um ponto anterior ou um espaço entre as extensões.

## Configurações do AutoCAD (somente Windows) {#autocad-settings-windows-only}

Essas opções determinam como os arquivos do AutoCAD são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**[!UICONTROL Extensões de Nome de Arquivo]**: especifica as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `dwg`. Não inclua um ponto anterior ou um espaço entre as extensões.

**[!UICONTROL Converter Informações do Documento]**: adiciona informações do documento da caixa de diálogo Propriedades do arquivo de origem, incluindo título, assunto, autor, palavras-chave, gerente, empresa, categoria e comentários. Essa opção é selecionada por padrão.

**[!UICONTROL Adicionar Marcadores ao Adobe PDF]**: converte cabeçalhos em marcadores.

**[!UICONTROL Sempre Nivelar Camadas no Adobe PDF]**: Nivela todas as camadas do AutoCAD.

**[!UICONTROL Abrir painel de camadas quando visualizado no Adobe Acrobat]**: mostra a estrutura das camadas quando o PDF é aberto no Acrobat.

**[!UICONTROL Converter todos os layouts]**: inclui todos os layouts no PDF.

**[!UICONTROL Converter espaço do modelo em 3D]**: quando selecionado, o layout do espaço do modelo é convertido em uma anotação 3D no PDF.

**[!UICONTROL Adicionar Links ao Adobe PDF]**: se selecionada, preserva todos os links.

**[!UICONTROL Anexar arquivo Source ao Adobe PDF]**: adiciona o arquivo de origem ao arquivo PDF como anexo.

**[!UICONTROL Criar arquivo compatível com PDF/A-1b]**: força o uso da configuração de Adobe PDF PDF/A-1b.

**[!UICONTROL Converter todas as camadas]**: por padrão, o PDF Generator converte somente a camada padrão dos arquivos do AutoCAD em PDF em vez de todas as camadas do arquivo. Selecione essa opção para converter todas as camadas do arquivo.

**[!UICONTROL Incorporar Informações de Escala]**: Preserva as informações de escala de desenho.

**[!UICONTROL Converter layout atual]**: inclui somente o layout atual no PDF.

**[!UICONTROL Lista de layouts do AutoCAD a serem convertidos]**: um desenho do AutoCAD pode ter vários layouts. Quando esta caixa está vazia, todos os layouts no desenho do AutoCAD são incluídos no documento PDF gerado. Para converter seletivamente um subconjunto dos layouts, forneça uma lista separada por vírgulas de nomes de layout.

## Configurações do OpenOffice {#openoffice-settings}

Essas opções determinam como os arquivos OpenOffice são convertidos. Para obter instruções sobre como acessar essas opções, consulte [Criar ou editar configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#create-or-edit-file-type-settings).

**Tentar PDFMaker como Conversor de Fallback**: quando esta opção é selecionada e uma conversão usando OpenOffice falha ou atinge o limite de tempo limite especificado, o PDF Generator tenta a conversão usando o PDFMaker. Se a conversão usando o PDFMaker falhar ou atingir o tempo limite especificado, uma exceção será gravada no arquivo de log.

**Extensões de Nome de Arquivo**: especifique as extensões de nome de arquivo para tipos de arquivo, separadas por vírgulas, que são aceitas para este aplicativo. O padrão é `odt,odp,ods,odg,odf,sxw,sxi,sxd`. Não inclua um ponto anterior ou um espaço entre as extensões.

**Intervalo**: converter todas as páginas ou especificar páginas específicas ou um intervalo de páginas. Se um intervalo de páginas não estiver definido, todas as páginas serão convertidas. Para exportar um intervalo de páginas, use o formato 3-6. Para exportar páginas únicas, use o formato 7;9;11. Você pode exportar uma combinação de intervalos de páginas e páginas únicas usando um formato como 3-6;8;10;12.

**Orientação da página**: somente para arquivos de texto simples, selecione retrato ou paisagem para o documento PDF convertido.

**Imagens**: configure como as imagens são convertidas. As imagens do EPS com visualizações incorporadas são exportadas somente como visualizações. As imagens do EPS sem visualizações incorporadas são exportadas como espaços reservados vazios. Com a compactação sem perdas de imagens, todos os pixels são preservados. Com a compactação JPEG de imagens e um nível de alta qualidade, quase todos os pixels são preservados. Com um nível de baixa qualidade, alguns pixels são perdidos e artefatos são introduzidos, mas os tamanhos de arquivo são reduzidos.

**Geral**: habilite as opções para converter um PDF marcado ou exportar notas de documento do Writer e FormCalc, efeitos de transição de slides Impress ou páginas em branco para o PDF. Quando as tags são exportadas, o tamanho do arquivo pode aumentar consideravelmente. Algumas tags exportadas são sumários, hiperlinks e controles.

Você também pode especificar como os formulários são enviados. As opções são XML, FDF, PDF ou HTML. Essa configuração substitui a propriedade de URL do controle definida no documento. Somente uma configuração comum pode ser selecionada para o documento PDF:

* PDF (envia o documento inteiro)
* FDF (envia o conteúdo de controle)
* HTML
* XML

**PDF marcado**: permite a criação de PDF marcado a partir de documentos OpenOffice. O PDF marcado contém informações sobre a estrutura do conteúdo do documento. Isso pode ajudar ao exibir o documento em dispositivos com telas diferentes e ao usar um software de leitor de tela. Também ajuda o software de acessibilidade a executar várias operações úteis com o documento PDF, como ler em voz alta o conteúdo do documento PDF.

**Exportar Notas**: Converte as notas em documentos OpenOffice em notas no documento PDF gerado.

**Usar efeitos de transição**: converte os efeitos de transição de slides em apresentações de OpenOffice em efeitos de transição de PDF correspondentes.

**Enviar Forms no Formato**: cria um formulário PDF que pode ser preenchido e impresso pelo usuário do documento PDF.

**Exportar Páginas em Branco Inseridas Automaticamente**: quando esta opção é selecionada, as páginas em branco inseridas automaticamente são incluídas no documento PDF gerado. Isso é útil se você estiver imprimindo um documento PDF de frente e verso. Por exemplo, um livro pode ser configurado de modo que a primeira página do capítulo sempre comece em uma página ímpar. Se o capítulo anterior terminar em uma página ímpar, o OpenOffice inserirá uma página em branco com número par. Essa opção controla se essa página com número par deve ser incluída no PDF gerado.

## Outras configurações do aplicativo (somente Windows) {#other-applications-settings-windows-only}

Não é possível alterar as configurações de outros aplicativos por meio do console de administração; elas exibem as extensões de nome de arquivo dos tipos de arquivos compatíveis. Para obter instruções sobre como acessar essas configurações, consulte [Criar ou editar configurações de tipo de arquivo](https://help.adobe.com/en_US/AEMForms/6.1/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7e42.2.html).

* Corel WordPerfect: `wpd`
* PageMaker Adobe: `pmd, pm6, p65, pm`
* Adobe FrameMaker: `fm`
* Adobe Photoshop: `psd`

O suporte para esses tipos de arquivos pode precisar ser personalizado. Para obter mais informações, consulte &quot;Adicionando Suporte para Formatos de Arquivo Nativos Adicionais&quot; em [Programando com Formulários AEM](https://www.adobe.com/go/learn_aemforms_programming_62).

Para obter ajuda sobre como configurar uma impressora de rede PDFG, consulte [Configurando uma impressora de rede PDFG (somente Windows)](/help/forms/using/admin-help/setting-pdfg-network-printer-windows.md).
