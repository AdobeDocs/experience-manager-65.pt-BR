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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%
---
# Gerenciando programaticamente os nós de preferências {#programmatically-managing-the-preferencesnodes}

**Exemplos e exemplos neste documento são somente para AEM Forms no ambiente JEE.**

Este tópico descreve como você pode usar a API de serviço do Gerenciador de preferências (Java) para gerenciar programaticamente os nós de preferências.

Você pode alterar manualmente as definições de configuração na interface do Administrador. Para alterar as opções, navegue até `Home>Settings>User Management> Configuration>Manual Configuration`. Importar `config.xml` depois de fazer as alterações, você notará que todas as alterações, exceto as alterações feitas no nó `/Adobe/Adobe Experience Manager Forms/Config/UM persist`, foram perdidas. A visualização da Importação e exportação do Gerenciamento de usuários não oferece suporte à alteração das definições de configuração de outros componentes. Agora, essas alterações podem ser feitas usando as APIs `PreferencesManagerServiceClient`.

**Resumo das etapas** Para gerenciar programaticamente os Nós de Preferências, execute as seguintes etapas:

1. Incluir arquivos de projeto.
1. Criar um cliente PreferencesManagerService
1. Executar as operações de permissão ou função apropriadas

**Incluir arquivos de projeto**

Inclua os arquivos necessários no projeto de desenvolvimento. Se você estiver criando uma aplicação cliente usando Java, inclua os arquivos JAR necessários. Se você estiver usando serviços da Web, certifique-se de incluir os arquivos proxy.

**Criar um cliente PreferencesManagerService**

Antes de executar programaticamente uma operação User Management PreferencesManagerService, você deve criar um cliente PreferencesManagerService. Com a API Java, isso é feito criando um objeto PreferencesManagerServiceClient.

**Invocar as operações de permissão ou função apropriadas**

Depois de criar o cliente de serviço, você pode chamar as operações do Gerenciador de preferências. O cliente do serviço permite ler e definir permissões.
