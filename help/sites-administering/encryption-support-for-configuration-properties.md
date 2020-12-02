---
title: Suporte de criptografia para propriedades de configuração
seo-title: Suporte de criptografia para propriedades de configuração
description: 'null'
seo-description: nulo
uuid: 26dc5e46-9332-4d9b-8874-895b90391e8c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
discoiquuid: 4e08c297-aa4b-44cf-84c8-1e11582d9ebb
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# Suporte de criptografia para propriedades de configuração{#encryption-support-for-configuration-properties}

## Visão geral {#overview}

Esse recurso permite que todas as propriedades de configuração do OSGi sejam armazenadas em um formulário criptografado protegido em vez de texto limpo. O formulário na interface do usuário do console da Web é usado para criar texto criptografado a partir de texto não criptografado usando a chave principal de criptografia do sistema inteiro.

O suporte ao Plug-in de configuração OSGi foi adicionado para descriptografar a propriedade antes de ser usada por um serviço.

>[!NOTE]
>
>Os serviços que esperam um valor criptografado precisam usar a verificação IsProtected para ver se o valor é criptografado antes de tentar descriptografá-lo, pois ele já pode ter sido descriptografado.

## Ativando o suporte à criptografia {#enabling-encryption-support}

Estas etapas mostram como criptografar a senha SMTP para o serviço de e-mail. Você pode concluir essas etapas para uma propriedade OSGI que deseja criptografar.

1. Vá para o console da Web AEM em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. No canto superior esquerdo, vá para **Principal - Suporte de criptografia**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. A página **Adobe Experience Manager Web Console Crypto Support** é exibida.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. No campo **Texto sem formatação**, digite o texto dos dados confidenciais que deseja proteger.
1. Selecione **Protect**. O texto Protegido é exibido como texto criptografado.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copie o texto protegido da Etapa 5 e cole-o no valor do formulário OSGI. Neste exemplo, a senha criptografada **SMTP** é adicionada ao *Serviço de e-mail Day CQ*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Salve as propriedades do serviço Day CQ Mail. A senha SMTP agora será enviada como um valor criptografado.

## Suporte para descriptografia {#decryption-support}

AEM agora fornece um Plug-in de configuração para descriptografar as propriedades de configuração. Este plug-in AEM descriptografará e recuperará automaticamente as propriedades de texto limpo.
