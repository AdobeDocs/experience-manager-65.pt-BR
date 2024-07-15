---
title: Descontinuação de credenciais JWT no Adobe Developer Console
description: Saiba mais sobre o impacto da descontinuação de credenciais JWT no Adobe Developer Console no AEM
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: bb4367fa9916a8bafa6255562b2454ddae143351
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# Descontinuação de credenciais JWT no Adobe Developer Console {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> O AEM as a Cloud Service deve consultar [este artigo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) para obter mais informações.

Os clientes do Adobe usam o [Adobe Developer Console](https://developer.adobe.com/console) para gerar credenciais que habilitam o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de Servidor para Servidor do OAuth. As credenciais da Nova conta de serviço (JWT) não podem ser criadas em ou após 3 de junho de 2024, e as credenciais JWT existentes não funcionarão em ou após 27 de janeiro de 2025. Você pode [ler sobre a descontinuação](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artigo fornece algum contexto adicional sobre como os clientes do Adobe Experience Manager (AEM) 6.5 devem lidar com a desativação.

O principal argumento é que o AEM agora oferece suporte às novas credenciais OAuth de servidor para servidor para AEM. Você pode ter recebido um email com instruções para migrar suas credenciais do JWT. Essa migração agora pode ser feita.

As seções abaixo listam os cenários em que os clientes devem (ou em alguns casos não) substituir suas credenciais da Conta de serviço (JWT) por credenciais de Servidor para Servidor OAuth, agora que o AEM oferece suporte a eles. [Leia como](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) migrar as credenciais.

## Integração do AEM a outras soluções da Adobe {#integrating-aem-with-other-adobe-solutions}

**Ação**: migrar sua configuração como AEM agora dá suporte a credenciais OAuth.

**Versões relevantes do AEM**: Adobe Managed Services (Service Pack 21 e superior).

Os clientes de AEM usam o AEM para configurar integrações com todas as outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics e outros.

![Integrando o AEM a outras soluções](/help/sites-administering/assets/jwt-deprecation.png)

Consulte [Configuração de integrações IMS para AEM](/help/sites-administering/setting-up-ims-integrations-for-aem.md) para obter detalhes sobre como:

* criar configurações com credenciais do OAuth
* migrar configurações, que foram criadas com credenciais JWT, para usar credenciais OAuth

## APIs do Cloud Manager {#cloud-manager-apis}

**Ação**: confirme quando é possível migrá-los do JWT para as credenciais do OAuth.

**Versões relevantes do AEM**: Adobe Managed Services (Service Pack 21 e superior).

Os clientes criam projetos do Adobe Developer Console para que possam invocar [APIs do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). As credenciais no projeto do Adobe Developer devem ser migradas para o tipo de credencial servidor para servidor OAuth antes que as credenciais do JWT obsoletas expirem em janeiro de 2025.
