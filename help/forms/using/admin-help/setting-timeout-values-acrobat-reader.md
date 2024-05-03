---
title: Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC
description: Saiba como definir valores de tempo limite para usar com extensões do Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Ao trabalhar em muitos arquivos PDF nas extensões do Acrobat Reader DC, certifique-se de que os seguintes valores de tempo limite estejam definidos adequadamente para evitar que os trabalhos atinjam o tempo limite e falhem:

**Tempo Limite de Descarte de Documento**

Esse valor pode ser definido no console de administração. Clique em Configurações > Configurações principais do sistema > Configurações e especifique um valor para Tempo limite padrão de descarte de documentos.

**Tempo limite de formulários AEM do Gerenciador de usuários:** Esse valor pode ser definido ao editar o arquivo config.xml. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração e clique em Exportar. Abra o arquivo config.xml exportado e edite as seguintes linhas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salve e importe o arquivo config.xml de volta para o console de administração.

**Tempo Limite de Sessão do Servidor de Aplicativos:** Esse valor pode ser definido no servidor de aplicativos. Para obter mais informações, consulte a documentação fornecida com o servidor de aplicativos.
