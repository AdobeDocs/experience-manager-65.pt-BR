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
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Manipuladores de logon único e tempo limite {#single-sign-on-and-timeout-handlers}

O espaço de trabalho do AEM Forms está habilitado para SSO. Se um usuário tiver feito logon em um aplicativo do AEM Forms, como o Forms Manager ou a interface do usuário PDF Generator, e acessar o AEM Forms workspace na mesma sessão do navegador, ele será conectado ao AEM Forms workspace e vice-versa.

## Lidar com o tempo limite do servidor no espaço de trabalho do AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

O tempo limite da sessão de um usuário pode ser configurado no Console de administração.

Para definir o tempo limite, faça logon no `https://'[server]:[port]'/adminui`, navegue até **Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema** e faça as configurações desejadas.

No AEM Forms, o tempo limite do espaço de trabalho é tratado como:

* A duração da sessão para um usuário está disponível em resposta a `initialize` chamada que inicializa a sessão do usuário.
* Uma caixa de diálogo pop-up notifica o usuário de que a sessão está prestes a expirar, 15 segundos antes da expiração da sessão.

Nesta caixa de diálogo pop-up:

* Clique em OK para encerrar a sessão do usuário.
* Clique em Cancelar para reinicializar a sessão do usuário.

>[!NOTE]
>
>Se nenhuma ação for tomada, o usuário será automaticamente desconectado do espaço de trabalho do AEM Forms três segundos antes da expiração da sessão.
