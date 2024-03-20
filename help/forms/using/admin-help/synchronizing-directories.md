---
title: Sincronização de diretórios
description: Saiba como sincronizar o banco de dados de Gerenciamento de usuários com alterações nos servidores de diretório de origem usando a sincronização manual ou agendada.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# Sincronização de diretórios {#synchronizing-directories}

Para sincronizar domínios, você pode optar por fazer uma sincronização manual ou programada. A *sincronização manual* sincroniza todos os domínios selecionados. A *sincronização agendada* sincroniza todos os domínios.

A sincronização de diretórios é usada para extrair detalhes dos servidores de diretórios especificados nas configurações de diretório para o banco de dados de Gerenciamento de Usuários. Posteriormente, você também poderá fazer uma sincronização manual se ocorrerem alterações ou atualizações nos servidores de diretório. Por exemplo, você pode fazer uma sincronização manual se usuários e grupos forem adicionados ou se forem feitas alterações na conta de um usuário.

Você também pode definir uma programação de sincronização diária para sincronizar automaticamente o banco de dados do User Management com alterações ou atualizações nos servidores de diretório de origem. No entanto, esse processo usa recursos de rede e de servidor. Escolha períodos de pouco uso e evite a programação de sincronizações desnecessárias que imobilizam os recursos do sistema e da rede. Para minimizar sincronizações desnecessárias, use a opção de sincronização imediata.

Você também pode especificar se deseja enviar informações de usuário e grupo para o Adobe LiveCycle Content Services 9 (obsoleto) ao sincronizar domínios.

>[!NOTE]
>
>Não crie vários usuários e grupos locais enquanto uma sincronização de diretório LDAP estiver em andamento. A tentativa desse processo pode resultar em erros.

>[!NOTE]
>
>Se o processo de sincronização de domínio for interrompido (por exemplo, o servidor de aplicativos é desligado durante o processo), aguarde um pouco antes de tentar sincronizar o domínio. Para avaliar o status da sincronização, verifique o estado. Se o Gerenciamento de Usuários adquiriu um bloqueio antes do desligamento, aguarde 10 minutos para que o bloqueio seja liberado após a reinicialização do servidor. Se o status da sincronização for &quot;Em Andamento&quot;, mas a sincronização for interrompida ou interrompida, o Gerenciamento de Usuários tentará novamente a sincronização após 3 minutos. Após três tentativas sem êxito, o Gerenciamento de usuários declara a sincronização como uma falha e libera o bloqueio.

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES (Obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários projetem, gerenciem, monitorem e otimizem processos centrados no ser humano. O suporte aos Content Services (obsoleto) termina em 31/12/2014. Consulte [documento do ciclo de vida do produto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Habilitar a sincronização do diretório delta {#enable-delta-directory-synchronization}

A sincronização de diretórios delta melhora a eficiência da sincronização de diretórios. Quando a sincronização do diretório delta está habilitada, o Gerenciamento de Usuários sincroniza apenas os usuários e grupos que foram adicionados ou atualizados desde a última sincronização.

O Gerenciamento de Usuários executa as seguintes etapas quando a sincronização do diretório delta está habilitada:

* Busca todos os usuários nos servidores de diretórios, mas atualiza o banco de dados de Gerenciamento de Usuários somente com os usuários cujo timestamp tenha sido alterado.
* Buscar todos os grupos, mas atualizar o banco de dados de Gerenciamento de usuários somente com os grupos cujo carimbo de data/hora tenha sido alterado.
* Procure membros do grupo somente para os grupos cujos carimbos de data e hora foram alterados e atualize o banco de dados de Gerenciamento de Usuários com essas informações.

>[!NOTE]
>
>Os usuários e grupos que foram removidos do diretório não são excluídos do banco de dados de Gerenciamento de Usuários até que você execute uma sincronização completa do diretório.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Em Sincronização delta, marque a caixa de seleção e clique em Salvar.
1. Edite as definições de diretório para cada um dos domínios enterprise que usarão o recurso de sincronização de diretório delta. Nas páginas Configurações do usuário e Configurações do grupo, localize a configuração Modificar carimbo de data e hora e digite `modify TimeStamp` como o valor. Para obter detalhes sobre a edição de domínios enterprise, consulte [Edição e conversão de domínios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Habilitar ou desabilitar o log detalhado durante a sincronização {#enable-or-disable-detailed-logging-during-synchronization}

Por padrão, o Gerenciamento de usuários registra estatísticas detalhadas durante o processo de sincronização.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Registro de Estatísticas de Sincronização, desmarque a caixa de seleção para desativar o registro detalhado ou selecione-o para ativar o registro e, em seguida, clique em Salvar.

## Configurar a opção de nova tentativa de sincronização de diretório {#configure-the-directory-synchronization-retry-option}

Você pode configurar o Gerenciamento de Usuários para verificar periodicamente se há falhas nas tentativas de sincronização de diretórios. O Gerenciamento de usuários tenta, então, concluir as sincronizações com falha.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Sincronizar Expressão Cron do Terminador de Sincronização, insira uma expressão cron que represente o intervalo em que o Gerenciamento de Usuários tenta novamente sincronizações com falha. O uso da expressão cron é baseado no sistema de agendamento de tarefas de código aberto Quartz, versão 1.4.0.

   O padrão é 0 0/13 &amp;ast; ? &amp;ast; , que significa que a verificação ocorre a cada 13 minutos.

## Sincronizar diretórios manualmente {#manually-synchronize-directories}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. (Opcional) Para enviar informações de usuários e grupos para o Content Services (Obsoleto), selecione a opção Selecionar esta opção para enviar usuários e grupos para provedores de armazenamento principal externos registrados. Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos.
1. Marque a caixa de seleção de cada domínio enterprise a ser sincronizado e clique em Sincronizar Agora.

   Se você selecionar vários domínios, a sincronização de todos os domínios poderá ser executada ao mesmo tempo. No entanto, se você selecionar os domínios separadamente, somente uma sincronização de domínio poderá ser executada de cada vez.

## Agendar sincronização de diretórios {#schedule-directory-synchronization}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Agendar sincronização:

   * Para ativar a sincronização automática diariamente, em Scheduler, selecione Ocorre. Selecione Diariamente na lista e digite a hora no formato de 24 horas na caixa correspondente. Quando você salva suas configurações, esse valor é convertido em uma expressão CRON, que é exibida na caixa Expressão CRON.
   * Para agendar a sincronização em um dia da semana ou mês específico ou em um mês específico, selecione Expressão Cron e digite a expressão apropriada na caixa. Por exemplo, sincronize à 1h30 da última sexta-feira do mês.

O uso da expressão cron é baseado no sistema de agendamento de tarefas de código aberto Quartz, versão 1.4.0.

* Para desativar a sincronização automática, selecione Ocorre e selecione Nunca na lista.
* (Opcional) Para enviar informações de usuários e grupos para o Content Services (Obsoleto), selecione a opção Selecionar esta opção para enviar usuários e grupos para provedores de armazenamento principal externos registrados. Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos.
* Clique em Salvar.

## Interromper todas as sincronizações de diretório em andamento {#stop-all-directory-synchronizations-currently-in-progress}

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Gerenciamento de domínio.
1. Clique em Abort. Este botão é exibido somente enquanto uma sincronização de diretório está em andamento.
