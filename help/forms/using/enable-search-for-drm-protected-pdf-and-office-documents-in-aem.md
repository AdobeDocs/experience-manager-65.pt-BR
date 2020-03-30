---
title: Ative o AEM para pesquisar documentos PDF e documentos do Microsoft Office protegidos por segurança
seo-title: Ative o AEM para pesquisar documentos PDF e documentos do Microsoft Office protegidos por segurança
description: Saiba como habilitar a pesquisa nativa do AEM para realizar a pesquisa de texto completo em documentos PDF protegidos por DRM.
seo-description: Saiba como habilitar a pesquisa nativa do AEM para realizar a pesquisa de texto completo em documentos PDF protegidos por DRM.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Ative o AEM para pesquisar documentos PDF e documentos do Microsoft Office protegidos por segurança{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

O Adobe Experience Manager fornece uma interface de usuário para pesquisar e localizar vários ativos armazenados no AEM. A pesquisa nativa é capaz de pesquisar e localizar ativos AEM e executar pesquisa de texto em vários formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você também pode estender e ativar a pesquisa nativa para realizar a pesquisa de texto completo em documentos PDF e Microsoft Office protegidos por DRM.

Execute as seguintes etapas para habilitar o AEM a pesquisar documentos PDF e Microsoft Office protegidos por segurança do documento:

## Antes de você iniciar {#before-you-start}

* Instale e configure a segurança do documento do AEM Forms.
* Adicione o pacote sun.util.calendário à lista de permissões da Configuração do firewall de **desserialização.** A configuração está listada em `https://'[server]:[port]'/system/console/configMgr`.
* Verifique se todos os pacotes do AEM estão ativos e em execução. Os pacotes estão listados em `https://'[server]:[port]'/system/console/bundles`. Se todos os pacotes não estiverem ativos, aguarde e verifique o status dos pacotes após alguns minutos.

## Estabeleça uma conexão segura no fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Uma conexão segura permite um fluxo contínuo de informações entre os formulários AEM no JEE e os serviços OSGi em execução no mesmo servidor. Use um dos seguintes métodos para estabelecer uma conexão segura:

* Configurar o pacote SDK do cliente AEM Forms com AEM Forms em credenciais de administrador JEE
* Configurar o pacote SDK do cliente do AEM Forms usando autenticação mútua

### Configurar o pacote SDK do cliente AEM Forms com AEM Forms em credenciais de administrador JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra o gerenciador de configuração do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;porta>/lc/system/console/configMgr.
1. Pesquise e abra o pacote SDK do cliente do AEM Forms. Especifique o valor para as seguintes propriedades:

   * **URL do servidor:** Especifique o URL HTTP de AEM Forms no servidor JEE. Para ativar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;caminho do AEM Forms no arquivo de armazenamento de chaves JEE>.
   * **Nome** do serviço: Adicione o Rights ManagementService à lista de serviços especificados.
   * **Nome de usuário:** Especifique o nome de usuário dos Formulários AEM na conta JEE a ser usada para iniciar chamadas do AEM Forms no servidor JEE. A conta especificada deve ter permissões para chamar serviços de Documento no AEM Forms no servidor JEE.
   * **Senha**: Especifique a senha do AEM Forms na conta JEE mencionada no campo Nome de usuário.
   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos PDF e do Microsoft Office protegidos pela segurança do documento.

### Configurar o pacote SDK do cliente do AEM Forms usando autenticação mútua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e autenticação](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html)mútua.
1. Abra o gerenciador de configuração do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;porta>/lc/system/console/configMgr.
1. Pesquise e abra o pacote SDK do cliente do AEM Forms. Especifique o valor para as seguintes propriedades:

   * **URL do servidor:** Especifique o URL HTTPS do AEM Forms no servidor JEE. Para ativar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;caminho do AEM Forms no arquivo de armazenamento de chaves JEE>.
   * **Habilitar SSL** de 2 vias: Ative a opção Ativar SSL de 2 vias.
   * **URL** do arquivo KeyStore: Especifique o URL do arquivo de armazenamento de chaves.
   * **URL** do arquivo TrustStore: Especifique o URL do arquivo Truststore.
   * **Senha** do KeyStore: Especifique a senha para o arquivo de armazenamento de chaves.
   * **TrustStorePassword**: Especifique a senha para o arquivo Truststore.
   * **Nome** do serviço: Adicione o Rights ManagementService à lista de serviços especificados.
   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos PDF e documentos do Microsoft Office protegidos por segurança

## Indexar um exemplo de PDF ou documento do Microsoft Office protegido por política {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Faça logon nos ativos AEM como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e carregue um PDF ou documento do Microsoft Office protegido por política para a pasta recém-criada. Agora, pesquise o conteúdo dos documentos protegidos por política usando a pesquisa do AEM. Ele deve retornar o documento que contém o texto pesquisado.

