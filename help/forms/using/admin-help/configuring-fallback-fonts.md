---
title: Configuração de fontes de fallback
description: Saiba como configurar fontes substitutas para o AEM Forms. Você pode usar o arquivo FontManagerResources.properties para mapear as fontes padrão para as fontes de fallback manualmente.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 76dd2b0c-9f16-47bf-a565-99277be750fb
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: b26425d0-6fde-5e02-bfd6-e560e2fa86c9
    internal-label: PDF Generator
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%
---
# Configuração de fontes de fallback {#configuring-fallback-fonts}

Você pode configurar manualmente o arquivo FontManagerResources.properties para mapear as fontes padrão dos formulários do AEM para fallback (ou substituto) se as fontes padrão não estiverem disponíveis no servidor. Esse arquivo de propriedade está no arquivo adobe-fontmanager.jar.

>[!NOTE]
>
>A configuração de fonte de fallback também se aplica ao serviço de montagem.

1. Navegue até o arquivo adobe-livecycle-*`[appserver]`*.ear no diretório *`[aem-forms root]`*/configurationManager/export, faça uma cópia de backup e desempacote o original.
1. Localize o arquivo adobe-fontmanager.jar e desempacote-o.
1. Localize o arquivo FontManagerResources.properties e abra-o em um editor de texto.
1. Modifique os locais e nomes das fontes Genérica e de Fallback, conforme necessário, e salve o arquivo.

   As entradas de fonte no arquivo FontManagerResources.properties são relativas ao diretório *`[aem-forms root]`*/fonts. Se você especificar fontes que não sejam fontes padrão do AEM Forms, instale essas fontes dentro dessa estrutura de diretório (seja em um diretório existente ou em um recém-criado).

   >[!NOTE]
   >
   >Se a fonte especificada ou a fonte padrão não contiver um caractere unicode específico ou se não estiver disponível, o caractere será retirado de uma fonte de fallback de acordo com a seguinte prioridade:

   * Fonte específica da localidade
   * Fonte ROOT se localidade não estiver definida
   * Fonte genérica, pesquisada por conjunto de ordens na tabela de fallback

1. Reempacotar o arquivo adobe-fontmanager.jar.
1. Reempacote o arquivo adobe-livecycle-*`[appserver]`*.ear e implante-o novamente manualmente ou executando o Configuration Manager.

>[!NOTE]
>
>Não use o Configuration Manager para reempacotar o arquivo adobe-livecycle-`[appserver]`.ear porque ele substituirá suas modificações pelos valores padrão dos formulários do AEM.
