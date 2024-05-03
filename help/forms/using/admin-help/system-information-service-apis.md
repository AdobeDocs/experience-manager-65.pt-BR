---
title: APIs de serviço de informações do sistema
description: Este documento fornece informações detalhadas sobre as APIs fornecidas pelo serviço de informações do sistema.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/system_information_service
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 4da96c8f-8bd0-4cad-9087-18e324f084e7
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# APIs de serviço de informações do sistema {#system-information-service-apis}

O serviço de informações do sistema fornece um conjunto de APIs REST para recuperar informações. A tabela a seguir fornece informações detalhadas sobre as APIs:

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
   <td><p>Essa API é um empacotador para <a href="https://docs.oracle.com/javase/6/docs/api/java/lang/System.html#getProperties()">system.getProperties</a> API Java. Recupera a configuração do ambiente de trabalho atual. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.envVar</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.envVar</p></td>
   <td><p>Recupera todas as variáveis de ambiente do sistema operacional do host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.logs</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.logs</p></td>
   <td><p>Baixa um arquivo zip que contém os logs do servidor de aplicativos. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.config</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.config</p></td>
   <td><p>Recupera todo o conteúdo do arquivo config.xml. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.services</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.services</p></td>
   <td><p>Recupera parâmetros de status e configuração de serviços de formulários AEM.</p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.vitalDetails</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.vitalDetails</p></td>
   <td><p>Recupera o tempo de atividade do servidor, argumentos JVM, memória do sistema, tamanho do heap, nome do sistema operacional, número de threads ativos e contagem de threads. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.coreSettings</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.coreSettings</p></td>
   <td><p>Recupera valores das seguintes propriedades:</p>
    <ul>
     <li><p>AdobeTempDir</p></li>
     <li><p>AdobeServerFontDir</p></li>
     <li><p>CustomerFontDir</p></li>
     <li><p>DiretórioRaizDeArmazenamentoDoDocumentoGlobal</p></li>
     <li><p>TamanhoMáxEmLinhaDoDocumentoPadrão</p></li>
     <li><p>DefaultDocumentDisposeTimeout</p></li>
     <li><p>EnableDocumentDBStorage</p></li>
     <li><p>CompartilhamentoDeRedeDeUsoDoArmazenamentoDoDocumentoGlobal</p></li>
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
   <td><p>Recupera informações de versão e licença de componentes de formulários AEM instalados. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfNo.serverConfig</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.serverConfig</p></td>
   <td><p>Baixa os arquivos de configuração do servidor de aplicativos host. </p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.threads?delay=[n]&amp;iterações=[n]</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.threads?delay=[n]&amp;iterations=[n]</p></td>
   <td><p>Recupera o rastreamento de contagem e pilha de threads ativos. Ele aceita os seguintes parâmetros:</p>
    <ul>
     <li><p>iterações= [n]: especifica a contagem de iterações. Substitua n por um número. </p></li>
     <li><p>Delay= [n]: especifica o número de milissegundos a ser aguardado antes de iniciar a próxima iteração. </p></li>
    </ul><p></p></td>
  </tr>
  <tr>
   <td><p>SystemInfo.info</p></td>
   <td><p>https://'[server]:[port]'/rest/services/ SystemInfo.info</p></td>
   <td><p>Esta API é um invólucro para todas as APIs de serviço de informações do sistema. Internamente, ele executa todas as APIs de informações do sistema e baixa informações no formato zip. </p><p><i><strong>observação</strong>: O SystemInfo.info não fornece rastreamento de contagem e pilha de threads ativos. </i></p></td>
  </tr>
 </tbody>
</table>
