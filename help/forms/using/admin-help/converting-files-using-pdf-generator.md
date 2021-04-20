---
title: Conversão de arquivos usando o Gerador de PDF
seo-title: Conversão de arquivos usando o Gerador de PDF
description: Saiba como converter arquivos usando o Gerador de PDF.
seo-description: Saiba como converter arquivos usando o Gerador de PDF.
uuid: 295afb8f-130a-44f5-b0ab-e4c93c0c9e52
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 999ae2be-56ba-48c1-861b-8d4c991a0206
feature: PDF Generator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 0%

---


# Conversão de arquivos usando o Gerador de PDF{#converting-files-using-pdf-generator}

Você pode usar as páginas da Web do Gerador de PDF para converter arquivos.

## Criar um arquivo PDF {#create-a-pdf-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Criar PDF.
1. Clique em Procurar para localizar e selecionar o arquivo.

   >[!NOTE]
   >
   >O PDF Generator é capaz de detectar automaticamente o tipo de arquivo de arquivos .doc, .xls, .ppt e .rtf, mesmo quando o nome do arquivo não tem a extensão de arquivo. Esse recurso não funciona com arquivos .docx, .xlsx e .pptx.

1. Em Configurações, selecione Usar configurações personalizadas ou Fazer upload de arquivo de configurações.

   * Se você estiver usando configurações personalizadas, selecione uma configuração de Adobe PDF, uma configuração de segurança e uma configuração de tipo de arquivo e especifique um tempo limite.

      As configurações do Adobe PDF são aplicáveis somente a conversões PS para PDF, EPS para PDF, PRN para PDF, Imagem para PDF com OCR e nativo para PDF. A configuração de tempo limite especifica o tempo máximo que a conversão leva para ser concluída. O padrão é 270 segundos. Essas configurações não são usadas durante conversões Imagem para PDF e OpenOffice-para-PDF.

   * Se você estiver carregando um arquivo de configurações, digite seu caminho e nome na caixa ou clique em Procurar para localizar e selecionar o arquivo.

1. (Opcional) Em XMP Arquivo de metadados, digite o caminho e o nome do arquivo de XMP ou clique em Procurar para localizar e selecionar o arquivo. Um arquivo de XMP pode ser usado para incluir informações de metadados padrão. (Consulte [Sobre XMP arquivos](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Clique em Criar. Quando o arquivo é criado, um link para ele é exibido. Se ocorrer um erro durante a conversão, um aviso será exibido. Se você estiver criando um arquivo Postscript, o aviso também conterá um link para o arquivo de log.
1. Clique no link do arquivo PDF. O arquivo é aberto no Acrobat.

### Sobre arquivos XMP {#about-xmp-files}

Os documentos PDF criados pelo Gerador de PDF no Acrobat 5.0 ou posterior contêm metadados de documento no formato XML. ** Metadados inclui informações sobre o documento e seu conteúdo, como o nome do autor, palavras-chave e informações de direitos autorais que os utilitários de pesquisa podem usar.

Os metadados do documento contêm (mas não se limitam a) informações que também aparecem na guia Descrição da caixa de diálogo Propriedades do documento no Acrobat. As alterações feitas na guia Descrição são refletidas nos metadados do documento. Os metadados do documento podem ser estendidos e modificados com produtos de terceiros.

A Adobe Extensible Metadata Platform (XMP) fornece aos aplicativos do Adobe uma estrutura XML comum que padroniza a criação, o processamento e o intercâmbio de metadados de documentos entre fluxos de trabalho de publicação. Você pode salvar e importar o código-fonte XML de metadados de documento em XMP formato, facilitando o compartilhamento de metadados entre vários documentos. Para obter mais informações sobre XMP arquivos, consulte [Plataforma de Metadados Extensível (XMP)](https://www.adobe.com/products/xmp/) e [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html).

Você pode criar arquivos XMP no Acrobat.

## Converter um arquivo HTML ou arquivo ZIP em PDF {#convert-an-html-file-or-zip-file-to-pdf}

Você pode usar o Gerador de PDF para converter os seguintes tipos de arquivos no Adobe PDF:

* Arquivos HTML, que podem ser convertidos ao carregar um arquivo HTML ou especificar o URL de uma página da Web ou site.
* Arquivos arquivados (ZIP), que podem conter arquivos HTML, arquivos de imagem ou ambos.

Se o arquivo ZIP contiver mais de um arquivo HTML no nível mais baixo de sua hierarquia de pastas, o arquivo ZIP também deverá conter um arquivo index.htm ou index.html.

>[!NOTE]
>
>* O recurso HTML para PDF requer determinadas fontes no diretório de fontes do sistema. Nos sistemas Linux, Solaris e AIX, o diretório de fontes do sistema deve conter a fonte Courier. Em sistemas Windows, o diretório de fontes do sistema deve conter Times New Roman.
   >
   >
* (Somente no sistema baseado em UNIX) Uma das seguintes fontes japonesas deve estar disponível no servidor do AEM Forms para converter uma página da Web com fonte japonesa em um documento PDF.
   >
   >  
* &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Gothic Pro-VI&quot;
>  * &quot;Kozuka Mincho Pro-VI&quot;
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * &quot;Sazanami Mincho&quot;
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;

   >
   >
* Para fazer upload de um arquivo do sistema de arquivos local, use a opção Fazer upload do arquivo na página HTML para PDF.


1. No console de administração, clique em Serviços > Gerador de PDF > HTML para PDF.
1. Especifique o arquivo para converter executando uma das seguintes tarefas:

   * Em Fazer upload do arquivo, digite o caminho e o nome do arquivo HTML ou arquivo ZIP, ou clique em Procurar para localizar e selecioná-lo.
   * Na caixa Especificar URL, digite o URL da página ou do site a ser convertido.

   >[!NOTE]
   >
   >O arquivo que você está convertendo deve ter uma extensão de nome de arquivo .html, .htm ou .zip.

1. Especifique as configurações:

   * Para usar configurações personalizadas, selecione Usar configurações personalizadas, especifique as configurações de segurança e tipo de arquivo e especifique um valor de tempo limite. O valor padrão é 270 segundos.
   >[!NOTE]
   >
   >Se você tiver configurado o serviço Gerar PDF para usar o Acrobat WebCapture, as Configurações de tipo de arquivo selecionadas nesta página não afetarão o PDF produzido. Em vez disso, faça as alterações apropriadas na versão do Acrobat que está instalada no servidor.

   * Para usar um arquivo de configurações existente, selecione Fazer upload do arquivo de configurações e clique em Procurar para ir para o local do arquivo.


1. Para carregar um arquivo de XMP, clique em Procurar e vá para o local do arquivo. Um arquivo de XMP pode ser usado para incluir informações de metadados padrão. (Consulte [Sobre XMP arquivos](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Clique em Criar. Quando o arquivo é criado, um link para o arquivo PDF é exibido.
1. Clique no link para exibir o documento PDF no Acrobat.

## Exportar um arquivo PDF para outro formato de arquivo (somente Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

Você pode exportar arquivos PDF para vários formatos de arquivo, conforme descrito no capítulo Gerar serviço PDF de [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

1. No console de administração, clique em Serviços > Gerador de PDF > Export PDF.
1. Clique em Procurar para localizar o arquivo PDF a ser exportado.
1. Na lista Export PDF file to , selecione o formato para exportar o arquivo PDF.
1. Na caixa Especificar um tempo limite, digite o tempo de espera antes que o aplicativo atinja o tempo limite. O valor padrão é 270 segundos.

   O Tempo de conversão exibido quando o arquivo é convertido pode ser maior que o valor especificado aqui. O Tempo de conversão inclui o tempo gasto aguardando o encadeamento ou o processo, o tempo gasto para converter o arquivo e o tempo gasto pelo conversor de fallback (se aplicável). time. O valor Especificar um tempo limite é apenas o tempo gasto para converter o arquivo.

1. (Opcional) Na opção **Especificar perfil de comprovação personalizado**, clique em Procurar e selecione um [perfil de comprovação personalizado](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). Os perfis de comprovação são usados somente durante a conversão de documentos em formato PDF (PDF/A).
1. Clique em Exportar. Quando a conversão for concluída, um link para o arquivo exportado será exibido.
1. Clique no link para exibir o arquivo convertido.

## Otimizar um PDF (somente Windows) {#optimize-a-pdf}

O PDF Generator suporta a redução do tamanho dos arquivos PDF.

>[!NOTE]
>
>Otimizar um documento assinado digitalmente remove e invalida as assinaturas digitais.

1. No console de administração, clique em Serviços > Gerador de PDF > Optimize PDF.
1. Clique em Procurar para localizar o arquivo PDF a ser otimizado.
1. Especifique as configurações:

   * Para usar configurações personalizadas, selecione Usar configurações personalizadas, especifique as configurações de tipo de arquivo e especifique um valor de tempo limite. O valor padrão é 270 segundos.
   * Para usar um arquivo de configurações existente, selecione Fazer upload do arquivo de configurações e clique em Procurar para ir para o local do arquivo.

1. Clique em Criar.

