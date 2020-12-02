---
title: Configuração do Connector para IBM Content Manager
seo-title: Configuração do Connector para IBM Content Manager
description: Configure o Connector for IBM Content Manager para permitir a comunicação entre formulários AEM e o IBM Content Manager.
seo-description: Configure o Connector for IBM Content Manager para permitir a comunicação entre formulários AEM e o IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Configurando o Connector para IBM Content Manager{#configuring-connector-for-ibm-content-manager}

O Connector for IBM Content Manager permite a comunicação entre formulários AEM e o IBM Content Manager. Para obter informações adicionais de plano de fundo, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurar a conexão do IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. No console de administração, clique em Serviços > Conector para IBM Content Manager.
1. Na caixa Nome do armazenamento de dados, digite o nome do armazenamento de dados do IBM Content Manager ao qual você deseja se conectar. Se o banco de dados for local, informe o nome do banco de dados. Se o banco de dados for remoto, insira o nome do alias.
1. Na caixa Nome de usuário, digite a ID de usuário de um usuário que se conectará ao armazenamento de dados do IBM Content Manager.
1. Na caixa Senha, digite a senha do usuário.
1. (Opcional) Na caixa String de conexão com alias, digite argumentos de conexão adicionais. Na maioria dos casos, esta caixa deve estar vazia. Para obter informações adicionais, consulte a documentação da IBM.
1. Clique em Salvar.

## Validação das configurações de serviço {#validation-of-service-settings}

Se você inserir um alias, nome de usuário ou senha incorretos do dataStore, obterá os seguintes resultados, dependendo de o serviço Content Repository Connector for IBM Content Manager estar em execução no momento:

* Se o serviço for parado, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você start o serviço, uma exceção será lançada e o serviço não será start.
* Se o serviço for iniciado, quando você salvar as informações de configuração do serviço, ele tentará validar as informações de credenciais imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.

