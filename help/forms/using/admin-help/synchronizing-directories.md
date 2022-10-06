---
title: Sincronização de diretórios
seo-title: Synchronizing directories
description: Saiba como sincronizar o banco de dados de Gerenciamento de usuários com alterações nos servidores de diretório de origem usando sincronização manual ou agendada.
seo-description: Learn how to synchronize the User Management database with changes to the source directory servers using manual or scheduled synchronization.
uuid: 71cbc04d-6172-49b7-a490-ff3233c1b2bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7ec0698a-9e6e-48d4-bba2-5a6eee313900
exl-id: cb642289-4137-4ba7-8bde-0e458c8c94fe
source-git-commit: 2a2f8538b6554540b546f4d345c0b3c0d3e706f3
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 0%

---

# Sincronização de diretórios {#synchronizing-directories}

Para sincronizar domínios, você pode optar por fazer uma sincronização manual ou agendada. A *sincronização manual* sincroniza qualquer domínio selecionado. A *sincronização agendada* sincroniza todos os domínios.

A sincronização de diretórios é usada para extrair detalhes dos servidores de diretórios especificados nas configurações de diretório para o banco de dados de Gerenciamento de Usuários. Posteriormente, você também poderá fazer uma sincronização manual se ocorrerem alterações ou atualizações nos servidores de diretório. Por exemplo, você pode fazer uma sincronização manual se usuários e grupos forem adicionados ou se alterações forem feitas na conta de um usuário.

Você também pode definir um agendamento diário de sincronização para sincronizar automaticamente o banco de dados de Gerenciamento de usuários com alterações ou atualizações nos servidores de diretório de origem. No entanto, esteja ciente de que esse processo usa recursos de rede e servidor. Escolha períodos de tempo de baixo uso e evite agendar sincronizações desnecessárias que vinculem os recursos do sistema e da rede. Para minimizar sincronizações desnecessárias, use a opção de sincronização imediata.

Você também pode especificar se deseja enviar informações do usuário e do grupo para o Adobe LiveCycle Content Services 9 (obsoleto) ao sincronizar domínios.

>[!NOTE]
>
>Não crie vários usuários e grupos locais enquanto uma sincronização de diretório LDAP estiver em andamento. Tentar esse processo pode resultar em erros.

>[!NOTE]
>
>Se o processo de sincronização de domínio for interrompido (por exemplo, o servidor de aplicativos é desligado durante o processo), aguarde enquanto você tenta sincronizar o domínio. Para avaliar o status da sincronização, verifique o estado . Se o Gerenciamento de usuários tiver adquirido um bloqueio antes do encerramento, aguarde 10 minutos para que o bloqueio seja liberado após a reinicialização do servidor. Se o status de sincronização for &quot;Em Andamento&quot;, mas a sincronização for interrompida ou paralisada, o Gerenciamento de usuários tentará novamente a sincronização após 3 minutos. Depois de três tentativas malsucedidas, o Gerenciamento de usuários declara a sincronização uma falha e libera o bloqueio.

>[!NOTE]
>
>O Adobe® LiveCycle® Content Services ES (obsoleto) é um sistema de gerenciamento de conteúdo instalado com o LiveCycle. Ele permite que os usuários criem, gerenciem, monitorem e otimizem processos centrados em seres humanos. O suporte aos Serviços de conteúdo (obsoleto) termina em 31/12/2014. Consulte [Documento de ciclo de vida do produto Adobe](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html).

## Ativar a sincronização do diretório delta {#enable-delta-directory-synchronization}

A sincronização de diretório delta melhora a eficiência da sincronização de diretórios. Quando a sincronização de diretório delta está ativada, o Gerenciamento de usuários sincroniza somente usuários e grupos que foram adicionados ou atualizados desde a última sincronização.

O Gerenciamento de usuários executa as seguintes etapas quando a sincronização de diretório delta está habilitada:

* Busque todos os usuários dos servidores de diretório, mas atualize o banco de dados de Gerenciamento de usuários somente com os usuários cujo carimbo de data e hora foi alterado.
* Busque todos os grupos, mas atualize o banco de dados de Gerenciamento de usuários somente com os grupos cujo carimbo de data e hora foi alterado.
* Busque membros do grupo somente para os grupos cujos carimbos de data e hora foram alterados e atualize o banco de dados de Gerenciamento de usuários com essas informações.

>[!NOTE]
>
>Os usuários e grupos que foram removidos do diretório não são excluídos do banco de dados de Gerenciamento de usuários até que você execute uma sincronização completa do diretório.

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Em Sincronização delta, marque a caixa de seleção e clique em Salvar.
1. Edite as configurações de diretório para cada um dos domínios corporativos que usarão o recurso de sincronização de diretório delta. Nas páginas Configurações do usuário e Configurações do grupo , localize a configuração Modificar carimbo de data e hora e insira `modify TimeStamp` como o valor. Para obter detalhes sobre como editar domínios corporativos, consulte [Edição e conversão de domínios existentes](/help/forms/using/admin-help/editing-converting-existing-domains.md#editing-and-converting-existing-domains).

## Ativar ou desativar o registro detalhado durante a sincronização {#enable-or-disable-detailed-logging-during-synchronization}

Por padrão, o Gerenciamento de usuários registra estatísticas detalhadas durante o processo de sincronização.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Sincronizar registro de estatísticas, desmarque a caixa de seleção para desativar o registro detalhado ou selecione-o para ativar o registro e, em seguida, clique em Salvar.

## Configurar a opção de nova tentativa de sincronização de diretório {#configure-the-directory-synchronization-retry-option}

Você pode configurar o Gerenciamento de usuários para verificar periodicamente se há tentativas de sincronização de diretórios com falha. O Gerenciamento de usuários tenta concluir as sincronizações que falharam.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema.
1. Em Synch Finisher Cron Expression, digite uma expressão cron que represente o intervalo em que as tentativas do Gerenciamento de usuários falharam nas sincronizações. O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

   O padrão é 0/13 &amp;ast; ? &amp;ast; , o que significa que a verificação ocorre a cada 13 minutos.

## Sincronizar diretórios manualmente {#manually-synchronize-directories}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. (Opcional) Para inserir informações do usuário e do grupo nos Serviços de conteúdo (obsoleto), selecione a opção Selecionar essa opção para enviar usuários e grupos para os principais provedores de armazenamento externos registrados . Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos .
1. Marque a caixa de seleção de cada domínio empresarial a ser sincronizado e clique em Sincronizar agora.

   Se você selecionar vários domínios, a sincronização de domínio para todos poderá ser executada ao mesmo tempo. No entanto, se você selecionar os domínios separadamente, somente uma sincronização de domínio pode ser executada por vez.

## Agendar sincronização de diretórios {#schedule-directory-synchronization}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Agendar sincronização:

   * Para ativar a sincronização automática diariamente, em Scheduler, selecione Ocorrências. Selecione Diariamente na lista e digite a hora no formato de 24 horas na caixa correspondente. Quando você salva suas configurações, esse valor é convertido em uma expressão cron, exibida na caixa Expressão do Cron.
   * Para agendar a sincronização em um dia específico da semana ou mês, ou em um mês específico, selecione Expressão de trabalho e digite a expressão apropriada na caixa. Por exemplo, sincronize às 1:30 da manhã na última sexta-feira do mês.

O uso da expressão cron é baseado no sistema de programação de trabalhos de código aberto do Quartz, versão 1.4.0.

* Para desativar a sincronização automática, selecione Ocorre e selecione Nunca na lista.
* (Opcional) Para inserir informações do usuário e do grupo nos Serviços de conteúdo (obsoleto), selecione a opção Selecionar essa opção para enviar usuários e grupos para os principais provedores de armazenamento externos registrados . Essa opção também se aplica ao adicionar novos usuários e grupos por meio da página Usuários e grupos .
* Clique em Salvar.

## Parar todas as sincronizações de diretório em curso {#stop-all-directory-synchronizations-currently-in-progress}

1. No console de administração, clique em Configurações > Gerenciamento de usuário > Gerenciamento de domínio.
1. Clique em Abortar. Este botão é exibido somente enquanto uma sincronização de diretório está em andamento.
