---
title: Tipos de certificado usados por extensões do Acrobat Reader DC
seo-title: Tipos de certificado usados por extensões do Acrobat Reader DC
description: Saiba mais sobre os tipos de certificados usados pelas extensões do Acrobat Reader DC.
seo-description: Saiba mais sobre os tipos de certificados usados pelas extensões do Acrobat Reader DC.
uuid: 93c02abc-2d5a-44ed-b93c-981afbd0553d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 331b9317-87b5-4a96-a1bc-429675ff90c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---


# Tipos de certificado usados pelas extensões do Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

O Visualizador de certificados fornece as seguintes informações sobre o certificado:

* Nome &quot;amigável&quot; do certificado
* Perfis de certificados
* Período de validade
* Direitos de uso de extensões do Acrobat Reader DC

## Nome &quot;amigável&quot; do certificado {#certificate-friendly-name}

O nome &quot;amigável&quot; de um certificado de extensões do Acrobat Reader DC é uma string que descreve as propriedades do certificado, como no exemplo a seguir:

ARE 2D Barcode Full Production V6.1 P8 0002054

A string contém os seguintes elementos:

**Tipo de certificado:** descreve os módulos de formulários AEM que o certificado ativa e o nível de ativação, como ARE 2D Barcode Full. Para obter uma lista dos tipos de certificados disponíveis, consulte a coluna Tipo na tabela na seção perfis de certificados.

**Tipo de implantação:** indica o uso pretendido do certificado, como Produção. O valor pode ser Avaliação ou Produção. Para obter uma lista de tipos de implantação associados a cada tipo de certificado, consulte a coluna Tipo de implantação na tabela da seção perfis de certificado.

**Versão de direitos de uso:** descreve a versão do algoritmo de direitos de uso para a qual o certificado pode ser usado, como V6.1. Esta versão não significa a versão das extensões Acrobat ou Acrobat Reader DC.

**Código do perfil:** O código do perfil é uma descrição resumida das propriedades completas do certificado, como P8, por exemplo. Para obter uma lista dos códigos de perfil associados a cada tipo de arquivo, consulte a coluna de código de Perfil na tabela da seção Perfis de certificado.

**Número de série:** Um número de série é atribuído a cada certificado emitido pelo Adobe, como 0002054. O suporte empresarial do Adobe ou um representante de conta empresarial do Adobe pode usar esse número de série para rastrear o certificado em um pedido de produto específico ou em uma relação OEM.

## Perfis de certificado {#certificate-profiles}

A tabela a seguir lista os perfis de certificados que você pode encontrar ao analisar certificados de extensões Acrobat Reader DC.

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
   <td><p>Máximo</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P2</p></td>
   <td><p>Teste interno SAP</p></td>
   <td><p>2 anos</p></td>
   <td><p>Avaliação e teste</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensões Acrobat Reader DC, produção</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P4</p></td>
   <td><p>Extensões Acrobat Reader DC, Uso interno do Adobe</p></td>
   <td><p>2 anos</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P5</p></td>
   <td><p>Extensões da Acrobat Reader DC, integração de parceiro</p></td>
   <td><p>2 anos</p></td>
   <td><p>Avaliação e teste</p></td>
  </tr>
  <tr>
   <td><p>P6</p></td>
   <td><p>Extensões do Acrobat Reader DC, Avaliação</p></td>
   <td><p>60 dias</p></td>
   <td><p>Avaliação</p></td>
  </tr>
  <tr>
   <td><p>P8</p></td>
   <td><p>Forms, produção</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>P9</p></td>
   <td><p>Adobe Acrobat 7.x, produção</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção</p></td>
  </tr>
  <tr>
   <td><p>I10</p></td>
   <td><p>Forms; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I11</p></td>
   <td><p>Forms; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I12</p></td>
   <td><p>Apenas assinatura; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Somente comentários offline; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Apenas comentários; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I15</p></td>
   <td><p>Permissões completas; podem ser usados por OEMs</p></td>
   <td><p>Máximo</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
 </tbody>
</table>

## Período de validade {#validity-period}

Os certificados de avaliação são emitidos a clientes e desenvolvedores para que possam avaliar e desenvolver aplicativos de amostra para produtos. O período de validade destes certificados está compreendido entre 60 e 90 dias. Caducam no final do segundo mês seguinte aos dados de emissão.

Os certificados de Integração de Parceiros são emitidos para parceiros comerciais da Adobe para suportar o desenvolvimento, a integração, a prototipagem e a demonstração de software. Estes certificados são válidos por dois anos a contar da data da sua emissão.

Os certificados de uso interno do Adobe são usados dentro do Adobe para suportar desenvolvimento, integração, protótipo e demonstração de software. Estes certificados são válidos por dois anos a contar da data da sua emissão.

Os certificados de produção são emitidos para clientes que compraram extensões da Acrobat Reader DC. Esses certificados são válidos pelo período máximo permitido pela autoridade de certificação (CA), mostrado como *Max* na tabela Perfis de certificados.

## Direitos de uso de extensões do Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Ao examinar o certificado de extensões do Acrobat Reader DC no Visualizador de certificados, você pode selecionar o item de direitos de uso na guia Detalhes (se configurado) para ver uma lista discriminada dos direitos de uso do Adobe Reader que o certificado pode ativar. Os direitos de uso ativados em um determinado documento podem ser um subconjunto daqueles ativados pelo certificado.

Se for necessário fazer comentários on-line em um ambiente não colaborativo, entre em contato com o Suporte à Adobe para obter mais informações. A propriedade Mode corresponde ao tipo de implantação e é *production* ou *assessment*.

Os direitos de uso de extensões permitidos do Acrobat Reader DC consistem em um ou mais elementos específicos. Esses elementos são usados em combinações diferentes para obter variedades de funcionalidade de produtos licenciados.

<table>
 <thead>
  <tr>
   <th><p>Elemento de direitos de uso</p></th>
   <th><p>Recurso ativado no Adobe Reader ao exibir um documento PDF com direitos ativados</p></th>
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
   <td><p>Envie dados, por email ou offline, para um servidor quando ele não estiver sendo executado em uma sessão do navegador.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Crie páginas a partir de páginas de modelo no mesmo formulário PDF.</p></td>
  </tr>
  <tr>
   <td><p>Assinatura</p></td>
   <td><p>Assine e salve digitalmente documentos PDF e apague assinaturas digitais.</p></td>
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
   <td><p>Código de barrasTexto simples</p></td>
   <td><p>Imprima um documento com dados de formulário codificados em um formulário não criptografado que não exija que o software de servidor licenciado decodifice.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Carregue e baixe anotações, como comentários, de e para um servidor de revisão de documentos e comentários online.</p></td>
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
>Os direitos de uso de extensões do Acrobat Reader DC podem ser licenciados do Adobe somente em determinadas combinações que funcionam em conjunto. Não é possível licenciar esses recursos independentemente. Para obter informações sobre as combinações disponíveis de direitos de uso, entre em contato com um representante de conta de formulários AEM.

