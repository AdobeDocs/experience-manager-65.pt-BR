---
title: Visão geral dos serviços AEM Documentos
seo-title: Visão geral dos serviços AEM Documentos
description: Os Serviços de Documento AEM são um conjunto de Serviços OSGi para criar, montar e proteger Documentos PDF.
seo-description: Os Serviços de Documento AEM são um conjunto de Serviços OSGi para criar, montar e proteger Documentos PDF.
uuid: 439144b7-f805-4819-9ed9-a6e9e374b5ed
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 10d406db-ac10-479b-b08b-d0735116a12b
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 0%

---


# Visão geral dos serviços de Documento AEM{#overview-of-aem-document-services}

Os Serviços de Documento AEM são um conjunto de Serviços OSGi para criar, montar e proteger Documentos PDF. Os Serviços de documento contêm os seguintes serviços:

## Serviço de Saída {#output-service}

O serviço de Saída permite que você crie documentos em diferentes formatos, incluindo PDF, formatos de impressora a laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e Printer Control Language (PCL). A lista a seguir especifica formatos de impressora de etiquetas:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Um documento pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo no sistema de arquivos. O serviço de Saída mescla dados de formulário XML com um design de formulário para gerar um documento. O serviço de Saída pode gerar um documento sem unir dados de formulário XML ao documento. No entanto, o fluxo de trabalho principal está mesclando dados no documento.

>[!NOTE]
>
>Normalmente, um design de formulário é criado usando o Designer. Para obter informações sobre como criar designs de formulário para o serviço de Saída, consulte Ajuda do Designer.

Ao usar o serviço de Saída para unir dados XML a um design de formulário, o resultado é um documento PDF não interativo. Um documento PDF não interativo não permite que os usuários digitem dados em seus campos. Por outro lado, você pode usar o serviço Forms para criar um formulário PDF interativo que permite que os usuários digitem dados em seus campos.

As quatro operações de serviço de Saída a seguir estão disponíveis para uso:

* **generatePDFOuput**: Mescla um design de formulário com dados para gerar um documento PDF
* **generatePrintedOutput**: Une um design de formulário com dados de formulário para gerar um documento para enviar a uma impressora laser ou a uma impressora de rede de etiquetas

* **generatePDFOutputBatch**: Une vários modelos com vários registros de dados em uma única invocação para gerar um lote de arquivos PDF. Também há a opção de gerar um único PDF combinando todos os PDFs
* **generatePrintedOutputBatch**: Une vários modelos com vários registros de dados em uma única invocação para gerar um lote de documentos de impressão (PS, PCL, ZPL, DPL, IPL, TPCL). Há também a opção de gerar um único documento de impressão.

## Serviço de Assembler {#assembler-service}

O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Cada tarefa enviada ao serviço Assembler inclui um documento XML de Descrição do Documento (DDX), documentos de origem e recursos externos (strings e gráficos). O documento DDX fornece instruções sobre como usar os documentos de origem para produzir um conjunto de documentos resultantes.

Além das capacidades acima mencionadas, o serviço Assembler:

* Converte documentos PDF em PDF/A padrão.
* Transforma PDF forms, formulários XML (criados no Designer) e PDF forms (criados no Acrobat) em PDF/A-1b, PDF/A-2b e PDF/A-3b.
* Converte documentos PDF assinados ou não assinados (Assinaturas digitais necessárias).
* Valida a conformidade de um arquivo PDF/A e o converte, se necessário.

### Sobre o DDX {#about-ddx}

Ao usar o serviço Assembler, use uma linguagem baseada em XML chamada XML de Descrição do Documento (DDX) para descrever a saída desejada. DDX é uma linguagem de marcação declarativa cujos elementos representam blocos componentes de documentos. Esses blocos componentes incluem documentos PDF, documentos XDP, fragmentos de formulário XDP e outros elementos, como comentários, marcadores e texto estilizado.

O documento DDX pode especificar documentos resultantes com essas características:

* DOCUMENTO PDF que é montado a partir de vários documentos PDF
* Vários documentos PDF separados por um único documento PDF
* PORTFOLIO PDF que inclui uma interface de usuário independente e vários documentos PDF e não PDF
* Documento XDP montado em vários documentos XDP
* Documento XDP que contém fragmentos XML que são inseridos dinamicamente em um documento XDP
* DOCUMENTO PDF que empacota um documento XDP
* Arquivos XML que relatam as características de um documento PDF. As características reportadas incluem texto, comentários, dados de formulário, anexos de arquivo, arquivos usados em Portfolio PDF, marcadores e propriedades de PDF. As propriedades do PDF incluem propriedades de formulário, rotação de página e autor de documento.

Você pode usar o DDX para aumentar documentos PDF como parte da montagem ou desmontagem do documento. É possível especificar qualquer combinação dos seguintes efeitos:

* Adicione ou remova marcas d&#39;água ou planos de fundo em páginas selecionadas.
* Adicione ou remova cabeçalhos e rodapés de páginas selecionadas.
* Remove a estrutura e os recursos de navegação de um Pacote PDF ou Portfolio PDF. O resultado é um único arquivo PDF.
* Rótulos de página de renumeração. Rótulos de página geralmente são usados para numeração de página.
* Importe metadados de outro documento de origem.
* Adicione ou remova anexos de arquivos, marcadores, links, comentários e JavaScript.
* Defina as características da visualização inicial e otimize para exibição na Web.
* Defina permissões para PDF criptografado.
* Gire páginas ou gire e alterne o conteúdo das páginas.
* Alterar o tamanho das páginas selecionadas.
* Mesclar dados com um PDF baseado em XFA.

Você pode usar um mapa de entrada simples para especificar os locais dos documentos de origem e resultantes. Você também pode usar os seguintes tipos de URL de dados externos:

* Arquivo
* FTP
* HTTP/HTTPS

## Serviço de Garantia de Documento {#doc-assurance-service}

O Serviço de Garantia de Documento ajuda você a criptografar e descriptografar documentos, estender a funcionalidade do Adobe Reader com direitos de uso adicionais e adicionar assinaturas digitais aos documentos. Seus usuários podem interagir facilmente com PDF forms e documentos, enquanto sua organização melhora a segurança, o arquivamento e a conformidade.

O serviço de Garantia de Documento contém três serviços: assinatura, criptografia e extensão do leitor.

### Serviço de assinatura {#signature-service}

O serviço de assinatura permite que você trabalhe com assinaturas e documentos digitais no servidor AEM. Por exemplo, o serviço de assinatura é normalmente usado nas seguintes situações:

* O servidor AEM certifica um formulário antes de ele ser enviado para um usuário abrir usando o Acrobat ou o Adobe Reader.
* O servidor AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
* O servidor AEM assina um formulário em nome de um notário público.

O serviço de assinatura acessa certificados e credenciais armazenados no repositório de confiança.

### Serviço de criptografia {#encryption-service}

O serviço de criptografia permite que você criptografe e descriptografe documentos. Quando um documento é criptografado, seu conteúdo se torna ilegível. É possível criptografar todo o documento PDF (incluindo seu conteúdo, metadados e anexos), tudo o que não seja seus metadados ou apenas os anexos. Um usuário autorizado pode descriptografar o documento para obter acesso ao seu conteúdo. Se um documento PDF for criptografado com uma senha, o usuário deverá especificá-la antes que o documento possa ser visualizado no Adobe Reader ou Acrobat. Se um documento PDF for criptografado com um certificado, o usuário deverá descriptografar o documento PDF com uma chave privada (certificado). A chave privada usada para descriptografar o documento PDF deve corresponder à chave pública usada para criptografá-lo.

### Serviço de Extensão do Reader {#reader-extension-service}

O serviço Extensões de Reader permite que sua organização compartilhe facilmente documentos PDF interativos estendendo a funcionalidade da Adobe Reader com direitos de uso adicionais. O serviço Extensões do Reader funciona com o Adobe Reader 7.0 ou posterior. O serviço adiciona direitos de uso a um documento PDF. Essa ação ativa recursos que geralmente não estão disponíveis quando um documento PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não precisam de software ou plug-ins adicionais para trabalhar com documentos habilitados para direitos.

Quando documentos PDF tiverem os direitos de uso apropriados adicionados, os recipient poderão fazer as seguintes atividades no Adobe Reader:

* Preencha documentos PDF e formulários online ou offline, permitindo que recipient salvem cópias localmente para seus registros e ainda mantenham informações adicionadas intactas
* Salve documentos PDF em um disco rígido local para manter o documento original e quaisquer comentários, dados ou anexos adicionais
* Anexar arquivos e clipes de mídia a documentos PDF
* Assine, certifique e autentique documentos PDF aplicando assinaturas digitais usando tecnologias PKI (Public Key Infrastructure — Infraestrutura de Chaves Públicas) padrão do setor
* Enviar documentos PDF concluídos ou anotados eletronicamente
* Use documentos e formulários PDF como um front-end de desenvolvimento intuitivo para bancos de dados internos e serviços da Web
* Compartilhe documentos PDF com outras pessoas para que os revisores possam adicionar comentários usando ferramentas de marcação intuitivas. Essas ferramentas incluem notas adesivas eletrônicas, carimbos, destaques e tachado de texto. As mesmas funções estão disponíveis no Acrobat.
* Oferece suporte à decodificação de formulários com códigos de barras.

Esses recursos especiais do usuário são ativados automaticamente quando um documento PDF com direitos ativados é aberto no Adobe Reader. Quando o usuário terminar de trabalhar com um documento habilitado para direitos, essas funções serão novamente desativadas no Adobe Reader. Elas permanecem desativadas até que o usuário receba outro documento PDF com direitos ativados.

O serviço DocAssurance não está disponível para uso. Para configurar o serviço DocAssurance, consulte [Instalando e Configurando Serviços de Documento](../../forms/using/install-configure-document-services.md).

## Enviar para o serviço de impressora {#send-to-printer-service}

O serviço Enviar para impressora fornece a API para enviar documentos para a impressora especificada para impressão.
