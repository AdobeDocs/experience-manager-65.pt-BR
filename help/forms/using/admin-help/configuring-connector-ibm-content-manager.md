---
title: Configuração do conector para o Gerenciador de conteúdo do IBM&reg;
description: Configure o Conector para o Gerenciador de conteúdo do IBM&reg; para permitir a comunicação entre os formulários AEM e o Gerenciador de conteúdo do IBM&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/connecting_to_a_content_management_system
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 50f0c963-8007-4e2a-aa73-d99b97d9a1aa
source-git-commit: ab3d016c7c9c622be361596137b150d8719630bd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Configuração do conector para o Gerenciador de conteúdo IBM®{#configuring-connector-for-ibm-content-manager}

O conector para o IBM® Content Manager permite a comunicação entre os formulários AEM e o IBM® Content Manager. Para obter informações adicionais, consulte &quot;Conectores para ECM&quot; em [Referência de serviços](https://www.adobe.com/go/learn_aemforms_services_63).

## Configurar a conexão do Gerenciador de conteúdo IBM® {#configure-the-ibm-content-manager-connection}

1. No console de administração, clique em Serviços > Conector para o IBM® Content Manager.
1. Na caixa Nome do armazenamento de dados, digite o nome do armazenamento de dados do IBM® Content Manager ao qual você deseja se conectar. Se o banco de dados for local, digite o nome do banco de dados. Se o banco de dados for remoto, digite seu nome de alias.
1. Na caixa Nome do usuário, digite a ID do usuário que vai se conectar ao armazenamento de dados do IBM® Content Manager.
1. Na caixa Senha, digite a senha do usuário.
1. (Opcional) Na caixa String de Conexão de Alias, insira argumentos de conexão adicionais. Normalmente, essa caixa deve estar vazia. Para obter informações adicionais, consulte a documentação da IBM®.
1. Clique em Salvar.

## Validação das configurações de serviço {#validation-of-service-settings}

Se você digitar um alias, nome de usuário ou senha incorretos do dataStore, os resultados a seguir serão exibidos dependendo se o Conector de repositório de conteúdo do serviço IBM® Content Manager estiver em execução:

* Se o serviço for interrompido, quando você salvar as informações de configuração do serviço, nenhum erro será exibido. No entanto, na próxima vez que você iniciar o serviço, uma exceção será lançada e o serviço não será iniciado.
* Se o serviço for iniciado, quando você salvar as informações de configuração do serviço, o serviço tentará validar as informações de credencial imediatamente. Nesse caso, ocorre um erro e as informações de configuração não são salvas.
