---
title: Estratégia de backup e recuperação para formulários AEM
seo-title: Backup and recovery strategy for AEM forms
description: Saiba como implementar uma estratégia para fazer backup dos dados e garantir que eles permaneçam sincronizados com os dados dos formulários de AEM.
seo-description: Learn how to implement a strategy to back up data and ensuring that it remains in sync with the AEM forms data.
uuid: 98fc3115-76e5-4e58-aa30-3601866a441f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: f192a8a3-1116-4d32-9b57-b53d532c0dbf
exl-id: 01ec6ebc-6d80-4417-9604-c8571aebb57e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1491'
ht-degree: 0%

---

# Estratégia de backup e recuperação para formulários AEM{#backup-and-recovery-strategy-for-aem-forms}

Se a implementação do AEM forms armazenar dados personalizados adicionais em um banco de dados diferente, você será responsável por implementar uma estratégia para fazer backup desses dados e garantir que eles permaneçam sincronizados com os dados AEM forms. Além disso, o aplicativo deve ser projetado de forma que seja robusto o suficiente para lidar com um cenário em que os bancos de dados adicionais fiquem fora de sincronia. É altamente recomendável que qualquer operação de banco de dados executada seja feita no contexto de uma transação para ajudar a manter um estado consistente.

Depois de identificar como AEM formulários são usados, determine quais arquivos devem ser submetidos a backup, com que frequência e a janela de backup a serem disponibilizados.

>[!NOTE]
>
>Assim como em qualquer outro aspecto da implementação dos formulários de AEM, sua estratégia de backup e recuperação deve ser desenvolvida e testada em um ambiente de desenvolvimento ou de preparo antes de ser usada na produção, para garantir que toda a solução funcione conforme o esperado, sem perda de dados.

O Adobe Experience Manager (AEM) é parte integrante dos AEM formulários. Portanto, é necessário fazer backup AEM também em sincronia com AEM backup de formulários como Solução de Gerenciamento de Correspondência e serviços, como o gerente de formulários, são baseados em dados armazenados AEM parte dos formulários AEM.Para evitar perda de dados, o backup dos dados específicos dos AEM formulários deve ser feito de forma a garantir que GDS e AEM (repositório) correlacionem-se com referências de banco de dados.Os diretórios de banco de dados, GDS, AEM e Raiz de Armazenamento de Conteúdo devem ser restaurados para um computador com um computador Nome DNS como original.

## Tipos de backups {#types-of-backups}

A estratégia de backup dos formulários AEM envolve dois tipos de backups:

**Imagem do sistema:** Um backup completo do sistema que você pode usar para restaurar o conteúdo do computador se o disco rígido ou o computador inteiro parar de funcionar. Um backup de imagem do sistema é necessário somente antes da implantação de produção de formulários AEM. As políticas corporativas internas ditam a frequência com que os backups de imagem do sistema são necessários.

**Dados específicos dos formulários AEM:** Os dados do aplicativo existem no banco de dados, no Global Document Storage (GDS) e AEM repositório e devem ser submetidos a backup em tempo real. GDS é um diretório usado para armazenar arquivos de longa duração usados em um processo. Esses arquivos podem incluir PDF, políticas ou modelos de formulário.

>[!NOTE]
>
>Se o Content Services (obsoleto) estiver instalado, faça backup também do diretório raiz do armazenamento de conteúdo. Consulte [Diretório raiz do armazenamento de conteúdo (somente Serviços de conteúdo)](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-directory-content-services-only).

O banco de dados é usado para armazenar artefatos de formulário, configurações de serviço, estado do processo e referências de banco de dados a arquivos GDS. Se você ativou o armazenamento de documentos no banco de dados, os dados persistentes e os documentos no GDS também são armazenados no banco de dados. O backup e a recuperação do banco de dados podem ser feitos com os seguintes métodos:

* **Backup de instantâneo** O modo indica que o sistema de formulários AEM está no modo de backup indefinidamente ou por um número especificado de minutos, após o qual o modo de backup não está mais ativado. Para entrar ou sair do modo de backup de snapshot, você pode usar uma das opções a seguir. Após um cenário de recuperação, o modo de backup de snapshot não deve ser ativado.

   * Use a página Configurações de Backup no Console de Administração. Para entrar no modo de instantâneo, marque a caixa de seleção Operar no modo de backup seguro . Desmarque a caixa de seleção para sair do modo de instantâneo.
   * Use o script LCBackupMode (consulte [Faça o backup dos diretórios do banco de dados, GDS e raiz do armazenamento de conteúdo](/help/forms/using/admin-help/backing-aem-forms-data.md#back-up-the-database-gds-aem-repository-and-content-storage-root-directories)). Para sair do modo de backup do snapshot, no argumento do script, defina a variável `continuousCoverage` para `false` ou usar o `leaveContinuousCoverage` opção.
   * Use a API de Backup/Recuperação fornecida. <!-- Fix broken link(see AEM forms API Reference section on AEM Forms Help and Tutorials page).-->

* **Backup em andamento** indica que o sistema está sempre em modo de backup, com uma nova sessão de modo de backup sendo iniciada assim que a sessão anterior é lançada. Nenhum tempo limite está associado ao modo de backup em andamento. Quando o script ou as APIs LCBackupMode são chamados para sair do modo de backup contínuo, uma nova sessão do modo de backup contínuo é iniciada. Esse modo é útil para oferecer suporte a backups contínuos, mas ainda permitindo que documentos antigos e desnecessários sejam excluídos do diretório GDS. O modo de backup contínuo não é suportado por meio da página Backup and Recovery. Após um cenário de recuperação, o modo de backup contínuo ainda é ativado. Você pode deixar o modo de backup contínuo (modo de backup contínuo) usando o script LCBackupMode com o `leaveContinuousCoverage` opção.

>[!NOTE]
>
>Deixar o modo de backup em andamento imediatamente faz com que uma nova sessão de modo de backup seja iniciada. Para desativar completamente o modo de backup em andamento, use o `leaveContinuousCoverage` no script, que substitui a sessão de backup em andamento existente. Quando estiver no modo de backup de snapshot, você poderá sair do modo de backup como costuma fazer.

Para evitar perda de dados, o backup dos dados específicos dos formulários de AEM deve ser feito de forma a garantir que os documentos do diretório raiz de armazenamento de conteúdo e GDS correlacionem-se com as referências do banco de dados.

>[!NOTE]
>
>Quando o GDS é armazenado no sistema de arquivos e não no banco de dados, execute o backup do banco de dados antes do backup GDS.

## Considerações especiais para backup e recuperação {#special-considerations-for-backup-and-recovery}

Use as seguintes diretrizes se precisar recuperar formulários AEM em um ambiente diferente devido às seguintes alterações:

* Alteração no endereço IP, nome do host ou porta do servidor de formulários AEM
* Alteração nas letras da unidade ou no caminho do diretório
* Alterar para outro host, porta ou nome de banco de dados

Normalmente, esses cenários de recuperação são causados por falha de hardware do servidor que hospeda o servidor de aplicativos, o servidor de banco de dados ou o servidor de formulários. Além das configurações específicas dos formulários AEM descritas nesta seção, você também deve fazer as alterações necessárias para outras partes da implantação dos formulários AEM, como balanceadores de carga e firewalls, se o nome do host ou endereço IP de um servidor de formulários AEM for alterado.

### O que não pode ser alterado {#what-cannot-be-changed}

Embora seja possível alterar o servidor de banco de dados e muitos outros parâmetros, não é possível alterar o tipo de servidor de aplicativos ou o tipo de banco de dados ao recuperar formulários AEM de um backup. Por exemplo, se estiver recuperando um backup de formulários AEM, não será possível alterar o servidor de aplicativos de JBoss para WebLogic ou banco de dados de Oracle para DB2. Além disso, os formulários de AEM recuperados devem usar os mesmos caminhos de sistema de arquivos, como o diretório de fontes.

### Reinício após uma recuperação {#restarting-after-a-recovery}

Antes de reiniciar o servidor de formulários após uma recuperação, faça o seguinte:

1. Inicie o sistema no modo de manutenção.
1. Faça o seguinte para garantir que o Gerenciador de Formulários seja sincronizado com formulários AEM no modo de manutenção:

   1. Vá para https://&lt;*server*>:&lt;*porta*>/lc/fm e faça logon usando credenciais de administrador/senha.
   1. Clique no nome do usuário (nesse caso, Super Administrador) no canto superior direito.
   1. Clique em **Opções de administração**.
   1. Clique em **Iniciar** para sincronizar ativos do repositório.

1. Em um ambiente em cluster, o nó principal (com relação a AEM) deve estar acima dos nós secundários.
1. Certifique-se de que nenhum processo seja iniciado a partir de fontes internas ou externas, como os iniciadores do processo Web, SOAP ou EJB, até que a operação normal do sistema seja validada.

Se o banco de dados dos principais formulários de AEM for movido ou alterado, revise os Guias de instalação relevantes para o servidor de aplicativos para obter informações sobre a atualização das informações de conexão do banco de dados das fontes de dados dos formulários de AEM IDP_DS e EDC_DS.

### Alteração do nome do host ou endereço IP dos formulários AEM {#changing-the-aem-forms-hostname-or-ip-address}

Em um cluster, se você usar o armazenamento em cache de TCP em vez de UDP, deverá atualizar a configuração do localizador de cache. Consulte &quot;Configuração dos localizadores de armazenamento em cache (somente TCP)&quot; no guia de configuração relevante para o servidor de aplicativos.

### Alteração dos caminhos do sistema do arquivo de arquivos do nó de formulários AEM {#changing-the-aem-forms-node-file-system-paths}

Se você alterar os caminhos do sistema de arquivos para um nó independente, deverá atualizar as referências apropriadas em preferências, outras configurações do sistema, aplicativos personalizados e aplicativos AEM formulários implantados. Por outro lado, para um cluster, todos os nós devem usar a mesma configuração de caminho do sistema de arquivos. Você deve definir o diretório raiz GDS (Global Document Storage, Armazenamento de Documento Global) e garantir que ele aponte para uma cópia do GDS recuperado, que está sincronizada com o banco de dados recuperado. A configuração do caminho GDS é importante porque o GDS pode conter dados destinados a persistir nas reinicializações do servidor de aplicativos.

Em um ambiente em cluster, a configuração do caminho do sistema de arquivos do repositório deve ser a mesma para todos os nós do cluster antes do backup e após a recuperação.

Use o `LCSetGDS`no `[*aem-forms root]*\sdk\misc\Foundation\SetGDSCommandline` para definir o caminho GDS depois de alterar os caminhos do sistema de arquivos. Consulte a `ReadMe.txt` na mesma pasta para obter detalhes. Se não for possível usar o caminho do diretório GDS antigo, `LCSetGDS` deve ser usado para definir o novo caminho para o GDS antes de iniciar AEM formulários.

>[!NOTE]
>
>Essa circunstância é a única sob a qual você deve usar esse script para alterar a localização do GDS. Para alterar o local do GDS enquanto AEM formulários estiver em execução, use o Console de administração. (Consulte [Definir configurações gerais do AEM forms](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)*.) *

Depois de definir o caminho GDS, inicie o servidor de formulários no modo de manutenção e use o console de administração para atualizar os caminhos restantes do sistema de arquivos para o novo nó. Depois de verificar se todas as configurações necessárias foram atualizadas, reinicie e teste AEM formulários.
