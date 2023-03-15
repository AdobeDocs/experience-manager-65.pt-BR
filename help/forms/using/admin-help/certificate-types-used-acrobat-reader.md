---
title: Tipos de certificado usados pelas extensões do Acrobat Reader DC
seo-title: Certificate types used by Acrobat Reader DC extensions
description: Saiba mais sobre os tipos de certificado usados pelas extensões do Acrobat Reader DC.
seo-description: Learn about the certificate types used by Acrobat Reader DC extensions.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 4%

---

# Tipos de certificado usados pelas extensões do Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

O Visualizador de certificados fornece as seguintes informações sobre o certificado:

* Nome &quot;amigável&quot; do certificado
* Perfis de certificado
* Período de validade
* Direitos de uso de extensões do Acrobat Reader DC

## Nome &quot;amigável&quot; do certificado {#certificate-friendly-name}

O nome &quot;amigável&quot; de um certificado de extensões Acrobat Reader DC é uma string que descreve as propriedades do certificado, como no exemplo a seguir:

SÃO 2D Código de Barras Produção Completa V6.1 P8 0002054

A string contém os seguintes elementos:

**Tipo de certificado:** Descreve os módulos de formulários de AEM ativados pelo certificado e o nível de ativação, como ARE 2D Barcode Full. Para obter uma lista dos tipos de certificados disponíveis, consulte a coluna Tipo na tabela na seção Perfis de certificado .

**Tipo de implantação:** Indica o uso pretendido do certificado, como Produção. O valor pode ser Avaliação ou Produção. Para obter uma lista de tipos de implantação associados a cada tipo de certificado, consulte a coluna Deployment type na tabela na seção Certificate profiles .

**Versão de direitos de uso:** Descreve a versão do algoritmo de direitos de uso para a qual o certificado pode ser usado, como V6.1. Essa versão não significa a versão do Acrobat ou do Acrobat Reader DC Extensions.

**Código do perfil:** O código de perfil é uma descrição resumida de propriedades completas de certificados, como P8, por exemplo. Para obter uma lista dos códigos de perfil associados a cada tipo de arquivo, consulte a coluna Código de perfil na tabela na seção Perfis de certificado .

**Número de série:** É atribuído um número de série a cada certificado emitido por Adobe, como 0002054. O Adobe Enterprise Support ou um representante de conta Adobe Enterprise pode usar esse número de série para rastrear o certificado para um pedido de produto específico ou para um relacionamento OEM.

## Perfis de certificado {#certificate-profiles}

A tabela a seguir lista os perfis de certificado que podem ser encontrados ao analisar certificados de extensões do Acrobat Reader DC.

<table>
 <thead>
  <tr>
   <th><p>Código do perfil</p></th>
   <th><p>Tipo</p></th>
   <th><p>Período de validade</p></th>
   <th><p>Tipo de implantação</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>P1</p></td>
   <td><p>Produção SAP</p></td>
   <td><p>Max</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>Teste interno SAP</p></td>
   <td><p>2 anos</p></td>
   <td><p>Avaliação e ensaio</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensões do Acrobat Reader DC, Produção</p></td>
   <td><p>Max</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensões do Acrobat Reader DC, Uso interno do Adobe</p></td>
   <td><p>2 anos</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensões do Acrobat Reader DC, Integração de parceiros</p></td>
   <td><p>2 anos</p></td>
   <td><p>Avaliação e ensaio</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensões do Acrobat Reader DC, Avaliação</p></td>
   <td><p>60 dias</p></td>
   <td><p>Avaliação</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, Produção</p></td>
   <td><p>Max</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, Produção</p></td>
   <td><p>Max</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Apenas assinatura; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Comentários offline somente; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Apenas comentários; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Permissões completas; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
 </tbody>
</table>

## Período de validade {#validity-period}

Os certificados de avaliação são emitidos para clientes e desenvolvedores, para que eles possam avaliar e desenvolver aplicativos de amostra para produtos. O período de validade destes certificados situa-se entre 60 e 90 dias. Eles expiram no final do segundo mês seguinte aos dados de emissão.

Os certificados de Integração de parceiros são emitidos para parceiros comerciais da Adobe para dar suporte ao desenvolvimento, integração, protótipo e demonstração de software. Estes certificados são válidos por dois anos a contar da data de emissão.

Os certificados de uso interno do Adobe são usados no Adobe para dar suporte ao desenvolvimento, integração, protótipo e demonstração de software. Estes certificados são válidos por dois anos a contar da data de emissão.

Os certificados de produção são emitidos para clientes que compraram extensões do Acrobat Reader DC. Estes certificados são válidos pelo período máximo permitido pela autoridade de certificação (CA), indicado como *Max* na tabela Perfis de certificado.

## Direitos de uso de extensões do Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Ao examinar o certificado de extensões do Acrobat Reader DC no Visualizador de certificados, é possível selecionar o item de direitos de uso na guia Detalhes (se configurado) para ver uma lista discriminada dos direitos de uso do Adobe Reader que o certificado pode habilitar. Os direitos de uso ativados em um documento específico podem ser um subconjunto daqueles ativados pelo certificado.

Se for necessário fazer comentários online em um ambiente não colaborativo, entre em contato com o Suporte ao Adobe para obter mais informações. A propriedade Mode corresponde ao tipo de implantação e é *produção* ou *avaliação*.

Os direitos de uso de extensões permitidos do Acrobat Reader DC consistem em um ou mais elementos específicos. Esses elementos são usados em combinações diferentes para obter variedades de funcionalidade de produto licenciada.

<table>
 <thead>
  <tr>
   <th><p>Elemento de direitos de uso</p></th>
   <th><p>Recurso ativado no Adobe Reader ao exibir um documento PDF habilitado para direitos</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormFillInAndSave</p></td>
   <td><p>Preencha os campos do formulário e salve os arquivos localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importe e exporte dados de formulário como arquivos FDF, XFDF, XML e XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormAddDelete</p></td>
   <td><p>Adicione, altere ou exclua campos e propriedades de campos no formulário PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Enviar dados, por email ou offline, para um servidor quando ele não estiver em execução em uma sessão do navegador.</p></td>
  </tr>
  <tr>
   <td><p>ModeloDeEsparto</p></td>
   <td><p>Crie páginas a partir de páginas de modelo no mesmo formulário de PDF.</p></td>
  </tr>
  <tr>
   <td><p>Assinatura</p></td>
   <td><p>Assine digitalmente e salve documentos PDF e limpe assinaturas digitais.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Crie e modifique anotações de documentos, como comentários.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Salve anotações como comentários em um arquivo de dados separado e carregue comentários de um arquivo.</p></td>
  </tr>
  <tr>
   <td><p>Código de barrasPlaintext</p></td>
   <td><p>Imprima um documento com dados de formulário codificados em um formulário não criptografado que não requer software de servidor licenciado para decodificação.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Faça upload e download de anotações, como comentários, de e para um servidor online de análise e comentário de documentos.</p></td>
  </tr>
  <tr>
   <td><p>FormOnline</p></td>
   <td><p>Conecte-se a serviços da Web ou bancos de dados definidos em um formulário PDF.</p></td>
  </tr>
  <tr>
   <td><p>EFModif</p></td>
   <td><p>Modifique objetos de arquivo incorporados associados ao documento PDF.</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os direitos de uso das extensões Acrobat Reader DC podem ser licenciados do Adobe somente em determinadas combinações que trabalham juntas. Não é possível licenciar esses recursos independentemente. Para obter informações sobre as combinações disponíveis de direitos de uso, entre em contato com um representante de conta dos formulários AEM.
