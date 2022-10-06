---
title: Configuração de fontes de fallback
seo-title: Configuring fallback fonts
description: Saiba como configurar fontes de fallback.
seo-description: Learn how to configure fallback fonts.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 0%

---

# Configuração de fontes de fallback {#configuring-fallback-fonts}

Você pode configurar manualmente o arquivo FontManagerResources.properties para mapear as fontes padrão AEM formulários para fallback (ou substituto) se as fontes padrão não estiverem disponíveis no servidor. Esse arquivo de propriedade está localizado no arquivo adobe-fontmanager.jar.

>[!NOTE]
>
>A configuração de fonte de fallback também se aplica ao serviço de montagem.

1. Navegue até o adobe-livecycle-*`[appserver]`* Arquivo .ear no *`[aem-forms root]`*/configurationManager/export, faça uma cópia de backup e descompacte o original.
1. Localize o arquivo adobe-fontmanager.jar e descompacte-o.
1. Localize o arquivo FontManagerResources.properties e abra-o em um editor de texto.
1. Modifique os locais e nomes das fontes Genéricas e de Fallback, conforme necessário, e salve o arquivo.

   As entradas de fonte no arquivo FontManagerResources.properties são relativas à variável *`[aem-forms root]`* diretório /fonts. Se você especificar fontes que não são padrão AEM fontes de formulários, deverá instalar essas fontes dentro dessa estrutura de diretório (em um diretório existente ou em um recém-criado).

   >[!NOTE]
   >
   >Se a fonte ou fonte padrão especificada não contiver um caractere unicode específico ou se não estiver disponível, o caractere será retirado de uma fonte de fallback de acordo com a seguinte prioridade:

   * Fonte específica da localidade
   * Fonte RAIZ se a localidade não estiver definida
   * Fonte genérica, pesquisada por ordem definida na tabela de fallback

1. Reempacote o arquivo adobe-fontmanager.jar.
1. Reempacote o adobe-livecycle-*`[appserver]`* Arquivo .ear e, em seguida, reimplante-o manualmente ou executando o Configuration Manager.

>[!NOTE]
>
>Não use o Configuration Manager para reempacotar o adobe-livecycle-`[appserver]`Arquivo .ear porque substituirá suas modificações pelos valores padrão dos formulários AEM.
