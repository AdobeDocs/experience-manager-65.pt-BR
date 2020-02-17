---
title: Iniciar e parar serviços
seo-title: Iniciar e parar serviços
description: Saiba como iniciar e parar os serviços associados aos módulos do AEM Forms e ao servidor e banco de dados de aplicativos.
seo-description: Saiba como iniciar e parar os serviços associados aos módulos do AEM Forms e ao servidor e banco de dados de aplicativos.
uuid: 8c831cb2-4165-4118-8a09-764cec4e5e05
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_services
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b93060bd-c6e1-40d2-8acd-ccafb8ed56da
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Iniciar e parar serviços {#starting-and-stopping-services}

Há dois tipos de serviços que fazem parte dos formulários do AEM:

* Serviços que controlam o banco de dados e o servidor de aplicativos para formulários AEM.
* Serviços que controlam módulos de formulários do AEM

## Iniciar ou parar os serviços associados aos módulos de formulários do AEM {#start-or-stop-the-services-associated-with-aem-forms-modules}

Os módulos de formulários AEM (por exemplo, Forms, Rights Management, Output) operam como serviços. Às vezes, pode ser necessário interromper ou iniciar os serviços desses módulos de formulários do AEM. Por exemplo, você deve parar e reiniciar um serviço de formulários AEM depois de alterar uma configuração para o serviço.

1. No console de administração, clique em **Serviços** > **Aplicativos e serviços** > Gerenciamento **** de serviços.
1. Na página Gerenciamento de serviços, marque a caixa de seleção ao lado do serviço para parar ou iniciar e clique em Parar ou Iniciar.

## Iniciar ou parar serviços para o servidor de aplicativos e banco de dados {#start-or-stop-services-for-the-application-server-and-database}

Uma implementação completa dos formulários AEM inclui um servidor de aplicativos e serviços de banco de dados:

* *`[application server]`* para formulários AEM
* *`[database]`* para formulários AEM

No Windows, esses serviços podem ser acessados por meio de Ferramentas **administrativas > painel** **** Serviços. Por exemplo, se você instalou formulários AEM em JBoss usando o método chave na mão, os seguintes serviços estão disponíveis no sistema:

* Formulários JBoss for Adobe Experience Manager
* Formulários MySQL for Adobe Experience Manager

Inicie ou pare esses serviços selecionando-os na lista no painel Serviços e, em seguida, clicando no botão de ação apropriado no painel.

No UNIX® ou no Linux, insira o seguinte texto de uma linha de comando, onde *`[service name]`* é o nome do serviço que você está verificando:

```as3
     ps -A | grep [service name]
```

