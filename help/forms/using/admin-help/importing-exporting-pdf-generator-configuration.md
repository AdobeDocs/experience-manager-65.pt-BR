---
title: Importação e exportação de arquivos de configuração do Gerador de PDF
seo-title: Importação e exportação de arquivos de configuração do Gerador de PDF
description: Saiba como importar e exportar arquivos de configuração do Gerador de PDF.
seo-description: Saiba como importar e exportar arquivos de configuração do Gerador de PDF.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Importação e exportação de arquivos de configuração do Gerador de PDF {#importing-and-exporting-pdf-generator-configuration-files}

O arquivo de configuração contém as informações de conversão do Gerador de PDF, incluindo o PDF, o tipo de arquivo e as configurações de segurança.

>[!NOTE]
>
>Não é possível alterar a configuração de tempo limite do Gerador de PDF importando um arquivo nativo2pdfconfig.xml personalizado. A configuração de tempo limite nesse arquivo é apenas para fins informativos e exibe a configuração atual no Gerador de PDF. Para alterar a configuração de tempo limite, consulte &quot;Definição de parâmetros de desempenho do Gerador de PDF&quot; em [Instalação e implantação de formulários](https://www.adobe.com/go/learn_aemforms_installJBoss_63)AEM.

## Exportar seu arquivo de configuração atual {#export-your-current-configuration-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Exportar configuração.
1. Para exportar as configurações, selecione a opção apropriada:

   * Para exportar todas as configurações nomeadas, selecione Baixar toda a configuração.
   * Para exportar apenas uma configuração, configuração de segurança ou configuração de tipo de arquivo do Adobe PDF, selecione Download da configuração mínima.

      Se você estiver exportando uma configuração mínima, selecione as configurações de tipo de arquivo, segurança e Adobe PDF a serem exportadas.

1. Clique em Baixar e salve o arquivo XML em um local apropriado.

## Importar um arquivo de configuração {#import-a-configuration-file}

>[!NOTE]
>
>Seu sistema será reconfigurado com base nas informações do arquivo importado.

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Importar um arquivo de configuração existente.
1. Para especificar o local do arquivo na caixa Arquivo de configuração, clique em Procurar para localizar e selecionar o arquivo e clique em **Importar**.

## Converter todas as camadas em arquivos AutoCAD {#convert-all-layers-within-autocad-files}

Por padrão, o Gerador de PDF converte somente a camada padrão de arquivos AutoCAD em PDF em vez de todas as camadas no arquivo. Para converter todas as camadas, siga este procedimento.

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Exportar configuração.
1. Selecione Baixar toda a configuração e clique em Baixar.
1. Em um editor de texto, abra o arquivo baixado e, sob a `AutoCAD` tag na `PDFMaker` tag , adicione o texto `convertAllPages="true"`.
1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Importar um arquivo de configuração existente, especifique o arquivo atualizado e clique em Importar.

   Todos os arquivos AutoCAD convertidos usando o arquivo de configuração modificado terão todas as camadas convertidas.

## Redefina sua configuração para as configurações originais instaladas com o Gerador de PDF {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Redefinir configuração para configurações padrão e clique em Importar.

