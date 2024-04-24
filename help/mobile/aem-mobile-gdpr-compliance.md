---
title: Adobe Experience Manager Mobile - Disponibilidade do GDPR
description: Saiba mais sobre como o Adobe Experience Manager está pronto para ajudá-lo com suas obrigações de conformidade com o GDPR.
contentOwner: trushton
exl-id: d06e675f-fb61-47da-85de-e0b50dd44153
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 0%

---

# AEM Mobile - Disponibilidade do GDPR {#aem-mobile-gdpr-readiness}

>[!IMPORTANT]
>
>O GDPR é usado como exemplo nas seções abaixo, mas os detalhes abordados se aplicam a todas as regulamentações de proteção e privacidade de dados; como o GDPR e o CCPA.

## Suporte ao GDPR da AEM Mobile {#aem-mobile-gdpr-support}

A AEM Mobile está pronta para ajudar os clientes com suas obrigações de conformidade com o GDPR. Nenhum dado pessoal é armazenado no AEM Mobile. Se você tiver sido provisionado, poderá fazer logon no Adobe Experience Mobile com sua Adobe ID.

<!-- [https://aemmobile.adobe.com/signin/index.html](https://aemmobile.adobe.com/signin/index.html) -->

## Adobe Digital Publishing Suite {#adobe-digital-publishing-suite}

O produto de publicação digital do Adobe (que precede o AEM Mobile) é compatível com as iniciativas de preparação do GDPR do Adobe. Consulte [https://business.adobe.com/privacy/general-data-protection-regulation.html](https://business.adobe.com/privacy/general-data-protection-regulation.html). A seguir são fornecidos detalhes específicos sobre o suporte a funções relevantes do GDPR no produto do Digital Publishing Suite, incluindo como trabalhar com o Adobe para iniciar solicitações do GDPR.

Para não confundir o AEM Mobile com o produto mais antigo do Digital Publishing Suite, é possível fazer logon no produto do Digital Publishing Suite aqui:

[https://acrobat.adobe.com/us/en/](https://acrobat.adobe.com/us/en/)

### Iniciando uma solicitação do GDPR {#initiating-a-gdpr-request}

Entre em contato com o Atendimento ao cliente do Adobe para que você possa iniciar uma solicitação de GDPR para a Digital Publishing Suite.

As seguintes IDs são necessárias para localizar dados do cliente. Qualquer subconjunto recebido implica que as outras IDs não eram aplicáveis a esse usuário.

Obrigatório:

* ID do contrato do cliente: *dpsc-contractId*

Forneça pelo menos 1 dos seguintes itens:

* ID do OAuth fornecida pelo cliente do usuário final (a ID usada no sistema de direito direto do cliente): *dpsc-directEntitlementId*
* Para usuários de aplicativos Windows, a App Store ID do usuário final: *dpsc-windowsAppStoreId*
* O endereço de email que o usuário final usou para interagir com o aplicativo da DPS: *email*

### Perguntas frequentes {#frequently-asked-questions-faq}

**O Adobe exclui minhas compras do App Store ao iniciar uma solicitação DELETE?**

O Adobe exclui informações que tem de compras da App Store (assinaturas e assim por diante), mas as compras ainda estão registradas nas App Store. Se o aplicativo (usuário final) estiver conectado à App Store, esses recibos serão coletados novamente e enviados ao Adobe. Posteriormente, elas são consideradas novas compras e são restauradas pelo aplicativo, com acesso novamente.

**O Adobe está excluindo os direitos fornecidos pelo cliente ao iniciar uma solicitação DELETE?**

O Adobe exclui informações que possui sobre as bonificações diretas adicionais do cliente. Se o aplicativo (usuário final) fizer logon no mecanismo OAuth usado pelo cliente, ele enviará informações para o Adobe e os serviços coletarão os direitos adicionais novamente.

**O que se espera do usuário final?**

Como a chave para atribuir direitos ao aplicativo reside no dispositivo como parte do software do visualizador, o usuário final deve desinstalar o aplicativo. O usuário final deve perceber que, se reinstalar o aplicativo, as compras existentes (associadas ao usuário da App Store) e os subsídios de direito direto (associados ao usuário OAuth do cliente) ainda serão restaurados.

**O que acontece quando um aplicativo é compartilhado entre pessoas em um dispositivo?**

O Adobe tem o mínimo de informações associadas diretamente a um usuário específico. Ele associa os dados usando uma UUID criada aleatoriamente que é mantida nos dados do aplicativo e é transmitida em cada solicitação iniciada pelo aplicativo. Isso significa que os usuários finais que compartilham o aplicativo no mesmo dispositivo usam a mesma UUID e todos os dados são considerados de propriedade da pessoa que faz a solicitação de GDPR. Tanto para as solicitações de acesso quanto para as de exclusão, o DPSC considera as pessoas que compartilham um aplicativo como uma única pessoa.

**Quais dados pessoais são rastreados com o Analytics?**

Nenhum. Há dados sendo rastreados, mas no nível do aplicativo (não pessoal). Isso inclui eventos como inicializações, falhas, fechamentos, atividades, compras ou sobreposições de fólio. Os locais geográficos, nomes, IDs de dispositivo ou endereços IP não são rastreados.

**O usuário final forneceu suas informações, mas nada foi encontrado. Por que não?**

À medida que o produto da Digital Publishing Suite evoluía, as implementações de serviço eram alteradas e mais dados eram ofuscados. Se nenhum dado for encontrado usando os dados fornecidos pelo usuário, significa que os dados do usuário não poderão ser rastreados até essa pessoa.

### Exemplo {#example}

Entre em contato com o Atendimento ao cliente do Adobe para iniciar uma solicitação de GDPR.

Este é um exemplo das entradas e saídas resultantes de uma solicitação do GDPR do Digital Publishing Suite:

#### Entradas: {#inputs}

```
dpsc-contractId = "12345-1234-12416234" 
directEntitlementId = "1234-1234-1234" 
windowsAppStoreId = "testWinAppStoreId" 
email = "test@what.com"
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
