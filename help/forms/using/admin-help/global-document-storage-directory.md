---
title: Diretório de armazenamento de documentos global
seo-title: Global document storage directory
description: O diretório global document storage (GDS) é um diretório usado para armazenar arquivos de longa duração usados em um processo.
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 1%

---

# Diretório de armazenamento de documentos global{#global-document-storage-directory}

O *armazenamento global de documentos (GDS)* diretory é um diretório usado para armazenar arquivos de longa duração usados em um processo. Esses arquivos incluem PDF, políticas e modelos de formulário. Arquivos de longa duração são uma parte essencial do estado geral de muitas implantações de formulários AEM. Se alguns ou todos os documentos de longa duração forem perdidos ou corrompidos, o servidor de formulários poderá se tornar instável. Os documentos de entrada para invocações assíncronas de trabalhos também são armazenados no diretório GDS e devem estar disponíveis para processar solicitações. É importante considerar a confiabilidade do sistema de arquivos que hospeda o diretório GDS. Use uma matriz redundante de discos independentes (RAID) ou outra tecnologia adequada para suas necessidades de qualidade e nível de serviço.

Arquivos de vida longa podem conter informações confidenciais do usuário. Essas informações podem exigir credenciais especiais quando acessadas usando as APIs de formulários AEM ou interfaces do usuário. É importante que o diretório GDS seja devidamente protegido por meio do sistema operacional. Somente a conta de administrador usada para executar o servidor de aplicativos deve ter acesso de leitura/gravação ao diretório GDS.

Além de selecionar um diretório seguro e altamente disponível para GDS, você também pode optar por habilitar o armazenamento de documentos no banco de dados. Observe que, mesmo usando o banco de dados de formulários AEM para armazenamento de documentos, AEM formulários ainda requer o diretório GDS. (Consulte [Opções de backup quando o banco de dados é usado para armazenamento de documentos](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

AEM dados do aplicativo forms estão no diretório GDS e no banco de dados AEM forms. A tabela a seguir descreve os dados e suas localizações.

<table>
 <thead>
  <tr>
   <th><p>Dados de formulários AEM</p></th>
   <th><p>Banco de dados</p></th>
   <th><p>GDS</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Dados do aplicativo (usuários, funções, processos, políticas, endpoints, eventos e assim por diante).</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Contêineres de serviço implantados</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Gerenciador de documentos </p></td>
   <td><p>Não</p></td>
   <td><p>Sim</p></td>
  </tr>
  <tr>
   <td><p>Repositório Forms</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Configuração do sistema</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Pastas vigiadas</p></td>
   <td><p>Não</p></td>
   <td><p>Sim</p></td>
  </tr>
 </tbody>
</table>

## Configuração do diretório GDS {#configuring-the-gds-directory}

A localização do diretório GDS pode ser configurada manualmente durante o processo de instalação dos formulários AEM. Se a configuração de localização permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos da seguinte maneira:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Alterar a localização padrão do GDS {#change-the-default-gds-location}

Você pode alterar o local do GDS no console de administração depois que a instalação dos formulários AEM for concluída. Você deve realocar os dados manualmente para concluir o processo.

>[!NOTE]
>
>Migre os dados da seguinte maneira ou ocorrerá perda de dados.

1. Faça logon no console de administração e clique em Configurações > Configurações principais do sistema > Configurações.
1. Na caixa Diretório de armazenamento de documentos global, digite o caminho completo para o novo diretório GDS e clique em OK.
1. Encerre imediatamente o servidor de aplicativos.
1. Mova todos os arquivos do diretório GDS antigo para o novo local, mantendo a estrutura do diretório interno.
1. Reinicie o servidor de aplicativos.

## Sobre arquivos de implantação {#about-deployment-files}

AEM formulários consiste em dois tipos de arquivos de implantação: os contêineres de serviço e os arquivos EAR Java 2 Platform, Enterprise Edition (J2EE). Os arquivos EAR consistem em pacotes de aplicativos J2EE padrão que contêm a funcionalidade principal de formulários AEM. Os arquivos EAR específicos do servidor de aplicativos são os seguintes:

* adobe-core *[appserver]*.ear
* adobe-core *[appserver]*-*[SO]*.ear

A implementação AEM formulários envolve a implantação dos arquivos EAR montados e de suporte no servidor de aplicativos, onde você planeja executar a solução de formulários AEM. Se você configurou e montou vários módulos, os módulos implantáveis são compactados dentro dos arquivos EAR implantáveis. Para implantar esses arquivos, copie-os na *[página inicial do appserver]*\server\all\deploy directory.

Os módulos e arquivos de formulários AEM são empacotados em arquivos JAR. Como não são arquivos do tipo J2EE, eles não são implantados no servidor de aplicativos. Em vez disso, elas são copiadas para o diretório GDS e uma referência à localização é armazenada no banco de dados de formulários AEM. Por esse motivo, o diretório GDS deve ser compartilhado entre todos os nós do cluster. Todos os nós devem ter acesso ao diretório de armazenamento central para os DSCs.

>[!NOTE]
>
>Antes de implantar os contêineres de serviço, verifique se você criou e configurou o diretório GDS. (Consulte [Configuração do diretório GDS](global-document-storage-directory.md#configuring-the-gds-directory))
