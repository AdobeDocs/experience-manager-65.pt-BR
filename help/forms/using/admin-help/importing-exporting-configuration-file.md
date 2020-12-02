---
title: Importação e exportação do arquivo de configuração
seo-title: Importação e exportação do arquivo de configuração
description: Saiba como importar e exportar o arquivo de configuração para editar as preferências do servidor ou configurar outra instância do produto de formulários AEM.
seo-description: Saiba como importar e exportar o arquivo de configuração para editar as preferências do servidor ou configurar outra instância do produto de formulários AEM.
uuid: 32e8a709-2d7c-4740-9533-d53aa751bc58
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c1636537-f7dc-48d8-a3f0-9052bcd28b62
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---


# Importando e exportando o arquivo de configuração {#importing-and-exporting-the-configuration-file}

Use a página Configuração manual para baixar uma cópia das configurações no formato XML. As configurações neste arquivo controlam todas as preferências do servidor. Em seguida, você pode editar o arquivo e carregá-lo de volta ao servidor. Você também pode usar o arquivo para configurar outra instância de produto de formulários AEM.

Para evitar riscos de segurança, o valor da senha de ligação para o servidor de diretório não está incluído num ficheiro de configuração exportado. Atualize a senha no arquivo XML antes de importá-lo para um novo sistema.

>[!NOTE]
>
>A importação do arquivo de configuração reconfigura AEM formulários com base nas informações do arquivo. Somente um administrador do sistema ou um consultor de serviços profissionais familiarizado com o produto de formulários AEM e o XML devem considerar modificar o arquivo de configuração. Talvez seja necessário editar o arquivo de configuração, por exemplo, para reconfigurar uma configuração corrompida.

**Exportar as informações de configuração**

1. No Console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Importar e exportar arquivos de configuração.
1. Clique em Exportar. Se estiver usando o Microsoft Internet Explorer, você será solicitado a especificar um local para salvar o arquivo. Se você estiver usando o Firefox, o arquivo será salvo na área de trabalho.

**Importar as informações de configuração**

1. No Console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Importar e exportar arquivos de configuração.
1. Clique em Procurar para localizar o arquivo de configuração, clique em Importar e em OK.

