---
title: Configuração de fontes de fallback
description: Saiba como configurar fontes substitutas para o AEM Forms. Você pode usar o arquivo FontManagerResources.properties para mapear as fontes padrão para as fontes de fallback manualmente.
uuid: 2745541c-8c6d-4bb4-aa14-ec19afd6bc35
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d997a268-a40a-462d-badd-94f0731f7ba4
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# Configuração de fontes de fallback {#configuring-fallback-fonts}

Você pode configurar manualmente o arquivo FontManagerResources.properties para mapear as fontes de formulários AEM padrão para fallback (ou substituto) se as fontes padrão não estiverem disponíveis no servidor. Esse arquivo de propriedade está no arquivo adobe-fontmanager.jar.

>[!NOTE]
>
>A configuração de fonte de fallback também se aplica ao serviço de montagem.

1. Navegue até o adobe-livecycle-*`[appserver]`* arquivo .ear no *`[aem-forms root]`* diretório /configurationManager/export, faça uma cópia de backup e desempacote o original.
1. Localize o arquivo adobe-fontmanager.jar e desempacote-o.
1. Localize o arquivo FontManagerResources.properties e abra-o em um editor de texto.
1. Modifique os locais e nomes das fontes Genérica e de Fallback, conforme necessário, e salve o arquivo.

   As entradas de fonte no arquivo FontManagerResources.properties são relativas ao *`[aem-forms root]`* diretório /fonts. Se você especificar fontes que não sejam fontes de formulários AEM padrão, instale essas fontes dentro dessa estrutura de diretório (seja em um diretório existente ou em um recém-criado).

   >[!NOTE]
   >
   >Se a fonte especificada ou a fonte padrão não contiver um caractere unicode específico ou se não estiver disponível, o caractere será retirado de uma fonte de fallback de acordo com a seguinte prioridade:

   * Fonte específica da localidade
   * Fonte ROOT se localidade não estiver definida
   * Fonte genérica, pesquisada por conjunto de ordens na tabela de fallback

1. Reempacotar o arquivo adobe-fontmanager.jar.
1. Reempacotar o adobe-livecycle-*`[appserver]`* arquivo .ear e, em seguida, reimplante-o manualmente ou executando o Configuration Manager.

>[!NOTE]
>
>Não use o Configuration Manager para empacotar novamente o adobe-livecycle-`[appserver]`Arquivo .ear porque ele substituirá suas modificações pelos valores padrão dos formulários AEM.
