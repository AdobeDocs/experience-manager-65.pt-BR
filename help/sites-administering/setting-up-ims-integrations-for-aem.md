---
title: Configuração de integrações do IMS para o AEM
description: Saiba como configurar integrações do IMS para o AEM
feature: Security
role: Admin
exl-id: 3c6dbb7e-847f-407b-ac9c-4676dba671a5
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
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
source-wordcount: '504'
ht-degree: 4%
---
# Configuração de integrações do IMS para o AEM {#setting-up-ims-integrations-for-aem}


>[!NOTE]
>
>Os clientes do Adobe usam o [Adobe Developer Console](https://developer.adobe.com/console) para gerar credenciais que habilitam o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. O tipo de credencial Conta de serviço (JWT) agora está obsoleto em favor das credenciais de servidor para servidor OAuth com o Service Pack 20. Esta alteração pode voltar a ser transferida para Service Packs mais antigos, começando com o Service Pack 11 até o Service Pack 20 com o uso de um hotfix que você pode [baixar](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/ims-jwt-compatibility-package-6.5-1.0.zip).

O Adobe Experience Manager (AEM) pode ser integrado a muitas outras soluções da Adobe. Por exemplo, Adobe Target, Adobe Analytics e outros.

As integrações usam uma integração IMS, configurada com S2S OAuth.

* Depois de criar:

  * [Credenciais na Developer Console](#credentials-in-the-developer-console)

* Em seguida, é possível:

  * Criar uma (nova) [configuração do OAuth](#creating-oauth-configuration)

  * [Migrar uma configuração JWT existente para uma configuração OAuth](#migrating-existing-JWT-configuration-to-oauth)

>[!CAUTION]
>
>Anteriormente, as configurações eram feitas com [Credenciais JWT que agora estão sujeitas a desativação no Adobe Developer Console](/help/sites-administering/jwt-credentials-deprecation-in-adobe-developer-console.md).
>
>Essas configurações não podem mais ser criadas ou atualizadas, mas podem ser migradas para configurações OAuth.

## Credenciais na Developer Console {#credentials-in-the-developer-console}

Como primeira etapa, você deve configurar as credenciais do OAuth no Adobe Developer Console.

Para obter detalhes sobre como fazer essa configuração, consulte a documentação do Developer Console, dependendo das suas necessidades:

* Visão geral:

  * [Autenticação de servidor para servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/)

* Criação de uma nova credencial OAuth:

  * [Guia de implementação de credenciais do OAuth de servidor para servidor](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)

* Migrar uma credencial JWT existente para uma credencial OAuth:

  * [Migração da credencial de conta de serviço (JWT) para a credencial de servidor para servidor do OAuth](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration)

Por exemplo:

![Credencial OAuth na Developer Console](assets/ims-configuration-developer-console.png)

## Criação de uma configuração OAuth {#creating-oauth-configuration}

Para criar uma nova Integração do Adobe IMS usando o OAuth:

1. No AEM, navegue até **Ferramentas**, **Segurança**, **Integração do Adobe IMS**.

1. Selecione **Criar**.

1. Conclua a configuração com base nos detalhes da [Developer Console](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation). Por exemplo:

   ![Criar configuração OAuth](assets/ims-create-oauth-configuration.png)

1. **Salve** suas alterações.

## Migração de uma configuração JWT existente para uma configuração OAuth {#migrating-existing-JWT-configuration-to-oauth}

Para migrar uma Integração do Adobe IMS existente com base em credenciais JWT:

>[!NOTE]
>
>Este exemplo mostra uma Configuração IMS do Launch.

1. No AEM, navegue até **Ferramentas**, **Segurança**, **Integração do Adobe IMS**.

1. Selecione a configuração JWT que precisa ser migrada. As configurações JWT estão marcadas com o aviso **Credenciais JWT (obsoletas)**.

1. Selecionar **Propriedades**:

   ![Selecionar configuração JWT](assets/ims-migrate-jwt-select-configuration.png)

1. A configuração é aberta como somente leitura:

   ![Propriedades de Configuração - Somente Leitura](assets/ims-migrate-jwt-properties-read-only.png)

1. Selecione **OAuth** na lista suspensa **Tipo de Autenticação**:

   ![Selecionar tipo de autenticação](assets/ims-migrate-jwt-authentication-type.png)

1. As propriedades disponíveis são atualizadas. Use os detalhes do Developer Console para concluí-los:

   ![Detalhes de OAuth completos](assets/ims-migrate-jwt-complete-oauth-details.png)

1. Use **Salvar e fechar** para manter suas atualizações.
Quando você retornar ao console, o aviso **Credenciais JWT (obsoletas)** desaparecerá.
