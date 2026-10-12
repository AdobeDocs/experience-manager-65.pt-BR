---
title: Importação e exportação do arquivo de configuração
description: Saiba como importar e exportar o arquivo de configuração para editar as preferências do servidor ou configurar outra instância do produto AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
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
source-wordcount: '264'
ht-degree: 0%
---
# Importação e exportação do arquivo de configuração {#importing-and-exporting-the-configuration-file}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Use a página Configuração Manual para baixar uma cópia das definições de configuração no formato XML. As configurações deste arquivo controlam todas as preferências do servidor. Em seguida, você pode editar o arquivo e carregá-lo de volta no servidor. Você também pode usar o arquivo para configurar outra instância do produto AEM Forms.

Para evitar riscos de segurança, o valor da senha de vinculação do servidor de diretório não é incluído em um arquivo de configuração exportado. Atualize a senha no arquivo XML antes de importar o arquivo para um novo sistema.

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura os formulários do AEM com base nas informações do arquivo. Somente um administrador do sistema ou um consultor de serviços profissionais familiarizado com o produto AEM Forms e o XML deve considerar a modificação do arquivo de configuração. Talvez seja necessário editar o arquivo de configuração, por exemplo, para redefinir uma configuração corrompida.

**Exportar as informações de configuração**

1. No Console De Administração, clique Em Configurações > Gerenciamento De Usuários > Configuração > Importar E Exportar Arquivos De Configuração.
1. Clique em Exportar. Se estiver usando o Microsoft Internet Explorer, você será solicitado a especificar um local para salvar o arquivo. Se você estiver usando o Firefox, o arquivo será salvo na área de trabalho.

**Importar as informações de configuração**

1. No Console De Administração, clique Em Configurações > Gerenciamento De Usuários > Configuração > Importar E Exportar Arquivos De Configuração.
1. Clique em Procurar para localizar o arquivo de configuração, clique em Importar e em OK.
