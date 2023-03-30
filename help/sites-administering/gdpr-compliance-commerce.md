---
title: Comércio AEM - Preparação para o GDPR
seo-title: AEM Commerce - GDPR Readiness
description: "Comércio AEM - Preparação para o GDPR"
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 71842228dd3cb1ce3b79728912e8333d25fccefc
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 0%

---

# Comércio AEM - Preparação para o GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes cobertos são aplicáveis a todas as regulamentações de proteção e privacidade de dados; como o GDPR e a CCPA.

O Regulamento Geral sobre a Proteção de Dados da União Europeia sobre os direitos de privacidade de dados entra em vigor em maio de 2018. Consulte a [Página do GDPR no Centro de privacidade do Adobe](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparação para o GDPR do AEM](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

![screen_shot_2018-03-22at11606](assets/screen_shot_2018-03-22at111606.jpg)

Com as integrações do Adobe out-of-the-box, AEM é a camada de experiência, consumindo os serviços para enviar dados de volta à plataforma de comércio do cliente que é executada em um modo sem periféricos.

Para algumas plataformas de comércio, o Adobe armazena informações de perfil ( `/home/users`) e tokens de comércio (para fazer logon na plataforma de comércio) no AEM. Para estes casos de uso, leia [Lidar com solicitações de GDPR para a plataforma de AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at11621](assets/screen_shot_2018-03-22at111621.jpg)

## Lidar com solicitações de GDPR para comércio de AEM {#handling-gdpr-requests-for-aem-commerce}

Para a integração do Salesforce Commerce Cloud, AEM Commerce não armazena informações relevantes do GDPR. Encaminhe a solicitação para o [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para as integrações hybris e HCL WebSphere® Commerce, há alguns dados em AEM. Use o [Instruções do GDPR da plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considere estas questões:

1. **Onde meus dados são armazenados/usados?** Informações de perfil de usuário em cache, como nome, identificador de usuário do Commerce, token, senha e dados de endereço, conforme mostrado AEM.
1. **Com quem compartilho os dados do GDPR cobertos?** Qualquer atualização dos dados relevantes do GDPR no AEM Commerce não é armazenada (exceto informações de perfil relevantes, como mencionado acima), mas é enviada de volta em proxy para a plataforma de comércio.
1. **Como excluir meus dados de usuário**? Exclua o perfil de usuário no AEM e chame a exclusão de usuário na plataforma de comércio.

>[!NOTE]
>
>Dê uma olhada no [wiki da hybris](https://wiki.hybris.com/) ou [Documentação do HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), se necessário.
