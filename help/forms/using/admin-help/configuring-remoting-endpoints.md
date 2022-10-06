---
title: Configuração de endpoints remotos
seo-title: Configuring Remoting endpoints
description: Saiba como configurar endpoints remotos.
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Configuração de endpoints remotos {#configuring-remoting-endpoints}

Um terminal remoto permite que um aplicativo criado com o Flex chame o serviço usando (obsoleto para formulários AEM) AEM Remoção de formulários. Um terminal remoto é criado automaticamente para cada serviço ativado. Um destino Flex com o mesmo nome do ponto de extremidade é criado e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

## Remoção das configurações de ponto de extremidade {#remoting-endpoint-settings}

**Método de autenticação de cliente Flex:** Determina o tipo de resposta que o servidor envia para o cliente quando o serviço chamado está habilitado para segurança, a operação invocada não oferece suporte a invocações anônimas e o cliente transmite nenhuma ou credenciais inválidas.
