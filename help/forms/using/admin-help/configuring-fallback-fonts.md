---
title: Configuração de fontes de fallback
seo-title: Configuração de fontes de fallback
description: Saiba como configurar fontes de fallback.
seo-description: Saiba como configurar fontes de fallback.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: Gerador de PDF
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Configurar fontes de fallback {#configuring-fallback-fonts}

Você pode configurar manualmente o arquivo FontManagerResources.properties para mapear as fontes padrão AEM formulários para fallback (ou substituto) se as fontes padrão não estiverem disponíveis no servidor. Esse arquivo de propriedade está localizado no arquivo adobe-fontmanager.jar.

>[!NOTE]
>
>A configuração de fonte de fallback também se aplica ao serviço de montagem.

1. Navegue até o arquivo adobe-livecycle-*`[appserver]`*.ear no diretório *`[aem-forms root]`*/configurationManager/export , faça uma cópia de backup e descompacte o original.
1. Localize o arquivo adobe-fontmanager.jar e descompacte-o.
1. Localize o arquivo FontManagerResources.properties e abra-o em um editor de texto.
1. Modifique os locais e nomes das fontes Genéricas e de Fallback, conforme necessário, e salve o arquivo.

   As entradas de fonte no arquivo FontManagerResources.properties são relativas ao diretório *`[aem-forms root]`*/fonts. Se você especificar fontes que não são padrão AEM fontes de formulários, deverá instalar essas fontes dentro dessa estrutura de diretório (em um diretório existente ou em um recém-criado).

   >[!NOTE]
   >
   >Se a fonte ou fonte padrão especificada não contiver um caractere unicode específico ou se não estiver disponível, o caractere será retirado de uma fonte de fallback de acordo com a seguinte prioridade:

   * Fonte específica da localidade
   * Fonte RAIZ se a localidade não estiver definida
   * Fonte genérica, pesquisada por ordem definida na tabela de fallback

1. Reempacote o arquivo adobe-fontmanager.jar.
1. Reempacote o arquivo adobe-livecycle-*`[appserver]`*.ear e depois reimplante-o manualmente ou executando o Configuration Manager.

>[!NOTE]
>
>Não use o Configuration Manager para reempacotar o arquivo adobe-livecycle-`[appserver]`.ear porque ele substituirá as modificações pelos valores padrão dos formulários AEM.

