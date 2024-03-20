---
title: Suporte de criptografia para propriedades de configuração
description: Saiba mais sobre o suporte de criptografia para propriedades de configuração fornecido no AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: security
exl-id: 3c3db1c8-5b22-45dd-aeaf-5cf830a9486b
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '279'
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

1. Acesse o console da Web do AEM em *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr*
1. No canto superior esquerdo, vá para **Principal - Suporte a criptografia**

   ![chlimage_1-325](assets/chlimage_1-325.png)

1. A variável **Suporte à criptografia do console da Web da Adobe Experience Manager** é exibida.

   ![screen_shot_2018-08-01at113417am](assets/screen_shot_2018-08-01at113417am.png)

1. No **Texto sem formatação** insira o texto dos dados confidenciais que deseja proteger.
1. Selecionar **Protect**. O texto protegido é exibido como texto criptografado.

   ![screen_shot_2018-08-01at113844am](assets/screen_shot_2018-08-01at113844am.png)

1. Copie o Texto protegido da Etapa 5 e cole-o no valor de Formulário OSGI. Neste exemplo, o script **Senha SMTP** é adicionado à *Serviço de email Day CQ*.

   ![screen_shot_2016-12-18at105809pm](assets/screen_shot_2016-12-18at105809pm.png)

1. Salve as propriedades do Day CQ Mail Service. A senha SMTP agora será enviada como um valor criptografado.

## Suporte para descriptografia {#decryption-support}

O AEM agora fornece um Plug-in de configuração para descriptografar propriedades de configuração. Este plug-in AEM descriptografará e recuperará automaticamente as propriedades de texto não criptografado.
