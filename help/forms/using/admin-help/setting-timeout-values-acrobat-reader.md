---
title: Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC
seo-title: Setting timeout values for use with Acrobat Reader DC extensions
description: Saiba como definir valores de tempo limite para usar com extensões do Acrobat Reader DC.
seo-description: Learn how to set timeout values for use with Acrobat Reader DC extensions.
uuid: d6d072a0-0a30-417a-98b1-df8b4ff8f911
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_acrobat_reader_dc_extensions
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a9aeeb89-45e9-4d5d-aa25-8145c89b64f2
exl-id: 0a55aab3-14a3-41ad-8533-dc2cd116a848
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Configuração de valores de tempo limite para uso com extensões do Acrobat Reader DC  {#setting-timeout-values-for-use-with-acrobat-reader-dc-extensions}

Ao trabalhar em muitos arquivos PDF nas extensões do Acrobat Reader DC, certifique-se de que os seguintes valores de tempo limite estejam definidos adequadamente para evitar que os processos atinjam o tempo limite e falhem:

**Tempo Limite de Descarte de Documento**

Esse valor pode ser definido no console de administração. Clique em Configurações > Configurações principais do sistema > Configurações e especifique um valor para Tempo limite padrão de descarte de documentos.

**Tempo limite de formulários AEM do Gerenciador de usuários:** Esse valor pode ser definido ao editar o arquivo config.xml. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração e clique em Exportar. Abra o arquivo config.xml exportado e edite as seguintes linhas:

&lt;entry key=&quot;assertionValidityInMinutes&quot; value=&quot;600&quot;/>

&lt;entry key=&quot;SessionTimeout&quot; value=&quot;600&quot;/>

Salve e importe o arquivo config.xml de volta para o console de administração.

**Tempo Limite de Sessão do Servidor de Aplicativos:** Esse valor pode ser definido no servidor de aplicativos. Para obter mais informações, consulte a documentação fornecida com o servidor de aplicativos.
