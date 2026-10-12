---
title: AEM Commerce - Disponibilidade do GDPR
description: Saiba mais sobre os procedimentos para lidar com solicitações do GDPR no AEM Commerce e como usá-los.
contentOwner: carlino
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
solution: Experience Manager, Experience Manager Sites
feature: Compliance
role: Admin, Developer, Leader, User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c42c36cf-eeed-484a-8b39-a33a68192a07
    internal-label: Compliance
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%
---
# AEM Commerce - Disponibilidade do GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR e o CCPA.

O Regulamento Geral sobre a Proteção de Dados da União Europeia entra em vigor em maio de 2018. Consulte a [página do GDPR no Centro de privacidade da Adobe](https://business.adobe.com/br/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Preparação do GDPR da AEM](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Com as integrações Commerce prontas para uso da Adobe, o AEM é a camada de experiência, consumindo serviços e enviando dados de volta para a plataforma de comércio do cliente, que é executada em um modo headless.

Para algumas plataformas de comércio, o Adobe armazena informações de perfil ( `/home/users`) e tokens de comércio (para fazer logon na plataforma de comércio) no AEM. Para estes casos de uso, leia [Manipulando solicitações do GDPR para a plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Lidar com solicitações do GDPR para o AEM Commerce {#handling-gdpr-requests-for-aem-commerce}

Para a integração do Salesforce Commerce Cloud, a AEM Commerce não armazena informações relevantes do GDPR. Encaminhe a solicitação para a [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para as integrações hybris e HCL WebSphere® Commerce, há alguns dados no AEM. Use as [instruções do GDPR da Plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considere estas perguntas:

1. **Onde meus dados são armazenados/usados?** Informações de perfil de usuário em cache, como nome, identificador de usuário de comércio, token, senha e dados de endereço, conforme mostrado no AEM.
1. **Com quem compartilho os dados cobertos do GDPR?** Nenhuma atualização de dados relevantes para o GDPR na AEM Commerce é armazenada (exceto as informações de perfil relevantes, como mencionado acima), mas é enviada por proxy para a plataforma de comércio.
1. **Como excluir meus dados de usuário**? Exclua o perfil de usuário no AEM e chame a exclusão de usuário na plataforma de comércio.

>[!NOTE]
>
>Consulte a [hybris wiki](https://wiki.hybris.com/) ou a [documentação do HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), se necessário.
