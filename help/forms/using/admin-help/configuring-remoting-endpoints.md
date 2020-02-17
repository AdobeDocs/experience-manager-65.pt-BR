---
title: Configurando pontos finais remotos
seo-title: Configurando pontos finais remotos
description: Saiba como configurar pontos de extremidade remotos.
seo-description: Saiba como configurar pontos de extremidade remotos.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configurando pontos finais remotos {#configuring-remoting-endpoints}

Um terminal remoto permite que um aplicativo criado com o Flex chame o serviço usando formulários AEM Remoting (obsoletos para formulários AEM). Um terminal remoto é criado automaticamente para cada serviço ativado. Um destino Flex com o mesmo nome do ponto de extremidade é criado e os clientes Flex podem criar objetos remotos que apontam para esse destino para chamar operações no serviço relevante.

## Configurações de ponto de extremidade remoto {#remoting-endpoint-settings}

**** Método de autenticação de cliente Flex: Determina o tipo de resposta que o servidor envia para o cliente quando o serviço chamado está habilitado para segurança, a operação invocada não suporta invocações anônimas e o cliente transmite nenhuma credenciais ou inválidas.
