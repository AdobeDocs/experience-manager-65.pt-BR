---
title: Permitir que o AEM pesquise documentos protegidos por segurança de documentos no PDF e no Microsoft Office
description: Saiba como habilitar a pesquisa nativa de AEM para executar a pesquisa de texto completo em documentos PDF protegidos por DRM.
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 0%

---

# Permitir que o AEM pesquise documentos protegidos por segurança de documentos no PDF e no Microsoft Office{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

O Adobe Experience Manager fornece uma interface para pesquisar e localizar vários ativos armazenados no AEM. A pesquisa nativa é capaz de pesquisar e localizar ativos AEM e realizar pesquisas de texto em vários formatos de documento comumente usados, como arquivos de texto simples, documentos do Microsoft Office e documentos PDF. Você também pode estender e habilitar a pesquisa nativa para executar a pesquisa de texto completo em documentos do PDF e do Microsoft Office protegidos por DRM.

Execute as seguintes etapas para permitir que o AEM pesquise documentos protegidos do PDF e do Microsoft Office:

## Antes de começar {#before-you-start}

* Instale e configure a Segurança de documentos do AEM Forms.
* Incluir na lista de permissões Adicione o pacote sun.util.calendar ao arquivo da **Configuração do firewall de desserialização.** Configuração listada em `https://'[server]:[port]'/system/console/configMgr`.
* Certifique-se de que todos os pacotes AEM estejam funcionando. Os pacotes estão listados em `https://'[server]:[port]'/system/console/bundles`. Se todos os pacotes não estiverem ativos, aguarde e verifique o status dos pacotes depois de por alguns minutos.

## Estabelecer uma conexão segura no fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Uma conexão segura permite o fluxo contínuo de informações entre o AEM Forms no JEE e os serviços OSGi em execução no mesmo servidor. Use um dos métodos a seguir para estabelecer uma conexão segura:

* Configurar o pacote de SDK do cliente da AEM Forms com AEM Forms nas credenciais de administrador do JEE
* Configurar o conjunto de SDKs do cliente da AEM Forms usando autenticação mútua

### Configurar o pacote de SDK do cliente da AEM Forms com AEM Forms nas credenciais de administrador do JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra o gerenciador de configuração do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o pacote AEM Forms Client SDK. Especifique o valor para as seguintes propriedades:

   * **URL do Servidor:** Especifique a URL HTTP do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.
   * **Nome de usuário:** especifique o nome de usuário da conta do AEM Forms no JEE a ser usada para iniciar chamadas do AEM Forms no servidor JEE. A conta especificada deve ter permissões para chamar Serviços de documento no AEM Forms no servidor JEE.
   * **Senha**: especifique a senha da AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. O AEM é habilitado para pesquisar documentos protegidos pelo PDF e pelo Microsoft Office.

### Configurar o conjunto de SDKs do cliente da AEM Forms usando autenticação mútua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para o AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e autenticação mútua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra o gerenciador de configuração do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o pacote AEM Forms Client SDK. Especifique o valor para as seguintes propriedades:

   * **URL do Servidor:** Especifique a URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Habilitar SSL bidirecional**: habilitar a opção Habilitar SSL bidirecional.
   * **URL do Arquivo do KeyStore**: especifique a URL do arquivo do keystore.
   * **URL do arquivo TrustStore**: especifique a URL do arquivo truststore.
   * **Senha do KeyStore**: especifique a senha para o arquivo de keystore.
   * **TrustStorePassword**: especifique a senha para o arquivo truststore.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos protegidos pelo PDF e pelo Microsoft Office

   >[!NOTE]
   >
   > É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Indexar um exemplo de PDF protegido por política ou documento do Microsoft Office {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e faça upload de um PDF ou documento do Microsoft Office protegido por política para a pasta recém-criada. Agora, pesquise o conteúdo dos documentos protegidos por política usando a pesquisa por AEM. Ele deve retornar o documento contendo o texto pesquisado.
