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
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---

# Iniciar e parar serviços {#starting-and-stopping-services}

Há dois tipos de serviços que fazem parte dos formulários AEM:

* Serviços que controlam o servidor de aplicativos e o banco de dados do AEM Forms.
* Serviços que controlam módulos de formulários AEM

## Iniciar ou parar os serviços associados aos módulos de formulários AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

Os módulos de formulários AEM (por exemplo, Forms, Rights Management, Output) operam como serviços. Às vezes, pode ser necessário interromper ou iniciar os serviços desses módulos de formulários AEM. Por exemplo, você deve interromper e reiniciar um serviço de formulários AEM depois de alterar uma configuração do serviço.

>[!NOTE]
>
> É recomendável usar o comando &quot;Ctrl + C&quot; para reiniciar o SDK. Reiniciar o SDK do AEM usando métodos alternativos, por exemplo, parar processos Java, pode levar a inconsistências no ambiente de desenvolvimento do AEM.

1. No console de administração, clique em **Serviços** > **Aplicativos e serviços** > **Gerenciamento de serviços**.
1. Na página Gerenciamento de Serviços, marque a caixa de seleção ao lado do serviço a ser interrompido ou iniciado e clique em Interromper ou Iniciar.

## Iniciar ou interromper serviços para o servidor de aplicativos e o banco de dados {#start-or-stop-services-for-the-application-server-and-database}

Uma implementação completa dos formulários AEM inclui um servidor de aplicativos e serviços de banco de dados:

* *`[application server]`* para formulários AEM
* *`[database]`* para formulários AEM

No Windows, esses serviços podem ser acessados por meio da **Ferramentas administrativas** > **Painel Serviços**. Por exemplo, se você instalou formulários AEM no JBoss usando o método turnkey, os seguintes serviços estão disponíveis no sistema:

* JBoss para o Adobe Experience Manager Forms
* MySQL para Adobe Experience Manager Forms

Inicie ou interrompa esses serviços selecionando-os na lista do painel Serviços e clicando no botão de ação apropriado no painel.

No UNIX® ou Linux, digite o seguinte texto a partir de uma linha de comando, onde *`[service name]`* é o nome do serviço que você está verificando:

```java
     ps -A | grep [service name]
```
