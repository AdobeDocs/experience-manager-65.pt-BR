---
title: Ofertas de segurança do documento
seo-title: Ofertas de segurança do documento
description: Saiba mais sobre várias ferramentas e recursos da Segurança do Documento AEM
seo-description: Saiba mais sobre várias ferramentas e recursos da Segurança do Documento AEM
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: e45e335d433f17a48ba1bf27a93c5b1003369512
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---


# Ofertas de segurança do documento{#document-security-offerings}

A segurança do documento Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Usando a segurança do documento, é possível distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem Adobe Portable Documento Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

É possível proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um recipient pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os recipient podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor Documento Security; aplique as políticas aos documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. É possível distribuir o documento protegido por política para recipient autorizados pela política.

O diagrama a seguir mostra a arquitetura típica da Segurança do Documento AEM Forms:

![Segurança do documento - Arquitetura recomendada](do-not-localize/document_security_architecture.png)

## Clientes do Documento Security {#document-security-clients}

O Documento Security fornece vários clientes para proteger documentos, visualização e editar documentos protegidos e indexadores para permitir a pesquisa em texto completo em documentos protegidos. Você pode escolher um cliente com base em seus requisitos e nos recursos do cliente.

O Documento Security Server é o componente central através do qual o Documento Security realiza transações como autenticação de usuário, gerenciamento em tempo real de políticas e aplicação de confidencialidade. O servidor também fornece um repositório central para políticas, registros de auditoria e outras informações relacionadas.

O servidor Documento Security fornece uma interface baseada na Web (página da Web) para criar políticas, gerenciar documentos protegidos por política e monitorar eventos associados a documentos protegidos por política. Os administradores também podem configurar opções globais, como autenticação de usuário, auditoria e mensagens para usuários convidados, e gerenciar contas de usuários convidados.

O servidor está incluído na oferta suplementar de Segurança do Documento AEM Forms. Você pode entrar em contato com a equipe [de vendas da AEM Forms](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) para comprar o complemento Documento Security.

### Documentos Protect {#protect-documents}

O AEM Forms Documento Security fornece várias ferramentas para aplicar políticas de segurança. Você pode escolher uma ferramenta de acordo com seus requisitos e especificações.

![Ofertas de segurança para documentos](assets/document-security-offerings.png)

Você pode usar o SDK de segurança do Documento, o Adobe Acrobat, o Documento Security Extension for Microsoft Office ou a Biblioteca de proteção portátil para aplicar e rastrear as políticas de segurança:

* **SDK de segurança do documento:** o SDK é um cliente rico em recursos. Você pode usar o SDK de segurança do Documento para acessar a funcionalidade do servidor do documento, abrir documentos protegidos por política e desenvolver extensões personalizadas, plug-ins ou aplicativos. Por exemplo, você pode desenvolver extensões para proteger formatos de arquivo personalizados ou integrar o SDK às soluções de Prevenção de perda de dados (DLP). Extensões, aplicativos e plug-ins desenvolvidos usando o Document Security SDK enviam documentos para o servidor AEM Forms designado e as políticas são aplicadas no servidor. Observe também que o SDK do cliente de segurança do documento AEM Forms (CSDK) não pode desproteger os documentos protegidos usando a biblioteca de proteção portátil (PPL) e vice-versa.

   O SDK de segurança do Documento está disponível para Java e C++. O Java SDK está incluído na oferta AEM Forms Documento Security e é instalado na implantação de formulários AEM no JEE. Você pode entrar em contato com [AEM equipe de suporte](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) para adquirir o SDK C++. O SDK C++ pode ser compilado com o Microsoft Visual Studio 2013. Você pode visitar o site [Documentação da API de segurança do Documento](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) para saber e usar os recursos do SDK.

* **Adobe Acrobat:** você pode usar o Adobe Acrobat para aplicar política de segurança a documentos PDF que criam aplicativos de desktop populares, como o Microsoft Office, navegadores da Web ou qualquer aplicativo que suporte impressão em formato PDF.

   Você pode comprar e baixar o Adobe Acrobat do [site do Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). O artigo da Adobe Acrobat [que configura políticas de segurança para PDFs](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) fornece informações detalhadas sobre como criar e aplicar políticas no Adobe Acrobat.

* **Extensão de segurança do documento para Microsoft Office**: Você pode usar o Documento Security Extension for Microsoft Office para aplicar políticas predefinidas aos seus arquivos do Microsoft Office a partir dos programas do Microsoft Office. A extensão garante que somente pessoas autorizadas possam usar arquivos do Microsoft Word, Excel e PowerPoint protegidos por política. Somente usuários autorizados que tenham o plug-in instalado podem usar os arquivos protegidos por política.

   A extensão Segurança do Documento está disponível como um plug-in do Microsoft Office. Você pode entrar em contato com [AEM equipe de suporte](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) para obter a extensão. Mais tarde, você pode visitar a ajuda do [Documento Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) para saber mais sobre como instalar, configurar e usar a extensão.

* **Biblioteca de proteção portátil: a Biblioteca de proteção** portátil (PPL) protege um documento localmente, sem enviar o documento para o servidor AEM Forms. Somente as credenciais de segurança e os detalhes da política viajam pela rede. O PPL também permite limitar o acesso de recuperação de política somente para usuários conectados. Você pode buscar políticas com o contexto do usuário conectado AEM usuário.

   Juntamente com o acima, a Biblioteca de proteção portátil tem todos os recursos do SDK de segurança do Documento. Você pode usar o SDK de segurança do Documento para acessar a funcionalidade do servidor do documento, abrir documentos protegidos por política e desenvolver extensões personalizadas, plug-ins ou aplicativos. Observe também que a biblioteca de proteção portátil (PPL) não pode desproteger os documentos protegidos usando o SDK do cliente de segurança do documento AEM Forms (CSDK) e vice-versa.

   A Biblioteca de proteção portátil está disponível para Java e C++ em versões de 32 bits e 64 bits. Ele também está disponível como um pacote OSGi para AEM Forms no OSGi. O PPL C++ pode ser compilado com o Microsoft Visual Studio 2013. Se você tiver licenciado o complemento AEM Forms Documento Security, entre em contato com a [equipe de suporte do AEM Forms Documento Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) para adquirir a Biblioteca Portable Protection. Posteriormente, você poderá usar a Ajuda da Biblioteca de proteção portátil (fornecida com a biblioteca) para configurar e usar a Biblioteca de proteção portátil.

### Visualização ou edição de documentos protegidos {#view-or-edit-protected-documents}

* Para **documentos PDF**, você pode usar o Adobe Acrobat DC, o Acrobat Reader e o Acrobat Reader Mobile para visualização de documentos PDF protegidos. A maioria dos usuários já tem o Acrobat Reader instalado em seus dispositivos, portanto, não é necessário obter ou aprender software adicional para visualização de documentos protegidos. Você também pode baixar o Acrobat Reader do [site de download da Acrobat Reader](https://get.adobe.com/reader/).

* Para **documentos do Microsoft Office**, necessita da extensão de Segurança de Documentos do Microsoft Office e AEM Forms para o Microsoft Office. A extensão Segurança do Documento está disponível como um plug-in do Microsoft Office. Você pode baixar a extensão do site da Adobe.

### Documentos protegidos por índice {#index-protected-documents}

Os mecanismos de pesquisa de texto completo do Microsoft Windows (servidor SharePoint Index) e do Adobe Experience Manager (AEM) podem executar pesquisa de texto completo em formatos de documento usados com frequência, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você pode usar indexadores de Segurança do Documento para permitir que mecanismos de pesquisa de texto completo pesquisem documentos PDF protegidos:

* **Indexador do iFilter:** você pode usar o indexador do iFilter para indexar documentos PDF protegidos e habilitar mecanismos de pesquisa de texto completo do Microsoft Windows (Serviço de Indexação de Área de Trabalho e Servidor de Indexação do SharePoint) para pesquisar documentos PDF protegidos. Para obter informações detalhadas, consulte [AEM IFilter do SharePoint para Documentos Protegidos](assets/sharepoint-ifilter-doc-security.pdf).

* **Indexador de segurança do Documento AEM Forms:** você pode usar o indexador de segurança do Documento AEM Forms para indexar documentos PDF protegidos e permitir que o Adobe Experience Manager pesquise documentos PDF protegidos. Os indexadores fazem parte da oferta AEM Forms Documento Security. Eles estão incluídos no AEM Forms em instaladores JEE.

