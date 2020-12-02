---
title: Configuração de valores de tempo limite para uso com extensões Acrobat Reader DC
seo-title: Configuração de valores de tempo limite para uso com extensões Acrobat Reader DC
description: Saiba como definir valores de tempo limite para uso com extensões Acrobat Reader DC.
seo-description: Saiba como definir valores de tempo limite para uso com extensões Acrobat Reader DC.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---


# Configuração de valores de tempo limite para uso com extensões Acrobat Reader DC {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Ao trabalhar em vários arquivos PDF em extensões Acrobat Reader DC, verifique se os seguintes valores de tempo limite estão definidos adequadamente para evitar que as tarefas sejam atingidas e que falhem:

**Tempo limite de eliminação do documento**

Esse valor pode ser definido no console de administração. Clique em Configurações > Configurações principais do sistema > Configurações e especifique um valor para Tempo limite de eliminação padrão do Documento.

**Gerenciador de usuários AEM tempo limite de formulários:** esse valor pode ser definido editando o arquivo config.xml. No console de administração, clique em Configurações > Gerenciamento de usuário > Configuração > Importar e exportar arquivos de configuração e, em seguida, clique em Exportar. Abra o arquivo config.xml exportado e edite as seguintes linhas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot; />

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot; />

Salve e importe o arquivo config.xml de volta para o console de administração.

**Tempo limite da sessão do servidor de aplicativos:** esse valor pode ser definido no servidor de aplicativos. Para obter mais informações, consulte a documentação fornecida com o servidor de aplicativos.
