---
title: Manipuladores de logon único e tempo limite
seo-title: Single Sign On and timeout handlers
description: Como definir o valor de tempo limite da sessão para o espaço de trabalho do AEM Forms.
seo-description: How-to set the session timeout value for AEM Forms workspace.
uuid: 17583fd5-6453-41d3-bb63-a639983fbea9
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 698990a2-dd3f-480f-9d15-d87563860297
exl-id: 4f824d80-f3f8-4010-9583-5a9ab1151a7b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Manipuladores de logon único e tempo limite {#single-sign-on-and-timeout-handlers}

O espaço de trabalho do AEM Forms é habilitado para SSO. Se um usuário tiver feito logon em um aplicativo do AEM Forms, como a interface do usuário do Forms Manager ou PDF Generator, e acessar o espaço de trabalho do AEM Forms na mesma sessão do navegador, o usuário estará conectado ao espaço de trabalho do AEM Forms e vice-versa.

## Lidar com o tempo limite do servidor no espaço de trabalho do AEM Forms {#handling-server-timeout-in-nbsp-aem-forms-workspace}

O tempo limite da sessão de um usuário pode ser configurado no Console de administração.

Para definir o tempo limite, faça logon no `https://'[server]:[port]'/adminui`, navegue até **Configurações > Gerenciamento de usuários > Configuração > Configurar atributos avançados do sistema** e faça as configurações desejadas.

No espaço de trabalho do AEM Forms, o tempo limite é tratado como:

* A duração da sessão de um usuário está disponível em resposta a `initialize` chamada que inicializa a sessão do usuário.
* Uma caixa de diálogo pop-up notifica o usuário que a sessão está prestes a expirar, 15 segundos antes da expiração da sessão.

Nesta caixa de diálogo pop-up:

* Clique em OK para encerrar a sessão do usuário.
* Clique em Cancelar para reinicializar a sessão do usuário.

>[!NOTE]
>
>Se nenhuma ação for executada, o usuário será desconectado automaticamente do espaço de trabalho do AEM Forms três segundos antes da expiração da sessão.
