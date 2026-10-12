---
title: Iniciar e parar serviços
description: Saiba como iniciar e parar serviços associados aos módulos do AEM Forms e ao servidor de aplicativos e banco de dados.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 55bf5196-22c6-4286-8c92-ff44d81dde49
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
source-wordcount: '311'
ht-degree: 0%
---
# Iniciar e parar serviços {#starting-and-stopping-services}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Há dois tipos de serviços que fazem parte dos formulários do AEM:

* Serviços que controlam o servidor de aplicativos e o banco de dados do AEM Forms.
* Serviços que controlam os módulos de formulários do AEM

## Iniciar ou parar os serviços associados aos módulos do AEM Forms {#start-or-stop-the-services-associated-with-aem-forms-modules}

Os módulos do AEM Forms (por exemplo, Forms, Rights Management, Output) operam como serviços. Às vezes, pode ser necessário interromper ou iniciar os serviços desses módulos do AEM Forms. Por exemplo, você deve interromper e reiniciar um serviço do AEM Forms depois de alterar uma configuração do serviço.

>[!NOTE]
>
> É recomendável usar o comando &#39;Ctrl + C&#39; para reiniciar o SDK. Reiniciar o AEM SDK usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

1. No console de administração, clique em **Serviços** > **Aplicativos e Serviços** > **Gerenciamento de Serviços**.
1. Na página Gerenciamento de Serviços, marque a caixa de seleção ao lado do serviço a ser interrompido ou iniciado e clique em Interromper ou Iniciar.

## Iniciar ou interromper serviços para o servidor de aplicativos e o banco de dados {#start-or-stop-services-for-the-application-server-and-database}

Uma implementação completa do AEM Forms inclui um servidor de aplicativos e serviços de banco de dados:

* *`[application server]`* para formulários do AEM
* *`[database]`* para formulários do AEM

No Windows, esses serviços podem ser acessados por meio das **Ferramentas Administrativas** > **Painel de serviços**. Por exemplo, se você instalou o AEM Forms no JBoss usando o método turnkey, os seguintes serviços estão disponíveis no sistema:

* JBoss para o Adobe Experience Manager Forms
* MySQL para Adobe Experience Manager Forms

Inicie ou interrompa esses serviços selecionando-os na lista do painel Serviços e clicando no botão de ação apropriado no painel.

No UNIX® ou Linux, digite o seguinte texto em uma linha de comando, onde *`[service name]`* é o nome do serviço que você está verificando:

```java
     ps -A | grep [service name]
```
