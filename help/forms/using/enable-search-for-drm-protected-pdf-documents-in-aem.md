---
title: Permitir que o AEM pesquise documentos PDF protegidos por segurança de documentos

description: Saiba como habilitar a pesquisa nativa do AEM para executar a pesquisa de texto completo em documentos do PDF protegidos por DRM.


contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security

docset: aem65

feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%
---
# Permitir que o AEM pesquise documentos PDF protegidos por segurança de documentos{#enable-aem-to-search-document-security-protected-pdf-documents}

A pesquisa do AEM é capaz de pesquisar e localizar ativos do AEM e executar pesquisa de texto em vários formatos de documento usados com frequência, como arquivos de texto simples, documentos do Microsoft Office e documentos do PDF. Você também pode estender a pesquisa nativa para executar a pesquisa de texto completo nos [Documentos do PDF protegidos com a Segurança de documentos do AEM](../../forms/using/admin-help/document-security.md). Para permitir que o AEM execute a pesquisa de texto completo nesses documentos, execute as seguintes etapas:

1. Estabelecer uma conexão segura
1. Indexar um exemplo de documento do PDF protegido por política

## Pré-requisitos {#prerequisites}

* Se estiver usando o AEM Forms no OSGi:

  * Instale o [pacote do AEM Forms Document Security Indexer](https://helpx.adobe.com/br/aem-forms/kb/aem-forms-releases.html) no servidor do AEM Forms.

  * Verifique se um AEM Forms no servidor JEE está em execução e se a segurança de documentos está instalada no AEM Forms correspondente no servidor JEE. O AEM Form no servidor JEE é necessário para indexar o documento protegido.

* Se você estiver usando somente o AEM Forms no servidor JEE, o pacote indexador já está instalado.
* Verifique se todos os pacotes estão em funcionamento. Se todos os pacotes não estiverem ativos, aguarde até que todos os pacotes estejam em execução.

  * Para o AEM Forms no OSGi, os pacotes estão listados em https://&#39;[server]:[port]&#39;/system/console/bundles.
  * Para o AEM Forms no JEE, os pacotes estão listados em https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. Por exemplo, https://localhost:8080/lc/system/console/bundles.

* Adicione o pacote *sun.util.calendar* ao incluo na lista de permissões. Para adicionar o pacote ao incluo na lista de permissões, execute as seguintes etapas:

  1. Abra o Console da Web do AEM. A URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
  1. Localize e abra a **Configuração do Firewall de Desserialização**.

  1. Adicione o pacote sun.util.calendar ao campo de classes ou prefixos de pacote e clique em **Salvar**.

### Estabelecer uma conexão segura entre o AEM Forms JEE e as pilhas OSGi {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

Você pode usar um dos seguintes métodos para estabelecer a conexão segura:

* Configurar o pacote Adobe LiveCycle Client SDK com as credenciais de administrador do AEM Forms no JEE
* Configurar o pacote Adobe LiveCycle Client SDK usando autenticação mútua

#### Configurar o pacote Adobe LiveCycle Client SDK com as credenciais de administrador do AEM Forms no JEE {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. Abra o Console da Web do AEM. A URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o **Pacote do Adobe LiveCycle Client SDK**. Especifique o valor para os seguintes campos:

   * **URL do Servidor:** Especifique a URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação via https, reinicie o servidor com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.
   * **Nome de usuário:** especifique o nome de usuário da conta do AEM Forms no JEE a ser usada para iniciar chamadas do servidor AEM. A conta especificada deve ter permissões para iniciar serviços de documento no AEM Forms no servidor JEE.
   * **Senha**: especifique a senha da AEM Forms na conta JEE mencionada no campo Nome de usuário.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos do PDF protegidos por segurança de documentos.

#### Configurar o pacote Adobe LiveCycle Client SDK usando autenticação mútua {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. Ative a autenticação mútua para o AEM Forms no JEE. Para obter informações detalhadas, consulte [CAC e autenticação mútua](https://helpx.adobe.com/livecycle/kb/cac-mutual-authentication.html).
1. Abra o Console da Web do AEM. A URL é https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. Localize e abra o Pacote **Adobe LiveCycle Client SDK**. Especifique o valor para as seguintes propriedades:

   * **URL do servidor**: especifique a URL HTTPS do AEM Forms no servidor JEE. Para habilitar a comunicação via https, reinicie o servidor do AEM com o parâmetro -Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file>.
   * **Habilitar SSL bidirecional**: habilitar a opção Habilitar SSL bidirecional.
   * **URL do Arquivo do KeyStore**: especifique a URL do arquivo do keystore.
   * **URL do arquivo TrustStore**: especifique a URL do arquivo truststore.
   * **Senha do KeyStore**: especifique a senha para o arquivo de keystore.
   * **TrustStorePassword**: especifique a senha para o arquivo truststore.
   * **Nome do Serviço**: adicione o RightsManagementService à lista de serviços especificados.

   Clique em **Salvar**. O AEM está habilitado para pesquisar documentos do PDF protegidos por segurança de documentos

### Indexar um exemplo de documento do PDF protegido por política {#index-a-sample-policy-protected-pdf-document}

1. Faça logon no AEM Assets como administrador.
1. Crie uma pasta no AEM Digital Asset Manager e faça upload dos documentos do PDF protegidos por política para a pasta recém-criada.

   Agora, você pode pesquisar os documentos protegidos por política usando a pesquisa do AEM.

   >[!NOTE]
   >
   > É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.
