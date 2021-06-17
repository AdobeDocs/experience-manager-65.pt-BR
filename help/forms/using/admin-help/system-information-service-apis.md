---
title: APIs do Serviço de informações do sistema
seo-title: APIs do Serviço de informações do sistema
description: Este documento fornece informações detalhadas sobre as APIs fornecidas pelo serviço de informações do sistema.
seo-description: Este documento fornece informações detalhadas sobre as APIs fornecidas pelo serviço de informações do sistema.
uuid: 7f624216-56e6-4d49-b9a1-3c9af045dabe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 79fccce2-d090-4b50-9c58-3f2a00e651b2
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
source-git-commit: d1fc2ff44378276522c2ff3208f5b3bdc4484bba
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# APIs do Serviço de Informações do Sistema {#system-information-service-apis}

O serviço de informação do sistema fornece um conjunto de REST APIs para recuperar informações. A tabela a seguir fornece informações detalhadas sobre as APIs:

<table>
 <thead>
  <tr>
   <th><p>Nome</p></th>
   <th><p>URL</p></th>
   <th><p>Descrição</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>SystemInfo.properties</p></td>
   <td><p>https://'[server]:[port]'/rest/services/SystemInfo.properties'</p></td>
   <td><p>Esta API é um wrapper para a API Java <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a>. Ele recupera a configuração do ambiente de trabalho atual. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera todas as variáveis de ambiente do sistema operacional host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Faz o download de um arquivo zip que contém logs do servidor de aplicativos. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera todo o conteúdo do arquivo config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera o status e os parâmetros de configuração dos AEM forms services.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Recupera o tempo de atividade do servidor, argumentos da JVM, memória do sistema, tamanho do heap, nome do sistema operacional, número de threads ativos e contagem de threads. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera valores das seguintes propriedades:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>GlobalDocumentStorageRootDir</p></li>
     <li><p>DefaultDocumentMaxInlineSize</p></li>
     <li><p>DefaultDocumentDispTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>GlobalDocumentStorageUseNetworkShare</p></li>
     <li><p>EnableFIPS</p></li>
     <li><p>EnableWSDL</p></li>
     <li><p>DataServicesConfigFile </p></li>
     <li><p>EnableRDS</p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.database</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.database</p></td>
   <td><p>Recupera informações detalhadas sobre o banco de dados.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.licenseInfo</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.licenseInfo</p></td>
   <td><p>Recupera informações de versão e licença dos componentes de formulários AEM instalados. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Faz o download dos arquivos de configuração do servidor de aplicativos host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera a contagem e o rastreamento de pilha de threads ativos. Ele aceita os seguintes parâmetros:</p>
    <ul>
     <li><p>iterações= [n]: Especifica a contagem de iterações. Substitua n por um número. </p></li>
     <li><p>Delay= [n]: Especifica o número de milissegundos a aguardar antes de iniciar a próxima iteração. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Essa API é um wrapper para todas as APIs do serviço de informações do sistema. Internamente, ele executa todas as APIs de informações do sistema e baixa informações no formato zip. </p><p><i><strong>observação</strong>: O SystemInfo.info não fornece rastreamento de contagem e pilha de threads ativos. </i></p></td>
  </tr>
 </tbody>
</table>
