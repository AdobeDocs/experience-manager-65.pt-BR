---
title: AEM Mobile - Prontidão para o RGPD
seo-title: AEM Mobile - Prontidão para o RGPD
description: 'null'
seo-description: nulo
uuid: 817c434f-4b78-40f7-99d6-6efafdedb77e
contentOwner: trushton
discoiquuid: 9399dd3d-a485-4f53-a6f2-7b190da4235b
translation-type: tm+mt
source-git-commit: 85a3dac5db940b81da9e74902a6aa475ec8f1780
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 1%

---


# AEM Mobile - Disponibilidade do GDPR {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>O RGPD é utilizado como exemplo nas seções abaixo, mas os detalhes abrangidos são aplicáveis a todas as normas de proteção de dados e privacidade; como o RGPD, o CCPA, etc.

## Suporte ao AEM Mobile GDPR {#aem-mobile-gdpr-support}

A AEM Mobile está pronta para ajudar os clientes com suas obrigações de conformidade com o RGPD. Nenhum dado pessoal é armazenado no AEM Mobile. Se você estiver provisionado, poderá fazer logon no Adobe Experience Mobile com seu Adobe ID.

[https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html)

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

O produto de publicação digital do Adobe (que precede o AEM Mobile) suporta as iniciativas de preparação para o RGPD do Adobe. Consulte [https://www.adobe.com/privacy/general-data-protection-regulation.html](https://www.adobe.com/privacy/general-data-protection-regulation.html). As informações a seguir fornecerão especificações sobre o suporte para funções relevantes do RGPD no produto Digital Publishing Suite, incluindo como trabalhar com o Adobe para iniciar solicitações do RGPD.

Para garantir que você não esteja confundindo a AEM Mobile com o produto mais antigo da Digital Publishing Suite, faça logon no produto da Digital Publishing Suite aqui:

[https://digitalpublishing.acrobat.com/welcome.html](https://digitalpublishing.acrobat.com/welcome.html)

### Iniciando uma solicitação do RGPD {#initiating-a-gdpr-request}

Entre em contato com o Atendimento ao cliente da Adobe para iniciar uma solicitação de RGPD para a Digital Publishing Suite.

As seguintes IDs são necessárias para localizar os dados do cliente. Qualquer subconjunto recebido incluirá as outras IDs que não se aplicam a este usuário.

Obrigatório:

* ID do contrato do cliente: *dpsc-ContractId*

Forneça pelo menos um dos seguintes:

* A ID OAuth fornecida pelo cliente final (a ID usada no sistema de direito direto do cliente): *dpsc-directEntitlementId*
* Para usuários de aplicativos do Windows, a ID da App Store do usuário final: *dpsc-windowsAppStoreId*
* O endereço de email que o usuário final usou para interagir com o aplicativo DPS: *email*

### Perguntas frequentes (FAQ) {#frequently-asked-questions-faq}

**A Adobe excluirá minhas compras da App Store ao iniciar uma solicitação de DELETE?**

O Adobe excluirá as informações que possui sobre compras na App Store (subscrição etc.) mas as compras ainda estarão gravadas nas App Stores. Se o aplicativo (usuário final) estiver conectado à App Store, esses recebimentos serão coletados novamente e enviados à Adobe e, subsequentemente, serão considerados como novas compras e restaurados pelo aplicativo para terem acesso novamente.

**A Adobe excluirá os direitos fornecidos pelo cliente ao iniciar uma solicitação de DELETE?**

O Adobe excluirá as informações que possui sobre as licenças de direito direto adicionais do cliente. Se o aplicativo (usuário final) fizer logon no mecanismo OAuth usado pelo cliente, ele enviará informações para a Adobe e os serviços coletarão os direitos extras novamente.

**O que é esperado do usuário final?**

Como a chave para atribuir direitos ao aplicativo reside no dispositivo como parte do software do visualizador, o usuário final deve desinstalar o aplicativo. O usuário final deve perceber que, se reinstalar o aplicativo, as compras existentes (associadas ao usuário da App Store) e as licenças de direito direto (associadas ao usuário OAuth do cliente) ainda serão restauradas.

**O que acontece quando um aplicativo é compartilhado entre pessoas em um dispositivo?**

Adobe tem muito pouca informação que associa diretamente a um usuário específico. Ela associa os dados usando uma UUID criada aleatoriamente, que é mantida nos dados do aplicativo e transmitida em cada solicitação que o aplicativo inicia. Isso significa que os usuários finais que compartilham o aplicativo no mesmo dispositivo usarão a mesma UUID e todos os dados serão considerados de propriedade da pessoa que faz a solicitação do RGPD. Para solicitações de acesso e exclusão, o DPSC considerará as pessoas que compartilham um aplicativo como uma pessoa.

**Quais dados pessoais são rastreados pelo Analytics?**

Nenhum. Há dados sendo rastreados, mas estão no nível do aplicativo (não pessoais). Isso inclui eventos como inicializações, falhas, fechamento, atividades, compras ou sobreposições de fólio. Locais geográficos, nomes, IDs de dispositivo ou endereços IP não são rastreados.

**O usuário final forneceu suas informações, mas nada foi encontrado. Por que não?**

À medida que o produto da Digital Publishing Suite evoluía, as implementações de serviço eram alteradas e mais dados eram ofuscados. Se nenhum dado foi encontrado usando os dados fornecidos pelo usuário, isso significa que os dados do usuário não podem ser rastreados até essa pessoa.

### Exemplo {#example}

Entre em contato com o Atendimento ao cliente da Adobe para iniciar uma solicitação de RGPD.

Veja um exemplo das entradas e saídas resultantes de uma solicitação de RGPD da Digital Publishing Suite:

#### Entradas: {#inputs}

```
dpsc-contractId = “12345-1234-12416234” 
directEntitlementId = “1234-1234-1234” 
windowsAppStoreId = “testWinAppStoreId” 
email = “test@what.com”
```

#### Saídas {#outputs}

```
{

    "jobId": "test-1524750204384",

    "product": "DPSC",

    "action": "access",

    "userIDS": [

        {

        "namespace": "email",

        "value": "test@what.com"

        },

        {

        "namespace": "windowsAppStoreId",

        "value": "testWinAppStoreId"

        },

        {

        "namespace": "directEntitlementId",

        "value": "1234-1234-1234"

        }

    ],

    "receiptData": {

    "recordsFound": 6,

    "recordsAffected": 0,

    "tablesModified": 0,

    "subscriptionsFound": 24,

    "entitlementsFound": 24

    },

    "records": {

        "DPS_Stage_EntitlementUserDevices": [

        {

            "user_id": "testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "device_id": "appleStore:test1b16-f032-4d9c-9200-0d19999405c4",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test967d-5179-4dc6-958c-facd9d94da38",

            "device_id": "appleStore:test3f07-d5aa-4b32-8fac-b2b690b7ccd7",

            "account_id": "test@what.com"

        },

        {

            "user_id": "test1838-6494-4e74-912c-1edf61581d0e",

            "device_id": "appleStore:test3813-f8cc-49ce-b021-50eb0814a3bb",

            "account_id": "1234-1234-1234"

        },

        {

            "user_id": "test5468-1a11-4e4c-be43-274181a9ef81",

            "device_id": "appleStore:testf082-2783-498d-ab62-b1b2e3eb67ae",

            "account_id": "1234-1234-1234"

        }

        ],

            "DPS_Stage_EntitlementUsers": [

        {

            "id": "store:test04a7-33a3-4b90-863d-79981ead0f19:appleStore",

            "part_id": "0",

            "alias_user_id": "testWinAppStoreId"

        },

        {

            "id": "internal:testd2da-0606-4444-87ef-0d5a1d4a121d:adobe",

            "part_id": "0",

            "user_id": "test@what.com"

        }

        ],

            "DPS_Stage_Subscriptions": [

        {

            "id": "appleStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test3531-a209-4391-beb9-951c7822244e",

            "overflow": "test4e59-86a8-4b75-b699-77e980c287ab",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "test491b-379e-4d24-96ef-e481bf8d3062",

            "overflow": "test931b-7422-485d-85a5-134828187b6c",

            "entitlement_count": "12"

        }

        ],

            "DPS_Stage_Entitlements": [

        {

            "id": "samsungStore:testc685-c9ca-4c1e-a11b-07d10ec724cf",

            "account_id": "test7332-60a0-42b8-a508-474668d83d2e",

            "overflow": "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "entitlement_count": "12"

        },

        {

            "id": "appleStore:test5468-1a11-4e4c-be43-274181a9ef81",

            "account_id": "testf766-102a-460d-8f5a-42f7bb9d68b7",

            "overflow": "test4d96-2197-45a8-9caf-2aa2846b770c",

            "entitlement_count": "12"

        }

        ],

            "s3Buckets": {

            "name": "DPS-Entitlements-Overflow",

            "folder": "stage/",

            "overflows": {

            "subscriptions": [

            "test4e59-86a8-4b75-b699-77e980c287ab",

            "test931b-7422-485d-85a5-134828187b6c"

        ],

            "entitlements": [

            "test9bc3-94d0-43cf-b132-0629868f7d9d",

            "test4d96-2197-45a8-9caf-2aa2846b770c"

                ]

            }

        }

    }

}
```

