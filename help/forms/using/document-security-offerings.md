---
title: Ofertas de segurança de documentos
seo-title: Ofertas de segurança de documentos
description: Saiba mais sobre várias ferramentas e recursos do AEM Document Security
seo-description: Saiba mais sobre várias ferramentas e recursos do AEM Document Security
uuid: 24e3275c-cd44-47c0-a6a0-e4cfb1bced8a
contentOwner: khsingh
geptopics: SG_AEMFORMS/categories/working_with_document_security
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 91e85e86-2361-4d1d-aa73-c3cce46ab1f1
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Ofertas de segurança de documentos{#document-security-offerings}

A segurança de documentos do Adobe Experience Manager Forms garante que somente usuários autorizados possam usar seus documentos. Usando a segurança do documento, é possível distribuir com segurança todas as informações salvas em um formato compatível. Os formatos de arquivo suportados incluem o Adobe Portable Document Format (PDF) e arquivos do Microsoft Word, Excel e PowerPoint.

É possível proteger documentos usando políticas. As configurações de confidencialidade especificadas em uma política determinam como um destinatário pode usar um documento ao qual você aplica a política. Por exemplo, você pode especificar se os destinatários podem imprimir ou copiar texto, editar texto ou adicionar assinaturas e comentários a documentos protegidos.

As políticas são armazenadas no servidor do Document Security; aplique as políticas a documentos por meio do aplicativo cliente. Quando você aplica uma política a um documento, as configurações de confidencialidade especificadas na política protegem as informações que o documento contém. É possível distribuir o documento protegido por política para destinatários autorizados pela política.

O diagrama a seguir mostra a arquitetura típica do AEM Forms Document Security:

![Document Security - Arquitetura recomendada](do-not-localize/document_security_architecture.png)

## Clientes do Document Security {#document-security-clients}

O Document Security fornece vários clientes para proteger documentos, exibir e editar documentos protegidos e indexadores para permitir a pesquisa em texto completo em documentos protegidos. Você pode escolher um cliente com base em seus requisitos e nos recursos do cliente.

O Document Security Server é o componente central através do qual o Document Security realiza transações como autenticação de usuário, gerenciamento em tempo real de políticas e aplicação de confidencialidade. O servidor também fornece um repositório central para políticas, registros de auditoria e outras informações relacionadas.

O servidor do Document Security fornece uma interface baseada na Web (página da Web) para criar políticas, gerenciar documentos protegidos por política e monitorar eventos associados a documentos protegidos por política. Os administradores também podem configurar opções globais, como autenticação de usuário, auditoria e mensagens para usuários convidados, e gerenciar contas de usuários convidados.

O servidor está incluído na oferta complementar do AEM Forms Document Security. Você pode entrar em contato com a equipe [de](https://www.adobe.com/products/request-consultation/marketing-cloud.html?s_osc=70114000002JNwKAAW&s_iid=70114000002JHs3AAG) vendas do AEM Forms para comprar o complemento Document Security.

### Proteger documentos {#protect-documents}

O AEM Forms Document Security fornece várias ferramentas para aplicar políticas de segurança. Você pode escolher uma ferramenta conforme seus requisitos e especificações.

![ofertas de segurança de documentos](assets/document-security-offerings.png)

Você pode usar o Document Security SDK, o Adobe Acrobat, o Document Security Extension for Microsoft Office ou a Biblioteca de proteção portátil para aplicar e rastrear as políticas de segurança:

* **** SDK do Document Security: O SDK é um cliente rico em recursos. Você pode usar o Document Security SDK para acessar a funcionalidade do servidor de documentos, abrir documentos protegidos por política e desenvolver extensões personalizadas, plug-ins ou aplicativos. Por exemplo, você pode desenvolver extensões para proteger formatos de arquivo personalizados ou integrar o SDK às soluções de Prevenção de perda de dados (DLP). Extensões, aplicativos e plug-ins desenvolvidos usando o Document Security SDK enviam documentos para o servidor AEM Forms designado e as políticas são aplicadas no servidor. Observe também que o SDK do cliente de segurança de documento do AEM Forms (CSDK) não pode desproteger os documentos protegidos usando a biblioteca de proteção portátil (PPL) e vice-versa.

   O Document Security SDK está disponível para Java e C++. O Java SDK está incluído na oferta AEM Forms Document Security e é instalado na implantação de formulários AEM no JEE. Você pode entrar em contato com a equipe [de suporte do](https://helpx.adobe.com/marketing-cloud/contact-support.html) AEM para adquirir o SDK C++. O SDK C++ pode ser compilado com o Microsoft Visual Studio 2013. Você pode visitar o site de documentação [da API do](https://help.adobe.com/en_US/livecycle/11.0/Services/WS92d06802c76abadb76c48dfe12dbeb3e281-7ff0.2.html) Document Security para saber e usar os recursos do SDK.

* **** Adobe Acrobat: Você pode usar o Adobe Acrobat para aplicar política de segurança a documentos PDF que criam aplicativos de desktop populares, como Microsoft Office, navegadores da Web ou qualquer aplicativo que suporte impressão em formato PDF.

   Você pode comprar e baixar o Adobe Acrobat do site da [Adobe](https://acrobat.adobe.com/us/en/free-trial-download.html). O artigo do Adobe Acrobat que [configura políticas de segurança para PDFs](https://helpx.adobe.com/acrobat/using/setting-security-policies-pdfs.html) fornece informações detalhadas sobre como criar e aplicar políticas no Adobe Acrobat.

* **Document Security Extension for Microsoft Office**: Você pode usar o Document Security Extension for Microsoft Office para aplicar políticas predefinidas a seus arquivos do Microsoft Office a partir dos programas do Microsoft Office. A extensão garante que somente pessoas autorizadas possam usar arquivos do Microsoft Word, Excel e PowerPoint protegidos por política. Somente usuários autorizados que tenham o plug-in instalado podem usar os arquivos protegidos por política.

   A extensão do Document Security está disponível como um plug-in do Microsoft Office. Você pode entrar em contato com a equipe [de suporte do](https://helpx.adobe.com/ca/marketing-cloud/contact-support.html) AEM para adquirir a extensão. Posteriormente, você poderá visitar a ajuda do [Document Security Extension for Microsoft Office](https://helpx.adobe.com/aem-forms/aem-document-security/aem-document-security-extension-help.html) para saber mais sobre a instalação, configuração e uso da extensão.

* **** Biblioteca de proteção portátil: A Biblioteca de proteção portátil (PPL) protege um documento localmente, sem enviá-lo para o servidor de formulários AEM. Somente as credenciais de segurança e os detalhes da política viajam pela rede. O PPL também permite limitar o acesso de recuperação de política somente para usuários conectados. Você pode buscar políticas com o contexto do usuário conectado ao usuário do AEM.

   Juntamente com o acima, a Biblioteca de proteção portátil tem todos os recursos do Document Security SDK. Você pode usar o Document Security SDK para acessar a funcionalidade do servidor de documentos, abrir documentos protegidos por política e desenvolver extensões personalizadas, plug-ins ou aplicativos. Observe também que a biblioteca de proteção portátil (PPL) não pode desproteger os documentos protegidos usando o SDK (CSDK) do cliente de segurança de documento do AEM Forms e vice-versa.

   A Biblioteca de proteção portátil está disponível para Java e C++ em versões de 32 bits e 64 bits. Ele também está disponível como um pacote OSGi para o AEM Forms no OSGi. O PPL C++ pode ser compilado com o Microsoft Visual Studio 2013. Se você tiver licenciado o complemento AEM Forms Document Security, entre em contato com a equipe de suporte do [AEM Forms Document Security](https://helpx.adobe.com/marketing-cloud/contact-support.html) para adquirir a Biblioteca de proteção portátil. Posteriormente, você poderá usar a Ajuda da Biblioteca de proteção portátil (fornecida com a biblioteca) para configurar e usar a Biblioteca de proteção portátil.

### Exibir ou editar documentos protegidos {#view-or-edit-protected-documents}

* Para documentos **** PDF, você pode usar o Adobe Acrobat DC, o Acrobat Reader e o Acrobat Reader Mobile para exibir documentos PDF protegidos. A maioria dos usuários já tem o Acrobat Reader instalado em seus dispositivos, portanto, não é necessário obter ou aprender software adicional para exibir documentos protegidos. Você também pode baixar o Acrobat Reader do site [de download do](https://get.adobe.com/reader/)Acrobat Reader.

* Para documentos **do** Microsoft Office, você precisa do Microsoft Office e da extensão AEM Forms Document Security para Microsoft Office. A extensão do Document Security está disponível como um plug-in do Microsoft Office. Você pode baixar a extensão do site da Adobe.

### Indexar documentos protegidos {#index-protected-documents}

Os mecanismos de pesquisa de texto completo do Microsoft Windows (servidor SharePoint Index) e do Adobe Experience Manager (AEM) podem executar pesquisa de texto completo em formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você pode usar indexadores do Document Security para permitir que mecanismos de pesquisa de texto completo pesquisem documentos PDF protegidos:

* **** Indexador do iFilter: Você pode usar o indexador iFilter para indexar documentos PDF protegidos e habilitar os mecanismos de pesquisa de texto completo do Microsoft Windows (Serviço de Indexação de Área de Trabalho e Servidor de Indexação do SharePoint) para pesquisar documentos PDF protegidos. Para obter informações detalhadas, consulte IFilter do [AEM SharePoint para documentos](assets/sharepoint-ifilter-doc-security.pdf)protegidos.

* **** Indexador do AEM Forms Document Security: Você pode usar o indexador do AEM Forms Document Security para indexar documentos PDF protegidos e permitir que o Adobe Experience Manager pesquise documentos PDF protegidos. Os indexadores fazem parte da oferta AEM Forms Document Security. Eles estão incluídos no AEM Forms em instaladores JEE.

