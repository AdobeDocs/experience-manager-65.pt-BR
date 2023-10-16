---
title: Comércio AEM - Disponibilidade do GDPR
seo-title: AEM Commerce - GDPR Readiness
description: Saiba mais sobre os procedimentos para lidar com solicitações do GDPR no Comércio de AEM e como usá-los.
seo-description: null
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
exl-id: 3a483b9d-627a-41d3-8ac1-66f9c5e89ad5
source-git-commit: 3400df1ecd545aa0fb0e3fcdcc24f629ce4c99ba
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Comércio AEM - Disponibilidade do GDPR{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR e o CCPA.

O Regulamento Geral sobre a Proteção de Dados da União Europeia entra em vigor em maio de 2018. Consulte a [Página do GDPR no Centro de privacidade do Adobe](https://business.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [Disponibilidade do GDPR do AEM](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Com integrações de comércio prontas para uso do Adobe, o AEM é a camada de experiência, consumindo serviços e enviando dados de volta para a plataforma de comércio do cliente, que é executada em um modo headless.

Para algumas plataformas de comércio, o Adobe armazena informações de perfil ( `/home/users`) e tokens de comércio (para fazer logon na plataforma de comércio) no AEM. Para esses casos de uso, leia [Lidar com solicitações do GDPR para a plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Lidar com solicitações do GDPR para o comércio de AEM {#handling-gdpr-requests-for-aem-commerce}

Para a integração do Commerce Cloud do Salesforce, o AEM Commerce não armazena informações relevantes do GDPR. Encaminhe a solicitação para o [Salesforce Cloud](https://documentation.b2c.commercecloud.salesforce.com/DOC1/index.jsp).

Para as integrações do Hybris e do HCL WebSphere® Commerce, há alguns dados no AEM. Use o [Instruções do GDPR da plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considere estas perguntas:

1. **Onde meus dados são armazenados/usados?** Informações de perfil de usuário em cache, como nome, identificador de usuário de comércio, token, senha e dados de endereço, conforme mostrado no AEM.
1. **Com quem devo compartilhar os dados do GDPR cobertos?** Nenhuma atualização de dados relevantes para o GDPR no AEM Commerce é armazenada (exceto as informações de perfil relevantes, como mencionado acima), mas enviada por proxy para a plataforma de comércio.
1. **Como excluir meus dados de usuário**? Exclua o perfil do usuário no AEM e chame a exclusão de usuário na plataforma de comércio.

>[!NOTE]
>
>Dê uma olhada no [hybris wiki](https://wiki.hybris.com/) ou o [Documentação do HCL WebSphere® Commerce](https://help.hcltechsw.com/commerce/index.html), se necessário.
