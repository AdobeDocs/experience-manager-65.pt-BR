---
title: Ofertas de segurança de documentos
seo-title: Ofertas de segurança de documentos
description: Saiba mais sobre várias ferramentas e recursos da Segurança de documentos AEM
seo-description: Saiba mais sobre várias ferramentas e recursos da Segurança de documentos AEM
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1219'
ht-degree: 0%

---


# Ofertas de segurança de documentos{#document-security-offerings}

A segurança de documentos da Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Usando a segurança de documentos, você pode distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem Adobe Portable Document Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

Você pode proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um destinatário pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor de segurança de documentos; aplique as políticas aos documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. Você pode distribuir o documento protegido por política para recipients autorizados pela política.

O diagrama a seguir mostra a arquitetura típica da Segurança de documentos do AEM Forms:

![Segurança de documentos - Arquitetura recomendada](do-not-localize/document_security_architecture.png)

## Clientes de segurança de documentos {#document-security-clients}

A Segurança de documentos fornece vários clientes para proteger documentos, exibir e editar documentos protegidos e indexadores para permitir a pesquisa de texto completo em documentos protegidos. Você pode escolher um cliente com base em seus requisitos e nos recursos do cliente.

O Servidor de Segurança de Documentos é o componente central através do qual a Segurança de Documentos executa transações como autenticação de usuário, gerenciamento em tempo real de políticas e aplicação de confidencialidade. O servidor também fornece um repositório central para políticas, registros de auditoria e outras informações relacionadas.

O servidor de segurança de documentos fornece uma interface baseada na Web (página da Web) para criar políticas, gerenciar documentos protegidos por políticas e monitorar eventos associados a documentos protegidos por políticas. Os administradores também podem configurar opções globais, como autenticação de usuários, auditoria e mensagens para usuários convidados, e gerenciar contas de usuários convidados.

O servidor está incluído na oferta complementar de Segurança de documento da AEM Forms. Você pode entrar em contato com a [equipe de vendas](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&amp;s_iid=70114000002JHs3AAG) da AEM Forms para comprar o complemento Segurança de documentos.

### Documentos do Protect {#protect-documents}

A Segurança de documentos da AEM Forms fornece várias ferramentas para aplicar políticas de segurança. Você pode escolher uma ferramenta de acordo com seus requisitos e especificações.

![ofertas de segurança de documentos](assets/document-security-offerings.png)

Você pode usar o SDK de segurança de documentos, o Adobe Acrobat, a Extensão de segurança de documentos para o Microsoft Office ou a Biblioteca de proteção portátil para aplicar e rastrear as políticas de segurança:

* **SDK de segurança de documento:**  o SDK é um cliente rico em recursos. Você pode usar o SDK de segurança de documentos para acessar a funcionalidade do servidor de documentos, abrir documentos protegidos por políticas e desenvolver extensões, plug-ins ou aplicativos personalizados. Por exemplo, você pode desenvolver extensões para proteger formatos de arquivo personalizados ou integrar o SDK às soluções de Prevenção de perda de dados (DLP). Extensões, aplicativos e plug-ins desenvolvidos usando o SDK de segurança de documentos enviam documentos para um servidor designado da AEM Forms e as políticas são aplicadas no servidor. Além disso, observe que o SDK do cliente de segurança de documentos da AEM Forms (CSDK) não pode desproteger os documentos protegidos usando a biblioteca de proteção portátil (PPL) e vice-versa.

   O SDK de segurança de documentos está disponível para Java e C++. O Java SDK está incluído na oferta AEM Forms Document Security e é instalado na implantação de formulários AEM no JEE. Você pode entrar em contato com [AEM equipe de suporte](https://helpx.adobe.com/br/marketing-cloud/contact-support.html) para obter o SDK do C++. O SDK do C++ pode ser compilado com o Microsoft Visual Studio 2013. Você pode visitar o site [Documentação da API de segurança de documentos](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) para saber e usar os recursos do SDK.

* **Adobe Acrobat:** você pode usar o Adobe Acrobat para aplicar a política de segurança a documentos PDF que criam usando aplicativos de desktop populares, como o Microsoft Office, navegadores da Web ou qualquer aplicativo que suporte a impressão em formato PDF.

   Você pode comprar e baixar o Adobe Acrobat de [Adobe Website](https://acrobat.adobe.com/us/en/free-trial-download.html). O artigo da Adobe Acrobat [como configurar políticas de segurança para PDFs](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) fornece informações detalhadas sobre como criar e aplicar políticas no Adobe Acrobat.

* **Extensão de Segurança de Documento para Microsoft Office**: Você pode usar a Extensão de Segurança de Documento para o Microsoft Office para aplicar políticas predefinidas a seus arquivos do Microsoft Office a partir dos programas do Microsoft Office. A extensão garante que somente pessoas autorizadas possam usar arquivos protegidos por política do Microsoft Word, Excel e PowerPoint. Somente usuários autorizados que tenham o plug-in instalado podem usar os arquivos protegidos por política.

   A extensão Segurança de documento está disponível como um plug-in do Microsoft Office. Você pode entrar em contato com [AEM equipe de suporte](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) para obter a extensão. Posteriormente, você pode visitar a ajuda da [Extensão de segurança de documento para Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/download-installer.html) para saber mais sobre como instalar, configurar e usar a extensão.

* **Biblioteca de proteção portátil:** a Biblioteca de proteção portátil (PPL) protege um documento localmente, sem enviá-lo ao servidor da AEM Forms. Somente as credenciais de segurança e os detalhes da política viajam pela rede. O PPL também permite limitar o acesso à recuperação de política somente para usuários conectados. Você pode buscar políticas com o contexto do usuário conectado AEM usuário.

   Além disso, a Biblioteca de proteção portátil tem todos os recursos do SDK de segurança de documentos. Você pode usar o SDK de segurança de documentos para acessar a funcionalidade do servidor de documentos, abrir documentos protegidos por políticas e desenvolver extensões, plug-ins ou aplicativos personalizados. Além disso, observe que a biblioteca de proteção portátil (PPL) não pode desproteger os documentos protegidos usando o SDK (CSDK) do cliente de segurança de documentos da AEM Forms e vice-versa.

   A Biblioteca de proteção portátil está disponível para os idiomas Java e C++ em versões de 32 e 64 bits. Também está disponível como um pacote OSGi para AEM Forms no OSGi. O PPL C++ pode ser compilado com o Microsoft Visual Studio 2013. Se tiver licenciado o complemento AEM Forms Document Security, você pode entrar em contato com a equipe de suporte [AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) para adquirir a Portable Protection Library. Posteriormente, você pode usar a Ajuda da Biblioteca de proteção portátil (fornecida com a biblioteca) para configurar e usar a Biblioteca de proteção portátil.

### Exibir ou editar documentos protegidos {#view-or-edit-protected-documents}

* Para **documentos PDF**, você pode usar Adobe Acrobat DC, Acrobat Reader e Acrobat Reader Mobile para exibir documentos PDF protegidos. A maioria dos usuários já tem o Acrobat Reader instalado em seus dispositivos, portanto não é necessário obter ou aprender software adicional para exibir documentos protegidos. Você também pode baixar o Acrobat Reader de [Acrobat Reader download web site](https://get.adobe.com/reader/).

* Para **documentos do Microsoft Office**, você precisa da extensão Segurança de Documentos do Microsoft Office e AEM Forms para o Microsoft Office. A extensão Segurança de documento está disponível como um plug-in do Microsoft Office. Você pode baixar a extensão do site do Adobe.

### Indexar documentos protegidos {#index-protected-documents}

Os mecanismos de pesquisa de texto completo do Microsoft Windows (servidor de índice do SharePoint) e do Adobe Experience Manager (AEM) podem executar pesquisa de texto completo em formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você pode usar indexadores de Segurança de documento para permitir que mecanismos de pesquisa de texto completo pesquisem documentos PDF protegidos:

* **Indexador do iFilter:** você pode usar o indexador do iFilter para indexar documentos PDF protegidos e ativar mecanismos de pesquisa de texto completo do Microsoft Windows (Serviço de Indexação de Desktop e Servidor de Indexação do SharePoint) para pesquisar documentos PDF protegidos. Para obter informações detalhadas, consulte [AEM o IFilter do SharePoint para Documentos Protegidos](assets/sharepoint-ifilter-doc-security.pdf).

* **Indexador de segurança de documentos do AEM Forms:** você pode usar o indexador de segurança de documentos do AEM Forms para indexar documentos PDF protegidos e permitir que o Adobe Experience Manager pesquise documentos PDF protegidos. Os indexadores fazem parte da oferta AEM Forms Document Security. Eles estão incluídos no AEM Forms em instaladores JEE.

