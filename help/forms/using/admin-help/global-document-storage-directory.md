---
title: Diretório de armazenamento de documentos global
seo-title: Global document storage directory
description: O diretório de armazenamento global de documentos (GDS) é um diretório usado para armazenar arquivos de longa duração que são usados em um processo.
seo-description: The global document storage (GDS) directory is a directory used to store long-lived files that are used within a process.
uuid: 7681672c-a0dc-4445-8004-1b1e2ed3d301
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a33b8834-6e39-47eb-a53b-0982d32e80ad
exl-id: 7a64a643-808b-4644-8fd3-0dafe83e8dd9
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# Diretório de armazenamento de documentos global{#global-document-storage-directory}

A variável *armazenamento global de documentos (GDS)* diretório é um diretório usado para armazenar arquivos de longa duração que são usados em um processo. Esses arquivos incluem PDF, políticas e modelos de formulário. Arquivos de longa duração são uma parte essencial do estado geral de muitas implantações de formulários AEM. Se alguns ou todos os documentos de longa duração forem perdidos ou corrompidos, o Forms Server poderá se tornar instável. Os documentos de entrada para invocações de trabalho assíncrono também são armazenados no diretório GDS e devem estar disponíveis para processar solicitações. É importante considerar a confiabilidade do sistema de arquivos que hospeda o diretório GDS. Use um storage redundante de discos independentes (RAID) ou outra tecnologia, conforme apropriado para suas necessidades de qualidade e nível de serviço.

Arquivos de longa duração podem conter informações confidenciais do usuário. Essas informações podem exigir credenciais especiais quando acessadas usando as APIs de formulários AEM ou as interfaces do usuário. É importante que o diretório GDS seja adequadamente protegido pelo sistema operacional. Somente a conta de administrador usada para executar o servidor de aplicativos deve ter acesso de leitura/gravação ao diretório GDS.

Além de selecionar um diretório seguro e altamente disponível para GDS, você também pode optar por habilitar o armazenamento de documentos no banco de dados. Observe que mesmo com o uso do banco de dados de formulários AEM para armazenamento de documentos, os formulários AEM ainda exigem o diretório GDS. (Consulte [Opções de backup quando o banco de dados é usado para armazenamento de documentos](/help/forms/using/admin-help/files-back-recover.md#backup-options-when-database-is-used-for-document-storage).)

Os dados de aplicativos de formulários AEM residem no diretório GDS e no banco de dados de formulários AEM. A tabela a seguir descreve os dados e seus locais.

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
   <td><p>Dados de aplicativos (usuários, funções, processos, políticas, endpoints, eventos etc.)</p></td>
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
   <td><p>Repositório do Forms</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Configuração do sistema</p></td>
   <td><p>Sim</p></td>
   <td><p>Não</p></td>
  </tr>
  <tr>
   <td><p>Pastas monitoradas</p></td>
   <td><p>Não</p></td>
   <td><p>Sim</p></td>
  </tr>
 </tbody>
</table>

## Configuração do diretório GDS {#configuring-the-gds-directory}

A localização do diretório GDS pode ser configurada manualmente durante o processo de instalação dos formulários AEM. Se a configuração de local permanecer vazia durante a instalação, o local assumirá como padrão um diretório na instalação do servidor de aplicativos da seguinte maneira:

* (JBoss) `[appserver root]/server/[type]/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/DocumentServer/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

## Alterar a localização padrão do GDS {#change-the-default-gds-location}

Você pode alterar a localização do GDS no console de administração após a conclusão da instalação dos formulários AEM. Realoque manualmente os dados para concluir o processo.

>[!NOTE]
>
>Migre os dados da seguinte maneira ou ocorrerá perda de dados.

1. Faça logon no console de administração e clique em Configurações > Configurações do sistema principal > Configurações.
1. Na caixa Diretório de armazenamento de documentos global, digite o caminho completo para o novo diretório GDS e clique em OK.
1. Desative imediatamente o servidor de aplicativos.
1. Mova todos os arquivos do diretório GDS antigo para o novo local, mantendo a estrutura do diretório interno.
1. Reinicie o servidor de aplicativos.

## Sobre Arquivos de Implantação {#about-deployment-files}

Os formulários AEM consistem em dois tipos de arquivos de implantação, os containers de serviço e os arquivos EAR da Plataforma Java 2, Enterprise Edition (J2EE). Os arquivos EAR consistem em pacotes de aplicativos J2EE padrão que contêm a funcionalidade principal dos formulários AEM. Os arquivos EAR específicos do servidor de aplicativos são os seguintes:

* adobe-core-*[appserver]*.ear
* adobe-core-*[appserver]*-*[SO]*.ear

A implementação de formulários AEM envolve a implantação dos arquivos EAR montados e dos arquivos de suporte no servidor de aplicativos, onde você planeja executar a solução de formulários AEM. Se você configurou e montou vários módulos, os módulos implantáveis são empacotados dentro dos arquivos EAR implantáveis. Para implantar esses arquivos, copie-os no *[página inicial do appserver]* diretório \server\all\deploy.

Módulos e arquivos de formulários AEM são empacotados em arquivos JAR. Como não são arquivos do tipo J2EE, eles não são implantados no servidor de aplicativos. Em vez disso, eles são copiados para o diretório GDS e uma referência a seu local é armazenada no banco de dados de formulários AEM. Por esse motivo, o diretório GDS deve ser compartilhado entre todos os nós do cluster. Todos os nós devem ter acesso ao diretório de armazenamento central para os DSCs.

>[!NOTE]
>
>Antes de disponibilizar os contêineres de serviço, certifique-se de ter criado e configurado o diretório GDS. (Consulte [Configuração do diretório GDS](global-document-storage-directory.md#configuring-the-gds-directory))
