---
title: Definir configurações de bloqueio de conta
seo-title: Definir configurações de bloqueio de conta
description: Use a opção Habilitar bloqueio de conta para bloquear contas de usuário após um número especificado de falhas consecutivas de autenticação.
seo-description: Use a opção Habilitar bloqueio de conta para bloquear contas de usuário após um número especificado de falhas consecutivas de autenticação.
uuid: 5ff3fb76-8b11-4818-9a75-40ed8e121da5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d4409c6b-f4ef-499c-8daa-e93a163ff8ab
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 4%

---


# Definir configurações de bloqueio de conta {#configure-account-locking-settings}

Ao adicionar um domínio, especifique se deseja ativar o bloqueio de conta. Quando a opção Ativar bloqueio de conta é selecionada, as contas de usuário são bloqueadas após um número especificado de falhas de autenticação consecutivas. Após um período especificado, o usuário pode tentar autenticar novamente. Esse recurso impede que os usuários tentem várias combinações de credenciais para acessar o sistema.

Use as configurações na página Gerenciamento de domínio para especificar o número máximo de falhas de autenticação e o tempo em que as contas são bloqueadas. Essas configurações se aplicam a todos os domínios que têm bloqueio de conta ativado.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuário > Gerenciamento de domínio]**.
1. Na caixa Máximo de Falhas de Autenticação Consecutiva, digite o número de vezes consecutivas que um usuário pode tentar fazer logon sem êxito antes que sua conta seja bloqueada. O valor padrão é 20.
1. Na caixa Desbloquear a conta depois (minutos), digite o número de minutos em que a conta do usuário está bloqueada. Após o número especificado de minutos, o usuário pode tentar fazer logon novamente. O valor padrão é 30.
1. Clique em **[!UICONTROL Salvar]**.

