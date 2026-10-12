---
title: Manipuladores de logon único e tempo limite
description: Como definir o valor do tempo limite da sessão para o espaço de trabalho do AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
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
source-wordcount: '192'
ht-degree: 0%
---
# Manipuladores de logon único e tempo limite {#single-sign-on-and-timeout-handlers}

O espaço de trabalho do AEM Forms está habilitado para SSO. Se um usuário tiver feito logon em um aplicativo do AEM Forms, como o Forms Manager ou a interface do usuário do PDF Generator, e acessar o AEM Forms workspace na mesma sessão do navegador, ele será conectado ao AEM Forms workspace e vice-versa.

## Lidar com o tempo limite do servidor no espaço de trabalho do AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

O tempo limite da sessão de um usuário pode ser configurado no Console de administração.

Para definir o tempo limite, faça logon em `https://'[server]:[port]'/adminui`, navegue até **Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema** e faça as configurações desejadas.

No AEM Forms, o tempo limite do espaço de trabalho é tratado como:

* A duração da sessão de um usuário está disponível em resposta à chamada `initialize` que inicializa a sessão do usuário.
* Uma caixa de diálogo pop-up notifica o usuário de que a sessão está prestes a expirar, 15 segundos antes da expiração da sessão.

Nesta caixa de diálogo pop-up:

* Clique em OK para encerrar a sessão do usuário.
* Clique em Cancelar para reinicializar a sessão do usuário.

>[!NOTE]
>
>Se nenhuma ação for tomada, o usuário será automaticamente desconectado do espaço de trabalho do AEM Forms três segundos antes da expiração da sessão.
