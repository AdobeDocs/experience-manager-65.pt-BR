---
title: Tipos de certificado usados por extensões do Acrobat Reader DC
description: Saiba mais sobre os tipos de certificados usados pelas extensões do Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 800bffd5-0cdc-4251-bba4-e350f226f019
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 2%

---

# Tipos de certificado usados por extensões do Acrobat Reader DC {#certificate-types-used-by-acrobat-reader-dc-extensions}

O Visualizador de Certificados fornece as seguintes informações sobre o certificado:

* Nome &quot;amigável&quot; do certificado
* Perfis de certificado
* Período de validade
* direitos de uso de extensões do Acrobat Reader DC

## Nome &quot;amigável&quot; do certificado {#certificate-friendly-name}

O nome &quot;amigável&quot; de um certificado de extensões do Acrobat Reader DC é uma string que descreve as propriedades do certificado, como no exemplo a seguir:

SÃO 2D Código de barras Produção completa V6.1 P8 0002054

A string contém os seguintes elementos:

**Tipo de certificado:** Descreve os módulos de formulários AEM ativados pelo certificado e o nível de ativação, como o código de barras 2D completo do ARE. Para obter uma lista dos tipos de certificados disponíveis, consulte a coluna Tipo na tabela na seção Perfis de certificado.

**Tipo de implantação:** Indica o uso pretendido do certificado, como Produção. O valor pode ser Avaliação ou Produção. Para obter uma lista dos tipos de implantação associados a cada tipo de certificado, consulte a coluna Tipo de implantação na tabela na seção Perfis de certificado.

**Versão de direitos de uso:** Descreve a versão do algoritmo de direitos de uso para o qual o certificado pode ser usado, como V6.1. Esta versão não significa a versão do Acrobat ou as extensões do Acrobat Reader DC.

**Código do perfil:** O código do perfil é uma descrição resumida de propriedades completas do certificado, como por exemplo, P8. Para obter uma lista dos códigos de perfil associados a cada tipo de arquivo, consulte a coluna Código de perfil na tabela na seção Perfis de certificado.

**Número de série:** Um número de série é atribuído a cada certificado emitido pelo Adobe, como 0002054. O Suporte Adobe Enterprise ou um representante de conta Adobe Enterprise pode usar esse número de série para rastrear o certificado a um pedido de produto específico ou a um relacionamento OEM.

## Perfis de certificado {#certificate-profiles}

A tabela a seguir lista os perfis de certificado que você pode encontrar ao analisar certificados de extensões do Acrobat Reader DC.

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
   <td><p>Avaliação e teste</p></td>
  </tr>
  <tr>
   <td><p>P3</p></td>
   <td><p>Extensões do Acrobat Reader DC, Produção</p></td>
   <td><p>Max</p></td>
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
   <td><p>Extensões da Acrobat Reader DC, Integração de parceiros</p></td>
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
   <td><p>Somente assinatura; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I13</p></td>
   <td><p>Somente comentários offline; pode ser usado por OEMs</p></td>
   <td><p>Max</p></td>
   <td><p>Produção e avaliação</p></td>
  </tr>
  <tr>
   <td><p>I14</p></td>
   <td><p>Somente comentários; pode ser usado por OEMs</p></td>
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

Os certificados de avaliação são emitidos para clientes e desenvolvedores para que eles possam avaliar e desenvolver aplicativos de amostra para produtos. O período de validade destes certificados está compreendido entre 60 e 90 dias. Expiram no final do segundo mês seguinte aos dados da emissão.

Os certificados de integração de parceiros são emitidos para parceiros de negócios Adobe para oferecer suporte ao desenvolvimento, à integração, à criação de protótipos e à demonstração de software. Estes certificados são válidos por dois anos a contar da data de emissão.

Os certificados de uso interno do Adobe são usados no Adobe para oferecer suporte ao desenvolvimento, integração, protótipo e demonstração de software. Estes certificados são válidos por dois anos a contar da data de emissão.

Os certificados de produção são emitidos para clientes que compraram extensões do Acrobat Reader DC. Esses certificados são válidos pelo período máximo permitido pela autoridade de certificação (CA), mostrado como *Máx* na tabela Perfis de certificado.

## direitos de uso de extensões do Acrobat Reader DC {#acrobat-reader-dc-extensions-usage-rights}

Ao examinar o certificado de extensões do Acrobat Reader DC no Visualizador de certificados, você pode selecionar o item de direitos de uso na guia Detalhes (se configurada) para ver uma lista discriminada dos direitos de uso do Adobe Reader que o certificado pode ativar. Os direitos de uso ativados em um determinado documento podem ser um subconjunto daqueles ativados pelo certificado.

Se for necessário fazer comentários on-line em um ambiente não colaborativo, entre em contato com o Suporte da Adobe para obter mais informações. A propriedade Mode corresponde ao tipo de implantação e é *produção* ou *avaliação*.

Os direitos de uso permitidos das extensões do Acrobat Reader DC consistem em um ou mais elementos específicos. Esses elementos são usados em diferentes combinações para obter diversas funcionalidades licenciadas do produto.

<table>
 <thead>
  <tr>
   <th><p>Elemento de direitos de uso</p></th>
   <th><p>Recurso ativado no Adobe Reader ao visualizar um documento de PDF habilitado para direitos</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>FormulárioPreencherESalvar</p></td>
   <td><p>Preencha os campos do formulário e salve os arquivos localmente.</p></td>
  </tr>
  <tr>
   <td><p>FormImportExport</p></td>
   <td><p>Importar e exportar dados de formulário como arquivos FDF, XFDF, XML e XDP.</p></td>
  </tr>
  <tr>
   <td><p>FormulárioAdicionarExcluir</p></td>
   <td><p>Adicione, altere ou exclua campos e propriedades de campo no formulário PDF.</p></td>
  </tr>
  <tr>
   <td><p>SubmitStandalone</p></td>
   <td><p>Enviar dados, por email ou offline, para um servidor quando ele não estiver em execução em uma sessão do navegador.</p></td>
  </tr>
  <tr>
   <td><p>SpawnTemplate</p></td>
   <td><p>Crie páginas a partir de páginas de modelo no mesmo formulário de PDF.</p></td>
  </tr>
  <tr>
   <td><p>Assinatura</p></td>
   <td><p>Assine e salve digitalmente documentos de PDF e limpe assinaturas digitais.</p></td>
  </tr>
  <tr>
   <td><p>AnnotModify</p></td>
   <td><p>Criar e modificar anotações do documento, como comentários.</p></td>
  </tr>
  <tr>
   <td><p>AnnotImportExport</p></td>
   <td><p>Salve anotações como comentários em um arquivo de dados separado e carregue comentários de um arquivo.</p></td>
  </tr>
  <tr>
   <td><p>TextoSemFormataçãoCódigoDeBarras</p></td>
   <td><p>Imprima um documento com dados de formulário com código de barras em um formulário não criptografado que não exija software de servidor licenciado para decodificar.</p></td>
  </tr>
  <tr>
   <td><p>AnnotOnline</p></td>
   <td><p>Fazer upload e download de anotações, como comentários, para e de um servidor de comentários e revisão de documentos online.</p></td>
  </tr>
  <tr>
   <td><p>FormulárioOnline</p></td>
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
>Os direitos de uso de extensões do Acrobat Reader DC podem ser licenciados do Adobe somente em determinadas combinações que funcionam juntas. Não é possível licenciar esses recursos de forma independente. Para obter informações sobre as combinações disponíveis de direitos de uso, entre em contato com um representante de conta da AEM Forms.
