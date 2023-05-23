---
title: Importação e exportação do arquivo de configuração
seo-title: Importing and exporting the configuration file
description: Saiba como importar e exportar o arquivo de configuração para editar as preferências do servidor ou configurar outra instância do produto AEM Forms.
seo-description: Learn how to import and export the configuration file in order to edit server preferences or configure another AEM forms product instance.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
exl-id: 225dbeb5-a21c-4338-98c7-e10c32973721
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Importação e exportação do arquivo de configuração {#importing-and-exporting-the-configuration-file}

Use a página Configuração Manual para baixar uma cópia das definições de configuração no formato XML. As configurações deste arquivo controlam todas as preferências do servidor. Em seguida, você pode editar o arquivo e carregá-lo de volta no servidor. Você também pode usar o arquivo para configurar outra instância do produto AEM Forms.

Para evitar riscos de segurança, o valor da senha de vinculação do servidor de diretório não é incluído em um arquivo de configuração exportado. Atualize a senha no arquivo XML antes de importar o arquivo para um novo sistema.

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura os formulários AEM com base nas informações do arquivo. Somente um administrador de sistema ou um consultor de serviços profissionais familiarizado com o produto AEM Forms e o XML deve considerar a modificação do arquivo de configuração. Talvez seja necessário editar o arquivo de configuração, por exemplo, para redefinir uma configuração corrompida.

**Exportar as informações de configuração**

1. No Console De Administração, clique Em Configurações > Gerenciamento De Usuários > Configuração > Importar E Exportar Arquivos De Configuração.
1. Clique em Exportar. Se estiver usando o Microsoft Internet Explorer, você será solicitado a especificar um local para salvar o arquivo. Se você estiver usando o Firefox, o arquivo será salvo na área de trabalho.

**Importar as informações de configuração**

1. No Console De Administração, clique Em Configurações > Gerenciamento De Usuários > Configuração > Importar E Exportar Arquivos De Configuração.
1. Clique em Procurar para localizar o arquivo de configuração, clique em Importar e em OK.
