---
title: Conversão de arquivos usando o PDF Generator
description: O serviço PDF Generator converte formatos de arquivo nativos em PDF. Ele também converte o PDF para outros formatos de arquivo e otimiza o tamanho dos documentos PDF.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 0%

---

# Conversão de arquivos usando o PDF Generator{#converting-files-using-pdf-generator}

Você pode usar as páginas da Web do PDF Generator para converter arquivos.

## Criar um arquivo PDF {#create-a-pdf-file}

1. No console de administração, clique em Serviços > PDF Generator > Criar PDF.
1. Clique em Procurar para localizar e selecionar o arquivo.

   >[!NOTE]
   >
   >O PDF Generator é capaz de detectar automaticamente o tipo de arquivo .doc, .xls, .ppt e .rtf, mesmo quando o nome do arquivo não tem a extensão. Esse recurso não funciona com arquivos .docx, .xlsx e .pptx.

1. Em Configurações, selecione Usar configurações personalizadas ou Fazer upload do arquivo de configurações.

   * Se você estiver usando configurações personalizadas, selecione uma configuração do Adobe PDF, uma configuração de segurança e uma configuração de tipo de arquivo e especifique um tempo limite.

     As configurações do Adobe PDF são aplicáveis somente às conversões de PS para PDF, EPS para PDF, PRN para PDF, Imagem para PDF com OCR ativado e Nativo para PDF. A configuração de tempo limite especifica o tempo máximo que a conversão leva para ser concluída. O padrão é 270 segundos. Essas configurações não são usadas durante as conversões de imagem para PDF e de OpenOffice para PDF.

   * Se você estiver fazendo upload de um arquivo de configurações, digite o caminho e o nome na caixa ou clique em Procurar para localizar e selecionar o arquivo.

1. (Opcional) Em Arquivo de metadados XMP, digite o caminho e o nome do arquivo XMP ou clique em Procurar para localizar e selecionar o arquivo. Um arquivo XMP pode ser usado para incluir informações de metadados padrão. (Consulte [Sobre arquivos XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Clique em Criar. Quando o arquivo for criado, será exibido um link para ele. Se ocorrer um erro durante a conversão, um aviso será exibido. Se você estiver criando um arquivo Postscript, o aviso também conterá um link para o arquivo de log.
1. Clique no link para o arquivo PDF. O arquivo é aberto no Acrobat.

### Sobre arquivos XMP {#about-xmp-files}

os documentos PDF criados pelo PDF Generator no Acrobat 5.0 ou posterior contêm metadados de documento no formato XML. *Metadados* inclui informações sobre o documento e seu conteúdo, como nome do autor, palavras-chave e informações de copyright que os utilitários de pesquisa podem usar.

Os metadados do documento contêm (mas não se limitam a) informações que também aparecem na guia Descrição da caixa de diálogo Propriedades do documento no Acrobat. As alterações feitas na guia Descrição são refletidas nos metadados do documento. Os metadados de documentos podem ser estendidos e modificados usando produtos de terceiros.

A Plataforma de metadados extensíveis do Adobe (XMP) fornece aos aplicativos Adobe uma estrutura XML comum que padroniza a criação, o processamento e a troca de metadados de documentos em fluxos de trabalho de publicação. É possível salvar e importar o código-fonte XML de metadados do documento no formato XMP, facilitando o compartilhamento de metadados entre vários documentos. Para obter mais informações sobre arquivos XMP, consulte [Plataforma de metadados extensível (XMP)](https://www.adobe.com/products/xmp/) e [Centro de desenvolvedores do Adobe XMP](https://www.adobe.com/devnet/xmp.html).

Você pode criar arquivos XMP no Acrobat.

## Converter um arquivo HTML ou ZIP em PDF {#convert-an-html-file-or-zip-file-to-pdf}

Você pode usar o PDF Generator para converter os seguintes tipos de arquivos para o Adobe PDF:

* arquivos HTML, que podem ser convertidos por upload de um arquivo HTML ou especificando o URL de uma página da Web ou site.
* Arquivos compactados (ZIP), que podem conter arquivos HTML, arquivos de imagem ou ambos.

Se o arquivo ZIP contiver mais de um arquivo HTML no nível mais baixo de sua hierarquia de pastas, o arquivo ZIP também deverá conter um arquivo index.htm ou index.html.

>[!NOTE]
>
>* O recurso HTML para PDF exige determinadas fontes no diretório de fontes do sistema. Nos sistemas Linux, Solaris e AIX, o diretório de fontes do sistema deve conter a fonte Courier. Em sistemas Windows, o diretório de fontes do sistema deve conter Times New Roman.
>
>* (Somente para sistemas baseados em UNIX) Uma das seguintes fontes em japonês deve estar disponível no servidor do AEM Forms para converter uma página da Web com fonte em japonês em um documento PDF.
>
>  * &quot;Sazanami Gothic&quot;
>  * Kozuka Gothic Pro-VI
>  * Kozuka Mincho Pro-VI
>  * &quot;Sazanami Gothic&quot;
>  * &quot;Kozuka Mincho Pr6N&quot;
>  * Sazanami Mincho
>  * &quot;Adobe Heiti Std&quot;
>  * &quot;Adobe Song Std&quot;
>
>* Para fazer upload de um arquivo do sistema de arquivos local, use a opção Fazer upload de arquivo na página HTML para PDF.

1. No console de administração, clique em Serviços > PDF Generator > HTML para PDF.
1. Especifique o arquivo a ser convertido executando uma das seguintes tarefas:

   * Em Fazer upload do arquivo, digite o caminho e o nome do arquivo HTML ou ZIP, ou clique em Procurar para localizá-lo e selecioná-lo.
   * Na caixa Especificar URL, digite o URL da página ou do site que será convertido.

   >[!NOTE]
   >
   >O arquivo que você está convertendo deve ter uma extensão de nome de arquivo .html, .htm ou .zip.

1. Especifique as definições de configuração:

   * Para usar configurações personalizadas, selecione Usar configurações personalizadas, especifique as configurações de segurança e de tipo de arquivo e especifique um valor de tempo limite. O valor padrão é de 270 segundos.

   >[!NOTE]
   >
   >Se você tiver configurado o serviço Gerar PDF para usar o Acrobat WebCapture, as Configurações de Tipo de Arquivo selecionadas nesta página não afetarão o PDF produzido. Em vez disso, faça as alterações apropriadas na versão do Acrobat instalada no servidor.

   * Para usar um arquivo de configurações existente, selecione Fazer upload do arquivo de configurações e clique em Procurar para ir para o local do arquivo.

1. Para fazer upload de um arquivo XMP, clique em Procurar e vá para o local do arquivo. Um arquivo XMP pode ser usado para incluir informações de metadados padrão. (Consulte [Sobre arquivos XMP](converting-files-using-pdf-generator.md#about-xmp-files).)
1. Clique em Criar. Quando o arquivo é criado, um link para o arquivo PDF é exibido.
1. Clique no link para exibir o documento PDF no Acrobat.

## Exportar um arquivo PDF para outro formato de arquivo (somente Windows) {#export-a-pdf-file-to-another-file-format-windows-only}

É possível exportar arquivos de PDF para vários formatos de arquivo, conforme descrito no capítulo Gerar serviço de PDF de [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

1. No console de administração, clique em Serviços > PDF Generator > Export PDF.
1. Clique em Procurar para localizar o arquivo de PDF a ser exportado.
1. Na lista Export PDF arquivo para, selecione o formato para o qual o arquivo de PDF será exportado.
1. Na caixa Especificar um tempo limite, digite o tempo de espera antes que o aplicativo expire. O valor padrão é de 270 segundos.

   O Tempo de conversão exibido quando o arquivo é convertido pode ser maior que o valor especificado aqui. O Tempo de conversão inclui o tempo gasto aguardando o thread ou processo, o tempo gasto para converter o arquivo e o tempo gasto pelo conversor de fallback (se aplicável). hora. O valor de Especificar um tempo limite é apenas o tempo necessário para converter o arquivo.

1. (Opcional) Na **Especificar perfil de comprovação personalizado** clique em Procurar e selecione uma [perfil de comprovação personalizado](https://helpx.adobe.com/acrobat/using/preflight-profiles-acrobat-pro.html). Os perfis de comprovação são usados somente ao converter documentos no formato de arquivo PDF (PDF/A).
1. Clique em Exportar. Quando a conversão estiver concluída, um link para o arquivo exportado será exibido.
1. Clique no link para exibir o arquivo convertido.

## Otimizar um PDF (somente Windows) {#optimize-a-pdf}

O PDF Generator suporta a redução do tamanho de arquivos PDF.

>[!NOTE]
>
>A otimização de um documento assinado digitalmente remove e invalida as assinaturas digitais.

1. No console de administração, clique em Serviços > PDF Generator > Optimize PDF.
1. Clique em Procurar para localizar o arquivo de PDF a ser otimizado.
1. Especifique as definições de configuração:

   * Para usar configurações personalizadas, selecione Usar configurações personalizadas, especifique as configurações de tipo de arquivo e especifique um valor de tempo limite. O valor padrão é de 270 segundos.
   * Para usar um arquivo de configurações existente, selecione Fazer upload do arquivo de configurações e clique em Procurar para ir para o local do arquivo.

1. Clique em Criar.
