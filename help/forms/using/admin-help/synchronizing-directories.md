---
title: Sincronizando diretórios
seo-title: Sincronizando diretórios
description: Saiba como sincronizar o banco de dados Gerenciamento de usuários com as alterações nos servidores de diretório de origem usando sincronização manual ou programada.
seo-description: Saiba como sincronizar o banco de dados Gerenciamento de usuários com as alterações nos servidores de diretório de origem usando sincronização manual ou programada.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Sincronizando diretórios {#synchronizing-directories}

Para sincronizar domínios, você pode optar por fazer uma sincronização manual ou programada. Uma *sincronização manual* sincroniza todos os domínios selecionados. Uma *sincronização programada* sincroniza todos os domínios.

A sincronização de diretório é usada para extrair detalhes dos servidores de diretório especificados nas configurações de diretório para o banco de dados de Gerenciamento de usuário. Posteriormente, você também poderá fazer uma sincronização manual se ocorrerem alterações ou atualizações nos servidores de diretório. Por exemplo, você pode fazer uma sincronização manual se usuários e grupos forem adicionados ou se forem feitas alterações na conta de um usuário.

Você também pode definir um agendamento de sincronização diária para sincronizar automaticamente o banco de dados de Gerenciamento de usuários com alterações ou atualizações nos servidores de diretório de origem. No entanto, esteja ciente de que esse processo usa recursos de rede e servidor. Escolha períodos de tempo de baixa utilização e evite programar sincronizações desnecessárias que vinculem os recursos do sistema e da rede. Para minimizar sincronizações desnecessárias, use a opção de sincronização imediata.

Você também pode especificar se deseja enviar informações de usuário e grupo para o Adobe LiveCycle Content Services 9 (obsoleto) ao sincronizar domínios.

>[!NOTE]
>
>Não crie vários usuários e grupos locais enquanto uma sincronização de diretório LDAP estiver em andamento. Tentar esse processo pode resultar em erros.

>[!NOTE]
>
>Se o processo de sincronização do domínio for interrompido (por exemplo, o servidor de aplicativos será desligado durante o processo), aguarde um pouco antes de tentar sincronizar o domínio. Para avaliar o status da sincronização, verifique o estado. Se o Gerenciamento de usuários tiver adquirido um bloqueio antes do encerramento, aguarde 10 minutos para o bloqueio ser liberado após a reinicialização do servidor. Se o status da sincronização for &quot;Em andamento&quot;, mas a sincronização for interrompida ou parada, o Gerenciamento de usuários tentativas a sincronização após 3 minutos. Após três tentativas malsucedidas, o Gerenciamento de usuários declara a sincronização uma falha e libera o bloqueio.

>[!NOTE]
>
>O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gestão de conteúdo instalado com o LiveCycle. Ela permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto do Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html). Para saber mais sobre como configurar o Content Services (obsoleto), consulte [Administração do Content Services](https://help.adobe.com/en_US/livecycle/9.0/admin_contentservices.pdf).

## Ativar sincronização de diretório delta {#enable-delta-directory-synchronization}

A sincronização do diretório delta melhora a eficiência da sincronização do diretório. Quando a sincronização de diretório delta está ativada, o Gerenciamento de usuários sincroniza somente os usuários e grupos que foram adicionados ou atualizados desde a última sincronização.

O Gerenciamento de usuários executa as seguintes etapas quando a sincronização do diretório delta está ativada:

* Busque todos os usuários dos servidores de diretório, mas atualize o banco de dados Gerenciamento de usuários somente com os usuários cujo carimbo de data e hora foi alterado.
* Busque todos os grupos, mas atualize o banco de dados Gerenciamento de usuários somente com os grupos cujo carimbo de data e hora foi alterado.
* Busque membros do grupo somente para os grupos cujos carimbos de data e hora foram alterados e atualize o banco de dados de Gerenciamento de usuários com essas informações.

>[!NOTE]
>
>Os usuários e grupos que foram removidos do diretório não são excluídos do banco de dados Gerenciamento de usuários até que você execute uma sincronização completa do diretório.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Em Sincronização delta, marque a caixa de seleção e clique em Salvar.
1. Edite as configurações de diretório para cada um dos domínios corporativos que usarão o recurso de sincronização de diretório delta. Nas páginas Configurações do usuário e Configurações do grupo, localize a configuração Modificar carimbo de data e hora e digite `modify TimeStamp` como o valor. Para obter detalhes sobre como editar domínios corporativos, consulte [Editar e converter domínios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Ativar ou desativar o registro detalhado durante a sincronização {#enable-or-disable-detailed-logging-during-synchronization}

Por padrão, o Gerenciamento de usuários registra estatísticas detalhadas durante o processo de sincronização.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Configurar atributos avançados do sistema.
1. Em Sincronizar registro de estatísticas, desmarque a caixa de seleção para desativar o registro detalhado ou selecione-o para ativar o registro e clique em Salvar.

## Configure a opção de repetição de sincronização de diretório {#configure-the-directory-synchronization-retry-option}

Você pode configurar o Gerenciamento de usuários para verificar periodicamente se há tentativas de sincronização de diretórios que falharam. O Gerenciamento de usuários tenta concluir as sincronizações que falharam.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Configurar atributos avançados do sistema.
1. Em Sincronizar Expressão Cron do Finalizador, digite uma expressão cron que representa o intervalo no qual as tentativas de Gerenciamento de Usuário falharam nas sincronizações. O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

   O padrão é 0/13 &amp;ast; ? &amp;ast; , o que significa que a verificação ocorre a cada 13 minutos.

## Sincronizar manualmente diretórios {#manually-synchronize-directories}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. (Opcional) Para enviar informações de usuário e grupo para o Content Services (obsoleto), selecione a opção Selecionar essa opção para encaminhar usuários e grupos para os principais provedores de Armazenamentos externos registrados. Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos.
1. Marque a caixa de seleção de cada domínio corporativo a ser sincronizado e clique em Sincronizar agora.

   Se você selecionar vários domínios, a sincronização do domínio para todos os domínios poderá ser executada ao mesmo tempo. No entanto, se você selecionar os domínios separadamente, somente uma sincronização de domínio poderá ser executada por vez.

## Agendar sincronização de diretório {#schedule-directory-synchronization}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Agendar sincronização:

   * Para habilitar a sincronização automática diariamente, em Scheduler, selecione Ocorre. Selecione Diariamente na lista e digite a hora no formato de 24 horas na caixa correspondente. Quando você salva suas configurações, esse valor é convertido em uma expressão cron, exibida na caixa Expressão Cron.
   * Para programar a sincronização em um dia específico da semana ou mês, ou em um mês específico, selecione Expressão Cron e digite a expressão apropriada na caixa. Por exemplo, sincronize às 1:30 da manhã. na última sexta-feira do mês.

O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

* Para desativar a sincronização automática, selecione Ocorre e selecione Nunca na lista.
* (Opcional) Para enviar informações de usuário e grupo para o Content Services (obsoleto), selecione a opção Selecionar essa opção para encaminhar usuários e grupos para os principais provedores de Armazenamentos externos registrados. Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos.
* Clique em Salvar.

## Parar todas as sincronizações de diretório em andamento {#stop-all-directory-synchronizations-currently-in-progress}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Abortar. Este botão é exibido somente enquanto uma sincronização de diretório está em andamento.

