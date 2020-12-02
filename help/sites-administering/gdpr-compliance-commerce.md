---
title: Comércio AEM - Prontidão para o RGPD
seo-title: Comércio AEM - Prontidão para o RGPD
description: 'null'
seo-description: nulo
uuid: 7ca26587-8cce-4c75-8629-e0e5cfb8166c
contentOwner: carlino
discoiquuid: c637964a-dfcb-41fe-9c92-934620fe2cb3
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Comércio AEM - Preparação para o RGPD{#aem-commerce-gdpr-readiness}

>[!IMPORTANT]
>
>O RGPD é utilizado como exemplo nas seções abaixo, mas os detalhes abrangidos são aplicáveis a todas as normas de proteção de dados e privacidade; como o RGPD, o CCPA, etc.

O Regulamento Geral da Proteção de Dados da União sobre os direitos de privacidade dos dados entra em vigor em maio de 2018. Para obter mais informações, consulte a página [RGPD no Centro de Privacidade do Adobe](https://www.adobe.com/privacy/general-data-protection-regulation.html).

>[!NOTE]
>
>Consulte [AEM Prontidão do RGPD](/help/managing/data-protection-and-privacy.md) para obter mais detalhes.

![screen_shot_2018-03-22at111606](assets/screen_shot_2018-03-22at111606.jpg)

Em nossas integrações de Comércio prontas para uso, AEM é a camada de experiência, consumindo serviços e enviando dados de volta para a plataforma de comércio do cliente que é executada em um modo sem cabeçalho.

Para algumas plataformas de comércio, armazenamos informações do perfil ( `/home/users`) e tokens de comércio (para fazer logon na plataforma de comércio) no AEM. Para estes casos de uso, leia [Processando Solicitações GDPR para a Plataforma AEM](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md).

![screen_shot_2018-03-22at111621](assets/screen_shot_2018-03-22at111621.jpg)

## Tratamento de solicitações GDPR para comércio AEM {#handling-gdpr-requests-for-aem-commerce}

Para a integração com o Commerce Cloud Salesforces, o AEM Commerce não armazena informações relevantes do RGPD. Você deve encaminhar a solicitação para [Salesforce Cloud](https://documentation.demandware.com/).

Para as integrações hybris e IBM WebSphere, há alguns dados em AEM. Você deve usar as [AEM instruções GDPR da plataforma](/help/sites-administering/handling-gdpr-requests-for-aem-platform.md) e considerar estas questões:

1. **Onde meus dados são armazenados/usados?** As informações de perfil do usuário em cache, como nome, identificador do usuário de comércio, token, senha, dados de endereço e assim por diante, são exibidas AEM.
1. **Com quem compartilho os dados do RGPD cobertos?** Qualquer atualização dos dados relevantes do RGPD no AEM Commerce não é armazenada (exceto as informações relevantes do perfil, como mencionado acima), mas é enviada de volta à plataforma de comércio.
1. **Como excluir meus dados** do usuário? Exclua o perfil do usuário no AEM e chame a exclusão do usuário na plataforma de comércio.

>[!NOTE]
>
>Veja a [hybris wiki](https://wiki.hybris.com/) ou a [documentação do Webphere Commerce](https://www-01.ibm.com/support/docview.wss?uid=swg27036450), se necessário.

