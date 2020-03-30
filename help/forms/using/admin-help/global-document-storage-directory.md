---
title: Diretório global do armazenamento do documento
seo-title: Diretório global do armazenamento do documento
description: O diretório global documento armazenamento (GDS) é um diretório usado para armazenar arquivos de longa duração usados em um processo.
seo-description: O diretório global documento armazenamento (GDS) é um diretório usado para armazenar arquivos de longa duração usados em um processo.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Diretório global do armazenamento do documento{#global-document-storage-directory}

O diretório *global documento armazenamento (GDS)* é um diretório usado para armazenar arquivos de longa duração usados em um processo. Esses arquivos incluem PDFs, políticas e modelos de formulário. Arquivos de longa duração são uma parte essencial do estado geral de muitas implantações de formulários AEM. Se alguns ou todos os documentos de longa duração forem perdidos ou corrompidos, o servidor de formulários poderá ficar instável. documentos de entrada para invocações de trabalhos assíncronos também são armazenados no diretório GDS e devem estar disponíveis para solicitações de processamento. É importante considerar a confiabilidade do sistema de arquivos que hospeda o diretório GDS. Use uma matriz redundante de discos independentes (RAID) ou outra tecnologia, conforme apropriado para suas necessidades de qualidade e nível de serviço.

Arquivos de longa duração podem conter informações confidenciais do usuário. Essas informações podem exigir credenciais especiais quando acessadas por meio das APIs de formulários do AEM ou interfaces do usuário. É importante que o diretório GDS esteja adequadamente protegido pelo sistema operacional. Somente a conta de administrador usada para executar o servidor de aplicativos deve ter acesso de leitura/gravação ao diretório GDS.

Além de selecionar um diretório seguro e altamente disponível para GDS, você também pode optar por ativar o armazenamento do documento no banco de dados. Observe que mesmo com o uso do banco de dados de formulários AEM para o documento, os formulários AEM ainda precisam do diretório GDS. (Consulte Opções [de backup quando o banco de dados é usado para o armazenamento](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage)do documento.)

Os dados do aplicativo de formulários AEM residem no diretório GDS e no banco de dados de formulários AEM. A tabela a seguir descreve os dados e seus locais.

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
   <td><p>Dados do aplicativo (usuários, funções, processos, políticas, pontos de extremidade, eventos etc.)</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>container de serviço implantados</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Gerenciador de Documentos </p></td>
   <td><p>Não</p></td>
   <td><p>Sim</p></td>
  </tr>
  <tr>
   <td><p>Repositório de formulários</p></td>
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

O local do diretório GDS pode ser configurado manualmente durante o processo de instalação dos formulários AEM. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos da seguinte maneira:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Alterar a localização padrão do GDS {#change-the-default-gds-location}

Você pode alterar o local do GDS no console de administração depois que a instalação dos formulários AEM for concluída. Você deve realocar os dados manualmente para concluir o processo.

>[!NOTE]
>
>Migre os dados da seguinte maneira ou ocorrerá perda de dados.

1. Faça logon no console de administração e clique em Configurações > Configurações principais do sistema > Configurações.
1. Na caixa Diretório Global do Armazenamento do Documento, digite o caminho completo para o novo diretório GDS e clique em OK.
1. Encerre imediatamente o servidor de aplicativos.
1. Mova todos os arquivos do diretório GDS antigo para o novo local, mantendo a estrutura do diretório interno.
1. Reinicie o servidor de aplicativos.

## Sobre os arquivos de implantação {#about-deployment-files}

Os formulários AEM consistem em dois tipos de arquivos de implantação, os container de serviço e os arquivos Java 2 Platform, Enterprise Edition (J2EE) EAR. Os arquivos EAR consistem em pacotes padrão de aplicativos J2EE que contêm a funcionalidade principal dos formulários AEM. Os arquivos EAR específicos do servidor de aplicativos são os seguintes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[OS]*.ear

A implementação de formulários AEM envolve a implantação de arquivos EAR montados e de suporte para o servidor de aplicativos, onde você planeja executar sua solução de formulários AEM. Se você configurou e montou vários módulos, os módulos implantáveis são compactados dentro dos arquivos EAR implantáveis. Para implantar esses arquivos, copie-os na página inicial do *[appserver]*\server\all\deploy directory.

Os módulos e arquivos de arquivamento de formulários AEM são empacotados em arquivos JAR. Como não são arquivos do tipo J2EE, eles não são implantados no servidor de aplicativos. Em vez disso, eles são copiados para o diretório GDS e uma referência para sua localização é armazenada no banco de dados de formulários AEM. Por isso, o diretório GDS deve ser compartilhado entre todos os nós do cluster. Todos os nós devem ter acesso ao diretório central do armazenamento para os DSCs.

>[!NOTE]
>
>Antes de implantar os container de serviço, verifique se você criou e configurou o diretório GDS. (Consulte [Configuração do diretório](global-document-storage-directory.md#configuring-the-gds-directory)GDS)

