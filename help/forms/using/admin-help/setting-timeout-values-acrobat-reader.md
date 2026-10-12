---
title: Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC
description: Saiba como definir valores de tempo limite para usar com as extensões do Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
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
source-wordcount: '190'
ht-degree: 0%
---
# Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Ao trabalhar em muitos arquivos PDF nas extensões do Acrobat Reader DC, verifique se os seguintes valores de tempo limite estão definidos adequadamente para evitar que as tarefas atinjam o tempo limite e falhem:

**Tempo Limite para Descarte de Documentos**

Esse valor pode ser definido no console de administração. Clique em Configurações > Configurações principais do sistema > Configurações e especifique um valor para Tempo limite padrão de descarte de documentos.

**Tempo limite de formulários AEM do User Manager:** Esse valor pode ser definido ao editar o arquivo config.xml. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração e clique em Exportar. Abra o arquivo config.xml exportado e edite as seguintes linhas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salve e importe o arquivo config.xml de volta para o console de administração.

**Tempo Limite da Sessão do Servidor de Aplicativos:** Esse valor pode ser definido no servidor de aplicativos. Para obter mais informações, consulte a documentação fornecida com o servidor de aplicativos.
