---
title: Comércio AEM - Preparação para o GDPR
seo-title: Comércio AEM - Preparação para o GDPR
description: '"Comércio AEM - Preparação para o GDPR"'
seo-description: 'null'
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Comércio AEM - Preparação para o GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes cobertos são aplicáveis a todas as regulamentações de proteção e privacidade de dados; como GDPR, CCPA etc.

O Regulamento Geral sobre a Proteção de Dados da União Europeia sobre os direitos de privacidade de dados entra em vigor em maio de 2018. Para obter mais informações, consulte a página [GDPR no Centro de privacidade do Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [AEM Preparação do GDPR](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

Em nossas integrações prontas para uso do Commerce, AEM é a camada de experiência, consumindo serviços e enviando dados de volta para a plataforma de comércio do cliente que é executada em um modo sem periféricos.

Para algumas plataformas de comércio, armazenamos informações de perfil ( `/home/users`) e tokens de comércio (para fazer logon na plataforma de comércio) no AEM. Para esses casos de uso, leia [Manipular solicitações do GDPR para a plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Manipular solicitações do GDPR para AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Para a integração do Salesforces Commerce Cloud, AEM Commerce não armazena informações relevantes do GDPR. Você deve encaminhar a solicitação para o [Salesforce Cloud](https://documentation.demandware.com/).

Para as integrações hybris e IBM WebSphere, há alguns dados em AEM. Você deve usar as [AEM instruções do GDPR da plataforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considerar estas perguntas:

1. **Onde meus dados são armazenados/usados?** As informações de perfil do usuário em cache, como nome, identificador de usuário do Commerce, token, senha, dados de endereço etc., são mostradas AEM.
1. **Com quem compartilho os dados do GDPR cobertos?** Qualquer atualização dos dados relevantes do GDPR no AEM Commerce não é armazenada (exceto informações de perfil relevantes, como mencionado acima), mas é enviada de volta em proxy para a plataforma de comércio.
1. **Como excluir meus dados** do usuário? Exclua o perfil de usuário no AEM e chame a exclusão de usuário na plataforma de comércio.

>[!NOTE]
>
>Consulte a [hybris wiki](https://wiki.hybris.com/) ou a [documentação do Websphere Commerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450), se necessário.

