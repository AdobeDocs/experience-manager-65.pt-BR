---
title: Definir configurações de bloqueio de conta
description: Use a opção Habilitar Bloqueio de Conta para bloquear contas de usuário após um número especificado de falhas consecutivas de autenticação.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/setting_up_and_managing_domains
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: eb8c748d-51d9-4684-97c5-e982ad84ba9f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 5%
---
# Definir configurações de bloqueio de conta {#configure-account-locking-settings}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Ao adicionar um domínio, especifique se deseja ativar o bloqueio de conta. Quando a opção Habilitar bloqueio de conta está selecionada, as contas de usuário são bloqueadas após um número especificado de falhas consecutivas de autenticação. Após um período de tempo especificado, o usuário pode tentar autenticar novamente. Esse recurso impede que os usuários tentem várias combinações de credenciais para acessar o sistema.

Use as definições da página Gerenciamento de Domínio para especificar o número máximo de falhas de autenticação e o período de tempo em que as contas são bloqueadas. Essas configurações se aplicam a todos os domínios que têm o bloqueio de conta ativado.

1. No console de administração, clique em **[!UICONTROL Configurações > Gerenciamento de usuários > Gerenciamento de domínio]**.
1. Na caixa Máximo de falhas de autenticação consecutivas, digite o número de vezes consecutivas que um usuário pode tentar fazer logon sem sucesso antes que sua conta seja bloqueada. O valor padrão é 20.
1. Na caixa Desbloquear a conta após (minutos), digite o número de minutos em que a conta do usuário está bloqueada. Após o número especificado de minutos, o usuário pode tentar fazer logon novamente. O valor padrão é 30.
1. Clique em **[!UICONTROL Salvar]**.
