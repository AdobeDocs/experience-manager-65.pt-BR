---
title: Configuração do para aplicativos AEM
description: Saiba como usar os aplicativos Adobe Experience Manager para atualizar o conteúdo do OTA do seu aplicativo (no ar).
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
exl-id: f7aa5ac0-3d03-4c04-b9c2-1bda427b0588
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 523b1ccd-901e-5e3b-9fa7-f3dfd82463d5
    internal-label: Configuring
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%
---
# Configuração do para aplicativos AEM{#configuring-for-aem-apps}

O Adobe Experience Manager Apps permite atualizar o conteúdo do OTA do seu aplicativo (no ar). O conteúdo atualizado é armazenado na instância de publicação. Para permitir que o aplicativo no dispositivo se conecte à instância de publicação e verifique se há atualizações, a instância de publicação deve ser configurada para permitir um cabeçalho de referenciador vazio.

## Configurar cabeçalho de referenciador vazio {#configuring-empty-referrer-header}

Para configurar o serviço de filtro de referenciador:

* Abra o console Apache Felix (**Configurações**) em:
* https://<server>:<port_number>/system/console/configMgr
* Faça logon como administrador.
* No menu **Configurações**, selecione: *Filtro de referenciador Apache Sling*
* Marque o campo Permitir vazio para permitir cabeçalhos de referenciador vazios/ausentes.
* Clique em **Salvar** para salvar as alterações.

![chlimage_1-58](assets/chlimage_1-58a.png)

Consulte as [Configurações OSGI](/help/sites-deploying/osgi-configuration-settings.md) e a [Lista de Verificação de Segurança - Problemas com Falsificação de Solicitação Entre Sites](/help/sites-administering/security-checklist.md#protect-against-cross-site-request-forgery) para obter mais detalhes.
