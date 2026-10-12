---
title: Suporte de criptografia para propriedades de configuração
description: Saiba mais sobre o suporte à criptografia para propriedades de configuração fornecidas no AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%
---
# Suporte de criptografia para propriedades de configuração{#encryption-support-for-configuration-properties}

## Visão geral {#overview}

Esse recurso permite que todas as propriedades de configuração do OSGi sejam armazenadas em um formulário criptografado protegido, em vez de texto não criptografado. O formulário na interface do usuário do Console da Web é usado para criar texto criptografado a partir de texto não criptografado usando a chave mestra de criptografia em todo o sistema.

O suporte ao OSGi Configuration Plugin foi adicionado para descriptografar a propriedade antes que ela fosse usada por um serviço.

>[!NOTE]
>
>Os serviços que esperam um valor criptografado precisam usar a verificação IsProtected para ver se o valor está criptografado antes de tentar descriptografá-lo, pois ele já pode ter sido descriptografado.

## Ativação do suporte de criptografia {#enabling-encryption-support}

Essas etapas mostram como criptografar a senha SMTP para o serviço de email. Você pode concluir essas etapas para uma propriedade OSGI que deseja criptografar.

1. Vá para o Console da Web do AEM em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. No canto superior esquerdo, vá para **Principal - Suporte a criptografia**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. A página **Suporte à Criptografia do Console da Web da Adobe Experience Manager** é exibida.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. No campo **Texto sem formatação**, digite o texto dos dados confidenciais que deseja proteger.
1. Selecione **Proteger**. O texto protegido é exibido como texto criptografado.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copie o Texto protegido da Etapa 5 e cole-o no valor de Formulário OSGI. Neste exemplo, a **senha SMTP** criptografada é adicionada ao *Day CQ Mail Service*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Salve as propriedades do Day CQ Mail Service. A senha SMTP agora será enviada como um valor criptografado.

## Suporte para descriptografia {#decryption-support}

O AEM agora fornece um Plug-in de configuração para descriptografar propriedades de configuração. Este plug-in do AEM descriptografará e recuperará automaticamente as propriedades de texto não criptografado.
