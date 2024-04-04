---
title: Descontinuação de credenciais JWT no console do Adobe Developer
description: Saiba mais sobre o impacto da descontinuação de credenciais JWT no Console do Adobe Developer no AEM
exl-id: f19a92de-ba6a-4f6d-9e12-60ad1bad2e74
solution: Experience Manager, Experience Manager Sites
source-git-commit: dec88af3b2345d142d0cc3bc27cfbc27804ab57e
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# Descontinuação de credenciais JWT no console do Adobe Developer {#jwt-credentials-deprecation-in-adobe-developer-console}

>[!NOTE]
> O AEM as a Cloud Service deve fazer referência [este artigo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console.html) para obter mais informações.

Clientes do Adobe usam [Console do Adobe Developer](https://developer.adobe.com/console) para gerar credenciais que permitem o acesso a várias APIs. Os clientes selecionam entre vários tipos de credenciais, que variam de servidor para servidor do OAuth a aplicativo de página única. Um desses tipos de credenciais, as credenciais da Conta de serviço (JWT), foi descontinuado em favor das credenciais de Servidor para Servidor do OAuth. As credenciais da Nova conta de serviço (JWT) não podem ser criadas em ou após 3 de junho de 2024, e as credenciais JWT existentes não funcionarão em ou após 27 de janeiro de 2025. Você pode [leia sobre a descontinuação](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/).

Este artigo fornece contexto adicional sobre como os clientes do AEM 6.5 devem lidar com a desativação.

O principal argumento neste momento é que os recursos de AEM ainda não oferecem suporte às novas credenciais de servidor para servidor do OAuth. O suporte será fornecido em breve — até o final de abril de 2024, por meio de um pacote de compatibilidade especial para instalação do AEM 6.5, se você estiver executando o Service Pack 20 ou inferior mais recente (o Service Pack 21 e superior o incluirá automaticamente). Você pode ter recebido um email com instruções para migrar suas credenciais do JWT, mas tenha certeza de que pode e deve adiar a migração das credenciais até que o AEM ofereça suporte ao novo tipo de credencial servidor para servidor OAuth.

As seções abaixo listam os cenários em que os clientes devem (ou, em alguns casos, não) substituir suas credenciais da Conta de serviço (JWT) por credenciais de Servidor para Servidor OAuth, uma vez que o AEM ofereça suporte a eles no final de abril. [Saiba como](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) para substituir as credenciais no futuro.

## Integração do AEM a outras soluções da Adobe {#integrating-aem-with-other-adobe-solutions}

**Ação**: aguarde até depois do final de abril de 2024, quando o AEM permitir a migração.

**Versões relevantes do AEM**: Adobe Managed Services (Service Pack 20 e inferior).


Os clientes do AEM usam a interface do autor do AEM para configurar integrações com todas as outras soluções de Adobe. Por exemplo, Adobe Target, Adobe Analytics, Adobe Launch, AFCS e muito mais.

![Integração do AEM a outras soluções](/help/sites-administering/assets/jwt-deprecation.png)

Como exemplo, aqui estão [as instruções](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html?lang=en) para configurar a integração com o Adobe Target. A chave de API na variável [Concluir a configuração do IMS no AEM](https://docs.mktossl.com/docs/experience-manager-cloud-service/content/sites/integrations/integration-adobe-target-ims.html#completing-the-ims-configuration-in-aem) A seção deve ser migrada para o tipo de credencial servidor para servidor OAuth, assim que o AEM oferecer suporte a essas credenciais no final de abril. Essas instruções serão atualizadas e revisadas no final de abril para ajudar você a aplicar as novas credenciais de servidor para servidor do OAuth.

## APIs do Cloud Manager {#cloud-manager-apis}

**Ação**: aguarde até depois do final de abril de 2024, quando o AEM permitir a migração.

**Versões relevantes do AEM**: Adobe Managed Services (Service Pack 20 e inferior).

Os clientes criam projetos do Adobe Developer Console para que possam invocar [APIs do Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/guides/getting-started/create-api-integration/). As credenciais no projeto do Adobe Developer devem ser migradas para o tipo de credencial de servidor para servidor OAuth, depois que o AEM e o Cloud Manager forem compatíveis.
