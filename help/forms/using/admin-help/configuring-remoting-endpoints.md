---
title: Configuração de pontos de extremidade Remotos
description: Saiba como configurar pontos de extremidade remotos. Este documento explica como habilitar o aplicativo criado com o Flex para chamar o serviço usando o AEM forms Remoting.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---

# Configuração de pontos de extremidade Remotos {#configuring-remoting-endpoints}

Um endpoint de comunicação remota permite que um aplicativo criado com o Flex chame o serviço usando o AEM forms Remoting (Desaprovado para formulários AEM). Um ponto de extremidade remoto é criado automaticamente para cada serviço ativado. Um destino do Flex que tem o mesmo nome do endpoint é criado, e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

## Configurações de ponto de extremidade de comunicação remota {#remoting-endpoint-settings}

**Método de autenticação de cliente Flex:** Determina o tipo de resposta que o servidor envia de volta ao cliente quando o serviço chamado está habilitado para segurança, a operação chamada não dá suporte a invocações anônimas e o cliente passa credenciais inválidas ou nenhuma.
