---
title: Configuração do conector para o IBM Content Manager
seo-title: Configuring Connector for IBM Content Manager
description: Configure o Conector para o IBM Content Manager para permitir a comunicação entre AEM formulários e o IBM Content Manager.
seo-description: Configure the Connector for IBM Content Manager to enable communication between AEM forms and IBM Content Manager.
uuid: 3d55169d-93e3-4d4e-b18b-2a3394e1de3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3094b178-3b1a-46b3-8fbd-c20388afa3a7
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Configuração do conector para o IBM Content Manager{#configuring-connector-for-ibm-content-manager}

O conector para o IBM Content Manager permite a comunicação entre formulários AEM e o IBM Content Manager. Para obter mais informações de fundo, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurar a conexão do IBM Content Manager {#configure-the-ibm-content-manager-connection}

1. No console de administração, clique em Serviços > Conector para IBM Content Manager.
1. Na caixa Nome do armazenamento de dados, digite o nome do armazenamento de dados do IBM Content Manager ao qual deseja se conectar. Se o banco de dados for local, insira o nome do banco de dados. Se o banco de dados for remoto, insira o nome do alias.
1. Na caixa Nome do usuário, digite o ID do usuário de um usuário que se conectará ao armazenamento de dados do IBM Content Manager.
1. Na caixa Senha, digite a senha do usuário.
1. (Opcional) Na caixa Sequência de conexão de alias, insira argumentos de conexão adicionais. Na maioria dos casos, essa caixa deve estar vazia. Para obter mais informações, consulte a documentação do IBM.
1. Clique em Salvar.

## Validação das configurações do serviço {#validation-of-service-settings}

Se você inserir um alias, nome de usuário ou senha incorretos do dataStore, obterá os seguintes resultados, dependendo se o Conector de Repositório de Conteúdo para o serviço IBM Content Manager está em execução no momento:

* Se o serviço for interrompido, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço for iniciado, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações da credencial imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.
