---
title: Permitir que AEM pesquise documentos PDF protegidos pela segurança do documento
seo-title: Permitir que AEM pesquise documentos PDF protegidos pela segurança do documento
description: 'Saiba como habilitar a pesquisa de AEM nativa para executar a pesquisa de texto completo em documentos PDF protegidos por DRM.  '
seo-description: 'Saiba como habilitar a pesquisa de AEM nativa para executar a pesquisa de texto completo em documentos PDF protegidos por DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
feature: Document Security
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 1%

---


# Permitir que AEM pesquise documentos PDF protegidos pela segurança do documento{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM pesquisa é capaz de pesquisar e localizar AEM ativos e executar pesquisa de texto em vários formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Também é possível estender a pesquisa nativa para realizar a pesquisa de texto completo em [PDF Documents protegidos com AEM segurança do documento](../../forms/using/admin-help/document-security.md). Para permitir que o AEM execute a pesquisa de texto completo em tais documentos, execute as seguintes etapas:

1. Estabelecer uma conexão segura
1. Indexar um documento PDF protegido por política de exemplo

## Pré-requisitos {#prerequisites}

* Se estiver usando o AEM Forms no OSGi:

   * Instale o [pacote AEM Forms Document Security Indexer](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) no servidor AEM Forms.

   * Certifique-se de que um AEM Forms no servidor JEE esteja ativo e em execução e que a segurança do documento esteja instalada no AEM Forms correspondente no servidor JEE. O Formulário AEM no servidor JEE é necessário para indexar o documento protegido.

* Se você estiver usando somente o AEM Forms no servidor JEE, o pacote de indexador já estará instalado.
* Certifique-se de que todos os pacotes estejam funcionando. Se todos os pacotes não estiverem ativos, espere até que todos os pacotes estejam ativos e em execução.

   * Para AEM Forms no OSGi, os pacotes são listados em https://&#39;[server]:[port]&#39;/system/console/bundles.
   * Para AEM Forms no JEE, os pacotes são listados em https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Por exemplo https://localhost:8080/lc/system/console/bundles.

* Adicione o pacote *sun.util.calendar* à  lista de permissões. Para adicionar o pacote à  lista de permissões, execute as seguintes etapas:

   1. Abra AEM Console da Web. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Localize e abra **Configuração do firewall de desserialização**.

   1. Adicione o pacote sun.util.calendar ao campo Incluir na lista de permissões classes ou prefixos de pacote e clique em **Salvar**.

### Estabelecer uma conexão segura entre as pilhas AEM Forms JEE e OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Você pode usar um dos seguintes métodos para estabelecer a conexão segura:

* Configurar o pacote SDK do cliente do Adobe LiveCycle com o AEM Forms em credenciais de administrador do JEE
* Configurar o pacote SDK do cliente do Adobe LiveCycle usando autenticação mútua

#### Configurar o pacote SDK do cliente do Adobe LiveCycle com o AEM Forms em credenciais de administrador do JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM Console da Web. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o **Pacote do SDK do cliente do Adobe LiveCycle**. Especifique o valor para os seguintes campos:

   * **URL do servidor:** especifique o URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o servidor com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Nome** do serviço: Adicione o RightsManagementService à lista de serviços especificados.
   * **Nome de usuário:** especifique o nome de usuário da AEM Forms na conta JEE a ser usada para iniciar chamadas AEM servidor. A conta especificada deve ter permissões para iniciar serviços de documento no AEM Forms no servidor JEE.
   * **Senha**: Especifique a senha da AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. AEM é ativado para pesquisar documentos PDF protegidos pela segurança do documento.

#### Configurar o pacote SDK do cliente do Adobe LiveCycle usando autenticação mútua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e Autenticação Mútua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM Console da Web. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o pacote **Adobe LiveCycle Client SDK**. Especifique o valor das seguintes propriedades:

   * **URL** do servidor: Especifique o URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o servidor AEM com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> .
   * **Habilitar SSL** de 2 vias: Habilite a opção Habilitar SSL de 2 vias.
   * **URL** do arquivo KeyStore: Especifique o URL do arquivo de repositório de chaves.
   * **URL** do arquivo de confiança: Especifique o URL do arquivo truststore.
   * **Senha** do KeyStore: Especifique a senha do arquivo de repositório de chaves.
   * **TrustStorePassword**: Especifique a senha para o arquivo truststore.
   * **Nome** do serviço: Adicione o RightsManagementService à lista de serviços especificados.

   Clique em **Salvar**. AEM é ativado para pesquisar documentos PDF protegidos pela segurança do documento

### Indexar um documento PDF de exemplo protegido por política {#index-a-sample-policy-protected-pdf-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e faça upload dos documentos PDF protegidos por política para a pasta recém-criada.

   Agora, você pode pesquisar os documentos protegidos por política usando AEM pesquisa.

