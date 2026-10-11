---
title: Permitir que o AEM pesquise documentos do PDF e do Microsoft Office protegidos por segurança de documentos
description: Saiba como habilitar a pesquisa nativa do AEM para executar a pesquisa de texto completo em documentos do PDF protegidos por DRM.
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 0%
---
# Permitir que o AEM pesquise documentos do PDF e do Microsoft Office protegidos por segurança de documentos{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

O Adobe Experience Manager fornece uma interface para pesquisar e localizar vários ativos armazenados no AEM. A pesquisa nativa é capaz de pesquisar e localizar ativos do AEM e executar pesquisa de texto em vários formatos de documento usados com frequência, como arquivos de texto simples, documentos do Microsoft Office e documentos do PDF. Você também pode estender e habilitar a pesquisa nativa para executar a pesquisa de texto completo em documentos do PDF e do Microsoft Office protegidos por DRM.

Execute as seguintes etapas para permitir que o AEM pesquise documentos protegidos do PDF e do Microsoft Office:

## Antes de começar {#before-you-start}

* Instale e configure a Segurança de documentos do AEM Forms.
* Adicione o pacote sun.util.calendar ao incluo na lista de permissões da **Configuração do firewall de desserialização.** Configuração listada em `https://'[server]:[port]'/system/console/configMgr`.
* Verifique se todos os pacotes do AEM estão em funcionamento. Os pacotes estão listados em `https://'[server]:[port]'/system/console/bundles`. Se todos os pacotes não estiverem ativos, aguarde e verifique o status dos pacotes depois de por alguns minutos.

## Estabelecer uma conexão segura no fluxo de trabalho do AEM Forms (AEM Forms no JEE) {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

Uma conexão segura permite o fluxo contínuo de informações entre o AEM Forms no JEE e os serviços OSGi em execução no mesmo servidor. Use um dos métodos a seguir para estabelecer uma conexão segura:

* Configurar o pacote AEM Forms Client SDK com o AEM Forms nas credenciais do administrador do JEE
* Configurar o pacote AEM Forms Client SDK usando autenticação mútua

### Configurar o pacote AEM Forms Client SDK com o AEM Forms nas credenciais do administrador do JEE {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra o gerenciador de configurações do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o pacote AEM Forms Client SDK. Especifique o valor para as seguintes propriedades:

   * **URL do Servidor:** Especifique a URL HTTP do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.
   * **Nome de usuário:** especifique o nome de usuário da conta do AEM Forms no JEE a ser usada para iniciar chamadas do AEM Forms no servidor JEE. A conta especificada deve ter permissões para chamar Serviços de documento no AEM Forms no servidor JEE.
   * **Senha**: especifique a senha da AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos do PDF e do Microsoft Office protegidos por segurança de documentos.

### Configurar o pacote AEM Forms Client SDK usando autenticação mútua {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para o AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e autenticação mútua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra o gerenciador de configurações do AEM e faça logon como administrador. O URL padrão é https://&lt;serverName>:&lt;port>/lc/system/console/configMgr.
1. Pesquise e abra o pacote AEM Forms Client SDK. Especifique o valor para as seguintes propriedades:

   * **URL do Servidor:** Especifique a URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação por https, reinicie o AEM Forms no servidor JEE com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Habilitar SSL bidirecional**: habilitar a opção Habilitar SSL bidirecional.
   * **URL do Arquivo do KeyStore**: especifique a URL do arquivo do keystore.
   * **URL do arquivo TrustStore**: especifique a URL do arquivo truststore.
   * **Senha do KeyStore**: especifique a senha para o arquivo de keystore.
   * **TrustStorePassword**: especifique a senha para o arquivo truststore.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos do PDF e do Microsoft Office protegidos por segurança de documentos

   >[!NOTE]
   >
   > É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

## Indexar um exemplo de documento do PDF ou do Microsoft Office protegido por política {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e faça upload de um documento do PDF ou do Microsoft Office protegido por política para a pasta recém-criada. Agora, pesquise o conteúdo dos documentos protegidos por política usando a pesquisa do AEM. Ele deve retornar o documento contendo o texto pesquisado.
