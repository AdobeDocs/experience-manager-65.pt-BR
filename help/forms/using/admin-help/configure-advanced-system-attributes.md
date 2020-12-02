---
title: Configurar atributos avançados do sistema
seo-title: Configurar atributos avançados do sistema
description: Use a página Configurar atributos avançados do sistema para modificar determinadas configurações no arquivo de configuração sem a necessidade de exportar, editar e importar o arquivo.
seo-description: Use a página Configurar atributos avançados do sistema para modificar determinadas configurações no arquivo de configuração sem a necessidade de exportar, editar e importar o arquivo.
uuid: 6bcfbaa9-f492-46aa-97d2-00fc3e67d0d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 533ad3f7-3905-420d-8bb9-8ae8f14fb28e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 1%

---


# Configurar atributos avançados do sistema {#configure-advanced-system-attributes}

Use a página Configurar atributos avançados do sistema para modificar determinadas configurações no arquivo de configuração sem a necessidade de exportar, editar e importar o arquivo. (Consulte [Importando e exportando o arquivo de configuração](/help/forms/using/admin-help/importing-exporting-configuration-file.md#importing-and-exporting-the-configuration-file).)

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema]**.
1. (Opcional) Altere qualquer um dos seguintes atributos de sessão:

   **Limite de tempo limite da sessão (Minutos):** A quantidade de tempo, em minutos, antes que um usuário seja automaticamente desconectado do sistema. Por padrão, AEM componentes de formulários como o Workbench expiram após duas horas, independentemente da atividade ou da inatividade, e o usuário deve fazer logon novamente. Os valores válidos são `1` para `1440`. O valor padrão é `120` (2 horas). Essa configuração atualiza a chave de entrada `SAML/Producer/assertionValidityInMinutes` no arquivo de configuração.

   >[!NOTE]
   >
   >Você não deve definir o Limite de tempo limite da sessão abaixo de 10 minutos, pois o sistema pode não se comportar corretamente. O valor recomendado é de 10 a 120 (minutos).

   **Limite de asserção (segundos):** um tempo de buffer para compensar atrasos devido às diferenças de tempo do sistema entre AEM servidor de aplicativos de formulários em um cluster. AEM formulários atualiza o tempo de logon de um usuário pela quantidade de tempo (em segundos) especificada nesta propriedade. Os valores válidos são `0` para `3600`. O valor padrão é `60`. Essa configuração atualiza a chave de entrada `SAML/Producer/assertionThresholdInSeconds` no arquivo de configuração.

   **Renovações máximas permitidas de uma asserção:** O número máximo de vezes que uma sessão de usuário pode ser renovada de forma transparente sem precisar de um logon. Os valores válidos são `0` para `9999`. Um valor de `0` significa que as asserções não são renovadas. O valor padrão é 10. Essa configuração atualiza a chave de entrada `SAML/Producer/maxAssertionRenewalCount` no arquivo de configuração.

1. (Opcional) Altere qualquer um dos seguintes atributos de sincronização de diretório:

   **Registro de estatísticas de sincronização:** especifica se o Gerenciamento de usuários registra estatísticas detalhadas durante o processo de sincronização. (Consulte [Habilitar ou desabilitar o registro detalhado durante a sincronização](/help/forms/using/admin-help/synchronizing-directories.md#enable-or-disable-detailed-logging-during-synchronization).)

   **Expressão Cron do Finalizador de Sincronização:** O intervalo no qual as tentativas de Gerenciamento de Usuários falharam nas sincronizações. (Consulte [Configure a opção de repetição de sincronização de diretório](/help/forms/using/admin-help/synchronizing-directories.md#configure-the-directory-synchronization-retry-option).)

   **Tempo limite de bloqueio de trabalho do cluster em minutos:** usado em ambientes agrupados. Se a sincronização em um nó falhar e o bloqueio de cluster não for liberado, esse valor especificará o número de minutos que outro nó espera antes de adquirir o bloqueio à força. O valor padrão é `15` minutos. Os valores válidos são `1` a `1440` minutos.

1. (Opcional) Altere os seguintes atributos e clique em **[!UICONTROL OK]**:

   **Auditoria de Evento do Gerenciador de Usuários:** Selecione esta opção para ativar a auditoria de eventos de sincronização de diretórios e de eventos de autenticação, como sucesso, falha e bloqueio. Por padrão, essa opção não é selecionada a menos que você instale um componente que requer auditoria, como o Rights Management. Essa configuração atualiza a chave de entrada `APSAuditService` no arquivo de configuração.

   **Criação automática do grupo dinâmico:** permite a criação automática de grupos dinâmicos com base em domínios de email. (Consulte [Criar um grupo dinâmico](/help/forms/using/admin-help/creating-configuring-groups.md#create-a-dynamic-group).)

Você também pode reverter para as configurações originais de Gerenciamento de usuários clicando em Recarregar.
