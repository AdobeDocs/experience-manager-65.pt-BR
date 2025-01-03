---
title: Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC
description: Saiba como definir valores de tempo limite para usar com extensões do Acrobat Reader DC.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

Ao trabalhar em muitos arquivos PDF nas extensões do Acrobat Reader DC, certifique-se de que os seguintes valores de tempo limite estejam definidos adequadamente para evitar que os trabalhos atinjam o tempo limite e falhem:

**Tempo Limite para Descarte de Documentos**

Esse valor pode ser definido no console de administração. Clique em Configurações > Configurações principais do sistema > Configurações e especifique um valor para Tempo limite padrão de descarte de documentos.

**Tempo limite de AEM do Gerenciador de Usuários:** Esse valor pode ser definido ao editar o arquivo config.xml. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração e clique em Exportar. Abra o arquivo config.xml exportado e edite as seguintes linhas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salve e importe o arquivo config.xml de volta para o console de administração.

**Tempo Limite da Sessão do Servidor de Aplicativos:** Esse valor pode ser definido no servidor de aplicativos. Para obter mais informações, consulte a documentação fornecida com o servidor de aplicativos.
