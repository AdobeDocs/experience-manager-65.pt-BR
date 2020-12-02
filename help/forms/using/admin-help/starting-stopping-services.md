---
title: Iniciar e parar serviços
seo-title: Iniciar e parar serviços
description: Saiba como start e interromper os serviços associados aos módulos AEM Forms, ao servidor de aplicativos e ao banco de dados.
seo-description: Saiba como start e interromper os serviços associados aos módulos AEM Forms, ao servidor de aplicativos e ao banco de dados.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Iniciar e parar serviços {#starting-and-stopping-services}

Há dois tipos de serviços que fazem parte de AEM formulários:

* Serviços que controlam o banco de dados e o servidor de aplicativos para formulários AEM.
* Serviços que controlam AEM módulos de formulários

## Start ou interrupção dos serviços associados aos módulos de formulários AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

AEM módulos de formulários (por exemplo, Forms, Rights Management, Saída) operam como serviços. Às vezes, pode ser necessário interromper ou start os serviços desses módulos de formulários AEM. Por exemplo, você deve parar e reiniciar um serviço de formulários AEM depois de alterar uma configuração para o serviço.

1. No console de administração, clique em **Serviços** > **Aplicativos e Serviços** > **Gerenciamento de Serviços**.
1. Na página Gerenciamento de serviços, marque a caixa de seleção ao lado do serviço a ser parado ou start e clique em Parar ou Start.

## Serviços de start ou interrupção para o servidor de aplicativos e banco de dados {#start-or-stop-services-for-the-application-server-and-database}

Uma implementação completa de formulários AEM inclui um servidor de aplicativos e serviços de banco de dados:

* *`[application server]`* para formulários AEM
* *`[database]`* para formulários AEM

No Windows, esses serviços são acessíveis por meio das **Ferramentas administrativas** > **Painel de serviços**. Por exemplo, se você instalou formulários AEM em JBoss usando o método chave na mão, os seguintes serviços estão disponíveis no sistema:

* Formulários JBoss for Adobe Experience Manager
* Formulários MySQL for Adobe Experience Manager

Start ou pare esses serviços selecionando-os na lista no painel Serviços e, em seguida, clicando no botão de ação apropriado no painel.

No UNIX® ou no Linux, insira o seguinte texto de uma linha de comando, onde *`[service name]`* é o nome do serviço que você está verificando:

```java
     ps -A | grep [service name]
```

