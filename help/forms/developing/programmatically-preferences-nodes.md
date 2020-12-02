---
title: Gerenciamento programático de PreferencesNodes
seo-title: Gerenciamento programático de PreferencesNodes
description: 'null'
seo-description: nulo
uuid: f0cb117a-a6cc-4ca5-8511-b3bc9f6738e9
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9d4dba7f-49d8-4112-bc8a-04dafc99a936
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---


# Gerenciamento programático dos nós de preferências {#programmatically-managing-the-preferencesnodes}

Este tópico descreve como você pode usar a API de serviço do Preferences Manager (Java) para gerenciar programaticamente os nós de preferências.

É possível alterar manualmente as configurações da interface do usuário do administrador. Para alterar as opções, navegue até `Home>Settings>User Management> Configuration>Manual Configuration`. Importe `config.xml` depois de fazer as alterações, você notaria que todas as alterações, exceto as feitas no nó `/Adobe/Adobe Experience Manager Forms/Config/UM persist`, foram perdidas. A pré-visualização de Importação e exportação do Gerenciamento de Usuário não suporta a alteração das configurações de outros componentes. Agora, essas alterações podem ser feitas usando `PreferencesManagerServiceClient` APIs.

**Resumo das** etapasPara gerenciar programaticamente os nós de preferências, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente PreferencesManagerService
1. Chamar as operações de permissão ou função apropriadas

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando um aplicativo cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PreferencesManagerService**

Antes de executar programaticamente uma operação PreferencesManagerService do Gerenciamento de Usuário, você deve criar um cliente PreferencesManagerService. Com a API Java, isso é feito criando um objeto PreferencesManagerServiceClient.

**Chamar as operações de permissão ou função apropriadas**

Depois de criar o cliente de serviço, você pode chamar as operações do Gerenciador de preferências. O cliente de serviço permite que você leia e defina permissões.
