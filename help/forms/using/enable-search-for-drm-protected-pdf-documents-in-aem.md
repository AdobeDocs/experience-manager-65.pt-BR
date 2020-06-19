---
title: Ative o AEM para pesquisar documentos PDF protegidos por segurança de documentos
seo-title: Ative o AEM para pesquisar documentos PDF protegidos por segurança de documentos
description: 'Saiba como habilitar a pesquisa nativa do AEM para realizar a pesquisa de texto completo em documentos PDF protegidos por DRM.  '
seo-description: 'Saiba como habilitar a pesquisa nativa do AEM para realizar a pesquisa de texto completo em documentos PDF protegidos por DRM.  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 1%

---


# Ative o AEM para pesquisar documentos PDF protegidos por segurança de documentos{#enable-aem-to-search-document-security-protected-pdf-documents}

A pesquisa do AEM é capaz de pesquisar e localizar ativos do AEM e executar pesquisa de texto em vários formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você também pode estender a pesquisa nativa para realizar a pesquisa em texto completo em Documentos [PDF protegidos com segurança](../../forms/using/admin-help/document-security.md)do Documento AEM. Para permitir que o AEM realize uma pesquisa de texto completo nesses documentos, execute as seguintes etapas:

1. Estabeleça uma conexão segura
1. Indexar um exemplo de documento PDF protegido por política

## Pré-requisitos {#prerequisites}

* Se estiver usando AEM Forms no OSGi:

   * Instale o pacote [](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) AEM Forms Documento Security Indexer no servidor AEM Forms.

   * Verifique se um AEM Forms no servidor JEE está ativo e em execução e se a segurança do documento está instalada em AEM Forms correspondentes no servidor JEE. O formulário AEM no servidor JEE é necessário para indexar o documento protegido.

* Se você estiver usando apenas AEM Forms no servidor JEE, o pacote indexador já estará instalado.
* Verifique se todos os pacotes estão ativos e em execução. Se todos os pacotes não estiverem ativos, aguarde até que todos os pacotes estejam ativos e em execução.

   * Para AEM Forms no OSGi, os pacotes são listados em https://&#39;[server]:[port]&#39;/system/console/bundles.
   * Para AEM Forms em JEE, os pacotes são listados em https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Por exemplo, https://localhost:8080/lc/system/console/bundles.

* Adicione o pacote *sun.util.calendário* à lista permitida. Para adicionar o pacote à lista de permissões, execute as seguintes etapas:

   1. Abra o console da Web do AEM. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. Localize e abra a Configuração **do Firewall de** Deserialização.

   1. Adicione o pacote sun.util.calendário ao campo Classes listadas ou prefixos de pacote e clique em **Salvar**.

### Estabeleça uma conexão segura entre as pilhas JEE e OSGi do AEM Forms {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Você pode usar um dos seguintes métodos para estabelecer a conexão segura:

* Configurar o pacote SDK do Adobe LiveCycle Client com AEM Forms nas credenciais de administrador do JEE
* Configurar o pacote SDK do Adobe LiveCycle Client usando autenticação mútua

#### Configurar o pacote SDK do Adobe LiveCycle Client com AEM Forms nas credenciais de administrador do JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra o console da Web do AEM. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o pacote SDK do **Adobe LiveCycle Client**. Especifique o valor para os seguintes campos:

   * **URL do servidor:** Especifique o URL HTTPS dos AEM Forms no servidor JEE. Para ativar a comunicação por https, reinicie o servidor com o parâmetro -Djavax.net.ssl.trustStore=&lt;caminho dos AEM Forms no arquivo de armazenamento de chaves JEE>.
   * **Nome** do serviço: Adicione o Rights ManagementService à lista de serviços especificados.
   * **Nome de usuário:** Especifique o nome de usuário dos AEM Forms na conta JEE a ser usada para iniciar chamadas do servidor AEM. A conta especificada deve ter permissões para os serviços de documento de start no servidor JEE.
   * **Senha**: Especifique a senha dos AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos PDF protegidos pela segurança do documento.

#### Configurar o pacote SDK do Adobe LiveCycle Client usando autenticação mútua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e autenticação](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)mútua.
1. Abra o console da Web do AEM. O URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o **Adobe LiveCycle Client SDK** Bundle. Especifique o valor para as seguintes propriedades:

   * **URL** do servidor: Especifique o URL HTTPS dos AEM Forms no servidor JEE. Para ativar a comunicação por https, reinicie o servidor de AEM com o parâmetro -Djavax.net.ssl.trustStore=&lt;caminho dos AEM Forms no arquivo de armazenamento de chaves JEE>.
   * **Habilitar SSL** de 2 vias: Ative a opção Ativar SSL de 2 vias.
   * **URL** do arquivo KeyStore: Especifique o URL do arquivo de armazenamento de chaves.
   * **URL** do arquivo TrustStore: Especifique o URL do arquivo Truststore.
   * **Senha** do KeyStore: Especifique a senha para o arquivo de armazenamento de chaves.
   * **TrustStorePassword**: Especifique a senha para o arquivo Truststore.
   * **Nome** do serviço: Adicione o Rights ManagementService à lista de serviços especificados.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos PDF protegidos pela segurança do documento

### Indexar um exemplo de documento PDF protegido por política {#index-a-sample-policy-protected-pdf-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e carregue os documentos PDF protegidos por política para a pasta recém-criada.

   Agora, você pode pesquisar documentos protegidos por política usando a pesquisa do AEM.

