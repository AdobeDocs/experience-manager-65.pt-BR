---
title: Gerenciando programaticamente os PreferencesNodes
description: Use a API de serviço do Gerenciador de preferências (Java) para gerenciar programaticamente os nós de preferências.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 108eb249-879b-4e4f-b431-8118b8656e62
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Gerenciando programaticamente os nós de preferências {#programmatically-managing-the-preferencesnodes}

**Os exemplos e amostras neste documento são somente para AEM Forms no ambiente JEE.**

Este tópico descreve como você pode usar a API de serviço do Gerenciador de preferências (Java) para gerenciar programaticamente os nós de preferências.

Você pode alterar manualmente as definições de configuração na interface do Administrador. Para alterar as opções, navegue até `Home>Settings>User Management> Configuration>Manual Configuration`. Importar `config.xml` depois de fazer as alterações, você notará que todas as alterações, exceto as alterações feitas no nó `/Adobe/Adobe Experience Manager Forms/Config/UM persist` são perdidos. A visualização da Importação e exportação do Gerenciamento de usuários não oferece suporte à alteração das definições de configuração de outros componentes. Agora, essas alterações podem ser feitas usando `PreferencesManagerServiceClient` APIs.

**Resumo das etapas** Para gerenciar programaticamente os nós de preferências, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente PreferencesManagerService
1. Executar as operações de permissão ou função apropriadas

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PreferencesManagerService**

Antes de executar programaticamente uma operação User Management PreferencesManagerService, você deve criar um cliente PreferencesManagerService. Com a API Java, isso é feito criando um objeto PreferencesManagerServiceClient.

**Executar as operações de permissão ou função apropriadas**

Depois de criar o cliente de serviço, você pode chamar as operações do Gerenciador de preferências. O cliente do serviço permite ler e definir permissões.
