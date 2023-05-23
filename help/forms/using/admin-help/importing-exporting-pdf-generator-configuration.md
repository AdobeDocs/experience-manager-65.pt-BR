---
title: Importação e exportação de arquivos de configuração do Gerador de PDF
seo-title: Importing and exporting PDF Generator configuration files
description: Saiba como importar e exportar arquivos de configuração do Gerador de PDF.
seo-description: Learn how to import and export PDF Generator configuration files.
uuid: 3367253b-d222-4c5f-9455-a1810d96112e
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e25c1b35-73eb-4353-8e39-a2d4cdccd101
feature: PDF Generator
exl-id: b363b23a-29bb-4ea4-a8f2-5ba9fe3c7b27
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Importação e exportação de arquivos de configuração do Gerador de PDF {#importing-and-exporting-pdf-generator-configuration-files}

O arquivo de configuração contém as informações de conversão do Gerador de PDF, incluindo PDF, tipo de arquivo e configurações de segurança.

>[!NOTE]
>
>Não é possível alterar a configuração de tempo limite do Gerador de PDF importando um arquivo nativo2pdfconfig.xml personalizado. A configuração de tempo limite nesse arquivo é apenas para fins informativos e exibe a configuração atual no PDF Generator. Para alterar a configuração de tempo limite, consulte &quot;Definindo parâmetros de desempenho do Gerador de PDF&quot; em [Instalação e implantação de formulários AEM](https://www.adobe.com/go/learn_aemforms_installJBoss_63).

## Exportar seu arquivo de configuração atual {#export-your-current-configuration-file}

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Exportar configuração.
1. Para exportar as configurações, selecione a opção apropriada:

   * Para exportar todas as configurações nomeadas, selecione Baixar configuração inteira.
   * Para exportar apenas uma configuração do Adobe PDF, de segurança ou de tipo de arquivo, selecione Baixar configuração mínima.

      Se estiver exportando uma configuração mínima, selecione as configurações de Adobe PDF, segurança e tipo de arquivo a serem exportadas.

1. Clique em Baixar e salve o arquivo XML em um local apropriado.

## Importar um arquivo de configuração {#import-a-configuration-file}

>[!NOTE]
>
>O sistema será reconfigurado com base nas informações do arquivo importado.

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Import An Existing Configuration File.
1. Para especificar o local do arquivo na caixa Arquivo de Configuração, clique em Procurar para localizar e selecionar o arquivo e clique em **Importar**.

## Converter todas as camadas dentro de arquivos do AutoCAD {#convert-all-layers-within-autocad-files}

Por padrão, o Gerador de PDF converte somente a camada padrão de arquivos AutoCAD em PDF em vez de todas as camadas dentro do arquivo. Para converter todas as camadas, siga este procedimento.

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Exportar configuração.
1. Selecione Baixar toda a configuração e clique em Baixar.
1. Em um editor de texto, abra o arquivo baixado e, no `AutoCAD` tag na `PDFMaker` adicionar o texto `convertAllPages="true"`.
1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Importar um arquivo de configuração existente, especifique o arquivo atualizado e clique em Importar.

   Todos os arquivos do AutoCAD convertidos com o arquivo de configuração modificado terão todas as camadas convertidas.

## Redefina sua configuração para as configurações originais instaladas com o PDF Generator {#reset-your-configuration-to-the-original-settings-installed-with-pdf-generator}

1. No console de administração, clique em Serviços > Gerador de PDF > Arquivos de configuração > Importar configuração.
1. Selecione Redefinir configuração para configurações padrão e clique em Importar.
