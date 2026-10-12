---
title: Visão geral dos serviços de documento da AEM
description: Os Serviços de documento da AEM são um conjunto de Serviços OSGi para criar, montar e proteger Documentos do PDF.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services,Reader Extensions, Forms Service,PDF Generator
exl-id: 4c8a3877-1a3c-410d-ad1f-69c73ba4fcc1
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 621ad6f8-3769-57bb-838c-1d26cfb18d50
    internal-label: Reader Extensions
  - id: b59c0486-3350-52ed-8816-e0a8e11486b8
    internal-label: Forms Service
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 1%
---
# Visão geral dos serviços de documento da AEM{#overview-of-aem-document-services}

| Versão | Link do artigo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Clique aqui](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html) |
| AEM 6.5 | Este artigo |


Os Serviços de documento da AEM são um conjunto de Serviços OSGi para criar, montar e proteger Documentos do PDF. Os Serviços de documento contêm os seguintes serviços:

## Serviço de saída {#output-service}

O Output Service permite criar documentos em diferentes formatos, incluindo PDF, formatos de impressora a laser e formatos de impressora de etiquetas. Os formatos de impressora a laser são PostScript e PCL (Printer Control Language). A lista a seguir especifica os formatos de impressora de etiquetas:

* Zebra (ZPL)
* Intermec (IPL)
* Datamax (DPL)
* TecToshiba (TPCL)

Um documento pode ser enviado para uma impressora de rede, uma impressora local ou um arquivo no sistema de arquivos. O serviço de Saída mescla dados de formulário XML com um design de formulário para gerar um documento. O Serviço de saída pode gerar um documento sem mesclar dados de formulário XML no documento. No entanto, o fluxo de trabalho principal é a mesclagem de dados no documento.

>[!NOTE]
>
>Um design de formulário é normalmente criado usando o Designer. Para obter informações sobre como criar designs de formulário para o Serviço de saída, consulte a Ajuda do Designer.

Ao usar o Serviço de saída para mesclar dados XML com um design de formulário, o resultado é um documento PDF não interativo. Um documento não interativo do PDF não permite que os usuários insiram dados em seus campos. Por outro lado, você pode usar o serviço Forms para criar um formulário interativo do PDF que permita aos usuários inserir dados em seus campos.

As quatro operações de Serviço de saída a seguir estão disponíveis para uso:

* **generatePDFOuput**: mescla um design de formulário com dados para gerar um documento do PDF
* **generatePrintedOutput**: mescla um design de formulário com dados de formulário para gerar um documento para enviar a uma impressora laser ou a uma impressora de rede de etiquetas

* **generatePDFOutputBatch**: mescla vários modelos com vários registros de dados em uma única invocação para gerar um lote de arquivos do PDF. Também há a opção de gerar uma única PDF combinando todos os PDFs
* **generatePrintedOutputBatch**: mescla vários modelos com vários registros de dados em uma única invocação para gerar um lote de documentos de impressão (PS,PCL,ZPL,DPL,IPL,TPCL). Há também a opção de gerar um único documento de impressão.

## Serviço Assembler {#assembler-service}

O serviço Assembler permite combinar, reorganizar e aumentar documentos PDF e XDP e obter informações sobre documentos PDF. Cada tarefa enviada ao serviço Assembler inclui um documento XML de Descrição de Documento (DDX), documentos de origem e recursos externos (sequências e gráficos). O documento DDX fornece instruções sobre como usar os documentos de origem para produzir um conjunto de documentos resultantes.

Além dos recursos mencionados acima, o serviço Assembler:

* Converte documentos do PDF para o padrão PDF/A.
* Transforma o PDF forms, formulários XML (criados no Designer) e PDF forms (criados no Acrobat) em PDF/A-1b, PDF/A-2b e PDFA/A-3b.
* Converte documentos do PDF assinados ou não (assinaturas digitais são necessárias).
* Valida a conformidade de um arquivo PDF/A e o converte, se necessário.

### Sobre o DDX {#about-ddx}

Ao usar o serviço Assembler, use uma linguagem baseada em XML chamada Document Description XML (DDX) para descrever a saída desejada. O DDX é uma linguagem de marcação declarativa cujos elementos representam os blocos fundamentais de documentos. Esses blocos fundamentais incluem documentos PDF, documentos XDP, fragmentos de formulário XDP e outros elementos, como comentários, marcadores e texto estilizado.

O documento DDX pode especificar documentos resultantes com estas características:

* Documento do PDF que é montado a partir de vários documentos do PDF
* Vários documentos do PDF separados por um único documento do PDF
* PDF Portfolio, que inclui uma interface de usuário independente e vários documentos PDF e não PDF
* Documento XDP montado a partir de vários documentos XDP
* Documento XDP que contém fragmentos XML inseridos dinamicamente em um documento XDP
* Documento do PDF que empacota um documento XDP
* Arquivos XML que relatam as características de um documento do PDF. As características relatadas incluem texto, comentários, dados de formulário, anexos de arquivo, arquivos usados em portfólios do PDF, marcadores e propriedades do PDF. As propriedades do PDF incluem propriedades de formulário, rotação de página e autor de documento.

Você pode usar o DDX para aumentar documentos do PDF como parte da montagem ou desmontagem de documentos. Você pode especificar qualquer combinação dos seguintes efeitos:

* Adicionar ou remover marcas d&#39;água ou planos de fundo em páginas selecionadas.
* Adicionar ou remover cabeçalhos e rodapés nas páginas selecionadas.
* Remove a estrutura e os recursos de navegação de um Pacote do PDF ou PDF Portfolio. O resultado é um único arquivo PDF.
* Renumerar rótulos de página. Os rótulos de página normalmente são usados para numeração de páginas.
* Importar metadados de outro documento de origem.
* Adicione ou remova anexos de arquivo, marcadores, links, comentários e JavaScript.
* Defina as características de exibição iniciais e otimize para visualização na Web.
* Definir permissões para PDF criptografado.
* Girar páginas ou girar e deslocar o conteúdo nas páginas.
* Alterar o tamanho das páginas selecionadas.
* Mescle dados com uma PDF baseada em XFA.

Você pode usar um mapa de entrada simples para especificar os locais dos documentos de origem e resultantes. Você também pode usar os seguintes tipos de URL de dados externos:

* Arquivo
* FTP
* HTTP/HTTPS

## Serviço Doc Assurance {#doc-assurance-service}

O Doc Assurance Service ajuda a criptografar e descriptografar documentos, estender a funcionalidade do Adobe Reader com direitos de uso adicionais e adicionar assinaturas digitais aos documentos. Seus usuários podem interagir facilmente com o PDF forms e documentos, enquanto sua organização melhora a segurança, o arquivamento e a conformidade.

O serviço Doc Assurance contém três serviços: assinatura, criptografia e extensão do leitor.

### Serviço de assinatura {#signature-service}

O serviço de assinatura permite trabalhar com assinaturas digitais e documentos no servidor do AEM. Por exemplo, o serviço de Assinatura é normalmente usado nas seguintes situações:

* O servidor do AEM certifica um formulário antes que ele seja enviado a um usuário para ser aberto usando o Acrobat ou o Adobe Reader.
* O servidor do AEM valida uma assinatura que foi adicionada a um formulário usando o Acrobat ou o Adobe Reader.
* O servidor do AEM assina um formulário em nome de um notário público.

O serviço de Assinatura acessa certificados e credenciais armazenados no armazenamento de confiança.

### Serviço de criptografia {#encryption-service}

O serviço de criptografia permite criptografar e descriptografar documentos. Quando um documento é criptografado, seu conteúdo fica ilegível. Você pode criptografar todo o documento do PDF (incluindo seu conteúdo, metadados e anexos), tudo exceto seus metadados ou apenas os anexos. Um usuário autorizado pode descriptografar o documento para obter acesso ao conteúdo. Se um documento do PDF for criptografado com uma senha, o usuário deverá especificar a senha aberta para que o documento possa ser visualizado no Adobe Reader ou no Acrobat. Se um documento do PDF for criptografado com um certificado, o usuário deverá descriptografar o documento do PDF com uma chave privada (certificado). A chave privada usada para descriptografar o documento do PDF deve corresponder à chave pública usada para criptografá-lo.

### Serviço de extensão do Reader {#reader-extension-service}

O serviço Reader Extensions permite que sua organização compartilhe facilmente documentos interativos do PDF, estendendo a funcionalidade do Adobe Reader com direitos de uso adicionais. O serviço Reader Extensions funciona com o Adobe Reader 7.0 ou posterior. O serviço adiciona direitos de uso a um documento do PDF. Essa ação ativa recursos que geralmente não estão disponíveis quando um documento do PDF é aberto usando o Adobe Reader, como adicionar comentários a um documento, preencher formulários e salvar o documento. Usuários de terceiros não precisam de software ou plug-ins adicionais para trabalhar com documentos habilitados por direitos.

Quando os documentos do PDF têm os direitos de uso apropriados adicionados, os recipients podem fazer as seguintes atividades no Adobe Reader:

* Preencha os documentos e formulários do PDF on-line ou off-line, permitindo que os recipients salvem cópias localmente para seus registros e ainda mantenham as informações adicionadas intactas
* Salve documentos do PDF em um disco rígido local para manter o documento original e quaisquer comentários, dados ou anexos adicionais
* Anexar arquivos e clipes de mídia a documentos do PDF
* Assine, certifique e autentique documentos do PDF aplicando assinaturas digitais usando tecnologias de infraestrutura de chave pública (PKI) padrão do setor
* Enviar documentos do PDF preenchidos ou anotados eletronicamente
* Use documentos e formulários do PDF como um front-end de desenvolvimento intuitivo para bancos de dados internos e serviços da Web
* Compartilhe documentos do PDF com outras pessoas para que os revisores possam adicionar comentários usando ferramentas de marcação intuitivas. Essas ferramentas incluem notas adesivas eletrônicas, carimbos, destaques e tachado de texto. As mesmas funções estão disponíveis no Acrobat.
* Suporte para decodificação de formulários com código de barras.

Esses recursos especiais do usuário são ativados automaticamente quando um documento do PDF habilitado para direitos é aberto no Adobe Reader. Quando o usuário terminar de trabalhar com um documento habilitado para direitos, essas funções serão novamente desabilitadas no Adobe Reader. Eles permanecem desativados até que o usuário receba outro documento do PDF com direitos ativados.

Imediatamente, o serviço DocAssurance não está disponível para uso. Para configurar o serviço DocAssurance, consulte [Instalação e Configuração de Serviços de Documento](../../forms/using/install-configure-document-services.md).

## Enviar para Serviço de Impressora {#send-to-printer-service}

Enviar para Serviço de Impressora fornece API para Enviar documentos para impressora especificada para impressão.
