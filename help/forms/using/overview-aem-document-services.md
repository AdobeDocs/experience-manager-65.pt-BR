---
title: Visão geral dos AEM Document Services
seo-title: Overview of AEM Document Services
description: AEM Document Services são um conjunto de serviços OSGi para criar, montar e proteger documentos do PDF.
seo-description: AEM Document Services are a set of OSGi Services for creating, assembling, and securing PDF Documents.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1402'
ht-degree: 0%

---

# Visão geral dos AEM Document Services{#overview-of-aem-document-services}

AEM Document Services são um conjunto de serviços OSGi para criar, montar e proteger documentos do PDF. Os Serviços de Documento contêm os seguintes serviços:

## Serviço de saída {#output-service}

O Serviço de saída permite criar documentos em diferentes formatos, incluindo PDF, formatos de impressora laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e PCL (Printer Control Language). A lista a seguir especifica os formatos de impressora de etiquetas:

* Zebra (ZPL)
* Intermecenas (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Um documento pode ser enviado para uma impressora de rede, para uma impressora local ou para um arquivo no sistema de arquivos. O serviço de saída mescla dados de formulário XML com um design de formulário para gerar um documento. O serviço de saída pode gerar um documento sem mesclar dados de formulário XML no documento. No entanto, o fluxo de trabalho principal está mesclando dados no documento.

>[!NOTE]
>
>Normalmente, um design de formulário é criado usando o Designer. Para obter informações sobre como criar designs de formulário para o serviço Saída, consulte a Ajuda do Designer.

Ao usar o serviço de saída para unir dados XML a um design de formulário, o resultado é um documento PDF não interativo. Um documento PDF não interativo não permite que os usuários insiram dados em seus campos. Por outro lado, é possível usar o serviço Forms para criar um formulário PDF interativo que permite que os usuários insiram dados em seus campos.

As quatro operações de serviço de Saída a seguir estão disponíveis para uso:

* **generatePDFOuput**: Une um design de formulário aos dados para gerar um documento PDF
* **generatePrintedOutput**: Mescla um design de formulário com dados de formulário para gerar um documento para enviar a uma impressora laser ou de rede de etiquetas

* **generatePDFOutputBatch**: Une vários modelos com vários registros de dados em uma única invocação para gerar um lote de arquivos PDF. Há também a opção de gerar um único PDF combinando todos os PDF
* **generatePrintedOutputBatch**: Une vários modelos com vários registros de dados em uma única invocação para gerar um lote de documentos impressos (PS,PCL,ZPL,DPL,IPL,TPCL). Há também a opção de gerar um único documento impresso.

## Serviço de Assembler {#assembler-service}

O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Cada tarefa enviada ao serviço Assembler inclui um documento XML de Descrição de Documento (DDX), documentos de origem e recursos externos (strings e gráficos). O documento DDX fornece instruções sobre como usar os documentos de origem para produzir um conjunto de documentos resultantes.

Além dos recursos acima mencionados, o serviço Assembler:

* Converte documentos PDF em PDF/A padrão.
* Transforma PDF forms, formulários XML (criados no Designer) e PDF forms (criados no Acrobat) em PDF/A-1b, PDF/A-2b e PDFA/A-3b.
* Converte documentos PDF assinados ou não (são necessárias Assinaturas Digitais).
* Valida a conformidade de um arquivo PDF/A e o converte, se necessário.

### Sobre o DDX {#about-ddx}

Ao usar o serviço Assembler, use uma linguagem baseada em XML chamada Document Description XML (DDX) para descrever a saída desejada. DDX é uma linguagem de marcação declarativa cujos elementos representam blocos de construção de documentos. Esses blocos de construção incluem documentos PDF, documentos XDP, fragmentos de formulário XDP e outros elementos, como comentários, marcadores e texto estilizado.

O documento DDX pode especificar documentos resultantes com estas características:

* Documento PDF que é montado a partir de vários documentos PDF
* Vários documentos PDF separados por um único documento PDF
* Portfolio PDF que inclui uma interface de usuário autocontida e vários documentos PDF e não PDF
* Documento XDP que é montado a partir de vários documentos XDP
* Documento XDP que contém fragmentos XML que são inseridos dinamicamente em um documento XDP
* Documento PDF que compacta um documento XDP
* Arquivos XML que relatam as características de um documento PDF. As características relatadas incluem texto, comentários, dados de formulário, anexos de arquivo, arquivos usados em Portfolio de PDF, marcadores e propriedades de PDF. As propriedades de PDF incluem propriedades de formulário, rotação de página e autor do documento.

Você pode usar DDX para aumentar documentos PDF como parte da montagem ou desmontagem do documento. Você pode especificar qualquer combinação dos seguintes efeitos:

* Adicione ou remova marcas d&#39;água ou planos de fundo nas páginas selecionadas.
* Adicione ou remova cabeçalhos e rodapés em páginas selecionadas.
* Remove a estrutura e os recursos de navegação de um PDF Package ou PDF Portfolio. O resultado é um único arquivo PDF.
* Rótulos de página de renumeração. Rótulos de página geralmente são usados para numeração de página.
* Importe metadados de outro documento de origem.
* Adicione ou remova anexos de arquivo, marcadores, links, comentários e JavaScript.
* Defina as características de visualização inicial e otimize para visualização na Web.
* Defina permissões para PDF criptografado.
* Girar páginas ou girar e girar o conteúdo nas páginas.
* Altere o tamanho das páginas selecionadas.
* Mesclar dados com um PDF baseado em XFA.

Você pode usar um mapa de entrada simples para especificar os locais dos documentos de origem e resultantes. Você também pode usar os seguintes tipos de URLs de dados externos:

* Arquivo
* FTP
* HTTP/HTTPS

## Serviço de Garantia de Doc {#doc-assurance-service}

O Serviço de garantia de documentos ajuda você a criptografar e descriptografar documentos, estender a funcionalidade do Adobe Reader com direitos de uso adicionais e adicionar assinaturas digitais aos documentos. Seus usuários podem interagir facilmente com PDF forms e documentos, enquanto sua organização melhora a segurança, o arquivamento e a conformidade.

O serviço de garantia de documentos contém três serviços: assinatura, criptografia e extensão do leitor.

### Serviço de assinatura {#signature-service}

O serviço de assinatura permite que você trabalhe com assinaturas digitais e documentos no servidor de AEM. Por exemplo, o serviço de assinatura é normalmente usado nas seguintes situações:

* O servidor de AEM certifica um formulário antes de ele ser enviado a um usuário para ser aberto usando o Acrobat ou o Adobe Reader.
* O servidor de AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
* O servidor AEM assina um formulário em nome de um notário público.

O serviço de assinatura acessa certificados e credenciais armazenadas no armazenamento de confiança.

### Serviço de criptografia {#encryption-service}

O serviço Encryption permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. Você pode criptografar todo o documento do PDF (incluindo seu conteúdo, metadados e anexos), tudo menos seus metadados ou apenas os anexos. Um usuário autorizado pode descriptografar o documento para obter acesso a seu conteúdo. Se um documento do PDF for criptografado com uma senha, o usuário deverá especificar a senha de abertura para que o documento possa ser visualizado no Adobe Reader ou Acrobat. Se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com uma chave privada (certificado). A chave privada usada para descriptografar o documento PDF deve corresponder à chave pública usada para criptografá-lo.

### Serviço de extensão do Reader {#reader-extension-service}

O serviço Reader Extensions permite que sua organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço Reader Extensions funciona com o Adobe Reader 7.0 ou posterior. O serviço adiciona direitos de uso a um documento PDF. Essa ação ativa recursos que geralmente não estão disponíveis quando um documento do PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não exigem software ou plug-ins adicionais para trabalhar com documentos ativados por direitos.

Quando os documentos do PDF têm os direitos de uso apropriados adicionados, os recipients podem realizar as seguintes atividades no Adobe Reader:

* Preencha os documentos e formulários PDF on-line ou off-line, permitindo que os destinatários salvem cópias localmente para seus registros e ainda mantenham as informações adicionadas intactas
* Salve documentos do PDF em um disco rígido local para manter o documento original e quaisquer comentários, dados ou anexos adicionais
* Anexar arquivos e clipes de mídia a documentos PDF
* Assinar, certificar e autenticar documentos do PDF aplicando assinaturas digitais usando tecnologias PKI (Public Key Infrastructure, infraestrutura de chave pública) padrão do setor
* Enviar documentos PDF preenchidos ou anotados eletronicamente
* Use documentos e formulários PDF como um front-end de desenvolvimento intuitivo para bancos de dados internos e serviços da Web
* Compartilhe documentos do PDF com outras pessoas para que os revisores possam adicionar comentários usando ferramentas de marcação intuitivas. Essas ferramentas incluem notas autoadesivas eletrônicas, carimbos, destaques e tachado de texto. As mesmas funções estão disponíveis no Acrobat.
* Suporte à decodificação de formulários com códigos de barras.

Esses recursos especiais do usuário são ativados automaticamente quando um documento do PDF habilitado para direitos é aberto no Adobe Reader. Quando o usuário terminar de trabalhar com um documento habilitado para direitos, essas funções serão novamente desativadas no Adobe Reader. Eles permanecem desativados até que o usuário receba outro documento de PDF habilitado para direitos.

Imediatamente, o serviço DocAssurance não está disponível para uso. Para configurar o serviço DocAssurance, consulte [Instalar e configurar serviços de documento](../../forms/using/install-configure-document-services.md).

## Enviar para o serviço de impressora {#send-to-printer-service}

O serviço Enviar para impressora fornece a API para enviar documentos para a impressora especificada para impressão.
