---
title: Configurar atributos avançados do sistema
description: Use a página Configurar Atributos Avançados do Sistema para modificar determinadas configurações no arquivo de configuração sem a necessidade de exportar, editar e importar o arquivo.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 809af2c0-6f5c-4dd4-af48-dbf476c9ea45
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Configurar atributos avançados do sistema {#configure-advanced-system-attributes}

Use a página Configurar Atributos Avançados do Sistema para modificar determinadas configurações no arquivo de configuração sem a necessidade de exportar, editar e importar o arquivo. (Consulte [Importação e exportação do arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema]**.
1. (Opcional) Altere qualquer um dos seguintes atributos de sessão:

   **Limite de tempo limite da sessão (minutos):** O tempo, em minutos, antes que um usuário seja automaticamente desconectado do sistema. Por padrão, os componentes de formulários AEM, como o Workbench, expiram após duas horas, independentemente da atividade ou inatividade, e o usuário deve fazer logon novamente. Os valores válidos são `1` para `1440`. O valor padrão é `120` (2 horas). Esta configuração atualiza o `SAML/Producer/assertionValidityInMinutes` chave no arquivo de configuração.

   >[!NOTE]
   >
   >Você não deve definir o Limite de tempo de sessão abaixo de 10 minutos, pois o sistema pode não se comportar corretamente. O valor recomendado é de 10 a 120 (minutos).

   **Limite de asserção (segundos):** Um tempo de buffer para compensar atrasos devido a diferenças de tempo do sistema entre os servidores de aplicativos AEM Forms em um cluster. Os formulários AEM atualizam o tempo de logon de um usuário pela quantidade de tempo (em segundos) especificada nessa propriedade. Os valores válidos são `0` para `3600`. O valor padrão é `60`. Esta configuração atualiza o `SAML/Producer/assertionThresholdInSeconds` chave no arquivo de configuração.

   **Máximo de Renovações Permitidas de uma Asserção:** O número máximo de vezes que a sessão de um usuário pode ser renovada de forma transparente sem a necessidade de um logon. Os valores válidos são `0` para `9999`. Um valor de `0` significa que as afirmações não são renovadas. O valor padrão é 10. Esta configuração atualiza o `SAML/Producer/maxAssertionRenewalCount` chave no arquivo de configuração.

1. (Opcional) Altere qualquer um dos seguintes atributos de sincronização de diretórios:

   **Log de Estatísticas de Sincronização:** Especifica se o Gerenciamento de Usuários registra estatísticas detalhadas durante o processo de sincronização. (Consulte [Habilitar ou desabilitar o log detalhado durante a sincronização](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Expressão Cron da Unidade de Acabamento de Sincronização:** O intervalo em que o Gerenciamento de Usuários tenta novamente sincronizações com falha. (Consulte [Configurar a opção de nova tentativa de sincronização de diretório](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Tempo Limite de Bloqueio do Trabalho de Cluster em Minutos:** Usado em ambientes clusterizados. Se a sincronização em um nó falhar e o bloqueio do cluster não for liberado, esse valor especificará o número de minutos que outro nó aguarda antes de forçar a aquisição do bloqueio. O valor padrão é `15` minutos. Os valores válidos são `1` para `1440` minutos.

1. (Opcional) Altere os seguintes atributos e clique em **[!UICONTROL OK]**:

   **Auditoria de Eventos do Gerenciador de Usuários:** Selecione esta opção para habilitar a auditoria de eventos de sincronização de diretórios e de eventos de autenticação, como êxito, falha e bloqueio. Por padrão, essa opção não é selecionada a menos que você instale um componente que exija auditoria, como o Rights Management. Esta configuração atualiza o `APSAuditService` chave no arquivo de configuração.

   **Criação Automática de Grupo Dinâmico:** Habilita a criação automática de grupos dinâmicos com base em domínios de email. (Consulte [Criar um grupo dinâmico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

Você também pode reverter para as configurações originais do Gerenciamento de usuários clicando em Recarregar.
