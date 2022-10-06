---
title: Habilitar AEM para pesquisar documentos com segurança protegida PDF e documentos do Microsoft Office
seo-title: Enable AEM to search document security protected PDF and Microsoft Office documents
description: Saiba como habilitar a pesquisa de AEM nativa para executar a pesquisa de texto completo em documentos de PDF protegidos por DRM.
seo-description: Learn how to enable native AEM search to perform full-text search on DRM protected PDF documents.
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Habilitar AEM para pesquisar documentos com segurança protegida PDF e documentos do Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

O Adobe Experience Manager fornece uma interface de usuário para pesquisar e localizar vários ativos armazenados no AEM. A pesquisa nativa é capaz de pesquisar e localizar AEM ativos e executar pesquisa de texto em vários formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Também é possível estender e habilitar a pesquisa nativa para realizar a pesquisa de texto completo em documentos protegidos por DRM PDF e Microsoft Office.

Execute as seguintes etapas para permitir que o AEM pesquise documentos protegidos pelo PDF e documentos do Microsoft Office:

## Antes de você iniciar {#before-you-start}

* Instale e configure a segurança de documentos do AEM Forms.
* Adicione o pacote sun.util.calendar à  lista de permissões do **Configuração do firewall de desserialização.** A configuração é listada em `https://'[server]:[port]'/system/console/configMgr`.
* Certifique-se de que todos os pacotes de AEM estejam ativos e em execução. Os pacotes estão listados em `https://'[server]:[port]'/system/console/bundles`. Se todos os pacotes não estiverem ativos, aguarde e verifique o status dos pacotes após alguns minutos.

## Estabelecer uma conexão segura no fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Uma conexão segura permite um fluxo contínuo de informações entre o AEM Forms no JEE e os serviços OSGi em execução no mesmo servidor. Use um dos seguintes métodos para estabelecer uma conexão segura:

* Configurar o pacote SDK do cliente do AEM Forms com o AEM Forms em credenciais de administrador do JEE
* Configurar o pacote SDK do cliente do AEM Forms usando autenticação mútua

### Configurar o pacote SDK do cliente do AEM Forms com o AEM Forms em credenciais de administrador do JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra AEM gerenciador de configuração e faça logon como administrador. O URL padrão é https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o Pacote do SDK do cliente da AEM Forms. Especifique o valor das seguintes propriedades:

   * **URL do servidor:** Especifique o URL HTTP do AEM Forms no servidor JEE. Para ativar a comunicação via https, reinicie o AEM Forms no servidor JEE com o -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parâmetro.
   * **Nome do serviço**: Adicione o RightsManagementService à lista de serviços especificados.
   * **Nome de usuário:** Especifique o nome de usuário da AEM Forms na conta JEE a ser usada para iniciar chamadas do AEM Forms no servidor JEE. A conta especificada deve ter permissões para chamar serviços de Documento no AEM Forms no servidor JEE.
   * **Senha**: Especifique a senha da AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. AEM é ativado para pesquisar documentos protegidos pelo PDF e documentos do Microsoft Office.

### Configurar o pacote SDK do cliente do AEM Forms usando autenticação mútua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para AEM Forms no JEE. Para obter informações detalhadas, consulte [Autenticação CAC e Mútua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra AEM gerenciador de configuração e faça logon como administrador. O URL padrão é https://&lt;servername>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o Pacote do SDK do cliente da AEM Forms. Especifique o valor das seguintes propriedades:

   * **URL do servidor:** Especifique o URL HTTPS do AEM Forms no servidor JEE. Para ativar a comunicação via https, reinicie o AEM Forms no servidor JEE com o -Djavax.net.ssl.trustStore=&lt;path of=&quot;&quot; aem=&quot;&quot; forms=&quot;&quot; on=&quot;&quot; jee=&quot;&quot; keystore=&quot;&quot; file=&quot;&quot;> parâmetro.
   * **Habilitar SSL de 2 vias**: Habilite a opção Habilitar SSL de 2 vias.
   * **URL do arquivo KeyStore**: Especifique o URL do arquivo de repositório de chaves.
   * **URL de arquivo de confiança do TrustStore**: Especifique o URL do arquivo truststore.
   * **Senha do KeyStore**: Especifique a senha do arquivo de repositório de chaves.
   * **TrustStorePassword**: Especifique a senha para o arquivo truststore.
   * **Nome do serviço**: Adicione o RightsManagementService à lista de serviços especificados.

   Clique em **Salvar**. O AEM está ativado para procurar documentos com segurança protegida PDF e documentos do Microsoft Office

## Indexar um documento de exemplo protegido por política do PDF ou do Microsoft Office {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e faça upload de um documento do PDF ou Microsoft Office protegido por políticas para a pasta recém-criada. Agora, pesquise o conteúdo dos documentos protegidos por política usando AEM pesquisa. Ele deve retornar o documento que contém o texto pesquisado.
